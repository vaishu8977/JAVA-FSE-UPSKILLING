//Exercise 21: Custom Exception
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class AgeValidator {
    public static void main(String[] args) {
        int age = 15;
        try {
            if (age < 18)
                throw new InvalidAgeException("Not eligible to vote");
            else
                System.out.println("Eligible to vote");
        } catch (InvalidAgeException e) {
            System.out.println("Caught Exception: " + e.getMessage());
        }
    }
}

//Exercise 22: File Writing
import java.io.*;
import java.util.Scanner;

public class FileWriteExample {
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter text to write to file: ");
        String text = sc.nextLine();

        BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
        writer.write(text);
        writer.close();

        System.out.println("Data written to output.txt successfully.");
    }
}

//Exercise 23: File Reading
import java.io.*;

public class FileReadExample {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new FileReader("output.txt"));
        String line;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        reader.close();
    }
}

//Exercise 24: ArrayList Example
import java.util.ArrayList;
import java.util.Scanner;

public class StudentList {
    public static void main(String[] args) {
        ArrayList<String> students = new ArrayList<>();
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter student names (type 'end' to stop):");
        while (true) {
            String name = sc.nextLine();
            if (name.equalsIgnoreCase("end")) break;
            students.add(name);
        }

        System.out.println("Student Names:");
        for (String s : students) {
            System.out.println(s);
        }
    }
}

//Exercise 25: HashMap Example
import java.util.*;

public class StudentMap {
    public static void main(String[] args) {
        HashMap<Integer, String> students = new HashMap<>();
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter student ID and name (type -1 to stop):");
        while (true) {
            System.out.print("ID: ");
            int id = sc.nextInt();
            if (id == -1) break;
            sc.nextLine(); // consume newline
            System.out.print("Name: ");
            String name = sc.nextLine();
            students.put(id, name);
        }

        System.out.print("Enter ID to lookup: ");
        int lookupId = sc.nextInt();
        System.out.println("Student: " + students.getOrDefault(lookupId, "Not Found"));
    }
}

//Exercise 26: Thread Creation
class MyThread extends Thread {
    public void run() {
        System.out.println("Running in " + Thread.currentThread().getName());
    }

    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        t1.start();
        t2.start();
    }
}

//Exercise 27: Lambda Expressions
import java.util.*;

public class LambdaSort {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Alice", "Bob", "David");
        Collections.sort(names, (a, b) -> a.compareToIgnoreCase(b));
        names.forEach(System.out::println);
    }
}

//Exercise 28: Stream API
import java.util.*;
import java.util.stream.Collectors;

public class StreamFilter {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(10, 15, 20, 25, 30);
        List<Integer> even = numbers.stream()
                .filter(n -> n % 2 == 0)
                .collect(Collectors.toList());

        even.forEach(System.out::println);
    }
}

//Exercise 29: Records
record Person(String name, int age) {}

import java.util.*;

public class RecordExample {
    public static void main(String[] args) {
        List<Person> people = List.of(
            new Person("Alice", 22),
            new Person("Bob", 30),
            new Person("Eve", 18)
        );

        people.stream()
              .filter(p -> p.age() >= 21)
              .forEach(System.out::println);
    }
}

//Exercise 30: Pattern Matching for switch (Java 21)
public class PatternSwitch {
    public static void checkType(Object obj) {
        switch (obj) {
            case String s -> System.out.println("String: " + s);
            case Integer i -> System.out.println("Integer: " + i);
            case Double d -> System.out.println("Double: " + d);
            default -> System.out.println("Unknown type");
        }
    }

    public static void main(String[] args) {
        checkType("Hello");
        checkType(123);
        checkType(3.14);
    }
}

//Exercise 31: Basic JDBC Connection
import java.sql.*;

public class JDBCConnect {
    public static void main(String[] args) {
        try {
            Connection conn = DriverManager.getConnection("jdbc:sqlite:students.db");
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            while (rs.next()) {
                System.out.println(rs.getInt("id") + ": " + rs.getString("name"));
            }

            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

//Exercise 32: Insert and Update Operations in JDBC
import java.sql.*;

public class StudentDAO {
    Connection conn;

    StudentDAO() throws SQLException {
        conn = DriverManager.getConnection("jdbc:sqlite:students.db");
    }

    void insertStudent(int id, String name) throws SQLException {
        PreparedStatement ps = conn.prepareStatement("INSERT INTO students (id, name) VALUES (?, ?)");
        ps.setInt(1, id);
        ps.setString(2, name);
        ps.executeUpdate();
    }

    void updateStudent(int id, String name) throws SQLException {
        PreparedStatement ps = conn.prepareStatement("UPDATE students SET name=? WHERE id=?");
        ps.setString(1, name);
        ps.setInt(2, id);
        ps.executeUpdate();
    }
}

// Exercise 33: Transaction Handling in JDBC
import java.sql.*;

public class BankTransfer {
    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection("jdbc:sqlite:bank.db")) {
            conn.setAutoCommit(false);

            Statement stmt = conn.createStatement();
            stmt.executeUpdate("UPDATE accounts SET balance = balance - 100 WHERE id = 1");
            stmt.executeUpdate("UPDATE accounts SET balance = balance + 100 WHERE id = 2");

            conn.commit();
            System.out.println("Transaction successful");

        } catch (SQLException e) {
            System.out.println("Transaction failed: " + e.getMessage());
        }
    }
}

//Exercise 34: Create and Use Java Modules
module-info.java in com.utils:
module com.utils {
    exports com.utils;
}

module-info.java in com.greetings:
module com.greetings {
    requires com.utils;
}

//Exercise 35: TCP Client-Server Chat
Server:
import java.net.*;
import java.io.*;

public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket server = new ServerSocket(1234);
        Socket socket = server.accept();

        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

        out.println("Hello client!");
        System.out.println("Client: " + in.readLine());

        socket.close();
        server.close();
    }
}

Client:
import java.net.*;
import java.io.*;

public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 1234);

        BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

        System.out.println("Server: " + in.readLine());
        out.println("Hello server!");

        socket.close();
    }
}

//Exercise 36: HTTP Client API (Java 11+)
import java.net.http.*;
import java.net.URI;
import java.io.IOException;

public class HttpExample {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.github.com"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println("Status: " + response.statusCode());
        System.out.println("Body: " + response.body());
    }
}

//Exercise 37: Using javap to Inspect Bytecode
Demo.java:
public class Demo {
    public static int square(int x) {
        return x * x;
    }

    public static void main(String[] args) {
        System.out.println(square(5));
    }
}

Command to Compile and Inspect:
javac Demo.java
javap -c Demo

Sample Output (bytecode):
Compiled from "Demo.java"
public class Demo {
  public Demo();
    Code:
       0: aload_0
       1: invokespecial #1                  // Method java/lang/Object."<init>":()V
       4: return

  public static int square(int);
    Code:
       0: iload_0
       1: iload_0
       2: imul
       3: ireturn

  public static void main(java.lang.String[]);
    Code:
       0: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
       3: iconst_5
       4: invokestatic  #3                  // Method square:(I)I
       7: invokevirtual #4                  // Method java/io/PrintStream.println:(I)V
      10: return
}

//Exercise 38: Decompile a Class File
Steps:
Write a simple program like:
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
Compile:
javac Hello.java
Use a decompiler like:
JD-GUI
CFR
Sample CFR usage:
sh
Copy
Edit
java -jar cfr.jar Hello.class

// Exercise 39: Reflection in Java
import java.lang.reflect.*;
public class ReflectionDemo {
    public static void main(String[] args) throws Exception {
        Class<?> cls = Class.forName("java.lang.String");
        Method[] methods = cls.getDeclaredMethods();
        for (Method m : methods) {
            System.out.println(m.getName());
        }
    }
}

//Exercise 40: Virtual Threads (Java 21)
public class VirtualThreads {
    public static void main(String[] args) {
        for (int i = 0; i < 100_000; i++) {
            Thread.startVirtualThread(() -> System.out.println("Running virtual thread"));
        }
    }
}

//Exercise 41: ExecutorService and Callable
import java.util.concurrent.*;
import java.util.*;

public class CallableExample {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        List<Callable<String>> tasks = List.of(
            () -> "Task 1",
            () -> "Task 2",
            () -> "Task 3"
        );

        List<Future<String>> results = executor.invokeAll(tasks);
        for (Future<String> result : results) {
            System.out.println(result.get());
        }

        executor.shutdown();
    }
}