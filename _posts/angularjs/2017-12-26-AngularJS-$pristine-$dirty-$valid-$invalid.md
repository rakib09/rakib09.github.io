---
layout: post
title: "AngularJS - $pristine, $dirty, $valid, $invalid"
comments: true
categories: android
---

Today we will go through the AngularJS Forms validations. Forms are important part of any application. They help us to collect information from user so that it can be processed for corresponding activity. We need to validate form so that only the valid values are put in the form. For that we use JavaScript or any other JavaScript library like jQuery.

Angular also provides some help in this context. We can validate a form and see that the required validations work correctly. It provides different objects to the form. They are very helpful while validating forms:

    $pristine: It will be TRUE, if the user has not interacted with the form yet
    $dirty: It will be TRUE, if the user has already interacted with the form.
    $valid: It will be TRUE, if all containing form and controls are valid
    $invalid: It will be TRUE, if at least one containing form and control is invalid.
    $error: Is an object hash, containing references to all invalid controls or forms, where: 
        keys are validation tokens (error names)
        values are arrays of controls or forms that are invalid with given error.



There are some built in validation tokens, that can help in validating form:

    email
    max
    maxlength
    min
    minlength
    number
    pattern
    required
    url


In accordance with these AngularJS also provides corresponding CSS classes for them. We can use them for validation purpose.

    ng-pristine
    ng-dirty
    ng-valid
    ng-invalid


Lets see how we can use them. Usage:
In Form: myForm.$dirty
For Field: myForm.firldName.$dirty
In CSS:
.ng-dirty{
 background-color: yellow;
}

This is little bit information about the AngularJS form validation.
Use #ngvinod to discuss on Twitter about this.

http://www.ng-vinod.com/2014/07/angularjs-pristine-dirty-valid-invalid.html