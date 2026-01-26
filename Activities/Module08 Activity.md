---
layout: page
title: Code-Level Design
nav_exclude: true
---

# Readable Code Activity

### Getting started

Start by cloning the the [Starter Code](https://github.com/neu-se/spring-26-traffic-light-activity) from GitHub.
Run `npm install` to download the dependencies for this project, and then open it in VSC.
Run `npm run test` to run the tests of the existing code (or run the script in VSC). You will see that the tests pass.
If you run `npm run lint` you will see that there exactly 3 linting errors, all of which are in `incomeTax.ts`. You can ignore these for this activity.

### The Problem

Your team is writing a simulator for a traffic light in a large city. Whitley, an intern in your group, has written the code in `TrafficLight.ts`, and the tests in `TrafficLight.test.ts`.

Your team leader, Adrian, has asked you to critique Whitley's code based on the Five Code-Level Design Principles. Adrian says that he has already received some feedback from the client, who complained that the code expects all lights to display red to be on for 20 seconds, yellow for 5 seconds, and green for 15 seconds, but there are traffic lights in the city that do not conform to that pattern. They may have different display times, or they may have different symbols as well (e.g. left-turn arrows, etc.)

### The Task

Write a new file, called `betterTrafficLight.ts`, which uses the Principles of this module to address some of the problems raised by the customer. Put comments in your code that document your improvements.

Update `TrafficLight.test.ts` to import from `betterTrafficLight.ts`. Your code should pass all the existing tests without any modifications to them. After confirming that the existing tests pass, you are encouraged to add your own new tests in the same file to verify any extra improvements you make.

There should be no linting errors or warnings in `betterTrafficLight.ts`.

The package for this activity contains a npm script to run stryker, so you can judge the adequacy of your tests (`npm run stryker`). We encourage you to do so.

### Submit your work

Submit the file `betterTrafficLight.ts`. You are _not_ required submit your tests.

### Grading

This assignment will be graded on a Satisfactory/Minimal basis. To receive a satisfactory grade, your code must satisfy the criteria for readable code, and must address both of the problems raised by the customer. You will receive a minimal grade if your code does not satisfy the criteria for readable code, or if it does not address both of the problems raised by the customer. You will receive no credit if your code does not pass the tests in `TrafficLight.test.ts

Be sure to review Canvas assignment for submission and any other related details (if assigned).
