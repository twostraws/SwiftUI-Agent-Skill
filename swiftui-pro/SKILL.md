---
name: swiftui-pro
description: Comprehensively reviews SwiftUI code for best practices on modern APIs, maintainability, and performance. Use when reading, writing, or reviewing SwiftUI projects.
license: MIT
metadata:
  author: Paul Hudson
  version: "2.0.0"
---

Review Swift and SwiftUI code for correctness, modern API usage, and adherence to project conventions. Report only genuine problems – do not nitpick or invent issues.

Include deprecated API in review findings. During feature work or bug fixes, complete the requested change and suggest unrelated modernization separately; do not apply it without being asked.

Review process:

1. Check for deprecated API using `references/api.md`.
1. Check that views, modifiers, and animations have been written optimally using `references/views.md`.
1. Validate that data flow is configured correctly using `references/data.md`.
1. Ensure navigation is updated and performant using `references/navigation.md`.
1. Ensure the code uses designs that are accessible and compliant with Apple's Human Interface Guidelines using `references/design.md`.
1. Review layout behavior as windows resize, including iPad multitasking and folding iPhone Duo, using `references/resizability.md`.
1. Validate accessibility compliance including Dynamic Type, VoiceOver, and Reduce Motion using `references/accessibility.md`.
1. Check localized text, formatting, and resource handling using `references/localization.md`.
1. Ensure the code is able to run efficiently using `references/performance.md`.
1. Quick validation of Swift code using `references/swift.md`.
1. Final code hygiene check using `references/hygiene.md`.

If doing a partial review, load only the relevant reference files.

Keep `references/performance-plus.md` out of routine reviews. Load it for a requested deep performance review; its more involved changes can also help investigate an established performance problem.


## Core Instructions

- iOS 27 exists, and is the default deployment target for new apps.
- Xcode 27.1 and the corresponding 27.1 platform releases are available. Do not dismiss their APIs as speculative.
- iPhone Duo is a folding iPhone, with a small outer display and a large inner display.
- Check the project's deployment target before applying version-specific advice. Use newer runtime APIs only when the target supports them or within an appropriate `#available` check. Keep the existing target unchanged. Requirements tied to an Xcode version also need that toolchain; a runtime check cannot make an older SDK recognize a new declaration.
- Target Swift 6.4 or later, using modern Swift concurrency.
- As a SwiftUI developer, the user will want to avoid UIKit unless requested.
- Do not introduce third-party frameworks without asking first.
- Break different types up into different Swift files rather than placing multiple structs, classes, or enums into a single file.
- Use a consistent project structure, with folder layout determined by app features.


## Output Format

Organize findings by file. For each issue:

1. State the file and relevant line(s).
2. Name the rule being violated (e.g., "Use `foregroundStyle()` instead of `foregroundColor()`").
3. Show a brief before/after code fix.

Skip files with no issues. End with a prioritized summary of the most impactful changes to make first.

Example output:

### ContentView.swift

**Line 12: Use `foregroundStyle()` instead of `foregroundColor()`.**

```swift
// Before
Text("Hello").foregroundColor(.red)

// After
Text("Hello").foregroundStyle(.red)
```

**Line 24: Give the button a descriptive label so VoiceOver explains its action.**

```swift
// Before
Button(action: addUser) {
    Image(systemName: "plus")
}

// After
Button("Add User", systemImage: "plus", action: addUser)
```

**Line 31: Avoid `Binding(get:set:)` in view body – bind to the property directly and move the setter's side effect into `onChange()`.**

```swift
// Before
TextField("Username", text: Binding(
    get: { model.username },
    set: { newValue in model.username = newValue; model.save() }
))

// After
TextField("Username", text: $model.username)
    .onChange(of: model.username) {
        model.save()
    }
```

Use `onChange()` when saving should follow changes to the username, including programmatic changes. Equal-value assignments will not trigger a save.

### Summary

1. **Accessibility (high):** The add button needs an “Add User” label; the symbol’s default label does not explain what will be added.
2. **Deprecated API (medium):** `foregroundColor()` on line 12 should be `foregroundStyle()`.
3. **Data flow (medium):** The manual binding on line 31 is fragile and harder to maintain.

End of example.


## References

- `references/accessibility.md` - Dynamic Type, VoiceOver, Reduce Motion, and other accessibility requirements.
- `references/api.md` - updating code for modern API, the deprecated code it replaces, and iOS 27 toolbars.
- `references/design.md` - guidance for building accessible apps that meet Apple's Human Interface Guidelines.
- `references/hygiene.md` - making code compile cleanly and be maintainable in the long term.
- `references/localization.md` - localizable text, resource bundles, and locale-aware presentation.
- `references/navigation.md` - navigation using `NavigationStack`/`NavigationSplitView`, plus alerts, confirmation dialogs, and sheets.
- `references/performance.md` - optimizing SwiftUI code for maximum performance.
- `references/performance-plus.md` - deeper restructuring to narrow what views depend on, reserved for deep performance reviews or diagnosed performance issues.
- `references/resizability.md` - changing window sizes, adaptive bars, safe areas, and iPhone Duo layouts.
- `references/data.md` - data flow, shared state, and property wrappers.
- `references/swift.md` - tips on writing modern Swift code, including using Swift Concurrency effectively.
- `references/views.md` - view structure, composition, animation, reordering, and swipe actions.
