---
layout: post
---
In the field of software engineering, there comes many occasions when you get to see other engineer’s code, which is an extremely good opportunity to learn and grow. But sometimes you get a chance to see such an amazing piece of code that you instinctively say - What-the-F.

Inspired from DailyWTF (dead now), I’ve compiled a list of most common and worst code snippets that have crossed my eyes during my career.

## 1. Converting number to string
```
var str = i + "";
```
Most languages provide toString() method or some other standard approach to convert a number into string, but many developers still concatenate empty string to a number for this. There are few reasons for not to do like this:

Foremost, it looks ugly.
Secondly, the purpose of ‘+’ operator is either addition or concatenation, not to convert number into string
Lastly, compiler has to do 2 operations: first convert the number and then concatenate empty string. Though performance impact is negligible with modern compilers and processing power.

## 2. Comparing Boolean variable in IF statement
```
if(isActive == true){
    //Something
}
```
IF statement expects an expression that evaluates to true or false and since a Boolean variable also evaluates to true or false, there is no need to compare it explicitly with true/false.

## 3. Throwing exception from catch block
```
try{
  //Something
}
catch(ex){
  throw ex;
}
```
Why would anyone do this? Wrapping a piece of code in try block and throwing exception as it is from catch block? It’s useless and please don’t do this. Either do some meaningful working in catch block like logging or simply remove try-catch block altogether

## 4. Database operations in a loop
```
public void SomeFunction()
{
    var categories = _context.Categories.ToList();
    foreach(var category in categories)
    {
        var products = category.Products.ToList();
        //do something with products
    }
}
```
Many new developers fall prey to this and in many cases, they don’t know the concept of lazy loading and eager loading if they are using any ORM. This kind of code can cause some real performance issues because of repeated server-to-database round trips and network/serialization overheads.

## 5. Looping over HashMap to get value of a key
```
HashMap<String, ErrorLookupBO> errors = getAllReasonsMap();

for (Entry<String, ErrorLookupBO> entry : errors.entrySet()) {
      if (description != null && description == entry.getKey()) {
            error = (ErrorLookupBO) entry.getValue();
            return error;
      }
}
```
I recently came across with this code while doing code-review of a product. What is the point of having HashMap in the first place if loop is not avoided?

As Thom Holwerda have said:

![](/assets/images/1520215242873.jfif){: .center-image }

These are my top 5 What-The-Code moments. Let me know if you have come across with similar or even funnier WTFs in your career.

