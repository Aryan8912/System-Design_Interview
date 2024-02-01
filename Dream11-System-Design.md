# Designing an Online Auction System
In this article, we delve into the object-oriented design and implementation of an Online Auction System using C++. 

This system allows for the creation and management of auctions, user participation in bidding, and handling transactions.

## System Requirements

The Online Auction System should:

1. **Auction Management**: Create and manage auctions with item details, starting prices, and durations.
2. **User Account Management**: Handle user registrations for sellers and bidders.
3. **Bidding Process**: Allow users to place and track bids.
4. **Auction Monitoring**: Enable users to view ongoing auctions and status.
5. **Transaction Processing**: Handle winning bid transactions.

## Core Use Cases

1. **Creating and Managing Auctions**
2. **Registering and Managing User Accounts**
3. **Placing and Tracking Bids**
4. **Monitoring Auction Progress**
5. **Processing Transactions**

## Key Classes:
- `OnlineAuctionSystem`: Manages the system.
- `User`: Represents a system user.
- `Auction`: Manages auction details.
- `Bid`: Represents a user's bid.
```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

class Bid {
public:
    Bid(const std::string& bidder, double amount) : bidder(bidder), amount(amount) {}

    const std::string& getBidder() const {
        return bidder;
    }

    double getAmount() const {
        return amount;
    }

private:
    std::string bidder;
    double amount;
};

class Auction {
public:
    Auction(const std::string& item, double startingPrice, int duration)
        : item(item), startingPrice(startingPrice), duration(duration), status("Active") {}

    const std::string& getItem() const {
        return item;
    }

    double getStartingPrice() const {
        return startingPrice;
    }

    int getDuration() const {
        return duration;
    }

    const std::string& getStatus() const {
        return status;
    }

    void placeBid(const Bid& bid) {
        bids.push_back(bid);
        std::cout << "Bid placed by " << bid.getBidder() << " with amount $" << bid.getAmount() << ".\n";
    }

    void closeAuction() {
        status = "Closed";
        if (!bids.empty()) {
            const Bid& winningBid = *std::max_element(bids.begin(), bids.end(), [](const Bid& a, const Bid& b) {
                return a.getAmount() < b.getAmount();
            });

            std::cout << "Auction closed. Winning bid by " << winningBid.getBidder() << " with amount $" << winningBid.getAmount() << ".\n";
        } else {
            std::cout << "Auction closed with no bids.\n";
        }
    }

private:
    std::string item;
    double startingPrice;
    int duration;
    std::string status;
    std::vector<Bid> bids;
};

class User {
public:
    User(const std::string& username) : username(username) {}

    const std::string& getUsername() const {
        return username;
    }

    void participateInAuction(Auction& auction, double amount) {
        if (auction.getStatus() == "Active") {
            Bid bid(username, amount);
            auction.placeBid(bid);
        } else {
            std::cout << "Auction is closed. Cannot place a bid.\n";
        }
    }
};

class OnlineAuctionSystem {
public:
    Auction& createAuction(const std::string& item, double startingPrice, int duration) {
        auctions.emplace_back(item, startingPrice, duration);
        return auctions.back();
    }

    User& registerUser(const std::string& username) {
        users.emplace(username, User(username));
        return users[username];
    }

    void displayOngoingAuctions() const {
        std::cout << "Ongoing Auctions:\n";
        for (const auto& auction : auctions) {
            if (auction.getStatus() == "Active") {
                std::cout << "Item: " << auction.getItem() << ", Starting Price: $" << auction.getStartingPrice() << "\n";
            }
        }
    }

private:
    std::vector<Auction> auctions;
    std::unordered_map<std::string, User> users;
};

int main() {
    OnlineAuctionSystem auctionSystem;

    // Register users
    User& bidder1 = auctionSystem.registerUser("Alice");
    User& bidder2 = auctionSystem.registerUser("Bob");
    User& seller = auctionSystem.registerUser("Charlie");

    // Create auctions
    Auction& auction1 = auctionSystem.createAuction("Artwork", 100.0, 7);
    Auction& auction2 = auctionSystem.createAuction("Electronics", 200.0, 5);

    // Display ongoing auctions
    auctionSystem.displayOngoingAuctions();

    // Users participate in auctions
    bidder1.participateInAuction(auction1, 120.0);
    bidder2.participateInAuction(auction1, 150.0);
    bidder1.participateInAuction(auction2, 250.0);

    // Close auctions
    auction1.closeAuction();
    auction2.closeAuction();

    return 0;
}
