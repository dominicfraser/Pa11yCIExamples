This repository contains a simple example of using [Pa11y CI](https://github.com/pa11y/pa11y-ci), to go with [this article](https://hackernoon.com/using-pa11y-ci-and-drone-as-accessibility-testing-gatekeepers-a8b5a3415227).

Pa11y CI is built on top of [Pa11y](https://github.com/pa11y/pa11y), providing easy JSON configuration for testing against multiple URLs. It fully supports Pa11y [Actions](https://github.com/pa11y/pa11y#actions), allowing user interaction to be mocked.

See both the example [.pa11yci.json config file](./.pa11yci.json) and [Drone continuous delivery example](./drone.md).

To run first `npm install` and then run the example using `npm run test:accessibility`.
