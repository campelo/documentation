---
title: Python - Data types
series: Python - Getting started
published: true
description: Data types in python
tags: 'python, begginer, data, type'
cover_image: ../assets/cover.jpg
canonical_url: null
id: 942661
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

## Data types

**Python infers data types of variables**. This means that you don't need to write string, boolean, int or others to explicit declarations to work with variables. You can specify the type of a variable using cast for that. 

The basics for write a variable and its value is **variable name** + **equals sign** + **variable value**. That will create a new variable and its type will be infered by the value type.

```
myVariableName = myValue
```

I'll show you some data types bellow, but you can learn more about other ones on [this site](https://www.w3schools.com/python/python_datatypes.asp)

### Integer

```
myInteger = 3 // infered data type
```

or 

```
myInteger = int(3) // explicitly
```

### Float

```
myFloat = 3.5 // infered data type
```

or

```
myFloat = float(3.5) // explicitly
```

### String

```
myString = 'Have a nice day!' // infered data type
```

or

```
myString = str('Have a nice day!') // explicitly
```

You can use *double quotes* **"** or *single quotes* **'** to delimit the string. When you're using the first one, it'll be easier to write single quotes inside your value string.

```
myString = "Jhon's house"
```

Using single quotes everywhere, you should to scape **\\** all of the single quotes in the value.

```
myString = 'Jhon\'s house'
```

### Boolean

```
myBool = True
```

or 

```
myBool = bool(True)
```

###### Notes

You can access this code on [github](https://github.com/campelo/Python-First-steps).

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.