# W7D5 Notes

## React Hooks
- React hooks must start with the prefix "use"
- Multiple instances of the same custom hook do not share state

## Example
```js
//App.js FILE
import Counter from 'Counter';
import useCounter from 'hooks/useCounter';
import KanyeQuote from 'KanyeQuote';
import OfficeQuote from 'OfficeQuote';


export default function App() {
  const [count, increment, decrement, clear] = useCounter(0);

  return (
    <div className="App">
      <h1>Hello Custom Hooks</h1>
      <Counter initial="0" />

      <button onClick={increment}>Show/Hide</button>

      { count % 2 === 0 && 
      <ul>
        <KanyeQuote />
        <OfficeQuote />
      </ul>
      }

    </div>
  )
}
```

```js
// useCounter.js

const useCounter = function (initial) {
  const [count, setCount] = useState(0);

  const increment = function() {
    setCount(count + 1);
  };
  const decrement = function() {
    setCount(count - 1);
  };
  const clear = function() {
    setCount(0);
  };
  return [count, increment, decement, clear];
}
export default useCounter;
```

```js
//Counter.js
import useCounter from "hooks/useCounter"

const Counter = function(props) {

  const [count, increment, decrement, clear] = useCounter(props.initial || 0);

return (
  <div>
    {count}
    <button onClick={increment}>+</button>
    <button onClick={decrement}>-</button>
    <button onClick={clear}>0</button>
  </div>

)
}
export default Counter;
```

```js
// axios.js
import axios from 'axios';

const useAxios = function(url) {
  const [body, setBody] = useState("");
  const [error, setError] = useState(null);
  const [pending, setPending] = useState(true);

  useEffect(() => {
    axios.get(url)
      .then(res => {
        setBody(res.data);
        setError(null);
      });
      .catch(error => {
        setBody("");
        setError(err.message);
      })
      .finally(() => {
        setPending(false);
      })

  }, [url]);
  return {body, error, pending};
}
export default useAxios;
```

```js
// KanyeQuote.js

const {default: useAxios} = require("hooks/useAxios");

const KanyeQuote = function () {
  const {body, error, pending} = useAxios("https://api.kanye.rest");

  return (
    <li>
      {body && body.quote}
      {error && error}
      {pending && "Please wait..."}
    </li>    
  );
};
export default KanyeQuote;
```

```js
// OfficeQuote.js

const {default: useAxios} = require("hooks/useAxios");

const OfficeQuote = function () {
  const {body, error, pending} = useAxios("https://www.officeapi.dev/api/quotes/random");

  return (
    <li>
      {body && body.data.content}
      {error && error}
      {pending && "Please wait..."}
    </li>    
  );
};
export default OfficeQuote;
```

## Scheduler App custom hook
```js
const useVisualMode = function(initial) {
  const [mode, setMode] = useState(initial);
  const [history, setHistory] = useState([initial]);

  const transition = function (newMode) {
    
    // THIS IS NOT A GOOD PRACTICE
    // const newHistory = [...history];
    // newHistory.push(newMode);
    // setHistory(newHistory);

    setHistory([...history, newMode]);
  };

  const back = function () {

    const newHistory = [...history];
    newHistory.pop();
    
  };

  let mode = history[history.length - 1];

  mode = history.slice(-1)[0];

  return { mode, transition, back };
};
export default useVisualMode;
```

## Interview Question
- what does the spread operators do? 
  - Answer: if it's an object, remove curly brace. if it's an array, square brackets.
  - takes out the closings
