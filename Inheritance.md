# Inheritance

In Java language, a class can de derived from another class, that means it can inherit fields and methods from that class.

Here we have some short but important definitions:
- Subclass  
    It's the class that is derived from another class, also known as *derived class, extended class or child class*.
- Superclass    
    It's the class from the subclass is derived, also known as *base class or parent class*.

A class only have one direct superclass except *Object* class, which doesn't have it.

**So, What does inheritance mean?**     
Inheritance in Java allows us to create a class derived from existing class and doing this we can reuse fields and methods from the existing one.

A subclass inherits fields, methods and nested classes from its superclass except a constructor but the superclass constructor can be invoked from the subclass.

## Subclass
A subclass inherits all the protected and public members of its parent.    

**Note:**       
A subclass does not inherit the private members of its parent class. However, if the superclass has public or protected methods for accessing its private fields, these can also be used by the subclass. (The Java Tutorial)


Example:    
- This is the Person Class.
    ```Java
    public class Person {
        private String firstName;
        private String lastName;
        private int age;
        private String country;
        
        public Person(String firstName, String lastName, int age, String country){
            this.firstName = firstName;
            this.lastName = lastName;
            this.age = age;
            this.country = country;
        }
        
        public String getFullData(){
            return "Full Name : "+this.getFirstName()+" "+this.getlastName()+"\nAge: "+
                    this.getAge()+"\nCountry: "+this.getCountry();
        }
        
        public String getFirstName() {
            return firstName;
        }

        public void setFirstName(String firstName) {
            this.firstName = firstName;
        }

        public String getlastName() {
            return lastName;
        }

        public void setlastName(String lastName) {
            this.lastName = lastName;
        }

        public int getAge() {
            return age;
        }

        public void setAge(int age) {
            this.age = age;
        }

        public String getCountry() {
            return country;
        }

        public void setCountry(String country) {
            this.country = country;
        }
        
    }
    ```
- This is Employee Class derived from Person Class.
    ```java
    public class Employee extends Person{
        private double salary;
        public Employee(String firstName, String lastName, int age, String country, double salary){
            super(firstName, lastName, age, country);
            this.salary = salary;
        }

        public double getSalary() {
            return salary;
        }

        public void setSalary(double salary) {
            this.salary = salary;
        }
        
    }
    ```

## Overriding
Overriding is a feature that allows a subclass to provide a specific implementation of a method that already exists in the superclass. In other words, when the subclass has a method with the same name as a method from the superclass, that method is overriding the method of the superclass.
```Java
public class Employee extends Person{
    private double salary;
    public Employee(String firstName, String lastName, int age, String country, double salary){
        super(firstName, lastName, age, country);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
    
    public String getFullData(){
        return super.getFullData()+"\nSalary: "+this.getSalary();
    }
    
}
```
In the above example, we can visualize that getFullData() method of Employee class is overriding the method of the superclass (Person).
## Casting with objects.

### Reference variable
First of all we need to undertand what reference variable is.
```Java
    // Creating a reference
    Person person2;
    // Creating a references and a Person object
    Person person3 = new Person("Luis", "Alberto", 23, "Colombia");
```
Casting with reference variables works differently than primitive conversions due to a reference variable only refers to an object but doesn't contain the object itself.
It only labels the object in another way.
### Upcasting
It refers to cast to a superclass and is always allowed. Upcasting narrows the list of methods and properties to the object.
### Downcasting
It refers to cast to a subclass and the type of the object must be declared. Downcasting extends the list of methods and properties to the object.

![Upcasting-Downcasting](https://i.stack.imgur.com/Lkn0S.png "Image of downcasting and upcasting explanation.")

Example:
```Java
Person person1 = new Person("Fabrizio", "Condori", 20, "Perú");
Employee employee1 = new Employee("Juan", "Velazco", 30, "Perú", 4350);

//upcasting
Person person2 = new Employee("Luis", "Felipe", 19, "Bolivia", 15000);

//downcasting
Employee employee3 = (Employee) person2;
```

## Polymorphism
Polymorphism is mostly used with classes that are related by inheritance, as we know, a class inherits attributes and methods from its superclass but with polymorphism, classes can use those methods to perform different actions.
Example:
```Java
Person person1 = new Person("Fabrizio", "Condori", 20, "Perú");
Employee employee1 = new Employee("Juan", "Velazco", 30, "Perú", 4350);
Person person2 = new Employee("Luis", "Felipe", 19, "Bolivia", 15000);

System.out.println(person1.getFullData());
/*output

Full Name : Fabrizio Condori
Age: 20
Country: Perú*/
System.out.println(employee1.getFullData());
/*output

Full Name : Juan Velazco
Age: 30
Country: Perú
Salary: 4350.0
*/
System.out.println(person2.getFullData());
/*output

Full Name : Luis Felipe
Age: 19
Country: Bolivia
Salary: 15000.0
*/
```
On the above example, there is a weird output from one example (person2 variable) because the variable's type is a Person object and the method getFullData() behave as if the object was a Employee object. 
This is because the Java Virtual Machine (JVM) calls the methods for the object that is referred to in each variable, it does not call the methods that is defined by the variable's type.

## References
- https://docs.oracle.com/javase/tutorial/java/IandI/index.html
- https://www.w3schools.com/java/java_polymorphism.asp
- https://www.baeldung.com/java-type-casting