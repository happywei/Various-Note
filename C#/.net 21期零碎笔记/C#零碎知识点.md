## 一、String相关

- 1、根据char[]中的字符分割字符串，并忽略掉分割后字符串的空白字符，去除空白项
```
string name = "liuwei,shandongwa huanian|hunanwa";
string[] msgs = name.Split(new char[] { ',', ' ', '|' }, StringSplitOptions.RemoveEmptyEntries);
foreach (var item in msgs)
{
    Console.WriteLine(item);
}
```
- 2、String.Join方法：获取字符串数组中的元素，并在每个元素中用指定字符串分割。

```
string[] names = new string[] { "liuwei", "shandongwa", "huanian", "hunanwa" };
string txt = string.Join("~~~", names);
Console.WriteLine(txt);
```

- 3、String.Format 格式化
 
- 4、string.Replace 用一个字符串替换另一个字符串


## 二、文件读取相关

- 1、Path
- - Path.GetFileName 

Path.ChangeExtension 更改后缀名
```
//更改后缀名,只是更改字符串，不真修改
string extension = Path.ChangeExtension("1.txt", "avi");
Console.WriteLine(extension);
```

Path.Combine 合并路径

```
//合并路径的方法
string pth = Path.Combine(@"C:\", @"2.txt");
Console.WriteLine(pth);
```

Path.GetDirectoryName 返回文件的路径
Path.GetExtension 返回扩展名
Path.GetFileName 返回文件名和扩展名
Path.GetFileNameWithoutExtension 只返回文件名
Path.GetFullPath 返回绝对路径






- 2、File --->针对小文件读写
- - File.ReadAllLines //返回一个数组
- - File.ReadAllText //返回一坨字符串
- - File.WriteAllLines()
- - File.WriteAllText()
- 
- - File.Copy //复制
- - File.Creat("1.txt") //创建文件
- - File.Delete() //删除文件
- - File.Exist //判断该路径下的文件是否存在
- - File.Move //剪切，移动
- - File.Replace //替换
- - 

- 3、FileStream --->针对大文件读写

```
//创建一个文件，以流的方式往文件里面写内容
FileStream fs = new FileStream("1.txt", FileMode.OpenOrCreate, FileAccess.Write);
fs.Close(); //关闭
fs.Flush(); //清除缓冲区
fs.Dispose(); //释放文件的资源

或者套上using

//创建一个文件，以流的方式往文件里面写内容
using(FileStream fs = new FileStream("1.txt", FileMode.OpenOrCreate, FileAccess.Write))
{
    string msg = "liuwei";
    byte[] buffer = Encoding.UTF8.GetBytes(msg);
    fs.Write(buffer, 0, buffer.Length);
}

//以流的方式读取数据
using (FileStream fs = new FileStream("1.txt", FileMode.OpenOrCreate))
{
    byte[] buffer = new byte[fs.Length];
    fs.Read(buffer, 0, buffer.Length);
    string msg = Encoding.UTF8.GetString(buffer);
    Console.WriteLine(msg);
}
```

- 4、StreamReader ---> 简单的读取

比较麻烦的一种循环读取的方法

```
using (StreamReader reader = new StreamReader("1.txt", Encoding.Default))
{
    string msg;
    while ((msg = reader.ReadLine()) !=null)
    {
        Console.WriteLine(msg);
    }
}
```
直接读到末尾

```
using (StreamReader reader = new StreamReader("1.txt", Encoding.Default))
{
    string msg = reader.ReadToEnd();
    Console.WriteLine(msg);
}
```
或者使用reader.EndOfStream判断是否到了末尾

```
using (StreamReader reader = new StreamReader("1.txt", Encoding.Default))
{
    while (!reader.EndOfStream)
    {
    string msg = reader.ReadLine();
    Console.WriteLine(msg);
    }
}
```

- 5、StreamWriter

```
using(StreamWriter writer = new StreamWriter("one.txt"))
{
    writer.WriteLine("liuwei");
}
```



















