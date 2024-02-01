# Designing a Hotel Management System

In this article, we will explore the design and implementation of a Hotel Management System (HMS) using object-oriented principles in C++. 

The HMS is designed to streamline hotel operations including room booking, customer management, and service provision.

## System Requirements

The HMS will facilitate:

1. **Room Booking Management:** Manage bookings for various types of rooms.
2. **Customer Management:** Handle customer information and booking history.
3. **Room Service Management:** Manage orders for food and other services.
4. **Billing:** Generate bills for customers based on their usage of services.

## Core Use Cases

1. **Booking a Room:** Customers can book different types of rooms.
2. **Managing Customer Profiles:** Storing and retrieving customer details.
3. **Ordering Room Services:** Placing orders for room-related services.
4. **Generating Bills:** Calculating and producing bills for customers.

## Key Classes:
- `Hotel`: Manages the overall hotel operations.
- `Room`: Represents individual rooms in the hotel.
- `Customer`: Manages information about customers.
- `Booking`: Represents a room booking by a customer.
- `Service`: Represents additional services provided to customers.

```cpp
#include <iostream>
#include <vector>
#include <string>

class Room {
public:
    Room(int number, std::string type) : number(number), type(std::move(type)), booked(false) {}

    int getNumber() const { return number; }
    std::string getType() const { return type; }
    bool isBooked() const { return booked; }

    void bookRoom() { booked = true; }
    void unbookRoom() { booked = false; }

private:
    int number;
    std::string type;
    bool booked;
};

class Customer {
public:
    Customer(std::string name, std::string email) : name(std::move(name)), email(std::move(email)) {}

    std::string getName() const { return name; }
    std::string getEmail() const { return email; }

private:
    std::string name;
    std::string email;
};

class Booking {
public:
    Booking(Customer* customer, Room* room, int duration) : customer(customer), room(room), duration(duration) {}

    Customer* getCustomer() const { return customer; }
    Room* getRoom() const { return room; }
    int getDuration() const { return duration; }

private:
    Customer* customer;
    Room* room;
    int duration;
};

class Service {
public:
    Service(std::string name, double cost) : name(std::move(name)), cost(cost) {}

    std::string getName() const { return name; }
    double getCost() const { return cost; }

private:
    std::string name;
    double cost;
};

class Hotel {
public:
    void addRoom(int number, std::string type) {
        rooms.push_back(Room(number, std::move(type)));
    }

    void displayAvailableRooms() const {
        std::cout << "Available Rooms:\n";
        for (const Room& room : rooms) {
            if (!room.isBooked()) {
                std::cout << "Room " << room.getNumber() << " - " << room.getType() << "\n";
            }
        }
        std::cout << "----------------\n";
    }

    Room* bookRoom(Customer* customer, int roomNumber, int duration) {
        for (Room& room : rooms) {
            if (room.getNumber() == roomNumber && !room.isBooked()) {
                room.bookRoom();
                bookings.push_back(Booking(customer, &room, duration));
                return &room;
            }
        }
        return nullptr;
    }

    void displayCustomerBookings(Customer* customer) const {
        std::cout << "Bookings for " << customer->getName() << ":\n";
        for (const Booking& booking : bookings) {
            if (booking.getCustomer() == customer) {
                std::cout << "Room " << booking.getRoom()->getNumber() << ", Duration: " << booking.getDuration() << " days\n";
            }
        }
        std::cout << "----------------\n";
    }

    void orderRoomService(Customer* customer, Service* service) {
        std::cout << customer->getName() << " ordered " << service->getName() << " for Room Service. Cost: $" << service->getCost() << "\n";
    }

    double generateBill(Customer* customer) const {
        double totalCost = 0.0;
        for (const Booking& booking : bookings) {
            if (booking.getCustomer() == customer) {
                totalCost += booking.getDuration() * ROOM_RATE_PER_DAY;
            }
        }
        return totalCost;
    }

private:
    static const double ROOM_RATE_PER_DAY;
    std::vector<Room> rooms;
    std::vector<Booking> bookings;
};

const double Hotel::ROOM_RATE_PER_DAY = 100.0;

int main() {
    Hotel hotel;

    hotel.addRoom(101, "Standard");
    hotel.addRoom(102, "Deluxe");
    hotel.addRoom(103, "Suite");

    hotel.displayAvailableRooms();

    Customer customer1("John Doe", "john.doe@email.com");
    Customer customer2("Jane Smith", "jane.smith@email.com");

    Room* bookedRoom1 = hotel.bookRoom(&customer1, 101, 3);
    Room* bookedRoom2 = hotel.bookRoom(&customer2, 102, 5);

    if (bookedRoom1 && bookedRoom2) {
        std::cout << "Rooms booked successfully.\n";
    } else {
        std::cout << "Failed to book rooms.\n";
    }

    hotel.displayCustomerBookings(&customer1);
    hotel.displayCustomerBookings(&customer2);

    Service roomService("Dinner", 30.0);
    hotel.orderRoomService(&customer1, &roomService);

    double bill1 = hotel.generateBill(&customer1);
    double bill2 = hotel.generateBill(&customer2);

    std::cout << "Bill for " << customer1.getName() << ": $" << bill1 << "\n";
    std::cout << "Bill for " << customer2.getName() << ": $" << bill2 << "\n";

    return 0;
}
