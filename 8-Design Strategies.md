## Introduction
### How to achieve Quality Goals
1. Develop high-level solution strategies in parallel to the detailed concepts (e.g.; cross-cutting concepts, funtional and technical components, etc)
2. Use principles, patterns in creating the solution strategies
3. No single approach that gaurantees a suitable solution

## High Performance
```mermaid
  mindmap
    root (Strategies for High Performance)
      Additional Hardware
        Scaling-up
        Scaling-out
      Reduce comms between system components
        Caching
        Batching
      Appropriate distribution
        Increase Distribution
          Database Sharding
      Reduce flexibility of the system
      Perform Load Tests
        Frequent
      Compromise on Energy Efficiency
        Last Choice
        Depends on industry context
        Options
          Buying / renting high-end hardware
          Disabling power mgmt features
          Increase parallism
            Running on multiple GPUs
            Distribute computing on multiple computers
```
### Reduce Flexibility
Following solution has lot of flexbility;
1. minimumAmount of txn is configurable - and is read from external config file
2. we allow user to perform txn in currency of their choice - involves currency conversion
3. fee we collect for txn is  also externally configurable - here coming from db

Each of these flexibility increases latency.
```
  public class TransactionProcessor {
      ...
      // In real world, amount should be of type BigDecimal
      public boolean processTransaction(String type, double amount, String currency) {
          if (amount < config.getJSONObject("minimumAmount").getDouble(currency)) {
              LOGGER.info("Txn amount is below the min");
              return false;
          }
          double fee = database.getCurrentFee(type, currency);
          double netAmount = amount - fee;
          if (netAmount <= 0) {
              LOGGER.info("Txn amount is too low to cover the fees");
              return false;
          }
          ...
      }
  }
```
The solution with reduced flexibility. Need to strike a right balance when reducing flexibility.
```
  public class TransactionProcessor {
      ...
      // In real world, amount should be of type BigDecimal
      private static final double MINIMUM_AMOUNT_USD = 10;
      private static final double WITHDRAWAL_FEE_USD = 2;
      private static final double TRANSFER_FEE_USD = 3;
      public boolean processTransaction(String type, double amount) {
          if (amount < MINIMUM_AMOUNT_USD) {
              LOGGER.info("Txn amount is below the min");
              return false;
          }
          double fee = (type.equals("withdrawal")) ? WITHDRAWAL_FEE_USD : TRANSFER_FEE_USD;
          double netAmount = amount - fee;
          if (netAmount <= 0) {
              LOGGER.info("Txn amount is too low to cover the fees");
              return false;
          }
          ...
      }
  }
```

## Adaptibility & Flexibility
```mermaid
  mindmap
    root (Strategies for Adaptability and Flexibility)
      Determine where the system needs to be flexible
        Functionality Flexibility
          Strategy Pattern
          Feature Flags
        Data structures and data model
          Using schemaless formats (JSON)
          Using NoSQL DBs (MongoDB, etc)
        Use of third-party software or interfaces with other systems
          Facade Pattern
        User Interface
          Responsive Design
        Target Platform
          Cross platform technologies / programming languages (java, python)
          Containerization technologies (Docker)
      Use configuration files
          Env specific settings
          Externalize credentials, Api keys, etc
          Control App resources (number of threads, connections, cache settings, message queue, etc)
      Keep changes local
          SRC, High Cohesion, Modularity
          One database per microservice
      Using polymorphism in OO systems
      Use Information Hiding
      Decouple system components as much as possible
      Use understandable and maintainable code
```
### Funtionality Flexibility - Strategy Pattern
```mermaid
    classDiagram
        PaymentProcessor --> PaymentStrategy : uses
        CreditCardPayment ..|> PaymentStrategy : implements
        PaypalPayment ..|> PaymentStrategy : implements
        BankTransfer ..|> PaymentStrategy : implements

        class PaymentProcessor {
          -strategy:PaymentStrategy
          +setPaymentStrategy(strategy:PaymentStrategy):void
          +executePayment(amount:double):void
        }
        class PaymentStrategy {
          <<interface>>
          +pay(amount:double):void
        }
        class CreditCardPayment {
           +pay(amount:double):void
        }
        class PaypalPayment {
           +pay(amount:double):void
        }
        class BankTransfer {
           +pay(amount:double):void
        }
```
```
    public class PaymentProcessor {
        private PaymentStrategy strategy;
        //Point of flexibility. Allows us to change the implementation details at runtime
        public void setPaymentStrategy (PaymentStrategy strategy) {
          this.strategy = strategy;
        }
        public void executePayment(double amount) {
          strategy.pay(amount);
        }
    }
```
### Funtionality Flexibility - Feature Flags
```
  public void displayUserProfile() {
      if (config.isEnhancedProfileEnabled()) {
        displayEnhancedUserProfile(user);
      } else {
        displayBasicUserProfile(user);
      }
  }
```
### Facade Pattern (Used as Anti Corruption Layer)
```mermaid
    classDiagram
        UserProfile --> StorageFacade : uses
        StorageFacade --> Credentials : uses
        StorageFacade --> ConfigurationManager : uses
        StorageFacade --> DataStorage : uses

        class UserProfile {
          <<web application>>
          +uploadImage(file:File):void
          +downloadImage(fileNmae:String):File
        }
        class StorageFacade {
          <<facade>>
          +uploadFile(file:File):void
          +downloadFile(fileNmae:String):File
        }
        class Credentials {
          <<third-party storage lib>>
           +getAccessKey():String
           +getSecretKey():String
        }
        class ConfigurationManager {
          <<third-party storage lib>>
           +configure(settings:Properties):void
        }
        class DataStorage {
          <<third-party storage lib>>
           +putObject(credentials:Credentails, bucketName: String, fileName:String, file:File):void
           +getObject(credentials:Credentails, bucketName: String, fileName:String):File
        }
```
### Polymorphism
1. Allows objects of a different classes to be treated as objects of common superclass.
2. Enables flexibility to perform the same action on different objects with different implementations
```mermaid
    classDiagram
        EmailNotification ..|> Notification : implements
        SmsNotification ..|> Notification : implements
        AppNotification ..|> Notification : implements

       class Notification {
          <<interface>>
          +send(message:String):void
        }
        class EmailNotification {
          +send(message:String):void        }
        class SmsNotification {
          +send(message:String):void        }
        class AppNotification {
          +send(message:String):void        }
```
```
    public class NotificationService {
        public void sendAnnouncement(List<Notification> notifications, String message) {
          for(Notification notification : notifications)
              notification.send(message);
        } 
    }
```
  
## High Availability
```mermaid
    mindmap
      root(Strategies for High Availability)
        Error Prevention
          Use Transactions in database operations
          Input Validation
          Eliminating Performance Bottlenecks
            Backpressure in pipes and filters architecture
        Error Detection
          Monitoring
            Critical Metrics
            Visually and Programmatically
            Examples
              Uptime
              Incoming Http requests/sec
              Error rate
              CPU / Memory utilization
              Error status codes
          Validating Accuracy of Results
        Error Handling
          Robust Exception Handling
            Retry
            Connect to alternate provider
            If all fails, log task or put it in failed tasks queue
          Rollback
            Transaction Rollback
            Release Rollback
          Eliminating Single Point of Failure
          Automatic detection and replacement of faulty instance
```
### Validating Accuracy
Running 2nd Analytics process that runs on a schedule and counts all the accout balances of all the customers & adds the total net wire-transfers in and out of our bank to ensure no money is missing without any paper trace.
![Validating Accuracy!](/validate_accuracy.png)
