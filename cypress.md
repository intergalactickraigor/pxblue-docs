# Testing with Cypress.io
Cypress is a next-generation, open-source front-end testing framework built for the web that works with all modern Javascript frameworks. It addresses many of the pain points developers and test engineers often face when testing modern applications, making it simple to:

* [Set up tests](https://docs.cypress.io/guides/overview/why-cypress.html#Setting-up-tests)
* [Write tests](https://docs.cypress.io/guides/overview/why-cypress.html#Writing-tests)
* [Run tests](https://docs.cypress.io/guides/overview/why-cypress.html#Running-tests)
* [Debug Tests](https://docs.cypress.io/guides/overview/why-cypress.html#Debugging-tests)

Cypress is often compared to Selenium, however there are many fundamental/architectural difference between the two. Cypress is not constrained by the same restrictions as Selenium and enables you to write faster, easier and more reliable tests. Most other testing tools (like Selenium) operate by running outside of the browser and executing remote commands across the network. Cypress is the exact opposite. Cypress is executed in the same run loop as the application and backed by a Node.js server process. Having access to both parts (front and back) gives us the ability to respond to the application’s events in real time, while at the same time work outside of the browser for tasks that require a higher privilege. Cypress also operates at the network layer by reading and altering web traffic on the fly. This enables Cypress to not only modify everything coming in and out of the browser, but also to change code that may interfere with its ability to automate the browser. Learn more about [Cypress Architecture and key differences](https://docs.cypress.io/guides/overview/key-differences.html#Architecture)

Some of the advantages of Cypress are listed below.

## Capabilities

Cypress enables you to write all types of tests:

* End-to-end tests
* Integration tests
* Unit tests
* HTTP web requests
* API and services

and is capable of producing many testing artifacts, such as:
* Snapshots
* Recordings
* Code coverage analysis
* Reports

## How it works

Cypress includes a free, locally-installed Test Runner and a Dashboard Service for running tests in a unique interactive runner that allows you to see commands as they execute while also viewing the application under test. It's straightforward to set up and easy to start writing tests every day while your application is being developed.

After building a suite of tests and integrating Cypress with your CI provider, the Dashboard Service can record your test runs. Video recordings and snapshots are then available for you to view as artifacts, so you’ll never have to wonder, "why did this fail?".

### Advantages over other tools

A common pain point in UI test automation and end-to-end testing is that modern Javascript platforms are constantly changing, particularly in the open source community. The majority of front end development frameworks auto-generate IDs and classes for components that are used internally, but this can make it difficult to locate elements via test automation tooling. Identifying elements by these values (e.g., using IDs, CSS or xPath locators "without" property attributes) makes your tests brittle because they are subject to change any time a new version comes out (or even any time the page is refreshed).

Working with web-driver types of testing frameworks will require additional tools to help identify elements on a page, such as Selenium's page object generator or browser developer tools that assists in writing tests, unlike Cypress. 

#### Examples of common elements and finding selectors 
For example, identifying a delete button:

1) Selenium page object generator via css:
        
        @FindBy(css = "app footer.mat-simple-snackbar div button:nth-of-type(1)") @CacheLookup private WebElement delete;
        
2) Browser developer tools:
        
        <mat-icon _ngcontent-c6="" class="mat-icon material-icons" role="img" aria-hidden="true">delete</mat-icon>
        
3) Browser developer tools via selector:
        
        body > app > footer > div > button:nth-child(1) > span > mat-icon
        
4) Browser developer tools via xPath:
        
        /html/body/app/footer/div/button[1]

The common example above will require additional work to use in a web-driver type framework automation test. It will require changes to the TypeScript or Javascript code to provide unique IDs (and some Javascript platforms will actually override these with their automatically generated IDs anyway). If you have an existing application, going back and making (potentially) breaking changes (i.e., changing element IDs) to the code is not desirable. With web-driver testing type frameworks, you can simply add a "dev-id" to the element's html and use that ID as the unique identifying characteristic for the selector.

```
<div>
    <button mat-icon-button (click)="deleteItems()" dev-id="snackbar-delete-btn">
        <mat-icon>delete</mat-icon>
    </button>
</div>
```

After adding the "dev-id" to the element, the identification of the delete button will never have to change, making it safe even if the underlying component code changes. When you inspect the web element via developer tools you will now see the "dev-id" in the attributes property of the element, containing nodeValue="snackbar-delete-btn". This approach is common and now the delete button can be called by its locator and selector via ID, CSS or xPath making it more reliable because it contains a structure-based location with a custom attribute of "dev-id".
Example of the element with dev-id:
```
<button _ngcontent-c6="" dev-id="snackbar-delete-btn" mat-icon-button="" class="mat-icon-button">
    <span class="mat-button-wrapper">
        <mat-icon _ngcontent-c6="" class="mat-icon material-icons" role="img" aria-hidden="true">delete</mat-icon>
    </span>
    <div class="mat-button-ripple mat-ripple mat-button-ripple-round" matripple="" ng-reflect-centered="true" ng-reflect-disabled="false" ng-reflect-trigger="[object HTMLButtonElement]"></div>
    <div class="mat-button-focus-overlay"></div>
</button>
```
Example of use in a test
```
getDeleteButton() {return element(by.css('button.mat-icon-button:nth-of-type(1)')).getId(dev-id);})
WebElement click = driver.findelement(by.css('button.mat-icon-button:nth-of-type(1)')).click();

WebElement click = driver.findElement(By.id("snackbar-delete-btn")).click();

WebElement click = driver.findElement(By.xpath("//button[contains(@dev-id='snackbar-delete-btn')]")).click();
```

### Cypress Selector Playground
You can save time by utilizing the Cypress selector playground, a tool that is bundled with the testing framework. Similar to the code examples above and adding custom attributes to elements, Cypress works with many identifiers automatically and the Selector Playground will find them in the test runner. By adding any of these property types to your application under test, Cypress will locate the exact match and suggest how to interact with it.
Default Selectors and Priority:

* data-cy
* data-test
* data-testid
* id
* class
* tag
* attributes
* nth-child

This simplifies your selector logic and makes your selectors much more readable. You can take advantage of this by using a [data-cy] attribute on your element:

```
<div>
    <button mat-icon-button (click)="deleteItems()" data-cy="snackbar-delete-btn">
        <mat-icon>delete</mat-icon>
    </button>
</div>
```
Example of use in a test

```cy.get('[data-cy=snackbar-delete-btn] > .mat-button-wrapper > .mat-icon').click()```

or

```cy.get('[data-cy=snackbar-delete-btn]').click()```

## Getting Started
To get started , you should have a look at the [Cypress.io getting started guide](https://docs.cypress.io/guides/getting-started/installing-cypress.html#System-requirements). The key steps are outlined below.

1. Install dependencies

        yarn add --dev cypress mocha chai chance wait-on start-server-and-test
 
    | Package | Description |
    |-------|--------|
    |cypress|core package|
    |mocha|Cypress dependency|
    |chai|Cypress dependency|
    |chance| (optional) useful tool for generating random strings, numbers, etc. - helps reduce time when writing tests|
    |wait-on| (optional) module to wait on CI server before cypress runs|
    |start-server-and-test|(optional) another way to wait on CI server before running cypress|
    
2. Add cypress to package.json scripts:

        "scripts": {
            "cypress:open": "cypress open"
        }

3. Start your project

        yarn start

4. In a new terminal, start Cypress

        cd path/to/project
        cypress open
        
If this is the first time cypress has run on the project, it will create a default folder structure in the root of your project and include example tests.
5. You can simulate how Cypress runs in headless mode locally by running

        cypress run
