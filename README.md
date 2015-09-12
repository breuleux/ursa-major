
ursa-major
==========

Define structs in Earl Grey with typing and validation:

    require-macros:
       ursa-major -> struct

    struct Person:
       ;; use the uuid command in the console to generate a unique id for your struct
       type-id: "46cb4b46-35b8-11e5-9645-e3f320d7342e"
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


