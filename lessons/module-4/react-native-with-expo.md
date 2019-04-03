---
title: Introduction to React Native with Expo
module: 4
tags: react native, mobile, expo
---

### Goals

By the end of this lesson, you will:

* Understand the differences between React and React Native
* Know how to bootstrap a React Native application using Expo
* Understand how to preview your application in the Expo app
* Understand the different native components and how to style them
* Know how to debug React Native with warnings, errors, and Chrome debugger
* Be familiar with when to use the different React lifecycle methods for mobile development

---

Welcome to the world of mobile development. React Native is just like the React you know and love for the web, but it compiles JavaScript to native code (Objective-C, Java) for a specific native OS. So you get the features of native apps while just writing JS! You also get the benefits of reusable components, state management with Redux, and Chrome debugging tools.

Here are some things we already know:

- JavaScript
- React
- Redux
- npm
- `package.json`

What is new is dealing with iOS and Android. For the most part you can write a most of your code that is used by both. But know that there will be differences in some UI components that you use, the process for emulating devices will be different and there will be performance differences between the two (if it runs fast on Android, it should be blazing fast on iOS).

Be aware that there are some drawbacks to using React Native. One is that the Facebook team releases updates every 2 weeks. The code updates consistently and there will be breaking changes in the future. Also, if you have a lot of components to scroll through, a user can gesture fast enough to cause a lag in performance.

That being said, there are huge advantages to using React Native. You can prototype, develop, and deploy mobile apps very quickly using just JS that works natively on iOS and Android. You can use hot-module reload to update your app and instantly see the change without recompiling all of your code. You can also write native code to create custom components or tweak performance and then easily drop them into your React Native code. There are great APIs for animations and gestures to create rich mobile user experiences. All in all, React Native is a fantastic way to jump into mobile development and create useful apps that work across Android and iOS.

## Expo

Getting started with React Native development can require a lot of development
environment configuration, including Xcode and Android studio. For some
applications, this is unavoidable, however for many applications, we can instead
use the Expo framework to bootstrap our React Native applications.

Per the docs: [Expo](https://expo.io/) is a free and open source toolchain 
built around React Native to help you build native iOS and Android projects 
using JavaScript and React.

### Bootstraping our application

To create our first React Native application, we're going to use the Expo CLI,
go ahead and download it globally.

`npm i -g expo-cli`

Once installed, we can use the CLI to create our first application:

`expo init ConceptBox`

After running this command you'll be prompted with some questions. Choose a
*blank* starter project, and a *managed* workflow. You can try this again later
with different options, but for now we want to work from the simplest example
possible. Next, you'll be asked to give your ConceptBox a display name.
Choose whatever you like here. Next, you'll be asked if you'd like to use Yarn
for managing dependencies. This is largely a personal choice, but we'll say no,
and just stick with npm.

That's it! We've just created our first React Native project. Let's move into
the project and start it up.

```
cd ConceptBox
npm start
```

This will launch Metro Bundler for you, and enable you to run your application
on a device (as long as you're on the same wireless network as your computer).
To do that though, we'll need to download the Expo client onto our device.

### Running the application on a device

To take advantage of Expo, you'll need to download the Expo client app to your
device. There are variants for both [iOS and Android](https://expo.io/tools#client).
Go ahead and download whatever works for you, and get an account set up with
Expo.

Once you have the Expo app on your device, you should be be able to scan that QR
code that you see in the terminal and browser, which will launch your
application inside the Expo app. If its not working for you, make sure that your
phone is on the same wireless network as your computer, and that you don't have
any kind of proxy running (like a VPN).

If everything worked, you should see the render of App.js on the screen. Cool!
Open up App.js and make a small change, then save the file. Your device should
have updated as well. Super cool!

### React Native Components

In React Native, we don't use HTML tags in our rendering, instead relying on
specialized components to build out our UI. Before we move on, take 5 minutes
and see what you can learn about the following components:

- [View](https://facebook.github.io/react-native/docs/view)
- [Text](https://facebook.github.io/react-native/docs/text)
- [TouchableOpacity](https://facebook.github.io/react-native/docs/touchableopacity)

For each of these, make sure you know:
- How do I add it to my component?
- What props does this accept?
- Can it respond to touch events? How?
- What would I use this for?

After you've read about each of the components, turn and talk with a partner,
and discuss the answers to the above questions.

### Styling our components

Adding style to our React Native components is a point of significant difference
from regular React. Rather than using CSS, we'll be using an abstraction from
React Native called [StyleSheet](https://facebook.github.io/react-native/docs/stylesheet).

Looking at the documentation, we see that writing these styles does feel similar
to CSS. In order to add specific styles to a component, we use the style prop on
the component. Take a look:

```
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>Open up App.js to start working on your app!</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    color: 'red',
  },
});
```

Here, I've added a `text` property to the styles StyleSheet, and I'm passing
that style to the specific component that needs it. Try adding some styles of
your own.

### Lets actually build something

Having an app running on our device is neat, but we want to do more than that.
Our app is called ConceptBox, and we want to build something that can display
user inputed 'concepts'. Clever huh?

To start, we'll need to use the
[TextInput](https://facebook.github.io/react-native/docs/textinput) component
from the React Native library. Modify your App.js to look like what I have
below:

```
import React from 'react';
import { StyleSheet, TextInput, View } from 'react-native';

export default class App extends React.Component {
  render() {
    return (
      <View style={ styles.container }>
        <TextInput
          style={ styles.conceptInput }
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'flex-start',
    paddingTop: 100,
  },
  conceptInput: {
    height: 30,
    width: 200,
    fontSize: 30,
    borderColor: 'black',
    borderWidth: 1,
  },
});
```

### Build on your own

We have a text input now that can accept user input, but we need to do more with
our concepts. Take the next 20 minutes and try to accomplish the following:

- When a user type in the TextInput, it should update the state of our component
- There should be a button for the user to press, adding the concept to an array
  in state
- The component should list all of the available concepts on the device
- BONUS: A concept should be removable from the screen

We'll come back together and share our learnings after 20 minutes.

## Lets talk debugging

Debugging is a critical part of development on any platform, and React Native is
no different. If you're running the app on a device, shake the device to bring
up the Expo menu. You should see an option to 'Start remote debugging'. Click
that.

This opens up a browser window where you have access to the console and
debugger. Open up the console and select the `Pause on Exceptions` button. Then
throw a debugger into your JS and save, causing the app to reload. The debugger
should trigger, allowing you to inspect `this`, `props`, etc.

## A Refresher in the React Component Lifecycle

Just like normal React, we have access to the component lifecycle API. Here is a quick rundown of how each method is utilized for mobile:

### Mounting Cycle

* constructor(props) - Instantiate the component class and pass in props from the parent component (or container). Can also set local state in the component.
* componentWillMount() - Invoked just once, right before component renders.
* render() - Renders a React component or null.
* componentDidMount() - Invoked just once right after component renders. Good time to make API call or execute delayed code.

### Updating Cycle

* componentWillReceiveProps(nextProps) - Parent of component has passed in new props. This component will now re-render. Good time to set local state before the re-render (if necessary)
* shouldComponentUpdate(nextProps, nextState) - Returns either true or false. Defaults to true. If true, the component will re-render. If false, the component will not re-render. Usually used by comparing current props to passed in props.
* componentWillUpdate(nextProps, nextState) - Called once the component decides it will re-render. Can't set local state here.
* render() - Renders a React component or null if shouldComponentUpdate returns true.
* componentDidUpdate(prevProps, prevState) - Invoked right after component re-renders.

## Conclusion

This is just a taste of what you could do with React Native, but you should
realize by know that you really already know how do do most of the difficult
parts. Mobile apps often require a bit more configuration that what you may be
used to from the Web, but if you can work through that, you can add a valuable
skill to your toolset with React Native.

## Resources

- [React Native Docs](https://facebook.github.io/react-native/)
- [Expo Docs](https://docs.expo.io/versions/latest/)
- [React Native Styles Cheat
Sheet](https://github.com/vhpoet/react-native-styling-cheat-sheet)