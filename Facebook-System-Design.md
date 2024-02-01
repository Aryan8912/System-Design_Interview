Designing a Social Network Like Facebook
This blog post explores designing and implementing a social network platform similar to Facebook using Java.

We focus on user profiles, friendships, posting updates, and generating a feed of posts.

System Requirements
The Social Network platform should support:

User Profile Management: Enabling creation and management of user profiles.
Friendship Management: Allowing users to connect as friends.
Posting Updates: Permitting users to post updates and view others' updates.
Feed Generation: Displaying a feed composed of friends' posts.
Core Use Cases
Creating and Updating User Profiles
Managing Friendships
Creating Posts
Viewing the Feed
UML/Class Diagrams
Key Classes:

SocialNetworkSystem: Manages the overall operations.
User: Represents a user on the network.
Post: Represents a user's post.
Friendship: Manages the friendships between users.

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <string>

// Forward declarations
class User;
class Post;

// Class representing a Post
class Post {
public:
    Post(User* author, std::string content) : author(author), content(std::move(content)) {}

    User* getAuthor() const { return author; }
    std::string getContent() const { return content; }

private:
    User* author;
    std::string content;
};

// Class representing a User
class User {
public:
    User(std::string username) : username(std::move(username)) {}

    std::string getUsername() const { return username; }
    const std::vector<User*>& getFriends() const { return friends; }
    const std::vector<Post*>& getPosts() const { return posts; }

    void addFriend(User* friendUser) {
        if (friendUser != this) {
            friends.push_back(friendUser);
        }
    }

    void createPost(std::string content) {
        Post* post = new Post(this, std::move(content));
        posts.push_back(post);
    }

    void displayFeed() const {
        std::cout << "Feed for " << username << ":\n";
        for (const User* friendUser : friends) {
            std::cout << friendUser->getUsername() << "'s Posts:\n";
            for (const Post* post : friendUser->getPosts()) {
                std::cout << "- " << post->getContent() << "\n";
            }
        }
        std::cout << "----------------\n";
    }

private:
    std::string username;
    std::vector<User*> friends;
    std::vector<Post*> posts;
};

// Class representing the Social Network System
class SocialNetworkSystem {
public:
    void addUser(const User& user) { users[user.getUsername()] = new User(user); }

    User* getUser(const std::string& username) const {
        auto it = users.find(username);
        return (it != users.end()) ? it->second : nullptr;
    }

    void makeFriends(User* user1, User* user2) {
        user1->addFriend(user2);
        user2->addFriend(user1);
    }

private:
    std::unordered_map<std::string, User*> users;
};

int main() {
    SocialNetworkSystem socialNetwork;

    // Adding users to the social network
    socialNetwork.addUser(User("user1"));
    socialNetwork.addUser(User("user2"));
    socialNetwork.addUser(User("user3"));

    // Retrieving users
    User* user1 = socialNetwork.getUser("user1");
    User* user2 = socialNetwork.getUser("user2");
    User* user3 = socialNetwork.getUser("user3");

    // Making friends
    socialNetwork.makeFriends(user1, user2);
    socialNetwork.makeFriends(user1, user3);

    // Creating posts
    user1->createPost("Hello, this is user1's post!");
    user2->createPost("Greetings from user2!");
    user3->createPost("Post by user3.");

    // Displaying feeds
    user1->displayFeed();
    user2->displayFeed();
    user3->displayFeed();

    return 0;
}
