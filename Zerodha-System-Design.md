# Designing an Online Stock Brokerage System

In this article, we'll examine the object-oriented design and implementation of an Online Stock Brokerage System using Java. 

This system simulates key functionalities of stock trading platforms, enabling users to engage in buying and selling stocks, manage their portfolios, and stay updated with stock prices.

## System Requirements

The Stock Brokerage System needs to:

1. **User Account Management:** Manage user registrations and profiles.
2. **Stock Trading:** Enable stock buying and selling.
3. **Portfolio Management:** Allow users to manage their stock holdings.
4. **Stock Price Feed:** Provide real-time stock price updates.

## Core Use Cases

1. **Registering and Managing User Accounts**
2. **Buying and Selling Stocks**
3. **Managing Portfolio**
4. **Viewing Stock Prices**

## Key Classes:
- `StockBrokerageSystem`: Manages the entire system.
- `User`: Represents a system user.
- `Stock`: Represents a stock in the market.
- `Portfolio`: Manages a user's stock holdings.
- `Trade`: Handles stock trade transactions.

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <string>

class Stock {
public:
    Stock(std::string symbol, double price) : symbol(std::move(symbol)), price(price) {}

    const std::string& getSymbol() const { return symbol; }
    double getPrice() const { return price; }

private:
    std::string symbol;
    double price;
};

class Portfolio {
public:
    void addStock(const Stock& stock, int quantity) {
        stocks[stock.getSymbol()] += quantity;
    }

    void removeStock(const Stock& stock, int quantity) {
        if (stocks[stock.getSymbol()] >= quantity) {
            stocks[stock.getSymbol()] -= quantity;
        }
    }

    void displayPortfolio() const {
        std::cout << "Portfolio:\n";
        for (const auto& item : stocks) {
            std::cout << item.first << ": " << item.second << " shares\n";
        }
        std::cout << "----------------\n";
    }

private:
    std::unordered_map<std::string, int> stocks;
};

class Trade {
public:
    void executeBuyOrder(const Stock& stock, int quantity, Portfolio& portfolio) {
        // Simulate buying by adding stocks to the portfolio
        portfolio.addStock(stock, quantity);
        std::cout << "Buy order executed: " << quantity << " shares of " << stock.getSymbol() << "\n";
    }

    void executeSellOrder(const Stock& stock, int quantity, Portfolio& portfolio) {
        // Simulate selling by removing stocks from the portfolio
        portfolio.removeStock(stock, quantity);
        std::cout << "Sell order executed: " << quantity << " shares of " << stock.getSymbol() << "\n";
    }
};

class StockBrokerageSystem {
public:
    void registerUser(const std::string& username) {
        users.emplace_back(username);
        std::cout << "User registered: " << username << "\n";
    }

    void displayStockPrices() const {
        std::cout << "Stock Prices:\n";
        for (const auto& stock : stocks) {
            std::cout << stock.getSymbol() << ": $" << stock.getPrice() << "\n";
        }
        std::cout << "----------------\n";
    }

    User& getUser(const std::string& username) {
        auto it = std::find_if(users.begin(), users.end(), [&username](const User& user) {
            return user.getUsername() == username;
        });
        if (it != users.end()) {
            return *it;
        } else {
            throw std::runtime_error("User not found.");
        }
    }

private:
    std::vector<User> users;
    std::vector<Stock> stocks{
        Stock("AAPL", 150.0),
        Stock("GOOGL", 2800.0),
        // Add more stocks as needed
    };
};

int main() {
    StockBrokerageSystem brokerageSystem;

    // Register users
    brokerageSystem.registerUser("John");
    brokerageSystem.registerUser("Alice");

    // Display stock prices
    brokerageSystem.displayStockPrices();

    // Simulate stock trading
    User& john = brokerageSystem.getUser("John");
    Portfolio& johnPortfolio = john.getPortfolio();

    Trade trade;
    trade.executeBuyOrder(brokerageSystem.getStock("AAPL"), 5, johnPortfolio);
    trade.executeSellOrder(brokerageSystem.getStock("GOOGL"), 2, johnPortfolio);

    // Display updated portfolio
    johnPortfolio.displayPortfolio();

    return 0;
}
