# How to show hour only in a view

A date/time column displays date and hour. 

![alt text][img1]

If you need to display only hour, you could create a calculated field and use a formula to do that.
```
=TEXT(DateTimeColumnName,"hh:mm")
```

![alt text][img2]

or for imperial time

```
=TEXT(DateTimeColumnName,"hh:mm AM/PM")
```

![alt text][img3]

Sources:

[Calculated field formulas](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14))

[img1]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-show-hour-only-in-a-view/assets/img1.png "Image 1"
[img2]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-show-hour-only-in-a-view/assets/img2.png "Image 2"
[img3]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-show-hour-only-in-a-view/assets/img3.png "Image 3"