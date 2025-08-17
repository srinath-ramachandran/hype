# Skeleton Classes
## User
``` cpp
#pragma once
#include <string>
#include <vector>
#include <memory>

enum class UserRole { HOMEOWNER, PROPERTY_MANAGER, CHILD, GUEST };
enum class UserStatus { ACTIVE, SUSPENDED, DEACTIVATED };

class User {
protected:
    std::string userId;
    std::string name;
    std::string email;
    std::string passwordHash;
    UserRole role;
    UserStatus status;
public:
    virtual bool authenticate(const std::string& password) const = 0;
    virtual void suspend(const std::string& reason);
    virtual void activate();
    virtual void deactivate();
    virtual ~User() = default;
};

class Homeowner : public User {
public:
    void approveRule(const std::string& ruleId);
    void addDevice(const std::string& deviceId);
};

class PropertyManager : public User {
public:
    void assignDevice(const std::string& deviceId, const std::string& userId);
};

class Child : public User {
    // Add parental control settings as needed
};

class Guest : public User {
    std::string accessStart;
    std::string accessEnd;
};
```
