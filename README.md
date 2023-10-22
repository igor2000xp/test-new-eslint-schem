# Before setting up your Angular project check the current version of Angular and Node.JS on your computer.

## Checking the current version of Angular

```tsx
ng version
```
![image](https://github.com/igor2000xp/test-new-eslint-schem/assets/21989277/98670e93-99d5-487b-a9f2-6326834b9996)


## Setting up the latest version of Angular (global or local)

```tsx
npm install -g @angular/cli

// or so
npm install -g @angular/cli@latest

// or the version you need

npm install -g @angular/cli@16.1.1

// You can install the required version of Angular only in the current folder.
npm install --save-dev @angular/cli@16.1.1
```

## You can check which version of Node.JS is suitable for your version of Angular here:

[Angular CLI, Angular, Node.js, TypeScript, and RxJS version compatibility matrix. Officially part of the Angular documentation as of 2023-04-19 https://angular.io/guide/versions](https://gist.github.com/LayZeeDK/c822cc812f75bb07b7c55d07ba2719b3)

![image](https://github.com/igor2000xp/test-new-eslint-schem/assets/21989277/3f3fb16b-b5b3-4431-b677-5f8ec31edfb9)



## Some commands of nvm to manage your version of Node.JS:

```tsx
// Check and update node.js
nvm ls
nvm ls-remote
nvm ls-remote 16
nvm install --lts
nvm use 18.12.1
nvm alias default 18.12.1
```

## How to install nvm here:

[GitHub - nvm-sh/nvm: Node Version Manager - POSIX-compliant bash script to manage multiple active node.js versions](https://github.com/nvm-sh/nvm#troubleshooting-on-macos)

## Articles:
#### Migrate Angular app to ESLint with Prettier, AirBnB Styleguide, Husky and lint-staged
https://dev.to/bzvyagintsev/migrate-angular-app-to-eslint-with-prettier-airbnb-styleguide-husky-and-lint-staged-862

#### Angular ESLint
```
https://github.com/angular-eslint/angular-eslint/blob/main/.eslintrc.json

ng add @angular-eslint/schematics

npm install eslint-plugin-jasmine --save-dev

npm install eslint-plugin-import eslint-config-airbnb-typescript --save-dev

npm install eslint-config-airbnb-typescript eslint-plugin-import @ngrx/eslint-plugin --save-dev

npm i prettier eslint-config-prettier eslint-plugin-prettier --save-dev

```
### Prettier:

The question I am interested in: why do we need to use Prettier together with ESLint, if ESLint can do all the things by itself? The answer is pretty easy — Prettier formats code much better. It removes all formatting and reprints code in the consistent style from scratch. This allows developers to forget about formatting the code and not waste time discussing the code style on code reviews.
```
npm i prettier eslint-config-prettier eslint-plugin-prettier --save-dev
```

#### to the file .eslintrs.json change section extends:
```
      "extends": [
        "plugin:import/recommended",
        "eslint:recommended",
        "plugin:@typescript-eslint/recommended",
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates",
        "airbnb-typescript/base",
        "plugin:prettier/recommended"
      ],
```
#### Finally .eslintrs.json is like that:
```
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
          "tsconfig.*?.json"
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
        ],
        "import/no-extraneous-dependencies": [
          "error",
          {
            "devDependencies": true
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
        "plugin:@angular-eslint/template/recommended",
				"plugin:@angular-eslint/template/accessibility"
      ],
      "rules": {}
    },
    {
      "files": [
        "*.ts"
      ],
      "extends": [
        "plugin:@ngrx/recommended"
      ]
    },
		{
      "files": ["src/**/*.spec.ts", "src/**/*.d.ts"],
      // Jasmine rules
      "extends": ["plugin:jasmine/recommended"],
      // Plugin to run Jasmine rules
      "plugins": ["jasmine"],
      "env": { "jasmine": true },
      // Turn off 'no-unused-vars' rule
      "rules": {
        "@typescript-eslint/no-unused-vars": "off"
      }
    }
  ]
}
```
# Additional rules you can use

```json
"rules": {
        "@typescript-eslint/no-unused-vars": "warn",
        "import/prefer-default-export": "off",
        "no-useless-constructor": "off",
        "linebreak-style": "off",
        "@typescript-eslint/no-useless-constructor": "warn",
        "@angular-eslint/no-empty-lifecycle-method": "warn",
        "@typescript-eslint/no-empty-function": "warn",
        "class-methods-use-this": "off",
        "no-empty-function": "off",
        "arrow-body-style": "off",
        "no-console": "off",
      }
```
#### add into angular.json:
```
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
      }
    }
  },
```
#### Add in root project .prettierrc.json
```
{
"trailingComma": "es5",
"tabWidth": 2,
"semi": true,
"singleQuote": true,
"bracketSpacing": true,
"bracketSameLine": true,
"printWidth": 120,
"useTabs": false,
"endOfLine": "auto",
"arrowParens": "avoid"
}

```

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
