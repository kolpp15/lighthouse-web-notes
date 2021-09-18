# W7D4 Notes

## Two rules for hooks
1. Have to be called in the same order every time a component renders
2. Must be called inside a react functional component or react functions
3. a hook must be named starting with `use`

## Pure Function
- it has no side effects: this means whatever happens inside a function does not go out
- always returns the same output given the same inputs
- useEffect does not have a side effect
- You can have multiple useEffect in a single Component

```js
import {useEffect, useState} from 'react'

const App = () => {
  const [counter, setCounter] = useState(0);
  const [searchTerm, setSearchTerm] = useState('');



  useEffect(() => {
    document.title = 'welcome to our site';
    console.log('changed the document title');
  }, [counter, searchTerm]);
  // Second parameter: If counter and searchTerm changes, anything before gets called

  useEffect(() => {
    setTimeout(() => {
      console.log(`the current count is ${counter}`)
    }, 3000)

    //you can return a function sinde a function 
    return () => {
      clearInterval(interval);
      console.log(`interval cleared`)
    }
  })

  return (
    <div className="App">
      <h2>useEffect Hook</h2>
      <h2>Count: {counter}</h2>
      <button onClick={() => setCounter(counter + 1)}>Click me</button>
    </div>

    <div>
      <h2>Search term: {searchTerm}</h2>
      <input
        value={searchTerm}
        onChange={(event) => setSearchTerm(event.target.value)}
      />
    </div>

  );
}
```

## React Order of Operations
1. React Renders UI                      - checks all the codes
2. Browser Displays the UI               - display html to the browser
3. Cleanup for previous effects (if any) - then, look for cleanup if present
4. Run effects for current render 

## AXIOS (same as ajax)

```js
import {useEffect, useState} from 'react';
import axios from 'axios';

const Appointments = () => {
  const [appointments, setAppointments] = useState({});
  const [selectedAppt, setSelectedAppt] = useState(null);
  const [apptId, setApptId] = useState('');

  useEffect(() => {
    // GET /api/appointments
    axios.get('http://localhost:8001/api/appointments')
      .then((response) => {
        console.log(response.data);
        setAppointments(response.data);
      })
  }, []);  //need to get out from the invinite loop. If we want to loop only once, then add an empty array since it doesn't depend on anything

  useEffect(() => {
    console.log('apparently the id has changed');
    const targetAppt = appointments[apptId];
    console.log(targetAppt);
    setSelectedAppt(targetAppt);
  }, [apptId])

  return (
    <div>
      <h2>All the Appointments</h2>
      <h2>Total Appointments: {Object.keys(appointments).length}</h2>

      <div>
        <label>Enter and Appt Id</label>
        <input
          value={apptId}
          onChange={(event) => setApptId(event.target.value)}
        />
      </div>

      // ONLY if the left side is TRUTHY, right side will render (IF THERE"S APPOINTMENT, SHOW INFO)
      { seletedAppt && (<div>
          <h2>Selected Appt Information</h2>
          <h2>Interview#{selectedAppt.id} at {selectedAppt.time}</h2>

          // There may and may not have an interview so again follow the && statement
          {selectedAppt.interview && (
            <Fragment>
              <h2>Student: {selectAppt.interview.student}</h2>
              <h2>Interviewer: {selectAppt.interview.interviewer}</h2>
            </Fragment>
          )}
      )}
      </div>
      
    </div>
  );
};

export default Appointments;
```
- above && in React is the same as IF statement in JS
- ex) if left side is truthy, execute right side


## cleanout 
![cleanout]()