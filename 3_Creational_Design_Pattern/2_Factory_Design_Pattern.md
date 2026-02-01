FACTORY DESIGN PATTERN

```java
class EmailNotification {
    void send(){
        System.out.println("Sending Email")
    }
}

class SMSNotification {
    void send(){
        System.out.println("Sending SMS")
    }
}

class PushNotification {
    void send(){
        System.out.println("Sending Push Notification")
    }
}

public class NotificationService {
    public static void main(String args[]){
        String type = "EMAIL"

        if(type.equals("EMAIL") ){
            EmailNotification notice = new EmailNotification ()
            notice.send()
        } else if(type.equals("SMS") ){
            SMSNotification notice = new SMSNotification ()
            notice.send()
        } else if if(type.equals("PUSH") ){
            PushNotification notice = new xPushNotification()
            notice.send()
        }
    }
}

disadvantages:

- violates SRP
ex: NotificationService is doing two jobs, deciding which object to create and executing business logic

- violates OCP
ex: If a new notification type has to be add then we hae to modify existing code

else if (type.equals("WHATSAPP")) {
    WhatsAppNotification n = new WhatsAppNotification();
    n.send();
}

- LSP not applicable
ex: Client depends on concrete classes, no base class or common interface

- ISP not applicable 
ex: No interface, no forced methods exist

- violates DIP
ex: Highlevel class directly instantiates low level classes


Why factory Pattern?
=> It is named after "Factory" because, just like a factory produces different types of products, the pattern
   provides a central place to create object of different types

=> Instead of directly instantiating objects, the factory method is responsible for creating the correct object,
   making the system more flexible and organized
   
```java
interface Notification {
    void send();
}

class EmailNotification extends Notification {
    @override
    public void send {
         System.out.println("Sending Email Notification");
    }
}

class SMSNotification implements Notification {
    @Override
    public void send() {
        System.out.println("Sending SMS Notification");
    }
}

class PushNotification implements Notification {
    @Override
    public void send() {
        System.out.println("Sending Push Notification");
    }
}

class NotificationFactory {

    public static Notification getNotification(String type){

        if(type == null){
            throw new IllegalArgumentException("Notification type cannot be null");
        }

        switch( type.toUpperCase() ){
            case "EMAIL":
                return new EmailNotification();
            case "SMS":
                return new SMSNotification();
            case "PUSH":
                return new PushNotification();
            default:
                throw new IllegalArgumentException("Invalid notification type: " + type);
        }
    }
}

public class Main {
    public static void main(String[] args){
        Notification email = NotificationFactory.getNotification("EMAIL");
        email.send()
        Notification sms = NotificationFactory.etNotification("SMS");
        sms.send()
        Notification push = NotificationFactory.etNotification("PUSH");
        push.send()
    }
}



How this code satisfies SOLID Prinicples
1. SRP validated 
- EmailNotification sends email, SMSNotification sends sms , PushNotification sends push, NotificationFactory creates object, Main uses object
- Object creation and usage are separated

2. OCP validated
- If you consider "Simple Factory" pattern then, it is validated
- Adding new Whatsapp notification, we have to create separate class which will extend Notification
  In NotificationFactory, we have to add extra switch case in factory.
- Hence, it is fully respected for client and partially respected for factory. It is called "Simple Factory".
- In Factory Method Pattern the factory also validates the OCP rule, below is an example - the only change is how the factory is implemented

interface NotificationFactory {
    Notification createNotification();
}

class EmailNotificationFactory implements NotificationFactory {
    @Override
    public Notification createNotification() {
        return new EmailNotification();
    }
}

class SMSNotificationFactory implements NotificationFactory {
    @Override
    public Notification createNotification() {
        return new SMSNotification();
    }
}


3. LSP validated
- Client code does not care which subtype it gets as all subclasses implement Notification

4. ISP validated
- No unused methods, each class implements only what it needs.

5. DIP validated
- Client code depends on Notificagtion interface not on concrete classes like EmailNotification, SMSNotifcation 