class: dark middle

# Enterprise Web Development C&#35;
> Optional: Delegates & events

---
### Delegates & events
# Table of contents
- [Delegates](#delegates)
- [Events](#events)

---
name: delegates
class: dark middle

# Delegates & events
> Delegates

<small>When in doubt, mumble; when in trouble, delegate</small>

---
### Delegates & events
# Delegates

* Are reference types
* Holds a **reference to a method**
* **Declares signature** of the method: return type and parameters
  * Can only hold references to methods with an **exact match**
  * **Type-safe function pointer** (as in C++ for example) or a callback (JavaScript)
* Use the delegates `Action` or `Func<T>`
  * `Action` has no return type (`void`)
  * `Func<T>` can specify a return type

```cs
private void LogSomething()
{
    Console.WriteLine("Hello World");
}

Action action = LogSomething; // Pointer.

action(); // Invocation
action.Invoke(); // Or Invoke this way.
```

---
### Delegates
# Practical example

```cs
public class Button
{
    public string Text { get; set; }
*   public Action OnClicked { get; set; }
    public Button(string text, `Action onClicked`)
    {
        Text = text;
*       OnClicked = onClicked;
    }
    public void Click()
    {
        Console.WriteLine("Button clicked");
*       OnClicked?.Invoke(); // Watch out for null with '?'
    }
}
```

```cs
var button = new Button("Click me!",`LogSomething`);
void LogSomething()
{
   Console.WriteLine("Logging something after the button click");
}
// The caller has control `which` function is invoked, `not when`.
button.Click();
```


---
### `Action`
# Parameters
Passing parameters is possible by using type parameters in the declaration

1 Parameter
```cs
private void DoSomething(`int a`){
    Console.WriteLine(a);
}
Action<`int`> action = DoSomething;

action(`1`);
```

2 Parameters
```cs
private void DoSomething2(`int a`,` string b`){
    Console.WriteLine($"Param A:`{a}`, Param B:`{b}`");
}
Action<int,string> action2 = DoSomething2;

action2(`1`, `"Hello"`);
```

`N` amount of  parameters where X is a type and `N` <= 16:

Action&lt;x<sub>1</sub>,x<sub>2</sub>,x<sub>3</sub>x<sub>...</sub>,x<sub>n</sub>&gt;

---
### `Func<TResult>`
# Return Type
* `Action` cannot return anything, it always returns `void`.
* Use `Func<TResult>` when you need to return something.

```cs
private `string` ReturnSomething(){
    return "Something";
}
Func<`string`> action = ReturnSomething;

*string something = action();
Console.WriteLine(something); // Something
```

---
### `Func<TParameter,TResult>`
# TResult and a parameter

Add parameters, before the return type.
```cs
private string ReturnSomething2(`int a`){
    return $"Something, parameter a:{a}";
}

Func<`int`,string> action = ReturnSomething2;
// int is the parameter, string is the return type or TResult

string something = action(`1`);
Console.WriteLine(something); // Something, parameter a:1
```

---
### `Func<TParameter1,TParameter2,...,TResult>`
# TResult and multiple parameters
Func&lt;x<sub>1</sub>,x<sub>2</sub>,x<sub>3</sub>x<sub>...</sub>,x<sub>n</sub>,TResult&gt;
* `N` amount of  parameters where X is a type and `N` <= 15:
* `TResult` is always the last generic type 
  
```cs
private string ReturnSomething3(`int a, decimal b`){
    return $"Something, parameter a:{`a`}, parameter b:{`b`}";
}
Func<`int,decimal`,string> action = ReturnSomething3;

string something = action(`1`,`50M`);
Console.WriteLine(something); 
// Something, parameter a:1, parameter b:50
```

---
name: events
class: dark middle

# Delegates & events
> Events

---
### Delegates & events
# Events

* **Something that happened**
* **Inform others** about it
* Examples:
  * a new user was created
  * a product was added to a cart
  * some user changed something
  * someone scored a certain amount of points
  * ...
* Based on the **delegate model**
* Follows the [observer design pattern](https://refactoring.guru/design-patterns/observer).

---
### Events
# Observer Design Pattern

With this pattern you enable `subscribers` to register and receive notifications from a `publisher`. The event sender (= `publisher`) pushes a notification after an event occurred, the event receiver (= subscriber) receives it and does something with it.

<img src="https://refactoring.guru/images/patterns/diagrams/observer/solution2-en.png?id=fcea7791ac77b6ecb6fea2c2b4128d4a" class="center"/>

---
### Events
# Definition

Add the `event` keyword before the declaration of a `delegate`.

```cs
public class  Publisher 
{
  public `event` Action `OnSomethingChanged`; // `don't` use `get;set;`
  public void DoSomething()
  {// Other useful code.
    OnSomethingChanged?.Invoke(); // Emitting an event
  }
}
```

```cs
public class Subscriber
{
  private readonly Publisher _publisher;
  public Subscriber(Publisher publisher)
  {
    _publisher = publisher;
    _publisher.OnSomethingChanged `+=` ActOnSomething;
  }
  public void ActOnSomething()
  {
    Console.WriteLine("Act after event occurred");
  }
}
```

---
### Events
# Definition
Clean-up | unregister by implementing the `IDisposable` interface.

```cs
public class Subscriber `: IDisposable`
{
  private readonly Publisher _publisher;
  public Subscriber(Publisher publisher)
  {
    _publisher = publisher;
    _publisher.OnSomethingChanged `+=` ActOnSomething;
  }
* public void Dispose()
* {
*   _publisher.OnSomethingChanged `-=` ActOnSomething;
* }
  public void ActOnSomething()
  {
    Console.WriteLine("Act after event occurred");
  }
}
```

If you do not do this, you'll get memory leaks since the Garbage Collector cannot clean-up referenced objects
> TIP: Instantly implement `IDisposable` when registering.

---
### Events
# Event arguments

* Every event **can** have arguments, just like delegates

```cs
public class Publisher 
{
  public event Action<`int`> OnSomethingChanged;
  public void DoSomething()
  {
     OnSomethingChanged?.Invoke(`1`); // Emitting with parameter '1'
  }
}
```

```cs
public class Subscriber : IDisposable
{
  private readonly Pubslisher _publisher;
  public Subscriber(Publisher publisher)
  {
    _publisher = publisher
    publisher.OnSomethingChanged `+=` ActOnSomething;
  }
  public void ActOnSomething(`int a`)
  {
    Console.WriteLine($"Act after event with parameter a:{`a`}");
  }
  // ... Other methods and Dispose
}
```

---
### Events
# Custom event arguments

Example of custom event arguments
```cs
public class Publisher 
{
public event Action<`OnSomethingChangedEventArgs`> OnSomethingChanged;
public void DoSomething()
{
  // Insert useful code here
    OnSomethingChangedEventArgs args = new();
    args.Parameter1 = "Hello";
    OnSomethingChanged?.Invoke(this,args);
}
}
```

```cs
public class OnSomethingChangedEventArgs 
{
  public string Parameter1 {get;set;}
  public object Parameter2 {get;set;}
}
```

> Continued on next slide...

---
### Events
# Custom event arguments

Example of custom event arguments

```cs
public class Subscriber : IDisposable
{
  private readonly Pubslisher _publisher;
  public Subscriber(Publisher publisher)
  {
    _publisher = publisher
    publisher.OnSomethingChanged += ActOnSomething;
  }
  public void ActOnSomething(`OnSomethingChangedEventArgs args`)
  {
    Console.WriteLine($"Act after event with :{`args.Parameter1`}");
  }
  // ... Other methods and Dispose
}
```

---
### Events
# Naming conventions

Events
* Start with **On**SomethingChanged
* Ends with a past tense OnSomething**Changed**

CustomEventArgs
* Name of the class `OnSomethingChanged`**EventArgs**
  * Name of the event in combination with EventArgs

Examples:
* OnThresholdReached
* OnTransactionCreated
* OnCustomerChanged


* OnThresholdReachedEventArgs
* OnTransactionCreatedEventArgs
* OnCustomerChangedEventArgs

---
### Events
# Example

Use the events [notebook](https://github.com/HOGENT-Web/csharp/tree/main/chapters/03/notebooks/events.ipynb)

In the example you'll see how events can help to sent notifications to different components.

* 2 subscribers
  * `NotifierComponent`
  * `ListComponent`
* Publisher
  * `State`
* 1 activator which triggers the notification
  * `AddComponent`
