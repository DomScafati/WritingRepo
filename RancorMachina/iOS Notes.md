# Overview
- Had a meeting with Oge (Oh-Gee), and he said that it is, in fact, a modified TCA  they call Reactive Store
- These are notes explaining the unique architecture, typically in high-level terms or UIKit
- This architecture exists to **keep ViewControllers stupid** by moving:
	- **“what to show”** into a _Presenter_
	- **“what the user did”** into an _Interpreter_
	- **“what that means”** into a _Store_

Everything else is plumbing.
## Store Components:
- Central source of globabl State in the feature. 
- Actions represent an intent to update the state or otherwise do something with it. Methods in enum value form. These do not directly execute actions, they are sent to the store for processing. This is called dispatching.
- Store comprised of Reducer, ActionCreator and Middleware
## Reducer:
- Reducers have the signature: func reduce(into state: inout State, _ action: Action) -> SideEffect?
- core of business logic.
- they modify the current state given an action. The only component capable of modifying state.
-  Reducers can produce a SideEffect which is in turn processed by the Wireframe.
- SideEffect is any work that is difficult to test or represent in state like transitions, http and User Defaults writing.
- best to start with a single reducer that contains everything, but as your feature grows, may want to split into smaller reducers that get composed into your main reducer.
## ActionCreator
- One of the. only objects that can produce immediate feedaback by sending actions back into the store.
- Beause the actions it produces can be made asynchronous using Publishers, the AC is often used to execute API calls.
- AC is executed before the reducer which means it receives the old or current state and the action.
- if you need to do asynchronous work after the reducer runs, you can do that i the Wireframe by having the reducer return a SideEffect.
## Middleware
- two entry-point methods:
	- these methods are executed first and last in the store sprocessing pipeline.  they don't return anything, so they don't provide feedback into the store.
	- middleware is most often used for fire-and-forget stle hooks into particular events. sending analytics calls or producing logs are two common use-cases.

# Driving a Screen
- "Screen" will refer to the combination of a UIViewController and its Presenter and Interpreter.
- presenter and interpreter together fill the roll of a ViewModel from the MVVM architecture
- They exist to pull business logic out of the ViewController so that it is easier to test in isolation.
- In ReactiveStore Architecture,  both components are composed of Combine publishers along with mapping and filtering functions which apply that business logic.
- A presenter is initialized with a publisher of StoreState which gets mapped into many publisher properties.
- an interpreter is given many PassthroughSubject properties which it combines into a single publisher of StoreAction
- Interpreters and presenters exist to pull business logic out of ViewController into more focused, testable components. Together these form a Screen.
- Publishers facilitate communication between the Store and a Screen. Communication always occurs in the same direction forming an event loop.
	- ViewController -> UserInputs & View Events -> Interpreter -> Actions -> Store -> New State -> Presenter -> UIBindings -> ViewController
## Presenters
- The State kept in the Store is often global to the entire feature and structured in a way that is optimized for business logic, not rendering.
- If a value can be assigned directly to a UIKit property (`label.text`, `button.isEnabled`, `view.isHidden`, `imageView.image`), it belongs as a Presenter publisher.
- The job of a Presenter is to transform that state into something more appropriate for a UIView.  These will be UI bindings.
- These bindings are publisher properties. The values produced by these publishers  should be primitive things which can be directly assigned to view properties. This means Bools for controlling isHidden or AttributedStrings for assigning labels, or UIColors or setting background colors.
- The reason for primitive types like this is. because it can make testing easier. if we can make out ViewCotnrollers as dumb as possible, it will just assign these publisher properties to the appropriate places. 
- ex:
  ```
  publich protocol PresenterProtocol {
	  associatedtype State: StoreState
	  
	  init(state: AnyPublisher<State, Never>, environment: PluginEnvirionment)
  }
  ```
## Interpreters
- Views typically don't just present things to the user, the also offer ways to interact with what is on screen. 
- These are responsible for user interaction on a VC. 
- These also want VCs to be dumb as possible so we can ignore it in testing.
- Interpreters use PassthroughSubjects for every distinct event  that can happen.
- Transforms this primitive view events into distinct actions which  the Store processes in turn.
- The ViewController does nothing more than connect these view event subjects into their appropriate control or otherwise send events at the appropriate times.
- A primitive view event could be user interaction like button taps or text input but also include UIKit lifecycle events and delegate methods.
- ex:
  ```
  public protocol InterpreterProtocol {
	  associatedtype Action: StoreAction
	  
	  init(environment: PluginEnvironment)
	  
	  var actions: AnyPublisher<Action, Never> { get }
  }
  ```

## ViewControllers
- The only things about VC's that are really different in the Reactive Store architecture is that they almost never preserve any state and their methods are as simple as possible. 
- All state management is handled by the store and is mediated through the Presenter and Interpreter. This means the VCs just need to worry about basic UI logic.
- VCs are also responsible for retaining their presenter and interpreter. Without a strong reference, they may b=get deallocated which could cause your features to fail. For the same reason, the VC should also have a strong reference to the store. If you use a ViewContext, this aspect handled for you.
- If the VC does have its  own direct reference to the store, it should not directly call srore.dispatch() or store.state().

## ViewContext
- A context is an important element in controlling the complexity of ViewControllers. It provides a unified interface to the interpreter and Presenter as well as memory management.
- ViewContext will strongly retain the Store its connected to. so your VCs don't need a direct reference to the Store itself.
- ViewContext unifies the interpreter and Presented with a declarative, keypath-based API for binding UI elements to their corresponding publisher or subject.
- ViewContext also has its own set of cancelables so it can manage the subscription lifetimes fore you. This makes most UI setup one or two lines per UI element.
	- ViewController -> User Inputs & View Events -> ViewContext Interpreter -> Actions -> Store -> NewState -> ViewContext Presenter -> UIBindings -> ViewController

# The final mental model 

- **ViewController** → _Connect the wires_
- **ViewContext** → _Make wiring tolerable_
- **Presenter** → _What should be shown_
- **Interpreter** → _What the user did_
- **Store** → _What that means_


ViewController
  ↕ (only talks to)
ViewContext
  ↕
Presenter / Interpreter
  ↕
Store
