JavaBeans
-------------------------

**JavaBeans** are classes that **encapsulate many objects into a single object** (the bean). They are **serializable, have a zero-argument constructor**, and allow access to properties using **getter and setter methods**.   

The name "Bean" was given to encompass this standard, which aims to create **reusable software components** for Java.  

###Advantages
- The properties, events, and methods of a bean that are exposed to another application can be controlled.
- A bean may register to receive events from other objects and can generate events that are sent to those other objects.
- Auxiliary software can be provided to help configure a java bean.
- The configuration settings of a bean can be saved to persistent storage and restored.

###Disadvantages
- A class with a nullary constructor is subject to being instantiated in an invalid state. If such a class is instantiated manually by a developer (rather than automatically by some kind of framework), the developer might not realize that the class has been **improperly instantiated manually.** The **compiler cannot detect** such a problem, and even if it is documented, there is no guarantee that the developer will see the documentation.
- Having to create getters for every property and setters for many, most, or all of them can lead to an **immense quantity of boilerplate code.**

###Features
- Presence of a no argument constructor;
- Support for persistence;
- Properties manipulated by getter and setter methods;
- Support for introspection;
- Events as the mechanism of communication between beans;
- Support for customization via property editors. 

###XML
Under Package java.beans, there are two useful class  
`XMLDecoder`: The XMLDecoder class is used to read XML documents created using the XMLEncoder and is used just like the ObjectInputStream.  
`XMLEncoder`: The XMLEncoder class is a complementary alternative to the ObjectOutputStream and can used to generate a textual representation of a JavaBean in the same way that the ObjectOutputStream can be used to create binary representation of Serializable objects.  

### XML >  Yaml > Json 

Json is **simpler**, **lighter** and more **readable**. 
Json is a good t**emporarily data format to transfer** a piece of data from point A to Point B.

Yaml: YAML has many additional features lacking in JSON, including comments, extensible data types, relational anchors, strings without quotation marks, and mapping types preserving key order.

XML is a **Language**, more **powerful**.
	
