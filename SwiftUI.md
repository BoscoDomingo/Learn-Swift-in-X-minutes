# SwiftUI

Views are now value types, coming from `struct`, and are a function/result of their state, no longer do you have to manually update each one of them.

SwiftUI views must have a `ContentView` which in itself has a `body`, which is what is rendered, and *modifiers* for the different elements in that body. Ultimately, small atomic blocks make up greater architectures.

```
struct ContentView: View {
    var body: some View {
        Text("Hello World")
    }
}
```

The order of modifiers affects the final result, so be careful. For example:
```
Text("Some text").background(Color.blue).padding() //The padding is NOT coloured
Text("Some text").padding().background(Color.blue) //The padding is coloured
```

## Cycle of interactions

![Cycle of interactions](https://i.imgur.com/RDykMxL.png)

## States and bindings

You should **only have 1 source of truth** for each piece of information (or 1 `@State` per property), meaning all other Views that want to use that source of truth should make use of `@Binding`s (Bindings are read-write). `@State` is not a great fit for external data (such as things coming from backend), since it is "stuck" inside SwiftUI. Use the `BindableObject` protocol for these types of data:
![@State and BindableObject](https://i.imgur.com/g9hOeC9.png)
![@Binding](https://i.imgur.com/0LPvONN.png)

Generally speaking, you want to avoid the use of `@State` and favour other alternatives when possible

## Information from a Model

`@ObjectBinding` is akin to `@State` except it works between a Model and a View that listens to said Model's property's changes, where `@State` is between Views themselves.

![@ObjectBinding](https://i.imgur.com/K80oZAb.png)
An alternative for hierarchies is `@EnvironmentObject` which avoids having to pass the `BindableObject` property from View to View, and instead grab it straight from `Environment`, always with 1 source of truth and thus no concurrency problems.
![@EnvironmentObject](https://i.imgur.com/kgut0rm.png)

## Hosting SwiftUI inside UIKit
- `UIHostingController` - For iOS apps
- `NSHostingController` - For MacOS apps
- `WKHostingController` - For watchOS apps
They are all subclases of `UIViewController` and thus will work seamlessly with existing UIKit views

## Hosting UIKit inside SwiftUI
The `Representable` protocol exists for this purpose.
- `UIViewRepresentable` - For iOS apps
- `NSViewRepresentable` - For MacOS apps
- `WKInterfaceObjectRepresentable` - For watchOS apps
## Know more/Code snippets

* [A great resource for some example code with image previews](https://github.com/fzhlee/SwiftUI-Guide/blob/master/README_English.md)
* [Everything you'll ever need about SwiftUI](https://github.com/Juanpe/About-SwiftUI/blob/master/README.md)