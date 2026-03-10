Ah, generics in Swift! A splendid choice of topic. Picture, if you will, a versatile tool that allows you to write flexible and reusable functions, structures, and classes. Generics in Swift permit you to write code that avoids duplication while maintaining type safety and clarity.

In essence, generics enable you to define placeholders for types in your code. These placeholders can then be replaced with actual types when you use the code. This allows you to write functions, structures, and classes that can work with any type, rather than being tied to a specific one. The type being used is determined dynamically at runtime

The syntax of Generics may look strange, using angled brackets. But remember, explicit types are often expressed using `<>`.

**Heed these words:** Generics cannot be directly used with protocols, for that, you must utilize *associated types*.

### Ex. 1:
This is a real world example you might use on the job.

**Implementation**
```
struct User: Decodable {
    let id: Int
    let name: String
}
```

```
func fetch<T: Decodable>(url: URL) async throws -> T {
    let (data, _) = try await URLSession.shared.data(from: url)
    
    let decoded = try JSONDecoder().decode(T.self, from: data)
    
    return decoded
}
```

**Usage**
```
let url = URL(string: "https://api.example.com/user")!

let user: User = try await fetch(url: url)

print(user.name)
```

**Breakdown**:
- We want to do a fetch, it does not matter what the type is, it is the job of the implementing class to determine the type.
- We do a `URLSession.shared.data()` call to pull the raw data from the url and store it in a compound type called a touple.
- We decode using `JSONDecoder().decode()` and tell it to use whatever type is instructed by the implementing class.
- We return this decoded data
- When we finally want to use this function, swift uses type inference to tell we want to return a type of `User` at runtime and "fills in the blanks" so to speak.