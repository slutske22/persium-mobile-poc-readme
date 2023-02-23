### PERSIUM

# MapView Mobile: <br /> React Native Proof of Concept

<p float="left">
<img src="./assets/screenshots/2.png" width="200">
<img src="./assets/screenshots/1.png" width="200">
<img src="./assets/screenshots/3.png" width="200">
<img src="./assets/screenshots/9.png" width="200">
</p>

**_(This repository contains a README and screenshots only, for demonstration and portfolio purposes. No actual code is published here.)_**

This codebase is a proof of concept for Persium MapView. The MapView application lends itself well to being a native mobile application. The original frontend codebase is written with react and redux, which suggests that a mobile application could be quickly developed using react-native.

This project is bootstrapped with expo. To get it up and running:

- Clone the repo
- `npm install`
- `npm start`
- In the terminal, a QR code will be present. Use your iPhone or Android device to open the application. You will be prompted to download Expo Go as a means to view this application in development. You can also follow other options specified there if you are savvy with Android Studio or XCode.

## Why React Native?

The frontend codebase is written in react, with redux. The redux layer of the application (which emcompasses the model layer in an MVC scheme), can be copy-pasted from the front end almost verbatim. The fact that we can reuse almost all business logic saves hundreds of hours of development.

This is a huge advantage, in addition to the other general advantages of react native.

## Challenges

React-Native is an obvious choice for a mobile-native MapView application, but not a perfect choice. Here are a few of the primary challenges that this POC attempts to demonstrate are possible in RN:

### **The Map**

<p float="left">
<img src="./assets/screenshots/13.png" width="200">
<img src="./assets/screenshots/6.png" width="200">
<img src="./assets/screenshots/11.png" width="200">
</p>

The front end codebase uses leaflet and react-leaflet to render its primary map component. In this POC, I used [react-native-maps](https://github.com/react-native-maps/react-native-maps), the most popular mapping tool for react-native. This has worked well using the google maps option, with a custom style for the base of google maps. However, it also requires a google API key. Alternatives would be to use [mapbox for react-native](https://github.com/rnmapbox/maps), though tests with that showed very poor interactivity and performance.

Certain features present on the front end may prove challenging to reproduce using react-native (or any native app):

- Isobars and heatmap bezier curves - in the frontend javascript code, I was able to create perfectly smooth beziers using SVGs. This may be more challenging in a native environment, and may require [turfjs's bezierSpline](https://turfjs.org/docs/#bezierSpline), which is an inferior solution
- Windmaps in the frontend code are easily created using [leaflet-velocity](https://github.com/onaci/leaflet-velocity). There is no such parallel for mobile, so a similar effect would have to be coded from scratch

### **The Graphs**

<p float="left">
<img src="./assets/screenshots/5.png" width="200">
<img src="./assets/screenshots/4.png" width="200">
<img src="./assets/screenshots/8.png" width="200">
<img src="./assets/screenshots/7.png" width="200">
</p>

The frontend uses [HighchartsJS](https://www.highcharts.com/) for most of the graphing functionality. The graphs will need to be rewritten in a react-native friendly charting library. While there is a correlary [Highcharts for React Native](https://github.com/highcharts/highcharts-react-native), it doesn't seem particularly well maintained. Instead, this project uses [Victory.js](https://formidable.com/open-source/victory/), a charting library with excellent react-native support and up-to-date maintenance. Having 2 different libararies to build the same UI across 2 different platforms is not ideal, but developing the required Persium charts with Victory is relatively painless.
