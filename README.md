# Clean Code
"Communication is the professional developer’s first order of business." _Clean Code_

We communicate often with others for many reasons (eg. to get requirements, make decisions, ...), but the most common way we communicate with others is how we write our code. This training's purpose is to help us better communicate with others, and ourselves, though clean code.

The subset of ideas about writing clean code referred to here are Naming, Commenting, White Space, Formatting, and eslint. 

## Naming
 "Choosing good names takes time but saves more than it takes. So take care with your names and change them when you find better ones Everyone who reads your code (including you) will be happier if you do." _Clean Code_

 Selecting a good name should tell us
 - Why it exists
 - What it does
 - How it is used

<br />

### Change Names When You Find a Better One
If we don't rename, when appropriate, then we are failing to communicate properly.

__Bad__
``` javascript
const moonStage
```
__Good__
``` javascript
const lunarPhase
```

<br />

### Use Pronounceable Names
We often talk about code verbally. Make it easy to do so.

__Bad__
``` javascript
const HSMTZ
```
__Good__
``` javascript
const timeOfDay
```

<br />

###  Use Names that Distinguish the Differences
Don't make other developers, or your future self, confused about what something represents.

__Bad__
``` javascript
setPaymentStatus(4)
```
__Good__
``` javascript
setPaymentStatus(PAYMENT_STATUS.compleat)
```

<br />

### Avoid Encode and prefixes
Encoding makes it harder to find the right function as you start to type. If every function/variable/object/component started with fs then as soon as you type fs you would have a host of unhelpful info form the text editor/IDE.

__Bad__
``` javascript
/*
<FSButton />
<FSHeader />
*/
function gArticles() {
  return fetch('/service/.../articles?...')
}
```
__Good__
``` javascript
/*
<Button />
<Header />
*/
function getArticles() {
  return fetch('/service/.../articles?...')
}
```

<br />

### Pick one word for one abstract concept
Being consistent takes of a mental load when trying to figure out what is gong on.

__Bad__
``` javascript
const user = getUser()
const messages = retrieveMessages(user)
```
__Good__
``` javascript
const user = getUser()
const messages = getMessages(user.id)
```

<br />

### Using Context
A word can mean different things in differing context. Take the word state for example. It could be part of an address or it could be a state variable in a component. It's best not to make anyone guess.

__Bad__
``` javascript
const state
```
__Good__
``` javascript
const address = {
  state,
  // other params
}
```

<br />

### Don't Use mental mapping

__Bad__
``` javascript
/**
 * Makes url to get articles
 * 
 * @param {number} param1 sets page size
 * @param {Number} param2 page we want
 * @param {String} param3 
 * @param {String} param5 
 */
function serviceUrl(param1, param2, param3, param5) {
  return `/service/api/v1/articles?pageSize=${param1}&page=${param2}&type=${param3}&language=${param5}`
}
```
__Good__
``` javascript
/**
 * @param {Object} articleServiceParams
 * @param {Number} articleServiceParams.pageSize
 * @param {Number} articleServiceParams.pageNumber
 * @param {String} articleServiceParams.type
 * @param {String} articleServiceParams.language
 */
function makeArticlesUrl({pageSize, pageNumber, type, language}) {
  return `/service/api/v1/articles?pageSize=${pageSize}&page=${pageNumber}&type=${type}&language=${language}`
}
```

<br />

### Don't Allow disinformation
Naming should tell you what something is. If it doesn't, change it.

__Bad__
``` javascript
const setOfAccounts = {
  'laskjf-132': {},
  'sleksj-321': {},
}
```
__Good__
``` javascript
const accounts = {
  'laskjf-132': {},
  'sleksj-321': {},
}
```

<br />

### Don't Use Redundant Names

__Bad__
``` javascript
var sumVariable
```
__Good__
``` javascript
var sum
```

<br />

### Don't Be Cute or Punny
This can but fun, but it looses readability.

__Bad__
``` javascript
function imGonnaReckIt() {}
function cutTies() {}
```
__Good__
``` javascript
function closeOverlay() {}
function removePerson() {}
```

<br />

### Pick One Word Per Concept and Avoid Using The Same Word for Two Purposes
This makes finding what you are looking for easier.

__Bad__
``` javascript
function getUser() {}
function fetchContactInfo() {}
```
__Good__
``` javascript
function getUser() {}
function getContactInfo() {}
```

<br />

### Use Industry Names or Domain Specific Names as a Backup.
If its an industry standard then developers can know what it is without any prior explanation.

__Bad__
``` javascript
const userCompilation
```
__Good__
``` javascript
const userArray
```

<br />

### Object Names Should Be Nouns and Functions/Methods Should Be Verb or Verb Phrases
“Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.” _Clean Code_


## Comments
the book _Clean Code_ states that "comments are, at best, a necessary evil."

My take is comments are like salt. A little help a lot. A lot burns my eyes. Express as much as you can in code. Use comments as necessary. over commenting does make the code difficult to read, follow, and maintain.

If you decide to write a comment, make sure to take time to make it a good one. A poor comment can be pointless, distracting, or worse misleading.

### The primary purpose of good comments are to
  - Refer too or contain legal information.
  - Inform the reader of concepts in code.
  - Explain the reason the code took one path over another.
  - Clarify an API or standard library.
  - Warn the reader of possible pitfalls.
  - Keep track of todo item.
  - Emphasize code that seems possible unimportant.
  - Document and api.
  - Help autocompletion of a text editor or IDE.
  - (In rare cases) Marking a block of code.

### Some poor commenting practices include
  - Misleading the reader in what the code does.
  - Redundant explanations. The function/object/variable name says what it does but theres still a comment to tell you the exact same thing.
  - Redundant explanations. The function/object/variable name says what it does but theres still a comment to tell you the exact same thing.
  - Historical information. Perhaps in rare cases this is a good idea.
  - Statements that add nothing to understand anything about the code that we don't get form a quick reading of the code itself.
  - Indicating the closing of a block of code. If this happens try to refactor to make the block of code smaller.
  - Marking many blocks of code.
  - Indicating who wrote the file/line. This is kept track of much more accurately in source control.
  - Information about a block of code not close to where the comment is.
  - Statements littered with HTML. This makes it difficult to read/alter.
  - Statements with unclear text. They don't seem closely connected with the code.
  - Documenting private code as if its a public API
  - Code that has been commented out.

### Examples
  __Bad__
  ``` javascript
    function formatDateString(date) {
      // Show only day if in same week.
      if (isThisWeek(date)) {
        return listOfDaysInWeek()[date.getDay()]
      }

      // Show year only if in a previous calender year.
      return isThisYear(date) ? format(date, 'd MMMM') : format(date)
    }

    // using cache to determine if user has checked the latest message
    const [hasNewMessage, setTimeStamp, MessageDot] = useShowDot({
      name: 'headerMessages',
      latestCheck: messageSummaries?.userThreadSummaries?.[0]?.lastModifiedTime,
    })

    /**
     * Makes an article url and returns it.
     * @param {Object} articleServiceParams
     * @param {Number} articleServiceParams.pageSize
     * @param {Number} articleServiceParams.pageNumber
     * @param {String} articleServiceParams.type
     * @param {String} articleServiceParams.language
     */
    function makeArticlesUrl({pageSize, pageNumber, type, language}) {
      return `/service/api/v1/articles?pageSize=${pageSize}&page=${pageNumber}&type=${type}&language=${language}`
    }
  ```

  __Good__
  ``` javascript
    function formatDateString(date) {
      if (isThisWeek(date)) {
        // returning day of the week
        return listOfDaysInWeek()[date.getDay()]
      }

      if(isThisYear(date)) {
        // returns numerical day and four letter abbreviated month
        return format(date, 'd MMMM')
      }

      // returns year
      return format(date)
    }

    // legal comment @copyright

    // This helps us to keep the info of the user safe
    const obfuscatedPassword = hashData(user)

    // @Todo once the <Blah /> component is ready replace this.

    /**
     * @param {Object} articleServiceParams
     * @param {Number} articleServiceParams.pageSize
     * @param {Number} articleServiceParams.pageNumber
     * @param {String} articleServiceParams.type
     * @param {String} articleServiceParams.language
     */
    function makeArticlesUrl({pageSize, pageNumber, type, language}) {
      return `/service/api/v1/articles?pageSize=${pageSize}&page=${pageNumber}&type=${type}&language=${language}`
    }
  ```

## whitespace/formatting/eslint

"Code formatting is about communication, and communication is the professional developer’s first order of business.

Perhaps you thought that 'getting it working' was the first order of business for a professional developer. I hope by now, however, that this book has disabused you of that idea. The functionality that you create today has a good chance of changing in the next release, but the readability of your code will have a profound effect on all the changes that will ever be made. The coding style and readability set precedents that continue to affect maintainability and extensibility long after the original code has been changed beyond recognition. Your style and discipline survives, even though your code does not.

So what are the formatting issues that help us to communicate best?" _Clean Code_

### Whitespace
Vertical and horizontal whitespace go along way to making code easier to read and understand. The more related two things are the less space they should have. If you have ever tried to parse code on a single line... it is really hard.

Space out your code so that if you are having to look at it to fix a bug in the middle of the night, you can decern changes in though by the white space.

__Bad__
```javascript
  import React, { useState, useEffect } from 'react'
  import { css } from '@emotion/core'
  const elementCss = css`display: flex;`
  function areChildrenReady({children}) {
    return React.children(// blah blah blah)
  }
  function useHandleChildren({children}) {
    if(!areChildrenReady({children})) return null
    // stuff
    return result
  }
  function DisplayStuff({children, ...props}) {
    const readyChildren = useHandleChildren({children})
    return (
      readyChildren.map(child => {})
    )
  }
```

__Good__
```javascript
  import React, { useState, useEffect } from 'react'
  import { css } from '@emotion/core'

  const elementCss = css`
    display: flex;
  `

  function areChildrenReady({children}) {
    return React.children(// blah blah blah)
  }

  function useHandleChildren({children}) {
    if(!areChildrenReady({children})) return null

    // stuff
    
    return result
  }

  function DisplayStuff({children, ...props}) {
    const readyChildren = useHandleChildren({children})

    return (
      readyChildren.map(
        child => {
          <Blah  />
        }
      )
    )
  }
```

### Formatting and eslint
When it comes to formatting, a good linter and formatter goes a long way at making the code look consistent. But it can only do so much. It is up to the developer to determine what code should be grouped together and out its ordered.

Try to keep code representing a similar action or similar concepts together. It can make it easier to find what your looking for when you or someone else comes back.

If a file/function/component is getting large and requires large amounts of scrolling try to break it up into smaller concepts.

__Bad__
``` javascript
  function ScrollObserver({ children, observeScroll, fullyScrolledCallBack }) {
    const [isScrollSet, setIsScrollSet] = useState()
    const skeletonRef = useCallback(
      (node) => {if (node && !isScrollSet) {
          setIsScrollSet(true)
          observeSkeletonContainer(node)
        }},[isScrollSet, observeSkeletonContainer]
    )
    const [isSkeletonContainerVisible, observeSkeletonContainer] = useIsElementVisible()
    const scrolledCallBack = useCallback(fullyScrolledCallBack, [])
    useEffect(() => {
      if (observeScroll && isSkeletonContainerVisible) scrolledCallBack()
    }, [isSkeletonContainerVisible, observeScroll, scrolledCallBack])
    return (
      <>
        {children}
        <div ref={skeletonRef}>{observeScroll && (<div>{loadingIndicator}<div/>)}</div>
      </>
    )
  }
```

__Good__
``` javascript
  function ScrollObserver({ children, observeScroll, fullyScrolledCallBack }) {
    const [isScrollSet, setIsScrollSet] = useState()
    const [isSkeletonContainerVisible, observeSkeletonContainer] = useIsElementVisible()
    const scrolledCallBack = useCallback(fullyScrolledCallBack, [])

    const skeletonRef = useCallback(
      (node) => {
        if (node && !isScrollSet) {
          setIsScrollSet(true)
          observeSkeletonContainer(node)
        }
      },
      [isScrollSet, observeSkeletonContainer]
    )

    useEffect(() => {
      if (observeScroll && isSkeletonContainerVisible) {
        scrolledCallBack()
      }
    }, [isSkeletonContainerVisible, observeScroll, scrolledCallBack])
    
    return (
      <>
        {children}
        <div ref={skeletonRef}>
          {observeScroll && (
            <div>{loadingIndicator}<div/>
          )}
        </div>
      </>
    )
  }
```

When it comes to eslint, take care of all lint issues before merging into a master branch. Following the recommendations given by the linter will help keep to best practices and prevent most bugs. At times it may be necessary to ignore the linter, but do this as a last resort.

## Final Note
Clean code begets clean code. Take time to clean the code up so when you or someone else comes back it's easier to make to best changes.

But after all is said and done...
![](CodeQualityMeasurement.png)

### This is based on

[Clean Code Javascript](https://github.com/ryanmcdermott/clean-code-javascript)

Robert C. Martin's book [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

Along with some of my own thoughts.

### Thanks to 
Logan Allred

Jakob Anderson

Derrick Craven

David Gurney

Tyler Graf

Seven Stormberg

And those in the Frontier Architecture Working Group not mentioned here for feed back and help.
