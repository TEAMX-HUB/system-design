# FORM VALIDATION (CLIENT-SIDE FORM VALIDATION)

Client-side validation is an initial check and an important feature of good user experience; by catching invalid data on the client-side, the user can fix it straight away. If it gets to the server and is then rejected, a noticeable delay is caused by a round trip to the server and then back to the client-side to tell the user to fix their data.
When you enter data, the browser and/or the web server will check to see that the data is in the correct format and within the constraints set by the application. Validation done in the browser is called **client-side validation**, while validation done on the server is called **server-side validation.** Eg:

1. "This field is required" (You can't leave this field blank).
2. "Please enter your phone number in the format xxx-xxxx" (A specific data format is required for it to be considered valid).
3. "Please enter a valid email address" (the data you entered is not in the right format).
4. "Your password needs to be between 8 and 30 characters long and contain one uppercase letter, one symbol, and a number." (A very specific data format is required for your data).

If the information is correctly formatted, the application allows the data to be submitted to the server and (usually) saved in a database; if the information isn't correctly formatted, it gives the user an error message explaining what needs to be corrected, and lets them try again.

CREATING A FORM

```js
import logo from './logo.svg'
import './App.css'
import { useState } from 'react'

function App() {
  const [firstName, setFirstName] = useState('') // useState to store First Name
  const [lastName, setLastName] = useState('') // useState to store Last Name
  const [mobile, setMobile] = useState('') // useState to store Mobile Number
  const [age, setAge] = useState('') // useState to store Age
  const [email, setEmail] = useState('') // useState to store Email address of the user
  const [password, setPassword] = useState('') // useState to store Password

  return (
    <div className="main">
      <form>
        {/_ Input Field to insert First Name _/}
        <input
          placeholder="First Name"
          onChange={(e) => setFirstName(e.target.value)}
        />
        {/_ Input Field to insert Last Name _/}
<input
          placeholder="Mobile Number"
          onChange={(e) => setMobile(e.target.value)}
        />
        {/_ Input Field to insert Age _/}
        <input placeholder="Age" onChange={(e) => setAge(e.target.value)} />
        {/_ Input Field to insert Email Address of the user _/}
        <input placeholder="Email" onChange={(e) => setEmail(e.target.value)} />
        {/_ Input Field to insert Password _/}
        <input
          placeholder="Password"
          onChange={(e) => setPassword(e.target.value)}
        />
        <button type="submit">Submit</button>
         </form>
    </div>
  )
}

export default App
```

app.css :

```css
.main {
  padding: 5%;
  text-align: center;
}

input {
  padding: 1%;
  width: 50%;
  margin: 1% 2%;
}

button {
  font-weight: bold;
  background: red;
  border: none;
  color: white;
  padding: 1%;
}
```

VALIDATION

app.js :

``` js
import logo from './logo.svg'
import './App.css'
import { useState } from 'react'

function App() {
  const [firstName, setFirstName] = useState('') // useState to store First Name
  const [lastName, setLastName] = useState('') // useState to store Last Name
  const [mobile, setMobile] = useState('') // useState to store Mobile Number
  const [age, setAge] = useState('') // useState to store Age
  const [email, setEmail] = useState('') // useState to store Email address of the user
  const [password, setPassword] = useState('') // useState to store Password

  // Function which will validate the input data whenever submit button is clicked.

  function validateForm() {
    // Check if the First Name is an Empty string or not.

    if (firstName.length == 0) {
      alert('Invalid Form, First Name can not be empty')
      return
    }

    // Check if the Email is an Empty string or not.

    if (email.length == 0) {
        alert('Invalid Form, Email Address can not be empty')
      return
    }

    // check if the password follows constraints or not.

    // if password length is less than 8 characters, alert invalid form.

    if (password.length < 8) {
      alert(
        'Invalid Form, Password must contain greater than or equal to 8 characters.',
      )
      return
      }

    // variable to count upper case characters in the password.
    let countUpperCase = 0
    // variable to count lowercase characters in the password.
    let countLowerCase = 0
    // variable to count digit characters in the password.
    let countDigit = 0
    // variable to count special characters in the password.
    let countSpecialCharacters = 0

    for (let i = 0; i < password.length; i++) {
      const specialChars = [
        '!',
        '@',
        '#',
        '$',
        '%',
        '^',
        '&',
        '*',
        '(',
        ')',
        '_',
        '-',
        '+',
        '=',
        '[',
        '{',
        ']',
        '}',
        ':',
        ';',
        '<',
        '>',
      ]

      if (specialChars.includes(password[i])) {
        // this means that the character is special, so increment countSpecialCharacters
        countSpecialCharacters++
      } else if (!isNaN(password[i] * 1)) {
        // this means that the character is a digit, so increment countDigit
        countDigit++
      } else {
        if (password[i] == password[i].toUpperCase()) {
          // this means that the character is an upper case character, so increment countUpperCase
          countUpperCase++
        }
        if (password[i] == password[i].toLowerCase()) {
            // this means that the character is lowercase, so increment countUpperCase
          countLowerCase++
        }
      }
    }

    if (countLowerCase == 0) {
      // invalid form, 0 lowercase characters
      alert('Invalid Form, 0 lower case characters in password')
      return
    }

    if (countUpperCase == 0) {
      // invalid form, 0 upper case characters
      alert('Invalid Form, 0 upper case characters in password')
      return
    }

    if (countDigit == 0) {
        // invalid form, 0 digit characters
      alert('Invalid Form, 0 digit characters in password')
      return
    }

    if (countSpecialCharacters == 0) {
      // invalid form, 0 special characters characters
      alert('Invalid Form, 0 special characters in password')
      return
    }

    // if all the conditions are valid, this means that the form is valid

    alert('Form is valid')
  }

  return (
    <div className="main">
      <form>
        {/* Input Field to insert First Name */}
        <input
          placeholder="First Name"
          onChange={(e) => setFirstName(e.target.value)}
          />
        {/* Input Field to insert Last Name */}
        <input
          placeholder="Last Name"
          onChange={(e) => setLastName(e.target.value)}
        />
        {/* Input Field to insert Mobile Number */}
        <input
          placeholder="Mobile Number"
          onChange={(e) => setMobile(e.target.value)}
        />
        {/* Input Field to insert Age */}
        <input placeholder="Age" onChange={(e) => setAge(e.target.value)} />
        {/* Input Field to insert Email Address of the user */}
        <input placeholder="Email" onChange={(e) => setEmail(e.target.value)} />
        {/* Input Field to insert Password */}
        <input
          placeholder="Password"
          onChange={(e) => setPassword(e.target.value)}
        />
        <button
          type="submit"
          onClick={() => {
            validateForm()
            }}
        >
          Submit
        </button>
      </form>
    </div>
  )
}

export default App
```
