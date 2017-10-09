# `+>` for function composition

The statement:

```javascript
const doubleThenSquareThenHalf = value=>half(square(double(value)))
```

would be rewritable as:

```javascript
const doubleThenSquareThenHalf = double +> square +> half
```

If an async function is used as an operand, the expression would also evaluate to an async function:

```javascript
const doubleThenSquareThenHalfAsync = double +> squareAsync +> half
```

If a generator function is used as an operand, the expression would also evaluate to a generator function that pipes each yielded value of the supplied generator function to the subsequent functions:

```javascript
const randomBetween1And100Generator = randomBetween0And1Generator +> multiplyBy100
```

The expression evaluates to an async generator function if either or both the generator function or any of the other functions are async:

```javascript
const nextRouteAsyncGenerator = newLocationGenerator +> calculateRouteAsync
```

```javascript
const nextRouteAsyncGenerator = newLocationAsyncGenerator +> calculateRoute
```

It would be usable to tersely express the following:

```javascript
const switchOnEngineThenDrive = ()=>{switchOnEngine(); drive()}
```

as:

```javascript
const switchOnEngineThenDrive = switchOnEngine +> drive
```

Although it evaluates to `drive(switchOnEngine())`, it behaves the same as sequential execution for all intents and purposes, in cases of no-args functions.

As an analogy for how `x = x + y` is expressable as `x += y`, the following:

```javascript
x = x +> y
```

would be expressable as:

```javascript
x +>= y
```

e.g. for composing functions in a loop.

# Why `+>`?

To express accumulation via the `+` and function ordering via the `>`, and so as not to conflict with the pipeline-operator proposal here: https://github.com/tc39/proposal-pipeline-operator which has prior art from other languages. Discussion: https://github.com/tc39/proposal-pipeline-operator/issues/50
