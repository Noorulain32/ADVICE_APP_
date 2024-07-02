# ADVICE_APP_
This is an advice app. I have made it by using react framework and advice API.

# Advice Corner

Welcome to the Advice Corner app! This is a simple React application that fetches random advice from an API and displays it on the screen. Users can get new advice by clicking a button.

## Features

- Fetches and displays random advice.
- Keeps track of how many times the advice has been fetched.
- Simple and easy-to-understand UI.

## Installation

To get started with this project, follow these steps:

1. **Clone the repository:**

    ```bash
    git clone https://github.com/yourusername/advice-corner.git
    ```

2. **Navigate to the project directory:**

    ```bash
    cd advice-corner
    ```

3. **Install dependencies:**

    ```bash
    npm install
    ```

4. **Start the development server:**

    ```bash
    npm start
    ```

    This will start the app on `http://localhost:3000`.

## Usage

Once the app is running, you can see a piece of advice displayed on the screen. Click the "Get Advice" button to fetch a new piece of advice. The count of how many times you've fetched advice will be displayed below the advice.

## Code Overview

### `App` Component

The `App` component is the main component of the application. It uses the `useState` hook to manage the state for the advice text and the count of how many times advice has been fetched. The `useEffect` hook is used to fetch advice when the component is first rendered.

### `getAdvice` Function

This asynchronous function fetches advice from the `adviceslip.com` API and updates the state with the new advice and incremented count.

### `Message` Component

The `Message` component is a simple component that displays the count of how many times advice has been fetched.

```javascript
import { useEffect, useState } from "react";

export default function App() {
  const [advice, setAdvice] = useState("");
  const [count, setCount] = useState(0);

  async function getAdvice() {
    const res = await fetch("https://api.adviceslip.com/advice");
    const data = await res.json();
    setAdvice(data.slip.advice);
    setCount((c) => c + 1);
  }

  useEffect(function () {
    getAdvice();
  }, []);

  return (
    <div>
      <p>this is advice corner</p>
      <h1>{advice}</h1>
      <button onClick={getAdvice}>Get Advice</button>
      <p>
        <Message count={count} />
      </p>
    </div>
  );
}

function Message(props) {
  return (
    <p>
      you need <strong>{props.count}</strong>
    </p>
  );
}

