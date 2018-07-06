[Drone](https://drone.io/) is an open source [continuous delivery](https://stackify.com/continuous-delivery-vs-continuous-deployment-vs-continuous-integration/) platform that executes build and testing steps within a container based pipeline.

Pa11y CI is designed to work within such a system. If it produces an error response when running against a URL it will fail the pipeline step it is being executed in, blocking the deployment pipeline until it is resolved. 

Drone [pipelines](http://docs.drone.io/pipelines/) are written in a `drone.yml` file. The syntax is a superset of the popular docker-compose yaml specification.  Each step has a Docker image specified that the commands in the step are executed within.

An example of a Pa11y CI step would involve:

Adding a chromeLaunchConfig to our `.pa11yci.json` `"defaults":` object, otherwise Pa11y will not run in a container.

    "chromeLaunchConfig": {
      "args": ["--no-sandbox"]
    },

Running the app/ component and waiting for it to be ready (as some apps may take a few seconds to start up). For this we can `npm install -D wait-on`. We will assume a command already exists for running the app/ component.

We can then add commands such as the below to our `package.json`:

    "wait-on": "wait-on http-get://localhost:3000",
    "component:ci": "npm run component --hotReloading=false --watch=false"

We then need to specify our pipeline step:

    accessibility_test:
      image: // a Docker image that contains chrome headless
      group: tests
      commands:
        - npm run component:ci &
        - npm run wait-on
        - npm run test:accessibility

This will help to find accessibility issues detectable in code _before_ they go live. Of course this does not guarantee a fully accessible site, which requires deeper manual testing and design considerations, but it helps catch common issues.
