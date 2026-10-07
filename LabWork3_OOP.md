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
    }

    public void turnOn() {
        on = true;
    }

    public void turnOff() {
        on = false;
    }

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
** Частина Б**
