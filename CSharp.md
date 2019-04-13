# C# Related Notes

**Using Tuples**: At the moment I would
personally advise that these be kept within the internal API of a program rather than exposed
publicly, as tuples represent a simple composition of values rather than encapsulating them.

**Expression trees**: The below demos that the code is available for examination at execution time, which is the whole point of expression trees. 

```
Expression<Func<int, int, int>> adder = (x, y) => x + y;
Console.WriteLine(adder);
```

**Extension method**: 
```
using System;
namespace NodaTime.Extensions
{
    public static class DateTimeOffsetExtensions
    {
        public static Instant ToInstant(this DateTimeOffset dateTimeOffset)
        {
            return Instant.FromDateTimeOffset(dateTimeOffset);
        }
    }
}
```

```
string[] words = { "keys", "coat", "laptop", "bottle" };
IEnumerable<string> query =
    Enumerable.Select(
        Enumerable.OrderBy(
            Enumerable.Where(words, word => word.Length > 4),
            word => word),
word => word.ToUpper());

# with extension method and LINQ
string[] words = { "keys", "coat", "laptop", "bottle" };
IEnumerable<string> query = words
    .Where(word => word.Length > 4)
    .OrderBy(word => word)
    .Select(word => word.ToUpper());
```