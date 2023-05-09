---
title: "Animation"
date: 2023-05-09
---

# Animation in SwiftUI

SwiftUI animation is simply the process of changing the state of a view over time. It's the process of creating a smooth transition between two states of a view. In SwiftUI, animations are triggered by changing the value of a state property.

## simple example

https://user-images.githubusercontent.com/129020081/237012726-434d84ed-9245-4894-ae2e-0926546c577d.mp4
```Swift
struct ContentView: View {
    @State private var scale: CGFloat = 1.0

    var body: some View {
        Text("Hello, world!")
            .scaleEffect(scale)
            .onTapGesture {
                withAnimation {
                    self.scale += 0.2
                }
            }
    }
}
```
In this example, we're using the scaleEffect modifier to scale the text based on the value of the scale property. When the user taps on the text, we're using the withAnimation function to animate the change in the scale property.

## Popular SwiftUI Animation Techniques

### 1. Transitions

Transitions are animations that occur when a view is added or removed from the screen. They can make your app feel more polished and professional by providing a smooth visual transition between screens. In SwiftUI, you can create transitions using the transition modifier.
```Swift
struct ContentView: View {
    @State private var showText = false

    var body: some View {
        VStack {
            if showText {
                Text("Hello, world!")
                    .transition(.move(edge: .leading))
            }

            Button("Toggle Text") {
                withAnimation {
                    showText.toggle()
                }
            }
        }
    }
}
```
https://user-images.githubusercontent.com/129020081/237012185-7678fc1b-8c22-453f-8cd1-be9ff2763b6e.mp4

### 2. Keyframe Animation
Keyframe animation involves specifying a series of keyframes that define the properties of a view at different points in time. The system then generates the intermediate frames to create a smooth animation between the keyframes. In SwiftUI, you can create keyframe animations using the animation modifier.
``` Swift 
struct ContentView: View {
    @State private var rotation = 0.0

    var body: some View {
        Image(systemName: "bolt.fill")
            .font(.largeTitle)
            .rotationEffect(.degrees(rotation))
            .animation(
                Animation
                    .linear(duration: 2.0)
                    .repeatForever(autoreverses: false)
            )
            .onAppear {
                rotation = 360.0
            }
    }
}
```
In this example, we're using the animation modifier to create a keyframe animation that rotates the bolt icon 360 degrees over a period of 2 seconds. We're also using the repeatForever function to repeat the animation indefinitely.

https://user-images.githubusercontent.com/129020081/237013737-69413d58-6c0e-4c3f-b308-8ba85c0d008f.mp4

### 3. Gesture Animation
Gesture animation involves animating a view in response to a user gesture, such as a tap or swipe. In SwiftUI, you can create gesture animations using the gesture modifier.
``` Swift 
struct ContentView: View {
  @State private var offset = CGSize.zero

  var body: some View {
    Circle()
      .fill(Color.blue)
      .frame(width: 100, height: 100)
      .offset(offset)
      .gesture(
        DragGesture()
          .onChanged { value in
            offset = value.translation
          }
          .onEnded { _ in
            withAnimation {
              offset = .zero
            }
          }
      )
  }
}
```
In this example, we're using the `gesture` modifier to create a drag gesture animation on the circle view. When the user drags the circle, we're using the `onChanged` function to update the offset of the circle view based on the user's drag. When the user releases the circle, we're using the `onEnded` function to animate the circle back to its original position.

https://user-images.githubusercontent.com/129020081/237014644-facc670e-3805-4a60-b672-5dc923d8c1d3.mp4

### 4. Easing Functions
Easing functions are mathematical equations that determine how quickly an animation starts and stops. They determine the rate of change of an animation over time. In SwiftUI, you can use the animation modifier to specify an easing function for your animation.

There are several built-in easing functions in SwiftUI that you can use, such as .linear, .easeIn, .easeOut, .easeInOut, and .spring. Here's a brief overview of each of these functions:

1. .linear: This is a constant-speed animation. The view moves at the same rate from start to finish.
2. .easeIn: This is a slow-starting animation. The view moves slowly at the beginning and accelerates as it progresses.
3. .easeOut: This is a fast-ending animation. The view moves quickly at the beginning and decelerates as it reaches the end.
4. .easeInOut: This is a combination of .easeIn and .easeOut. The view moves slowly at the beginning, accelerates in the middle, and decelerates at the end.
5. .spring: This is a bouncy animation that simulates the motion of a spring. The view overshoots the final position and bounces back before settling into place.

#### Custom Easing Functions
In addition to the built-in easing functions, you can also create your own custom easing functions in SwiftUI. Custom easing functions can be useful if you want to create a specific type of animation that isn't possible with the built-in functions.

To create a custom easing function, you can use the timingCurve function of the Animation struct. The timingCurve function takes four parameters that define the control points of the easing curve: c0x, c0y, c1x, and c1y.

``` Swift
struct ContentView: View {
    @State private var scale: CGFloat = 1.0

    var body: some View {
        Text("Hello, world!")
            .scaleEffect(scale)
            .onTapGesture {
                withAnimation(
                    Animation.timingCurve(0.5, 0.2, 0.5, 0.8, duration: 1.0)
                ) {
                    self.scale += 0.2
                }
            }
    }
}
```
https://user-images.githubusercontent.com/129020081/237017464-7a32cf8a-52d0-480b-a91c-5c19a2f5449f.mp4

In this example, we're using the timingCurve function to create a custom easing function. The four parameters define the control points of the easing curve. The first two parameters (c0x and c0y) define the starting point of the curve, and the last two parameters (c1x and c1y) define the ending point of the curve. The duration parameter specifies the duration of the animation.

In this case, we're using a custom easing function that starts slowly, accelerates quickly in the middle, and then decelerates slowly at the end. This creates a smooth and natural-looking animation that feels more organic than a linear animation.




