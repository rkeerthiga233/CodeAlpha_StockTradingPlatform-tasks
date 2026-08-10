# CodeAlpha_StockTradingPlatform-tasks
C# CodeAlpha_StockTradingPlatform
Stock Trading Platform project in Java for CodeAlpha Internship.

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Stock {
    private String symbol;
    private String companyName;
    private double price;

    public Stock(String symbol, String companyName, double price) {
        this.symbol = symbol;
        this.companyName = companyName;
        this.price = price;
    }

    public String getSymbol() { return symbol; }
    public String getCompanyName() { return companyName; }
    public double getPrice() { return price; }
    public void setPrice(double price) { this.price = price; }
}

class Portfolio {
    private double cashBalance;
    private Map<String, Integer> shares = new HashMap<>();

    public Portfolio(double initialBalance) {
        this.cashBalance = initialBalance;
    }

    public void buyStock(Stock stock, int quantity) {
        double cost = stock.getPrice() * quantity;
        if (cost <= cashBalance) {
            cashBalance -= cost;
            shares.put(stock.getSymbol(), shares.getOrDefault(stock.getSymbol(), 0) + quantity);
            System.out.println("Successfully bought " + quantity + " shares of " + stock.getSymbol());
        } else {
            System.out.println("Transaction failed: Insufficient cash balance.");
        }
    }

    public void sellStock(Stock stock, int quantity) {
        int currentShares = shares.getOrDefault(stock.getSymbol(), 0);
        if (currentShares >= quantity) {
            shares.put(stock.getSymbol(), currentShares - quantity);
            cashBalance += stock.getPrice() * quantity;
            System.out.println("Successfully sold " + quantity + " shares of " + stock.getSymbol());
        } else {
            System.out.println("Transaction failed: Not enough shares owned.");
        }
    }

    public void displayPortfolio(Map<String, Stock> market) {
        System.out.println("\n--- PORTFOLIO SUMMARY ---");
        System.out.printf("Cash Balance: $%.2f\n", cashBalance);
        double totalPortfolioValue = cashBalance;

        for (Map.Entry<String, Integer> entry : shares.entrySet()) {
            String symbol = entry.getKey();
            int qty = entry.getValue();
            if (qty > 0) {
                double currentPrice = market.get(symbol).getPrice();
                double value = qty * currentPrice;
                totalPortfolioValue += value;
                System.out.printf("%s: %d shares | Current Price: $\%.2f \vert{} Total:$%.2f\n", 
                                  symbol, qty, currentPrice, value);
            }
        }
        System.out.printf("Total Account Value: $%.2f\n", totalPortfolioValue);
    }
}

public class StockTradingPlatform {
odeAlpha_StockTradingPlatform
