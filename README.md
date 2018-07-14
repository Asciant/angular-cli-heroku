# angular-cli-heroku
Deploy to Heroku with @angular/cli.

This project was inspired by `rbinsztock/angular-cli-heroku`. Although Rémy's project, the intention here was to provide a way to deploy to Heroku from an existing `@angular/cli` project.

## Assumptions
This project assumes:

1. You have an existing, or know how to create an `@angular/cli` project/app;
2. You have already created a Heroku Application with either the Heroku Toolbelt or Heroku Dashboard; and
3. You know how to deploy to Heroku generally, with the Heroku Toolbelt or through a GitHub repository automatic deployment.

## Express
Install express into your `@angular/cli` project with NPM:
`npm install express --save`

## heroku.js 
Save the heroku.js file to your app's root directory (same place as `package.json`.

This file creates a simply express server complements of `rbinsztock/angular-cli-heroku`.

## package.json
Within your `package.json` ensure the `"start:"` script points to `node heroku.js` and add a `heroku-postbuild` hook.

````
    "start": "node heroku.js",
    "heroku-postbuild": "ng build --aot --prod --output-path dist",
````

The `heroku-postbuild` hook will be run automatically by Heroku on deployment.

We override the `--output-path` for ease of deployment. The `outputPath` normally comes from angular.json and will usually point to `dist/projectName`. This creates obvious problems for our Express `heroku.js` server, so we insist the build uses just `dist`.

If your getting an error like `Error Not Found`, it will most likely relate to the build location from your `outputPath` not matching the paths within `heroku.js`.
