# How to create views for current, previous and next months

> :warning: **Important**: You must select the **Date and time** type for all of those fields

![alt text][img1]

## Current month
You should create some calculated fields to get the **current** month's start and end dates:

```
=Date(Year[Date column name],Month[Date column name],1)
```

![alt text][img2]

```
=Date(Year[Date column name],Month[Date column name]+1,1)-1
```

![alt text][img3]


Then, you can create a filter verifying if **today** is greather or equals to start of current month and less or equals to end of current month:

![alt text][img4]

## <a name="prevMonth"></a>Previous month
You should create some calculated fields to get the **next** (yes, the **next**) month's start and end dates.

```
=Date(Year[Date column name],Month[Date column name]+1,1)
```

![alt text][img5]

```
=Date(Year[Date column name],Month[Date column name]+2,1)-1
```

![alt text][img6]

Then, you can create a filter verifying if **today** is greather or equals to start of next month and less or equals to end of next month:

![alt text][img7]

## Next month
It's similar as the previous month, but your calculated fields should get the start and end dates of the [**previous month**](#prevMonth).

Sources:

[msdn filtering items last month](https://social.msdn.microsoft.com/Forums/sharepoint/en-US/1142ea9c-4268-4530-b1f5-d7487a90693d/filtering-for-items-completed-last-month?forum=sharepointcustomizationlegacy)

[img1]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img1.png "Image 1"
[img2]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img2.png "Image 2"
[img3]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img3.png "Image 3"
[img4]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img4.png "Image 4"
[img5]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img5.png "Image 5"
[img6]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img6.png "Image 6"
[img7]: https://github.com/campelo/documentation/blob/master/sharepoint/how-to-create-views-for-current-previous-and-next-months/assets/img7.png "Image 7"