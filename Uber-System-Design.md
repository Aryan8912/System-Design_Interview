# Designing a Ride-Sharing Service Like Uber

This article explores the object-oriented design and implementation of a Ride-Sharing Service similar to Uber using C++. 

We focus on the various aspects of ride-sharing, including user and driver management, ride booking, and fare calculation.

## System Requirements

The Ride-Sharing Service should:

1. **User and Driver Account Management**: Handle the registration and profiles of users and drivers.
2. **Ride Booking**: Enable users to book rides and drivers to accept them.
3. **Fare Calculation**: Compute fares based on distance and other factors.
4. **Ride History Management**: Keep a record of past rides for users and drivers.

## Core Use Cases

1. **Registering and Managing User and Driver Accounts**
2. **Booking and Managing Rides**
3. **Calculating and Processing Fares**
4. **Maintaining Ride History**

## Key Classes:
- `RideSharingService`: Manages the overall system.
- `User`: Represents a service user.
- `Driver`: Represents a driver.
- `Ride`: Manages ride details.
- `FareCalculator`: Calculates ride fares.

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

class Ride {
public:
    Ride(int distance, const std::string& user, const std::string& driver)
        : distance(distance), user(user), driver(driver) {}

    int getDistance() const {
        return distance;
    }

    const std::string& getUser() const {
        return user;
    }

    const std::string& getDriver() const {
        return driver;
    }

private:
    int distance;
    std::string user;
    std::string driver;
};

class FareCalculator {
public:
    static double calculateFare(int distance) {
        // Simple fare calculation based on distance
        const double ratePerKm = 0.5;
        return distance * ratePerKm;
    }
};

class User {
public:
    User(const std::string& username) : username(username) {}

    const std::string& getUsername() const {
        return username;
    }

    void bookRide(int distance, const std::string& driver) {
        rides.emplace_back(distance, username, driver);
        std::cout << "Ride booked with driver " << driver << ".\n";
    }

    const std::vector<Ride>& getRideHistory() const {
        return rides;
    }

private:
    std::string username;
    std::vector<Ride> rides;
};

class Driver {
public:
    Driver(const std::string& username) : username(username) {}

    const std::string& getUsername() const {
        return username;
    }

    void acceptRide(const Ride& ride) {
        std::cout << "Ride accepted from user " << ride.getUser() << ".\n";
        activeRides.push_back(ride);
    }

    const std::vector<Ride>& getActiveRides() const {
        return activeRides;
    }

private:
    std::string username;
    std::vector<Ride> activeRides;
};

class RideSharingService {
public:
    User& registerUser(const std::string& username) {
        users.emplace(username, User(username));
        return users[username];
    }

    Driver& registerDriver(const std::string& username) {
        drivers.emplace(username, Driver(username));
        return drivers[username];
    }

    void displayRideHistory(const std::string& username) const {
        auto userIt = users.find(username);
        if (userIt != users.end()) {
            const User& user = userIt->second;
            std::cout << "Ride history for user " << username << ":\n";
            for (const auto& ride : user.getRideHistory()) {
                std::cout << "Distance: " << ride.getDistance() << " km, Driver: " << ride.getDriver() << "\n";
            }
        } else {
            std::cout << "User not found.\n";
        }
    }

private:
    std::unordered_map<std::string, User> users;
    std::unordered_map<std::string, Driver> drivers;
};

int main() {
    RideSharingService rideService;

    // Register users and drivers
    User& user1 = rideService.registerUser("Alice");
    User& user2 = rideService.registerUser("Bob");
    Driver& driver1 = rideService.registerDriver("Charlie");
    Driver& driver2 = rideService.registerDriver("David");

    // Users book rides
    user1.bookRide(10, driver1.getUsername());
    user2.bookRide(5, driver2.getUsername());

    // Drivers accept rides
    const std::vector<Ride>& activeRidesDriver1 = driver1.getActiveRides();
    if (!activeRidesDriver1.empty()) {
        const Ride& acceptedRide = activeRidesDriver1[0];
        driver1.acceptRide(acceptedRide);
    }

    const std::vector<Ride>& activeRidesDriver2 = driver2.getActiveRides();
    if (!activeRidesDriver2.empty()) {
        const Ride& acceptedRide = activeRidesDriver2[0];
        driver2.acceptRide(acceptedRide);
    }

    // Display ride history for users
    rideService.displayRideHistory(user1.getUsername());
    rideService.displayRideHistory(user2.getUsername());

    return 0;
}
```

```js
class Ride {
    constructor(distance, user, driver) {
        this.distance = distance;
        this.user = user;
        this.driver = driver;
    }

    getDistance() {
        return this.distance;
    }

    getUser() {
        return this.user;
    }

    getDriver() {
        return this.driver;
    }
}

class FareCalculator {
    static calculateFare(distance) {
        const ratePerKm = 0.5;
        return distance * ratePerKm;
    }
}

class User {
    constructor(username) {
        this.username = username;
        this.rides = [];
    }

    getUsername() {
        return this.username;
    }

    bookRide(distance, driver) {
        this.rides.push(new Ride(distance, this.username, driver));
        console.log(`Ride booked with driver ${driver}.`);
    }

    getRideHistory() {
        return this.rides;
    }
}

class Driver {
    constructor(username) {
        this.username = username;
        this.activeRides = [];
    }

    getUsername() {
        return this.username;
    }

    acceptRide(ride) {
        console.log(`Ride accepted from user ${ride.getUser()}.`);
        this.activeRides.push(ride);
    }

    getActiveRides() {
        return this.activeRides;
    }
}

class RideSharingService {
    constructor() {
        this.users = {};
        this.drivers = {};
    }

    registerUser(username) {
        this.users[username] = new User(username);
        return this.users[username];
    }

    registerDriver(username) {
        this.drivers[username] = new Driver(username);
        return this.drivers[username];
    }

    displayRideHistory(username) {
        const user = this.users[username];
        if (user) {
            console.log(`Ride history for user ${username}:`);
            for (const ride of user.getRideHistory()) {
                console.log(`Distance: ${ride.getDistance()} km, Driver: ${ride.getDriver()}`);
            }
        } else {
            console.log("User not found.");
        }
    }
}

const rideService = new RideSharingService();

const user1 = rideService.registerUser("Alice");
const user2 = rideService.registerUser("Bob");
const driver1 = rideService.registerDriver("Charlie");
const driver2 = rideService.registerDriver("David");

user1.bookRide(10, driver1.getUsername());
user2.bookRide(5, driver2.getUsername());

const activeRidesDriver1 = driver1.getActiveRides();
if (activeRidesDriver1.length > 0) {
    const acceptedRide = activeRidesDriver1[0];
    driver1.acceptRide(acceptedRide);
}

const activeRidesDriver2 = driver2.getActiveRides();
if (activeRidesDriver2.length > 0) {
    const acceptedRide = activeRidesDriver2[0];
    driver2.acceptRide(acceptedRide);
}

rideService.displayRideHistory(user1.getUsername());
rideService.displayRideHistory(user2.getUsername());
```
