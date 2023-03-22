## Articles:
#### Migrate Angular app to ESLint with Prettier, AirBnB Styleguide, Husky and lint-staged
https://dev.to/bzvyagintsev/migrate-angular-app-to-eslint-with-prettier-airbnb-styleguide-husky-and-lint-staged-862

#### Angular ESLint
https://github.com/angular-eslint/angular-eslint/blob/main/.eslintrc.json

ng add @angular-eslint/schematics

npm install eslint-plugin-jasmine --save-dev

npm install eslint-plugin-import eslint-config-airbnb-typescript --save-dev

### Prettier:
The question I am interested in: why do we need to use Prettier together with ESLint, if ESLint can do all the things by itself? The answer is pretty easy — Prettier formats code much better. It removes all formatting and reprints code in the consistent style from scratch. This allows developers to forget about formatting the code and not waste time discussing the code style on code reviews.

npm i prettier eslint-config-prettier eslint-plugin-prettier --save-dev

to the file .eslintrs.json change section overrides (add red lines):
"overrides": [
{
"files": ["*.ts"],
"parserOptions": {
"project": [
"tsconfig.*?.json"
],
"createDefaultProgram": true
},

to the file .eslintrs.json change section extends:
"extends": [
"plugin:import/recommended",
"eslint:recommended",
"plugin:@typescript-eslint/recommended",
"plugin:@angular-eslint/recommended",
"plugin:@angular-eslint/template/process-inline-templates",
"airbnb-typescript/base",
"plugin:prettier/recommended"
],
add this sections:
{
"files": ["*.component.html"],
"extends": ["plugin:@angular-eslint/template/recommended"],
"rules": {
"max-len": ["warn", { "code": 140 }]
}
},
{
"files": ["*.component.ts"],
"extends": ["plugin:@angular-eslint/template/process-inline-templates"]
},

Finally .eslintrs.json is like that:
{
"root": true,
"ignorePatterns": [
"projects/**/*"
],
"overrides": [
{
"files": ["*.ts"],
"parserOptions": {
"project": [
"tsconfig.*?.json",
"e2e/tsconfig.json" - убрать!!!!!!!!!!!!
],
"createDefaultProgram": true
},
"extends": [
"plugin:import/recommended",
"eslint:recommended",
"plugin:@typescript-eslint/recommended",
"plugin:@angular-eslint/recommended",
"plugin:@angular-eslint/template/process-inline-templates",
"airbnb-typescript/base",
"plugin:prettier/recommended"
],
"rules": {
"@angular-eslint/directive-selector": [
"error",
{
"type": "attribute",
"prefix": "app",
"style": "camelCase"
}
],
"@angular-eslint/component-selector": [
"error",
{
"type": "element",
"prefix": "app",
"style": "kebab-case"
}
]
}
},
{
"files": ["*.component.html"],
"extends": ["plugin:@angular-eslint/template/recommended"],
"rules": {
"max-len": ["warn", { "code": 140 }]
}
},
{
"files": ["*.component.ts"],
"extends": ["plugin:@angular-eslint/template/process-inline-templates"]
},
{
"files": [
"*.html"
],
"extends": [
"plugin:@angular-eslint/template/recommended"
],
"rules": {}
}
]
}


add into angular.json:
"lint": {
"builder": "@angular-eslint/builder:lint",
"options": {
"lintFilePatterns": [
"src/**/*.ts",
"src/**/*.component.html",
"src/**/*.html"
]
}
}

Add in root project .prettierrc.json
{
"trailingComma": "es5",
"tabWidth": 2,
"semi": true,
"singleQuote": true,
"bracketSpacing": true,
"bracketSameLine": true,
"printWidth": 80,
"useTabs": false,
"endOfLine": "auto",
"arrowParens": "avoid"
}



# TestNewEslintSchem

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 15.2.4.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.
