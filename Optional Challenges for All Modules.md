# Follow this link https://github.com/Asabeneh/30-Days-Of-React/blob/master/06_Day_Map_List_Keys/06_map_list_keys.md

# Module 04 - Optional Challenge 1 - Rendering Array of Objects
**Solution 1**
```
import './App.css';
import React from 'react'

const countries = [
  { name: 'Singapore', city: 'Singapore',population:'6,014,723'},
  { name: 'Thailand', city: 'Bangkok',population:'71,801,279' },
  { name: 'Malaysia', city: 'Kuala Lumpur',population:'34,308,525' },
  { name: 'Indonesia', city: 'Jakarta',population:'227,534,122' },
  { name: 'Philippines', city: 'Manila',population:'117,337,368' },
]

const Country = ({ country: { name, city, population } }) => {
  return (
    <div>
      <h3>{name} - {population}</h3>
      <small>{city}</small>
    </div>
  )
}

const Countries = ({ countries }) => {
  const countryList = countries.map((country) => <Country country={country} />)
  return <div>{countryList}</div>
}

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <div className='container'>
          <div>
            <h1>Countries List</h1>
              <Countries countries={countries} />
          </div>
        </div>
      </header>
    </div>
  );
}

export default App;

```
**Solution 2**
```
import './App.css';
import React from 'react'

const countries = [
  { name: 'Singapore', city: 'Singapore',population:'6,014,723'},
  { name: 'Thailand', city: 'Bangkok',population:'71,801,279' },
  { name: 'Malaysia', city: 'Kuala Lumpur',population:'34,308,525' },
  { name: 'Indonesia', city: 'Jakarta',population:'227,534,122' },
  { name: 'Philippines', city: 'Manila',population:'117,337,368' },
]

const countryList = countries.map((country) => 
      <div>
        <h3>{country.name} - {country.population}</h3>
        <small>{country.city}</small>
      </div> );


function App() {
  return (
    <div className="App">
      <header className="App-header">
        <div className='container'>
          <div>
            <h1>Countries List</h1>
                {countryList}
          </div>
        </div>
      </header>
    </div>
  );
}

export default App;
```
