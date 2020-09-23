#How to validate if there are only numbers in a text column

Using a text column, expand column validation and add this formula:
```
=OR(IsEmpty(ColumnName),IsNumber(ColumnName + 0))
```
![alt text][img1]

Sources:

[Examples of common formulas in lists](https://support.microsoft.com/en-us/office/examples-of-common-formulas-in-lists-d81f5f21-2b4e-45ce-b170-bf7ebf6988b3)

[img1]: https://github.com/campelo/documentation-dev.to/blob/master/sharepoint/how-to-validate-if-there-are-only-numbers-in-a-text-column/assets/img1.png "Image 1"