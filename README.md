# Optionals in Python

> Adding optional variables in Python. It allows you to do `user.profile.username` and don't care about what will happen if `user` or `user.profile` is `None`. It looks similar to what you can do in `Swift` when you write this code `user?.profile?.username`.

### How to install

```
pip install optionals
```

### How to use Optionals

Main idea here is to use meta programming in Python under the hood. Yes, Python doesn't allow to create a `private` properties and methods. But we can emulate them, by catching each access to the property or a function call and decide, what we need to do - allow access to it or reject.

In the **Swift** and some other modern languages it's an idea of `optional` value. It allows to *unpack* value and do something.

Imagine that you have next code:

```python
def get_username(user):
  if user and user.profile and user.profile.username:
    return user.profile.username
  return None
```

It's very often situation. It means that you need to write this *a little bit ugly* code only to check that property exists.
Imagine that we can do this with idea of optional, when each property return not the value itself, but some `Optional` objct that we can unpack then.

```python
def get_username(user):
  return user.profile.username
```

In this case, if `user` or `user.profile` is empty, then all next calls will be *ignored* and an empty `Optional` will be returned. In other words - we will have a `None` in the end. But because we can't call anything on the `None` value, the `Optional` value allows us to solve the problem of the resolving a chain of calls.

The `Optional` can be converted to string or integer, or any other supported type. But it also can be checked on it's state - if it's set or unset:

```
username = user.profile.username
if username:
  print('Hello {username}')
else:
  print('Hello guest')
```

As we can see - the username is checked automatically on *boolean* value, we don't need to get the actual value from the `Optional`. But sometimes it may be mandatory to get exact value from the `Optional` and we can do it with `.value()` method.
