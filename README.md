# Open-Closed Principle (OCP)

The **`Open-Closed Principle (OCP)`** states that software entities (such as classes, modules, or functions) should be open for extension but closed for modification. In other words, you should be able to extend the behavior of a class without changing its source code. Let's illustrate the OCP with a C# example.

Suppose you have a basic **`Shape`** class hierarchy with different shapes like **`Circle`** and **`Rectangle`**. Initially, you have code that calculates the area of these shapes in a single method within the **`Shape`** class:

```csharp
public abstract class Shape
{
    public abstract double CalculateArea();
}

public class Circle : Shape
{
    public double Radius { get; set; }

    public override double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override double CalculateArea()
    {
        return Width * Height;
    }
}
```

Now, let's say you want to add a new shape, a **`Triangle`**. According to the Open-Closed Principle, you should be able to extend your code to support this new shape without modifying the existing **`Shape`** class. Here's how you can do it:

```csharp
public class Triangle : Shape
{
    public double Base { get; set; }
    public double Height { get; set; }

    public override double CalculateArea()
    {
        return 0.5 * Base * Height;
    }
}
```

With this approach, you've extended the behavior of your code by adding a new shape **`(Triangle)`** without changing the existing **`Shape`** class. The **`Shape`** class remains closed for modification but open for extension.

Now, you can use all these shapes like this:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var circle = new Circle { Radius = 5 };
        var rectangle = new Rectangle { Width = 4, Height = 3 };
        var triangle = new Triangle { Base = 6, Height = 4 };

        var shapes = new List<Shape> { circle, rectangle, triangle };

        foreach (var shape in shapes)
        {
            Console.WriteLine($"Area of {shape.GetType().Name}: {shape.CalculateArea()}");
        }
    }
}
```

This code adheres to the Open-Closed Principle by allowing you to add new shapes without altering existing code, making your system more maintainable and extensible.
