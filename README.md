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
  }, []);

  return (
    <div className="App">
      <h1>{time}</h1>
    </div>
  );
}
```
