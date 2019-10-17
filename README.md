# Form-Validation



```html
<form id="form">

  <label for="name">
      <input name="name" type="text">
  </label>

  <label for="email">
      <input name="email" type="text">
  </label>

  <label for="password">
      <input name="password" type="password">
  </label>

  <label for="password_confirmation">
      <input name="password_confirmation" type="password">
  </label>

  <button type="submit">Go</button>
</form>
```

```js
import { Validator } from 'form-validation';

Validator({
  form: '#form', // optional

  rules: {
    name: 'required|between:3,20',
    email: 'required|email',
    password: 'minLenght:4|confirmed'
  },

  // optional ***
  messages: {
    required: 'This is an important field, do not be lazy.',
    // field.rule
    'email.email': 'I need your clothes, boots and Email'
  },

  attributes: {
    password: 'Secret field'
  },

  options: {
    cached: false
  },

  submit(event) {
    if (event.isValid) {
      console.log('Good');
    }
  },

  onInput(event) {
    console.log(event);
  }
});
```
---

## If app size are important and do not want to load all rules

```js
import { MakeValidator } from 'form-validation/make';
import { required, email } from 'form-validation/rules';

const isEqualNumberOne = {
  name: 'isEqualNumberOne',
  rule(params) {
    return params.value === '1';
  },
  message: 'Some text for :isEqualNumberOne', // optional
  attribute: 'this key name' // optional
};

const Validator = MakeValidator([required, email, isEqualNumberOne]);
```

### Fields key pattern

```js
 rules: {
          'name': 'minLenght:3', // The rule for a single field
          'list.*': 'required', // The rule for array fields
          'list.*.email': 'email', // Rule for special fields in the array
        }
```
