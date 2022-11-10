# Four Concepts of Advanced Javascript

IIFE or Immediately Invoked Function Expression is a function that is invoked right when it is defined in code.
Closure is the the fact that an inner function has access to variables defined in the outer function even after the function is done running.
Functional Chaining is when one function can be called after another. eg fun1().fun2()
Prototype Inheritance is when one object inherits from another.

Here well show all four concepts tied together.
``` javascript
const chainable = (function myIIFE() {
    const protoObject = Object.create(null) // creating an object that does not inherit from any other object.
    const imPublic = {
        iCanChain() {
            protoObject.chained = true
            return this // this is referring the the object containing the function. In this case its the imPublic object.
        },
        iCanChainToo() {
            protoObject.chainedAgain = true
            return this
        },
        weThreeFunctionsAreClosures() {
            protoObject.weHaveAccessToPrivateVariables = true
            return this
        },
        iCreatePrototypicalInheritance() {
            return Object.create(protoObject) // The new object will inherit properties from the protoObject
        }
    }

    return imPublic
})()

const prototypicalInheritor = chainable.iCreatePrototypicalInheritance()
console.log(prototypicalInheritor) // returns {}
console.log(prototypicalInheritor.chained) // returns undefined
console.log(prototypicalInheritor.chainedAgain) // returns undefined
console.log(prototypicalInheritor.weHaveAccessToPrivateVariables) // returns undefined

chainable.iCanChain().iCanChainToo().weThreeFunctionsAreClosures()
console.log(prototypicalInheritor) // returns {}
// these return true now because of prototypical inheritance.
console.log(prototypicalInheritor.chained) // returns true
console.log(prototypicalInheritor.chainedAgain) // returns true
console.log(prototypicalInheritor.weHaveAccessToPrivateVariables) // returns true

const anotherPrototypicalInheritor = chainable.iCreatePrototypicalInheritance()
console.log(prototypicalInheritor) // returns {}
console.log(prototypicalInheritor.chained) // returns true
console.log(prototypicalInheritor.chainedAgain) // returns true
console.log(prototypicalInheritor.weHaveAccessToPrivateVariables) // returns true

```
