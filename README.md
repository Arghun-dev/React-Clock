# React-Clock

```js
import React, { useState, useEffect } from "react";
import "./styles.css";

export default function App() {
  const [time, setTime] = useState(new Date().toLocaleTimeString());

  const tick = () => {
    setTime(new Date().toLocaleTimeString());
  };

  useEffect(() => {
    const timer = setInterval(() => {
      tick();
    }, [1000]);

    return () => clearInterval(timer);
  }, [tick]);

  return (
    <div className="App">
      <h1>{time}</h1>
    </div>
  );
}
```

Experienced React developers probably already noticed that we have in the dependency array of the useEffect hook the function incrementCount. Actually, it might not have been necessary to include it here, but it is considered a good practice to always fill the dependency array with all variables (and functions) that are used in the useEffect hook.

We will not dive into why this is happening right now, I’ll just say it has to do with the fact that functions are reference types, and if we don’t move it inside the useEffect hook or wrap it with the useCallback hook, we can cause an infinite loop. Anyhow, for us what’s important right now is that that suggestion from the IDE — either move incrementCount inside useEffect or wrap it with the useCallback hook. Let’s choose the second option.

```js
import React, { useState, useEffect, useCallback } from "react";
import "./styles.css";

export default function App() {
  const [time, setTime] = useState(new Date().toLocaleTimeString());

  const tick = useCallback(() => {
    setTime(new Date().toLocaleTimeString());
  });

  useEffect(() => {
    const timer = setInterval(() => {
      tick();
    }, [1000]);

    return () => clearInterval(timer);
  }, [tick]);

  return (
    <div className="App">
      <h1>{time}</h1>
    </div>
  );
}
```
