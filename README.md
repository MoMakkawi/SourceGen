# [Compile-Time Source Code Generator](https://learn.microsoft.com/en-us/dotnet/csharp/roslyn-sdk/source-generators-overview) to generate folders :
The problem is when trying to generate the code in a file **but inside a folder**

#### in [ConsoleApp\SourceGenerator\HelloSourceGenerator.cs](https://github.com/MoMakkawi/SourceGen/blob/master/SourceGenerator/HelloSourceGenerator.cs) in HelloSourceGenerator class in Execute method 
```
var relativePath = Path.Combine("folder", $"{typeName}.g.cs");

context.AddSource(relativePath, source)
```


## in VS 17.6.4 & VS 17.6.2 the problem :
I presented earlier that I am working on to try to generate a folder by name "folder" and contain "program.g.cs" file.

the problem of generating **FOLDERS** is still **not** resolved.
The changes that occurred were generated an **_apparently empty file_** with the name: "folder/program.g.cs"

![files name with slash](https://github.com/dotnet/roslyn/assets/94985793/97b65c1a-67b3-4828-8a69-6d1090c980c3)


But the _**strange**_ thing is that the resulting file, although it is apparently empty, may contain the generated code in one way or another, but it is not visible.

![like empty sg out ](https://github.com/dotnet/roslyn/assets/94985793/01dee113-fa68-46bd-a146-178605dae339)



### How did I know that?

In the[ program.cs ](https://github.com/MoMakkawi/SourceGen/blob/master/ConsoleApp/Program.cs) file there is a declaration of a method called "HelloFrom". This method we considered partial because we will use the code generator to write the definition for us, which in turn will contain the implementation of this method.

![program](https://github.com/dotnet/roslyn/assets/94985793/419d2957-8f4f-4238-9963-ab161634dcc2)


Without the output of the code generator, the method will not be executed as required,
but the method was executed as if the output of the code generator existed, 
even though the resulting file was empty.

![output as if SG work true](https://github.com/dotnet/roslyn/assets/94985793/0d84f3ee-4301-4aaa-897b-85b5221cefdc)

## Solution for VS 17.6.2:
Based on the following GitHub comment : jan created an issue to track the bug: [#68489](https://github.com/dotnet/roslyn/issues/68489). Note that this is IDE-only problem, it should not prevent you from using directories in source-generated files in normal builds, such files just aren't displayed correctly in Visual Studio.

  =>so we will move to this issue: [Source Generator files with directories are not displayed correctly in IDE](https://github.com/dotnet/roslyn/issues/68489)

___________________________________________________________________________________________________

## in VS 17.5.2 the problem :
#### the build output interface will show this exception when you Build your solution ```(Ctrl + Shift + B)```:

2>CSC : warning CS8785: Generator 'HelloSourceGenerator' failed to generate source. It will not contribute to the output and compilation errors may occur as a result. Exception was of type 'ArgumentException' with message 'The hintName 'folder/Program.g.cs' contains an invalid character '/' at position 6.

Same proplem for this : ```\\``` and ```\```.

## Solution for VS 17.5.2 :
Based on the following GitHub conversation: [Allow directories in source generator outputs](https://github.com/dotnet/roslyn/pull/66438?notification_referrer_id=NT_kwDOBaleQbM1MzQ4OTk1MTY1Ojk0OTg1Nzkz&notifications_query=is%3Adone#issuecomment-1477484123) ,
the solution to this problem [is not in VS 17.5.2, so you will have to use VS 17.6 Preview](https://github.com/dotnet/roslyn/pull/66438#issuecomment-1477484123)
