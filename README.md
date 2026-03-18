# tasks
таск 4
```
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.print("Кол-во n чисел, которые надо найти: ");
        int amount = scan.nextInt();
        System.out.print("Введите значение a: ");
        int numberA = scan.nextInt();
        System.out.print("Введите значение b: ");
        int numberB = scan.nextInt();

        int result = solve(amount, numberA, numberB);
        System.out.println();
        System.out.print("Сумма n чисел: ");
        System.out.print(result);
    }

    public static int solve(int n, int a, int b) {
        int firstValue = 1, counter = 0, sum = 0;
        while (counter != n) {
            if (check(firstValue, a, b)) {
                sum += firstValue;
                counter++;
            }
            firstValue++;
        }
        return sum;
    }

    public static boolean check(int k, int a, int b) {
        return k % a == 0 && k % b != 0;
    }
}
```
таск 5
```
import java.io.PrintStream;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите h >= 1: ");
        int h = scanner.nextInt();
        for (int i = 1; i <= h; i++) { //кол-во строк
            for (int j = 1; j < i; j++) { //кол-во пробелов
                System.out.print(" ");
            }
            int s = h - i + 1; //символов в строке
            for (int k = 1; k <= s; k++) {
                if (i==1) {
                    System.out.print("*");
                } else if (i <= h - 2) {
                    if (k==1 || k==s) {
                        System.out.print("*");
                    } else {
                        System.out.print("$");
                    }
                } else {
                    System.out.print("*");
                }
            }
            System.out.println();
        }
    }
}
```
таск 6
```
import java.util.Scanner;

public class Main {
    public static class Task6Result {
        double f;  //точное значение функции
        double sn, se, se10;  //сумма n слагаемых, >e, >e/10
        int n, ne, ne10;  //количество слагаемых для сумм
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Введите значение x: ");
        double x = scanner.nextDouble();

        System.out.print("Введите количество итераций n: ");
        int n = scanner.nextInt();

        System.out.print("Введите порог e: ");
        double e = scanner.nextDouble();

        Task6Result result = task6(x, n, e);

        System.out.println("Результаты:");
        System.out.printf("1) Сумма %d слагаемых: %.10f%n", result.n, result.sn); //%d подставяет целое число, указанное после запятой, а %10а - дробное с 10 знаками после запятой
        System.out.printf("2) Сумма %d слагаемых > e = %.10f: %.10f%n", result.ne, e, result.se);
        System.out.printf("3) Сумма %d слагаемых > e/10 = %.10f: %.10f%n", result.ne10, e/10, result.se10);
        System.out.printf("4) Точное значение функции: %.10f%n", result.f);
        System.out.printf("Погрешность: %.2e%n", Math.abs(result.sn - result.f)); //разница между приближенной суммой и точным значением
    }

    public static double getCurr(double prev, double x, int i) {  //функция для следующего слагаемого ряда
        return prev * (x * (i + 1.0) / i);
    }

    public static Task6Result task6(double x, int n, double e) {
        Task6Result r = new Task6Result(); //создали "коробку" под переменные
        r.f = 1.0 / Math.pow(1 - x, 2); //точное значение функции

        double a = 1.0; //первое сагаемое ряда a0 = 1
        r.sn = 0.0; //сумма первых n слагаемых
        r.se = 0.0; //сумма слагаемых >e
        r.se10 = 0.0; //>e/10
        r.n = 0; // сколько слагаемых в sn
        r.ne = 0; //в se
        r.ne10 = 0; //в se10

        for (int i = 0; i < n || Math.abs(a) > e / 10; i++) { //до момента пока не достигли n-ого элемента или текущее слагаемое больше e/10 (мы не можем им принебречь)
            if (i < n) {
                r.sn += a;
                r.n++;
            }
            if (Math.abs(a) > e) {
                r.se += a;
                r.ne++;
            }
            if (Math.abs(a) > e / 10) {
                r.se10 += a;
                r.ne10++;
            }

            a = getCurr(a, x, i + 1); // вычисляем следующее слагаемое
        }

        return r;
    }
}
```
таск 7
```
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.print("Введите числа через пробел: ");
        String[] inputStr = scan.nextLine().split(" ");

        int[] input = new int[inputStr.length];
        for (int i = 0; i < inputStr.length; i++) {
            input[i] = Integer.parseInt(inputStr[i]);
        }

        System.out.println(solve2(input));
    }

    public static int countRepeat(int[] arr, int value) {
        int count = 0;
        for (int x : arr) {
            if (x == value) {
                count++;
            }
        }
        return count;
    }

    public static int indexOfNthLast(int[] arr, int value, int k) {
        int count = 0;
        for (int i = arr.length - 1; i >= 0; i--) {
            if (arr[i] == value) {
                count++;
                if (count == k) {
                    return i;
                }
            }
        }
        return -1;
    }

    public static int solve2(int[] arr) {
        int maxCount = 0;
        int suitableValue = arr[0];

        for (int i = 0; i < arr.length; i++) {
            int count = countRepeat(arr, arr[i]);

            if (count > maxCount || (count == maxCount && arr[i] > suitableValue)) {
                maxCount = count;
                suitableValue = arr[i];
            }
        }

        return indexOfNthLast(arr, suitableValue, 2);
    }
}
```
