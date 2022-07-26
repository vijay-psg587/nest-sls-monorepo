## **SQ Module**

> This is a standalone nestjs application. Potentially interacting with Github APIs to

-   Create a repo in github provided a github handlerId - that should follow some conventions
-   Create and populate secrets in github
-   Add the provided github handler as colloborator to the project with Admin access

### **Deployment**

-   This app will be deployed as a docker container into a lambda
-   This will make use of `serverless` framework for deployment
-   Resources in aws are created via some IaC providers like terraform/cloudformation/cdk, but that is not covered in this

### **Debugging**

-   Added start script to start sq-module
-   Added [launch.json](./../../../.vscode/launch.json) with `sqModeule-debug` configuration

### **Assumption**

-   Standalone module that is going to make use of [common](./../../libs/common/src/lib/common.module.ts) module
-   Should make use of configurations from env variable declared inside [.env](./../../config/development/.env) for the dev environment and these should be supplied via aws SSM. For now make use of the same from .env

### **Libs Used**

-   Middly - middleware for aws lambda
-   Class transformer and class validator for json marshalling and unmarshalling
-   Date-fns for dealing with dates and timestamps

### **Patterns Followed**

-   Decorator pattern with guards & logging
-   Middleware pattern to handle exceptions using middy
-   Singleton pattern with different types of scopes - `Request` scoped.
-   DI by default provided by `Nest IoC` container

### **Steps to Run**

-   Create the env variables in the desired location. You can follow the [template](./../../env-template/template.json)
-   Make sure to populate `NODE_LOCAL_DEV` as dev for local testing
-   Run `npm run start:sq-Module`
-   To debug run `sqModule-debug` config in vscode. For other IDEs use your own configuration

TODO:

    - Supply environments from aws SSM param block
    - Identify mechanisms for rollbacks in lambda
