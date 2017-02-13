###Shrinking Navigation Bar When Scrolling Down - Bootstrap 3 Navigation & jQuery
**Demo**: http://trungk18.github.io/Resizing-Header-On-Scroll

In this template, I will show you how to create an animated fixed navigation that will resize on scroll and when you scroll down the page a bit, the header resizes smaller, and gets back bigger when you scroll back to the top with just simple CSS3 animation and jQuery.

####Sticky Navigation

> To make a sticky nav you need to add the class navbar-fixed-top to your nav

Official documentation:
http://getbootstrap.com/components/#navbar-fixed-top
 
Let�s now take a look at our HTML markup. The markup consists of a header with a logo and navigation, some sections with color difference only. 

```html
<!-- Navigation -->
    <nav class="navbar navbar-default navbar-fixed-top">
        <div class="container">
            <!-- Brand and toggle get grouped for better mobile display -->
            <div class="navbar-header page-scroll">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#top-nav">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                <a class="brand" href="http://trungk18.github.io/"><img src="trungk18.png" class="img-responsive" title="trungk18" /></a>
            </div>
            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse" id="top-nav">
                <ul class="nav navbar-nav navbar-right">
                    <li class="page-scroll">
                        <a href="#portfolio">Portfolio</a>
                    </li>
                    <li class="page-scroll">
                        <a href="#about">About</a>
                    </li>
                    <li class="page-scroll">
                        <a href="#contact">Contact</a>
                    </li>
                </ul>
            </div>
            <!-- /.navbar-collapse -->
        </div>
        <!-- /.container-fluid -->
    </nav>

    <!-- Content Section -->
    <div class="content">
        <section id="portfolio"></section>
        <section id="about"></section>
        <section id="contact"></section>
    </div>
```

I am using navbar-default from bootstrap with navbar-fixed-top to make it stick to the top of webpage. The HTML is fairly straightforward. 

####Now take a look at CSS.

Class .navbar-default was set the padding top and down for 30px each, and the transition is based on padding. When the navbar gets resized on scroll, I shrink the value to 10px by adding child class navbar-shrink.
Finally, I added some example media queries so that our animated resizing navigation will work only in medium devices desktops [Bootstrap standard grid](http://getbootstrap.com/css/#grid). 

```css
    @media screen and (min-width: 992px) {

        .navbar-default {
            padding: 30px 0;
            transition: padding 0.3s;
        }

            .navbar-default.navbar-shrink {
                padding: 10px 0;
            }
    }

    .navbar-default a {
        color: #4D4D4D;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        text-transform: uppercase;
        text-decoration: none;
        line-height: 42px;
        font-weight: 700;
        font-size: 20px;
    }

    .navbar-default a.brand > img {            
        max-width: 70px;
    }

        .navbar-default a.active {
            color: #2dbccb;
        }


    .content {
        position: absolute;
        width: 100%;
        height: 100%;
    }

        .content > section {
            width: 100%;
            height: 100%;
        }

    #portfolio {
        background: #2dbccb;
    }

    #about {
        background-color: #eb7e7f;
    }

    #contact {
        background-color: #415c71;
    }
```

To make it happen, I am going to use jQuery to add and remove the class *navbar-shrink* when we scroll a certain amount (in this situation is 50px). Adding and removing this class will animate the navbar.

```javascript
    $(document).ready(function () {
        $(window).scroll(function () {

            //Method 1: Using addClass and removeClass
            //if ($(document).scrollTop() > 50) {
            //    $('.navbar-default').addClass('navbar-shrink');
            //} else {
            //    $('.navbar-default').removeClass('navbar-shrink');
            //}

            //Method 2: Using toggleClass
            $(".navbar-default").toggleClass("navbar-shrink", $(this).scrollTop() > 50)
        });
    });
```
We can use [toggleClass](http://api.jquery.com/toggleclass/) with 2 parameter. 
- The *first parameter* will be the target element.
- The *second parameter* for determining whether the class should be added or removed. If this parameter's value is true, then the class is added; if false, the class is removed.

####Conclusion
Nowadays it is not really hard to search for component we need to use in our front-end project, but the most important thing is you can understand how it�s worked and you can easily implement this animated resizing header into your next project.�
Thanks for checking it out and view the demo, feel free to fork and fix the source code then pull back to me.