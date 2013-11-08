This guide walks you through writing a simple jQuery client that consumes a Spring MVC-based [RESTful web service][u-rest].


What you will build
-------------------

You will build a jQuery client that consumes a Spring-based RESTful web service.
Specifically, the client will consume the service created in [Building a RESTful Web Servce][gs-rest-service].

The jQuery client will be accessed by opening the `index.html` file in your browser, and will consume the service accepting requests at:

    http://rest-service.guides.spring.io/greeting

The service will respond with a [JSON][u-json] representation of a greeting:

```json
{"id":1,"content":"Hello, World!"}
```

The client will render the ID and content into the DOM.


What you will need
------------------

 - About 15 minutes
 - A favorite text editor
 - A modern web browser
 - An internet connection


How to complete this guide
--------------------------

Like all Spring's [Getting Started guides](/guides/gs), you can start from scratch and complete each step, or you can bypass basic setup steps that are already familiar to you. Either way, you end up with working code.

To **start from scratch**, move on to [Create the Application Page](#scratch). When you are finished, you can compare your code with the sample code.

To **run the sample code**, do the following:

 - [Download][zip] and unzip the source repository for this guide, or clone it using [Git][u-git]:
`git clone https://github.com/spring-guides/gs-consuming-rest-jquery.git`
 - cd into `gs-consuming-rest-jquery/complete`.
 - Jump ahead to [Test the client](#test).


<a name="scratch"></a>
Create a jQuery Controller
--------------------------

First, you will create the jQuery controller module that will consume the REST service: 

`hello.js`
```js
$(function(){
    $.ajax({
        url: "http://rest-service.guides.spring.io/greeting"
    }).then(function(data) {
       $('.greeting-id').append(data.id);
       $('.greeting-content').append(data.content);
    });
});
```

This controller module is represented as a simple JavaScript function. It uses jQuery's `$.ajax()` method to consume the REST service at http://rest-service.guides.spring.io/greeting.

If successful, it will assign the JSON received to `data`, effectively making it a `Greeting` model object. The `id` and `content` are then appended to the `greeting-id` and `greeting-content` DOM elements respectively.


Create the Application Page
---------------------------

Now that you have a jQuery controller, you will create the HTML page that will load the client into the user's web browser:

`index.html`
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello jQuery</title>
    </head>

    <body>
        <div>
            <p>The ID is </p>
            <p>The content is </p>
        </div>
    </body>
</html>
```

This is a basic HTML file, but it can be modified to make it more functional. Add the following two script tags within the `<head>` section.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="hello.js"></script>
```

The first script tag loads the minified jQuery library (jquery.min.js) from a content delivery network (CDN) so that you don't have to download jQuery and place it in your project. It also loads the controller code (hello.js) from the application's path.

Now modify the `<p>` tags to include `class` attributes. Change the first to have a value of `greeting-id` and the second to have a value of `greeting-content` respectively. 

```html
<p class="greeting-id">The ID is </p>
<p class="greeting-content">The content is </p>
```

These `class` attributes help jQuery to reference the HTML elements and update the text with the values from the `id` and `content` properties of the JSON received from the REST service.

After making the modifications, your `index.html` should look like the completed version: 

`index.html`
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello jQuery</title>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
        <script src="hello.js"></script>
    </head>

    <body>
        <div>
            <p class="greeting-id">The ID is </p>
            <p class="greeting-content">The content is </p>
        </div>
    </body>
</html>
```


<a name="test"></a>
Test the client
---------------

You can now open the `index.html` page in your browser, where you see:

![Model data retrieved from the REST service is rendered into the DOM.](images/hello.png)

The ID value will increment each time you refresh the page.


Summary
-------

Congratulations! You've just developed an jQuery client that consumes a Spring-based RESTful web service.

[gs-rest-service]: /guides/gs-rest-service/
[zip]: https://github.com/spring-guides/gs-consuming-rest-jquery/archive/master.zip
[u-rest]: /understanding/REST
[u-json]: /understanding/JSON
[u-git]: /understanding/Git

