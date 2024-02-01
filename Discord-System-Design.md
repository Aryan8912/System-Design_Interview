# Designing a messaging platform like Discord
In this article, we will explore the object-oriented design and implementation of a messaging platform using C++.

## System Requirements:
User Profile Management:

1. **Creating User Profiles:**

Users should be able to create a profile with a unique username.
Include necessary information such as profile picture, status, etc.

2. **Updating User Profiles:**

Users should be able to update their profile information.
This includes changing the profile picture, updating status, etc.

3. **Viewing User Profiles:**

Users should be able to view profiles of other users.
Viewable information includes the username, profile picture, status, etc.

4. **Group and Organization Management:**

Users should be able to create and manage groups and organizations.
Include functionalities like creating, updating, and viewing group/organization profiles.

## Core Use Cases:
1. **User Registration:**

Users can create an account with a unique username and other required details.
The system should ensure the uniqueness of usernames.

2. **User Authentication:**

Securely authenticate users during login to ensure their identity.

3. **Profile Creation:**

Allow users to create a profile with additional details like a profile picture and status.

4. **Profile Update:**

Users can update their profiles by changing profile pictures, updating status, etc.

5. **Profile Viewing:**

Enable users to view profiles of other users.

6. **Group/Organization Creation:**

Users can create groups or organizations with specific details.
The creator becomes the administrator of the group/organization.

7. **Group/Organization Update:**

Administrators can update the details of groups or organizations they manage.

8. **Group/Organization Viewing:**

Users can view details of groups or organizations they are part of.

## Key Classes:
1. **User:**

Represents a user account with attributes like username, password, profile picture, and status.
Contains methods for creating, updating, and viewing profiles.

2. **UserProfile:**

Manages the details of a user's profile, including the profile picture, status, etc.
Associated with the User class.

3. **GroupOrganization:**

Represents a group or organization with attributes like name, description, members, etc.
Contains methods for creating, updating, and viewing group/organization profiles.
Includes an administrator who is a User.

4. **AuthenticationManager:**

Handles user authentication during login.
Validates the user's credentials.

```cpp
#include <iostream>
#include <string>
#include <vector>

class UserProfile {
public:
    std::string profilePicture;
    std::string status;

    UserProfile(const std::string& picture, const std::string& stat)
        : profilePicture(picture), status(stat) {}
};

class User {
public:
    std::string username;
    std::string password; // For simplicity, in a real-world scenario, this should be securely stored.
    UserProfile* profile;

    User(const std::string& uname, const std::string& pwd)
        : username(uname), password(pwd), profile(nullptr) {}

    void createProfile(const std::string& picture, const std::string& stat) {
        profile = new UserProfile(picture, stat);
    }

    void updateProfile(const std::string& picture, const std::string& stat) {
        if (profile) {
            profile->profilePicture = picture;
            profile->status = stat;
        }
    }

    void viewProfile() {
        if (profile) {
            std::cout << "Username: " << username << "\n"
                      << "Profile Picture: " << profile->profilePicture << "\n"
                      << "Status: " << profile->status << "\n";
        } else {
            std::cout << "Profile not available.\n";
        }
    }
};

class GroupOrganization {
public:
    std::string name;
    std::string description;
    User* administrator; // User who created the group/organization
    // Other attributes as needed

    GroupOrganization(const std::string& gName, const std::string& desc, User* admin)
        : name(gName), description(desc), administrator(admin) {}
};

class AuthenticationManager {
public:
    bool authenticateUser(User* user, const std::string& pwd) {
        return user && user->password == pwd;
    }
};

int main() {
    User user1("Alice", "password123");
    user1.createProfile("alice_pic.jpg", "Feeling happy!");

    User user2("Bob", "securePWD");
    user2.createProfile("bob_pic.jpg", "Busy with work.");

    GroupOrganization group1("Techies", "A group for tech enthusiasts", &user1);

    AuthenticationManager authManager;

    // Example: Authenticating users
    if (authManager.authenticateUser(&user1, "password123")) {
        std::cout << "Authentication successful for " << user1.username << ".\n";
        user1.viewProfile();
    } else {
        std::cout << "Authentication failed for " << user1.username << ".\n";
    }

    if (authManager.authenticateUser(&user2, "wrong_password")) {
        std::cout << "Authentication successful for " << user2.username << ".\n";
        user2.viewProfile();
    } else {
        std::cout << "Authentication failed for " << user2.username << ".\n";
    }

    // Example: Viewing group/organization details
    std::cout << "Group Name: " << group1.name << "\n"
              << "Description: " << group1.description << "\n"
              << "Administrator: " << group1.administrator->username << "\n";

    return 0;
}
