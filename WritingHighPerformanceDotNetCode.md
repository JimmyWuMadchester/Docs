# Writing High-Performance .NET code

### Is Managed Code Slower Than Native Code?

When you build your C# code, the compiler translates the high-level language to Intermediate Language (IL) and metadata about your types. When you run the code, it is just-in-time compiled. That is, the first time a method is executed, the CLR will invoke the JIP compiler on your IL to convert it to assembly code. Most code optimization happens at this stage. There is a definite performance hit on this first run, but after that you will always get the compiled version.

### Layers of Optimization

1. Architecture
1. Algorithms
1. .NET Framework
1. CLR
1. Assembly Code