# Introduction

JavaScript is one of the world's most popular programming languages.  
JavaScript's popularity is due entirely to its role as the scripting language of the web.  
Virtually every personal computer has at least one JavaScript interpreter on it and in active use.  

JavaScript is a very nice dynamic object-oriented general-purpose programming language.    
It has objects which can contain data and methods that act upon that data, and can contain other objects.  
It does not have classes, but it does have constructors which do what classes do.  
It does not have class-oriented inheritance, but it does have prototype-oriented inheritance.

Some argue that JavaScript is not truly object oriented because it does not provide information hiding,  
because it does not have private variables and private methods.  
But it turns out that JavaScript objects can have private variables and private methods. 

Some argue that JavaScript is not truly object oriented because it does not provide inheritance.   
But it turns out that JavaScript supports not only classical inheritance, but other code reuse patterns as well.

Few understand JavaScript because JavaScript is the world's most misunderstood programming language.


## Why JavaScript?

JavaScript is a language of many contrasts, so you might wonder  
**"Why should I use JavaScript?"**  

There are two answers.  

The first is that you don't have a choice if you want to be a real (web) developer:  
JavaScript is language of the web, the only language that is found in all browsers.  

The second answer is that, despite its deficiencies, JavaScript is really good.  
JavaScript is light-weight and expressive, and once you get the hang of it, it is a lot of fun.

## A bit of history

#### 1995
*Netscape*, at that time on the cutting edge of technological innovation,  
began seriously considering the development of a client-side scripting language.

*Brendan Eich*, an engineer at Netscape, began developing *Mocha* (later called *LiveScript*),  
a scripting language for the release of the Netscape Navigator 2.

#### 1996
Netscape entered into a development alliance with *Sun Microsystems*  
to complete the implementation of LiveScript in time for release,  
and, before the release, changed LiveScript’s name to JavaScript  
to capitalize on the success of Java (despite they have little in common).  

> #### The Name
> 
> JavaScript's name has been a source of confusion ever since.  
>
> The Java- prefix suggests that JavaScript is somehow related to Java,  
> that it is a subset or less capable version of Java.  
> But JavaScript is not interpreted Java (Java is interpreted Java).  
> Compared to Java, JavaScript is betterin the applications that Java was originally intended for.
>
> The -Script suffix suggests that it is not a real programming language,  
> that a scripting language is less than a programming language.  
> But JavaScript is a surprisingly powerful language.  
> Compared to C, JavaScript trades performance for expressive power and dynamism.

Netscape released version 1.1 of the language in Netscape Navigator 3.  
The popularity of the fledgling Web was reaching new heights,  
and Netscape had positioned itself to be the leading company in the market.  

Microsoft decided to put more resources into a competing browser named Internet Explorer.  
Microsoft introduced Internet Explorer 3 with a JavaScript implementation called JScript  
(so called to avoid any possible licensing issues with Netscape). 

> Microsoft’s implementation of JavaScript meant that there were different versions of the langauge floating around.  
> JavaScript had no standards governing its syntax or features, and its different versions highlighted this problem. 

#### 1997

With industry fears mounting, it was decided that the language must be standardized.  
So Netscape submitted JavaScript 1.1 to the European Computer Manufacturers Association (Ecma) as a proposal. 

ECMA defined a new standard of the scripting language named *ECMAScript* (pronounced as "ek-ma-script").

The ISO and IEC (ISO/IEC) adopted ECMAScript as a standard (ISO/IEC-16262).  

> #### Technical Committee #39
> TC39 was made up of programmers from Netscape, Sun, Microsoft, Borland, NOMBAS, and other companies, to  
> *standardize the syntax and semantics of a general purpose, cross-platform, vendor-neutral scripting language*  
> (www.ecma-international.org/memento/TC39.htm). 

#### 1999

The standard received a significant update as ECMAScript edition 3,  
and has stayed pretty much stable ever since. 

The fourth edition was abandoned, due to political differences concerning language complexity.  
Many parts of the fourth edition formed a basis of the new ECMAScript edition 5.

#### 2009 

The new ECMA published in December of 2009.

### toward the Future

We can only speculate what the future will be, but it's quite certain that it will include JavaScript.  
For quite some time JavaScript may have been underestimated and underused (or rather overused in the wrong ways),  
but every day we witness new uses of JavaScript in much more interesting and creative ways.  

Where they once wrote simple one-liners, often embedded in-line in HTML tag attributes (such as onclick),  
developers nowadays ship sophisticated, well-designed and architected, extensible applications, and libraries.  
JavaScript is indeed taken seriously and developers are starting to rediscover it  
and enjoy its unique object-oriented features more and more.

## JavaScript everywhere

An interesting thing about JavaScript is that it always runs inside a *host environment*.  
The browser is the most popular host environment, but it is not the only one.  
JavaScript can run on the server, on the desktop, and in rich media. 

Today, you can use JavaScript to do all of this:

* create rich and powerful client-side web applications
* build fast, scalable, network, server-side application
* create rich media applications using the HTML5 APIs
* write scripts that automate administrative tasks on your Windows desktop, using Windows Scripting Host
* write extensions/plugins for a plethora of desktop application such as Firefox, Dreamweaver, and Fiddler
* create web applications that store information in an off-line database on the user's desktop, using Google Gears
* create Yahoo! Widgets, Mac Dashboard widgets, that run on your desktop
* ...

JavaScript started inside web pages, but today it's safe to say it is practically everywhere.

## Hello JavaScript world!

JavaScript is designed to run as a scripting language in a host environment,  
so, unlike most programming languages, it has no concept of input or output,  
but rely on the host environment to provide mechanisms for communicating with the outside world.  

#### in the browser

`hello.html`:  

```html
<!DOCTYPE html>
<html>
<head>
  <title>...</title>
</head>
<body>
  <script src="hello.js"></script>
</body>
</html>
```

`hello.js`:  

```js
document.write('Hello JavaScript!');
```
