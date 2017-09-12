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


### Interface segregation principle (ISP)

### Dependency inversion principle (DIP)
