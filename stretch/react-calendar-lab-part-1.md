<img src="https://images.unsplash.com/photo-1435527173128-983b87201f4d?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxzZWFyY2h8Mnx8Y2FsZW5kYXJ8ZW58MHx8MHw%3D&auto=format&fit=crop&w=600&q=80">

# React Calendar - Part 1

## Intro

You goal for this lab will be to use the skills you have learned in React to recreate the React Calendar seen below:

## Setup

You will need to create a React-based [CodeSandbox](https://codesandbox.io/) to complete the lab

## Wireframes

We're going to go with a clean, minimalistic user interface.

> Note: Feel free to go with your own layout, colors, etc.

<img src="https://i.imgur.com/kG91EoR.png">

Follow the instructions below to complete your own React Calendar!

## Instructions

1. Copy the following code to your App.js to use as a starting point. 

  **DO NOT CHANGE THE `days` OR `dates` ARRAYS!**

  ```jsx
  import "./styles.css";

  export default function App() {

    const days = [
      {
        name: "Sunday"
      },
      {
        name: "Monday"
      },
      {
        name: "Tuesday"
      },
      {
        name: "Wednesday"
      },
      {
        name: "Thursday"
      },
      {
        name: "Friday"
      },
      {
        name: "Saturday"
      },
    ]

    // The following creates an array of numbers from [1..28]
    const dates = Array.from({length: 28}, (x, i) => i + 1)

    return (
      <div className="App">
        <h1>React Calendar</h1>
      </div>
    );
  }

  ```

2. Using the provided `dates` and `days` arrays, create a `<Calendar />` component that looks like the wireframe above.

  - You must pass the arrays down using props, and use that data to display the name & date for each day.
  - Your calendar should have 4 even rows (weeks) with 7 cells (days) in each row.
  - Inside each cell, you should display the name of the day on top & the date below.
  
  > Note: Don't forget to keep checking the wireframe to make sure you are on the right track!


## Code away and have fun!

### This lab is not is a deliverable.
