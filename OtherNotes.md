# Notes Taken From Other Resources

## Best practices

Make the best practices subconscious. Continuous learning & automation.

## CLI

C# (and all .NET languages) are compiled to an intermediate language called Common Intermediate Language (CIL, a.k.a. Microsoft Intermediate Language, MSIL), which is deployed to the target machine. When the application is loaded the local .NET JIT compiler compiles the CIL to native code. The upshot here is that the JIT compiler knows exactly what type of CPU the target machine has and so it can make full use of all instruction sets available to it. The new JIT compiler is, therefore, the key to making SIMD available to .NET developers. Another advantage of accessing SIMD via the JIT compiler is that your application’s performance will improve in the future without ever being rebuilt and re-deployed. When future processors with larger SIMD registers become available RyuJIT will be able to make full use them.

## Stateless service

* Not a cache or a database
* Frequently accessed metadata or configuration info
* No instance affinity
* Loss a node is a non-event

## Stateful service

* Database & caches
* Custom apps which hold large amounts of data
* Loss of a node is a notable event
