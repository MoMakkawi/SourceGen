# [Compile-Time Source Code Generator](https://learn.microsoft.com/en-us/dotnet/csharp/roslyn-sdk/source-generators-overview) to generate folders :
The problem is when trying to generate the code in a file **but inside a folder**

#### in [ConsoleApp\SourceGenerator\HelloSourceGenerator.cs](https://github.com/MoMakkawi/SourceGen/blob/master/SourceGenerator/HelloSourceGenerator.cs) in HelloSourceGenerator class in Execute method 
```
var relativePath = Path.Combine("folder", $"{typeName}.g.cs");

context.AddSource(relativePath, source)
```
#### the build output interface will show this exception when you Build your solution ```(Ctrl + Shift + B)```:

2>CSC : warning CS8785: Generator 'HelloSourceGenerator' failed to generate source. It will not contribute to the output and compilation errors may occur as a result. Exception was of type 'ArgumentException' with message 'The hintName 'folder/Program.g.cs' contains an invalid character '/' at position 6.

Same proplem for this : ```\\``` and ```\```.
