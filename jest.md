# Introduction to Jest
Jest is a testing platform built by Facebook for testing JavaScript applications. It is touted as providing a "zero configuration" experience to enable developers to write more test faster and more efficiently. You can read more on the [Jest Website](https://jestjs.io/).

## Snapshot testing 
Snapshot testing saves a 'snapshot' of your user interface that you can then later use for comparison when updates are made to your components. If the newly rendered component does not match the expected (i.e., the saved snapshot), the test will fail. Snapshot testing is a useful tool if you want to make sure your user interface does not change unexpectedly and works best when the user interface has been hardened/will not be changing often. It is not useful to attempt snapshot testing with a dynamic interface, though you can use multiple snapshots to test various allowable states of your components.

> Jest also offers the ability to run unit tests, integration tests, and component test by utilizing [JSDOM](https://airbnb.io/enzyme/docs/guides/jsdom.html), which will run the continuous integrations normally without a browser configuration.

Snapshot testing should be focused specifically on individual components within the application. Some possible areas for snapshot testing include:
* Form control components
* Navigation components
* Layout components
* Buttons and Indicator components
* Popups and Modal components

## Support
Jest testing can be utilized with most JavaScript frameworks and currently supports Angular and React with minimal configuration.
React projects have the Jest framework built-in as long as the project was created using the ```create-react-app``` CLI. Angular projects require some manual setup since Jest is not built in.

## Installation
To start testing with Jest, install the tools below and follow the basic example .

### React
```
yarn add jest –dev
yarn add renderer –dev
yarn add @babel/runtime –dev
```
```
// YourTestFile.test.js
import renderer from 'react-test-renderer'; // configuration for test file
```

For more information, check out the [NPM package](https://www.npmjs.com/package/jest) or the [Getting Started Guide](https://jestjs.io/docs/en/getting-started) for React.

### Angular
The following will install jest, @types/jest, ts-jest, and jest-zone-patch
```
yarn add -D @types/jest jest jest-preset-angular
```
```
// YourTestFile.e2e-spec.ts
import 'jest-preset-angular'; // configuration for spec test file
import './jestGlobalMocks'; // configuration for spec test file
```
For more information, check out the [NPM package](https://www.npmjs.com/package/jest-preset-angular) or the [Getting Started Guide](https://www.xfive.co/blog/testing-angular-faster-jest/) for Angular.

### Writing Snapshot Tests
```
it('multi-select app bar renders correctly', () => {
  const tree = renderer
    .create(<Myappbar />)
    .toJSON();
  expect(tree).toMatchSnapshot();
});
```

#### Results, example:
```
// Jest Snapshot v1, https://goo.gl/fbAQLP
exports[`multi-select app bar renders correctly 1`] = `
<header
  className="MuiPaper-root-10 MuiPaper-elevation4-16 MuiAppBar-root-1 MuiAppBar-positionStatic-5 MuiAppBar-colorPrimary-8"
>
  <div
    className="MuiToolbar-root-37 MuiToolbar-regular-39 MuiToolbar-gutters-38"
  >
    <h6
      className="MuiTypography-root-41 MuiTypography-h6-58 MuiTypography-colorInherit-70"
    >
      Multiselect list
    </h6>
  </div>
</header>
`;
```
