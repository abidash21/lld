Builder Design Pattern
- Helps in constructing complex object step by step
- Ideal when objects has many attributes or optional fields
- Allows to create different configurations of the object easily and clearly
- Traditionally we use constructors to create objects
- Constructors ensures objects are created in a valid state right when they are instantiated
- Helps in initialize an object with necessary values, guarantee that all required properties are setup immediately

```java
class User {
    String name;
    String email;
    String phone;
    String address;
    int age;

    User(String name) {
        this.name = name;
    }

    User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    User(String name, String email, String phone) {
        this.name = name;
        this.email = email;
        this.phone = phone;
    }

    User(String name, String email, String phone, String address) {
        this.name = name;
        this.email = email;
        this.phone = phone;
        this.address = address;
    }

    User(String name, String email, String phone, String address, int age) {
        this.name = name;
        this.email = email;
        this.phone = phone;
        this.address = address;
        this.age = age;
    }
}

problems:
1. Passing unncessary values - must pass values for all parameters 
2. Constructor overloading and huge combination - If there are many optional attributes then there would be multiple constructors,
   each for different combinations of parameters
3. Lack of readability

- The builder is responsible for assembling an object. We control the process by setting attributes one by one. Instead of passing all parameters in a 
  constructor, we pass the only the ones we care about and builder takes care of the rest

class User {
    private final string name;
    private final string email;
    private final string phone;
    private final string address;
    private final int age;

    private User(Builder builder) {
        this.name = builder.name;
        this.email = builder.email;
        this.phone = builder.phone;
        this.address = builder.address;
        this.age = builder.age;
    }

    public string getName(){
        return name;
    }

    public string getEmail(){
        return email;
    }

    public string getPhone(){
        return phone;   
    }

    public string getAddress(){
        return address;
    }

    public string getAge(){
        return age;
    }

    public static class Builder(){
        private final string name;
        private string email;
        private string phone;
        private string address;
        private int age;

        public Builder(String name){
            this.name = name;
        }

        public Builder email(String email){
            this.email = email
            return this;
        }
        public Builder phone(String phone){
            this.phone = phone
            return this;
        }
        public Builder address(String address){
            this.address = address
            return this;
        }
        public Builder age(int age){
            this.age = age
            return this;
        }

        public User build(){
            return new User(this);
        }
    }
}

public class Main {
    public static void main(String[] args){
        User user = new User.Builder("Abinash")
                .email("abinash@email.com")
                .phone("9999999999")
                .age(25)
                .build();

    }
}



Why builder is nested in the User class?
1. Encapsulation - tightly related to the car class and builder is for creating car objects
2. Access to private field without using getter and setter method
3. Logical grouping

Why is the builder static?
1. Builder doesn't need an instance of user to create new one, we can use builder directly.
2. The static builder allows clients to create a user object directly with User.Builder() without needing a separate builder instance.