**Завдання 1**

Dog
```csharp
class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    String makeSound() {
        return "Гав-гав!";
    }
}
```
Cat
```csharp
class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }

    @Override
    String makeSound() {
        return "Мяу!";
    }
}
```
Main
```csharp
public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog("Рекс");
        Animal cat = new Cat("Мурчик");

        System.out.println(dog.getName() + ": " + dog.makeSound());
        System.out.println(cat.getName() + ": " + cat.makeSound());
    }
}
```
**Завдання 2**

Point
```csharp
class Point implements Movable {
    private double x;
    private double y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public void setX(double x) {
        this.x = x;
    }

    @Override
    public void setY(double y) {
        this.y = y;
    }

    @Override
    public double getX() {
        return x;
    }

    @Override
    public double getY() {
        return y;
    }

    @Override
    public void moveTo(double x, double y) {
        this.x = x;
        this.y = y;
    }
}
```
**Завдання 3**

Smartphone
```csharp
class Smartphone implements GPS, Cellular {
    private double latitude;
    private double longitude;

    public Smartphone(double latitude, double longitude) {
        this.latitude = latitude;
        this.longitude = longitude;
    }

    @Override
    public double[] getCoordinates() {
        return new double[]{latitude, longitude};
    }

    @Override
    public void makeCall() {
        System.out.println("Здійснення дзвінка...");
    }

    @Override
    public void receiveCall() {
        System.out.println("Вхідний дзвінок...");
    }
}
```
**Завдання 4**

Car
```csharp
class Car implements Comparable {
    private int price;
    private int year;
    private int horsePower;

    public Car(int price, int year, int horsePower) {
        this.price = price;
        this.year = year;
        this.horsePower = horsePower;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public int getHorsePower() {
        return horsePower;
    }

    public void setHorsePower(int horsePower) {
        this.horsePower = horsePower;
    }

    @Override
    public int compareTo(Object obj) {
        Car other = (Car) obj;

        if (price != other.price) {
            return other.price - price;
        }

        if (year != other.year) {
            return year - other.year;
        }

        return horsePower - other.horsePower;
    }
}
```
