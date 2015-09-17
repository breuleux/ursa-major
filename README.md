
ursa-major
==========

Define structs in Earl Grey with typing and validation.

## Basic usage

Require the macro like this (`require-macro`, not `require`):

    require-macros:
       ursa-major -> struct

A struct is defined like this. Fields marked `maybe` can either be of
the specified type, or they can be `null`:

    struct Person:
       ;; use the uuid command in the console to generate a unique id for your struct
       ;; Try to add /StructName to the end of the uuid for readability, like this:
       type-id: "46cb4b46-35b8-11e5-9645-e3f320d7342e/Person"
       String? name
       Number? age
       maybe Person? mother
       maybe Person? father

Structs are instantiated with a dictionary of the required properties:

    p1 = Person(name = "Florence", age = 43)
    p2 = Person(name = "Rashid", age = 57)
    p3 = Person(name = "Emily", age = 23, mother = p1, father = p2)

Serialize/deserialize with kaiser. `type-id` must be defined for the
struct in order for this to work.

    require: kaiser

    serialized = kaiser.serialize(p3)
    deserialized = kaiser.deserialize(serialized)


## Validation

A `validate` method can be defined by a struct in order to ensure it
is in a consistent state. For example:

    struct OrderedTriple:
       Number? a
       Number? b
       Number? c
       validate() =
          if @a > @b or @b > @c:
             throw E.not-ordered("The order a < b < c failed to be preserved.")

    OrderedTriple(a = 1, b = 2, c = 3)    ;; OK!
    OrderedTriple(a = 1, b = -2, c = 3)   ;; ERROR!

`validate` is called whenever properties are set:

    o = OrderedTriple(a = 1, b = 2, c = 3)
    o.b = -2  ;; ERROR!

The `update` method can set many fields at once:

    o = OrderedTriple(a = 1, b = 2, c = 3)
    o.update(a = 100, b = 200, c = 300)  ;; OK!


