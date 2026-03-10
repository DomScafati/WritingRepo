SwiftUI utilized the dark magics known as result builders to create intuitive UI for bother end-user. In fact, imagine result builders like building blocks of a fortress. Instead of building your spires whole, you give instructions to your minions such as:

```
addTower()
addGate()
if hasMote {
	addBridge()
}
```

Now your thralls collect all those parts and assembles them into your castle. The result builder is the ultimate slave of ui building, taking multiple lines of code and compiling them into a single value behind-the-scenes.


### Why do we need this?
Swift normally wants every function to return one thing, like a number, a string, or a view. However, frameworks like SwiftUI lets us write multiple statements inside of closures like so:

```
var body: some View {
	VStack {
		Text("Hello")
		
		if showSubtitle {
			Text("Subtitle")
		}
	
		Button("Tap Me", action: doSomething)
	}
}
```

This is, of course, only possible because `VStack` is using a result builder (`@ViewBuilder`) and it is compiling our instructions into a single output.

### Custom View Builders

Here we will build our own Domain Specific Language (DSL) 

**Step 1**: Builder Definition
```
@resultBuilder
struct StringBuilder {
    static func buildBlock(_ components: String...) -> String {
        components.joined(separator: " ")
    }
}
```

**Step 2**: Use it in a Function
```
func makeSentence(@StringBuilder _ content: () -> String) -> String {
    content()
}
```

**Step 3:** Evoke the View Builder
This is true power. Write separate lines and Swift does your bidding!
```
let sentence = makeSentence {
    "Thank you,"
    "Dark Lord"
    "for your malicious kingdom"
}

print(sentence) // "Thank you Dark Lord for your malicious kingdom"
```


### Behind the Scenes
When you call:
```
makeSentence {
	"6"
	"6"
	"6"
}
```

Swift translates this to:
```
StringBuilder.buildBlock("6", "6", "6")
```


### Using If/Else


### Questions from the Damned

Q: What does the syntax `String...` mean? why is it used int he definition of `buildBlock`? 

A: This is simply `resultBuilder`'s way of saying `[String]`. It is uncommon, and most coding standards restrict this to result builder contexts only.