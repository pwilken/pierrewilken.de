---
layout: post
title: React Native - Probleme und Lösungen
lang: de
ref: rnprobsolv
date: 2018-09-01 11:30:00 +0300
description: React Native - Probleme und potentielle Lösungen
img: phone-broken.jpg 
tags: [React Native, ProblemSolution, mobile apps, android, iOS]
---

## Auflistung von Problemen bei der Entwicklung mit React-Native und potentiellen Lösungen

| Probleme | Lösungen |
| ------ | ------ |
| (rn001) ERROR  Metro Bundler can't listen on port 8081 | Noch laufende Node.js Prozesse killen. |
| (rn002) Development server responses error code 500 - Response error 10.0.2.2 | ```$Npm start``` danach ```$react-native run-android``` oder run-ios <=> Alternativ: bearbeite package.json: react-native Version zu "55.4" oder "55.2" und babel-preset-react-native zu "4.0.0" |
| (rn003) bundling failed: Error: Plugin 0 provided an invalid property of “default” (babel-preset-react-native) |```$npm remove babel-preset-react-native``` danach ```$npm add babel-preset-react-native@2.1.0``` |
| (rn004) Could not determine java version from '10.0.1'. | "app-folder/android/gradle/wrapper/gradle-wrapper.properties" distributionUrl ändern -- (z.B. zu) -> distributionUrl=https\://services.gradle.org/distributions/gradle-4.3-rc-2-all.zip |



