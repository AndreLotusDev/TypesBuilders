# C# Builder Pattern Examples

This repository demonstrates the implementation of the Builder Pattern in C#. The Builder Pattern is a design pattern designed to provide a flexible solution to various object creation problems in object-oriented programming. It is especially useful when an object needs to be created with numerous possible configurations. In C#, the Builder Pattern can significantly enhance code readability and maintainability when dealing with complex objects. We cover two primary types of the Builder Pattern: **Traditional Builder** and **Fluent Builder**.

## Traditional Builder Pattern

The Traditional Builder Pattern separates the construction of a complex object from its representation, allowing the same construction process to create various representations. This pattern involves at least the following components:

- **Product**: The actual object that is being built.
- **Builder**: An abstract interface for creating parts of the Product object.
- **ConcreteBuilder**: Implements the Builder interface and provides an interface for getting the result.
- **Director**: Constructs an object using the Builder interface.

### Example

```csharp
// Product
public class Car
{
    public string Engine { get; set; }
    public int Wheels { get; set; }
    public string Color { get; set; }
}

// Builder
public interface ICarBuilder
{
    void BuildEngine();
    void BuildWheels();
    void BuildColor();
    Car GetCar();
}

// ConcreteBuilder
public class SedanBuilder : ICarBuilder
{
    private Car _car = new Car();

    public void BuildEngine()
    {
        _car.Engine = "V6";
    }

    public void BuildWheels()
    {
        _car.Wheels = 4;
    }

    public void BuildColor()
    {
        _car.Color = "Black";
    }

    public Car GetCar()
    {
        return _car;
    }
}

// Director
public class CarDirector
{
    private ICarBuilder _builder;

    public CarDirector(ICarBuilder builder)
    {
        _builder = builder;
    }

    public void Construct()
    {
        _builder.BuildEngine();
        _builder.BuildWheels();
        _builder.BuildColor();
    }

    public Car GetCar()
    {
        return _builder.GetCar();
    }
}
```

## Fluent Builder Pattern

The Fluent Builder Pattern is a variation of the Builder Pattern that uses method chaining to make the client code more readable. It's particularly useful when configuring an object with many optional configurations.

### Example

```csharp
public class CarBuilder
{
    private Car _car = new Car();

    public CarBuilder SetEngine(string engine)
    {
        _car.Engine = engine;
        return this;
    }

    public CarBuilder SetWheels(int wheels)
    {
        _car.Wheels = wheels;
        return this;
    }

    public CarBuilder SetColor(string color)
    {
        _car.Color = color;
        return this;
    }

    public Car Build()
    {
        return _car;
    }
}
```

## Usage

```csharp
var sedanBuilder = new SedanBuilder();
var carDirector = new CarDirector(sedanBuilder);
carDirector.Construct();
Car sedan = carDirector.GetCar();

var sportsCar = new CarBuilder()
    .SetEngine("V8")
    .SetWheels(4)
    .SetColor("Red")
    .Build();
```
