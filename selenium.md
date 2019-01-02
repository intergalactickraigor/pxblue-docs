# Testing with Selenium Web-Driver
WebDriver is a web automation framework that allows you to execute your tests against different browsers. WebDriver also enables you to use a programming language in creating your test scripts. https://www.seleniumhq.org/projects/webdriver/

## Identifying elements in an application
Selenium web-driver uses 8 locators to find elements in an application:

| Locator | Description | Syntax/Example |
|-------|-----------|--------------|
|ID|Finds the first element matching the specified **id** attribute (should be unique)|```driver.findElement(By.id('myId'))```|
|Name|Finds the first element matching the specified **name** attribute|```driver.findElement(By.name('myName'))```|
|Class|Finds the first element matching the specified **class** attribute|```driver.findElement(By.classname('myCLass'))```|
|Tag|Finds the first element of the specified HTML **tag**|```driver.findElement(By.tagName('div'))```|
|Link Text|Finds the first ```<a>``` element whose link text ***exactly*** matches the specified text|```driver.findElement(By.linkText('Sign Up!'))```|
|Partial Link Text|Finds the first ```<a>``` element whose link text ***contains*** the specified text|```driver.findElement(By.partialLinkText('Home'))```|
|CSS|Finds the first element matching the specified CSS selector|```driver.findElement(By.cssSelector('.link:first-of-type'))```|
|XPath|Finds the first element matching the specified XPath query|```driver.findElement(By.xpath('//input[@username="userName"]'))```|

>**Does class require an axact match or will it match one of many classes that are on the element?**

>**Should classname be camelCase?**

>**What is XPath?**
 
### Categories of Locators
Selenium locators can be classified into two categories.

1. Structure-based locators: locators that rely on the structure of the DOM to find the elements.
    * XPath, Tag, and CSS
2. Attributes-based locators: locators that rely on element attributes to locate them.
    * ID, Name, Link, and CSS
    * These are generally prefered over structure-based locators because they are less prone to breaking changes.
    
>**Why is CSS in both?**

Teams should weigh the pros/cons of these two categories before choosing a testing strategy. Most teams choose to use the CSS locator because it is the most flexible and gives a good balance between using structure and attributes to find the application elements, provided that proper naming conventions are followed.

### Choosing a locator strategy
There is no such thing as a 100% reliable locator in Selenium. The right approach will depend on how the software application is developed and what sort of attributes are being used by the development team on various elements.

#### Preferred order of applicability
In general, this is the order in which you should try to use various locator types, if the option is available (i.e., if your team does not use IDs, try using Name...etc.).

1. ID
2. Name
3. Class
4. Tag
5. Link Text
6. Partial Link Text
7. CSS
8. XPath

Any other locator types beyond this are rarely used and require additional code to test, which is difficult to maintain if and when changes occur.

##### ID Locators
ID locators are generally the safest locator option and should always be the first choice. By W3C standards, IDs should be unique on the page, meaning you will never have a problem with finding more than one element matching the locator. The ID is also independent of the element type and location in the tree, so if the developing team moves an element or changes its type, WebDriver can still locate it.

This is the standard practice followed by many automation engineers in companies providing test automation services. Automation scripts based on IDs will be reliable and the chance of false positives will be very low.

If you have a flexible development team or access to the source code, you can request additional IDs be added into the code (on elements such as textfields, radio buttons, checkboxes, etc.). There is no harm in having an id on an element, except that it may unnecessarily bloat the code or make it more difficult to read if they are used in excess. In this case, we may need to mix in the use of other locators (e.g., CSS or XPath).

##### CSS and Xpath Locators
CSS and Xpath locators are very similar to one another. These locators can use combinations of HTML tag name, descendant elements, CSS class, or element attribute to make the matching pattern strict or loose, depending on need. Strict patterns risk small HTML changes causing them to break, while loose patterns risk matching more than one element.

When writing a CSS or Xpath locator, the trick is finding the balance between strict and loose - you want it to be durable enough to withstand HTML changes, but strict enough to fail when the app fails. A good rule of thumb is to make sure to start your CSS or XPath locators with an element that has an ID attribute.

CSS and XPath also allow you to select elements based on a custom attribute. For example:

```<input userName="userName"></input>```

We can identify this web element either by CSS or XPath as:
* CSS: input[username='userName']
* XPATH: //input[@username='userName']

For all locator types, with the exception of XPath, there is the possibility that they do not identify an element uniquely every time. There may be instances where you have two matches using the same locator and therefore By Xpath becomes the ideal choice. 
It is always advisable to use custom Xpath because **more often than not** they will always identify the element uniquely.

> **This last paragraph doesn't make sense: Is XPath always a unique match or not? It says both...**
