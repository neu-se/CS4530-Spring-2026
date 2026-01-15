---
layout: assignment
title: "Individual Project 2"
permalink: /assignments/ip2
parent: Assignments
nav_order: 2
due_date: "Wednesday February 4, 2026 11:00am (EST)"
submission_notes: Submit through Github Classroom (Commit your work in main branch) and link on Gradescope
---

Welcome back to the Game Nite team! In this second deliverable, you will be implementing new and exciting features to enhance the frontend interface and bring the web application to life. This assignment builds on the foundation you laid in the first project and will deepen your skills in frontend development with TypeScript and React.

The objectives of this assignment are to:

- Investigate and understand a large, existing codebase
- Implement interactive web applications with the React library

## Changelog

- NA

## 1. Getting Started

Start by accepting our [GitHub Classroom Invitation](https://classroom.github.com/a/2qFol7Uh). It will create a Github repository for you which will include the starter code for this assignment. Run `npm install` in the root directory to fetch all dependencies for the `client`, `server`, and `shared` folders.

### 1.1 Optional but Highly Recommended: MongoDB

It can be quite a bit easier to work on the application if restarting the server doesn't reset the entire application to an initial state.

Your starter code uses a proper repository layer, which connects to MongoDB through an adapter library called [Keyv] TODO TODO XXX TODO TUTORIAL. You can install MongoDB on your local machine.

1. Follow the [instructions in the official MongoDB documentation](https://www.mongodb.com/docs/manual/administration/install-community/) to install the free community edition.
2. Choose 'Install on Linux', 'Install on macOS', or 'Install on Windows', depending on your system. (the following steps are for Windows)
3. Scroll down to the section labeled 'Install MongoDB Community Edition.' and click on [MongoDB Download Center](https://www.mongodb.com/try/download/community?tck=docs_server).
4. For Windows, in the Package dropdown, select `msi`. Then download and run the installer.
5. On Windows, select the _“Install MongoDB as a Service”_ checkbox and install. This will start MongoDB as a background service.
6. Install "MongoDB Compass" if prompted.
7. Verify if the MongoDB server is running using the Windows Services app.

Mongo offers several methods of interacting with your Mongo databases.

- MongoDB Compass is an interactive application for creating, modifying, and querying MongoDB connections. It should be started as part of the installation process, showing a connection to `mongodb://localhost:27017/`.

  For Windows, install MongoDB Compass using the instructions above.

  For Mac:

  - Download the dmg file from [here](https://www.mongodb.com/try/download/compass). Once the application starts:
    1.  Click on "Add new connection" in the left sidebar.
    2.  Make sure the URI field contains `mongodb://localhost:27017`
    3.  Click on "Connect" - MongoDB will need to be running as a macOS service

- Mongo shell (_mongosh_) provides a command-line interface that can be used to interact with databases in MongoDB.

  For Windows:

  - Download it [here](https://www.mongodb.com/try/download/shell) using the msi package. You can also use _mongosh_ to see if the MongoDB server is running. Try the MongoDB Community Edition and the command `show dbs`; you should see a list of existing databases in your local instance.

  For Mac:

  - Mongo shell is automatically installed with MongoDB through the Mac installation instructions. To use it, make sure MongoDB is running as a macOS service, then type `mongosh` into the terminal.

### 1.2 Setting Up the Server To Use MongoDB

Create a file called `server/.env` — the dot before the "env" is important! Include the following text:

```
MONGODB_STR=mongodb://127.0.0.1:27017
```

This tells your server how to connect to the local MongoDB instance that you got running in the previous step. Now, you can start the application as before: in one terminal, run:

```
ip2-me $> npm run dev -w=server
```

Leaving that running, open another terminal and run:

```
ip2-me $> npm run dev -w=client
```

The application should work as before, but any changes you make in the application should survive restarting the server.

## 2. Recommendations When Working on the Project

1. Have the frontend and backend running, and have the project open in your browser, while you are working. It's very useful to have the website update as you make changes.
2. Use Git effectively: the first three tasks are cumulative, as are the last three tasks, and if you run into trouble with Task 5, you will want to be able to backtrack to a working implementation of Task 4.
3. Do not wait until the last minute to run `npm run lint` and `npm run build` to check for linter and typescript errors!
4. Follow the [debugging policy]({{ site.baseurl }}{% link debugging.md %}) to help in the debugging process.
5. Frequently add and commit changes with git. This saves your changes and makes it easy to go back to a state where most tasks were complete.
6. Task 6 is more challenging than the other tasks, but is only worth 20% of credit. Don't wait until the last minute to attempt this task if you intend to complete all parts of the assignment.

## 3. Project Submission

You will submit your code by pushing the final version into your repository (add/commit/push).**All commits must be visible on the main branch on GitHub classroom to receive credit.** Be sure to check if the correct version is submitted before the deadline.

On Gradescope, you will submit a plain `.txt` file containing two things:

1.  The link to your project's GitHub repo (e.g. `https://github.com/neu-cs4530/ip2-robsimmons`)
2.  The written responses and cURL commands requested in Task 3.

We will grade your code on GitHub by using the "Feedback" PR that is automatically created when the assignment is. The Feedback PR can be found under the "Pull requests" menu, like this:

![image]({{site.baseurl}}{% link /Assignments/ip1/github-pr.png %})

If you don't see your Feedback PR for the assignment, let us know on Piazza (be sure to include your GitHub username in your post).

Grades will be assigned on Gradescope and synced to the Canvas Gradebook.

### TypeScript ESLint, Vitest, and Configuration Files

The GitHub project contains a number of configuration files you **may not modify**: `package.json`, `package-lock.json`, `.prettierrc`, `tsconfig.json`, `vitest.config.mjs`, and `vite.config.mjs` are configuration files, as is everything in the `.github` directory. If you change any of these files, take care to change them back; the list of changes in the feedback PR should not show any changes to these files. You also may not include `eslint-disable` commands to disable ESLint's checks in your final submission.

The code you submit must pass GitHub's automatic checks, which mostly just amount to the TypeScript typechecker, the ESLint linter, and the tests. You can run these yourself like this:

```
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

### Task 1: Navigating to Other Profiles

Currently, going to the "Profile" link at the top of your page takes you to the path `/profile/<yourusername>`. Change `client/src/components/MessageList.tsx` so that clicking on the users' display name in chat takes you to the path `/profile/<theirusername>`. For example, if you are logged in as `user0` and you see a chat message from "Yāo" (the display name for `user1`), that should be a `<NavLink>` that takes you to `/profile/user1`.

This task is worth 10 points, based on checking that chat navigation works as expected.

### Task 2: Viewing Other Profiles

Change `client/src/pages/Profile.tsx` so that, if you are logged in as `user0` and navigate to `/profile/user1`, you see a page that allows you to see _but not edit_ that user’s username, display name, and when their account was created.

You may want to split this file into two or three new files, since the route to profile pages is now being used for two different purposes: viewing your own profile, and editing other profiles.

This task is worth 25 points:

- 10 points will be based on functionality.
- 15 points will be based on appropriately refactoring your code into multiple files with appropriate [code style]({{ site.baseurl }}{% link style.md %}).

### Task 3: More Profile Navigation

The code you changed in Task 1 was only one place where user display names were referenced. Here are some others:

- The "(DisplayName) entered chat/left chat" messages in chat
- The "Player #2 is (DisplayName)" messages in the game panel
- "Posted by (DisplayName)" in forum messages
- "Reply by (DisplayName)" in forum comments
- "(Display name) created 1 day ago" on the home page and the game list and forum list pages

For this task, you'll make three changes to all display name locations:

- Consistently refer to the current logged-in user by the second-person pronoun "you," instead of by their display name. (The exception is the "signed in as (DisplayName)" message in the header — leave that alone.)
- Create a consistent visual style for distinguishing references to "you," the current logged-in user, and references to other users.
- Consistently link other users' usernames to their profile. References to the current user ("you") should not link to the current user's profile.

This task is worth 15 points: one point for each of the three changes in each of the five places where display names occur. You should make this task easier on yourself by thinking about how to organizing your code in a way that minimizes duplication, and unnecessary duplication may lead to a deduction of up to 5 points.

### Task 4: Mine Finder

The backend has been implemented for Mine Finder, a game with a strong but legally-permissible resemblance to Microsoft's [Minesweeper](https://apps.microsoft.com/detail/9wzdncrfhwcn?hl=en-US&gl=US) game.

![image]({{site.baseurl}}{% link /Assignments/ip2/beforeafter.png %})

In Mine Finder, your game starts with a 6x6 or 7x5 grid containing five randomly-placed mines. Clicking on a grid position sweeps it, revealing how many of the eight adjacent grid positions contain mines — or exploding and ending the game if there is a mine in that grid position! When a grid position is revealed to have zero mines, all eight adjacent grid positions are automatically swept.

The backend logic for Mine Finder is implemented, and you can read the description of types in `shared/src/games/minefinder.types.ts`, the implementation in `server/src/games/minefinder.ts`, and the tests in `server/tests/games/minefinder.spec.ts`. The frontend implementation in `client/src/games/MineFinderGame.tsx` is the only part that is completely missing, and you will implement the game's frontend in React for this task.

The task is worth 22 points, two points for meeting each of the following conditions of satisfaction:

1.  Unswept grid positions should contain a question mark `❓`, unless the game has been won (`view.state === 'won'`), in which case they should contain a `🎉` emoji. (Mines are not revealed on loss.)
2.  Swept grid positions with no neighboring mines should appear empty.
3.  Swept grid positions with neighboring mines should contain the number of neighboring mines (unless the grid position itself contains a mine).
4.  Swept grid positions revealing a mine should contain a `💥` emoji.
5.  Swept grid positions should have the `cursor: default` CSS property set.
6.  Non-players should always see all grid positions with the `cursor: default` CSS property set, and clicking anywhere on the grid should never send a message or make a move.
7.  If the game is not over (`view.state === 'playing'`), the player of the game should see **unswept** grid positions with the `cursor: pointer` CSS property set.
8.  If the game is not over, the player of the game should be able to "sweep" a grid position by clicking on it: clicking on the upper-right grid position of a 7x5 grid should submit the game move `[6,0]`.
9.  If the game is over (`view.state !== 'playing'`), the player of the game should see all grid positions with the `cursor: default` CSS property set, and clicking anywhere on the grid should never send a message or make a move.
10. If the game is over, the player of the game should see the message "You won" or "You lost", as appropriate, below the game grid.
11. If the game is over, non-players should see "(DisplayName) won" or "(DisplayName) lost", as appropriate, below the game grid, where "(DisplayName)" is replaced by the player's display name.

Your implementation does not need to look like the example image above. It must be possible for a TA to effectively test a conditions of satisfaction in order to award points. The player name in the 10th and 11th conditions of satisfaction is not required to be as in Task 3.

### Task 5: Marking Mines

For this task, you will **not** change the Mine Finder logic on the server or anything else outside of `MineFinderGame.tsx`; the goal is to use React state to implement a feature.

It's very helpful to be able to flag a grid position as a known mine while playing Mine Finder. Without giving the backend any support for flagging grid positions, you can use React state to record and add flags. Storing flags in React state attached to the `MineFinder` React component has some drawbacks: only the player can see flags, and if a player navigates away and returns, all their flags will be gone. That is fine for the purposes of this task.

When a player _right_-clicks on a grid position with a `❓` in it, that question mark should be replaced with a flag `⛳`. Left-clicking a flagged grid position should have no effect — a flag should keep you from accidentally setting off a mine. Right-clicking a grid position with a flag should unflag the grid position, returning it to a `❓` and making it clickable again.

You can capture right clicks by adding an [`onContextMenu`](https://react.dev/reference/react-dom/components/common#common-props) property alongside the `onClick` handler you added in the last part.

This task is worth 8 points, 4 points from testing the implementation and 4 points from verifying the correct use of React state.

### Task 6: Mine Difficulty

GameNite's user researchers come to you with two different user stories they discovered when testing the new game:

> As a novice mine finder, I want access to easier and more forgiving puzzles, so that I can develop my skills without getting discouraged.

> As an expert mine finder, I want access to more challenging puzzles, so that I can show off my advanced logical skills.

In this task, you'll meet the needs of these users by modifying the Mine Finder game to allow for an initial difficulty selection. This task will require changes to all the parts of your project: the server, the client, and the shared code.

When a new single-player game of Mine Finder begins, the user should be shown a [drop down menu](https://react.dev/reference/react-dom/components/select) with three choices, "Easy", "Standard", and "Hard", and the "Standard" button should be selected by default. There should be a submit button that sends a move that is just the string "easy", "standard", or "hard". Sending that move should trigger the backend's Mine Finder logic to generate a board and start a game.

You can decide what "easy" and "difficult" actually mean, within the following constraints:

- An "Easy" difficulty game must have no more than 36 positions arranged in a rectangular grid, and at most 5 mines. Exposing _one_ mine in an "easy" game shouldn't be an automatic loss: players only lose when two mines are exposed.
- The "Standard" difficulty game should be exactly the previous version of the game.
- A "Hard" difficulty game must have at least than 40 positions arranged in a rectangular grid, and more than 1/6 of the positions should be mines.

**Hint:** you will likely want to transform both the `MineFinderState` and `MineFinderView` types so that the game can exist in different states: not started, and started. In the starter code, `MineFinderState` looks like this:

```typescript
export interface MineFinderState {
  width: number;
  height: number;
  board: boolean[][]; // each array is one row
  clicked: boolean[][]; // each array is one row
}
```

However, in the modified game, it will no longer be possible for the `start()` function to initialize a board: `start()` gets called before difficulty is selected, and `width` and `height` are dependent on the difficulty level.

Therefore, the new state should be some sort of a [discriminated union](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions), perhaps something like this:

```typescript
export type MineFinderState =
  | { state: "waiting" }
  | {
      state: "started";
      width: number;
      height: number;
      board: boolean[][]; // each array is one row
      clicked: boolean[][]; // each array is one row
    };
```

You are not required to use precisely this type; part of the task is figuring out what your `MineFinderState` type needs to be.

This task is worth 20 points:

- 4 points for implementing difficulty selection
- 4 points for implementing hard mode
- 4 points for implementing easy mode
- 4 points for fixing the tests and having >=95% line and branch coverage for `shared/src/games/minefinder.ts`
- 4 points for [code style]({{ site.baseurl }}{% link style.md %}) and appropriate documentation of helper functions.

## 5. Grading Summary

The assignment as a whole is worth 100 points.

- Task 1: 10 points
- Task 2: 25 points
- Task 3: 15 points
- Task 4: 22 points
- Task 5: 8 points
- Task 6: 20 points
