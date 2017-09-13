# SOLID Principle with C# Examples
The following notes are taken while reading this [post](https://www.codeproject.com/Tips/1033646/SOLID-Principle-with-Csharp-Example) on codeproject. Code examples are directly from the post.

## About SOLID
* **S**: Single responsibility principle (SRP)
* **O**: Open closed principle (OCP)
* **L**: Liskov substitution principle (LSP)
* **I**: Interface segregation principle (ISP)
* **D**: Dependency injection principle (DIP)

### Single responsibility principle (SRP)

A bad example that Employee class takes two responsibilities of employee database operation and employee report generation.
```C#
namespace SRP
{
    public class Employee
    {
        public int Employee_Id { get; set; }
        public string Employee_Name { get; set; }

        /// <summary>
        /// This method used to insert into employee table
        /// </summary>
        /// <param name="em">Employee object</param>
        /// <returns>Successfully inserted or not</returns>
        public bool InsertIntoEmployeeTable(Employee em)
        {
            // Insert into employee table.
            return true;
        }
        /// <summary>
        /// Method to generate report
        /// </summary>
        /// <param name="em"></param>
        public void GenerateReport(Employee em)
        {
            // Report generation with employee data using crystal report.
        }
    }
}
```

According to SRP, one class should take one responsibility so we should write one different class for report generation, so that any change in report generation should not affect the ‘Employee’ class.

```C#
namespace SRP
{
    public class Employee
    {
        public int Employee_Id { get; set; }
        public string Employee_Name { get; set; }

        /// <summary>
        /// This method used to insert into employee table
        /// </summary>
        /// <param name="em">Employee object</param>
        /// <returns>Successfully inserted or not</returns>
        public bool InsertIntoEmployeeTable(Employee em)
        {
            // Insert into employee table.
            return true;
        }
    }
    
    public class ReportGeneration
    {
         /// <summary>
         /// Method to generate report
         /// </summary>
         /// <param name="em"></param>
         public void GenerateReport(Employee em)
         {
             // Report reneration with employee data.
         }
    }
}
```
N.B. In practice, for projects I worked on, a repository pattern could be used here for CRUD database operations for Exployee entities. Therefore, you will have a simple POCO class for Employee class objects. And database operations are in the repository layer, for example EmployeeRepo.

### Open closed principle (OCP)
Open for extension but closed for modification.

A bad example with too many 'IF' statements. Everytime when we want to introduce another new report type like 'Excel', then another 'IF' is required.
```C#
public class ReportGeneration
{
    /// <summary>
    /// Report type
    /// </summary>
    public string ReportType { get; set; }

    /// <summary>
    /// Method to generate report
    /// </summary>
    /// <param name="em"></param>
    public void GenerateReport(Employee em)
    {
        if (ReportType == "CRS")
        {
             // Report generation with employee data in Crystal Report.
        }
        if (ReportType == "PDF")
        {
            // Report generation with employee data in PDF.
        }
     }
 }
```

Define a base type ReportGenerationBase that every types of report can inherit from. So the ReportGenerationBase is open for extension but also closed for modification.

The ```virtual``` keyword allows the method to be overridden by any class that inherits it.

```C#
public class ReportGenerationBase
{
    /// <summary>
    /// Method to generate report
    /// </summary>
    /// <param name="em"></param>
    public virtual void GenerateReport(Employee em)
    {
        // From base
    }
}
/// <summary>
/// Class to generate Crystal report
/// </summary>
public class CrystalReportGeneraion : IReportGeneration
{
    public override void GenerateReport(Employee em)
    {
        // Generate crystal report.
    }
}
/// <summary>
/// Class to generate PDF report
/// </summary>
public class PDFReportGeneraion : IReportGeneration
{
    public override void GenerateReport(Employee em)
    {
        // Generate PDF report.
    }
}
```

### Liskov substitution principle (LSP)
Child class should not break parent class's type definition and behavior. Another interesting thing to pay attention to is [mutability](https://stackoverflow.com/a/1030573/5098156) when discussing LSP. 

A classic example is Rectangle and Square.
```C#
// A base class of Rectangle with **virtual** properties. 
public class Rectangle 
{
    public virtual int Height { get; set; }
    public virtual int Width { get; set; }
}

public class Square : Rectangle
{
    private int _height;
    private int _width;
    public override int Height
    {
        get
        {
            return _height;
        }
        set   // Here is the main problem: Exposing the set method makes the Square class mutable
        {
            _height = value;
            _width = value;
        }
    }
    public override int Width
    {
        get
        {
            return _width;
        }
        set
        {
            _width = value;
            _height = value;
        }
    }
}

public class AreaCalculator
{
    public static int CalculateArea(Rectangle r)
    {
        return r.Height * r.Width;
    }

    public static int CalculateArea(Square s)
    {
        return s.Height * s.Height;
    }
}

[TestMethod]
public void TwentyFourfor4x6RectanglefromSquare()
{
    Rectangle newRectangle = new Square();
    newRectangle.Height = 4;
    newRectangle.Width = 6;
    var result = AreaCalculator.CalculateArea(newRectangle);
    Assert.AreEqual(24, result);    // Behaviour is broken for the parent Rectangle class.
}
```

The fix is shown below using the abstract class ```Shape```
```C#
public  abstract class Shape
{
    public abstract int Area();
}

public class Rectangle :Shape
{
    public  int Height { get; set; }
    public  int Width { get; set; }
    public override int Area()
    {
        return Height * Width;
    }
}

public class Square : Shape
{
    public int Sides { get; set; };
    public override int Area()
    {
        return Sides * Sides;
    }
}
```
Then with ```Shape```, ```Rectangle``` and ```Square``` are not parent and child relationship anymore. They can only have that relationship when the objects created are immutable. Therefore, a square is a rectangle and always will be.

### Interface segregation principle (ISP)
Any client should not be forced to use an interface which is irrelevant to it.

Bad code example:
```C#
public interface IEmployee
{
    bool AddEmployeeDetails();  // Applicable to all employee types
    bool ShowEmployeeDetails(int employeeId);   // Only apply to Permanent Employees
}

public class PermanentEmployee : IEmployee
{
    bool AddEmployeeDetails() {
        // Implementation goes here.
    }
    bool ShowEmployeeDetails(int employeeId) {
        // Implementation goes here.
    }
}

public class NonPermanentEmployee : IEmployee
{
    bool AddEmployeeDetails() {
        // ...
    }
    bool ShowEmployeeDetails(int employeeId) {
        // N/A to this class.
    }
}
```
With only one interface for both types of employees, the ```NonPermanentEmployee``` class is forced to implement the method of ```ShowEmployeeDetails(int employeeId)```. To correct it, we can split the responsibilities of Add and Show into two interfaces. 

Fix:
```C#
public interface IAddOperation
{
    bool AddEmployeeDetails();
}
public interface IGetOperation
{
    bool ShowEmployeeDetails(int employeeId);
}

public class PermanentEmployee : IAddOperation, IGetOperation
{
    // ...
}

public class NonPermanentEmployee : IAddOperation
{
    // ...
}
```

### Dependency inversion principle (DIP)
