# CB Online Widgets

> CB Online Widgets


Citybreak online3 comes with a set of standard widgets these widgets are fully customizable with its own CSS that can be sent in as a parameter, thus making it possible to change the style in different locations.
The widgets are JavaScript widgets that are easy to integrate with a few lines of code.


## Implementation

```javascript
<script type="text/javascript">
        (function() {
              var widget = document.createElement('script'); widget.type = 'text/javascript'; widget.async = true;
               widget.src = 'WIDGET_URL';
              var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(widget, s);
        })();
</script>
```

```html
<div id="citybreak_accommodation_searchform_widget"></div>
```

To implement the widgets you need to add two things to your webpage:

1. A script tag that points to our server. Should be loaded asynchronously by using the below script added just before </head>. Replace WIDGET_URL with a URL constructed according to instructions below.



2. A div tag somewhere in the document body with an id parameter for each widget. This is where the widget will be inserted into the document. There is a separate id for each widget, e.g:



## Combine widgets

To enable multiple Online3 widgets on the same page, it is required to use the "combine widget" in Online3. This is a widget that simply loads several widgets at once and inserts them in their corresponding div elements.

The combine widget is located at: /combinewidget/combine

The combine widget requires three parameters:

Parameter | Description
--------- | -----------
c= | Controller - A list of names of controllers for the desired widgets, e.g. "c=accommodationwidget&c=basketwidget&c=ferrywidget"
a= | Action - A list of names of actions for the widget controllers specified in the "c" parameter, e.g. "a=searchform&a=minibasket&a=searchform". This would pass "searchform" as an action to "accommodationwidget", "minibasket" as an action to "basketwidget" and "searchform" as an action to "ferrywidget".
p= | Parameters - A list of parameters to each widget action specified by the "c" and "a" parameters. To pass multiple parameters to a widget, use a semicolon-separated list of keys and values, e.g. "p=defaultCategoryId=1345;defaultRoomCfg=2&p=&p=alignDirection=2". This would send defaultCategoryId=1345 and defaultRoomCfg=2 to /accommodationwidget/searchform, an empty list of parameters to /basketwidget/minibasket and "alignDirection=2" to /ferrywidget/searchform in the previous examples. The parameters have to be passed in the correct order, i.e. the value of the first "a" parameter will be passed to the first "c" parameter and so on. The parameters must exactly match, i.e. if you have three controllers ("c" parameters) you have to pass three actions ("a" parameters) and three parameter values ("p" parameters).

### Example
```javascript
<script type="text/javascript">
        (function() {
              var widget = document.createElement('script'); widget.type = 'text/javascript'; widget.async = true;
               widget.src = 'ONLINE3URL/combinewidget/combine?c=accommodationwidget&c=basketwidget&c=ferrywidget&a=searchform&a=minibasket&a=searchform&p=defaultCategoryId=1345;defaultRoomCfg=2&p=&p=alignDirection=2';
              var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(widget, s);
        })();
</script>
```

```html
<div id="citybreak_accommodation_searchform_widget"></div>
<div id="citybreak_basket_minibasket_widget"></div>
<div id="citybreak_ferry_searchform_widget"></div>
```

## Accommodation search form

Script resource: /accommodationwidget/searchform
Div tag Id: citybreak_accommodation_searchform_widget

### Valid parameters

```cs
String css
//URL to where the CSS can found, if not submitted the default CSS will be used.

int? defaultCategoryId
//To set a default category on the widget, the Id category can be found in the dropdownlist of the widget, the category tree is administered in CBIS

String defaultRoomCfg
//This is a string that can be set the default number of room/adults/children, the string is build up by using our format.
```

### Parameters for number of rooms/cabins and guests

You define the number of adults and children (including the child’s age) that will stay in each room as parameters in the direct search, so called ”Room configuration”. It can for example be a search with two rooms where the first room shall have two adults and the other room shall have one adult and a child with age 5.

* “&pr”  is the base parameter for the room configuration that shall be searched.
* “a“ is the separator between adults and children.
* “r“ is the separator if the search is made on more rooms than one.
* “c“ is the separator if the search shall be made on more than one child.

Example:

* One room with one adults is entered ”&pr=1”
* Three  rooms with one adult in each room is entered “&pr=1r1r1“
* One room with one adult and one child (10 yrs) is entered “&pr=1a10“
* One room with one adult and two children (10, 12 yrs) is entered “&pr=1a10c12
* Two rooms with one adult and two children (10, 12 yrs) in the first room and two adults in the second room is entered “&pr=1a10c12r2“

```cs
DateTime? defaultArrivalDate
//A valid date to set the default arrival date in the widget, the format of the date must be the same as the format of the requested widget

DateTime? defaultDepartureDate
//A valid date to set the default departure date in the widget, the format of the date must be the same as the format of the requested widget

int? alignDirection
//Use this to position objects in the widget either to the left or to the right.
//0 = objects will be aligned to the left(default)
//2 = objects will be aligned to the right.

int? geoNodeId
//Use this to set a default geo node in the widget, this parameter will render the name of the geonode in textbox “Where do you want to go”.

int? productId
//Use this to set a default product in the widget, this parameter will render the name of the product in textbox “Where do you want to go”.

bool? lockCategory
//Use this parameter to lock down the category dropdown, when this is set then the dropdown with the categories will be hidden, and the auto complete of the “where do you want to go” will only display objects that are of / has this category.

String promotionCode
//Use this parameter if you want to set a promotion code in the promotion code field.
```

## Rental car search form

Script resource: /carrentalwidget/searchform
Div tag Id: citybreak_accommodation_searchform_widget

### Valid parameters

```cs
string css
//URL to where the CSS can found, if not submitted the default CSS will be used.

int? alignDirection
//Use this to position objects in the widget either to the left or to the right.
//0=objects will be aligned to the left (default)
//2=objects will be aligned to the right.
```

## Ferry search form

Script resource: /ferrywidget/searchform
Div tag Id: citybreak_ferry_searchform_widget

### Valid parameters

```cs
string css
//URL to where the CSS can found, if not submitted the default CSS will be used.

int? alignDirection
//Use this to position objects in the widget either to the left or to the right.
//0=objects will be aligned to the left (default)
//2=objects will be aligned to the right.
```

## Flight search form

Script resource /flightwidget/searchform
Div tag Id: citybreak_flight_searchform_widget

### Valid parameters

```cs
string css
//URL to where the CSS can found, if not submitted the default CSS will be used.

int? alignDirection
//Use this to position objects in the widget either to the left or to the right.
//0=objects will be aligned to the left (default)
//2=objects will be aligned to the right.

string defaultArrivalDate
//Use this to configure a default arrival date.

string defaultDepartureDate
//Use this to configure a default departure date.

bool? preselectFlexibleDates
//Use this to preselect flexible date search.
//True = flexible date search is preselected

int? preselectedEndLocationId
//Use this to preselect a end location id (aggregator location id).

bool? lockEndLocation
//Use this to locked/disabled changing the end location.
//True = changing end location is locked/disabled

int? sgid
//Use this to preselect start location using a CBIS geonode id.
```

## My booking basket 

Script resource: /basketwidget/minibasket
Div tag Id: citybreak_basket_minibasket_widget


## Activity transport search form widget

Script resource activitytransportwidget/searchform
Div tag Id: citybreak_activity_transport_searchform_widget

### Valid parameters

```cs
int cbisProductId
//The id of the product to display the search form for.
```

## Activity booking widget

This widget does not take a product id as parameter, instead you initialize it with javascript. This enables you to show multiple booking widgets on the same page.

Script resource activitywidget/booking
Div tag Id: citybreak_activity_booking_widget

### Valid parameters

```cs
string css
//URL to where the CSS can found, if not submitted the default CSS will be used.
```

### Initialization

To initialize a widget, create a container for the product and run initContainer with the required cbisProductId option.

```javascript
<script type="text/javascript">
  (function() {
   document.addEventListener('cb-activity-widget-loaded', function() {
       window.citybreakActivityBooking.initContainer(document.getElementById('activity_booking_widget-12345'), { 
            cbisProductId: 12345
        });
       window.citybreakActivityBooking.initContainer(citybreakjq('#activity_booking_widget-67891'), {
            cbisProductId: 67891
        });
    }, false);
  })();
</script>
```

```html
<div id="citybreak_activity_booking_widget">
   <div id="activity_booking_widget-12345"></div>
   <div id="activity_booking_widget-67891"></div>
</div>
```

Valid options to initContainer are:

```json
{
  cbisProductId: [required, int] a CBIS product id,
  proceedToBasket: [bool] whether to proceed to basket after booking, defaults to true,
  defaultDate: [date] a default selected date (Use JS new date format),
  startDate: [date] minimum selectable date,
  endDate: [date] maximum selectable date
}
```

### Booking event

You may also customize the booking process with the proceedToBasket option and cb-activity-booked event.

```javascript
<script type="text/javascript">
  (function() {
   document.addEventListener('cb-activity-booked', function(data) {
        console.log("Activity booked?: " + data.detail.success);
    }, false);
   document.addEventListener('cb-activity-widget-loaded', function() {
       window.citybreakActivityBooking.initContainer(document.getElementById('activity_booking_widget-12345'), {
            cbisProductId: 12345,
            proceedToBasket: false
        });
    }, false);
  })();
</script>
```

```html
<div id="citybreak_activity_booking_widget">
   <div id="activity_booking_widget-12345"></div>
</div>
```

The cb-activity-booked event receives:

```json
detail: {
    cbisProductId: a CBIS product id of the booked product,
    basketProductIds: a list of resulting basket product ids,
    complementaryUrl: url to complementary page (will redirect to basket if no complementary options are available),
    success: [bool] whether the product was added successfully to basket
}
```


### NOTE, ADD CABIN-FERRY Widgets
### NOTE, ADD CABIN-FERRY-NUPAC Widgets
