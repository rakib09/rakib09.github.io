---
layout: post
comments: true
categories: sementicui
---


## Sementic UI Calender
Calendar module for Semantic UI. See [https://jsbin.com/ruqakehefa/](https://jsbin.com/ruqakehefa/) for example usage.
[Github Link](https://github.com/mdehoog/Semantic-UI-Calendar)

## Installation
   
   Install using bower:
   
   ```bower install --save semantic-ui-calendar```
   
   Install using npm:
   
   ```npm install --save semantic-ui-calendar```
   
   Include javascript and css in html:
   
   ```
   <script type="text/javascript" src="/bower_components/semantic-ui-calendar/dist/calendar.min.js"></script>
   <link rel="stylesheet" href="/bower_components/semantic-ui-calendar/dist/calendar.min.css" />
   ```
## Basic HTML
```
<div class="ui calendar" id="date">
    <div class="ui input left icon">
        <i class="calendar icon"></i>
        <input name="date" type="text">
    </div>
</div>
```
## Javascript Calling
```
$("#date").calendar({
    type: 'date',
    parser: app.dateParser,
    parseFormat: 'dd/MM/yyyy',
    formatter: app.dateFormatter,
    minDate: $("#date").data('min-date') ? kendo.parseDate($("#date").data('min-date'), 'dd/MM/yyyy') : null,
    maxDate: $("#date").data('max-date') ? kendo.parseDate($("#date").data('max-date'), 'dd/MM/yyyy') : null,
});
var app = {
    dateParser: {
        date: function (txtDate, settings) {
            if (!txtDate) return null;
            if (settings.parseFormat) {
                return kendo.parseDate(txtDate, settings.parseFormat);
            } else {
                return kendo.parseDate(txtDate, "dd/MM/yyyy");
            }
        }
    }
};
```


### Trigger angular value on change Calender
```
<div class="ui calendar" id="date">
    <div class="ui input left icon">
        <i class="calendar icon"></i>
        <input name="date" type="text" ng-model="angularController.element">
    </div>
</div>

$("#date").calendar({
    type: 'date',
    parser: app.dateParser,
    parseFormat: 'dd/MM/yyyy',
    formatter: app.dateFormatter,
    minDate: $("#date").data('min-date') ? kendo.parseDate($("#date").data('min-date'), 'dd/MM/yyyy') : null,
    maxDate: $("#dateOfCheque").data('max-date') ? kendo.parseDate($("#date").data('max-date'), 'dd/MM/yyyy') : null,
    onChange: function (date, text, mode) {
    var $scope = angular.element($("#date")).scope();
    $scope.$apply(function() {
        $scope.angularController.element = text;
    });
    }
});
```

### Changed value from Javascript
calendar('set date', Javascript native Date object)

```
 $('#date').calendar('set date', new Date());
```

### Initialized Backend Date to Calender

```
<div class="ui calendar" id="date">
    <div class="ui input left icon">
        <i class="calendar icon"></i>
        <input name="date" type="text" value="${g.formatDate(date: new Date(), format: 'dd/MM/yyyy')}">
    </div>
</div>
```