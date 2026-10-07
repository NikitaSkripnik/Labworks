**Частина А**

Способи зламати:
```java
SmartLamp lamp = new SmartLamp(true, 100);
lamp.increaseBrightness(100); //Стане 200, проте за умовою не має
```
```java
SmartLamp lamp = new SmartLamp(true, 100);
lamp.increaseBrightness(-50); //Стане 50, проте за умовою не має
```
```java
SmartLamp lamp = new SmartLamp(true, 100);
lamp.on = false; //Спрацює, проте ми не можемо зовні змінювати цей стан
```

Виправлений код

```java
class SmartLamp {
    private boolean on;
    public int brightness;

    public SmartLamp(boolean on, int brightness) {
        this.on = on;
        this.brightness = brightness;
        if(this.brightness > 100)this.brightness=100;
        else if(this.brightness<0)this.brightness=0;
    }

    public void turnOn() {
        on = true;
    }

    public void turnOff() {
        on = false;
    }

    public boolean IsOn(){ return on; }

    public void increaseBrightness(int value) {
        if(value>0) {
            brightness += value;
            if (brightness > 100) brightness = 100;
        }
    }

    public void decreaseBrightness(int value) {
        if(value>0) {
            brightness -= value;
            if (brightness < 0) brightness = 0;
        }
    }

    public int getBrightness() {
        return brightness;
    }
}
```
**Частина Б**

Виправлений мною варіант:

Я ввів поле level, що змінюється від 0 до 1. У нього конвертуються значення, що задаються
```java
class SmartLamp {
    private boolean on;
    public double level;

    public SmartLamp(boolean on, int brightness) {
        this.on = on;
        this.level = brightness/100.0;
        if(this.level > 1)this.level=1;
        else if(this.level<0)this.level=0;
    }

    public void turnOn() {
        on = true;
    }

    public void turnOff() {
        on = false;
    }

    public boolean IsOn(){ return on; }

    public void increaseBrightness(int value) {
        if(value>0) {
            level += value/100.0;
            if (level > 1) level = 1;
        }
    }

    public void decreaseBrightness(int value) {
        if(value>0) {
            level -= value/100.0;
            if (level < 0) level = 0;
        }
    }

    public int getBrightness() {
        return (int)(level * 100.0);
    }
}
```

Відповідь ШІ:
```
Варіант 1 — зберігати яскравість як коефіцієнт

Замість int brightness можна використати double level, який зберігає яскравість у діапазоні 0.0–1.0. Наприклад, яскравість 70 буде представлена як 0.7. Публічні методи increaseBrightness(), decreaseBrightness() та getBrightness() перетворюватимуть це значення у звичний діапазон 0–100.

Варіант 2 — зберігати яскравість через кількість рівнів

Можна не зберігати саме значення яскравості 0–100, а зберігати внутрішній індекс рівня, наприклад brightnessLevel у діапазоні 0–20. Один рівень відповідатиме 5% яскравості: brightnessLevel = 14 означатиме яскравість 70. Публічні методи працюватимуть зі значеннями 0–100, а всередині вони перетворюватимуть їх на відповідний рівень.
```

**Частина В**

Клас: 
```java
class GameCharacter {
    private int health;
    private int maxHealth;
    private int energy;
    private int maxEnergy;

    public GameCharacter(int maxHealth, int maxEnergy) {
        if (maxHealth > 0) {
            this.maxHealth = maxHealth;
            this.health = maxHealth;
        } else {
            this.maxHealth = 1;
            this.health = 1;
        }

        if (maxEnergy > 0) {
            this.maxEnergy = maxEnergy;
            this.energy = maxEnergy;
        } else {
            this.maxEnergy = 1;
            this.energy = 1;
        }
    }

    public void takeDamage(int damage) {
        if (damage > 0) {
            health -= damage;

            if (health < 0) {
                health = 0;
            }
        }
    }

    public void heal(int amount) {
        if (amount > 0) {
            health += amount;

            if (health > maxHealth) {
                health = maxHealth;
            }
        }
    }

    public void spendEnergy(int amount) {
        if (amount <= energy) {
            energy -= amount;
        }
    }

    public void restoreEnergy(int amount) {
        if (amount > 0) {
            energy += amount;

            if (energy > maxEnergy) {
                energy = maxEnergy;
            }
        }
    }

    public int getHealth() {
        return health;
    }

    public int getEnergy() {
        return energy;
    }
}
```
Main:

```java
public class Main {
    public static void main(String[] args) {
        GameCharacter character = new GameCharacter(100, 50);

        System.out.println("Початковий стан:");
        System.out.println("Health: " + character.getHealth());
        System.out.println("Energy: " + character.getEnergy());

        character.takeDamage(30);
        character.spendEnergy(20);

        System.out.println("\nПісля звичайних операцій:");
        System.out.println("Health: " + character.getHealth());
        System.out.println("Energy: " + character.getEnergy());

        character.heal(100);
        character.restoreEnergy(100);

        System.out.println("\nПісля граничного відновлення:");
        System.out.println("Health: " + character.getHealth());
        System.out.println("Energy: " + character.getEnergy());

        character.takeDamage(200);
        character.spendEnergy(200);

        System.out.println("\nПісля недопустимо великої витрати:");
        System.out.println("Health: " + character.getHealth());
        System.out.println("Energy: " + character.getEnergy());
    }
}
```
