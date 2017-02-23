* Tutorial: http://cocoadevcentral.com/articles/000081.php
* Full syntax: http://learnxinyminutes.com/docs/c/

### Primative (Scalar) Types

# Learning C

- Tutorial: [http://cocoadevcentral.com/articles/000081.php](http://cocoadevcentral.com/articles/000081.php)
- Full syntax: [http://learnxinyminutes.com/docs/c/](http://learnxinyminutes.com/docs/c/)

### Primative (Scalar) Types

| type | bytes | format | description |
| --- | --- | --- | --- |
| char | 1 | %c | one single letter or number |
| int | 2 | %d | number, including negatives |
| unsigned int | 2 | %u | integer numbers, but not negative |
| long | 4 | %ld | longer int |
| float | 4 | %f | number with decimal |
| double | 8 | %lf | larger decimal |

*array = any of above with [] or [4]

## Learning Objective-C
•	Quick guide http://cocoadevcentral.com/d/learn_objectivec/
•	Full syntax http://learnxinyminutes.com/docs/objective-c/
•	Complier reference http://clang.llvm.org/docs/index.html

## Functions/Methods
### In C:
type functionName(paramtype para1Name, paramtype param2Name); type foo = functionName(param1, param2);

### In ObjctiveC:
-(type)Param1:(param1Type)param1Name Param2:(param2Type)param2Name type foo = [classInstance Param1:param1 Param2:param2];
strong = maintains memory throughout the life of the object copy = copy of the object, when we want the value fixed when we referenced to it (mutable) weak = object but doesn’t increase reference count, parent-child relationship between objects assign = float,ints, and car. Don’t have reference counting requirements, as not pointers
