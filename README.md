# Codsoft-task4-

import java.math.BigDecimal;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class CurrencyConverter {

    // Hardcoded exchange rates (for demonstration purposes)
    private static Map<String, BigDecimal> exchangeRates = new HashMap<>();

    static {
        // Define exchange rates (key format: "FROM-TO")
        exchangeRates.put("USD-EUR", new BigDecimal("0.85"));
        exchangeRates.put("USD-GBP", new BigDecimal("0.75"));
        exchangeRates.put("USD-JPY", new BigDecimal("110.25"));
        exchangeRates.put("EUR-USD", new BigDecimal("1.18"));
        exchangeRates.put("GBP-USD", new BigDecimal("1.33"));
        exchangeRates.put("JPY-USD", new BigDecimal("0.0091"));
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Input amount and currencies
        System.out.print("Enter amount: ");
        BigDecimal amount = scanner.nextBigDecimal();
        scanner.nextLine(); // Consume newline

        System.out.print("Enter from currency (e.g., USD, EUR, GBP, JPY): ");
        String fromCurrency = scanner.nextLine().toUpperCase();

        System.out.print("Enter to currency (e.g., USD, EUR, GBP, JPY): ");
        String toCurrency = scanner.nextLine().toUpperCase();

        // Perform currency conversion
        BigDecimal convertedAmount = convertCurrency(amount, fromCurrency, toCurrency);

        // Output the result
        System.out.println(amount + " " + fromCurrency + " = " + convertedAmount + " " + toCurrency);

        scanner.close();
    }

    // Method to convert currency based on predefined exchange rates
    private static BigDecimal convertCurrency(BigDecimal amount, String fromCurrency, String toCurrency) {
        String key = fromCurrency + "-" + toCurrency;
        BigDecimal rate = exchangeRates.get(key);

        if (rate == null) {
            throw new IllegalArgumentException("Unsupported currency conversion: " + fromCurrency + " to " + toCurrency);
        }

        return amount.multiply(rate).setScale(2, BigDecimal.ROUND_HALF_UP);
    }
}
