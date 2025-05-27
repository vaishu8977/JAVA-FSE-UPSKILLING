// Exercise 1: Hello World
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}

// Exercise 2: Simple Calculator
import java.util.Scanner;
public class Calculator {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter first number: ");
        double a = sc.nextDouble();
        System.out.print("Enter second number: ");
        double b = sc.nextDouble();
        System.out.print("Choose operation (+ - * /): ");
        char op = sc.next().charAt(0);
        double result = 0;
        switch (op) {
            case '+': result = a + b; break;
            case '-': result = a - b; break;
            case '*': result = a * b; break;
            case '/': result = b != 0 ? a / b : Double.NaN; break;
            default: System.out.println("Invalid operator"); return;
        }
        System.out.println("Result: " + result);
    }
}

// Exercise 3: Even or Odd Checker
import java.util.Scanner;
public class EvenOdd {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter an integer: ");
        int num = sc.nextInt();
        System.out.println(num % 2 == 0 ? "Even" : "Odd");
    }
}

// Exercise 4: Leap Year Checker
import java.util.Scanner;
public class LeapYear {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a year: ");
        int year = sc.nextInt();
        boolean leap = (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
        System.out.println(leap ? "Leap Year" : "Not a Leap Year");
    }
}

// Exercise 5: Multiplication Table
import java.util.Scanner;
public class MultiplicationTable {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int num = sc.nextInt();
        for (int i = 1; i <= 10; i++) {
            System.out.println(num + " x " + i + " = " + (num * i));
        }
    }
}

// Exercise 6: Data Type Demonstration
public class DataTypes {
    public static void main(String[] args) {
        int i = 10;
        float f = 3.14f;
        double d = 3.14159;
        char c = 'A';
        boolean b = true;
        System.out.println("int: " + i);
        System.out.println("float: " + f);
        System.out.println("double: " + d);
        System.out.println("char: " + c);
        System.out.println("boolean: " + b);
    }
}

// Exercise 7: Type Casting
public class TypeCasting {
    public static void main(String[] args) {
        double d = 9.99;
        int i = (int) d;
        System.out.println("Double to int: " + i);
        int j = 7;
        double dj = j;
        System.out.println("Int to double: " + dj);
    }
}

// Exercise 8: Operator Precedence
public class OperatorPrecedence {
    public static void main(String[] args) {
        int result = 10 + 5 * 2;
        System.out.println("Result: " + result);
    }
}

// Exercise 9: Grade Calculator
import java.util.Scanner;
public class GradeCalculator {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter marks (0-100): ");
        int marks = sc.nextInt();
        char grade = marks >= 90 ? 'A' : marks >= 80 ? 'B' : marks >= 70 ? 'C' : marks >= 60 ? 'D' : 'F';
        System.out.println("Grade: " + grade);
    }
}

// Exercise 10: Number Guessing Game
import java.util.*;
public class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Random rand = new Random();
        int target = rand.nextInt(100) + 1, guess;
        do {
            System.out.print("Guess the number (1-100): ");
            guess = sc.nextInt();
            if (guess < target) System.out.println("Too low");
            else if (guess > target) System.out.println("Too high");
            else System.out.println("Correct!");
        } while (guess != target);
    }
}

// Exercise 11: Factorial Calculator
import java.util.Scanner;
public class Factorial {
    public static int factorial(int n) {
        return (n == 0) ? 1 : n * factorial(n - 1);
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int num = sc.nextInt();
        System.out.println("Factorial: " + factorial(num));
    }
}

// Exercise 12: Method Overloading
public class MethodOverload {
    static int add(int a, int b) {
        return a + b;
    }
    static double add(double a, double b) {
        return a + b;
    }
    static int add(int a, int b, int c) {
        return a + b + c;
    }
    public static void main(String[] args) {
        System.out.println(add(2, 3));
        System.out.println(add(2.5, 3.5));
        System.out.println(add(1, 2, 3));
    }
}

// Exercise 13: Recursive Fibonacci
import java.util.Scanner;
public class FibonacciRecursive {
    static int fibonacci(int n) {
        if (n <= 1) return n;
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter n: ");
        int n = sc.nextInt();
        System.out.println("Fibonacci: " + fibonacci(n));
    }
}

// Exercise 14: Array Sum and Average
import java.util.Scanner;
public class ArraySumAverage {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        int sum = 0;
        for (int i = 0; i < n; i++) {
            System.out.print("Enter element " + (i + 1) + ": ");
            arr[i] = sc.nextInt();
            sum += arr[i];
        }
        double avg = (double) sum / n;
        System.out.println("Sum: " + sum + ", Average: " + avg);
    }
}

// Exercise 15: String Reversal
import java.util.Scanner;
public class ReverseString {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a string: ");
        String input = sc.nextLine();
        StringBuilder sb = new StringBuilder(input);
        System.out.println("Reversed: " + sb.reverse());
    }
}

// Exercise 16: Palindrome Checker
import java.util.Scanner;
public class PalindromeString {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a string: ");
        String str = sc.nextLine().replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        String rev = new StringBuilder(str).reverse().toString();
        System.out.println(str.equals(rev) ? "Palindrome" : "Not a Palindrome");
    }
}

// Exercise 17: Class and Object Creation
class Car {
    String make, model;
    int year;
    Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }
    void displayDetails() {
        System.out.println("Make: " + make + ", Model: " + model + ", Year: " + year);
    }
    public static void main(String[] args) {
        Car car1 = new Car("Toyota", "Corolla", 2022);
        car1.displayDetails();
    }
}

// Exercise 18: Inheritance Example
class Animal {
    void makeSound() {
        System.out.println("Some sound");
    }
}
class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark");
    }
    public static void main(String[] args) {
        Animal a = new Animal();
        a.makeSound();
        Dog d = new Dog();
        d.makeSound();
    }
}

// Exercise 19: Interface Implementation
interface Playable {
    void play();
}
class Guitar implements Playable {
    public void play() {
        System.out.println("Strumming the guitar");
    }
}
class Piano implements Playable {
    public void play() {
        System.out.println("Playing the piano");
    }
    public static void main(String[] args) {
        Playable g = new Guitar();
        Playable p = new Piano();
        g.play();
        p.play();
    }
}

// Exercise 20: Try-Catch Example
import java.util.Scanner;
public class TryCatchExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        try {
            System.out.print("Enter numerator: ");
            int a = sc.nextInt();
            System.out.print("Enter denominator: ");
            int b = sc.nextInt();
            System.out.println("Result: " + (a / b));
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero.");
        }
    }
}