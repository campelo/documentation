# How to remove thousands separator of a number column

All data have thousands separator for a number column

![alt text][img1]

Click on down-arrow beside a column name and select Column Settings > Format this column

![alt text][img2]

The select "Advanced mode"

![alt text][img3]

Use this json to show only numbers for this field
```
{
   "$schema": "https://developer.microsoft.com/json-schemas/sp/v2/column-formatting.schema.json",
   "elmType": "div",
   "txtContent": {
        "operator": "toString()",
        "operands" : ["@currentField"]
    }
}
```

![alt text][img4]

Sources:

[Microsoft official documentation](https://docs.microsoft.com/en-us/sharepoint/dev/declarative-customization/column-formatting)

[Github column samples](https://github.com/pnp/sp-dev-list-formatting/tree/master/column-samples)

[img1]: https://github.com/campelo/documentation-dev.to/blob/master/sharepoint/how-to-remove-thousands-separator-of-a-number-column/assets/img1.png "Image 1" 
[img2]: https://github.com/campelo/documentation-dev.to/blob/master/sharepoint/how-to-remove-thousands-separator-of-a-number-column/assets/img2.png "Image 2" 
[img3]: https://github.com/campelo/documentation-dev.to/blob/master/sharepoint/how-to-remove-thousands-separator-of-a-number-column/assets/img3.png "Image 3" 
[img4]: https://github.com/campelo/documentation-dev.to/blob/master/sharepoint/how-to-remove-thousands-separator-of-a-number-column/assets/img4.png "Image 4" 