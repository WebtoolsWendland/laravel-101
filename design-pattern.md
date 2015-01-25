# Design Pattern

## Introduction

In software engineering, a design pattern is a general reusable solution to a commonly occurring problem within a given context in software design. A design pattern is not a finished design that can be transformed directly into source or machine code[^1].

Read <http://www.phptherightway.com/pages/Design-Patterns.html>. 
## Model-View-Controller

MVC is an User-Interface Pattern[^2], It divides a given software application into three interconnected parts, so as to separate internal representations of information from the ways that information is presented to or accepted from the user[^3].

![MVC Process](images/mvc-process.svg)

* **Models** serve as a data access layer where data is fetched and returned in formats usable throughout your application.
* **Controllers** handle the request, process the data returned from models and load views to send in the response.
* **Views** are display templates (markup, xml, etc) that are sent in the response to the web browser.

## References

* [MVC and ADR are User-Interface Patterns, Not Application Architectures](http://paul-m-jones.com/archives/6079)
* [http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller](Model-view-controller)

[1]: http://en.wikipedia.org/wiki/Software_design_pattern "Software design pattern"
[2]: http://paul-m-jones.com/archives/6079 "MVC and ADR are User-Interface Patterns, Not Application Architectures"
[3]: http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller "Model-view-controller"