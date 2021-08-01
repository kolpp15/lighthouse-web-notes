# Weekend Notes

## Setting up project

1. create a new directory and a .js file
    - ex. abc.js
2. set up a test directory in the new directory
    - add a test file for the project file (ex. abcTest.js)
3. initialize the project as an NPM package
    - npm init 
    - inside package.json file, update the test script to: ./node_modules/mocha/bin/mocha
    - this way, we can test using "npm test"
4. to use mocha and chai, install the packages in the new directory
    - npm install mocha chai --save-dev



## Running all tests within the test directory

1. within the project directory call:
    - npm init -y
    - this will create package.json
2. create a "test" directory within the project folder
3. install mocha and chai in command:
    - npm install mocha chai --save-dev
4. In command, navigate to the project directory and run
    - ./node_modules/mocha/bin/mocha
    - this will run all tests within the test directory

## Set up new package.json file to use "npm test"

1. In command:
    - npm init
    - setpup a new package.json
2. Update the script part:
```
"scripts": {
  "test": "./node_modules/mocha/bin/mocha"
}
```
3. run mocha by commanding:
    - npm test