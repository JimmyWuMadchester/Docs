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