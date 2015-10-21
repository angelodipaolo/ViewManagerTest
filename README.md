# ViewManagerTest

This project demonstrates an issue with requiring native components in React Native. React Native fails to find a native compontent that subclasses `RCTViewManager` if the subclass's name ends with `Manager`. 

### Example

Define a `RCTViewManager` subclass that ends with `Manager` in the name.

```
@interface FooViewManager : RCTViewManager
@end

@implementation FooViewManager

RCT_EXPORT_MODULE()

@end

```

Attempt to require it in react using the fully-qualified name:

```
var FooViewManager = React.requireNativeComponent('FooViewManager', null);

```

You get an error in the console:

```
'Warning: Native component for "FooViewManager" does not exist'
```

The component is found if you use a subset of the name when requiring it.

```
var FooViewManager = React.requireNativeComponent('FooView', null);

```


This only seems to affect subclasses of `RCTViewManager` that end with `Manager` in the name.
