# Serializable Object
`serializable-object` is a lightweight library for serializing and deserializing objects. These objects can easily be transmitted as long as the class of the object is registered on both ends of the request.

---

### Installation
`npm install --save serializable-object`

### Quick Start
``
const SerializableObject = require('serializable-object')
let object = new SerializableObject()
``

### Serialization
``
let object = new SerializableObject()
object.value = 10
object.serialize() // { _class: 'SerializableObject', value: 10 }
``

### Deserialization
``
let object = new SerializableObject()
object.value = 10
let data = object.serialize()
let deserializedObject = new SerializableObject().deserialize(data) // SerializableObject { value: 10 }
``

### Extending Classes
Extending the `SerializableObject` class is easy. Just be sure to register the extended class after it has been defined.
``
class Subclass extends SerializableObject {}
let object = new SerializableObject()
object.subclass = new Subclass()
let data = object.serialize() // {_class: 'SerializableObject', subclass: { _class: 'Subclass' } }
let deserializedObject = new SerializableObject().deserialize(data) // SerializableObject { subclass: Subclass {} }
``
It is not necessary to call `deserialize` on the type of object that you want to be returned. The type of object returned will always match the `_class` of the serialized object that is provided.
``
class Subclass extends SerializableObject {}
let object = new Subclass()
object.value = 10
let data = object.serialize() // { _class: 'Subclass', value: 10 }
let deserializedObject = new SerializableObject().deserialize(data) // Subclass { value: 10}
```
