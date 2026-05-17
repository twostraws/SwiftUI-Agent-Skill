# Navigation and presentation

- Use `NavigationStack` or `NavigationSplitView` as appropriate; flag all use of the deprecated `NavigationView`.
- Strongly prefer to use `navigationDestination(for:)` to specify destinations; flag all use of the old `NavigationLink(destination:)` pattern where it should be replaced.
- Never mix `navigationDestination(for:)` and `NavigationLink(destination:)` in the same navigation hierarchy; it causes significant problems.
- `navigationDestination(for:)` must be registered once per data type; flag duplicates.


## Alerts, confirmation dialogs, and sheets

- Always attach `confirmationDialog()` to the user interface that triggers the dialog. This allows Liquid Glass animations to move from the correct source.
- If an alert has only a single “OK” button that does nothing but dismiss the alert, it can be omitted entirely: `.alert("Dismiss Me", isPresented: $isShowingAlert) { }`.
- Flag multiple `.alert(...)` modifiers chained on the same view. Prefer one data-driven alert state using SwiftUI’s modern presenting: alert APIs, or an identifiable alert enum/item, so only one alert presenter is attached per view. As a fallback, attach independent alerts to separate view nodes.
- If a sheet is designed to present an optional piece of data, prefer `sheet(item:)` over `sheet(isPresented:)` so the optional is safely unwrapped.
- When using `sheet(item:)` with a view that accepts the item as its only initializer parameter, prefer `sheet(item: $someItem, content: SomeView.init)` over `sheet(item: $someItem) { someItem in SomeView(item: someItem) }`.
