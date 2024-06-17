

### In summary:

`@State`: Internal state for a view.
`@Binding`: Allows child views to read and write state from a parent view.
`@ObservedObject`: Observes changes to an external object.
`@StateObject`: Owns an observable object for the lifetime of the view.
`@Environment`: Reads environment values.
`@EnvironmentObject`: Accesses an observable object provided by an ancestor view.
`@Published`: Marks properties in an observable object to trigger updates when they change.
\
\
##### @State
maange state within a single view.
##### @Binding
creates a two way binging to a state owned by a parent view
```
struct ParentView: View {
    @State private var isOn = false

    var body: some View {
        ChildView(isOn: $isOn)
    }
}

struct ChildView: View {
    @Binding var isOn: Bool

    var body: some View {
        Toggle("Switch", isOn: $isOn)
    }
}
```
\
##### @StateObject
Used to create an instance of an observable object that SwiftUI owns and manages the lifetime. Need to initialize within the view.
```
class Settings: ObservableObject {
    @Published var isOn = false
}

struct ContentView: View {
    @StateObject private var settings = Settings() // StateObject initializes and retains the object

    var body: some View {
        Toggle("Switch", isOn: $settings.isOn)
    }
}

```
\
##### @ObservableObject
Observe an object: ObservableObject without retaining.
##### @Published
Mark property to publish event if it updates.
```
class Settings: ObservableObject {
    @Published var isOn = false
}

struct ContentView: View {
    @ObservedObject var settings = Settings()

    var body: some View {
        Toggle("Switch", isOn: $settings.isOn)
    }
}
```
```
class Settings: ObservableObject {
    @Published var isOn = false
}

struct ParentView: View {
    @StateObject private var settings = Settings() // Parent view creates and owns the object

    var body: some View {
        ChildView(settings: settings) // Pass the object to the child view
    }
}

struct ChildView: View {
    @ObservedObject var settings: Settings // Child view observes the object

    var body: some View {
        Toggle("Switch", isOn: $settings.isOn)
    }
}

```
\
##### @Environment
To read a value from the environment.
```
struct ContentView: View {
    @Environment(\.colorScheme) var colorScheme

    var body: some View {
        Text(colorScheme == .dark ? "Dark Mode" : "Light Mode")
    }
}

```
\
##### @EnvironmentObject
To reas and write to an object: ObservableObject shared in the environment.
```
class Settings: ObservableObject {
    @Published var isOn = false
}

struct ParentView: View {
    @StateObject private var settings = Settings()

    var body: some View {
        ChildView().environmentObject(settings)
    }
}

struct ChildView: View {
    @EnvironmentObject var settings: Settings

    var body: some View {
        Toggle("Switch", isOn: $settings.isOn)
    }
}

```


---

I want to make a new property owned by the current view. You should use @State for value types, and @StateObject for reference types.

I want to refer to a value created elsewhere. You should use @Binding for value types, and either @ObservedObject or @EnvironmentObject for reference types