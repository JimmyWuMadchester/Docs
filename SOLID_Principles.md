# SOLID Principle with C# Examples
The following are notes taken while reading this [post](https://www.codeproject.com/Tips/1033646/SOLID-Principle-with-Csharp-Example) on codeproject.

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
