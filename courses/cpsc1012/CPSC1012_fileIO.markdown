---
layout: page
title: File input/output
permalink: /cpsc1012/fileIO
parent: CPSC1012
nav_order: 7
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

for (int i = 0; i < 3; i++) {   // 3 is the # of lines in the file
    line = reader.ReadLine();
    Console.WriteLine(line);
} // end for

reader.Close();
```

From a file of unknown length:
```csharp
using System.IO;

StreamReader reader = new StreamReader("test.txt");
while (reader.EndOfStream == false) { // this means "read until the end of the file"
  string line = reader.ReadLine();
  Console.WriteLine(line);
} // end while

reader.Close();
```
