---
layout: post
title:  "An Ode to Try Except Else"
date:   2022-10-18 +0000
---

Python has the ability to add an `else` clause during error handling. It allows you to not have to use a return statement in the catch block so it can look neater and convey your meaning more

For instance, I wanted to login and redirect to home I wrote this.

```python
def handleRegister():
    try:
        await Account.register(username, password)
        Redirects.goto(Redirects.home())
    except Exception as e:
        HandleAccountError(err)
```

However, if an error occurred during the redirect, then it would processed in the error handling and that's not my intention.
To prevent that I could move it out of the `try` statement.

```javascript
function handleRegister(){
    try {
        await Account.register(username, password);
    } catch (err) {
        HandleAccountError(err);
        return;
    }
    Redirects.goto(Redirects.home());
}
```

However, this feels much messier and disorganised compare to the original. By making use of the `try`, `catch`, `else` you can get a semantically equivalent and neater solution

```javascript
function handleRegister(){
    try {
        await Account.register(username, password);
    } catch (err) {
        HandleAccountError(err);
    } else {
        Redirects.goto(Redirects.home());
    }
}
```
