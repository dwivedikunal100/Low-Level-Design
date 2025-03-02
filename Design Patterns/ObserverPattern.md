# Observer Pattern in Java

The **Observer Pattern** is a software design pattern where an object (known as the subject) maintains a list of its dependents (observers), and notifies them automatically of any state changes, usually by calling one of their methods. It's often used to implement distributed event-handling systems.

## Key Components
1. **Subject**: The observable object that maintains a list of observers.
2. **Observer**: Interface implemented by all observer objects. Observers must provide an `update` method.
3. **Concrete Observer**: Classes that implement the `Observer` interface and define how they react to updates from the subject.

## Example Implementation

### Step 1: Define the Observable Class
```java
import java.util.ArrayList;
import java.util.List;

class WeatherStation {
    private List<Observer> observers = new ArrayList<>();
    private String weatherCondition;

    public void addObserver(Observer o) {
        observers.add(o);
    }

    public void removeObserver(Observer o) {
        observers.remove(o);
    }

    public void setWeather(String condition) {
        this.weatherCondition = condition;
        notifyObservers();
    }

    private void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(weatherCondition);
        }
    }
}
```

### Step 2: Define the Observer Interface
```java
interface Observer {
    void update(String weatherCondition);
}
```


### Step 3: Implement Concrete Observers
```java
class WeatherDisplay implements Observer {
    @Override
    public void update(String weatherCondition) {
        System.out.println("Weather Display: " + weatherCondition);
    }
}
```

### Main Class to Demonstrate the Pattern
```
public class Main {
    public static void main(String[] args) {
        // Create an observable object (subject)
        WeatherStation station = new WeatherStation();

        // Create observers and register them with the subject
        Observer display1 = new WeatherDisplay();
        Observer display2 = new WeatherDisplay();

        station.addObserver(display1);
        station.addObserver(display2);

        // Change the state of the subject, which notifies all registered observers
        station.setWeather("Sunny");
    }
}
```

### Summary
- **Subject**: Maintains a list of observers and notifies them when its state changes.
- **Observer Interface**: Defines an update method that observers must implement to receive notifications.
- **Concrete Observers**: Implement the observer interface and define how they react to updates.

This pattern allows for loose coupling between objects, enabling changes in one object to trigger updates in others without those objects needing to know about each other directly.