Everything in Python is an `object`. This includes strings, integers, etc: they are instances of their constructors:
```python
my_int = 2
print(my_int.__class__)
# <class 'int'>
```

*Classes themselves* are also objects; that is, the following code:
```python
class CustomClass:
	pass
```
creates an object 'CustomClass' that represents the class itself. All objects (including classes) are instances of a class, and the default *class of classes*, or 'metaclass', is the function `type`:
```python
# The following 2 expressions are equivalent:
class CustomClass:
	pass

# Signature is type(<class name>, <tuple of parent classes> <dict of class attributes>)
CustomClass = type("CustomClass", (), {})
```

Metaclasses can change the core behavior of the classes they instantiate. As a trivial example, instances of `UpperClass` will have their attribute names capitalized:
```python
# Define our metaclass
# 'type' is the base class for our metaclass
class UpperMeta(type):
	# 'new' creates the instance object, which is then configured by 'init'. This is mostly the same as calling 'type' directly (as a function).
	def __new__(cls, clsname, bases, attrs):
		uppercase_attrs = {
			attr if attr.startswith("__") else attr.upper: v
			for attr, v in attrs
		}

		# same function signature as 'type', except that first arg must be the class itself, just like any other class method.
		return super().__new__(cls, clsname, bases, attrs)

class CustomClass(metaclass=UpperMeta):
	foo = "bar"

instance = CustomClass()

hasattr(instance, "foo") # False
hasattr(instance, "FOO") # True
instance.FOO # "BAR"
```

## __call__
`__call__` is tricky when used in metaclasses: `__call__` defines the behavior of a  class *instance* when it is invoked as a function. Since a `class` is an *instance* of a metaclass, and we create instances by *invoking* the `class`, e.g. `MyClass(1,2,3)`, we can change the way new instances of a class are created by changing `__call__` in a metaclass. By default `__call__` works by first invoking `__new__` to create the new instance object, then `__init__` to configure it, but metaclasses can arbitrarily change this behavior.