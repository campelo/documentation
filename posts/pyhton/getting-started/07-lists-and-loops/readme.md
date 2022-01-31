---
title: Python - Lists and loops
series: Python - Getting started
published: true
description: Interacting with lists using loops
tags: 'python, begginer, loop, list'
cover_image: ../assets/cover.jpg
canonical_url: null
id: 974214
date: '2022-01-31T20:31:07Z'
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

# List

A list can hold many objects at the same time. So, you can make a list of students, cars, places or whatever you want.

## Declaring a list

To declare a list you should use brackets [] to create a new list variable. 

```python
# an empty list...
emptyList = []
```

If you want to create a new list with some objects, you should insert a comma to identify each of them.

```python
# a list of fruits...
fruits = ["orange", "apple", "banana"]
print(fruits)

# OUTPUT: 
# ['orange', 'apple', 'banana']
```

You can add new items any time to an existing list.

```python 
# appending new items to a list...
fruits.append("strawberry")
fruits.append("watermelon")

# OUTPUT: 
# ['orange', 'apple', 'banana', 'strawberry', 'watermelon']
```

## Picking up an element from a list

Elements from a list are index based. So, if you want to get the first element you should use 0, for the second one, 1 and so on.

```python
# getting the first element from a list...
print (fruits[0])

# getting the third element from a list...
print (fruits[2])

# OUTPUT
# orange
# banana
```

## Checking if an element is present on a list

You can check if a element is on a list using writing a new if line (*if element in list*) like the example bellow.

```python
fruit = 'pear'

if fruit in fruits:
  print(fruit + " is already on the list.")
else:
  print(fruit + " isn't on the list yet.")

# OUTPUT: 
# pear isn't on the list yet.
```
# Loop

A loop is used to run all over objets from a list.

## Interacting with a loop

You can easly write a for lace (*for element in list*) to loop through all elements of your list.

```python
# looping through all elements from my list...
for myFruit in fruits:
  print("I've added " + myFruit + " on my list.")

# OUTPUT:
# I've added orange on my list.
# I've added apple on my list.
# I've added banana on my list.
# I've added strawberry on my list.
# I've added watermelon on my list.
```

# Loop with range

Using [range](https://docs.python.org/3/library/functions.html#func-range) you can interact with a loop to display values from some criterias.

```python
print("Range with element to stop. It'll take from the first until the third element...")
for i in range(3):
  print(i, end="-")
  print(fruits[i])

print("It'll take the 3 next elements starting from the second one...")
for i in range(1, 3):
  print(i, end="-")
  print(fruits[i])

print("It'll take the 3 next elements starting from the second one using step 1 between them...")
for i in range(1, 3, 1):
  print(i, end="-")
  print(fruits[i])

print("It'll take the 4 next elements starting from the first one and using step 2 between them...")
for i in range(0, 4, 2):
  print(i, end="-")
  print(fruits[i])

/* */
# OUTPUT
# Range with element to stop. It'll take from the first until the third element...
# 0-orange
# 1-apple
# 2-banana
# It'll take the 3 next elements starting from the second one...
# 1-apple
# 2-banana
# It'll take the 3 next elements starting from the second one using step 1 between them...
# 1-apple
# 2-banana
# It'll take the 4 next elements starting from the first one and using step 2 between them...
# 0-orange
# 2-banana
```

## Exiting from a loop

If you want to stop a loop, you can use **break** to exit from it

```python
# It'll break when the fruit is "apple"...
for myFruit in fruits:
  print(myFruit)
  # if myFruit is apple, the loop will stop...
  if (myFruit == "apple"):
    break # It stops the loop...

# OUTPUT
# orange
# apple
```

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.
