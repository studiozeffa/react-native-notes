# React Native Basics

<!-- break -->

## Concepts

- A React Native app is simply a React app with a collection of custom components and APIs, which renders as a native mobile app instead of to the browser.
- Many of these components are inspired by the web (e.g. `View`, `Text`, `Image`).
- APIs are used to create stylesheets, access hardware sensors (camera, accelerometer, etc) and conditionally execute code on specific platforms.

<!-- break -->

## View

A `View` is like a `div`. Use it as a generic container, which can:

- be styled
- hold other components

``` jsx
const style = { /* ... */ };
return (
  <View style={style}>
    <Text>I'm inside a View!</Text>
  </View>
)
```

<!-- break -->

## Styles and StyleSheet

Styles are used to lay out and apply visual styles to a component. They are applied to components using the `style` attribute. A `StyleSheet` can be used to collect a group of styles.

Style notation is heavily inspired by CSS, but works differently - most notably, styles almost never cascade (that is, child components do not inherit styles applied to their parents).

Layout is governed by a system known as 'Yoga', which is very similar to flexbox. The one big exception is that it lays out neighbouring components in a column, rather than a row (i.e. `flexDirection` defaults to `'column'`).

Dimensions are numbers or percentages, instead of `px` or `em`.

<!-- break -->

## Styles and StyleSheet (example)

``` jsx
const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row'
  },
  box: {
    height: 200, width: 200,
    backgroundColor: 'azureblue'
  }
});

return (
  <View style={styles.container}>
    <View style={styles.box} />
    <View style={styles.box} />
  </View>
);
```

<!-- break -->

## Text

`Text` is used to render a set of characters to the screen.

Unlike all other components, `Text` will wrap when it reaches the end of its container. Styles will also cascade to child `Text` components.

Each platform has a predefined set of built-in fonts that can be used. You can also add custom fonts, similar to the web.

``` jsx
const style = { fontSize: 18, color: 'brown' };
return (
  <Text style={style}>
    The quick brown fox jumped over the lazy dog.
  </Text>
);
```

<!-- break -->

## Image

An `Image` component is used to render an image, either stored locally within the app, or from a remote URL.

Local images must be `require`d:

``` jsx
const source = require('./resources/image.png');
return <Image source={source} />
```

Remote images are loaded via their URL, and must have a specific height/width set (otherwise they will not be visible):

``` jsx
const source = { uri: 'http://lorempixel.com/350/150/' };
const style = { height: 150, width: 350 };
return <Image source={source} style={style} />
```

<!-- break -->

## Buttons

A React Native button can be created with one of two components:

- `TouchableHighlight`
- `TouchableOpacity`

You are free to use many other components as a child of the `Touchable*` component, typically you would use `Text` and/or `Image`.

Add an `onClick` attribute to govern what happens when the button is tapped.

A `Button` component also exists, which is a thin wrapper around `TouchableHighlight`. Use `TouchableHighlight` instead, as it is more flexible.

<!-- break -->

## TouchableHighlight

A button which changes the colour of its background when it is tapped.

Often used for main 'call-to-action' type buttons, or tappable items in a list.

``` jsx
const styles = StyleSheet.create({
  button: { backgroundColor: '#0288D1', padding: 20 },
  text: { color: '#FFFFFF' }
});
return (
  <TouchableHighlight style={styles.button}
   underlayColor="#01579B" onClick={onClick}>
    <Text style={styles.text}>Tap Me!</Text>
  </TouchableHighlight>
);
```

<!-- break -->

## TouchableOpacity

A button which lowers its opacity when it is tapped.

Often used for 'backgroundless' buttons, such as icon buttons in a header or tab bar.

``` jsx
const iconSource = require('./resources/icon.png');
const styles = StyleSheet.create({
  button: { padding: 4 },
  icon: { height: 20, width: 20 }
});
return (
  <TouchableOpacity style={styles.button}
   activeOpacity={0.5} onClick={onClick}>
    <Image style={styles.icon} source={iconSource} />
  </TouchableOpacity>
);
```
<!-- break -->

## ScrollView

Unlike the web, a regular `View` will not become scrollable when its content overflows the container.

We must use a `ScrollView` to achieve this.

``` jsx
return (
  <ScrollView>
    <Text>Laboris in ea fugiat nisi exercitation ipsum elit
    incididunt fugiat cupidatat in. Tempor nisi sint ad non
    excepteur mollit sint adipisicing. Laborum ut et culpa
    dolore elit eiusmod laborum in ullamco qui qui elit sunt.
    </Text>
  </ScrollView>
);
```