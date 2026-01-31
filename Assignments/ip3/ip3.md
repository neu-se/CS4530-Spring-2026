---
layout: assignment
title: "Individual Project 3"
permalink: /assignments/ip3
parent: Assignments
nav_order: 2
due_date: "Wednesday February 18, 2026 11:00am (EST)"
submission_notes: Submit through Github Classroom (Commit your work in main branch) and link on Gradescope
---

In this third individual deliverable, you will be given some more freedom in how your features are developed and will

The objectives of this assignment are to:

- Investigate and understand a large, existing codebase
- Make changes that span the frontend and backend of a full-stack application
- Get experience with implementing features using the socket.io implementation of websocket
- (Optional) allow you a chance to get experience with working with large-language-model based tools for coding

In keeping with the last objective, **you may use code generation (i.e. "AI") tools in this assignment, with two caveats:**

- You are responsible for every line of code in your final submission. If we ask you questions about your submitted code and you are unable to explain why decisions were made because you accepted the LLM's suggestions without understanding them, **you will receive a failing grade on this assignment**.
- You need to have a file in the root of your repository, `LLM.md`, that documents what tools you used, how you used them, and whether you think the experience saved you time overall. (How much time did you spend on the assignment? How much time did the use of tools cost, or save? Did you go down any blind alleys or wild-goose chases due to your use of the tools you used?)

## Changelog

- NA

## 1. Getting Started

Start by accepting our [GitHub Classroom Invitation] XXX TODO. It will create a Github repository for you which will include the starter code for this assignment. Run `npm install` in the root directory to fetch all dependencies for the `client`, `server`, and `shared` folders.

## 2. Recommendations When Working on the Project

1. Have the frontend and backend running, and have the project open in your browser, while you are working. It's very useful to have the website update as you make changes.
2. Frequently add and commit changes with git. This saves your changes and makes it easy to go back to a state where most tasks were complete, and is especially important when using tools that may be changing your code in unexpected ways.
3. Do not wait until the last minute to run `npm run lint` and `npm run check` to check for linter and typescript errors!
4. Follow the [debugging policy]({{ site.baseurl }}{% link debugging.md %}) to help in the debugging process.

## 3. Project Submission

You will submit your code by pushing the final version into your repository (add/commit/push). **All commits must be visible on the main branch on GitHub classroom to receive credit.** Be sure to check if the correct version is submitted before the deadline.

On Gradescope, you will submit a plain `.txt` file containing a link to your project's GitHub repo (e.g. `https://github.com/neu-cs4530/ip3-robsimmons`).

Grades will be assigned on Gradescope and synced to the Canvas Gradebook.

### TypeScript ESLint, Vitest, and Configuration Files

The GitHub project contains a number of configuration files you **may not modify**. The files `package.json`, `.prettierrc`, `tsconfig.json`, `vitest.config.mjs`, and `vite.config.mjs` are examples of configuration files, as is everything in the `.github` directory. If you change any of these files, take care to change them back; the list of changes in the feedback PR should not show any changes to these files. You also may not include `eslint-disable` commands to disable ESLint's checks in your final submission.

The code you submit must pass GitHub's automatic checks, which mostly just amount to the TypeScript typechecker, the ESLint linter, and the tests. You can run these yourself like this:

```
ip1-me $> npm run prettier --workspaces
ip1-me $> npm run check --workspaces
ip1-me $> npm run lint --workspaces
ip1-me $> npm run test --workspaces
```

When you push your code to GitHub, you can see the status icon for your most recent submission. It's initially a yellow circle, like this:

![image]({{site.baseurl}}{% link /Assignments/ip1/github-ci.png %})

After the tests run, this will turn into a red ❌ or a green ✅. Clicking on the icon will let you see details of the tests we ran.

The Actions tab on GitHub has the results of previous runs.

![image]({{site.baseurl}}{% link /Assignments/ip1/ActionsTab.png %})

**Up to 25% of your total grade on the assignment may be deducted for CI failures (5% for Prettier failures, 10% for TypeScript failures, and 10% for ESLint failures). In severe cases we may decline to grade your assignment entirely. Give yourself sufficient time to find and fix any errors.** ESLint _warnings_ do not cause CI to fail and will not automatically lead to a deduction, but it is bad practice to have lots of console statements in your code, and this can lead to a point deduction if it makes it hard for a TA to understand your code.

## 4. Implementation Tasks

The implementation tasks are framed in terms of user stories and conditions of satisfaction. These user stories are quite a bit more narrow, specific, and focused than the user stories we expect for the group project.

### Task 1: A New Game Has Been Created!

User story: _As someone who leaves Game Nite open in the background while I'm at work, I want to be able to see when new games are created, so that I can be one of the first to join or watch._

For this task, you will extend the websocket interface of Game Nite in order to alert users to the presence of new games. 

![image]({{site.baseurl}}{% link /Assignments/ip3/threenew.png %} =300x)

These essential conditions of satisfaction form the minimum viable product:

 - 1.1: When a user creates a new game, any users watching the Game Nite home page see the new game inserted to the top of the list of games. 
 - 1.2: A new game appearing on the home page does not cause currently-visible games to be removed. This means that new games may cause more than four games to be visible on the home page. 
 - 1.3: When a user creates a new game, any users watching the "All games" page at `/games` see the new game inserted.
 - 1.4: On both the home page and new games page, new games have some attention-getting designation as new games. ("New!")
 
For full credit, you should also implement these desirable conditions of satisfaction:

 - 1.5: Every browser session has a notional concept of "unviewed new games." If this count is non-zero, the "Games" sidebar item includes the count, for example by reading "Games (2 new!)"
 - 1.6: When a user starts a new game, their own count of unviewed new games does not increase.
 - 1.7: When the user is on the home page or the "All games" page, the count always stays zero.
 - 1.8: Navigating to the home page or the "All games" page resets the count.
 - 1.9: When a user is *not* on the home page or "All games" page and another user starts a game, the count of unviewed new games increases.

We will examine the style and quality of your code. For full credit, make sure:

 - Any modified or introduced functions have appropriately updated JSDoc comments
 - All code uses appropriate [code style]({{ site.baseurl }}{% link style.md %}).
 - Excessive repetition in React is avoided by creating new hooks or new components.

(This is not intended to be an exhaustive list.)

### Task 2: Reviewing Game Moves

User story: _As someone who likes reviewing game strategy, I want to be look back on the individual moves made in an ongoing or completed Game Nite game, so that I can improve my own gameplay and learn how other peoples' strategy differs._

For this task, you will change your backend in order to record a history of the moves played in a game, and display the record of moves in a human-readable way in the frontend.

![image]({{site.baseurl}}{% link /Assignments/ip3/movelog.png %} =300x)

These essential conditions of satisfaction form the minimum viable product:

 - 2.1: When a move is made, all users watching the chat see the same description of that move in the chat log.
 - 2.2: Past descriptions of game moves appear interleaved in the chat window with chat messages and "(User) entered chat" messages.
 - 2.3: Game moves are centered and styled in a way that emphasizes them more emphasis than "(User) entered chat"  messages.
 - 2.4: Descriptions of Nim moves have the form "(User) took {one token, two tokens, three tokens}, leaving N" or "(User) took {one token, two tokens, three tokens} and lost the game", as appropriate, with (User) either being "you" or the display name of the user.

For full credit, you should also implement these desirable conditions of satisfaction:

 - 2.5: Number Guesser also reports moves that make sense in the context of that game.
 - 2.6: The description of past moves gets stored in memory: it's possible to navigate away from a game page and then navigate back, and the log of all game moves will still be present.

We will examine the style and quality of your code. For full credit, make sure:

 - Functions are added where appropriate and given good names and informative JSDoc comments.
 - All code uses appropriate [code style]({{ site.baseurl }}{% link style.md %}).
 - The controller-service-repository pattern is respected: business logic is generally placed in the service layer, and the repository and controller don't know about each other.
 - The record types in `server/src/models.ts` give an indication of how the new data we are collected is being stored. 
 - The production of move descriptions is treated as a part of a game's logic, and is added to the existing interface of games in a reasonable way.

(This is not intended to be an exhaustive list.)

### Task 3: Testing

The starter code for this assignment includes Playwright end-to-end tests of login behavior and games. Pick a couple of your implemented conditions of satisfaction and create a new test file that implements automated end-to-end tests of that new behavior. Your code should be readable and make it clear what testable conditions you are describing and which conditions of satisfaction these testable conditions relate to.

Make sure that this file gets added to your Git repository and pushed to GitHub!

## 5. Grading Summary

The assignment as a whole is worth 100 points.

- Task 1: 45 points
  - MVP implementation: 20 points
  - Desirable tasks: 10 points
  - Code quality: 15 points
- Task 2: 45 points
  - MVP implementation: 20 points
  - Desirable tasks: 10 points
  - Code quality: 15 points
- Task 3: 10 points
