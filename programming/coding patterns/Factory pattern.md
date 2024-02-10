General idea is that instead of instantiating objects directly, client code should get object instances through a method that returns a common interface.Clients depend on this interface instead of specific objects. The interface may apply to more than one implementation, but the clients don't need to know this. 

The method that returns the common interface is called the factory, and the objects it returns are sometimes called products.

The creator class may be an abstract class, forcing subclasses to implement the `create()` method, or it may return a default product class.

To work, the factory method *must* return a common interface or base class that all implementations follow.

The client for the common interface may be the creator class *itself*. That is ok:
```python
class MailCreator(abc):

	@abstractmethod
	def factory(self):
		pass

	# THIS is the method clients will interact with
	def mail(self):
		product = self.factory()
		return product.mail_to_users()

# This is the interface for our products
class Mailable(abc):
	@abstractmethod
	def mail_to_users(self):
		pass

# Different implementations of Mailable
class Widget(Mailable):
	def mail_to_users(self):
		self._mail({type: 'widget', name: 'your_widget'})	

	def _mail(self, widgets):
		# use your imagination
		...

class Thingy(Mailable):
	def mail_to_users(self):
		self._other_mail('whatever')

class WidgetCreator(MailCreator):
	def factory(self):
		return Widget()

class ThingyCreator(MailCreator):
	def factory(self):
		return Thingy()
		
# The implementation of the creator determines the exact side-effect triggered by this client. Client can mail Widgets or Thingies depending on passed-in creator, but client doesn't care which.
def mail_stuff(creator: MailCreator):
	creator.mail()	

if __name__ == "__main__":
	mail_stuff(WidgetCreator())
	mail_stuff(ThingyCreator())
```

Use when:
1. You don't know exact types and dependencies of objects code should work with
2. You're writing a library or framework whose users should be able to extend its functionality. Users can subclass your creator classes to swap in their own implementations for different bits of functionality. For example, if your library saves something to a file, but a user wants to save to a particular database, they can override the `createRepo` method your code uses and as long as their `createRepo` returned the expected interface, it would just work.
3. You need to manage resources by re-using created object.

The Abstract Factory is a variant of this pattern where client code relies on abstract interfaces that all factories and products must implement.