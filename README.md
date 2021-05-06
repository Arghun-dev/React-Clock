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
