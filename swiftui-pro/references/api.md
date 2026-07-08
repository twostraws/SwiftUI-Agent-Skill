# Using modern SwiftUI API

- Always use `foregroundStyle()` instead of `foregroundColor()`.
- Always use `clipShape(.rect(cornerRadius:))` instead of `cornerRadius()`.
- Always use the `Tab` API instead of `tabItem()`.
- Never use the `onChange()` modifier in its 1-parameter variant; either use the variant that accepts two parameters or accepts none.
- Do not use `GeometryReader` if a newer alternative works: `containerRelativeFrame()`, `visualEffect()`, or the `Layout` protocol. Flag `GeometryReader` usage and suggest the modern alternative.
- When designing haptic effects, prefer using `sensoryFeedback()` over older UIKit APIs such as `UIImpactFeedbackGenerator`.
- Use the `@Entry` macro to define custom `EnvironmentValues`, `FocusValues`, `Transaction`, and `ContainerValues` keys. This replaces the legacy pattern of manually creating a type conforming to (for example) `EnvironmentKey` with a `defaultValue`, then extending `EnvironmentValues` with a computed property.
- Strongly prefer `overlay(alignment:content:)` over the deprecated `overlay(_:alignment:)`. For example, use `.overlay { Text("Hello, world!") }` rather than `.overlay(Text("Hello, world!"))`.
- Never use `.navigationBarLeading` and `.navigationBarTrailing` for toolbar item placement; they are deprecated. The correct, modern placements are `.topBarLeading` and `.topBarTrailing`.
- Prefer to rely on automatic grammar agreement when dealing with English, French, German, Portuguese, Spanish, and Italian. For example, use `Text("^[\(people) person](inflect: true)")` to show a number of people.
- You can fill and stroke a shape with two chained modifiers; you do *not* need an overlay for the stroke. The overlay was required previously, but this is fixed in iOS 17 and later.
- When referencing images from an asset catalog, prefer the generated symbol asset API when the project is configured to use them: `Image(.avatar)` rather than `Image("avatar")`.
- For web content on iOS 18–25, wrap `WKWebView` in a `UIViewRepresentable`. On iOS 26+, a native SwiftUI `WebView` is available. To support both with a single call site, create a shared wrapper that branches on availability:

```swift
import SwiftUI
import UIKit
import WebKit

struct WebView: View {
    let url: URL

    var body: some View {
        if #available(iOS 26, *) {
            SwiftUI.WebView(url)
        } else {
            _LegacyWebView(url: url)
        }
    }
}

private struct _LegacyWebView: UIViewRepresentable {
    let url: URL

    func makeUIView(context: Context) -> WKWebView { WKWebView() }

    func updateUIView(_ webView: WKWebView, context: Context) {
        guard webView.url != url else { return }
        webView.load(URLRequest(url: url))
    }
}
```

Usage: `WebView(url: someURL)` — identical on iOS 18 and iOS 26. Make sure to include `import WebKit`.
- `ForEach` over an `enumerated()` sequence should not convert to an array first. Use `ForEach(items.enumerated(), id: \.element.id)` directly.
- When hiding scroll indicators, use `.scrollIndicators(.hidden)` rather than `showsIndicators: false` in the initializer.
- Never use `Text` concatenation with `+`.

For example, the usage of `+` here is bad and deprecated:

```swift
Text("Hello").foregroundStyle(.red)
+
Text("World").foregroundStyle(.blue)
```

Instead, use text interpolation like this:

```swift
let red = Text("Hello").foregroundStyle(.red)
let blue = Text("World").foregroundStyle(.blue)
Text("\(red)\(blue)")
```


## Using ObservableObject

If using `ObservableObject` is absolutely required – for example if you are trying to create a debouncer using a Combine publisher – you should always make sure `import Combine` is added. This was previously provided through SwiftUI, but that is no longer the case.
