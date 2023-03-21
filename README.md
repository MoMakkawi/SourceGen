# Compile-Time Source Code Generator to generate folders :
The problem is when trying to generate the code in a file 
#### but inside a folder
```
var relativePath = Path.Combine("folder", $"{typeName}.g.cs");

context.AddSource(relativePath, source)
```
This will not work but will throw an exaption with the character number of  ```'\'```.

Note in my E.g.: the relativePath = folder\Program.g.cs

Same proplem for this : ```\\``` and ```//``` and ```'/'```.
