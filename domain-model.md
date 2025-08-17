# Domain Model

| Conceptual Class Category                           | Example for hype System                  |
|-----------------------------------------------------|------------------------------------------|
| **Physical or Tangible Objects**                    | Device, Sensor, Actuator, Hub, Room      |
| **Specifications, Designs or Descriptions of Things**| DeviceType, DeviceModel, DeviceProfile   |
| **Places**                                          | Home, Room, Zone                         |
| **Transactions**                                    | DeviceRegistration, AutomationRun, AlertEvent |
| **Transaction Line Items**                          | AutomationAction, DeviceCommand          |
| **Roles of People**                                 | Homeowner, Guest, Child, PropertyManager |
| **Containers of Other Things**                      | DeviceGroup, Room, Home, AutomationRuleSet |
| **Things in a Container**                           | Device in Room, AutomationRule in RuleSet, Devices in Device Repository|
| **Other Computers/Systems (external)**              | NotificationService, ManufacturerCloud, UserMgmtService, MobileApp |
| **Abstract Noun Concepts**                          | Permission, Status, Notification, Alert  |
| **Organizations**                                   | ServiceProvider, Manufacturer            |
| **Events**                                          | SecurityAlert, DeviceEvent, AutomationTrigger |
| **Processes**                                       | DeviceOnboarding, RuleExecution          |
| **Rules and Policies**                              | AutomationRule, AccessPolicy             |
| **Catalogs**                                        | DeviceCatalog, UserDirectory             |
| **Records of Finance, Work, Contracts, Legal, etc.**| AccessLog, AuditTrail                    |
| **Financial Instruments and Services**              | SubscriptionPlan                         |
| **Manuals, Books, Documents, Reference Papers**     | DeviceManual, HelpDocument               |

---

| Good Classes (Retained) | Bad Classes (Pruned) (with Rationale) |
|-------------------------|--------------------------------------|
| Device                  | DeviceManual (not essential to core automation) |
| Sensor                  | DeviceType, DeviceModel (better as attributes of Device) |
| Actuator                | AccessLog (not essential to core automation) |
| Home                    | DeviceCatalog (external resource, not a domain object) |
| Room                    | HelpDocument (not essential to core automation) |
| AutomationRule          | SubscriptionPlan (this is a business concern, not core automation) |
| User                    | ServiceProvider, Manufacturer (external/metadata) |
| Role                    | DeviceProfile (redundant with Device attributes) |
| Permission              | AuditTrail (system-level, not part of core automation) |
| DeviceGroup             | UserDirectory (not core automation) |
| Notification            | Zone (redundant since room is a part of the domain) |
| Alert                   | Status (useful as an attribute, not class) |
| DeviceCommand           | AutomationRuleSet (several AutomationRule selected in domain will represent this) |
| DeviceEvent             | AccessPolicy (covered by Role/Permission) |
| SecurityAlert           | DeviceOnboarding, RuleExecution (processes derived from use cases, captured in events already) |
| AutomationAction        | DeviceRegistration (captured in events) |
| Homeowner               |                                    |
| Guest                   |                                    |
| Child                   |                                    |
| PropertyManager         |                                    |

**Rationales:**  
- Pruned classes are either implementation details, metadata, external catalogs, or better represented as attributes or collections rather than classes.
- Good classes are those that are central to the domain and appear in essential use cases.
- 

## [Back to Home](https://sxr3455.github.io/hype/)
