# Skeleton Classes in C++
## User
``` cpp
#pragma once
#include <string>
#include <vector>
#include <memory>

class Role;

class User {
protected:
    std::string userId;
    std::string name;
    std::string email;
    std::string phone;
    std::vector<std::shared_ptr<Role>> roles;
public:
    virtual ~User() = default;
    virtual bool hasPermission(const std::string& permission) const = 0;
    virtual std::vector<std::shared_ptr<Role>> getRoles() const = 0;
};
```
## Role
``` cpp
#pragma once
#include <string>

class Role {
protected:
    std::string roleName;
    std::string description;
    int level;
public:
    std::string getDescription() const;
};
```
## Permission
``` cpp
#pragma once
#include <string>

class Permission {
protected:
    std::string permissionName;
    std::string description;
    bool granted;
public:
    bool isGranted() const;
};
```
## Child
``` cpp
#pragma once
#include "User.h"

class Child : public User {
    bool isAccessControlled;
public:
    // Inherited methods to be implemented
    bool hasPermission(const std::string& permission) const override;
    std::vector<std::shared_ptr<Role>> getRoles() const override;
};
```
## Guest
``` cpp
#pragma once
#include "User.h"
#include <string>

class Guest : public User {
    std::string guestCode;
    std::string accessDuration;
public:
    std::string getGuestCode() const;
    bool isCurrentGuest() const;
    // Inherited methods to be implemented
    bool hasPermission(const std::string& permission) const override;
    std::vector<std::shared_ptr<Role>> getRoles() const override;
};
```
## PropertyManager
``` cpp
#pragma once
#include "User.h"
#include <string>

class PropertyManager : public User {
    std::string company;
    std::string managerId;
public:
    std::string getCompany() const;
    std::string getManagerId() const;
    // Inherited methods to be implemented
    bool hasPermission(const std::string& permission) const override;
    std::vector<std::shared_ptr<Role>> getRoles() const override;
};
```
## Homeowner
``` cpp
#pragma once
#include "User.h"
#include <string>

class Homeowner : public User {
    std::string preferredLanguage;
public:
    void setPreferredLanguage(const std::string& language);
    // Inherited methods to be implemented
    bool hasPermission(const std::string& permission) const override;
    std::vector<std::shared_ptr<Role>> getRoles() const override;
};
```
## Home
``` cpp
#pragma once
#include <string>
#include <vector>
#include <memory>

class Room; // forward declaration
class Homeowner;

class Home {
    std::string homeId;
    std::string address;
    std::string name;
    std::shared_ptr<Homeowner> owner;
    std::vector<std::shared_ptr<Room>> rooms;
public:
    std::vector<std::shared_ptr<Room>> getRooms() const;
    std::shared_ptr<Homeowner> getOwner() const;
};
```
## Room
``` cpp
#pragma once
#include <string>
#include <vector>
#include <memory>

class Device; // forward declaration

class Room {
    std::string roomId;
    std::string name;
    int floor;
    std::string type;
    std::vector<std::shared_ptr<Device>> devices;
public:
    std::vector<std::shared_ptr<Device>> getDevices() const;
    void addDevice(const std::shared_ptr<Device>& device);
};
```
## DeviceGroup
```cpp
#pragma once
#include <string>
#include <vector>
#include <memory>

class Device; // forward declaration

class DeviceGroup {
    std::string groupId;
    std::string name;
    std::vector<std::shared_ptr<Device>> devices;
public:
    std::vector<std::shared_ptr<Device>> getDevices() const;
    void addDevice(const std::shared_ptr<Device>& dev);
};
```
## DeviceStatus Enum
``` cpp
#pragma once

enum class DeviceStatus {
    ONLINE,
    OFFLINE,
    MALFUNCTION
};
```
## DeviceType Enum
``` cpp
#pragma once

enum class DeviceType {
    SENSOR,
    ACTUATOR,
    HYBRID
};
```
## Device
``` cpp
#pragma once
#include <string>
#include <vector>
#include <memory>
#include "DeviceStatus.h"
#include "DeviceType.h"

class DeviceCommand; // forward declaration

class Device {
protected:
    std::string deviceId;
    std::string name;
    DeviceStatus status;
    std::string location;
    std::string lastCommunication;
    DeviceType deviceType;
public:
    virtual bool sendCommand(const DeviceCommand& deviceCommand) = 0;
    virtual DeviceStatus getStatus() const = 0;
    virtual ~Device() = default;
};
```
## Sensor
``` cpp
#pragma once
#include "Device.h"
#include <string>

class Sensor : public Device {
    std::string sensorType;
    std::string unit;
    float value;
public:
    float readValue();
    // Device methods to be implemented
    bool sendCommand(const DeviceCommand& deviceCommand) override;
    DeviceStatus getStatus() const override;
};
```
## Actuator
``` cpp
#pragma once
#include "Device.h"
#include <string>

class Actuator : public Device {
    std::string actuatorType;
    std::string state;
    std::string lastActionTime;
public:
    bool activate();
    std::string getState() const;
    // Device methods to be implemented
    bool sendCommand(const DeviceCommand& deviceCommand) override;
    DeviceStatus getStatus() const override;
};
```
## DeviceEvent
``` cpp
#pragma once
#include <string>
#include <memory>

class Device;

class DeviceEvent {
    std::string eventId;
    std::string eventType;
    std::string occuredAt;
    std::shared_ptr<Device> device;
public:
    std::shared_ptr<Device> getDevice() const;
};
```
## AutomationRule
``` cpp
#pragma once
#include <string>
#include <vector>
#include <memory>

class AutomationAction; // forward declaration

class AutomationRule {
    std::string ruleId;
    std::string description;
    bool isActive;
    std::string triggerTime;
    std::vector<std::shared_ptr<AutomationAction>> actions;
public:
    bool evaluate();
    std::vector<std::shared_ptr<AutomationAction>> getActions() const;
};
```
## AutomationAction
``` cpp
#pragma once
#include <string>

class AutomationAction {
    std::string actionId;
    std::string description;
    std::string actionType;
    std::string parameters;
public:
    bool execute();
};
```
## DeviceCommand
``` cpp
#pragma once
#include <string>

class DeviceCommand {
    std::string commandId;
    std::string commandType;
    std::string parameters;
public:
    std::string getParameters() const;
};
```
## Notification
``` cpp
#pragma once
#include <string>

class Notification {
    std::string notificationId;
    std::string type;
    std::string timestamp;
    std::string message;
    bool isRead;
public:
    void markRead();
    std::string getMessage() const;
};
```
## Alert
``` cpp
#pragma once
#include <string>

class Alert {
    std::string alertId;
    std::string type;
    int priority;
    std::string timestamp;
    std::string description;
public:
    std::string getDescription() const;
};
```
## SecurityAlert
``` cpp
#pragma once
#include "Alert.h"
#include <string>

class SecurityAlert : public Alert {
    std::string severity;
    std::string detectedAt;
    std::string location;
public:
    std::string getSeverity() const;
};
```
