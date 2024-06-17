Navigation Controllers in Swift UI

### NavigationStack
For single column.
```
NavigationStack {
  List(parks) { park in
    NavigationLink(park.name, value: park)
  }
  .navigationDestination(for: Park.self) { park in
    ParkView(park)
  }
}
```

Make NavigationStack.
To make a NavigationLink:
  - add view modifer .navigationDestination(for:destination:) which associates the view with a data type
  - In the view add NavigationLink passing instance of same data type
___

Manage navigation state using a state to track the paths or more advances NavigationPath
```
@State private var presentedParks: [Parks] = []
```
___

Navigate to different view types by adding multiple .navigationDestination(for:destination:) for each data type.
___
```
// associate data to a destination view
navigationDestination(for data:, destination: )

navigationDestination<D, C>( 
  for data: D.type,
  @ViewBuilder destination: @Escaping (D) -> C
) -> some View where D: Hashable, C: View

// Associate destination view with binding in order to push on top.
// e.g. press button push view.
navigationDestination(isPresented:destination:)

```
___
Do not put a navigation destination modifier inside a “lazy” container, like List or LazyVStack!!

These containers create child views only when needed to render on screen. Add the navigation destination modifier outside these containers so that the navigation stack can always see the destination.

### NavigationSplitView
For 2-3 columns.



`NavigationStack` and `NavigationSplitView` instances to replace `NavigationView` in iOS 16+.
