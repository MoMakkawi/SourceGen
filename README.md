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

## Solution :
Based on the following GitHub conversation: [Allow directories in source generator outputs](https://github.com/dotnet/roslyn/pull/66438?notification_referrer_id=NT_kwDOBaleQbM1MzQ4OTk1MTY1Ojk0OTg1Nzkz&notifications_query=is%3Adone#issuecomment-1477484123) ,
the solution to this problem [is not in VS 17.5.2, so you will have to use VS 17.6 Preview](https://github.com/dotnet/roslyn/pull/66438#issuecomment-1477484123)
