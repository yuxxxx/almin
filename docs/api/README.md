# API Reference

<!-- 
    Don't manually update!
    API Reference is generated by documentation-wrapper
    see tools/update-api-reference.sh
-->

## Dispatcher class

### `Dispatcher`

Dispatcher is the **central** event bus system.

also have these method.

-   `onDispatch(function(payload){  });`
-   `dispatch(payload);`

Almost event pass the (on)dispatch.

#### FAQ

Q. Why use payload object instead emit(key, ...args).
A. It is for optimization and limitation.
If apply emit style, we cast ...args for passing other dispatcher at every time.

#### `dispatch(payload: DispatcherPayload)`

dispatch action object.
StoreGroups receive this action and reduce state.

**Parameters**

-   `payload`: **DispatcherPayload**

#### `onDispatch(payloadHandler): Function`

add onAction handler and return unbind function

**Parameters**

-   `payloadHandler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `pipe(toDispatcher: Dispatcher): Function`

delegate payload object to other dispatcher.

**Parameters**

-   `toDispatcher`: **Dispatcher**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `isDispatcher(v: (Dispatcher | Any)): boolean`

if {@link v} is instance of Dispatcher, return true

**Parameters**

-   `v`: **(Dispatcher | Any)**

Returns: **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**

### `DispatcherPayload`

payload The payload object that must have `type` property.

**Properties**

-   `type` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The event type to dispatch.

## Store class

### `StoreGroup`

StoreGroup is a **UI** parts of Store.
StoreGroup has event queue system.
It means that StoreGroup thin out change events of stores.
If you want to know all change events, and directly use `store.onChange()`.

#### `release()`

release all events handler.
You can call this when no more call event handler

### `constructor({ dispatcher, store })`

**Parameters**

-   `dispatcher`: **Dispatcher**
-   `store`: **(StoreGroup | Store)** - store is either Store or StoreGroup

### `getState(): Any`

return state value of StoreGroup.

Returns: **Any** - states object of stores

### `onChange(onChangeHandler: function (changingStores: Array<Store>)): Function`

if anyone store is changed, then call onChangeHandler

**Parameters**

-   `onChangeHandler`: **function (changingStores: [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Store>)**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - release handler function.

### `onDidExecuteEachUseCase(handler: function (useCase: UseCase))`

called the {@link handler} with useCase when the useCase is done.

**Parameters**

-   `handler`: **function (useCase: UseCase)**

### `onDispatch(handler): Function`

called the {@link handler} with user-defined payload object when a UseCase dispatch with payload.
This `onDispatch` is not called at built-in event. It is filtered by Context.
If you want to _All_ dispatched event and use listen directly your `dispatcher` object.
In other word, listen the dispatcher of `new Context({dispatcher})`.

**Parameters**

-   `handler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)**

### `onErrorDispatch(errorHandler: function (error: Error)): function (this: Dispatcher)`

called the {@link errorHandler} with error when error is occurred.

**Parameters**

-   `errorHandler`: **function (error: [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error))**

Returns: **function (this: Dispatcher)**

### `onWillExecuteEachUseCase(handler: function (useCase: UseCase, args: Any))`

called the {@link handler} with useCase when the useCase will do.

**Parameters**

-   `handler`: **function (useCase: UseCase, args: Any)**

### `release()`

release all events handler.
You can call this when no more call event handler

### `useCase(useCase: UseCase): UseCaseExecutor`

**Parameters**

-   `useCase`: **UseCase**

**Examples**

```javascript
context.useCase(UseCaseFactory.create()).execute(args);
```

Returns: **UseCaseExecutor**

### `defaultStoreName`

A UseCase `dispatch(payload)` and subscribers of the dispatcher are received the payload.

**Examples**

```javascript
abcUseCase
 .dispatch({
     type: "ABC",
     value: "value"
 })

abcStore
 .onDispatch(({ type, value }) => {
     console.log(type);  // "ABC"
     console.log(value); // 42
 });
```

### `Dispatcher`

Dispatcher is the **central** event bus system.

also have these method.

-   `onDispatch(function(payload){  });`
-   `dispatch(payload);`

Almost event pass the (on)dispatch.

#### FAQ

Q. Why use payload object instead emit(key, ...args).
A. It is for optimization and limitation.
If apply emit style, we cast ...args for passing other dispatcher at every time.

#### `dispatch(payload: DispatcherPayload)`

dispatch action object.
StoreGroups receive this action and reduce state.

**Parameters**

-   `payload`: **DispatcherPayload**

#### `onDispatch(payloadHandler): Function`

add onAction handler and return unbind function

**Parameters**

-   `payloadHandler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `pipe(toDispatcher: Dispatcher): Function`

delegate payload object to other dispatcher.

**Parameters**

-   `toDispatcher`: **Dispatcher**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `isDispatcher(v: (Dispatcher | Any)): boolean`

if {@link v} is instance of Dispatcher, return true

**Parameters**

-   `v`: **(Dispatcher | Any)**

Returns: **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**

### `DispatcherPayload`

payload The payload object that must have `type` property.

**Properties**

-   `type` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The event type to dispatch.

## StoreGroup class

### `StoreGroup`

StoreGroup is a **UI** parts of Store.
StoreGroup has event queue system.
It means that StoreGroup thin out change events of stores.
If you want to know all change events, and directly use `store.onChange()`.

#### `release()`

release all events handler.
You can call this when no more call event handler

### `constructor({ dispatcher, store })`

**Parameters**

-   `dispatcher`: **Dispatcher**
-   `store`: **(StoreGroup | Store)** - store is either Store or StoreGroup

### `getState(): Any`

return state value of StoreGroup.

Returns: **Any** - states object of stores

### `onChange(onChangeHandler: function (changingStores: Array<Store>)): Function`

if anyone store is changed, then call onChangeHandler

**Parameters**

-   `onChangeHandler`: **function (changingStores: [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Store>)**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - release handler function.

### `onDidExecuteEachUseCase(handler: function (useCase: UseCase))`

called the {@link handler} with useCase when the useCase is done.

**Parameters**

-   `handler`: **function (useCase: UseCase)**

### `onDispatch(handler): Function`

called the {@link handler} with user-defined payload object when a UseCase dispatch with payload.
This `onDispatch` is not called at built-in event. It is filtered by Context.
If you want to _All_ dispatched event and use listen directly your `dispatcher` object.
In other word, listen the dispatcher of `new Context({dispatcher})`.

**Parameters**

-   `handler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)**

### `onErrorDispatch(errorHandler: function (error: Error)): function (this: Dispatcher)`

called the {@link errorHandler} with error when error is occurred.

**Parameters**

-   `errorHandler`: **function (error: [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error))**

Returns: **function (this: Dispatcher)**

### `onWillExecuteEachUseCase(handler: function (useCase: UseCase, args: Any))`

called the {@link handler} with useCase when the useCase will do.

**Parameters**

-   `handler`: **function (useCase: UseCase, args: Any)**

### `release()`

release all events handler.
You can call this when no more call event handler

### `useCase(useCase: UseCase): UseCaseExecutor`

**Parameters**

-   `useCase`: **UseCase**

**Examples**

```javascript
context.useCase(UseCaseFactory.create()).execute(args);
```

Returns: **UseCaseExecutor**

### `defaultStoreName`

A UseCase `dispatch(payload)` and subscribers of the dispatcher are received the payload.

**Examples**

```javascript
abcUseCase
 .dispatch({
     type: "ABC",
     value: "value"
 })

abcStore
 .onDispatch(({ type, value }) => {
     console.log(type);  // "ABC"
     console.log(value); // 42
 });
```

### `Dispatcher`

Dispatcher is the **central** event bus system.

also have these method.

-   `onDispatch(function(payload){  });`
-   `dispatch(payload);`

Almost event pass the (on)dispatch.

#### FAQ

Q. Why use payload object instead emit(key, ...args).
A. It is for optimization and limitation.
If apply emit style, we cast ...args for passing other dispatcher at every time.

#### `dispatch(payload: DispatcherPayload)`

dispatch action object.
StoreGroups receive this action and reduce state.

**Parameters**

-   `payload`: **DispatcherPayload**

#### `onDispatch(payloadHandler): Function`

add onAction handler and return unbind function

**Parameters**

-   `payloadHandler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `pipe(toDispatcher: Dispatcher): Function`

delegate payload object to other dispatcher.

**Parameters**

-   `toDispatcher`: **Dispatcher**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `isDispatcher(v: (Dispatcher | Any)): boolean`

if {@link v} is instance of Dispatcher, return true

**Parameters**

-   `v`: **(Dispatcher | Any)**

Returns: **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**

### `DispatcherPayload`

payload The payload object that must have `type` property.

**Properties**

-   `type` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The event type to dispatch.

## Context class

### `StoreGroup`

StoreGroup is a **UI** parts of Store.
StoreGroup has event queue system.
It means that StoreGroup thin out change events of stores.
If you want to know all change events, and directly use `store.onChange()`.

#### `release()`

release all events handler.
You can call this when no more call event handler

### `constructor({ dispatcher, store })`

**Parameters**

-   `dispatcher`: **Dispatcher**
-   `store`: **(StoreGroup | Store)** - store is either Store or StoreGroup

### `getState(): Any`

return state value of StoreGroup.

Returns: **Any** - states object of stores

### `onChange(onChangeHandler: function (changingStores: Array<Store>)): Function`

if anyone store is changed, then call onChangeHandler

**Parameters**

-   `onChangeHandler`: **function (changingStores: [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Store>)**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - release handler function.

### `onDidExecuteEachUseCase(handler: function (useCase: UseCase))`

called the {@link handler} with useCase when the useCase is done.

**Parameters**

-   `handler`: **function (useCase: UseCase)**

### `onDispatch(handler): Function`

called the {@link handler} with user-defined payload object when a UseCase dispatch with payload.
This `onDispatch` is not called at built-in event. It is filtered by Context.
If you want to _All_ dispatched event and use listen directly your `dispatcher` object.
In other word, listen the dispatcher of `new Context({dispatcher})`.

**Parameters**

-   `handler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)**

### `onErrorDispatch(errorHandler: function (error: Error)): function (this: Dispatcher)`

called the {@link errorHandler} with error when error is occurred.

**Parameters**

-   `errorHandler`: **function (error: [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error))**

Returns: **function (this: Dispatcher)**

### `onWillExecuteEachUseCase(handler: function (useCase: UseCase, args: Any))`

called the {@link handler} with useCase when the useCase will do.

**Parameters**

-   `handler`: **function (useCase: UseCase, args: Any)**

### `release()`

release all events handler.
You can call this when no more call event handler

### `useCase(useCase: UseCase): UseCaseExecutor`

**Parameters**

-   `useCase`: **UseCase**

**Examples**

```javascript
context.useCase(UseCaseFactory.create()).execute(args);
```

Returns: **UseCaseExecutor**

### `defaultStoreName`

A UseCase `dispatch(payload)` and subscribers of the dispatcher are received the payload.

**Examples**

```javascript
abcUseCase
 .dispatch({
     type: "ABC",
     value: "value"
 })

abcStore
 .onDispatch(({ type, value }) => {
     console.log(type);  // "ABC"
     console.log(value); // 42
 });
```

### `Dispatcher`

Dispatcher is the **central** event bus system.

also have these method.

-   `onDispatch(function(payload){  });`
-   `dispatch(payload);`

Almost event pass the (on)dispatch.

#### FAQ

Q. Why use payload object instead emit(key, ...args).
A. It is for optimization and limitation.
If apply emit style, we cast ...args for passing other dispatcher at every time.

#### `dispatch(payload: DispatcherPayload)`

dispatch action object.
StoreGroups receive this action and reduce state.

**Parameters**

-   `payload`: **DispatcherPayload**

#### `onDispatch(payloadHandler): Function`

add onAction handler and return unbind function

**Parameters**

-   `payloadHandler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `pipe(toDispatcher: Dispatcher): Function`

delegate payload object to other dispatcher.

**Parameters**

-   `toDispatcher`: **Dispatcher**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `isDispatcher(v: (Dispatcher | Any)): boolean`

if {@link v} is instance of Dispatcher, return true

**Parameters**

-   `v`: **(Dispatcher | Any)**

Returns: **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**

### `DispatcherPayload`

payload The payload object that must have `type` property.

**Properties**

-   `type` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The event type to dispatch.

## UseCase class

### `StoreGroup`

StoreGroup is a **UI** parts of Store.
StoreGroup has event queue system.
It means that StoreGroup thin out change events of stores.
If you want to know all change events, and directly use `store.onChange()`.

#### `release()`

release all events handler.
You can call this when no more call event handler

### `constructor({ dispatcher, store })`

**Parameters**

-   `dispatcher`: **Dispatcher**
-   `store`: **(StoreGroup | Store)** - store is either Store or StoreGroup

### `getState(): Any`

return state value of StoreGroup.

Returns: **Any** - states object of stores

### `onChange(onChangeHandler: function (changingStores: Array<Store>)): Function`

if anyone store is changed, then call onChangeHandler

**Parameters**

-   `onChangeHandler`: **function (changingStores: [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Store>)**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - release handler function.

### `onDidExecuteEachUseCase(handler: function (useCase: UseCase))`

called the {@link handler} with useCase when the useCase is done.

**Parameters**

-   `handler`: **function (useCase: UseCase)**

### `onDispatch(handler): Function`

called the {@link handler} with user-defined payload object when a UseCase dispatch with payload.
This `onDispatch` is not called at built-in event. It is filtered by Context.
If you want to _All_ dispatched event and use listen directly your `dispatcher` object.
In other word, listen the dispatcher of `new Context({dispatcher})`.

**Parameters**

-   `handler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)**

### `onErrorDispatch(errorHandler: function (error: Error)): function (this: Dispatcher)`

called the {@link errorHandler} with error when error is occurred.

**Parameters**

-   `errorHandler`: **function (error: [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error))**

Returns: **function (this: Dispatcher)**

### `onWillExecuteEachUseCase(handler: function (useCase: UseCase, args: Any))`

called the {@link handler} with useCase when the useCase will do.

**Parameters**

-   `handler`: **function (useCase: UseCase, args: Any)**

### `release()`

release all events handler.
You can call this when no more call event handler

### `useCase(useCase: UseCase): UseCaseExecutor`

**Parameters**

-   `useCase`: **UseCase**

**Examples**

```javascript
context.useCase(UseCaseFactory.create()).execute(args);
```

Returns: **UseCaseExecutor**

### `defaultStoreName`

A UseCase `dispatch(payload)` and subscribers of the dispatcher are received the payload.

**Examples**

```javascript
abcUseCase
 .dispatch({
     type: "ABC",
     value: "value"
 })

abcStore
 .onDispatch(({ type, value }) => {
     console.log(type);  // "ABC"
     console.log(value); // 42
 });
```

### `Dispatcher`

Dispatcher is the **central** event bus system.

also have these method.

-   `onDispatch(function(payload){  });`
-   `dispatch(payload);`

Almost event pass the (on)dispatch.

#### FAQ

Q. Why use payload object instead emit(key, ...args).
A. It is for optimization and limitation.
If apply emit style, we cast ...args for passing other dispatcher at every time.

#### `dispatch(payload: DispatcherPayload)`

dispatch action object.
StoreGroups receive this action and reduce state.

**Parameters**

-   `payload`: **DispatcherPayload**

#### `onDispatch(payloadHandler): Function`

add onAction handler and return unbind function

**Parameters**

-   `payloadHandler`

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `pipe(toDispatcher: Dispatcher): Function`

delegate payload object to other dispatcher.

**Parameters**

-   `toDispatcher`: **Dispatcher**

Returns: **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** - call the function and release handler

#### `isDispatcher(v: (Dispatcher | Any)): boolean`

if {@link v} is instance of Dispatcher, return true

**Parameters**

-   `v`: **(Dispatcher | Any)**

Returns: **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**

### `DispatcherPayload`

payload The payload object that must have `type` property.

**Properties**

-   `type` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The event type to dispatch.