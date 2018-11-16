Selenium web-driver uses 8 locators to find elements in an application. The following are the list of object identifiers or locators supported by web-driver.

ID Select element with the specified @ID attribute
Name Select first element with the specified @Name attribute
Linktext Select link (anchor tag) element which contains text matching the specified link text
Partial Linktext Select link (anchor tag) element which contains text matching the specified partial link text
Tag Name Locate Element using a Tag Name
Class name Locate Element using a class Name
CSS Select the element using CSS selectors. 
Xpath Locate an element using an XPath expression.

Selenium locators can be classified into two categories.
Structure-based locators: locators that rely on the structure of the application to find the elements.
XPath, DOM and CSS
Attributes-based locators: locators that rely on the attributes of the elements to locate them in the application and preferred over others.
Identifier, Name, Link and CSS

Teams should consider this before choosing a locator strategy and or if your application under test supports test automation.
Most teams choose CSS because it is the most flexible and gives a good balance between using structure and attributes to find the application elements as long as the elements have naming conventions.

There is no such thing as a reliable locator in Selenium, locator strategies totally depend on how the software application is developed and what are used as attributes by the developing team for each web element.
This is the priority in which a locator can be used based on the availability within an application.
Method	Syntax	Description
By ID	driver.findElement(By.id(<element ID>))	Locates an element using the ID attribute
By name	driver.findElement(By.name(<element name>))	Locates an element using the Name attribute
By class name	driver.findElement(By.classname(<element class>))	Locates an element using the Class attribute
By tag	driver.findElement(By.tagName(<htmltagname>))	Locates an element using the HTML tag
By link text	driver.findElement(By.linkText(<linktext>))	Locates a link using link text
By partial link text	driver.findElement(By.partialLinkText(<linktext>))	Locates a link using the link’s partial text
By CSS	driver.findElement(By.cssSelector(<css selector>))	Locates an element using CSS selector 
By XPath	driver.findElement(By.xpath(<xpath>))	Locates an element using XPath query
*All other locators that follow beyond this are rarely used and require additional code to test, which is simply hard to maintain if changes occur.
ID locators are best.
IDs are the safest locator option and should always be the first choice. By W3C standards, it should be unique in the page, meaning you will never have a problem with finding more than one element matching the locator.
The ID is also independent of the element type and location in the tree and if the developing team moves an element or changes its type, WebDriver can still locate it.
IDs are often also used in the application page’s JavaScript, so a developer will avoid changing an element’s ID to avoid having to change the JavaScript.
If you have a flexible developing team or even an eye for the app source code you can always get extra IDs added into the code.
However, sometimes adding too many IDs everywhere is impractical or not viable so we need to mix in the use of CSS or Xpath locators.
CSS and Xpath locators
CSS and Xpath locators are conceptually very similar.
These types of locators with combinations of tag name, descendant elements, CSS class or element attribute makes the matching pattern strict or loose, strict meaning that small HTML changes will invalidate it and lose meaning that it might match more than one HTML element.
When writing a CSS or Xpath locators it’s all about finding the balance between strict and loose; durable enough to work with HTML changes and strict enough to fail when the app fails.
There is no doubt that 'ID' is the most reliable locator in Selenium, as it is always unique. For rest of locator strategies, you need to make sure that their occurrence is not more than once in the application area. Also, when you go with XPath and CSS, make sure you start the locator with the element having "Id" attribute.
We can also ask the development team to provide "ID" locator to web elements (Input boxes, drop downs, radio buttons, checkboxes, list boxes…etc) instead of identifying the element via other locators like css or xpath.
This is core practice followed by many automation engineers in companies that provide test automation services. Automation scripts will be reliable in this case and the chance of false positives will not be there if we use ID locators in Automation scripts.
Developer ID is another locator strategy that can be used to identify objects in application. This is some attribute with value, which can be added to HTML tag to identify it uniquely.
The below example illustrates a case when the tag had no attribute, so we talk with the development team to add the attribute.
<input ></input>
The above tag has no attribute, so with selenium we cannot identify this uniquely. So we can ask developing team to add unique developer ID to it.
<input userName="userName"></input>
Now we can identify this web element either by CSS or XPath as:
CSS=input[username='userName']
XPATH=//input[@username='userName']
The thing with all the locators except By Xpath is that they do not identify an element uniquely all the time, there can be instances where you might have two matches using the same locator and therefore By Xpath becomes the ideal choice. 
It is always advisable to use custom Xpath because more often than not they will always identify the element uniquely.
