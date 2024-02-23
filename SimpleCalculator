import java.util.Scanner;
import java.util.*;

public class SimpleCalculator {
    private static double currentValue = 0;
    private static String expressionBeforeCalculation;
    private static Stack<Integer> stack = new Stack<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("> " + currentValue);
            String input = scanner.nextLine();

            if (input.equals("c")) {
                clearCalculator();
            } else if (input.equals("=")) {
                displayCurrentValue();
            } else {
                try {
                    currentValue = evaluateExpression(input);
                } catch (Exception e) {
                    handleInvalidInput();
                }
            }
        }
    }

    private static void clearCalculator() {
        currentValue = 0;
        stack.clear();
    }

    private static void displayCurrentValue() {
        System.out.println(currentValue);
    }


    public static int evaluateExpression(String expression) {
        StringBuilder currentNumber = new StringBuilder();
        char currentOp = 0;

        for (char ch : expression.toCharArray()) {
            if (Character.isDigit(ch)) {
                // Accumulate digits to form a number
                currentNumber.append(ch);
            } else if (isOperator(ch)) {
                // Check if there was a number before the operator
                if (currentNumber.length() > 0) {
                    int operand = Integer.parseInt(currentNumber.toString());
                    stack.push(operand);
                    currentNumber.setLength(0); // Reset the StringBuilder
                }
                currentOp = ch;
            } else {
                System.out.println("Invalid ..");
            }
        }

        // Handle the case where the expression ends with a number
        if (currentNumber.length() > 0) {
            int lastOperand = Integer.parseInt(currentNumber.toString());
            stack.push(lastOperand);
        }

        // Perform operation
        int operand2 = stack.pop();
        int operand1 = stack.pop();
        int result = performOperation(operand1, operand2, currentOp);
        stack.push(result);

        return stack.peek();
    }

    private static void handleInvalidInput() {
        System.out.println("Invalid input. Please try again.");
    }

    private static boolean isOperator(char ch) {
        return ch == '+' || ch == '-' || ch == '*' || ch == '/';
    }
    private static int performOperation(int operand1, int operand2, char operator) {
        switch (operator) {
            case '+':
                return operand1 + operand2;
            case '-':
                return operand1 - operand2;
            case '*':
                return operand1 * operand2;
            case '/':
                if (operand2 != 0) {
                    return operand1 / operand2;
                } else {
                    throw new ArithmeticException("Cannot divide by zero");
                }
            default:
                throw new IllegalArgumentException("Invalid operator: " + operator);
        }
    }
}
