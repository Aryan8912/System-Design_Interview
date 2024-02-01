# Designing an Online Shopping System Like Amazon

In this article, we're going to design and implement an Online Shopping System resembling Amazon, using C++. 

This system will cover product listings, user accounts, shopping carts, and order processing.

## System Requirements

The Online Shopping System should:

1. **Product Management:** Manage a catalog of products.
2. **User Account Management:** Handle user registrations and logins.
3. **Shopping Cart Management:** Allow users to add and remove products from their shopping cart.
4. **Order Processing:** Process user orders and maintain order history.

## Core Use Cases

1. **Browsing Products**
2. **Managing User Accounts**
3. **Handling Shopping Carts**
4. **Processing Orders**

## Key Classes:
- `OnlineShoppingSystem`: Manages the overall system.
- `Product`: Represents a product in the catalog.
- `User`: Represents a user of the system.
- `ShoppingCart`: Manages the shopping cart.
- `Order`: Represents a user's order.

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

// Forward declarations
class User;
class Product;

// Enum for order status
enum class OrderStatus {
    PLACED,
    SHIPPED,
    DELIVERED
};

// Class representing a Product
class Product {
public:
    Product(int id, std::string name, double price) : id(id), name(std::move(name)), price(price) {}

    int getId() const { return id; }
    std::string getName() const { return name; }
    double getPrice() const { return price; }

private:
    int id;
    std::string name;
    double price;
};

// Class representing a User
class User {
public:
    User(std::string username, std::string password) : username(std::move(username)), password(std::move(password)) {}

    std::string getUsername() const { return username; }

private:
    std::string username;
    std::string password;  // In a real system, password management would be more secure
};

// Class representing an Order
class Order {
public:
    Order(int orderId, User user, std::vector<Product> products, double total)
        : orderId(orderId), user(std::move(user)), products(std::move(products)), total(total), status(OrderStatus::PLACED) {}

    void shipOrder() { status = OrderStatus::SHIPPED; }

    void deliverOrder() { status = OrderStatus::DELIVERED; }

    void displayOrderDetails() const {
        std::cout << "Order ID: " << orderId << "\nUser: " << user.getUsername() << "\nProducts:\n";

        for (const auto& product : products) {
            std::cout << "- " << product.getName() << " ($" << product.getPrice() << ")\n";
        }

        std::cout << "Total: $" << total << "\nStatus: ";

        switch (status) {
            case OrderStatus::PLACED:
                std::cout << "Placed\n";
                break;
            case OrderStatus::SHIPPED:
                std::cout << "Shipped\n";
                break;
            case OrderStatus::DELIVERED:
                std::cout << "Delivered\n";
                break;
        }
    }

private:
    int orderId;
    User user;
    std::vector<Product> products;
    double total;
    OrderStatus status;
};

// Class representing a Shopping Cart
class ShoppingCart {
public:
    void addProduct(const Product& product) { products.push_back(product); }

    void removeProduct(int productId) {
        products.erase(std::remove_if(products.begin(), products.end(), [productId](const Product& p) { return p.getId() == productId; }), products.end());
    }

    double calculateTotal() const {
        double total = 0.0;
        for (const auto& product : products) {
            total += product.getPrice();
        }
        return total;
    }

    void displayCartContents() const {
        std::cout << "Shopping Cart Contents:\n";
        for (const auto& product : products) {
            std::cout << "- " << product.getName() << " ($" << product.getPrice() << ")\n";
        }
        std::cout << "Total: $" << calculateTotal() << "\n";
    }

    Order checkout(User user) const {
        int orderId = generateOrderId();
        double total = calculateTotal();
        Order order(orderId, user, products, total);
        return order;
    }

private:
    std::vector<Product> products;

    static int generateOrderId() {
        static int orderIdCounter = 1;
        return orderIdCounter++;
    }
};

// Class representing the Online Shopping System
class OnlineShoppingSystem {
public:
    void addUser(const User& user) { users[user.getUsername()] = user; }

    void addProduct(const Product& product) { products[product.getId()] = product; }

    User loginUser(const std::string& username, const std::string& password) const {
        auto it = users.find(username);
        if (it != users.end() && it->second.getUsername() == username && it->second.getPassword() == password) {
            return it->second;
        }
        throw std::runtime_error("Invalid credentials");
    }

    Product getProductById(int productId) const {
        auto it = products.find(productId);
        if (it != products.end()) {
            return it->second;
        }
        throw std::runtime_error("Product not found");
    }

    void displayProductCatalog() const {
        std::cout << "Product Catalog:\n";
        for (const auto& pair : products) {
            std::cout << "- " << pair.second.getName() << " ($" << pair.second.getPrice() << ")\n";
        }
    }

private:
    std::unordered_map<std::string, User> users;
    std::unordered_map<int, Product> products;
};

int main() {
    OnlineShoppingSystem shoppingSystem;

    // Adding users to the system
    shoppingSystem.addUser(User("user1", "password1"));
    shoppingSystem.addUser(User("user2", "password2"));

    // Adding products to the catalog
    shoppingSystem.addProduct(Product(1, "Laptop", 999.99));
    shoppingSystem.addProduct(Product(2, "Smartphone", 499.99));
    shoppingSystem.addProduct(Product(3, "Headphones", 99.99));

    // Logging in users
    User loggedInUser1 = shoppingSystem.loginUser("user1", "password1");
    User loggedInUser2 = shoppingSystem.loginUser("user2", "password2");

    // Displaying the product catalog
    shoppingSystem.displayProductCatalog();

    // User1 adds products to the shopping cart
    ShoppingCart cart1;
    cart1.addProduct(shoppingSystem.getProductById(1));
    cart1.addProduct(shoppingSystem.getProductById(2));

    // Displaying the contents of the shopping cart
    cart1.displayCartContents();

    // User2 adds products to the shopping cart
    ShoppingCart cart2;
    cart2.addProduct(shoppingSystem.getProductById(2));
    cart2.addProduct(shoppingSystem.getProductById(3));

    // Displaying the contents of the second shopping cart
    cart2.displayCartContents();

    // User1 checks out and places an order
    Order order1 = cart1.checkout(loggedInUser1);
    order1.displayOrderDetails();

    // User2 checks out and places an order
    Order order2 = cart2.checkout(loggedInUser2);
    order2.displayOrderDetails();

    return 0;
}
