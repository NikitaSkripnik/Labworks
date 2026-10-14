**Завдання 1**
```csharp
public class TimeSpan {
    private int hours;
    private int minutes;

    public TimeSpan() {
        this.hours = 0;
        this.minutes = 0;
    }

    public TimeSpan(int minutes) {
        if (minutes < 0) {
            this.hours = 0;
            this.minutes = 0;
            return;
        }

        this.hours = minutes / 60;
        this.minutes = minutes % 60;
    }

    public TimeSpan(int hours, int minutes) {
        if (hours < 0 || minutes < 0 || minutes > 59) {
            this.hours = 0;
            this.minutes = 0;
            return;
        }

        this.hours = hours;
        this.minutes = minutes;
    }

    public TimeSpan(TimeSpan span) {
        this.hours = span.getHours();
        this.minutes = span.getMinutes();
    }

    public int getHours() {
        return hours;
    }

    public int getMinutes() {
        return minutes;
    }

    private void normalize() {
        hours += minutes / 60;
        minutes %= 60;
    }

    public void add(int hours, int minutes) {
        if (hours < 0 || minutes < 0 || minutes > 59) {
            return;
        }

        this.hours += hours;
        this.minutes += minutes;
        normalize();
    }

    public void add(int minutes) {
        if (minutes < 0) {
            return;
        }

        this.minutes += minutes;
        normalize();
    }

    public void add(TimeSpan span) {
        add(span.getHours(), span.getMinutes());
    }

    private void setTotalMinutes(int totalMinutes) {
        hours = totalMinutes / 60;
        minutes = totalMinutes % 60;
    }

    public void subtract(int hours, int minutes) {
        if (hours < 0 || minutes < 0 || minutes > 59) {
            return;
        }

        int current = getTotalMinutes();
        int value = hours * 60 + minutes;

        if (value <= current) {
            setTotalMinutes(current - value);
        }
    }

    public void subtract(int minutes) {
        if (minutes < 0) {
            return;
        }

        int current = getTotalMinutes();

        if (minutes <= current) {
            setTotalMinutes(current - minutes);
        }
    }

    public void subtract(TimeSpan span) {
        subtract(span.getTotalMinutes());
    }

    public double getTotalHours() {
        return getTotalMinutes() / 60.0;
    }

    public int getTotalMinutes() {
        return hours * 60 + minutes;
    }

    public void scale(int factor) {
        if (factor <= 0) {
            return;
        }

        setTotalMinutes(getTotalMinutes() * factor);
    }
}
```
**Завдання 2**
Person
```csharp
public class Person {
    private String surname;
    private String name;
    private int age;

    public Person(String surname, String name, int age) {
        this.surname = surname;
        this.name = name;
        this.age = age;
    }

    public String getSurname() {
        return surname;
    }

    public void setSurname(String surname) {
        this.surname = surname;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Людина " + surname + " " + name + ", вік: " + age;
    }
}
```
Student
```csharp
public class Student extends Person {
    private String group;
    private String studentId;

    public Student(String surname, String name, int age, String group, String studentId) {
        super(surname, name, age);
        this.group = group;
        this.studentId = studentId;
    }

    public String getGroup() {
        return group;
    }

    public void setGroup(String group) {
        this.group = group;
    }

    public String getStudentId() {
        return studentId;
    }

    public void setStudentId(String studentId) {
        this.studentId = studentId;
    }

    @Override
    public String toString() {
        return "Студент групи " + group + ", " + getSurname() + " " + getName() + ", вік: " + getAge() + ". Номер студентського квитка: " + studentId;
    }
}
```
Lectuer
```csharp
public class Lecturer extends Person {
    private String department;
    private double salary;

    public Lecturer(String surname, String name, int age, String department, double salary) {
        super(surname, name, age);
        this.department = department;
        this.salary = salary;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String toString() {
        return "Викладач кафедри " + department + ", " + getSurname() + " " + getName() + ", вік: " + getAge() + ". Зарплата: " + salary;
    }
}
```
Main
```csharp
public class Main {
    public static void main(String[] args) {
        Person person = new Person("Шевченко", "Олег", 30);

        Student student1 = new Student("Іваненко", "Андрій", 19, "АІ-251", "12345");
        Student student2 = new Student("Петренко", "Марія", 20, "АІ-252", "67890");
        Lecturer lecturer1 = new Lecturer("Коваленко", "Олена", 45, "Інформатики", 25000);
        Lecturer lecturer2 = new Lecturer("Бондаренко", "Ігор", 50, "Математики", 30000);
        Person[] people = {person, student1, student2, lecturer1, lecturer2};

        for (Person p : people) {
            System.out.println(p.toString());
        }
    }
}
```
