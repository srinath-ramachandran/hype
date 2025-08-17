# Design Pattern and Use Descriptions
## GRASP Patterns
### Controller
Classes like DeviceManager, UserManager, and AutomationEngine control application logic and coordinate between UI/API and entities. These classes offer a clear medium and division of responsiblities, and take over a lot of the tasks that the Device, User or the Automation Rule itself has to carry out. The controller design also ensures less coupling and high cohesion, and ensures high testability
### Information Expert
Each class is responsible for its own data (e.g., Device manages its state and behavior). THe logic is placed along with the data that is needed to carry out the logic. 
### Creator 
UserManager creates User objects, DeviceManager creates Devices, etc. This ensures that the appropriate class creates the objects that are needed. 

## SOLID Principles
### Single Responsibility 
Each class has a clear, focused responsibility (e.g., SecurityAlert only manages alerts) inorder to promote less coupling and high cohesion.
### Open/Closed Principle
Adding new device or user types means subclassing, not modifying core logic. Promotes extension as opposed to modification of core logic. 
### Liskov Substitution 
All subclasses can be used wherever the parent class is expected (e.g., Sensor/Actuator as Device).
### Interface Segregation
Interface seggregation is not applied right off the bat, but if interfaces are to be used, they can be made to be focused (e.g., INotifiable, IRule, etc).
### Dependency Inversion
High-level modules are made to be dependent on abstractions (e.g., notification channels). This promotes testability and flexibility. 

## GoF (Gang Of Four) Design Patterns
### Factory Method
Used for creating objects like User or Device based on type. This decision avoids scattered object creation logic and offers more control over object creation.
### Observer 
AutomationRule observes Events and triggers actions. The observer pattern here is used to decouple event producers and consumers.
### Strategy 
Different evaluation or action strategies for automation rules. The strategy pattern in this design is used to promote runtime selection of behaviors. 
### Composite 
The composite pattern is not incorporated in the design as of yet, but it can be used to group actions if actions can further be grouped. 

## Microservices
### API Gateway
All client communication beyond the Cloudfront CDN instance goes through a single API gateway. This way, the access to the internal system mechanisms are centralized and secure. 
