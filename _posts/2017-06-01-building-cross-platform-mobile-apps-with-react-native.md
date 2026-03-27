---
title: "Building Cross-Platform Mobile Apps with React Native"
description: "Lessons learned shipping to both iOS and Android from a single JavaScript codebase."
tags: [Mobile]
---

When React Native launched, the promise was straightforward: write JavaScript once, ship to iOS and Android. After shipping several apps with it, the reality is nuanced — but more positive than the skeptics expected.

## The good parts

**Shared business logic** is where React Native really delivers. Navigation state, API calls, data transforms, validation — all of it runs from a single JS bundle. For a team that already knows React, the ramp-up is measured in days, not months.

**Hot reloading** is legitimately faster than native development. Seeing a layout change reflected in under a second, without a full recompile, changes how you explore UI ideas.

**Community and ecosystem** have caught up considerably. Libraries for maps, cameras, payments, and analytics cover the common use cases. When something isn't covered, the native module bridge lets you drop into Swift or Kotlin without abandoning the JS layer.

## The parts that bite you

### Platform divergence is real

React Native gives you a shared component model, but not a shared design system. iOS and Android have different conventions — back-navigation, typography, gesture handling, sheet modals. Apps that ignore this feel wrong on both platforms. Budget time to write platform-specific variants using the `.ios.js` / `.android.js` file convention:

```
components/
  Button.js          ← shared logic
  Button.ios.js      ← iOS-specific styling
  Button.android.js  ← Android-specific styling
```

### The bridge is a bottleneck

Before the New Architecture (Fabric + JSI), heavy animations that crossed the JS/native bridge could stutter. The rule was simple: if it needs to run at 60fps, do it natively or use `Animated` with `useNativeDriver: true`. With JSI, synchronous native calls are now possible, which removes most of this concern for new projects.

### Build tooling is fragile

CocoaPods on iOS and Gradle on Android have their own dependency resolution models that occasionally conflict with the JS layer. Keep a clean upgrade checklist. Pin your React Native version at the start of a project and upgrade deliberately, not reactively.

## What I'd tell my past self

1. Start with [Expo](https://expo.dev) for any app that doesn't need custom native modules. The managed workflow eliminates most tooling pain.
2. Use TypeScript from day one. The JS/native boundary is already stringly-typed enough.
3. Test on a real device early. The simulator lies about performance and gesture feel.
4. Hire one iOS and one Android engineer to review your platform-specific code, even if you're a JS team.

React Native is not a silver bullet, but for the right team and the right product it genuinely halves the mobile development surface area. That's a real advantage.
