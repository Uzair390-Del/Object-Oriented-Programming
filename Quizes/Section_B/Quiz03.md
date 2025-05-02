# Task Description

Create a base class named **Temperature** that:

- Has a private float member `celsius` representing temperature in Celsius.
- Overloads the unary `-` operator to return a `Temperature` object with the negative of the current temperature.
- Overloads the binary `+` operator to add two `Temperature` objects (add their Celsius values).
- Overloads the comparison operator `>` to compare two `Temperature` objects.
- Has a public member function `display()` to print the temperature in Celsius with a "°C" suffix.

Create a derived class named **ExtendedTemperature** that:

- Publicly inherits from `Temperature`.
- Adds a member function `toFahrenheit()` that returns the temperature converted to Fahrenheit.
- Adds a member function `increase(float delta)` that increases the temperature by `delta` degrees Celsius.

---

# Requirements

- Implement all operator overloads inside the `Temperature` class.
- Use public inheritance for `ExtendedTemperature`.
- Demonstrate the following in `main()`:
  - Create two `Temperature` objects and add them using `+`.
  - Negate a `Temperature` object using unary `-`.
  - Compare two `Temperature` objects using `>`.
  - Create an `ExtendedTemperature` object, display its Celsius and Fahrenheit values, increase its temperature, and display the updated temperature.

---

# Sample Output
```cpp
Temperature 1: 25°C
Temperature 2: 30°C
Sum: 55°C
Negation of Temperature 1: -25°C
Is Temperature 2 > Temperature 1? Yes

ExtendedTemperature value: 20°C
In Fahrenheit: 68°F
Increasing temperature by 5°C...
New temperature: 25°C
```