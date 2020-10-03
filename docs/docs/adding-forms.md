---
title: Adding Forms
---

गॅटस्बी रिऍक्ट वर बिल्ड केलेले असल्यामुळे जे काही रिऍक्ट वर शक्य आहे ते सर्व गॅटस्बी वर देखील शक्य आहे .रिऍक्ट फॉर्म कसे तयार करावे याबद्दल अतिरिक्त तपशील या मध्ये पाहता येईल [React forms documentation](https://reactjs.org/docs/forms.html) (जे गॅटस्बीसह बिल्ड केले जाते)

खालील पेज-पासून सुरुवात करा.

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

हे गॅटस्बी पेज एक रिऍक्टचे घटक असून जेव्हा तुम्हाला एक फॉर्म तयार करायचा असेल, तेव्हा वापरकर्त्याने काय एंटर केले आहे ते आपल्याला फॉर्मची स्थिती स्टोर करावी लागेल. आपले कार्य (stateless) घटक वर्ग (stateful) घटकात रूपांतरीत करा

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  render() {
    return <div>Hello world!</div>
  }
}
```

आता जेव्हा आपण क्लास कॉम्पोनन्ट तयार केला आहे तर आपण कॉम्पोनन्ट मध्ये `state` ऍड करू  शकतो.

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  render() {
    return <div>Hello world!</div>
  }
}
```

आणि आता तुम्ही काही इनपुट फील्ड जोडू शकता.

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  render() {
    return (
      <form>
        <label>
          First name
          <input type="text" name="firstName" />
        </label>
        <label>
          Last name
          <input type="text" name="lastName" />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

जेव्हा वापरकर्ता इनपुट बॉक्समध्ये टाईप करतो, तेव्हा state अपडेट व्हायला हवे. स्थिती अपडेट करण्यासाठी `onChange` प्रॉप जोडा आणि नवीन स्थितीसह इनपुट उपडेट ठेवण्यासाठी `value` प्रॉप जोडा:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value,
    })
  }

  render() {
    return (
      <form>
        <label>
          First name
          <input
            type="text"
            name="firstName"
            value={this.state.firstName}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Last name
          <input
            type="text"
            name="lastName"
            value={this.state.lastName}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

आता जेव्हा तुमचे इनपुट कार्यरत आहेत, फॉर्म सादर करताना काहीतरी घडावं अशी तुमची इच्छा असल्यास फॉर्म घटकात `onSubmit` प्रॉप्स जोडा आणि वापरकर्ता फॉर्म सादर करताना अलर्ट दर्शवण्यासाठी `handleSubmit` जोडा: 

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value,
    })
  }

  handleSubmit = event => {
    event.preventDefault()
    alert(`Welcome ${this.state.firstName} ${this.state.lastName}!`)
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          First name
          <input
            type="text"
            name="firstName"
            value={this.state.firstName}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Last name
          <input
            type="text"
            name="lastName"
            value={this.state.lastName}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

हा फॉर्म वापरकर्त्याची माहिती दाखवण्याव्यतिरिक्त काही अतिरिक्त करत नाही. या वेळी, आपण हा फॉर्म एका कॉम्पोनन्ट कडे हलवू शकता, फॉर्म स्टेट बॅकएंड सर्वरवर पाठवा, किंवा रोबस्त मान्यता जोडा. तुम्ही अप्रतिम रिऍक्ट देखील वापरू शकता, जसे लायब्ररी [Formik](https://github.com/jaredpalmer/formik) किंवा [Final Form](https://github.com/final-form/react-final-form) आपल्या विकास प्रक्रियेला गती देण्यासाठी वापरू शकता.

गॅटस्बीची पॉवर लेव्हरेज करत आहे आणि रिऍक्ट इकोसिस्टिम मुळे हे सर्व शक्य आहे.
