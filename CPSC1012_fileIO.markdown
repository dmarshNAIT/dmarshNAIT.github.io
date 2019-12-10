---
layout: page
title: File input/output
permalink: /cpsc1012/fileIO
---

## Writing to a file
```csharp
using System.IO;

StreamWriter writer = new StreamWriter("test.txt");
writer.WriteLine("hello world");
writer.Close();
```

## Reading from a file
Reading a single line:
```csharp
using System.IO;

StreamReader reader = new StreamReader("test.txt");
string line = reader.ReadLine();
Console.WriteLine(line);
reader.Close();
```


From a file of known length:
```csharp
using System.IO;

StreamReader reader = new StreamReader("test.txt");
string line;

for (int i = 0; i < 3; i++) {
    line = reader.ReadLine();
    Console.WriteLine(line);
} // end for
reader.Close();
```

From a file of unknown length:
```csharp
using System.IO;

StreamReader reader = new StreamReader("test.txt");
while (reader.EndOfStream == false) {
  string line = reader.ReadLine();
  Console.WriteLine(line);
} // end while
reader.Close();
```
