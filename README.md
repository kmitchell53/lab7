# lab7

money convertor

package assignments;

public class MoneyConverter {
    private final int[] bills = {10, 5, 1}; // Ten, five, and one dollar bills
    private final int[] coins = {25, 10, 5, 1}; // Quarters, dimes, nickels, pennies
    private final String[] billNames = {"ten dollar bills", "five dollar bills", "one dollar bills"};
    private final String[] coinNames = {"quarters", "dimes", "nickels", "pennies"};

    public void convert(double amount) {
        int dollars = (int) amount; // Extract whole dollar amount
        int cents = (int) Math.round((amount - dollars) * 100); // Extract cents

        // Convert dollars into bills
        for (int i = 0; i < bills.length; i++) {
            int count = dollars / bills[i];
            dollars %= bills[i];
            System.out.println(count + " " + billNames[i]);
        }

        // Convert cents into coins
        for (int i = 0; i < coins.length; i++) {
            int count = cents / coins[i];
            cents %= coins[i];
            System.out.println(count + " " + coinNames[i]);
        }
    }
}




driver

package assignments;

import java.util.Scanner;

public class driver {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        MoneyConverter converter = new MoneyConverter();

        while (true) {
            System.out.print("\nEnter a monetary amount (or type 'quit' to exit): ");
            String input = scanner.nextLine().trim();

            // Exit loop if user types "quit"
            if (input.equalsIgnoreCase("quit")) {
                System.out.println("Goodbye!");
                break;
            }

            try {
                double amount = Double.parseDouble(input);
                if (amount < 0) {
                    System.out.println("Amount must be positive. Try again.");
                    continue;
                }
                converter.convert(amount);
            } catch (NumberFormatException e) {
                System.out.println("EXCEPTION: Invalid input");
            }
        }

        scanner.close();
    }
}
