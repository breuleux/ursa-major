
ursa-major
==========

Define structs in Earl Grey with typing and validation:

    require-macros:
       ursa-major -> struct

    struct Person:
       String? name
       Number? age
       nullable Person? mother
       nullable Person? father

    p1 = Person(name = "Florence", age = 43)
    p2 = Person(name = "Rashid", age = 57)
    p3 = Person(name = "Emily", age = 23, mother = p1, father = p2)


    require: kaiser

    serialized = kaiser.serialize(p3)
    deserialized = kaiser.deserialize(serialized)


