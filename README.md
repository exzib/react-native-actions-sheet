# react-native-actions-sheet-custom-backdrop

A fork of [react-native-actions-sheet](https://github.com/ammarahm-ed/react-native-actions-sheet) with support for custom backdrop components (BlurView, gradients, images, etc.).

## Installation

```bash
npm install react-native-actions-sheet-custom-backdrop
# or
yarn add react-native-actions-sheet-custom-backdrop
```

### Peer Dependencies

```bash
npm install react-native-gesture-handler react-native-reanimated react-native-safe-area-context
```

## Custom Backdrop Usage

This fork adds a `CustomBackdropComponent` prop that allows you to render any custom backdrop instead of the default dark overlay.

### Props

| Prop | Type | Description |
|------|------|-------------|
| `CustomBackdropComponent` | `React.ComponentType<CustomBackdropProps>` | Custom component to render as backdrop |

### CustomBackdropProps

Your custom backdrop component receives:

| Prop | Type | Description |
|------|------|-------------|
| `opacity` | `SharedValue<number>` | Animated opacity value (0 to `defaultOverlayOpacity`, default 0.3) |
| `onPress` | `() => void` | Handler to call when backdrop is pressed |

### Example: BlurView Backdrop

```tsx
import ActionSheet, { CustomBackdropProps } from 'react-native-actions-sheet-custom-backdrop';
import { BlurView } from '@react-native-community/blur';
import Animated, { useAnimatedStyle } from 'react-native-reanimated';
import { Pressable, StyleSheet } from 'react-native';

const BlurBackdrop = ({ opacity, onPress }: CustomBackdropProps) => {
  const animatedStyle = useAnimatedStyle(() => ({
    opacity: opacity.value / 0.3, // normalize 0-0.3 to 0-1
  }));

  return (
    <Animated.View style={[StyleSheet.absoluteFill, animatedStyle]}>
      <BlurView style={StyleSheet.absoluteFill} blurType="dark" blurAmount={10}>
        <Pressable style={StyleSheet.absoluteFill} onPress={onPress} />
      </BlurView>
    </Animated.View>
  );
};

// Usage
<ActionSheet ref={actionSheetRef} CustomBackdropComponent={BlurBackdrop}>
  <View style={{ padding: 20 }}>
    <Text>Sheet content here</Text>
  </View>
</ActionSheet>
```

### Example: Gradient Backdrop

```tsx
import LinearGradient from 'react-native-linear-gradient';

const GradientBackdrop = ({ opacity, onPress }: CustomBackdropProps) => {
  const animatedStyle = useAnimatedStyle(() => ({
    opacity: opacity.value / 0.3,
  }));

  return (
    <Animated.View style={[StyleSheet.absoluteFill, animatedStyle]}>
      <LinearGradient
        colors={['transparent', 'rgba(0,0,0,0.8)']}
        style={StyleSheet.absoluteFill}
      >
        <Pressable style={StyleSheet.absoluteFill} onPress={onPress} />
      </LinearGradient>
    </Animated.View>
  );
};
```

### Example: Expo Blur

```tsx
import { BlurView } from 'expo-blur';

const ExpoBlurBackdrop = ({ opacity, onPress }: CustomBackdropProps) => {
  const animatedStyle = useAnimatedStyle(() => ({
    opacity: opacity.value / 0.3,
  }));

  return (
    <Animated.View style={[StyleSheet.absoluteFill, animatedStyle]}>
      <BlurView intensity={50} style={StyleSheet.absoluteFill}>
        <Pressable style={StyleSheet.absoluteFill} onPress={onPress} />
      </BlurView>
    </Animated.View>
  );
};
```

## Original Documentation

For all other features and API reference, check out the original documentation: [https://rnas.vercel.app](https://rnas.vercel.app)

## Credits

This is a fork of [react-native-actions-sheet](https://github.com/ammarahm-ed/react-native-actions-sheet) by [ammarahm-ed](https://github.com/ammarahm-ed).

### MIT Licensed
