# Comprehensive Research Documentation on Form Validation in React.js

## Introduction

Form validation is a crucial aspect of web development, ensuring that user-submitted data is accurate and valid before being processed. In React.js, form validation can be achieved using various techniques and libraries. In this research documentation, we will explore different approaches to form validation in React.js, including built-in validation, custom validation, and popular libraries.

## Table of Contents

1. Built-in Form Validation in React.js
   1. Using HTML5 Form Validation Attributes
   2. Handling Built-in Validation Events

2. Custom Form Validation in React.js
   1. Validating on Submit
   2. Validating on Change
   3. Displaying Error Messages

3. Popular Libraries for Form Validation in React.js
   1. Formik
   2. Yup

## 1. Built-in Form Validation in React.js

### Using HTML5 Form Validation Attributes

React.js leverages the native HTML5 form validation attributes like `required`, `pattern`, `min`, `max`, etc. to perform basic validation. These attributes can be applied to form elements like input, select, and textarea.

Example:

```jsx
<form>
  <input type="text" required />
  <input type="email" required />
  <input type="number" min="0" max="100" />
  <input type="submit" value="Submit" />
</form>
```

### Handling Built-in Validation Events

React.js also allows handling built-in form validation events like `onInvalid`, `onInput`, and `onSubmit` to provide custom validation logic and error messages.

Example:

```jsx
class MyForm extends React.Component {
  handleSubmit = (event) => {
    event.preventDefault();
    // Custom validation logic
    // Submit form if valid, display errors otherwise
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" required />
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

## 2. Custom Form Validation in React.js

### Validating on Submit

Implementing custom validation on form submission involves checking the form data and displaying errors accordingly.

Example:

```jsx
class MyForm extends React.Component {
  state = {
    username: '',
    password: '',
    errors: {},
  };

  handleSubmit = (event) => {
    event.preventDefault();
    const { username, password } = this.state;
    const errors = {};

    // Custom validation logic
    if (!username) {
      errors.username = 'Username is required';
    }
    if (!password) {
      errors.password = 'Password is required';
    }

    // Handle form submission if there are no errors
    if (Object.keys(errors).length === 0) {
      // Submit form
    } else {
      this.setState({ errors });
    }
  };

  render() {
    const { username, password, errors } = this.state;
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" value={username} onChange={(e) => this.setState({ username: e.target.value })} />
        {errors.username && <p>{errors.username}</p>}
        <input type="password" value={password} onChange={(e) => this.setState({ password: e.target.value })} />
        {errors.password && <p>{errors.password}</p>}
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### Validating on Change

You can also perform real-time validation on form inputs as the user types by handling the `onChange` event.

Example:

```jsx
class MyForm extends React.Component {
  state = {
    username: '',
    errors: {},
  };

  handleChange = (event) => {
    const { name, value } = event.target;
    this.setState({ [name]: value });

    // Real-time validation
    const errors = {};
    if (name === 'username' && !value) {
      errors.username = 'Username is required';
    }
    this.setState({ errors });
  };

  handleSubmit = (event) => {
    event.preventDefault();
    // Form submission logic
  };

  render() {
    const { username, errors } = this.state;
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" name="username" value={username} onChange={this.handleChange} />
        {errors.username && <p>{errors.username}</p>}
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### Displaying Error Messages

Displaying clear and user-friendly error messages is essential for a better user experience. We've already seen examples of how to display error messages in the previous sections. By conditionally rendering error messages, we ensure that users are aware of the validation requirements.

## 3. Popular Libraries for Form Validation in React.js

### Formik

Formik is a widely used form library in the React.js ecosystem that simplifies form management and validation. It provides an easy way to define form fields, validation rules, and error handling.

Example:

```jsx
import { Formik, Form, Field, ErrorMessage } from 'formik';

const MyForm = () => (
  <Formik
    initialValues={{ username: '', password: '' }}
    validate={(values) => {
      const errors = {};
      if (!values.username) {
        errors.username = 'Username is required';
      }
      if (!values.password) {
        errors.password = 'Password is required';
      }
      return errors;
    }}
    onSubmit={(values) => {
      // Submit form
    }}
  >
    <Form>
      <Field type="text" name="username" />
      <ErrorMessage name="username" component="div" />
      <Field type="password" name="password" />
      <ErrorMessage name="password" component="div" />
      <button type="submit">Submit</button>
    </Form>
  </Formik>
);
```

### Yup

Yup is a schema validation library often used with Formik. It allows us to define validation rules in a schema and reuse them across different components.

Example:

```jsx
import { Formik, Form, Field, ErrorMessage } from 'formik';
import * as Yup from 'yup';

const validationSchema = Yup.object().shape({
  username: Yup.string().required('Username is required'),
  password: Yup.string().required('Password is required'),
});

const MyForm = () => (
  <Formik
    initialValues={{ username: '', password: '' }}
    validationSchema={validationSchema}
    onSubmit={(values) => {
      // Submit form
    }}
  >
    <Form>
      <Field type="text" name="username" />
      <ErrorMessage name="username" component="div" />
      <Field type="password" name="password" />
      <ErrorMessage name="password" component="div" />
      <button type="submit">Submit</button>
    </Form>
  </Formik>
);
```

## Conclusion

Form validation is a crucial aspect of creating interactive and user-friendly web applications. In this research documentation, we explored different techniques for implementing form validation in React.js, including built-in validation, custom validation, and popular libraries like Formik and Yup.