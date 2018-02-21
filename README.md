# Bridge-API-Documentation
This repository holds the XML file for **Bootstrapper.dll**. This [XML](./Bootstrapper.xml) file directly feeds into Visual Studio's intellisense. Bellow is a small guide on how to add some documentation to any of the API's features.

# Guide
### Members
The Members element is a encapslating element that holds all of the members inside of it.
```xml
<members>
  <member>
  </member>
</members>
```
### Member
The Member element is a single method, class, field, and so on. The name attribute determines which memeber it will be doucmenting.

The format for selecting the member you want to doucment is a follows.

```xml
<member name="F:GTANetworkAPI.Event.ChatMessage">
  ...
</member>
```

The first character is the type of member you want to doucment, in this example it's "F" which means that you are accessing a Field, here is a list of the members and their Character.


| Character | Description |
|--- |---|
| N | Namespace |
| T | Type: class, interface, struct, enum, delegate |
| F | Field |
| P | Property (including indexers or other indexed properties) |
| M | Method (including such special methods as constructors, operators, and so forth)  |   
| E | Event |
| ! | Error string |


After you pick the correct character it's followed by a colon and then the full member's name. For example if I wanted to access the method CreateBlip, I would use this.

```xml
<member name="M:GTANetworkMethods.Blip.CreateBlip()">
  ...
</member>
```
As you can see in this example I now added some function parentheses, this is where you would put the arugments for the method for example,

```xml
<member name="M:GTANetworkMethods.Blip.CreateBlip(System.UInt32,GTANetworkAPI.Vector3,System.Single,System.Byte,System.String,System.Byte,System.Single,System.Boolean,System.Int16,System.UInt32)">
  ...
</member>
```
We just have to put the types of the arguments because this is how we would select methods that might have overloads. For example this CreateBlip method has an overload and we would be able to access that method like this,

```xml
<member name="M:GTANetworkMethods.Blip.CreateBlip(GTANetworkAPI.Vector3,System.Single,System.UInt32)">
  ...
</member>
```
This will access the method that only requires a Vector3, Float and the optional argument of dimension which is a uint. With that being said you are also required to use the full name of the type. For example, 

`
float = System.Single, bool = System.Boolean, uint = System.UInt32
`
### Member's Children

#### Summary

We will start with the `<summary>` element. This element adds a summery to the memeber you are documenting. This is how we would place it in the Member element,

```xml
<member name="M:GTANetworkMethods.Blip.CreateBlip(GTANetworkAPI.Vector3,System.Single,System.UInt32)">
  <summary>
  Creates blip with the given Vector3, and Range. Uses the default parameters.
  </summary>
</member>
```
The summary looks like this in Visual Studio, don't worry about the *pos:* line we will get to that in the next section.

![alt text](https://i.imgur.com/3MV9rQt.png)

#### Param

The `<param>` element allows you to create documentation for certain parameters in a method. The there's one attribute for this element and that's the name. 

```xml
<member name="M:GTANetworkMethods.Blip.CreateBlip(GTANetworkAPI.Vector3,System.UInt32)">
  <summary>
  Creates blip with the given Vector3. Uses the default parameters.
  </summary>
  <param name="pos">The position of the blip.</param>
  <param name="dimension">Optional, defaults to Global Dimension.</param>
</member>
```

This attribute **MUST** match the parameter name in the intellisense dialog. If you don't understand what I mean by this take a look at this picture. 

![alt text](https://i.imgur.com/QcDsvle.png)

That "pos" must be exactly the same as the name attribute. Look back at the above code and check to see that the `<param name="pos">` looks exactly like the "pos" in the picture.

---

##### Sources

* [Processing the XML File](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/processing-the-xml-file)
* [Recommended Tags for Documentation Comments](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments)
* [XML Tutorial](https://www.w3schools.com/xml/default.asp)
