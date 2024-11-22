# Serialization and DeSerialization 

## Serialization : 

  ### Definition :
   > In C#, serialization is the process of converting object into byte stream so that it can be saved to memory, file or database. The reverse process of serialization is called deserialization.   Serialization and DeSerialization


Serialization : 

Definition : 
In C#, serialization is the process of converting object into byte stream so that it can be saved to memory, file or database. The reverse process of serialization is called deserialization.

C# SerializableAttribute 
To serialize the object, you need to apply SerializableAttribute attribute to the type. If you don't apply SerializableAttribute attribute to the type, SerializationException exception is thrown at runtime.

![image](https://github.com/user-attachments/assets/2f48c0e8-faa2-4094-807a-26d4c39ed2f2)


C# Serialization example
Let's see the simple example of serialization in C# where we are serializing the object of Student class. Here, we are going to use BinaryFormatter.Serialize(stream, reference) method to serialize the object.

using System;  
using System.IO;  
using System.Runtime.Serialization.Formatters.Binary;  
[Serializable]  
class Student  
{  
    int rollno;  
    string name;  
    public Student(int rollno, string name)  
    {  
        this.rollno = rollno;  
        this.name = name;  
    }  
}  

public class SerializeExample  

{  

    public static void Main(string[] args)  
    
    {  

        FileStream stream = new FileStream("e:\\sss.txt", FileMode.OpenOrCreate);  
        BinaryFormatter formatter=new BinaryFormatter();  
        Student s = new Student(101, "sonoo");  
        formatter.Serialize(stream, s);  
  
        stream.Close();  
    }  
}



DeSerialization : 
Definition : 
In C# programming, deserialization is the reverse process of serialization. It means you can read the object from byte stream. Here, we are going to use BinaryFormatter.Deserialize(stream) method to deserialize the stream

C# SerializableAttribute 
To serialize the object, you need to apply SerializableAttribute attribute to the type. If you don't apply SerializableAttribute attribute to the type, SerializationException exception is thrown at runtime.


C# Serialization example
Let's see the simple example of deserialization in C# 


using System;  
using System.IO;  
using System.Runtime.Serialization.Formatters.Binary;  
[Serializable]  
class Student  
{  
    public int rollno;  
    public string name;  
    public Student(int rollno, string name)  
    {  
        this.rollno = rollno;  
        this.name = name;  
    }  
}  
public class DeserializeExample  
{  
    public static void Main(string[] args)  
    {  
    
        FileStream stream = new FileStream("e:\\sss.txt", FileMode.OpenOrCreate);  
        BinaryFormatter formatter=new BinaryFormatter();  
        Student s=(Student)formatter.Deserialize(stream);  
        Console.WriteLine("Rollno: " + s.rollno);  
        Console.WriteLine("Name: " + s.name);  
        stream.Close();  
    }  
}  



JSON format:

NameSpace : System.Text.Json
		
		using System.Text.Json;
		
Serialisation: Object to JSON.

string jsonString = JsonSerializer.Serialize(object); // Object convert into only a json formate without a arranging. 
		byte[] jsonString = JsonSerializer.SerializeToUtf8Bytes(purchase1); this is for a byte code conversion */
    var options = new JsonSerializerOptions();
        		    options.WriteIndented = true;
    string jsonString = JsonSerializer.Serialize(purchase1, options); /* We got a good         readable type JSON because ( options.WriteIndented = true; ). */
Save the file using following
        File.WriteAllText("E:\\Purchase.json", jsonString); /* File - Provides static methods for the creation, copying, deletion, moving, and opening of a single file, and aids in the creation of FileStream objects. */


Example : Serialize to Json.

using System.Text.Json;

public class Purchase
{

    public string ProductName { get; set; }
    public DateTime DateTime { get; set; }
    public decimal ProductPrice { get; set; }
}

public class Program
{
    public static void Main()
    {
        Purchase purchase1 = new Purchase()
        {
	
            ProductName = "Orange juse",
            DateTime = DateTime.UtcNow,
            ProductPrice = 2.3m
        };
        var options = new JsonSerializerOptions();
        options.WriteIndented = true;

        string jsonString = JsonSerializer.Serialize(purchase1, options);
        File.WriteAllText("E:\\Purchase.json", jsonString);

     }
}


DeSerialisation: JSON to Object.


string variableName= File.ReadAllText("Path");
Eg : var purchaseJson = File.ReadAllText("E:\\Purchase.json");
// Purchase.json file is readed using those ReadAllText method and stored in purchaseJson. */
ClassName objectName = JsonSerializer.Deserialize<ClassName>(variableName);


Eg : Purchase purchase =  JsonSerializer.Deserialize<Purchase>(purchaseJson);
 /*The JSON file readed file is saved in the purchaseJson and it Deserialize to Purchase class object.
byte[] jsonString = JsonSerializer.SerializeToUtf8Bytes(purchase1); this is for a byte code conversion */
 

Example : DeSerialize from Json.

using System.Text.Json;

public class Purchase
{
    public string ProductName { get; set; }
    public DateTime DateTime { get; set; }
    public decimal ProductPrice { get; set; }
}

public class Program
{
    public static void Main()
    { 
        string purchaseJson = File.ReadAllText("E:\\Purchase.json");

        Purchase purchase =  JsonSerializer.Deserialize<Purchase>(purchaseJson);

     }
}


   
   

## DeSerialization : 
