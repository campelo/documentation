---
title: Excel - How to get a substring from a text
published: true
description: Getting a substring from a cell in excel
tags: 'excel, substring'
cover_image: ./assets/img2.png
canonical_url: null
id: 935082
date: '2021-12-23T23:10:15Z'
---

## Text on right
Find the char that you are looking for ("," on this sample)
```
=FIND(",",F2)
```

Get all right text from this char
```
=RIGHT(F2,LEN(F2)-FIND(",",F2))
```

Use <strong>trim</strong> function to remove unwanted spaces
```
=TRIM(RIGHT(F2,LEN(F2)-FIND(",",F2)))
```

![alt text][img3]

## Text on the middle

First we will eliminate all right side from searched text.
```
=FIND(G2,FIND(",",G2)-1)
```
![alt text][img1]

Then we will eliminate all left side from searched text.
```
=RIGHT(F2,LEN(F2)-FIND("@",SUBSTITUTE(F2,"/","@",LEN(F2)-LEN(SUBSTITUTE(F2,"/",""))),1))
```
![alt text][img2]

Sources:

[Substring](https://www.excel-easy.com/examples/substring.html#:~:text=To%20extract%20the%20leftmost%20characters,correct%20number%20of%20leftmost%20characters.)

[Getting the last position of a character using excel formula](https://trumpexcel.com/find-characters-last-position/)

[img1]: ./assets/img1.png "Image 1" 

[img2]: ./assets/img2.png "Image 2" 

[img3]: ./assets/img3.png "Image 3" 
