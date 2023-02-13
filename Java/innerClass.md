https://johngrib.github.io/wiki/java/inner-class-may-be-static/

An inner class may be static if it doesn't reference its enclosing instance.

A static inner class does not keep an implicit reference to its enclosing instance. This prevents a common cause of memory leaks and uses less memory per instance of the class.