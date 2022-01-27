# React Hook Form VS Formik

### A comprehensive comparison of the two libraries, with examples <a href="#3001" id="3001"></a>

![](https://miro.medium.com/max/1400/1\*St-bCu45SR6OiUHVH34sxA.png)

Working with forms is one of the most challenging problems to solve when developing applications with React. React is a minimalist UI library focused only on controlling the behavior of the interface, making sure that the UI change appropriately as a response to the user’s activity.

It doesn’t offer a complete solution for responding to user’s inputs, but it does offer [a method to save form values into local state](https://reactjs.org/docs/forms.html) with Controlled Components.

Handling forms in React requires you to write lots of boilerplate code for:

* Managing and validating user input values with state
* Keeping track of invalid error messages
* Handling form submission

To make form building experience easy and great, many developers have created libraries to help to build forms with React. One of the most popular solutions for building forms is a library called [Formik](https://jaredpalmer.com/formik/).

I have personally used Formik as my go-to solution when building forms with React, and it worked great. But recently, I have been playing with a new form builder library called [React Hook Form](https://react-hook-form.com).

In this article, I will help you see the benefits of using React Hook Form over Formik. But first, let’s start with learning how to create a regular React form.

As a side note, if you’re looking for a good tool and platform to publish and reuse your React form components, I recommend you use [**Bit**](https://bit.dev).

[Bit](https://bit.dev) makes it quick and easy to publish components from any project with tools that automate the long and time-consuming (manual) work that’s traditionally part of this process.

Example: Exploring React components published on [Bit.dev](https://bit.dev)

![](https://miro.medium.com/max/700/1\*T6i0a9d9RykUYZXNh2N-DQ.gif)

## How to handle forms with React <a href="#3c46" id="3c46"></a>

Here’s an example of a React form built without any library. We’re going to use the Bootstrap framework to make the form prettier:



In the example above, we first create a function component with a single state named `formState` where we keep the state of input values, input validity, and input errors. The form has two inputs for `email` and `password` respectively, so we need to write initial values for each input:

```tsx
export default () => {  const [formState, setFormState] = useState({    formValues: {      email: "",      password: ""    },    formErrors: {      email: "",      password: ""    },    formValidity: {      email: false,      password: false    }  });
```

Next, we write the UI rendering function inside the `return` statement:

```tsx
return (    <div className="container">      <div className="row mb-5">        <div className="col-lg-12 text-center">          <h1 className="mt-5">React regular form</h1>        </div>      </div>      <div className="row">        <div className="col-lg-12">          <form onSubmit={handleSubmit}>            <div className="form-group">              <label>Email address</label>              <input                type="email"                name="email"                className={`form-control ${                  formState.formErrors.email ? "is-invalid" : ""                }`}                placeholder="Enter email"                onChange={handleChange}                value={formState.formValues.email}              />              <div className="invalid-feedback">                {formState.formErrors.email}              </div>            </div>            <div className="form-group">              <label>Password</label>              <input                type="password"                name="password"                className={`form-control ${                  formState.formErrors.password ? "is-invalid" : ""                }`}                placeholder="Password"                onChange={handleChange}                value={formState.formValues.password}              />              <div className="invalid-feedback">                {formState.formErrors.password}              </div>            </div>            <button type="submit" className="btn btn-primary btn-block">              Submit            </button>          </form>        </div>      </div>    </div>  );
```

We used `formValues` to display the value of inputs, while `formErrors` are used to dynamically indicate that the form values are invalid.

Next, we write the `handleChange` function as follows:

```tsx
const handleChange = ({ target }) => {  const { formValues } = formState;  formValues[target.name] = target.value;  setFormState({ formValues });  handleValidation(target);};
```

The function will update the state value and run the `handleValidation` function to check the new state value:

```tsx
const handleValidation = target => {    const { name, value } = target;    const fieldValidationErrors = formState.formErrors;    const validity = formState.formValidity;    const isEmail = name === "email";    const isPassword = name === "password";    const emailTest = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/i;validity[name] = value.length > 0;    fieldValidationErrors[name] = validity[name]      ? ""      : `${name} is required and cannot be empty`;if (validity[name]) {      if (isEmail) {        validity[name] = emailTest.test(value);        fieldValidationErrors[name] = validity[name]          ? ""          : `${name} should be a valid email address`;      }      if (isPassword) {        validity[name] = value.length >= 3;        fieldValidationErrors[name] = validity[name]          ? ""          : `${name} should be 3 characters minimum`;      }    }setFormState({      ...formState,      formErrors: fieldValidationErrors,      formValidity: validity    });  };
```

The `handleValidation` function is where things get really complicated. It needs to first check which input that’s being validated, and then proceed to validate accordingly.

If it’s `email` field, it will check for the email pattern. If it’s a `password` field, it will validate the value is at least 3 characters long. We’ll then set the error message into `formErrors` and mark the validity of the field with `formValidity` .

Finally, we need to write the `handleSubmit` function:

```tsx
const handleSubmit = event => {  event.preventDefault();  const { formValues, formValidity } = formState;  if (Object.values(formValidity).every(Boolean)) {    // Form is valid    console.log(formValues);  } else {    for (let key in formValues) {      let target = {        name: key,        value: formValues[key]      };      handleValidation(target);    }  }};
```

When the form is valid, we’ll log the values into the console. If not, we’ll run the `handleValidation` function for every property inside `formValues` object. React will let users know which form is invalid.

And that’s how you build a form with React. As we’ve just seen, a form with only two input fields is already _very verbose_. Imagine how you will write a form with a dozen fields!

Now that you know how building forms the “React” will result in a code that’s verbose, repetitive, and time-consuming, you’re ready to learn how Formik reduces the pain of building forms.

## This is how Formik can help you <a href="#5c56" id="5c56"></a>

[Formik](https://jaredpalmer.com/formik/docs/overview) is a popular form building solution because it provides you a reusable form component where you can simply use its API for handling the three most annoying part in form building:

1. Getting values in and out of form state
2. Validation and error messages
3. Handling form submission

To get started with Formik, you need to install it using the `npm install formik` command. Here’s the same form with two input fields, build using Formik:



This new form uses four components provided by Formik: `Formik`, `Form`, `Field`, and `ErrorMessage`. To use Formik, we need to wrap the `Form` component inside `Formik` component:

```tsx
<Formik>  <Form>    {/* the rest of the code here */}  </Form></Formik>
```

Just as the regular form, we will first initialize the value of our form with state, but instead of writing the whole state for value, validation, and validity, we simply use Formik’s `initialValues` props:

```tsx
<Formik  initialValues={{    email: "",    password: ""  }}  onSubmit={onSubmit}>
```

The Formik component also accepts a function prop to run on submit event, so let’s write down the `onSubmit` function, which will be run only when the form values are valid:

```tsx
// Put this inside your component before the return statementconst onSubmit = values => {  // form is valid  console.log(values);}
```

Next, it’s time to write our form using the `Form` component. First, we’re going to use props passed down from `Formik` component into `Form` by using the destructuring props pattern. We’ll take the `errors` and `touched` props so that we know when an input field has been touched and if it contains any errors:

```tsx
{({errors, touched}) => (    <Form>      <div className='form-group'>        <label htmlFor='email'>Email</label>        <Field          name='email'          placeholder='Enter email'          className={`form-control ${            touched.email && errors.email ? 'is-invalid' : ''          }`}          validate={validateEmail}        />        <ErrorMessage          component='div'          name='email'          className='invalid-feedback'        />      </div>      <div className='form-group'>        <label htmlFor='password'>Password</label>        <Field          name='password'          type='password'          placeholder='Enter password'          className={`form-control ${            touched.password && errors.password ? 'is-invalid' : ''          }`}          validate={validatePassword}        />        <ErrorMessage          component='div'          name='password'          className='invalid-feedback'        />      </div>    <button className='btn btn-primary btn-block' type='submit'>        Submit      </button>    </Form>  )}
```

The `ErrorMessage` component from Formik will automatically display any error message found from Formik’s `errors` props by matching the name you passed into it with the name of the `Field` component.

By passing `div` into its `component` props. We’re telling Formik to render the error message as a `div` element

As you can see in the code above, we also pass a `validate` prop that contains validation functions. Let’s write these functions to complete our form:

```tsx
function validateEmail(value) {  let error;  if (!value) {    error = "Email is required";  } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(value)) {    error = "Invalid email address format";  }    return error;}function validatePassword(value) {  let error;  if (!value) {    error = "Password is required";  } else if (value.length < 3) {    error = "Password must be 3 characters at minimum";  }    return error;}
```

Formik’s validate function will simply pass on the value of the `Field` component that you can use inside your validation functions. If the value is invalid, Formik expects a `string` containing the error message, else you can simply return `undefined` . This way, you can separate validation functions instead of streamlining them as one like in the regular form, which is very prone to error.

And now the Formik form is complete. You’ve just learned how Formik reduces the amount of code you’ve written to build a form. Isn’t that great? You don’t have to get values in and out of form, and you can separate your validation functions.

Formik is already so much easier than a regular form. But does React Hook Form really offer any kind of benefits over Formik? As it turns out, React Hook Form is even better than Formik.

## Enter React Hook Form <a href="#bc63" id="bc63"></a>

Just like Formik, [React Hook Form](https://react-hook-form.com/get-started) is a form builder library that aims to reduce the pain of creating forms with React. A big difference between the two is that React Hook Form is designed to make use of uncontrolled components to avoid unnecessary re-rendering caused by user inputs.

Here’s how you implement the same form with React Hook Form. The first thing to notice is that here we’re writing even fewer lines of code than with Formik:



To start using React Hook Form, we need to install it with `npm install react-hook-form` command. Then, we need to import the useForm hook, which handles the process of receiving inputs, validating values and submitting the form, and the `ErrorMessage` component, which is very identical to the one you see in Formik.

```tsx
import { useForm, ErrorMessage } from "react-hook-form";
```

First, we’re going to call the `useForm` hook, which will return an object with a set of functions that we can use to build the form:

```tsx
export default () => {  const { register, errors, handleSubmit } = useForm();
```

The core concept of React Hook Form is to `register` your uncontrolled component into the Hook by using the [`ref`](https://reactjs.org/docs/refs-and-the-dom.html)[ prop](https://reactjs.org/docs/refs-and-the-dom.html). This will make its value available for both the form validation and submission:

```tsx
<input  name='email'  placeholder='Enter email'  className={`form-control ${errors.email ? 'is-invalid' : ''}`}  ref={register({    required: 'Email is required',    pattern: {      value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i,      message: 'Invalid email address format',    },  })}/>;
```

The register function also serves to create the validation rule for the current input element. [React Hook Form’s validation rule](https://react-hook-form.com/get-started#Applyvalidation) is designed to be very similar to [HTML standard form validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form\_validation#Using\_built-in\_form\_validation).

With the validation in place, any error message we receive will be passed to the `errors` object, which contains form errors and error messages corresponding to each input.

We will then pass the errors object to the `ErrorMessage` component, which will look for a matching `errors` object prop with the `name` prop we passed into it. Then, we specify the message to be rendered as a `div` by using the `as` prop:

```tsx
<ErrorMessage className="invalid-feedback" name="email" as="div" errors={errors} />
```

Lastly, we just need to pass the handleSubmit function to our form’s onSubmit prop, which will pass the form data when it’s valid. In this example, we will pass the data to our `onSubmit` function, which will log the form data just like in other code examples:

```tsx
export default () => {  const { register, errors, handleSubmit } = useForm();  const onSubmit = values => {    // form is valid    console.log(values);  }  return (    <div className="container">      {/* .. other code */}      <form onSubmit={handleSubmit(onSubmit)}>
```

And now your React Hook Form is complete. Aside from having fewer lines of code, React Hook Form is based on the idea of harnessing uncontrolled components through Hooks so that you can have the best performance with least re-render.

Here is a brief comparison between React Hook Form and Formik:

Comparison between React Hook Form and Formik. [Source](https://react-hook-form.com/faqs#ReactHookFormFormikorReduxForm).

![](https://miro.medium.com/max/700/1\*NJYbnMpxaVbmqZPGr3I\_ww.png)

## Conclusion <a href="#a66a" id="a66a"></a>

Through this article, you’ve learned about the pain of building forms with React and how form building libraries like Formik and React Hook Form can help you build forms with less tears.

Both Formik and React Hook Form are solving the same problem, but React Hook Form’s way of building a form with uncontrolled components and hooks enable it to score a better performance result than Formik.

Also, you don’t need to import any components at all. You can simply write plain input elements with a `ref` prop and you’re good to go.

If you’re looking for a form building library, I recommend you to use React Hook Form. It’s better than Formik.

## Learn More <a href="#98af" id="98af"></a>

[\
](https://blog.bitsrc.io/will-react-classes-get-deprecated-because-of-hooks-bb62938ac1f5)
