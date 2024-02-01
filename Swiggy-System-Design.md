# Designing an Online Food Delivery Service Like Swiggy

In this article, we explore the object-oriented design and implementation of an Online Food Delivery Service similar to Swiggy using Java. 

This system encompasses functionalities essential for online food ordering and delivery.

## System Requirements

The Online Food Delivery System should:

1. **Restaurant Management**: Manage restaurant profiles, menus, and availability.
2. **User Account Management**: Handle customer and delivery agent profiles.
3. **Order Processing**: Enable customers to place orders and track their status.
4. **Delivery Management**: Assign orders to delivery agents and manage the delivery process.
5. **Payment Processing**: Handle various modes of payment.

## Core Use Cases

1. **Adding and Managing Restaurants**
2. **Registering and Managing User and Delivery Agent Accounts**
3. **Placing and Tracking Orders**
4. **Assigning and Managing Deliveries**
5. **Processing Payments**

## UML/Class Diagrams

Key Classes:

- `OnlineFoodDeliveryService`: Manages the overall system.
- `User`: Represents a customer.
- `Restaurant`: Manages a restaurant's profile and menu.
- `Order`: Represents a food order.
- `DeliveryAgent`: Manages a delivery agent's information.
- `Payment`: Handles payment transactions.

```cpp
#include <iostream>
#include <vector>
#include <string>

// Enum to represent order status
enum class OrderStatus {
    Placed,
    InProgress,
    Delivered,
    Cancelled
};

// Forward declaration of classes
class User;
class Restaurant;
class Order;
class DeliveryAgent;

// Class to represent the overall Online Food Delivery Service
class OnlineFoodDeliveryService {
private:
    std::vector<User> users;
    std::vector<Restaurant> restaurants;
    std::vector<Order> orders;
    std::vector<DeliveryAgent> deliveryAgents;

public:
    // Functions for restaurant management
    void addRestaurant(const std::string& name, const std::string& menu);
    void displayRestaurants();

    // Functions for user and delivery agent management
    void registerUser(const std::string& name, const std::string& address);
    void registerDeliveryAgent(const std::string& name);

    // Function for order processing
    void placeOrder(int userId, int restaurantId, const std::string& items);
    void trackOrder(int orderId);
};

// Class to represent a User
class User {
private:
    int userId;
    std::string name;
    std::string address;

public:
    User(int id, const std::string& n, const std::string& addr)
        : userId(id), name(n), address(addr) {}

    friend class OnlineFoodDeliveryService;
};

// Class to represent a Restaurant
class Restaurant {
private:
    int restaurantId;
    std::string name;
    std::string menu;

public:
    Restaurant(int id, const std::string& n, const std::string& m)
        : restaurantId(id), name(n), menu(m) {}

    friend class OnlineFoodDeliveryService;
};

// Class to represent an Order
class Order {
private:
    int orderId;
    int userId;
    int restaurantId;
    std::string items;
    OrderStatus status;

public:
    Order(int id, int uId, int rId, const std::string& it)
        : orderId(id), userId(uId), restaurantId(rId), items(it), status(OrderStatus::Placed) {}

    friend class OnlineFoodDeliveryService;
};

// Class to represent a DeliveryAgent
class DeliveryAgent {
private:
    int agentId;
    std::string name;

public:
    DeliveryAgent(int id, const std::string& n)
        : agentId(id), name(n) {}

    friend class OnlineFoodDeliveryService;
};

// Implementation of OnlineFoodDeliveryService functions
void OnlineFoodDeliveryService::addRestaurant(const std::string& name, const std::string& menu) {
    int restaurantId = static_cast<int>(restaurants.size()) + 1;
    restaurants.emplace_back(restaurantId, name, menu);
}

void OnlineFoodDeliveryService::displayRestaurants() {
    std::cout << "Available Restaurants:\n";
    for (const auto& restaurant : restaurants) {
        std::cout << "ID: " << restaurant.restaurantId << ", Name: " << restaurant.name << "\n";
    }
}

void OnlineFoodDeliveryService::registerUser(const std::string& name, const std::string& address) {
    int userId = static_cast<int>(users.size()) + 1;
    users.emplace_back(userId, name, address);
}

void OnlineFoodDeliveryService::registerDeliveryAgent(const std::string& name) {
    int agentId = static_cast<int>(deliveryAgents.size()) + 1;
    deliveryAgents.emplace_back(agentId, name);
}

void OnlineFoodDeliveryService::placeOrder(int userId, int restaurantId, const std::string& items) {
    int orderId = static_cast<int>(orders.size()) + 1;
    orders.emplace_back(orderId, userId, restaurantId, items);
}

void OnlineFoodDeliveryService::trackOrder(int orderId) {
    for (const auto& order : orders) {
        if (order.orderId == orderId) {
            std::cout << "Order Status: ";
            switch (order.status) {
                case OrderStatus::Placed:
                    std::cout << "Placed\n";
                    break;
                case OrderStatus::InProgress:
                    std::cout << "In Progress\n";
                    break;
                case OrderStatus::Delivered:
                    std::cout << "Delivered\n";
                    break;
                case OrderStatus::Cancelled:
                    std::cout << "Cancelled\n";
                    break;
            }
            return;
        }
    }
    std::cout << "Order not found.\n";
}

// Sample usage
int main() {
    OnlineFoodDeliveryService foodDeliveryService;

    // Add restaurants
    foodDeliveryService.addRestaurant("Restaurant A", "Menu A");
    foodDeliveryService.addRestaurant("Restaurant B", "Menu B");

    // Display available restaurants
    foodDeliveryService.displayRestaurants();

    // Register users and delivery agents
    foodDeliveryService.registerUser("User 1", "Address 1");
    foodDeliveryService.registerUser("User 2", "Address 2");
    foodDeliveryService.registerDeliveryAgent("Agent 1");
    foodDeliveryService.registerDeliveryAgent("Agent 2");

    // Place orders
    foodDeliveryService.placeOrder(1, 1, "Dish 1, Dish 2");
    foodDeliveryService.placeOrder(2, 2, "Dish 3, Dish 4");

    // Track orders
    foodDeliveryService.trackOrder(1);
    foodDeliveryService.trackOrder(2);

    return 0;
}
