---
title: "Redux Saga: Managing Side Effects the Right Way"
description: "A deep dive into generator-based middleware for predictable async flows in React apps."
tags: [JavaScript]
---

Managing async logic in React apps has always been messy. Callbacks lead to deeply nested code. Promises help, but complex orchestration — retrying failed requests, cancelling in-flight calls, racing multiple effects — quickly becomes hard to read and test. Redux Saga cuts through this with a different primitive: generator functions.

## What is Redux Saga?

Redux Saga is a Redux middleware that models side effects (API calls, timers, browser events) as a stream of actions. Instead of dispatching a thunk that fires off a promise, you write *saga* functions using `function*` generators. The saga middleware intercepts specific action types and runs your generator in response.

```js
import { call, put, takeLatest } from 'redux-saga/effects';
import { fetchUserSuccess, fetchUserFailure } from './actions';
import api from './api';

function* fetchUser(action) {
  try {
    const user = yield call(api.getUser, action.payload.id);
    yield put(fetchUserSuccess(user));
  } catch (err) {
    yield put(fetchUserFailure(err.message));
  }
}

export function* watchFetchUser() {
  yield takeLatest('FETCH_USER_REQUEST', fetchUser);
}
```

The `yield call(...)` expression suspends the generator until the Promise resolves — but crucially, the middleware handles the async mechanics. Your generator stays synchronous-looking and easy to step through in a debugger.

## Why generators?

The key insight is that generators are *pauseable*. Unlike async/await (which is also pauseable), generators give the middleware full control over *when* to resume. This makes effects like `takeLatest` (cancel any previous in-flight saga if a new action arrives) trivial to implement, and nearly impossible to achieve cleanly with promises alone.

## Testing becomes trivial

Because `yield call(api.getUser, id)` only produces a plain description of the call — it doesn't execute it — your tests never need to mock the network:

```js
import { call, put } from 'redux-saga/effects';
import { fetchUser } from './sagas';

test('fetchUser saga', () => {
  const gen = fetchUser({ payload: { id: 42 } });

  expect(gen.next().value).toEqual(call(api.getUser, 42));
  expect(gen.next({ name: 'Kawi' }).value).toEqual(put(fetchUserSuccess({ name: 'Kawi' })));
});
```

No mocks. No async test setup. Just plain equality assertions on the yielded values.

## When to use it

Redux Saga shines when your async logic involves:

- **Sequencing** — do A, then B, then C, roll back if C fails
- **Cancellation** — abort an in-flight request when the user navigates away
- **Racing** — take whichever of two requests resolves first
- **Polling** — repeat a request on an interval until a condition is met

For simple fire-and-forget API calls, a thunk or even inline `useEffect` is often enough. Reach for sagas when the orchestration itself is the hard part.

## Further reading

- [Official Redux Saga docs](https://redux-saga.js.org)
- My conference slides: [Redux Saga: Practical Introduction](/slides/redux-saga-practical-intro/)
