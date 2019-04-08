# C# Related Notes

**Using Tuples**: At the moment I would
personally advise that these be kept within the internal API of a program rather than exposed
publicly, as tuples represent a simple composition of values rather than encapsulating them.

The GetType() method declared on System.Object is
non-virtual, and the somewhat complex rules around when boxing occurs mean that if you call
GetType() on a value type value, it always needs to be boxed first. Normally that’s a little
inefficient but doesn’t cause any confusion. With nullable value types, it will either cause a
NullReferenceException or return the underlying non-nullable value type.

**IEnumerable vs IEnumerator**: An IEnumerable is a sequence which can be iterated over, whereas an IEnumerator is
like a cursor within a sequence. There can be multiple IEnumerator instances iterating over
the same IEnumerable, probably without changing its state at all. If that didn’t make much sense, you might want to 
think about an IEnumerable as like a book and an IEnumerator as a bookmark.

## .Net core vs .Net Framework

* [https://stackoverflow.com/questions/38063837/whats-the-difference-between-net-core-net-framework-and-xamarin](https://stackoverflow.com/questions/38063837/whats-the-difference-between-net-core-net-framework-and-xamarin)

## Object and collection initializers

```
var order = new Order
{
    OrderId = "xyz",
    Customer = new Customer { Name = "Jon", Address = "UK" },
    Items =
    {
        new OrderItem { ItemId = "abcd123", Quantity = 1 },
        new OrderItem { ItemId = "fghi456", Quantity = 2 }
    }
};
```

## Exception handling

Another way to avoid exceptions is to return null for extremely common error cases instead of throwing an exception. An extremely common error case can be considered normal flow of control. By returning null in these cases, you minimize the performance impact to an app. [ref.](https://docs.microsoft.com/en-us/dotnet/standard/exceptions/best-practices-for-exceptions#design-classes-so-that-exceptions-can-be-avoided)

### Catch Blocks

In general, do not specify Exception as the exception filter unless either you know how to handle all exceptions that might be thrown in the try block, or you have included a throw statement at the end of your ```catch``` block.

In ```catch``` blocks, always order exceptions from the most derived to the least derived. When your code cannot recover from an exception, don't catch that exception. Enable methods further up the call stack to recover if possible.

You should catch exceptions when the following conditions are true:

* You have a good understanding of why the exception might be thrown, and you can implement a specific recovery, such as prompting the user to enter a new file name when you catch a FileNotFoundException object.

* You can create and throw a new, more specific exception.
    ```
    int GetInt(int[] array, int index)
    {
        try
        {
            return array[index];
        }
        catch(System.IndexOutOfRangeException e)
        {
            throw new System.ArgumentOutOfRangeException(
                "Parameter index is out of range.", e);
        }
    }
    ```

* You want to partially handle an exception before passing it on for additional handling. In the following example, a ```catch``` block is used to add an entry to an error log before re-throwing the exception.
    ```
    try
    {
        // Try to access a resource.
    }
    catch (System.UnauthorizedAccessException e)
    {
        // Call a custom error logging procedure.
        LogError(e);
        // Re-throw the error.
        throw;     
    }
    ```

### Finally Blocks

```finally``` is bad for performance.

A ```finally``` block enables you to clean up actions that are performed in a ```try``` block. If present, the ```finally``` block executes last, after the ```try``` block and any matched ```catch``` block. A finally block always runs, regardless of whether an exception is thrown or a ```catch``` block matching the exception type is found.

Clean up resources allocated with either using statements, or finally blocks. Prefer using statements to automatically clean up resources when exceptions are thrown. Use finally blocks to clean up resources that don't implement IDisposable. Code in a finally clause is almost always executed even when exceptions are thrown.

