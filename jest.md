#Jest Snapshot testing 
Integrated testing solution written by Facebook and is a useful tool if you want to make sure your User Interface does not change unexpectedly. Snapshot testing works best when the User Interface has been hardened or the User Interface will not be changing often.

Jest also offers the ability to run all tests including unit tests, integration tests and component test by utilizing the jsdom and will run in the Continuous Integrations normally without a browser configuration.

Jest Snapshot testing should be focused specifically on components within the application by rendering each component one by one.
##Examples of component areas for snapshot testing:
Form control components
Navigation components
Layout components
Buttons and Indicator components
Popups and Modal components

Jest Snapshot testing can be achieved on most Java platforms and currently supports Angular and React with minimal configurations.
React projects have the Jest framework built-in, if the project was setup using the “create-react-app” cli.
Angular projects require manual configuration since Jest is not built in.

To start Snapshot testing install the tools below and follow the basic example 

React:
Yarn add jest –dev (only if jest does not exist in project)
Yarn add renderer –dev
yarn add @babel/runtime –dev
import renderer from 'react-test-renderer'; (configuration for test file)

Package information
https://www.npmjs.com/package/jest

Jest getting started for React projects.
https://jestjs.io/docs/en/getting-started

Angular:
yarn add -D @types/jest jest jest-preset-angular (This will install jest, @types/jest, ts-jest, jest-zone-patch)
import 'jest-preset-angular'; (configuration for spec test file)
import './jestGlobalMocks'; (configuration for spec test file)

Package information
https://www.npmjs.com/package/jest-preset-angular

Jest getting started for Angular projects
https://www.xfive.co/blog/testing-angular-faster-jest/

Test:
it('multi-select app bar renders correctly', () => {
  const tree = renderer
    .create(<Myappbar />)
    .toJSON();
  expect(tree).toMatchSnapshot();
});

Results:
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
