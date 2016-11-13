# React Native Electron

[Electron](http://electron.atom.io/) extensions to [React Native for Web](https://github.com/necolas/react-native-web)

## Introduction

This project aims to provide extensions to [React Native for Web](https://github.com/necolas/react-native-web) targeted to the [Electron](http://electron.atom.io/) environment to support additional modules exposed by React Native (ex Clipboard, WebView) using Electron APIs.

This is very early stage, not fully tested, and APIs will likely change between releases, so don't use this library if you need something stable.

## Installation

```sh
npm install react-native-electron
```

`electron`, `react` and `react-native-web` are required peer dependencies, make sure to install them as well:

```sh
npm install electron react react-native-web
```

## Example

See the `example` directory for the source code and Webpack config.

To run the demo app, fork this repository and run:

- `npm install`
- `npm run example:server`
- In another terminal instance, `npm run example:electron`

## APIs

### Alert

[React Native's Alert](https://facebook.github.io/react-native/docs/alert.html) implementation using [Electron's dialog](http://electron.atom.io/docs/api/dialog/)

```
Alert.alert(
  title: string,
  message: ?string,
  buttons: ?Array<{text: string, onPress?: () => void}> = [],
  type: ?('none' | 'info' | 'error' | 'question' | 'warning') = 'none'
): void
```

### Clipboard

[React Native's Clipboard](https://facebook.github.io/react-native/docs/clipboard.html) implementation using [Electron's clipboard](http://electron.atom.io/docs/api/clipboard/)

`Clipboard.getString(type: ?string): Promise<?string>`

`Clipboard.setString(text: string, type: ?string): void`

### Linking

[React Native's Linking](https://facebook.github.io/react-native/docs/linking.html) implementation using [Electron's shell](http://electron.atom.io/docs/api/shell/)

`Linking.openURL(url: string): Promise<void>`

## Components

### WebView

[React Native's WebView](https://facebook.github.io/react-native/docs/webview.html) implementation using [Electron's webview tag](http://electron.atom.io/docs/api/web-view-tag/)

Communication between the WebView and its container is possible by providing an `onMessage()` handler, that will receive events having messages injected in `event.nativeEvent.data`, and calling the `postMessage()` method to send messages to the WebView contents. Messages must be strings.  
This bridge is implemented using the [`preload` attribute](http://electron.atom.io/docs/api/web-view-tag/#preload) of Electron's WebView. If you override this attribute, make sure to provide a [similar implementation](https://github.com/PaulLeCam/react-native-electron/blob/master/src/components/WebView.preload.js) so the bridge can work.  
Loading this preload script uses node's `__dirname`, make sure your application injects it as expected, see this [Webpack config for example](https://github.com/PaulLeCam/react-native-electron/blob/master/example/webpack.config.babel.js#L12).

**Props:**

- `onMessage: ?(event: Event) => void`
- `source: {uri: string} | {html: string}`

**Methods**

- `postMessage (message: string): void`

## License

MIT  
See [LICENSE](LICENSE) file.
