---
title: DOM Standard
source: https://dom.spec.whatwg.org/
snapshot: https://dom.spec.whatwg.org/commit-snapshots/3071e5f269448350fdea79bb284eedaf17bc431e/
retrieved: 2026-10-10
converted: 2026-10-10
author: WHATWG
license: CC BY 4.0
tags:
  - spec
  - whatwg
---

# DOM

> [!info] Unofficial copy
> This page is an unofficial, non-normative copy of the [DOM Standard](https://dom.spec.whatwg.org/), based on the [snapshot of commit 3071e5f](https://dom.spec.whatwg.org/commit-snapshots/3071e5f269448350fdea79bb284eedaf17bc431e/), retrieved on 2026-10-10. It is not reviewed or endorsed by the WHATWG; for the authoritative text see the original.
> 
> Copyright © WHATWG (Apple, Google, Mozilla, Microsoft). Licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
> 
> Changes: converted automatically from HTML to Markdown with mdVü on 2026-10-10; the WHATWG logo and the MDN browser-support boxes were removed, notes, warnings and examples became callouts, relative links and image addresses were made absolute, and links between the HTML, DOM and Infra standards point to the local copies.

Living Standard — Last Updated 9 October 2026

Participate:

[GitHub whatwg/dom](https://github.com/whatwg/dom) ([new issue](https://github.com/whatwg/dom/issues/new/choose), [open issues](https://github.com/whatwg/dom/issues))

[Chat on Matrix](https://whatwg.org/chat)

Commits:

[GitHub whatwg/dom/commits](https://github.com/whatwg/dom/commits)

[Snapshot as of this commit](https://dom.spec.whatwg.org/commit-snapshots/3071e5f269448350fdea79bb284eedaf17bc431e/)

Tests:

[web-platform-tests dom/](https://github.com/web-platform-tests/wpt/tree/master/dom) ([ongoing work](https://github.com/web-platform-tests/wpt/labels/dom))

Translations (non-normative):

[日本語](https://triple-underscore.github.io/DOM4-ja.html)

[简体中文](https://htmlspecs.com/dom/)

[한국어](https://ko.htmlspecs.com/dom/)

## Abstract

DOM defines a platform-neutral model for events, aborting activities, and node trees.

## Table of Contents
1. [1 Infrastructure](#1-infrastructure)
   1. [1.1 Trees](#11-trees)
   2. [1.2 Ordered sets](#12-ordered-sets)
   3. [1.3 Selectors](#13-selectors)
   4. [1.4 Name validation](#14-name-validation)
2. [2 Events](#2-events)
   1. [2.1 Introduction to "DOM Events"](#21-introduction-to-dom-events)
   2. [2.2 Interface `Event`](#22-interface-event)
   3. [2.3 Legacy extensions to the `Window` interface](#23-legacy-extensions-to-the-window-interface)
   4. [2.4 Interface `CustomEvent`](#24-interface-customevent)
   5. [2.5 Constructing events](#25-constructing-events)
   6. [2.6 Defining event interfaces](#26-defining-event-interfaces)
   7. [2.7 Interface `EventTarget`](#27-interface-eventtarget)
   8. [2.8 Observing event listeners](#28-observing-event-listeners)
   9. [2.9 Dispatching events](#29-dispatching-events)
   10. [2.10 Firing events](#210-firing-events)
   11. [2.11 Action versus occurrence](#211-action-versus-occurrence)
3. [3 Aborting ongoing activities](#3-aborting-ongoing-activities)
   1. [3.1 Interface `AbortController`](#31-interface-abortcontroller)
   2. [3.2 Interface `AbortSignal`](#32-interface-abortsignal)
      1. [3.2.1 Garbage collection](#321-garbage-collection)
   3. [3.3 Using `AbortController` and `AbortSignal` objects in APIs](#33-using-abortcontroller-and-abortsignal-objects-in-apis)
4. [4 Nodes](#4-nodes)
   1. [4.1 Introduction to "The DOM"](#41-introduction-to-the-dom)
   2. [4.2 Node tree](#42-node-tree)
      1. [4.2.1 Document tree](#421-document-tree)
      2. [4.2.2 Shadow tree](#422-shadow-tree)
         1. [4.2.2.1 Slots](#4221-slots)
         2. [4.2.2.2 Slottables](#4222-slottables)
         3. [4.2.2.3 Finding slots and slottables](#4223-finding-slots-and-slottables)
         4. [4.2.2.4 Assigning slottables and slots](#4224-assigning-slottables-and-slots)
         5. [4.2.2.5 Signaling slot change](#4225-signaling-slot-change)
      3. [4.2.3 Mutation algorithms](#423-mutation-algorithms)
      4. [4.2.4 Mixin `NonElementParentNode`](#424-mixin-nonelementparentnode)
      5. [4.2.5 Mixin `DocumentOrShadowRoot`](#425-mixin-documentorshadowroot)
      6. [4.2.6 Mixin `ParentNode`](#426-mixin-parentnode)
      7. [4.2.7 Mixin `NonDocumentTypeChildNode`](#427-mixin-nondocumenttypechildnode)
      8. [4.2.8 Mixin `ChildNode`](#428-mixin-childnode)
      9. [4.2.9 Mixin `Slottable`](#429-mixin-slottable)
      10. [4.2.10 Old-style collections: `NodeList` and `HTMLCollection`](#4210-old-style-collections-nodelist-and-htmlcollection)
          1. [4.2.10.1 Interface `NodeList`](#42101-interface-nodelist)
          2. [4.2.10.2 Interface `HTMLCollection`](#42102-interface-htmlcollection)
   3. [4.3 Mutation observers](#43-mutation-observers)
      1. [4.3.1 Interface `MutationObserver`](#431-interface-mutationobserver)
      2. [4.3.2 Queuing a mutation record](#432-queuing-a-mutation-record)
      3. [4.3.3 Interface `MutationRecord`](#433-interface-mutationrecord)
   4. [4.4 Interface `Node`](#44-interface-node)
   5. [4.5 Interface `Document`](#45-interface-document)
      1. [4.5.1 Interface `DOMImplementation`](#451-interface-domimplementation)
   6. [4.6 Interface `DocumentType`](#46-interface-documenttype)
   7. [4.7 Interface `DocumentFragment`](#47-interface-documentfragment)
   8. [4.8 Interface `ShadowRoot`](#48-interface-shadowroot)
   9. [4.9 Interface `Element`](#49-interface-element)
      1. [4.9.1 Interface `NamedNodeMap`](#491-interface-namednodemap)
      2. [4.9.2 Interface `Attr`](#492-interface-attr)
   10. [4.10 Interface `CharacterData`](#410-interface-characterdata)
   11. [4.11 Interface `Text`](#411-interface-text)
   12. [4.12 Interface `CDATASection`](#412-interface-cdatasection)
   13. [4.13 Interface `ProcessingInstruction`](#413-interface-processinginstruction)
   14. [4.14 Interface `Comment`](#414-interface-comment)
5. [5 Ranges](#5-ranges)
   1. [5.1 Introduction to "DOM Ranges"](#51-introduction-to-dom-ranges)
   2. [5.2 Boundary points](#52-boundary-points)
   3. [5.3 Interface `AbstractRange`](#53-interface-abstractrange)
   4. [5.4 Interface `StaticRange`](#54-interface-staticrange)
   5. [5.5 Interface `Range`](#55-interface-range)
6. [6 Traversal](#6-traversal)
   1. [6.1 Interface `NodeIterator`](#61-interface-nodeiterator)
   2. [6.2 Interface `TreeWalker`](#62-interface-treewalker)
   3. [6.3 Interface `NodeFilter`](#63-interface-nodefilter)
7. [7 Sets](#7-sets)
   1. [7.1 Interface `DOMTokenList`](#71-interface-domtokenlist)
8. [8 XPath](#8-xpath)
   1. [8.1 Interface `XPathResult`](#81-interface-xpathresult)
   2. [8.2 Interface `XPathExpression`](#82-interface-xpathexpression)
   3. [8.3 Mixin `XPathEvaluatorBase`](#83-mixin-xpathevaluatorbase)
   4. [8.4 Interface `XPathEvaluator`](#84-interface-xpathevaluator)
9. [9 XSLT](#9-xslt)
   1. [9.1 Interface `XSLTProcessor`](#91-interface-xsltprocessor)
10. [10 Security and privacy considerations](#10-security-and-privacy-considerations)
11. [11 Historical](#11-historical)
12. [Acknowledgments](#acknowledgments)
13. [Intellectual property rights](#intellectual-property-rights)
14. [Index](#index)
    1. [Terms defined by this specification](#terms-defined-by-this-specification)
    2. [Terms defined by reference](#terms-defined-by-reference)
15. [References](#references)
    1. [Normative References](#normative-references)
    2. [Non-Normative References](#non-normative-references)
16. [IDL Index](#idl-index)

## 1. Infrastructure

This specification depends on the Infra Standard. [\[INFRA\]](#normative-references)

Some of the terms used in this specification are defined in Encoding, Selectors, Trusted Types, Web IDL, XML, Namespaces in XML, and Associating Style Sheets with XML documents. [\[ENCODING\]](#normative-references) [\[SELECTORS4\]](#normative-references) [\[TRUSTED-TYPES\]](#normative-references) [\[WEBIDL\]](#normative-references) [\[XML\]](#normative-references) [\[XML-NAMES\]](#normative-references) [\[XML-STYLESHEET\]](#normative-references)

When extensions are needed, the DOM Standard can be updated accordingly, or a new standard can be written that hooks into the provided extensibility hooks for applicable specifications.

### 1.1. Trees

A tree is a finite hierarchical tree structure. In tree order is preorder, depth-first traversal of a [tree](#11-trees).

An object that participates in a [tree](#11-trees) has a parent, which is either null or an object, and has children, which is an [ordered set](infra-spec-whatwg-org.md#513-sets) of objects. An object A whose [parent](#11-trees) is object B is a [child](#11-trees) of B.

The root of an object is itself, if its [parent](#11-trees) is null, or else it is the [root](#11-trees) of its [parent](#11-trees). The [root](#11-trees) of a [tree](#11-trees) is any object [participating](#11-trees) in that [tree](#11-trees) whose [parent](#11-trees) is null.

An object A is called a descendant of an object B, if either A is a [child](#11-trees) of B or A is a [child](#11-trees) of an object C that is a [descendant](#11-trees) of B.

An inclusive descendant is an object or one of its [descendants](#11-trees).

An object A is called an ancestor of an object B if and only if B is a [descendant](#11-trees) of A.

An inclusive ancestor is an object or one of its [ancestors](#11-trees).

An object A is called a sibling of an object B, if and only if B and A share the same non-null [parent](#11-trees).

An inclusive sibling is an object or one of its [siblings](#11-trees).

An object A is preceding an object B if A and B are in the same [tree](#11-trees) and A comes before B in [tree order](#11-trees).

An object A is following an object B if A and B are in the same [tree](#11-trees) and A comes after B in [tree order](#11-trees).

The first child of an object is its first [child](#11-trees) or null if it has no [children](#11-trees).

The last child of an object is its last [child](#11-trees) or null if it has no [children](#11-trees).

The previous sibling of an object is its first [preceding](#11-trees) [sibling](#11-trees) or null if it has no [preceding](#11-trees) [sibling](#11-trees).

The next sibling of an object is its first [following](#11-trees) [sibling](#11-trees) or null if it has no [following](#11-trees) [sibling](#11-trees).

The index of an object is its number of [preceding](#11-trees) [siblings](#11-trees), or 0 if it has none.

### 1.2. Ordered sets

The ordered set parser takes a string input and then runs these steps:
1. Let inputTokens be the result of [splitting input on ASCII whitespace](infra-spec-whatwg-org.md#47-strings).
2. Let tokens be a new [ordered set](infra-spec-whatwg-org.md#513-sets).
3. [For each](infra-spec-whatwg-org.md#51-lists) token of inputTokens: [append](infra-spec-whatwg-org.md#513-sets) token to tokens.
4. Return tokens.

The ordered set serializer takes a set and returns the [concatenation](infra-spec-whatwg-org.md#47-strings) of set using U+0020 SPACE.

### 1.3. Selectors

To scope-match a selectors string given a string selectors against a [node](#42-node-tree) node:
1. Let selector be the result of [parse a selector](https://drafts.csswg.org/selectors-4/#parse-a-selector) selectors. [\[SELECTORS4\]](#normative-references)
2. If selector is failure, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Return the result of [match a selector against a tree](https://drafts.csswg.org/selectors-4/#match-a-selector-against-a-tree) with selector and node’s [root](#11-trees) using [scoping root](https://drafts.csswg.org/selectors-4/#scoping-root) node. [\[SELECTORS4\]](#normative-references).

> [!note]
> Support for namespaces within selectors is not planned and will not be added.

### 1.4. Name validation

A [string](infra-spec-whatwg-org.md#47-strings) is a valid namespace prefix if its [length](infra-spec-whatwg-org.md#47-strings) is at least 1 and it does not contain [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), U+0000 NULL, U+002F (/), or U+003E (>).

A [string](infra-spec-whatwg-org.md#47-strings) is a valid attribute local name if its [length](infra-spec-whatwg-org.md#47-strings) is at least 1 and it does not contain [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), U+0000 NULL, U+002F (/), U+003D (=), or U+003E (>).

A [string](infra-spec-whatwg-org.md#47-strings) name is a valid element local name if the following steps return true:
1. If name’s [length](infra-spec-whatwg-org.md#47-strings) is 0, then return false.
2. If name’s 0th [code point](infra-spec-whatwg-org.md#46-code-points) is an [ASCII alpha](infra-spec-whatwg-org.md#46-code-points):
   1. If name contains [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), U+0000 NULL, U+002F (/), or U+003E (>), then return false.
   2. Return true.
3. If name’s 0th [code point](infra-spec-whatwg-org.md#46-code-points) is not U+003A (:), U+005F (\_), or in the range U+0080 to U+10FFFF, inclusive, then return false.
4. If name’s subsequent [code points](infra-spec-whatwg-org.md#46-code-points), if any, are not [ASCII alphas](infra-spec-whatwg-org.md#46-code-points), [ASCII digits](infra-spec-whatwg-org.md#46-code-points), U+002D (-), U+002E (.), U+003A (:), U+005F (\_), or in the range U+0080 to U+10FFFF, inclusive, then return false.
5. Return true.

> [!note]
> This concept is used to validate [element](#49-interface-element) [local names](#49-interface-element), when constructed by DOM APIs. The intention is to allow any name that is possible to construct using the HTML parser (the branch where the first [code point](infra-spec-whatwg-org.md#46-code-points) is an [ASCII alpha](infra-spec-whatwg-org.md#46-code-points)), plus some additional possibilities. For those additional possibilities, the ASCII range is restricted for historical reasons, but beyond ASCII anything is allowed.

> [!note]
> The following JavaScript-compatible regular expression is an implementation of [valid element local name](#14-name-validation):
> 
> ```javascript
> /^(?:[A-Za-z][^\0\t\n\f\r\u0020/>]*|[:_\u0080-\u{10FFFF}][A-Za-z0-9-.:_\u0080-\u{10FFFF}]*)$/u
> 
> ```

A [string](infra-spec-whatwg-org.md#47-strings) is a valid doctype name if it does not contain [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), U+0000 NULL, or U+003E (>).

> [!note]
> The empty string is a [valid doctype name](#14-name-validation).

To validate and extract a namespace and qualifiedName, given a context:
1. If namespace is the empty string, then set it to null.
2. Let prefix be null.
3. Let localName be qualifiedName.
4. If qualifiedName contains a U+003A (:):
   1. Set prefix to the part of qualifiedName before the first U+003A (:).
   2. Set localName to the part of qualifiedName after the first U+003A (:).
   3. If prefix is not a [valid namespace prefix](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
5. [Assert](infra-spec-whatwg-org.md#310-assertions): prefix is either null or a [valid namespace prefix](#14-name-validation).
6. If context is "`attribute`" and localName is not a [valid attribute local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
7. If context is "`element`" and localName is not a [valid element local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
8. If prefix is non-null and namespace is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NamespaceError`](https://webidl.spec.whatwg.org/#namespaceerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
9. If prefix is "`xml`" and namespace is not the [XML namespace](infra-spec-whatwg-org.md#8-namespaces), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NamespaceError`](https://webidl.spec.whatwg.org/#namespaceerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
10. If either qualifiedName or prefix is "`xmlns`" and namespace is not the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NamespaceError`](https://webidl.spec.whatwg.org/#namespaceerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
11. If namespace is the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces) and neither qualifiedName nor prefix is "`xmlns`", then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NamespaceError`](https://webidl.spec.whatwg.org/#namespaceerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
12. Return (namespace, prefix, localName).

> [!note]
> Various APIs in this specification used to validate namespace prefixes, attribute local names, element local names, and doctype names more strictly. This was done in a way that aligned with various XML-related specifications. (Although not all rules from the those specifications were enforced.)
> 
> This was found to be annoying for web developers, especially since it meant there were some names that could be created by the HTML parser, but not by DOM APIs. So, the validations have been loosened to just those described above.

## 2. Events

### 2.1. Introduction to "DOM Events"

Throughout the web platform [events](#22-interface-event) are [dispatched](#29-dispatching-events) to objects to signal an occurrence, such as network activity or user interaction. These objects implement the [`EventTarget`](#27-interface-eventtarget) interface and can therefore add [event listeners](#27-interface-eventtarget) to observe [events](#22-interface-event) by calling [`addEventListener()`](#27-interface-eventtarget):

```
obj.addEventListener("load", imgFetched)

function imgFetched(ev) {
  // great success
  …
}

```

[Event listeners](#27-interface-eventtarget) can be removed by utilizing the [`removeEventListener()`](#27-interface-eventtarget) method, passing the same arguments.

Alternatively, [event listeners](#27-interface-eventtarget) can be removed by passing an [`AbortSignal`](#32-interface-abortsignal) to [`addEventListener()`](#27-interface-eventtarget) and calling [`abort()`](#31-interface-abortcontroller) on the controller owning the signal.

[Events](#22-interface-event) are objects too and implement the [`Event`](#22-interface-event) interface (or a derived interface). In the example above ev is the [event](#22-interface-event). ev is passed as an argument to the [event listener](#27-interface-eventtarget)’s [callback](#27-interface-eventtarget) (typically a JavaScript Function as shown above). [Event listeners](#27-interface-eventtarget) key off the [event](#22-interface-event)’s [`type`](#22-interface-event) attribute value ("`load`" in the above example). The [event](#22-interface-event)’s [`target`](#22-interface-event) attribute value returns the object to which the [event](#22-interface-event) was [dispatched](#29-dispatching-events) (obj above).

Although [events](#22-interface-event) are typically [dispatched](#29-dispatching-events) by the user agent as the result of user interaction or the completion of some task, applications can [dispatch](#29-dispatching-events) [events](#22-interface-event) themselves by using what are commonly known as synthetic events:

```
// add an appropriate event listener
obj.addEventListener("cat", function(e) { process(e.detail) })

// create and dispatch the event
var event = new CustomEvent("cat", {"detail":{"hazcheeseburger":true}})
obj.dispatchEvent(event)

```

Apart from signaling, [events](#22-interface-event) are sometimes also used to let an application control what happens next in an operation. For instance as part of form submission an [event](#22-interface-event) whose [`type`](#22-interface-event) attribute value is "`submit`" is [dispatched](#29-dispatching-events). If this [event](#22-interface-event)’s [`preventDefault()`](#22-interface-event) method is invoked, form submission will be terminated. Applications who wish to make use of this functionality through [events](#22-interface-event) [dispatched](#29-dispatching-events) by the application (synthetic events) can make use of the return value of the [`dispatchEvent()`](#27-interface-eventtarget) method:

```
if(obj.dispatchEvent(event)) {
  // event was not canceled, time for some magic
  …
}

```

When an [event](#22-interface-event) is [dispatched](#29-dispatching-events) to an object that [participates](#11-trees) in a [tree](#11-trees) (e.g., an [element](#49-interface-element)), it can reach [event listeners](#27-interface-eventtarget) on that object’s [ancestors](#11-trees) too. Effectively, all the object’s [inclusive ancestor](#11-trees) [event listeners](#27-interface-eventtarget) whose [capture](#27-interface-eventtarget) is true are invoked, in [tree order](#11-trees). And then, if [event](#22-interface-event)’s [`bubbles`](#22-interface-event) is true, all the object’s [inclusive ancestor](#11-trees) [event listeners](#27-interface-eventtarget) whose [capture](#27-interface-eventtarget) is false are invoked, now in reverse [tree order](#11-trees).

Let’s look at an example of how [events](#22-interface-event) work in a [tree](#11-trees):

```
<!doctype html>
<html>
 <head>
  <title>Boring example</title>
 </head>
 <body>
  <p>Hello <span id=x>world</span>!</p>
  <script>
   function test(e) {
     debug(e.target, e.currentTarget, e.eventPhase)
   }
   document.addEventListener("hey", test, {capture: true})
   document.body.addEventListener("hey", test)
   var ev = new Event("hey", {bubbles:true})
   document.getElementById("x").dispatchEvent(ev)
  </script>
 </body>
</html>

```

The `debug` function will be invoked twice. Each time the [event](#22-interface-event)’s [`target`](#22-interface-event) attribute value will be the `span` [element](#49-interface-element). The first time [`currentTarget`](#22-interface-event) attribute’s value will be the [document](#45-interface-document), the second time the `body` [element](#49-interface-element). [`eventPhase`](#22-interface-event) attribute’s value switches from [`CAPTURING_PHASE`](#22-interface-event) to [`BUBBLING_PHASE`](#22-interface-event). If an [event listener](#27-interface-eventtarget) was registered for the `span` [element](#49-interface-element), [`eventPhase`](#22-interface-event) attribute’s value would have been [`AT_TARGET`](#22-interface-event).

### 2.2. Interface [`Event`](#22-interface-event)

```webidl
[Exposed=*]
interface Event {
  constructor(DOMString type, optional EventInit eventInitDict = {});

  readonly attribute DOMString type;
  readonly attribute EventTarget? target;
  readonly attribute EventTarget? srcElement; // legacy
  readonly attribute EventTarget? currentTarget;
  sequence<EventTarget> composedPath();

  const unsigned short NONE = 0;
  const unsigned short CAPTURING_PHASE = 1;
  const unsigned short AT_TARGET = 2;
  const unsigned short BUBBLING_PHASE = 3;
  readonly attribute unsigned short eventPhase;

  undefined stopPropagation();
           attribute boolean cancelBubble; // legacy alias of .stopPropagation()
  undefined stopImmediatePropagation();

  readonly attribute boolean bubbles;
  readonly attribute boolean cancelable;
           attribute boolean returnValue;  // legacy
  undefined preventDefault();
  readonly attribute boolean defaultPrevented;
  readonly attribute boolean composed;

  [LegacyUnforgeable] readonly attribute boolean isTrusted;
  readonly attribute DOMHighResTimeStamp timeStamp;

  undefined initEvent(DOMString type, optional boolean bubbles = false, optional boolean cancelable = false); // legacy
};

dictionary EventInit {
  boolean bubbles = false;
  boolean cancelable = false;
  boolean composed = false;
};

```

An [`Event`](#22-interface-event) object is simply named an event. It allows for signaling that something has occurred, e.g., that an image has completed downloading.

A potential event target is null or an [`EventTarget`](#27-interface-eventtarget) object.

An [event](#22-interface-event) has an associated target (a [potential event target](#22-interface-event)). Unless stated otherwise it is null.

An [event](#22-interface-event) has an associated relatedTarget (a [potential event target](#22-interface-event)). Unless stated otherwise it is null.

> [!note]
> Other specifications use [relatedTarget](#22-interface-event) to define a `relatedTarget` attribute. [\[UIEVENTS\]](#normative-references)

An [event](#22-interface-event) has an associated touch target list (a [list](infra-spec-whatwg-org.md#51-lists) of zero or more [potential event targets](#22-interface-event)). Unless stated otherwise it is the empty list.

> [!note]
> The [touch target list](#22-interface-event) is for the exclusive use of defining the [`TouchEvent`](https://w3c.github.io/touch-events/#idl-def-touchevent) interface and related interfaces. [\[TOUCH-EVENTS\]](#normative-references)

An [event](#22-interface-event) has an associated path. A [path](#22-interface-event) is a [list](infra-spec-whatwg-org.md#51-lists) of [event path items](#22-interface-event). An event path item is a [struct](infra-spec-whatwg-org.md#53-structs) consisting of an invocation target (an [`EventTarget`](#27-interface-eventtarget) object), an invocation-target-in-shadow-tree (a boolean), a shadow-adjusted target (a [potential event target](#22-interface-event)), a relatedTarget (a [potential event target](#22-interface-event)), a touch target list (a [list](infra-spec-whatwg-org.md#51-lists) of [potential event targets](#22-interface-event)), a root-of-closed-tree (a boolean), and a slot-in-closed-tree (a boolean). A [path](#22-interface-event) is initially the empty list.

`event = new Event(type [, eventInitDict])`

Returns a new event whose [`type`](#22-interface-event) attribute value is set to type. The eventInitDict argument allows for setting the [`bubbles`](#22-interface-event) and [`cancelable`](#22-interface-event) attributes via object members of the same name.

`` event . `type` ``

Returns the type of event, e.g. "`click`", "`hashchange`", or "`submit`".

`` event . `target` ``

Returns the object to which event is [dispatched](#29-dispatching-events) (its [target](#22-interface-event)).

`` event . `currentTarget` ``

Returns the object whose [event listener](#27-interface-eventtarget)’s [callback](#27-interface-eventtarget) is currently being invoked.

`` event . `composedPath()` ``

Returns the [invocation target](#22-interface-event) objects of event’s [path](#22-interface-event) (objects on which listeners will be invoked), except for any [nodes](#42-node-tree) in [shadow trees](#422-shadow-tree) of which the [shadow root](#48-interface-shadowroot)’s [mode](#48-interface-shadowroot) is "`closed`" that are not reachable from event’s [`currentTarget`](#22-interface-event).

`` event . `eventPhase` ``

Returns the [event](#22-interface-event)’s phase, which is one of [`NONE`](#22-interface-event), [`CAPTURING_PHASE`](#22-interface-event), [`AT_TARGET`](#22-interface-event), and [`BUBBLING_PHASE`](#22-interface-event).

`event . stopPropagation()`

When [dispatched](#29-dispatching-events) in a [tree](#11-trees), invoking this method prevents event from reaching any objects other than the current object.

`event . stopImmediatePropagation()`

Invoking this method prevents event from reaching any registered [event listeners](#27-interface-eventtarget) after the current one finishes running and, when [dispatched](#29-dispatching-events) in a [tree](#11-trees), also prevents event from reaching any other objects.

`` event . `bubbles` ``

Returns true or false depending on how event was initialized. True if event goes through its [target](#22-interface-event)’s [ancestors](#11-trees) in reverse [tree order](#11-trees); otherwise false.

`` event . `cancelable` ``

Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was [dispatched](#29-dispatching-events), can be canceled by invoking the [`preventDefault()`](#22-interface-event) method.

`event . preventDefault()`

If invoked when the [`cancelable`](#22-interface-event) attribute value is true, and while executing a listener for the event with [`passive`](#27-interface-eventtarget) set to false, signals to the operation that caused event to be [dispatched](#29-dispatching-events) that it needs to be canceled.

`` event . `defaultPrevented` ``

Returns true if [`preventDefault()`](#22-interface-event) was invoked successfully to indicate cancelation; otherwise false.

`` event . `composed` ``

Returns true or false depending on how event was initialized. True if event invokes listeners past a [`ShadowRoot`](#48-interface-shadowroot) [node](#42-node-tree) that is the [root](#11-trees) of its [target](#22-interface-event); otherwise false.

`` event . `isTrusted` ``

Returns true if event was [dispatched](#29-dispatching-events) by the user agent, and false otherwise.

`` event . `timeStamp` ``

Returns the event’s timestamp as the number of milliseconds measured relative to the occurrence.

The `type` attribute must return the value it was initialized to. When an [event](#22-interface-event) is created the attribute must be initialized to the empty string.

The `target` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [target](#22-interface-event).

The `srcElement` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [target](#22-interface-event).

The `currentTarget` attribute must return the value it was initialized to. When an [event](#22-interface-event) is created the attribute must be initialized to null.

The `composedPath()` method steps are:
1. Let composedPath be an empty [list](infra-spec-whatwg-org.md#51-lists).
2. Let path be [this](https://webidl.spec.whatwg.org/#this)’s [path](#22-interface-event).
3. If path [is empty](infra-spec-whatwg-org.md#51-lists), then return composedPath.
4. Let currentTarget be [this](https://webidl.spec.whatwg.org/#this)’s [`currentTarget`](#22-interface-event) attribute value.
5. [Assert](infra-spec-whatwg-org.md#310-assertions): currentTarget is an [`EventTarget`](#27-interface-eventtarget) object.
6. [Append](infra-spec-whatwg-org.md#51-lists) currentTarget to composedPath.
7. Let currentTargetIndex be 0.
8. Let currentTargetHiddenSubtreeLevel be 0.
9. Let index be path’s [size](infra-spec-whatwg-org.md#51-lists) − 1.
10. While index is greater than or equal to 0:
    1. If path\[index\]'s [root-of-closed-tree](#22-interface-event) is true, then increase currentTargetHiddenSubtreeLevel by 1.
    2. If path\[index\]'s [invocation target](#22-interface-event) is currentTarget, then set currentTargetIndex to index and [break](infra-spec-whatwg-org.md#39-iteration).
    3. If path\[index\]'s [slot-in-closed-tree](#22-interface-event) is true, then decrease currentTargetHiddenSubtreeLevel by 1.
    4. Decrease index by 1.
11. Let currentHiddenLevel and maxHiddenLevel be currentTargetHiddenSubtreeLevel.
12. Set index to currentTargetIndex − 1.
13. While index is greater than or equal to 0:
    1. If path\[index\]'s [root-of-closed-tree](#22-interface-event) is true, then increase currentHiddenLevel by 1.
    2. If currentHiddenLevel is less than or equal to maxHiddenLevel, then [prepend](infra-spec-whatwg-org.md#51-lists) path\[index\]'s [invocation target](#22-interface-event) to composedPath.
    3. If path\[index\]'s [slot-in-closed-tree](#22-interface-event) is true:
       1. Decrease currentHiddenLevel by 1.
       2. If currentHiddenLevel is less than maxHiddenLevel, then set maxHiddenLevel to currentHiddenLevel.
    4. Decrease index by 1.
14. Set currentHiddenLevel and maxHiddenLevel to currentTargetHiddenSubtreeLevel.
15. Set index to currentTargetIndex + 1.
16. While index is less than path’s [size](infra-spec-whatwg-org.md#51-lists):
    1. If path\[index\]'s [slot-in-closed-tree](#22-interface-event) is true, then increase currentHiddenLevel by 1.
    2. If currentHiddenLevel is less than or equal to maxHiddenLevel, then [append](infra-spec-whatwg-org.md#51-lists) path\[index\]'s [invocation target](#22-interface-event) to composedPath.
    3. If path\[index\]'s [root-of-closed-tree](#22-interface-event) is true:
       1. Decrease currentHiddenLevel by 1.
       2. If currentHiddenLevel is less than maxHiddenLevel, then set maxHiddenLevel to currentHiddenLevel.
    4. Increase index by 1.
17. Return composedPath.

The `eventPhase` attribute must return the value it was initialized to, which must be one of the following:

`NONE` (numeric value 0)

[Events](#22-interface-event) not currently [dispatched](#29-dispatching-events) are in this phase.

`CAPTURING_PHASE` (numeric value 1)

When an [event](#22-interface-event) is [dispatched](#29-dispatching-events) to an object that [participates](#11-trees) in a [tree](#11-trees) it will be in this phase before it reaches its [target](#22-interface-event).

`AT_TARGET` (numeric value 2)

When an [event](#22-interface-event) is [dispatched](#29-dispatching-events) it will be in this phase on its [target](#22-interface-event).

`BUBBLING_PHASE` (numeric value 3)

When an [event](#22-interface-event) is [dispatched](#29-dispatching-events) to an object that [participates](#11-trees) in a [tree](#11-trees) it will be in this phase after it reaches its [target](#22-interface-event).

Initially the attribute must be initialized to [`NONE`](#22-interface-event).

---

Each [event](#22-interface-event) has the following associated flags that are all initially unset:
- stop propagation flag
- stop immediate propagation flag
- canceled flag
- in passive listener flag
- composed flag
- initialized flag
- dispatch flag

The `stopPropagation()` method steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [stop propagation flag](#22-interface-event).

The `cancelBubble` getter steps are to return true if [this](https://webidl.spec.whatwg.org/#this)’s [stop propagation flag](#22-interface-event) is set; otherwise false.

The [`cancelBubble`](#22-interface-event) setter steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [stop propagation flag](#22-interface-event) if the given value is true; otherwise do nothing.

The `stopImmediatePropagation()` method steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [stop propagation flag](#22-interface-event) and [this](https://webidl.spec.whatwg.org/#this)’s [stop immediate propagation flag](#22-interface-event).

The `bubbles` and `cancelable` attributes must return the values they were initialized to.

To set the canceled flag, given an [event](#22-interface-event) event, if event’s [`cancelable`](#22-interface-event) attribute value is true and event’s [in passive listener flag](#22-interface-event) is unset, then set event’s [canceled flag](#22-interface-event), and do nothing otherwise.

The `returnValue` getter steps are to return false if [this](https://webidl.spec.whatwg.org/#this)’s [canceled flag](#22-interface-event) is set; otherwise true.

The [`returnValue`](#22-interface-event) setter steps are to [set the canceled flag](#22-interface-event) with [this](https://webidl.spec.whatwg.org/#this) if the given value is false; otherwise do nothing.

The `preventDefault()` method steps are to [set the canceled flag](#22-interface-event) with [this](https://webidl.spec.whatwg.org/#this).

> [!note]
> There are scenarios where invoking [`preventDefault()`](#22-interface-event) has no effect. User agents are encouraged to log the precise cause in a developer console, to aid debugging.

The `defaultPrevented` getter steps are to return true if [this](https://webidl.spec.whatwg.org/#this)’s [canceled flag](#22-interface-event) is set; otherwise false.

The `composed` getter steps are to return true if [this](https://webidl.spec.whatwg.org/#this)’s [composed flag](#22-interface-event) is set; otherwise false.

---

The `isTrusted` attribute must return the value it was initialized to. When an [event](#22-interface-event) is created the attribute must be initialized to false.

> [!note]
> [`isTrusted`](#22-interface-event) is a convenience that indicates whether an [event](#22-interface-event) is [dispatched](#29-dispatching-events) by the user agent (as opposed to using [`dispatchEvent()`](#27-interface-eventtarget)). The sole legacy exception is [`click()`](html-spec-whatwg-org.md#65-activation-behavior-of-elements), which causes the user agent to dispatch an [event](#22-interface-event) whose [`isTrusted`](#22-interface-event) attribute is initialized to false.

The `timeStamp` attribute must return the value it was initialized to.

---

To initialize an event, with type, bubbles, and cancelable, run these steps:
1. Set event’s [initialized flag](#22-interface-event).
2. Unset event’s [stop propagation flag](#22-interface-event), [stop immediate propagation flag](#22-interface-event), and [canceled flag](#22-interface-event).
3. Set event’s [`isTrusted`](#22-interface-event) attribute to false.
4. Set event’s [target](#22-interface-event) to null.
5. Set event’s [`type`](#22-interface-event) attribute to type.
6. Set event’s [`bubbles`](#22-interface-event) attribute to bubbles.
7. Set event’s [`cancelable`](#22-interface-event) attribute to cancelable.

The `initEvent(type, bubbles, cancelable)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this)’s [dispatch flag](#22-interface-event) is set, then return.
2. [Initialize](#22-interface-event) [this](https://webidl.spec.whatwg.org/#this) with type, bubbles, and cancelable.

> [!note]
> [`initEvent()`](#22-interface-event) is redundant with [event](#22-interface-event) constructors and incapable of setting [`composed`](#22-interface-event). It has to be supported for legacy content.

### 2.3. Legacy extensions to the [`Window`](html-spec-whatwg-org.md#722-the-window-object) interface

```webidl
partial interface Window {
  [Replaceable] readonly attribute (Event or undefined) event; // legacy
};

```

Each [`Window`](html-spec-whatwg-org.md#722-the-window-object) object has an associated current event (undefined or an [`Event`](#22-interface-event) object). Unless stated otherwise it is undefined.

The `event` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [current event](#23-legacy-extensions-to-the-window-interface).

> [!note]
> Web developers are strongly encouraged to instead rely on the [`Event`](#22-interface-event) object passed to event listeners, as that will result in more portable code. This attribute is not available in workers or worklets, and is inaccurate for events dispatched in [shadow trees](#422-shadow-tree).

### 2.4. Interface [`CustomEvent`](#24-interface-customevent)

```webidl
[Exposed=*]
interface CustomEvent : Event {
  constructor(DOMString type, optional CustomEventInit eventInitDict = {});

  readonly attribute any detail;

  undefined initCustomEvent(DOMString type, optional boolean bubbles = false, optional boolean cancelable = false, optional any detail = null); // legacy
};

dictionary CustomEventInit : EventInit {
  any detail = null;
};

```

[Events](#22-interface-event) using the [`CustomEvent`](#24-interface-customevent) interface can be used to carry custom data.

`event = new CustomEvent(type [, eventInitDict])`

Works analogously to the constructor for [`Event`](#22-interface-event) except that the eventInitDict argument now allows for setting the [`detail`](#24-interface-customevent) attribute too.

`` event . `detail` ``

Returns any custom data event was created with. Typically used for synthetic events.

The `detail` attribute must return the value it was initialized to.

The `initCustomEvent(type, bubbles, cancelable, detail)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this)’s [dispatch flag](#22-interface-event) is set, then return.
2. [Initialize](#22-interface-event) [this](https://webidl.spec.whatwg.org/#this) with type, bubbles, and cancelable.
3. Set [this](https://webidl.spec.whatwg.org/#this)’s [`detail`](#24-interface-customevent) attribute to detail.

### 2.5. Constructing events

[Specifications](#1-infrastructure) may define event constructing steps for all or some [events](#22-interface-event). The algorithm is passed an [event](#22-interface-event) event and an [`EventInit`](#22-interface-event) eventInitDict as indicated in the [inner event creation steps](#25-constructing-events).

> [!note]
> This construct can be used by [`Event`](#22-interface-event) subclasses that have a more complex structure than a simple 1:1 mapping between their initializing dictionary members and IDL attributes.

When a constructor of the [`Event`](#22-interface-event) interface, or of an interface that inherits from the [`Event`](#22-interface-event) interface, is invoked, these steps must be run, given the arguments type and eventInitDict:
1. Let event be the result of running the [inner event creation steps](#25-constructing-events) with this interface, null, now, and eventInitDict.
2. Initialize event’s [`type`](#22-interface-event) attribute to type.
3. Return event.

To create an event using eventInterface, which must be either [`Event`](#22-interface-event) or an interface that inherits from it, and optionally given a [realm](https://tc39.es/ecma262/#realm) realm, run these steps:
1. If realm is not given, then set it to null.
2. Let dictionary be the result of [converting](https://webidl.spec.whatwg.org/#dfn-convert-ecmascript-to-idl-value) the JavaScript value undefined to the dictionary type accepted by eventInterface’s constructor. (This dictionary type will either be [`EventInit`](#22-interface-event) or a dictionary that inherits from it.)

   > [!warning]
   > This does not work if members are required; see [whatwg/dom#600](https://github.com/whatwg/dom/issues/600).

3. Let event be the result of running the [inner event creation steps](#25-constructing-events) with eventInterface, realm, the time of the occurrence that the event is signaling, and dictionary.

   > [!example]
   > In macOS the time of the occurrence for input actions is available via the `timestamp` property of `NSEvent` objects.

4. Initialize event’s [`isTrusted`](#22-interface-event) attribute to true.
5. Return event.

> [!note]
> [Create an event](#25-constructing-events) is meant to be used by other specifications which need to separately [create](#25-constructing-events) and [dispatch](#29-dispatching-events) events, instead of simply [firing](#210-firing-events) them. It ensures the event’s attributes are initialized to the correct defaults.

The inner event creation steps, given an eventInterface, realm, time, and dictionary, are as follows:
1. Let event be the result of creating a new object using eventInterface. If realm is non-null, then use that realm; otherwise, use the default behavior defined in Web IDL.

   > [!warning]
   > As of the time of this writing Web IDL does not yet define any default behavior; see [whatwg/webidl#135](https://github.com/whatwg/webidl/issues/135).

2. Set event’s [initialized flag](#22-interface-event).
3. Initialize event’s [`timeStamp`](#22-interface-event) attribute to the [relative high resolution coarse time](https://w3c.github.io/hr-time/#dfn-relative-high-resolution-coarse-time) given time and event’s [relevant global object](html-spec-whatwg-org.md#81334-relevant).
4. [For each](infra-spec-whatwg-org.md#52-maps) member → value of dictionary: if event has an attribute whose [identifier](https://webidl.spec.whatwg.org/#dfn-identifier) is member, then initialize that attribute to value.
5. Run the [event constructing steps](#25-constructing-events) with event and dictionary.
6. Return event.

### 2.6. Defining event interfaces

In general, when defining a new interface that inherits from [`Event`](#22-interface-event) please always ask feedback from the [WHATWG](https://whatwg.org/) or the [W3C WebApps WG](https://www.w3.org/2008/webapps/) community.

The [`CustomEvent`](#24-interface-customevent) interface can be used as starting point. However, do not introduce any `init*Event()` methods as they are redundant with constructors. Interfaces that inherit from the [`Event`](#22-interface-event) interface that have such a method only have it for historical reasons.

### 2.7. Interface [`EventTarget`](#27-interface-eventtarget)

```webidl
[Exposed=*]
interface EventTarget {
  constructor();

  undefined addEventListener(DOMString type, EventListener? callback, optional (AddEventListenerOptions or boolean) options = {});
  undefined removeEventListener(DOMString type, EventListener? callback, optional (EventListenerOptions or boolean) options = {});
  boolean dispatchEvent(Event event);
};

callback interface EventListener {
  undefined handleEvent(Event event);
};

dictionary EventListenerOptions {
  boolean capture = false;
};

dictionary AddEventListenerOptions : EventListenerOptions {
  boolean passive;
  boolean once = false;
  AbortSignal signal;
};

```

An [`EventTarget`](#27-interface-eventtarget) object represents a target to which an [event](#22-interface-event) can be [dispatched](#29-dispatching-events) when something has occurred.

Each [`EventTarget`](#27-interface-eventtarget) object has an associated event listener list (a [list](infra-spec-whatwg-org.md#51-lists) of zero or more [event listeners](#27-interface-eventtarget)). It is initially the empty list.

An event listener can be used to observe a specific [event](#22-interface-event) and consists of:
- type (a string)
- callback (null or an [`EventListener`](#27-interface-eventtarget) object)
- capture (a boolean, initially false)
- passive (null or a boolean, initially null)
- once (a boolean, initially false)
- signal (null or an [`AbortSignal`](#32-interface-abortsignal) object)
- removed (a boolean for bookkeeping purposes, initially false)

> [!note]
> Although [callback](#27-interface-eventtarget) is an [`EventListener`](#27-interface-eventtarget) object, an [event listener](#27-interface-eventtarget) is a broader concept as can be seen above.

Each [`EventTarget`](#27-interface-eventtarget) object also has an associated get the parent algorithm, which takes an [event](#22-interface-event) event, and returns an [`EventTarget`](#27-interface-eventtarget) object. Unless specified otherwise it returns null.

> [!note]
> [Nodes](#42-node-tree), [shadow roots](#48-interface-shadowroot), and [documents](#45-interface-document) override the [get the parent](#27-interface-eventtarget) algorithm.

Each [`EventTarget`](#27-interface-eventtarget) object can have an associated activation behavior algorithm. The [activation behavior](#27-interface-eventtarget) algorithm is passed an [event](#22-interface-event), as indicated in the [dispatch](#29-dispatching-events) algorithm.

> [!note]
> This exists because user agents perform certain actions for certain [`EventTarget`](#27-interface-eventtarget) objects, e.g., the [`area`](html-spec-whatwg-org.md#4813-the-area-element) element, in response to synthetic [`MouseEvent`](https://w3c.github.io/pointerevents/#dom-mouseevent) [events](#22-interface-event) whose [`type`](#22-interface-event) attribute is `click`. Web compatibility prevented it from being removed and it is now the enshrined way of defining an activation of something. [\[HTML\]](#normative-references)

Each [`EventTarget`](#27-interface-eventtarget) object that has [activation behavior](#27-interface-eventtarget), can additionally have both (not either) a legacy-pre-activation behavior algorithm and a legacy-canceled-activation behavior algorithm.

> [!note]
> These algorithms only exist for checkbox and radio [`input`](html-spec-whatwg-org.md#4105-the-input-element) elements and are not to be used for anything else. [\[HTML\]](#normative-references)

`target = new EventTarget();`

Creates a new [`EventTarget`](#27-interface-eventtarget) object, which can be used by developers to [dispatch](#29-dispatching-events) and listen for [events](#22-interface-event).

`target . addEventListener(type, callback [, options])`

Appends an [event listener](#27-interface-eventtarget) for [events](#22-interface-event) whose [`type`](#22-interface-event) attribute value is type. The callback argument sets the [callback](#27-interface-eventtarget) that will be invoked when the [event](#22-interface-event) is [dispatched](#29-dispatching-events).

The options argument sets listener-specific options. For compatibility this can be a boolean, in which case the method behaves exactly as if the value was specified as options’s [`capture`](#27-interface-eventtarget).

When set to true, options’s [`capture`](#27-interface-eventtarget) prevents [callback](#27-interface-eventtarget) from being invoked when the [event](#22-interface-event)’s [`eventPhase`](#22-interface-event) attribute value is [`BUBBLING_PHASE`](#22-interface-event). When false (or not present), [callback](#27-interface-eventtarget) will not be invoked when [event](#22-interface-event)’s [`eventPhase`](#22-interface-event) attribute value is [`CAPTURING_PHASE`](#22-interface-event). Either way, [callback](#27-interface-eventtarget) will be invoked if [event](#22-interface-event)’s [`eventPhase`](#22-interface-event) attribute value is [`AT_TARGET`](#22-interface-event).

When set to true, options’s [`passive`](#27-interface-eventtarget) indicates that the [callback](#27-interface-eventtarget) will not cancel the event by invoking [`preventDefault()`](#22-interface-event). This is used to enable performance optimizations described in [§ 2.8 Observing event listeners](#28-observing-event-listeners).

When set to true, options’s [`once`](#27-interface-eventtarget) indicates that the [callback](#27-interface-eventtarget) will only be invoked once after which the event listener will be removed.

If an [`AbortSignal`](#32-interface-abortsignal) is passed for options’s [`signal`](#27-interface-eventtarget), then the event listener will be removed when signal is aborted.

The [event listener](#27-interface-eventtarget) is appended to target’s [event listener list](#27-interface-eventtarget) and is not appended if it has the same [type](#27-interface-eventtarget), [callback](#27-interface-eventtarget), and [capture](#27-interface-eventtarget).

`target . removeEventListener(type, callback [, options])`

Removes the [event listener](#27-interface-eventtarget) in target’s [event listener list](#27-interface-eventtarget) with the same type, callback, and options.

`target . dispatchEvent(event)`

[Dispatches](#29-dispatching-events) a synthetic event event to target and returns true if either event’s [`cancelable`](#22-interface-event) attribute value is false or its [`preventDefault()`](#22-interface-event) method was not invoked; otherwise false.

To flatten options, run these steps:
1. If options is a boolean, then return options.
2. Return options\["[`capture`](#27-interface-eventtarget)"\].

To flatten more options, run these steps:
1. Let capture be the result of [flattening](#27-interface-eventtarget) options.
2. Let once be false.
3. Let passive and signal be null.
4. If options is a [dictionary](https://webidl.spec.whatwg.org/#dfn-dictionary):
   1. Set once to options\["[`once`](#27-interface-eventtarget)"\].
   2. If options\["[`passive`](#27-interface-eventtarget)"\] [exists](infra-spec-whatwg-org.md#52-maps), then set passive to options\["[`passive`](#27-interface-eventtarget)"\].
   3. If options\["[`signal`](#27-interface-eventtarget)"\] [exists](infra-spec-whatwg-org.md#52-maps), then set signal to options\["[`signal`](#27-interface-eventtarget)"\].
5. Return capture, passive, once, and signal.

The `new EventTarget()` constructor steps are to do nothing.

> [!note]
> Because of the defaults stated elsewhere, the returned [`EventTarget`](#27-interface-eventtarget)’s [get the parent](#27-interface-eventtarget) algorithm will return null, and it will have no [activation behavior](#27-interface-eventtarget), [legacy-pre-activation behavior](#27-interface-eventtarget), or [legacy-canceled-activation behavior](#27-interface-eventtarget).

> [!note]
> In the future we could allow custom [get the parent](#27-interface-eventtarget) algorithms. If this would be useful, support [issue #583](https://github.com/whatwg/dom/issues/583). For now, all author-created [`EventTarget`](#27-interface-eventtarget)s do not participate in a tree structure.

The default passive value, given an event type type and an [`EventTarget`](#27-interface-eventtarget) eventTarget, is determined as follows:
1. Return true if all of the following are true:
   - type is one of "`touchstart`", "`touchmove`", "`wheel`", or "`mousewheel`". [\[TOUCH-EVENTS\]](#normative-references) [\[UIEVENTS\]](#normative-references)
   - eventTarget is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object, or is a [node](#42-node-tree) whose [node document](#44-interface-node) is eventTarget, or is a [node](#42-node-tree) whose [node document](#44-interface-node)’s [document element](#421-document-tree) is eventTarget, or is a [node](#42-node-tree) whose [node document](#44-interface-node)’s [body element](html-spec-whatwg-org.md#317-dom-tree-accessors) is eventTarget. [\[HTML\]](#normative-references)
2. Return false.

To add an event listener, given an [`EventTarget`](#27-interface-eventtarget) object eventTarget and an [event listener](#27-interface-eventtarget) listener, run these steps:
1. If eventTarget is a [`ServiceWorkerGlobalScope`](https://w3c.github.io/ServiceWorker/#serviceworkerglobalscope) object, its [service worker](https://w3c.github.io/ServiceWorker/#serviceworkerglobalscope-service-worker)’s [script resource](https://w3c.github.io/ServiceWorker/#dfn-script-resource)’s [has ever been evaluated flag](https://w3c.github.io/ServiceWorker/#dfn-has-ever-been-evaluated-flag) is set, and listener’s [type](#27-interface-eventtarget) matches the [`type`](#22-interface-event) attribute value of any of the [service worker events](https://w3c.github.io/ServiceWorker/#dfn-service-worker-events), then [report a warning to the console](https://console.spec.whatwg.org/#report-a-warning-to-the-console) that this might not give the expected results. [\[SERVICE-WORKERS\]](#normative-references)
2. If listener’s [signal](#27-interface-eventtarget) is non-null and is [aborted](#32-interface-abortsignal), then return.
3. If listener’s [callback](#27-interface-eventtarget) is null, then return.
4. If listener’s [passive](#27-interface-eventtarget) is null, then set it to the [default passive value](#27-interface-eventtarget) given listener’s [type](#27-interface-eventtarget) and eventTarget.
5. If eventTarget’s [event listener list](#27-interface-eventtarget) does not [contain](infra-spec-whatwg-org.md#51-lists) an [event listener](#27-interface-eventtarget) whose [type](#27-interface-eventtarget) is listener’s [type](#27-interface-eventtarget), [callback](#27-interface-eventtarget) is listener’s [callback](#27-interface-eventtarget), and [capture](#27-interface-eventtarget) is listener’s [capture](#27-interface-eventtarget), then [append](infra-spec-whatwg-org.md#51-lists) listener to eventTarget’s [event listener list](#27-interface-eventtarget).
6. If listener’s [signal](#27-interface-eventtarget) is non-null, then [add the following](#32-interface-abortsignal) abort steps to it:
   1. [Remove an event listener](#27-interface-eventtarget) with eventTarget and listener.

> [!note]
> The [add an event listener](#27-interface-eventtarget) concept exists to ensure [event handlers](html-spec-whatwg-org.md#8181-event-handlers) use the same code path. [\[HTML\]](#normative-references)

The `addEventListener(type, callback, options)` method steps are:
1. Let capture, passive, once, and signal be the result of [flattening more](#27-interface-eventtarget) options.
2. [Add an event listener](#27-interface-eventtarget) with [this](https://webidl.spec.whatwg.org/#this) and an [event listener](#27-interface-eventtarget) whose [type](#27-interface-eventtarget) is type, [callback](#27-interface-eventtarget) is callback, [capture](#27-interface-eventtarget) is capture, [passive](#27-interface-eventtarget) is passive, [once](#27-interface-eventtarget) is once, and [signal](#27-interface-eventtarget) is signal.

To remove an event listener, given an [`EventTarget`](#27-interface-eventtarget) object eventTarget and an [event listener](#27-interface-eventtarget) listener, run these steps:
1. If eventTarget is a [`ServiceWorkerGlobalScope`](https://w3c.github.io/ServiceWorker/#serviceworkerglobalscope) object and its [service worker](https://w3c.github.io/ServiceWorker/#serviceworkerglobalscope-service-worker)’s [set of event types to handle](https://w3c.github.io/ServiceWorker/#dfn-set-of-event-types-to-handle) [contains](infra-spec-whatwg-org.md#51-lists) listener’s [type](#27-interface-eventtarget), then [report a warning to the console](https://console.spec.whatwg.org/#report-a-warning-to-the-console) that this might not give the expected results. [\[SERVICE-WORKERS\]](#normative-references)
2. Set listener’s [removed](#27-interface-eventtarget) to true and [remove](infra-spec-whatwg-org.md#51-lists) listener from eventTarget’s [event listener list](#27-interface-eventtarget).

> [!note]
> HTML needs this to define event handlers. [\[HTML\]](#normative-references)

To remove all event listeners, given an [`EventTarget`](#27-interface-eventtarget) object eventTarget: [for each](infra-spec-whatwg-org.md#51-lists) listener of eventTarget’s [event listener list](#27-interface-eventtarget): [remove an event listener](#27-interface-eventtarget) with eventTarget and listener.

> [!note]
> HTML needs this to define `document.open()`. [\[HTML\]](#normative-references)

The `removeEventListener(type, callback, options)` method steps are:
1. Let capture be the result of [flattening](#27-interface-eventtarget) options.
2. If [this](https://webidl.spec.whatwg.org/#this)’s [event listener list](#27-interface-eventtarget) [contains](infra-spec-whatwg-org.md#51-lists) an [event listener](#27-interface-eventtarget) whose [type](#27-interface-eventtarget) is type, [callback](#27-interface-eventtarget) is callback, and [capture](#27-interface-eventtarget) is capture, then [remove an event listener](#27-interface-eventtarget) with [this](https://webidl.spec.whatwg.org/#this) and that [event listener](#27-interface-eventtarget).

> [!note]
> The event listener list will not contain multiple event listeners with equal type, callback, and capture, as [add an event listener](#27-interface-eventtarget) prevents that.

The `dispatchEvent(event)` method steps are:
1. If event’s [dispatch flag](#22-interface-event) is set, or if its [initialized flag](#22-interface-event) is not set, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidStateError`](https://webidl.spec.whatwg.org/#invalidstateerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Initialize event’s [`isTrusted`](#22-interface-event) attribute to false.
3. Return the result of [dispatching](#29-dispatching-events) event to [this](https://webidl.spec.whatwg.org/#this).

### 2.8. Observing event listeners

In general, developers do not expect the presence of an [event listener](#27-interface-eventtarget) to be observable. The impact of an [event listener](#27-interface-eventtarget) is determined by its [callback](#27-interface-eventtarget). That is, a developer adding a no-op [event listener](#27-interface-eventtarget) would not expect it to have any side effects.

Unfortunately, some event APIs have been designed such that implementing them efficiently requires observing [event listeners](#27-interface-eventtarget). This can make the presence of listeners observable in that even empty listeners can have a dramatic performance impact on the behavior of the application. For example, touch and wheel events which can be used to block asynchronous scrolling. In some cases this problem can be mitigated by specifying the event to be [`cancelable`](#22-interface-event) only when there is at least one non-[`passive`](#27-interface-eventtarget) listener. For example, non-[`passive`](#27-interface-eventtarget) [`TouchEvent`](https://w3c.github.io/touch-events/#idl-def-touchevent) listeners must block scrolling, but if all listeners are [`passive`](#27-interface-eventtarget) then scrolling can be allowed to start [in parallel](html-spec-whatwg-org.md#211-parallelism) by making the [`TouchEvent`](https://w3c.github.io/touch-events/#idl-def-touchevent) uncancelable (so that calls to [`preventDefault()`](#22-interface-event) are ignored). So code dispatching an event is able to observe the absence of non-[`passive`](#27-interface-eventtarget) listeners, and use that to clear the [`cancelable`](#22-interface-event) property of the event being dispatched.

Ideally, any new event APIs are defined such that they do not need this property. (Use [whatwg/dom](https://github.com/whatwg/dom/issues) for discussion.)

To legacy-obtain service worker fetch event listener callbacks given a [`ServiceWorkerGlobalScope`](https://w3c.github.io/ServiceWorker/#serviceworkerglobalscope) global, run these steps. They return a [list](infra-spec-whatwg-org.md#51-lists) of [`EventListener`](#27-interface-eventtarget) objects.
1. Let callbacks be « ».
2. [For each](infra-spec-whatwg-org.md#51-lists) listener of global’s [event listener list](#27-interface-eventtarget): if listener’s [type](#27-interface-eventtarget) is "`fetch`" and listener’s [callback](#27-interface-eventtarget) is non-null, then [append](infra-spec-whatwg-org.md#51-lists) listener’s [callback](#27-interface-eventtarget) to callbacks.
3. Return callbacks.

### 2.9. Dispatching events

To dispatch an [event](#22-interface-event) event to an [`EventTarget`](#27-interface-eventtarget) object target, with an optional legacy target override flag and an optional legacyOutputDidListenersThrowFlag:
1. Set event’s [dispatch flag](#22-interface-event).
2. Let targetOverride be target, if legacy target override flag is not given, and target’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object) otherwise. [\[HTML\]](#normative-references)

   > [!note]
   > legacy target override flag is only used by HTML and only when target is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object.

3. Let activationTarget be null.
4. Let relatedTarget be the result of [retargeting](#48-interface-shadowroot) event’s [relatedTarget](#22-interface-event) against target.
5. Let clearTargets be false.
6. If target is not relatedTarget or target is event’s [relatedTarget](#22-interface-event):
   1. Let touchTargets be a new [list](infra-spec-whatwg-org.md#51-lists).
   2. [For each](infra-spec-whatwg-org.md#51-lists) touchTarget of event’s [touch target list](#22-interface-event): [append](infra-spec-whatwg-org.md#51-lists) the result of [retargeting](#48-interface-shadowroot) touchTarget against target to touchTargets.
   3. [Append to an event path](#29-dispatching-events) with event, target, targetOverride, relatedTarget, touchTargets, and false.
   4. Let isActivationEvent be true, if event is a [`MouseEvent`](https://w3c.github.io/pointerevents/#dom-mouseevent) object and event’s [`type`](#22-interface-event) attribute is "`click`"; otherwise false.
   5. If isActivationEvent is true and target has [activation behavior](#27-interface-eventtarget), then set activationTarget to target.
   6. Let slottable be target, if target is a [slottable](#4222-slottables) and is [assigned](#4222-slottables), and null otherwise.
   7. Let slotInClosedTree be false.
   8. Let parent be the result of invoking target’s [get the parent](#27-interface-eventtarget) with event.
   9. While parent is non-null:
      1. If slottable is non-null:
         1. Assert: parent is a [slot](#4221-slots).
         2. Set slottable to null.
         3. If parent’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot) whose [mode](#48-interface-shadowroot) is "`closed`", then set slotInClosedTree to true.
      2. If parent is a [slottable](#4222-slottables) and is [assigned](#4222-slottables), then set slottable to parent.
      3. Let relatedTarget be the result of [retargeting](#48-interface-shadowroot) event’s [relatedTarget](#22-interface-event) against parent.
      4. Let touchTargets be a new [list](infra-spec-whatwg-org.md#51-lists).
      5. [For each](infra-spec-whatwg-org.md#51-lists) touchTarget of event’s [touch target list](#22-interface-event): [append](infra-spec-whatwg-org.md#51-lists) the result of [retargeting](#48-interface-shadowroot) touchTarget against parent to touchTargets.
      6. If parent is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object, or parent is a [node](#42-node-tree) and target’s [root](#11-trees) is a [shadow-including inclusive ancestor](#48-interface-shadowroot) of parent:
         1. If isActivationEvent is true, event’s [`bubbles`](#22-interface-event) attribute is true, activationTarget is null, and parent has [activation behavior](#27-interface-eventtarget), then set activationTarget to parent.
         2. [Append to an event path](#29-dispatching-events) with event, parent, null, relatedTarget, touchTargets, and slotInClosedTree.
      7. Otherwise, if parent is relatedTarget, then set parent to null.
      8. Otherwise:
         1. Set target to parent.
         2. If isActivationEvent is true, activationTarget is null, and target has [activation behavior](#27-interface-eventtarget), then set activationTarget to target.
         3. [Append to an event path](#29-dispatching-events) with event, parent, target, relatedTarget, touchTargets, and slotInClosedTree.
      9. If parent is non-null, then set parent to the result of invoking parent’s [get the parent](#27-interface-eventtarget) with event.
      10. Set slotInClosedTree to false.
   10. Let clearTargetsItem be the last [event path item](#22-interface-event) in event’s [path](#22-interface-event) whose [shadow-adjusted target](#22-interface-event) is non-null.
   11. If clearTargetsItem’s [shadow-adjusted target](#22-interface-event), clearTargetsItem’s [relatedTarget](#22-interface-event), or an [`EventTarget`](#27-interface-eventtarget) object in clearTargetsItem’s [touch target list](#22-interface-event) is a [node](#42-node-tree) whose [root](#11-trees) is a [shadow root](#48-interface-shadowroot): set clearTargets to true.
   12. If activationTarget is non-null and activationTarget has [legacy-pre-activation behavior](#27-interface-eventtarget), then run activationTarget’s [legacy-pre-activation behavior](#27-interface-eventtarget).
   13. [For each](infra-spec-whatwg-org.md#51-lists) item of event’s [path](#22-interface-event), in reverse order:
       1. If item’s [shadow-adjusted target](#22-interface-event) is non-null, then set event’s [`eventPhase`](#22-interface-event) attribute to [`AT_TARGET`](#22-interface-event).
       2. Otherwise, set event’s [`eventPhase`](#22-interface-event) attribute to [`CAPTURING_PHASE`](#22-interface-event).
       3. [Invoke](#29-dispatching-events) with item, event, "`capturing`", and legacyOutputDidListenersThrowFlag if given.
   14. [For each](infra-spec-whatwg-org.md#51-lists) item of event’s [path](#22-interface-event):
       1. If item’s [shadow-adjusted target](#22-interface-event) is non-null, then set event’s [`eventPhase`](#22-interface-event) attribute to [`AT_TARGET`](#22-interface-event).
       2. Otherwise:
          1. If event’s [`bubbles`](#22-interface-event) attribute is false, then [continue](infra-spec-whatwg-org.md#39-iteration).
          2. Set event’s [`eventPhase`](#22-interface-event) attribute to [`BUBBLING_PHASE`](#22-interface-event).
       3. [Invoke](#29-dispatching-events) with item, event, "`bubbling`", and legacyOutputDidListenersThrowFlag if given.
7. Set event’s [`eventPhase`](#22-interface-event) attribute to [`NONE`](#22-interface-event).
8. Set event’s [`currentTarget`](#22-interface-event) attribute to null.
9. Set event’s [path](#22-interface-event) to the empty list.
10. Unset event’s [dispatch flag](#22-interface-event), [stop propagation flag](#22-interface-event), and [stop immediate propagation flag](#22-interface-event).
11. If clearTargets is true:
    1. Set event’s [target](#22-interface-event) to null.
    2. Set event’s [relatedTarget](#22-interface-event) to null.
    3. Set event’s [touch target list](#22-interface-event) to the empty list.
12. If activationTarget is non-null:
    1. If event’s [canceled flag](#22-interface-event) is unset, then run activationTarget’s [activation behavior](#27-interface-eventtarget) with event.
    2. Otherwise, if activationTarget has [legacy-canceled-activation behavior](#27-interface-eventtarget), then run activationTarget’s [legacy-canceled-activation behavior](#27-interface-eventtarget).
13. Return false if event’s [canceled flag](#22-interface-event) is set; otherwise true.

To append to an event path, given an [event](#22-interface-event) event, an [`EventTarget`](#27-interface-eventtarget) object invocationTarget, a [potential event target](#22-interface-event) shadowAdjustedTarget, a [potential event target](#22-interface-event) relatedTarget, a [list](infra-spec-whatwg-org.md#51-lists) of [potential event targets](#22-interface-event) touchTargets, and a boolean slotInClosedTree:
1. Let invocationTargetInShadowTree be false.
2. If invocationTarget is a [node](#42-node-tree) and its [root](#11-trees) is a [shadow root](#48-interface-shadowroot), then set invocationTargetInShadowTree to true.
3. Let rootOfClosedTree be false.
4. If invocationTarget is a [shadow root](#48-interface-shadowroot) whose [mode](#48-interface-shadowroot) is "`closed`", then set rootOfClosedTree to true.
5. [Append](infra-spec-whatwg-org.md#51-lists) a new [event path item](#22-interface-event) to event’s [path](#22-interface-event) whose [invocation target](#22-interface-event) is invocationTarget, [invocation-target-in-shadow-tree](#22-interface-event) is invocationTargetInShadowTree, [shadow-adjusted target](#22-interface-event) is shadowAdjustedTarget, [relatedTarget](#22-interface-event) is relatedTarget, [touch target list](#22-interface-event) is touchTargets, [root-of-closed-tree](#22-interface-event) is rootOfClosedTree, and [slot-in-closed-tree](#22-interface-event) is slotInClosedTree.

To invoke, given an [event path item](#22-interface-event) pathItem, an [event](#22-interface-event) event, a string phase, and an optional legacyOutputDidListenersThrowFlag:
1. Let targetItem be pathItem.
2. While targetItem’s [shadow-adjusted target](#22-interface-event) is null: set targetItem to the [event path item](#22-interface-event) preceding targetItem in event’s [path](#22-interface-event).
3. Set event’s [target](#22-interface-event) to targetItem’s [shadow-adjusted target](#22-interface-event).
4. Set event’s [relatedTarget](#22-interface-event) to pathItem’s [relatedTarget](#22-interface-event).
5. Set event’s [touch target list](#22-interface-event) to pathItem’s [touch target list](#22-interface-event).
6. If event’s [stop propagation flag](#22-interface-event) is set, then return.
7. Initialize event’s [`currentTarget`](#22-interface-event) attribute to pathItem’s [invocation target](#22-interface-event).
8. Let listeners be a [clone](infra-spec-whatwg-org.md#51-lists) of event’s [`currentTarget`](#22-interface-event) attribute value’s [event listener list](#27-interface-eventtarget).

   > [!note]
   > This avoids [event listeners](#27-interface-eventtarget) added after this point from being run. Note that removal still has an effect due to the [removed](#27-interface-eventtarget) field.

9. Let invocationTargetInShadowTree be pathItem’s [invocation-target-in-shadow-tree](#22-interface-event).
10. Let found be the result of running [inner invoke](#29-dispatching-events) with event, listeners, phase, invocationTargetInShadowTree, and legacyOutputDidListenersThrowFlag if given.
11. If found is false and event’s [`isTrusted`](#22-interface-event) attribute is true:
    1. Let originalEventType be event’s [`type`](#22-interface-event) attribute value.
    2. If event’s [`type`](#22-interface-event) attribute value is a match for any of the strings in the first column in the following table, set event’s [`type`](#22-interface-event) attribute value to the string in the second column on the same row as the matching string, and return otherwise.

       | "`animationend`" | "`webkitAnimationEnd`" |
       | --- | --- |
       | "`animationiteration`" | "`webkitAnimationIteration`" |
       | "`animationstart`" | "`webkitAnimationStart`" |
       | "`transitionend`" | "`webkitTransitionEnd`" |

       Legacy event type

    3. [Inner invoke](#29-dispatching-events) with event, listeners, phase, invocationTargetInShadowTree, and legacyOutputDidListenersThrowFlag if given.
    4. Set event’s [`type`](#22-interface-event) attribute value to originalEventType.

To inner invoke, given an [event](#22-interface-event) event, a [list](infra-spec-whatwg-org.md#51-lists) of [event listeners](#27-interface-eventtarget) listeners, a string phase, a boolean invocationTargetInShadowTree, and an optional legacyOutputDidListenersThrowFlag:
1. Let found be false.
2. [For each](infra-spec-whatwg-org.md#51-lists) listener of listeners, whose [removed](#27-interface-eventtarget) is false:
   1. If event’s [`type`](#22-interface-event) attribute value is not listener’s [type](#27-interface-eventtarget), then [continue](infra-spec-whatwg-org.md#39-iteration).
   2. Set found to true.
   3. If phase is "`capturing`" and listener’s [capture](#27-interface-eventtarget) is false, then [continue](infra-spec-whatwg-org.md#39-iteration).
   4. If phase is "`bubbling`" and listener’s [capture](#27-interface-eventtarget) is true, then [continue](infra-spec-whatwg-org.md#39-iteration).
   5. If listener’s [once](#27-interface-eventtarget) is true, then [remove an event listener](#27-interface-eventtarget) given event’s [`currentTarget`](#22-interface-event) attribute value and listener.
   6. Let targetGlobal be event’s [`currentTarget`](#22-interface-event)’s [node document](#44-interface-node)’s [relevant global object](html-spec-whatwg-org.md#81334-relevant) if event’s [`currentTarget`](#22-interface-event) is a [node](#42-node-tree); otherwise event’s [`currentTarget`](#22-interface-event)’s [relevant global object](html-spec-whatwg-org.md#81334-relevant).
   7. Let listenerGlobal be listener [callback](#27-interface-eventtarget)’s [associated realm](https://webidl.spec.whatwg.org/#dfn-associated-realm)’s [global object](html-spec-whatwg-org.md#8133-realms-settings-objects-and-global-objects).
   8. If targetGlobal or listenerGlobal is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object whose [associated `Document`](html-spec-whatwg-org.md#722-the-window-object) is not [fully active](html-spec-whatwg-org.md#733-fully-active-documents), then [continue](infra-spec-whatwg-org.md#39-iteration).
   9. Let currentEvent be undefined.
   10. If listenerGlobal is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object:
       1. Set currentEvent to listenerGlobal’s [current event](#23-legacy-extensions-to-the-window-interface).
       2. If invocationTargetInShadowTree is false, then set listenerGlobal’s [current event](#23-legacy-extensions-to-the-window-interface) to event.
   11. If listener’s [passive](#27-interface-eventtarget) is true, then set event’s [in passive listener flag](#22-interface-event).
   12. If listenerGlobal is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object, then [record timing info for event listener](https://w3c.github.io/long-animation-frames/#record-timing-info-for-event-listener) given event and listener.
   13. [Call a user object’s operation](https://webidl.spec.whatwg.org/#call-a-user-objects-operation) with listener’s [callback](#27-interface-eventtarget), "`handleEvent`", « event », and event’s [`currentTarget`](#22-interface-event) attribute value. If this throws an exception exception:
       1. [Report](html-spec-whatwg-org.md#8146-runtime-script-errors) exception for listener’s [callback](#27-interface-eventtarget)’s corresponding JavaScript object’s [associated realm](https://webidl.spec.whatwg.org/#dfn-associated-realm)’s [global object](html-spec-whatwg-org.md#8133-realms-settings-objects-and-global-objects).
       2. Set legacyOutputDidListenersThrowFlag if given.

          > [!note]
          > The legacyOutputDidListenersThrowFlag is only used by Indexed Database API. [\[INDEXEDDB\]](#non-normative-references)

   14. Unset event’s [in passive listener flag](#22-interface-event).
   15. If listenerGlobal is a [`Window`](html-spec-whatwg-org.md#722-the-window-object) object, then set listenerGlobal’s [current event](#23-legacy-extensions-to-the-window-interface) to currentEvent.
   16. If event’s [stop immediate propagation flag](#22-interface-event) is set, then [break](infra-spec-whatwg-org.md#39-iteration).

3. Return found.

### 2.10. Firing events

To fire an event named e at target, optionally using an eventConstructor, with a description of how IDL attributes are to be initialized, and a legacy target override flag, run these steps:
1. If eventConstructor is not given, then let eventConstructor be [`Event`](#22-interface-event).
2. Let event be the result of [creating an event](#25-constructing-events) given eventConstructor, in the [relevant realm](html-spec-whatwg-org.md#81334-relevant) of target.
3. Initialize event’s [`type`](#22-interface-event) attribute to e.
4. Initialize any other IDL attributes of event as described in the invocation of this algorithm.

   > [!note]
   > This also allows for the [`isTrusted`](#22-interface-event) attribute to be set to false.

5. Return the result of [dispatching](#29-dispatching-events) event at target, with legacy target override flag set if set.

> [!note]
> Fire in the context of DOM is short for [creating](#25-constructing-events), initializing, and [dispatching](#29-dispatching-events) an [event](#22-interface-event). [Fire an event](#210-firing-events) makes that process easier to write down.

> [!example]
> If the [event](#22-interface-event) needs its [`bubbles`](#22-interface-event) or [`cancelable`](#22-interface-event) attribute initialized, one could write "[fire an event](#210-firing-events) named `submit` at target with its [`cancelable`](#22-interface-event) attribute initialized to true".
> 
> Or, when a custom constructor is needed, "[fire an event](#210-firing-events) named `click` at target using [`MouseEvent`](https://w3c.github.io/pointerevents/#dom-mouseevent) with its [`detail`](https://w3c.github.io/uievents/#dom-uievent-detail) attribute initialized to 1".
> 
> Occasionally the return value is important:
> 1. Let doAction be the result of [firing an event](#210-firing-events) named `like` at target.
> 2. If doAction is true, then …

### 2.11. Action versus occurrence

An [event](#22-interface-event) signifies an occurrence, not an action. Phrased differently, it represents a notification from an algorithm and can be used to influence the future course of that algorithm (e.g., through invoking [`preventDefault()`](#22-interface-event)). [Events](#22-interface-event) must not be used as actions or initiators that cause some algorithm to start running. That is not what they are for.

> [!note]
> This is called out here specifically because previous iterations of the DOM had a concept of "default actions" associated with [events](#22-interface-event) that gave folks all the wrong ideas. [Events](#22-interface-event) do not represent or cause actions, they can only be used to influence an ongoing one.

## 3. Aborting ongoing activities

Though promises do not have a built-in aborting mechanism, many APIs using them require abort semantics. [`AbortController`](#31-interface-abortcontroller) is meant to support these requirements by providing an [`abort()`](#31-interface-abortcontroller) method that toggles the state of a corresponding [`AbortSignal`](#32-interface-abortsignal) object. The API which wishes to support aborting can accept an [`AbortSignal`](#32-interface-abortsignal) object, and use its state to determine how to proceed.

APIs that rely upon [`AbortController`](#31-interface-abortcontroller) are encouraged to respond to [`abort()`](#31-interface-abortcontroller) by rejecting any unsettled promise with the [`AbortSignal`](#32-interface-abortsignal)’s [abort reason](#32-interface-abortsignal).

> [!example]
> A hypothetical `doAmazingness({ ... })` method could accept an [`AbortSignal`](#32-interface-abortsignal) object to support aborting as follows:
> 
> ```javascript
> const controller = new AbortController();
> const signal = controller.signal;
> 
> startSpinner();
> 
> doAmazingness({ ..., signal })
>   .then(result => ...)
>   .catch(err => {
>     if (err.name == 'AbortError') return;
>     showUserErrorMessage();
>   })
>   .then(() => stopSpinner());
> 
> // …
> 
> controller.abort();
> ```
> 
> `doAmazingness` could be implemented as follows:
> 
> ```javascript
> function doAmazingness({signal}) {
>   return new Promise((resolve, reject) => {
>     signal.throwIfAborted();
> 
>     // Begin doing amazingness, and call resolve(result) when done.
>     // But also, watch for signals:
>     signal.addEventListener('abort', () => {
>       // Stop doing amazingness, and:
>       reject(signal.reason);
>     });
>   });
> }
> 
> ```

APIs that do not return promises can either react in an equivalent manner or opt to not surface the [`AbortSignal`](#32-interface-abortsignal)’s [abort reason](#32-interface-abortsignal) at all. [`addEventListener()`](#27-interface-eventtarget) is an example of an API where the latter made sense.

APIs that require more granular control could extend both [`AbortController`](#31-interface-abortcontroller) and [`AbortSignal`](#32-interface-abortsignal) objects according to their needs.

### 3.1. Interface [`AbortController`](#31-interface-abortcontroller)

```webidl
[Exposed=*]
interface AbortController {
  constructor();

  [SameObject] readonly attribute AbortSignal signal;

  undefined abort(optional any reason);
};

```

`controller = new AbortController()`

Returns a new controller whose [`signal`](#31-interface-abortcontroller) is set to a newly created [`AbortSignal`](#32-interface-abortsignal) object.

`controller . signal`

Returns the [`AbortSignal`](#32-interface-abortsignal) object associated with this object.

`controller . abort(reason)`

Invoking this method will store reason in this object’s [`AbortSignal`](#32-interface-abortsignal)’s [abort reason](#32-interface-abortsignal), and signal to any observers that the associated activity is to be aborted. If reason is undefined, then an "[`AbortError`](https://webidl.spec.whatwg.org/#aborterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be stored.

An [`AbortController`](#31-interface-abortcontroller) object has an associated signal (an [`AbortSignal`](#32-interface-abortsignal) object).

The `new AbortController()` constructor steps are:
1. Let signal be a new [`AbortSignal`](#32-interface-abortsignal) object.
2. Set [this](https://webidl.spec.whatwg.org/#this)’s [signal](#31-interface-abortcontroller) to signal.

The `signal` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [signal](#31-interface-abortcontroller).

The `abort(reason)` method steps are to [signal abort](#31-interface-abortcontroller) on [this](https://webidl.spec.whatwg.org/#this) with reason if it is given.

To signal abort on an [`AbortController`](#31-interface-abortcontroller) controller with an optional reason, [signal abort](#32-interface-abortsignal) on controller’s [signal](#31-interface-abortcontroller) with reason if it is given.

### 3.2. Interface [`AbortSignal`](#32-interface-abortsignal)

```webidl
[Exposed=*]
interface AbortSignal : EventTarget {
  [NewObject] static AbortSignal abort(optional any reason);
  [Exposed=(Window,Worker), NewObject] static AbortSignal timeout([EnforceRange] unsigned long long milliseconds);
  [NewObject] static AbortSignal _any(sequence<AbortSignal> signals);

  readonly attribute boolean aborted;
  readonly attribute any reason;
  undefined throwIfAborted();

  attribute EventHandler onabort;
};
```

`AbortSignal . abort(reason)`

Returns an [`AbortSignal`](#32-interface-abortsignal) instance whose [abort reason](#32-interface-abortsignal) is set to reason if not undefined; otherwise to an "[`AbortError`](https://webidl.spec.whatwg.org/#aborterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

`AbortSignal . any(signals)`

Returns an [`AbortSignal`](#32-interface-abortsignal) instance which will be aborted once any of signals is aborted. Its [abort reason](#32-interface-abortsignal) will be set to whichever one of signals caused it to be aborted.

`AbortSignal . timeout(milliseconds)`

Returns an [`AbortSignal`](#32-interface-abortsignal) instance which will be aborted in milliseconds milliseconds. Its [abort reason](#32-interface-abortsignal) will be set to a "[`TimeoutError`](https://webidl.spec.whatwg.org/#timeouterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

`signal . aborted`

Returns true if signal’s [`AbortController`](#31-interface-abortcontroller) has signaled to abort; otherwise false.

`signal . reason`

Returns signal’s [abort reason](#32-interface-abortsignal).

`signal . throwIfAborted()`

Throws signal’s [abort reason](#32-interface-abortsignal), if signal’s [`AbortController`](#31-interface-abortcontroller) has signaled to abort; otherwise, does nothing.

An [`AbortSignal`](#32-interface-abortsignal) object has an associated abort reason (a JavaScript value), which is initially undefined.

An [`AbortSignal`](#32-interface-abortsignal) object has associated abort algorithms, (a [set](infra-spec-whatwg-org.md#513-sets) of algorithms which are to be executed when it is [aborted](#32-interface-abortsignal)), which is initially empty.

> [!note]
> The [abort algorithms](#32-interface-abortsignal) enable APIs with complex requirements to react in a reasonable way to [`abort()`](#31-interface-abortcontroller). For example, a given API’s [abort reason](#32-interface-abortsignal) might need to be propagated to a cross-thread environment, such as a service worker.

An [`AbortSignal`](#32-interface-abortsignal) object has a dependent (a boolean), which is initially false.

An [`AbortSignal`](#32-interface-abortsignal) object has associated source signals (a weak [set](infra-spec-whatwg-org.md#513-sets) of [`AbortSignal`](#32-interface-abortsignal) objects that the object is dependent on for its [aborted](#32-interface-abortsignal) state), which is initially empty.

An [`AbortSignal`](#32-interface-abortsignal) object has associated dependent signals (a weak [set](infra-spec-whatwg-org.md#513-sets) of [`AbortSignal`](#32-interface-abortsignal) objects that are dependent on the object for their [aborted](#32-interface-abortsignal) state), which is initially empty.

---

The static `abort(reason)` method steps are:
1. Let signal be a new [`AbortSignal`](#32-interface-abortsignal) object.
2. Set signal’s [abort reason](#32-interface-abortsignal) to reason if it is given; otherwise to a new "[`AbortError`](https://webidl.spec.whatwg.org/#aborterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Return signal.

The static `timeout(milliseconds)` method steps are:
1. Let signal be a new [`AbortSignal`](#32-interface-abortsignal) object.
2. Let global be signal’s [relevant global object](html-spec-whatwg-org.md#81334-relevant).
3. [Run steps after a timeout](html-spec-whatwg-org.md#87-timers) given global, "`AbortSignal-timeout`", milliseconds, and the following step:
   1. [Queue a global task](html-spec-whatwg-org.md#8172-queuing-tasks) on the [timer task source](html-spec-whatwg-org.md#87-timers) given global to [signal abort](#32-interface-abortsignal) given signal and a new "[`TimeoutError`](https://webidl.spec.whatwg.org/#timeouterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   For the duration of this timeout, if signal has any event listeners registered for its [`abort`](#32-interface-abortsignal) event, there must be a strong reference from global to signal.

4. Return signal.

The static `any(signals)` method steps are to return the result of [creating a dependent abort signal](#32-interface-abortsignal) from signals using [`AbortSignal`](#32-interface-abortsignal) and the [current realm](https://tc39.es/ecma262/#current-realm).

The `aborted` getter steps are to return true if [this](https://webidl.spec.whatwg.org/#this) is [aborted](#32-interface-abortsignal); otherwise false.

The `reason` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [abort reason](#32-interface-abortsignal).

The `throwIfAborted()` method steps are to throw [this](https://webidl.spec.whatwg.org/#this)’s [abort reason](#32-interface-abortsignal), if [this](https://webidl.spec.whatwg.org/#this) is [aborted](#32-interface-abortsignal).

> [!example]
> This method is primarily useful for when functions accepting [`AbortSignal`](#32-interface-abortsignal)s want to throw (or return a rejected promise) at specific checkpoints, instead of passing along the [`AbortSignal`](#32-interface-abortsignal) to other methods. For example, the following function allows aborting in between each attempt to poll for a condition. This gives opportunities to abort the polling process, even though the actual asynchronous operation (i.e., `await func()`) does not accept an [`AbortSignal`](#32-interface-abortsignal).
> 
> ```
> async function waitForCondition(func, targetValue, { signal } = {}) {
>   while (true) {
>     signal?.throwIfAborted();
> 
>     const result = await func();
>     if (result === targetValue) {
>       return;
>     }
>   }
> }
> 
> ```

The `onabort` attribute is an [event handler IDL attribute](html-spec-whatwg-org.md#8181-event-handlers) for the `onabort` [event handler](html-spec-whatwg-org.md#8181-event-handlers), whose [event handler event type](html-spec-whatwg-org.md#8181-event-handlers) is `abort`.

> [!note]
> Changes to an [`AbortSignal`](#32-interface-abortsignal) object represent the wishes of the corresponding [`AbortController`](#31-interface-abortcontroller) object, but an API observing the [`AbortSignal`](#32-interface-abortsignal) object can choose to ignore them. For instance, if the operation has already completed.

---

An [`AbortSignal`](#32-interface-abortsignal) object is aborted when its [abort reason](#32-interface-abortsignal) is not undefined.

To add an algorithm algorithm to an [`AbortSignal`](#32-interface-abortsignal) object signal:
1. If signal is [aborted](#32-interface-abortsignal), then return.
2. [Append](infra-spec-whatwg-org.md#513-sets) algorithm to signal’s [abort algorithms](#32-interface-abortsignal).

To remove an algorithm algorithm from an [`AbortSignal`](#32-interface-abortsignal) signal, [remove](infra-spec-whatwg-org.md#51-lists) algorithm from signal’s [abort algorithms](#32-interface-abortsignal).

To signal abort, given an [`AbortSignal`](#32-interface-abortsignal) object signal and an optional reason:
1. If signal is [aborted](#32-interface-abortsignal), then return.
2. Set signal’s [abort reason](#32-interface-abortsignal) to reason if it is given; otherwise to a new "[`AbortError`](https://webidl.spec.whatwg.org/#aborterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let dependentSignalsToAbort be a new [list](infra-spec-whatwg-org.md#51-lists).
4. [For each](infra-spec-whatwg-org.md#51-lists) dependentSignal of signal’s [dependent signals](#32-interface-abortsignal):
   1. If dependentSignal is not [aborted](#32-interface-abortsignal):
      1. Set dependentSignal’s [abort reason](#32-interface-abortsignal) to signal’s [abort reason](#32-interface-abortsignal).
      2. [Append](infra-spec-whatwg-org.md#51-lists) dependentSignal to dependentSignalsToAbort.
5. [Run the abort steps](#32-interface-abortsignal) for signal.
6. [For each](infra-spec-whatwg-org.md#51-lists) dependentSignal of dependentSignalsToAbort, [run the abort steps](#32-interface-abortsignal) for dependentSignal.

To run the abort steps for an [`AbortSignal`](#32-interface-abortsignal) signal:
1. [For each](infra-spec-whatwg-org.md#51-lists) algorithm of signal’s [abort algorithms](#32-interface-abortsignal): run algorithm.
2. [Empty](infra-spec-whatwg-org.md#51-lists) signal’s [abort algorithms](#32-interface-abortsignal).
3. [Fire an event](#210-firing-events) named [`abort`](#32-interface-abortsignal) at signal.

To create a dependent abort signal from a list of [`AbortSignal`](#32-interface-abortsignal) objects signals, using signalInterface, which must be either [`AbortSignal`](#32-interface-abortsignal) or an interface that inherits from it, and a realm:
1. Let resultSignal be a [new](https://webidl.spec.whatwg.org/#new) object implementing signalInterface using realm.
2. [For each](infra-spec-whatwg-org.md#51-lists) signal of signals: if signal is [aborted](#32-interface-abortsignal), then set resultSignal’s [abort reason](#32-interface-abortsignal) to signal’s [abort reason](#32-interface-abortsignal) and return resultSignal.
3. Set resultSignal’s [dependent](#32-interface-abortsignal) to true.
4. [For each](infra-spec-whatwg-org.md#51-lists) signal of signals:
   1. If signal’s [dependent](#32-interface-abortsignal) is false:
      1. [Append](infra-spec-whatwg-org.md#513-sets) signal to resultSignal’s [source signals](#32-interface-abortsignal).
      2. [Append](infra-spec-whatwg-org.md#513-sets) resultSignal to signal’s [dependent signals](#32-interface-abortsignal).
   2. Otherwise, [for each](infra-spec-whatwg-org.md#51-lists) sourceSignal of signal’s [source signals](#32-interface-abortsignal):
      1. Assert: sourceSignal is not [aborted](#32-interface-abortsignal) and not [dependent](#32-interface-abortsignal).
      2. [Append](infra-spec-whatwg-org.md#513-sets) sourceSignal to resultSignal’s [source signals](#32-interface-abortsignal).
      3. [Append](infra-spec-whatwg-org.md#513-sets) resultSignal to sourceSignal’s [dependent signals](#32-interface-abortsignal).
5. Return resultSignal.

#### 3.2.1. Garbage collection

A non-[aborted](#32-interface-abortsignal) [dependent](#32-interface-abortsignal) [`AbortSignal`](#32-interface-abortsignal) object must not be garbage collected while its [source signals](#32-interface-abortsignal) is non-empty and it has registered event listeners for its [`abort`](#32-interface-abortsignal) event or its [abort algorithms](#32-interface-abortsignal) is non-empty.

### 3.3. Using [`AbortController`](#31-interface-abortcontroller) and [`AbortSignal`](#32-interface-abortsignal) objects in APIs

Any web platform API using promises to represent operations that can be aborted must adhere to the following:
- Accept [`AbortSignal`](#32-interface-abortsignal) objects through a `signal` dictionary member.
- Convey that the operation got aborted by rejecting the promise with [`AbortSignal`](#32-interface-abortsignal) object’s [abort reason](#32-interface-abortsignal).
- Reject immediately if the [`AbortSignal`](#32-interface-abortsignal) is already [aborted](#32-interface-abortsignal), otherwise:
- Use the [abort algorithms](#32-interface-abortsignal) mechanism to observe changes to the [`AbortSignal`](#32-interface-abortsignal) object and do so in a manner that does not lead to clashes with other observers.

> [!example]
> The method steps for a promise-returning method `doAmazingness(options)` could be as follows:
> 1. Let global be [this](https://webidl.spec.whatwg.org/#this)’s [relevant global object](html-spec-whatwg-org.md#81334-relevant).
> 2. Let p be [a new promise](https://webidl.spec.whatwg.org/#a-new-promise).
> 3. If options\["`signal`"\] [exists](infra-spec-whatwg-org.md#52-maps):
>    1. Let signal be options\["`signal`"\].
>    2. If signal is [aborted](#32-interface-abortsignal), then [reject](https://webidl.spec.whatwg.org/#reject) p with signal’s [abort reason](#32-interface-abortsignal) and return p.
>    3. [Add the following abort steps](#32-interface-abortsignal) to signal:
>       1. Stop doing amazing things.
>       2. [Reject](https://webidl.spec.whatwg.org/#reject) p with signal’s [abort reason](#32-interface-abortsignal).
> 4. Run these steps [in parallel](html-spec-whatwg-org.md#211-parallelism):
>    1. Let amazingResult be the result of doing some amazing things.
>    2. [Queue a global task](html-spec-whatwg-org.md#8172-queuing-tasks) on the amazing task source given global to [resolve](https://webidl.spec.whatwg.org/#resolve) p with amazingResult.
> 5. Return p.

APIs not using promises should still adhere to the above as much as possible.

## 4. Nodes

### 4.1. Introduction to "The DOM"

In its original sense, "The DOM" is an API for accessing and manipulating documents (in particular, HTML and XML documents). In this specification, the term "document" is used for any markup-based resource, ranging from short static documents to long essays or reports with rich multimedia, as well as to fully-fledged interactive applications.

Each such document is represented as a [node tree](#42-node-tree). Some of the [nodes](#42-node-tree) in a [tree](#11-trees) can have [children](#11-trees), while others are always leaves.

To illustrate, consider this HTML document:

```
<!DOCTYPE html>
<html class=e>
 <head><title>Aliens?</title></head>
 <body>Why yes.</body>
</html>

```

It is represented as follows:
- [Document](#45-interface-document)
  - [Doctype](#46-interface-documenttype): `html`
  - [`Element`](#49-interface-element): `html` `class`="`e`"
    - [`Element`](#49-interface-element): `head`
      - [`Element`](#49-interface-element): `title`
        - [`Text`](#411-interface-text): Aliens?
    - [`Text`](#411-interface-text): ⏎␣
    - [`Element`](#49-interface-element): `body`
      - [`Text`](#411-interface-text): Why yes.⏎

Note that, due to the magic that is [HTML parsing](html-spec-whatwg-org.md#132-parsing-html-documents), not all [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points) were turned into [`Text`](#411-interface-text) [nodes](#42-node-tree), but the general concept is clear. Markup goes in, a [tree](#11-trees) of [nodes](#42-node-tree) comes out.

> [!note]
> The most excellent [Live DOM Viewer](https://software.hixie.ch/utilities/js/live-dom-viewer/) can be used to explore this matter in more detail.

### 4.2. Node tree

Nodes are objects that [implement](https://webidl.spec.whatwg.org/#implements) [`Node`](#44-interface-node). [Nodes](#42-node-tree) [participate](#11-trees) in a [tree](#11-trees), which is known as the node tree.

> [!note]
> In practice you deal with more specific objects.
> 
> Objects that [implement](https://webidl.spec.whatwg.org/#implements) [`Node`](#44-interface-node) also implement an inherited interface: [`Document`](#45-interface-document), [`DocumentType`](#46-interface-documenttype), [`DocumentFragment`](#47-interface-documentfragment), [`Element`](#49-interface-element), [`CharacterData`](#410-interface-characterdata), or [`Attr`](#492-interface-attr).
> 
> Objects that implement [`DocumentFragment`](#47-interface-documentfragment) sometimes implement [`ShadowRoot`](#48-interface-shadowroot).
> 
> Objects that implement [`Element`](#49-interface-element) also typically implement an inherited interface, such as [`HTMLAnchorElement`](html-spec-whatwg-org.md#451-the-a-element).
> 
> Objects that implement [`CharacterData`](#410-interface-characterdata) also implement an inherited interface: [`Text`](#411-interface-text), [`ProcessingInstruction`](#413-interface-processinginstruction), or [`Comment`](#414-interface-comment).
> 
> Objects that implement [`Text`](#411-interface-text) sometimes implement [`CDATASection`](#412-interface-cdatasection).
> 
> Thus, every [node](#42-node-tree)’s [primary interface](https://webidl.spec.whatwg.org/#dfn-primary-interface) is one of: [`Document`](#45-interface-document), [`DocumentType`](#46-interface-documenttype), [`DocumentFragment`](#47-interface-documentfragment), [`ShadowRoot`](#48-interface-shadowroot), [`Element`](#49-interface-element) or an inherited interface of [`Element`](#49-interface-element), [`Attr`](#492-interface-attr), [`Text`](#411-interface-text), [`CDATASection`](#412-interface-cdatasection), [`ProcessingInstruction`](#413-interface-processinginstruction), or [`Comment`](#414-interface-comment).

For brevity, this specification refers to an object that [implements](https://webidl.spec.whatwg.org/#implements) [`Node`](#44-interface-node) and an inherited interface `NodeInterface`, as a `NodeInterface` [node](#42-node-tree).

A [node tree](#42-node-tree) is constrained as follows, expressed as a relationship between a [node](#42-node-tree) and its potential [children](#11-trees):

[`Document`](#45-interface-document)

In [tree order](#11-trees):
1. Zero or more [`ProcessingInstruction`](#413-interface-processinginstruction) or [`Comment`](#414-interface-comment) [nodes](#42-node-tree).
2. Optionally one [`DocumentType`](#46-interface-documenttype) [node](#42-node-tree).
3. Zero or more [`ProcessingInstruction`](#413-interface-processinginstruction) or [`Comment`](#414-interface-comment) [nodes](#42-node-tree).
4. Optionally one [`Element`](#49-interface-element) [node](#42-node-tree).
5. Zero or more [`ProcessingInstruction`](#413-interface-processinginstruction) or [`Comment`](#414-interface-comment) [nodes](#42-node-tree).

[`DocumentFragment`](#47-interface-documentfragment)

[`Element`](#49-interface-element)

Zero or more [`Element`](#49-interface-element) or [`CharacterData`](#410-interface-characterdata) [nodes](#42-node-tree).

[`DocumentType`](#46-interface-documenttype)

[`CharacterData`](#410-interface-characterdata)

[`Attr`](#492-interface-attr)

No [children](#11-trees).

> [!note]
> [`Attr`](#492-interface-attr) [nodes](#42-node-tree) [participate](#11-trees) in a [tree](#11-trees) for historical reasons; they never have a (non-null) [parent](#11-trees) or any [children](#11-trees) and are therefore alone in a [tree](#11-trees).

To determine the length of a [node](#42-node-tree) node, run these steps:
1. If node is a [`DocumentType`](#46-interface-documenttype) or [`Attr`](#492-interface-attr) [node](#42-node-tree), then return 0.
2. If node is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree), then return node’s [data](#410-interface-characterdata)’s [length](infra-spec-whatwg-org.md#47-strings).
3. Return the number of node’s [children](#11-trees).

A [node](#42-node-tree) is considered empty if its [length](#42-node-tree) is 0.

#### 4.2.1. Document tree

A document tree is a [node tree](#42-node-tree) whose [root](#11-trees) is a [document](#45-interface-document).

The document element of a [document](#45-interface-document) is the [element](#49-interface-element) whose [parent](#11-trees) is that [document](#45-interface-document), if it exists; otherwise null.

> [!note]
> Per the [node tree](#42-node-tree) constraints, there can be only one such [element](#49-interface-element).

A [node](#42-node-tree) is in a document tree if its [root](#11-trees) is a [document](#45-interface-document).

A [node](#42-node-tree) is in a document if it is [in a document tree](#421-document-tree). The term [in a document](#421-document-tree) is no longer supposed to be used. It indicates that the standard using it has not been updated to account for [shadow trees](#422-shadow-tree).

#### 4.2.2. Shadow tree

A shadow tree is a [node tree](#42-node-tree) whose [root](#11-trees) is a [shadow root](#48-interface-shadowroot).

A [shadow root](#48-interface-shadowroot) is always attached to another [node tree](#42-node-tree) through its [host](#47-interface-documentfragment). A [shadow tree](#422-shadow-tree) is therefore never alone. The [node tree](#42-node-tree) of a [shadow root](#48-interface-shadowroot)’s [host](#47-interface-documentfragment) is sometimes referred to as the light tree.

> [!note]
> A [shadow tree](#422-shadow-tree)’s corresponding [light tree](#422-shadow-tree) can be a [shadow tree](#422-shadow-tree) itself.

A [node](#42-node-tree) is connected if its [shadow-including root](#48-interface-shadowroot) is a [document](#45-interface-document).

##### 4.2.2.1. Slots

A [shadow tree](#422-shadow-tree) contains zero or more [elements](#49-interface-element) that are slots.

> [!note]
> A [slot](#4221-slots) can only be created through HTML’s [`slot`](html-spec-whatwg-org.md#4124-the-slot-element) element.

A [slot](#4221-slots) has an associated name (a string). Unless stated otherwise it is the empty string.

Use these [attribute change steps](#49-interface-element) to update a [slot](#4221-slots)’s [name](#4221-slots):
1. If element is a [slot](#4221-slots), localName is `name`, and namespace is null:
   1. If value is oldValue, then return.
   2. If value is null and oldValue is the empty string, then return.
   3. If value is the empty string and oldValue is null, then return.
   4. If value is null or the empty string, then set element’s [name](#4221-slots) to the empty string.
   5. Otherwise, set element’s [name](#4221-slots) to value.
   6. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with element’s [root](#11-trees).

> [!note]
> The first [slot](#4221-slots) in a [shadow tree](#422-shadow-tree), in [tree order](#11-trees), whose [name](#4221-slots) is the empty string, is sometimes known as the "default slot".

A [slot](#4221-slots) has an associated assigned nodes (a list of [slottables](#4222-slottables)). Unless stated otherwise it is empty.

##### 4.2.2.2. Slottables

[`Element`](#49-interface-element) and [`Text`](#411-interface-text) [nodes](#42-node-tree) are slottables.

> [!note]
> A [slot](#4221-slots) can be a [slottable](#4222-slottables).

A [slottable](#4222-slottables) has an associated name (a string). Unless stated otherwise it is the empty string.

Use these [attribute change steps](#49-interface-element) to update a [slottable](#4222-slottables)’s [name](#4222-slottables):
1. If localName is `slot` and namespace is null:
   1. If value is oldValue, then return.
   2. If value is null and oldValue is the empty string, then return.
   3. If value is the empty string and oldValue is null, then return.
   4. If value is null or the empty string, then set element’s [name](#4222-slottables) to the empty string.
   5. Otherwise, set element’s [name](#4222-slottables) to value.
   6. If element is [assigned](#4222-slottables), then run [assign slottables](#4224-assigning-slottables-and-slots) for element’s [assigned slot](#4222-slottables).
   7. Run [assign a slot](#4224-assigning-slottables-and-slots) for element.

A [slottable](#4222-slottables) has an associated assigned slot (null or a [slot](#4221-slots)). Unless stated otherwise it is null. A [slottable](#4222-slottables) is assigned if its [assigned slot](#4222-slottables) is non-null.

A [slottable](#4222-slottables) has an associated manual slot assignment (null or a [slot](#4221-slots)). Unless stated otherwise, it is null.

> [!note]
> A [slottable](#4222-slottables)’s [manual slot assignment](#4222-slottables) can be implemented using a weak reference to the [slot](#4221-slots), because this variable is not directly accessible from script.

##### 4.2.2.3. Finding slots and slottables

To find a slot for a given [slottable](#4222-slottables) slottable and an optional boolean open (default false):
1. If slottable’s [parent](#11-trees) is null, then return null.
2. Let shadow be slottable’s [parent](#11-trees)’s [shadow root](#49-interface-element).
3. If shadow is null, then return null.
4. If open is true and shadow’s [mode](#48-interface-shadowroot) is not "`open`", then return null.
5. If shadow’s [slot assignment](#48-interface-shadowroot) is "`manual`", then return the [slot](#4221-slots) in shadow’s [descendants](#11-trees) whose [manually assigned nodes](html-spec-whatwg-org.md#4124-the-slot-element) [contains](infra-spec-whatwg-org.md#51-lists) slottable, if any; otherwise null.
6. Return the first [slot](#4221-slots) in [tree order](#11-trees) in shadow’s [descendants](#11-trees) whose [name](#4221-slots) is slottable’s [name](#4222-slottables), if any; otherwise null.

To find slottables for a given [slot](#4221-slots) slot:
1. Let result be « ».
2. Let root be slot’s [root](#11-trees).
3. If root is not a [shadow root](#48-interface-shadowroot), then return result.
4. Let host be root’s [host](#47-interface-documentfragment).
5. If root’s [slot assignment](#48-interface-shadowroot) is "`manual`":
   1. [For each](infra-spec-whatwg-org.md#51-lists) [slottable](#4222-slottables) slottable of slot’s [manually assigned nodes](html-spec-whatwg-org.md#4124-the-slot-element), if slottable’s [parent](#11-trees) is host, [append](infra-spec-whatwg-org.md#51-lists) slottable to result.
6. Otherwise, for each [slottable](#4222-slottables) [child](#11-trees) slottable of host, in [tree order](#11-trees):
   1. Let foundSlot be the result of [finding a slot](#4223-finding-slots-and-slottables) given slottable.
   2. If foundSlot is slot, then [append](infra-spec-whatwg-org.md#51-lists) slottable to result.
7. Return result.

To find flattened slottables for a given [slot](#4221-slots) slot:
1. Let result be « ».
2. If slot’s [root](#11-trees) is not a [shadow root](#48-interface-shadowroot), then return result.
3. Let slottables be the result of [finding slottables](#4223-finding-slots-and-slottables) given slot.
4. If slottables is the empty list, then append each [slottable](#4222-slottables) [child](#11-trees) of slot, in [tree order](#11-trees), to slottables.
5. For each node of slottables:
   1. If node is a [slot](#4221-slots) whose [root](#11-trees) is a [shadow root](#48-interface-shadowroot):
      1. Let temporaryResult be the result of [finding flattened slottables](#4223-finding-slots-and-slottables) given node.
      2. Append each [slottable](#4222-slottables) in temporaryResult, in order, to result.
   2. Otherwise, append node to result.
6. Return result.

##### 4.2.2.4. Assigning slottables and slots

To assign slottables for a [slot](#4221-slots) slot:
1. Let slottables be the result of [finding slottables](#4223-finding-slots-and-slottables) for slot.
2. If slottables and slot’s [assigned nodes](#4221-slots) are not identical, then run [signal a slot change](#4225-signaling-slot-change) for slot.
3. Set slot’s [assigned nodes](#4221-slots) to slottables.
4. For each slottable of slottables: set slottable’s [assigned slot](#4222-slottables) to slot.

To assign slottables for a tree, given a [node](#42-node-tree) root, run [assign slottables](#4224-assigning-slottables-and-slots) for each [slot](#4221-slots) of root’s [inclusive descendants](#11-trees), in [tree order](#11-trees).

To assign a slot, given a [slottable](#4222-slottables) slottable:
1. Let slot be the result of [finding a slot](#4223-finding-slots-and-slottables) with slottable.
2. If slot is non-null, then run [assign slottables](#4224-assigning-slottables-and-slots) for slot.

##### 4.2.2.5. Signaling slot change

Each [similar-origin window agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism) has signal slots (a [set](infra-spec-whatwg-org.md#513-sets) of [slots](#4221-slots)), which is initially empty. [\[HTML\]](#normative-references)

To signal a slot change, for a [slot](#4221-slots) slot:
1. [Append](infra-spec-whatwg-org.md#513-sets) slot to slot’s [relevant agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism)’s [signal slots](#4225-signaling-slot-change).
2. [Queue a mutation observer microtask](#43-mutation-observers).

#### 4.2.3. Mutation algorithms

To ensure pre-insert validity given a [node](#42-node-tree) node, a [node](#42-node-tree) parent, null or a [node](#42-node-tree) child, and a [list](infra-spec-whatwg-org.md#51-lists) of [nodes](#42-node-tree) childrenToExclude:
1. If parent is not a [`Document`](#45-interface-document), [`DocumentFragment`](#47-interface-documentfragment), or [`Element`](#49-interface-element) [node](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If node is a [host-including inclusive ancestor](#47-interface-documentfragment) of parent, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If child is non-null and its [parent](#11-trees) is not parent, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotFoundError`](https://webidl.spec.whatwg.org/#notfounderror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. If node is not a [`DocumentFragment`](#47-interface-documentfragment), [`DocumentType`](#46-interface-documenttype), [`Element`](#49-interface-element), or [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
5. If parent is not a [document](#45-interface-document):
   1. If node is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
   2. Return.
6. If node is a [`Text`](#411-interface-text) [node](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
7. If node is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree), then return.
8. If node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree):
   1. If node has more than one [element](#49-interface-element) [child](#11-trees) or has a [`Text`](#411-interface-text) [node](#42-node-tree) [child](#11-trees), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
   2. If node has no [element](#49-interface-element) [child](#11-trees), then return.
9. If node is a [`DocumentFragment`](#47-interface-documentfragment) or [`Element`](#49-interface-element) [node](#42-node-tree):
   1. If any of the following are true:
      - parent has an [element](#49-interface-element) [child](#11-trees) that childrenToExclude does not [contain](infra-spec-whatwg-org.md#51-lists);
      - child is non-null and a [doctype](#46-interface-documenttype) is [following](#11-trees) child; or
      - child is a [doctype](#46-interface-documenttype) that childrenToExclude does not [contain](infra-spec-whatwg-org.md#51-lists),

      then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   2. Return.

10. [Assert](infra-spec-whatwg-org.md#310-assertions): node is a [doctype](#46-interface-documenttype).
11. If any of the following are true:
    - parent has a [doctype](#46-interface-documenttype) [child](#11-trees) that childrenToExclude does not [contain](infra-spec-whatwg-org.md#51-lists);
    - child is non-null and an [element](#49-interface-element) is [preceding](#11-trees) child; or
    - child is null and parent has an [element](#49-interface-element) [child](#11-trees) that childrenToExclude does not [contain](infra-spec-whatwg-org.md#51-lists),

    then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

To pre-insert a [node](#42-node-tree) node into a [node](#42-node-tree) parent before null or [node](#42-node-tree) child:
1. [Ensure pre-insert validity](#423-mutation-algorithms) given node, parent, child, and « ».
2. Let referenceChild be child.
3. If referenceChild is node, then set referenceChild to node’s [next sibling](#11-trees).
4. [Insert](#423-mutation-algorithms) node into parent before referenceChild.
5. Return node.

[Specifications](#1-infrastructure) may define insertion steps for all or some [nodes](#42-node-tree). The algorithm is passed insertedNode, as indicated in the [insert](#423-mutation-algorithms) algorithm below. These steps must not modify the [node tree](#42-node-tree) that insertedNode [participates](#11-trees) in, create [browsing contexts](html-spec-whatwg-org.md#732-browsing-contexts), [fire events](#210-firing-events), or otherwise execute JavaScript. These steps may [queue tasks](html-spec-whatwg-org.md#8172-queuing-tasks) to do these things asynchronously, however.

> [!example]
> While the [insertion steps](#423-mutation-algorithms) cannot execute JavaScript (among other things), they will indeed have script-observable consequences. Consider the below example:
> 
> ```
> const h1 = document.querySelector('h1');
> 
> const fragment = new DocumentFragment();
> const script = fragment.appendChild(document.createElement('script'));
> const style = fragment.appendChild(document.createElement('style'));
> 
> script.innerText= 'console.log(getComputedStyle(h1).color)'; // Logs 'rgb(255, 0, 0)'
> style.innerText = 'h1 {color: rgb(255, 0, 0);}';
> 
> document.body.append(fragment);
> 
> ```
> 
> The script in the above example logs `'rgb(255, 0, 0)'` because the following happen in order:
> 1. The [insert](#423-mutation-algorithms) algorithm runs, which will insert the [`script`](html-spec-whatwg-org.md#4121-the-script-element) and `
>      style` elements in order.
>    1. The HTML Standard’s [insertion steps](#423-mutation-algorithms) run for the [`script`](html-spec-whatwg-org.md#4121-the-script-element) element; they do nothing. [\[HTML\]](#normative-references)
>    2. The HTML Standard’s [insertion steps](#423-mutation-algorithms) run for the `
>           style` element; they immediately apply its style rules to the document. [\[HTML\]](#normative-references)
>    3. The HTML Standard’s [post-connection steps](#423-mutation-algorithms) run for the [`script`](html-spec-whatwg-org.md#4121-the-script-element) element; they run the script, which immediately observes the style rules that were applied in the above step. [\[HTML\]](#normative-references)

[Specifications](#1-infrastructure) may also define post-connection steps for all or some [nodes](#42-node-tree). The algorithm is passed connectedNode, as indicated in the [insert](#423-mutation-algorithms) algorithm below.

> [!note]
> The purpose of the [post-connection steps](#423-mutation-algorithms) is to provide an opportunity for [nodes](#42-node-tree) to perform any connection-related operations that modify the [node tree](#42-node-tree) that connectedNode [participates](#11-trees) in, create [browsing contexts](html-spec-whatwg-org.md#732-browsing-contexts), or otherwise execute JavaScript. These steps allow a batch of [nodes](#42-node-tree) to be [inserted](#423-mutation-algorithms) *atomically* with respect to script, with all major side effects occurring *after* the batch insertions into the [node tree](#42-node-tree) is complete. This ensures that all pending [node tree](#42-node-tree) insertions completely finish before more insertions can occur.

[Specifications](#1-infrastructure) may define children changed steps for all or some [nodes](#42-node-tree). The algorithm is passed no argument and is called from [insert](#423-mutation-algorithms), [remove](#423-mutation-algorithms), and [replace data](#410-interface-characterdata).

To insert a [node](#42-node-tree) node into a [node](#42-node-tree) parent before null or a [node](#42-node-tree) child, with an optional boolean suppressObservers (default false):
1. Let nodes be node’s [children](#11-trees), if node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree); otherwise « node ».
2. Let count be nodes’s [size](infra-spec-whatwg-org.md#51-lists).
3. If count is 0, then return.
4. If node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree):
   1. [Remove](#423-mutation-algorithms) its [children](#11-trees) with [*suppressObservers*](#423-mutation-algorithms) set to true.
   2. [Queue a tree mutation record](#432-queuing-a-mutation-record) for node with « », nodes, null, and null.

      > [!note]
      > This step intentionally does not pay attention to suppressObservers.

5. If child is non-null:
   1. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is parent and [start offset](#53-interface-abstractrange) is greater than child’s [index](#11-trees): increase its [start offset](#53-interface-abstractrange) by count.
   2. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is parent and [end offset](#53-interface-abstractrange) is greater than child’s [index](#11-trees): increase its [end offset](#53-interface-abstractrange) by count.
6. Let previousSibling be child’s [previous sibling](#11-trees) or parent’s [last child](#11-trees) if child is null.
7. For each node in nodes, in [tree order](#11-trees):
   1. [Adopt](#45-interface-document) node into parent’s [node document](#44-interface-node).
   2. If child is null, then [append](infra-spec-whatwg-org.md#513-sets) node to parent’s [children](#11-trees).
   3. Otherwise, [insert](infra-spec-whatwg-org.md#51-lists) node into parent’s [children](#11-trees) before child’s [index](#11-trees).
   4. If parent is a [shadow host](#49-interface-element) whose [shadow root](#48-interface-shadowroot)’s [slot assignment](#48-interface-shadowroot) is "`named`" and node is a [slottable](#4222-slottables), then [assign a slot](#4224-assigning-slottables-and-slots) for node.
   5. If parent’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot), and parent is a [slot](#4221-slots) whose [assigned nodes](#4221-slots) is the empty list, then run [signal a slot change](#4225-signaling-slot-change) for parent.
   6. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with node’s [root](#11-trees).
   7. For each [shadow-including inclusive descendant](#48-interface-shadowroot) inclusiveDescendant of node, in [shadow-including tree order](#48-interface-shadowroot):
      1. Run the [insertion steps](#423-mutation-algorithms) with inclusiveDescendant.
      2. If inclusiveDescendant is not [connected](#422-shadow-tree), then [continue](infra-spec-whatwg-org.md#39-iteration).
      3. If inclusiveDescendant is an [element](#49-interface-element) and inclusiveDescendant’s [custom element registry](#49-interface-element) is non-null:
         1. If inclusiveDescendant’s [custom element registry](#49-interface-element)’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is true, then [append](infra-spec-whatwg-org.md#513-sets) inclusiveDescendant’s [node document](#44-interface-node) to inclusiveDescendant’s [custom element registry](#49-interface-element)’s [scoped document set](html-spec-whatwg-org.md#4134-the-customelementregistry-interface).
         2. If inclusiveDescendant is [custom](#49-interface-element), then [enqueue a custom element callback reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) with inclusiveDescendant, callback name "`connectedCallback`", and « ».
         3. Otherwise, [try to upgrade](html-spec-whatwg-org.md#4135-upgrades) inclusiveDescendant.

            > [!note]
            > If this successfully upgrades inclusiveDescendant, its `connectedCallback` will be enqueued automatically during the [upgrade an element](html-spec-whatwg-org.md#4135-upgrades) algorithm.

      4. Otherwise, if inclusiveDescendant is a [shadow root](#48-interface-shadowroot), inclusiveDescendant’s [custom element registry](#48-interface-shadowroot) is non-null, and inclusiveDescendant’s [custom element registry](#48-interface-shadowroot)’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is true, then [append](infra-spec-whatwg-org.md#513-sets) inclusiveDescendant’s [node document](#44-interface-node) to inclusiveDescendant’s [custom element registry](#48-interface-shadowroot)’s [scoped document set](html-spec-whatwg-org.md#4134-the-customelementregistry-interface).

8. If suppressObservers is false, then [queue a tree mutation record](#432-queuing-a-mutation-record) for parent with nodes, « », previousSibling, and child.
9. Run the [children changed steps](#423-mutation-algorithms) for parent.
10. Let staticNodeList be a [list](infra-spec-whatwg-org.md#51-lists) of [nodes](#42-node-tree), initially « ».

    > [!note]
    > We collect all [nodes](#42-node-tree) *before* calling the [post-connection steps](#423-mutation-algorithms) on any one of them, instead of calling the [post-connection steps](#423-mutation-algorithms) *while* we’re traversing the [node tree](#42-node-tree). This is because the [post-connection steps](#423-mutation-algorithms) can modify the tree’s structure, making live traversal unsafe, possibly leading to the [post-connection steps](#423-mutation-algorithms) being called multiple times on the same [node](#42-node-tree).

11. For each node of nodes, in [tree order](#11-trees):
    1. For each [shadow-including inclusive descendant](#48-interface-shadowroot) inclusiveDescendant of node, in [shadow-including tree order](#48-interface-shadowroot): [append](infra-spec-whatwg-org.md#51-lists) inclusiveDescendant to staticNodeList.
12. [For each](infra-spec-whatwg-org.md#51-lists) node of staticNodeList: if node is [connected](#422-shadow-tree), then run the [post-connection steps](#423-mutation-algorithms) with node.

To append a [node](#42-node-tree) node to a [node](#42-node-tree) parent: [pre-insert](#423-mutation-algorithms) node into parent before null.

---

[Specifications](#1-infrastructure) may define moving steps for all or some [nodes](#42-node-tree). The algorithm is passed a [node](#42-node-tree) movedNode, a boolean isSubtreeRoot, and a [node](#42-node-tree) oldAncestor as indicated in the [move](#423-mutation-algorithms) algorithm below. Like the [insertion steps](#423-mutation-algorithms), these steps must not modify the [node tree](#42-node-tree) that movedNode [participates](#11-trees) in, create [browsing contexts](html-spec-whatwg-org.md#732-browsing-contexts), [fire events](#210-firing-events), or otherwise execute JavaScript. These steps may queue tasks to do these things asynchronously, however.

To move a [node](#42-node-tree) node into a [node](#42-node-tree) newParent before null or a [node](#42-node-tree) child:
1. If newParent’s [shadow-including root](#48-interface-shadowroot) is not the same as node’s [shadow-including root](#48-interface-shadowroot), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   > [!note]
   > This has the side effect of ensuring that a move is only performed if newParent’s [connected](#422-shadow-tree) is node’s [connected](#422-shadow-tree).

2. If node is a [host-including inclusive ancestor](#47-interface-documentfragment) of newParent, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If child is non-null and its [parent](#11-trees) is not newParent, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotFoundError`](https://webidl.spec.whatwg.org/#notfounderror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. If node is not an [`Element`](#49-interface-element) or a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
5. If node is a [`Text`](#411-interface-text) [node](#42-node-tree) and newParent is a [document](#45-interface-document), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
6. If newParent is a [document](#45-interface-document), node is an [`Element`](#49-interface-element) [node](#42-node-tree), and either newParent has an [element](#49-interface-element) [child](#11-trees), child is a [doctype](#46-interface-documenttype), or child is non-null and a [doctype](#46-interface-documenttype) is [following](#11-trees) child then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
7. Let oldParent be node’s [parent](#11-trees).
8. [Assert](infra-spec-whatwg-org.md#310-assertions): oldParent is non-null.
9. Run the [live range pre-remove steps](#55-interface-range), given node.
10. For each [`NodeIterator`](#61-interface-nodeiterator) object iterator whose [root](#6-traversal)’s [node document](#44-interface-node) is node’s [node document](#44-interface-node): run the [`NodeIterator` pre-remove steps](#61-interface-nodeiterator) given node and iterator.
11. Let oldPreviousSibling be node’s [previous sibling](#11-trees).
12. Let oldNextSibling be node’s [next sibling](#11-trees).
13. [Remove](infra-spec-whatwg-org.md#51-lists) node from oldParent’s [children](#11-trees).
14. If node is [assigned](#4222-slottables), then run [assign slottables](#4224-assigning-slottables-and-slots) for node’s [assigned slot](#4222-slottables).
15. If oldParent’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot), and oldParent is a [slot](#4221-slots) whose [assigned nodes](#4221-slots) [is empty](infra-spec-whatwg-org.md#51-lists), then run [signal a slot change](#4225-signaling-slot-change) for oldParent.
16. If node has an [inclusive descendant](#11-trees) that is a [slot](#4221-slots):
    1. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with oldParent’s [root](#11-trees).
    2. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with node.
17. [Add transient registered observers](#43-mutation-observers) given node and oldParent.
18. If child is non-null:
    1. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is newParent and [start offset](#53-interface-abstractrange) is greater than child’s [index](#11-trees): increase its [start offset](#53-interface-abstractrange) by 1.
    2. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is newParent and [end offset](#53-interface-abstractrange) is greater than child’s [index](#11-trees): increase its [end offset](#53-interface-abstractrange) by 1.
19. Let newPreviousSibling be child’s [previous sibling](#11-trees) if child is non-null, and newParent’s [last child](#11-trees) otherwise.
20. If child is null, then [append](infra-spec-whatwg-org.md#513-sets) node to newParent’s [children](#11-trees).
21. Otherwise, [insert](infra-spec-whatwg-org.md#51-lists) node into newParent’s [children](#11-trees) before child’s [index](#11-trees).
22. If newParent is a [shadow host](#49-interface-element) whose [shadow root](#48-interface-shadowroot)’s [slot assignment](#48-interface-shadowroot) is "`named`" and node is a [slottable](#4222-slottables), then [assign a slot](#4224-assigning-slottables-and-slots) for node.
23. If newParent’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot), and newParent is a [slot](#4221-slots) whose [assigned nodes](#4221-slots) [is empty](infra-spec-whatwg-org.md#51-lists), then run [signal a slot change](#4225-signaling-slot-change) for newParent.
24. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with node’s [root](#11-trees).
25. For each [shadow-including inclusive descendant](#48-interface-shadowroot) inclusiveDescendant of node, in [shadow-including tree order](#48-interface-shadowroot):
    1. Let isSubtreeRoot be true if inclusiveDescendant is node; otherwise false.
    2. Run the [moving steps](#423-mutation-algorithms) with inclusiveDescendant, isSubtreeRoot, and oldParent.

       > [!note]
       > Because the [move](#423-mutation-algorithms) algorithm is a separate primitive from [insert](#423-mutation-algorithms) and [remove](#423-mutation-algorithms), it does not invoke the [insertion steps](#423-mutation-algorithms) or [removing steps](#423-mutation-algorithms) for inclusiveDescendant.

    3. If inclusiveDescendant is [custom](#49-interface-element) and newParent is [connected](#422-shadow-tree), then [enqueue a custom element callback reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) with inclusiveDescendant, callback name "`connectedMoveCallback`", and « ».

26. [Queue a tree mutation record](#432-queuing-a-mutation-record) for oldParent with « », « node », oldPreviousSibling, and oldNextSibling.
27. [Queue a tree mutation record](#432-queuing-a-mutation-record) for newParent with « node », « », newPreviousSibling, and child.

---

To replace a [node](#42-node-tree) child with a [node](#42-node-tree) node within a [node](#42-node-tree) parent:
1. [Ensure pre-insert validity](#423-mutation-algorithms) given node, parent, child, and « child ».
2. Let referenceChild be child’s [next sibling](#11-trees).
3. If referenceChild is node, then set referenceChild to node’s [next sibling](#11-trees).
4. Let previousSibling be child’s [previous sibling](#11-trees).
5. Let removedNodes be the empty set.
6. [Adopt](#45-interface-document) node into parent’s [node document](#44-interface-node).
7. If child’s [parent](#11-trees) is non-null:
   1. Set removedNodes to « child ».
   2. [Remove](#423-mutation-algorithms) child with [*suppressObservers*](#423-mutation-algorithms) set to true.

   > [!note]
   > The above can only be false if child is node.

8. Let nodes be node’s [children](#11-trees) if node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree); otherwise « node ».
9. [Insert](#423-mutation-algorithms) node into parent before referenceChild with [*suppressObservers*](#423-mutation-algorithms) set to true.
10. [Queue a tree mutation record](#432-queuing-a-mutation-record) for parent with nodes, removedNodes, previousSibling, and referenceChild.
11. Return child.

To replace all with a [node](#42-node-tree) or null node within a [node](#42-node-tree) parent:
1. Let removedNodes be parent’s [children](#11-trees).
2. Let addedNodes be the empty set.
3. If node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree), then set addedNodes to node’s [children](#11-trees).
4. Otherwise, if node is non-null, set addedNodes to « node ».
5. [Remove](#423-mutation-algorithms) all parent’s [children](#11-trees), in [tree order](#11-trees), with [*suppressObservers*](#423-mutation-algorithms) set to true.
6. If node is non-null, then [insert](#423-mutation-algorithms) node into parent before null with [*suppressObservers*](#423-mutation-algorithms) set to true.
7. If either addedNodes or removedNodes [is not empty](infra-spec-whatwg-org.md#51-lists), then [queue a tree mutation record](#432-queuing-a-mutation-record) for parent with addedNodes, removedNodes, null, and null.

> [!note]
> This algorithm does not make any checks with regards to the [node tree](#42-node-tree) constraints. Specification authors need to use it wisely.

---

To pre-remove a [node](#42-node-tree) child from a [node](#42-node-tree) parent:
1. If child’s [parent](#11-trees) is not parent, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotFoundError`](https://webidl.spec.whatwg.org/#notfounderror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. [Remove](#423-mutation-algorithms) child.
3. Return child.

[Specifications](#1-infrastructure) may define removing steps for all or some [nodes](#42-node-tree). The algorithm is passed a [node](#42-node-tree) removedNode, a boolean isSubtreeRoot, and a [node](#42-node-tree) oldAncestor as indicated in the [remove](#423-mutation-algorithms) algorithm below.

To remove a [node](#42-node-tree) node, with an optional boolean suppressObservers (default false):
1. Let parent be node’s [parent](#11-trees).
2. Assert: parent is non-null.
3. Run the [live range pre-remove steps](#55-interface-range), given node.
4. For each [`NodeIterator`](#61-interface-nodeiterator) object iterator whose [root](#6-traversal)’s [node document](#44-interface-node) is node’s [node document](#44-interface-node): run the [`NodeIterator` pre-remove steps](#61-interface-nodeiterator) given node and iterator.
5. Let oldPreviousSibling be node’s [previous sibling](#11-trees).
6. Let oldNextSibling be node’s [next sibling](#11-trees).
7. [Remove](infra-spec-whatwg-org.md#51-lists) node from its parent’s [children](#11-trees).
8. If node is [assigned](#4222-slottables), then run [assign slottables](#4224-assigning-slottables-and-slots) for node’s [assigned slot](#4222-slottables).
9. If parent’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot), and parent is a [slot](#4221-slots) whose [assigned nodes](#4221-slots) is the empty list, then run [signal a slot change](#4225-signaling-slot-change) for parent.
10. If node has an [inclusive descendant](#11-trees) that is a [slot](#4221-slots):
    1. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with parent’s [root](#11-trees).
    2. Run [assign slottables for a tree](#4224-assigning-slottables-and-slots) with node.
11. Run the [removing steps](#423-mutation-algorithms) with node, true, and parent.
12. Let isParentConnected be parent’s [connected](#422-shadow-tree).
13. If node is [custom](#49-interface-element) and isParentConnected is true, then [enqueue a custom element callback reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) with node, callback name "`disconnectedCallback`", and « ».

    > [!note]
    > It is intentional for now that [custom](#49-interface-element) [elements](#49-interface-element) do not get parent passed. This might change in the future if there is a need.

14. For each [shadow-including descendant](#48-interface-shadowroot) descendant of node, in [shadow-including tree order](#48-interface-shadowroot):
    1. Run the [removing steps](#423-mutation-algorithms) with descendant, false, and parent.
    2. If descendant is [custom](#49-interface-element) and isParentConnected is true, then [enqueue a custom element callback reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) with descendant, callback name "`disconnectedCallback`", and « ».
15. [Add transient registered observers](#43-mutation-observers) given node and parent.
16. If suppressObservers is false, then [queue a tree mutation record](#432-queuing-a-mutation-record) for parent with « », « node », oldPreviousSibling, and oldNextSibling.
17. Run the [children changed steps](#423-mutation-algorithms) for parent.

#### 4.2.4. Mixin [`NonElementParentNode`](#424-mixin-nonelementparentnode)

> [!note]
> Web compatibility prevents the [`getElementById()`](#424-mixin-nonelementparentnode) method from being exposed on [elements](#49-interface-element) (and therefore on [`ParentNode`](#426-mixin-parentnode)).

```webidl
interface mixin NonElementParentNode {
  Element? getElementById(DOMString elementId);
};
Document includes NonElementParentNode;
DocumentFragment includes NonElementParentNode;

```

`node . getElementById(elementId)`

Returns the first [element](#49-interface-element) within node’s [descendants](#11-trees) whose [ID](#49-interface-element) is elementId.

To get an element by ID, given a [node](#42-node-tree) node and a string elementId, return the first [element](#49-interface-element), in [tree order](#11-trees), within node’s [descendants](#11-trees), whose [ID](#49-interface-element) is elementId; otherwise, if there is no such [element](#49-interface-element), null.

The `getElementById(elementId)` method steps are to return the result of [getting an element by ID](#424-mixin-nonelementparentnode) given [this](https://webidl.spec.whatwg.org/#this) and elementId.

#### 4.2.5. Mixin [`DocumentOrShadowRoot`](#425-mixin-documentorshadowroot)

```webidl
interface mixin DocumentOrShadowRoot {
  readonly attribute CustomElementRegistry? customElementRegistry;
};
Document includes DocumentOrShadowRoot;
ShadowRoot includes DocumentOrShadowRoot;

```

`` registry = documentOrShadowRoot . `customElementRegistry` ``

Returns documentOrShadowRoot’s [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object, if any; otherwise null.

The `customElementRegistry` getter steps are:
1. If [this](https://webidl.spec.whatwg.org/#this) is a [document](#45-interface-document), then return [this](https://webidl.spec.whatwg.org/#this)’s [custom element registry](#45-interface-document).
2. [Assert](infra-spec-whatwg-org.md#310-assertions): [this](https://webidl.spec.whatwg.org/#this) is a [`ShadowRoot`](#48-interface-shadowroot) [node](#42-node-tree).
3. Return [this](https://webidl.spec.whatwg.org/#this)’s [custom element registry](#48-interface-shadowroot).

> [!note]
> The [`DocumentOrShadowRoot`](#425-mixin-documentorshadowroot) mixin is also expected to be used by other standards that want to define APIs shared between [documents](#45-interface-document) and [shadow roots](#48-interface-shadowroot).

#### 4.2.6. Mixin [`ParentNode`](#426-mixin-parentnode)

To convert nodes into a node, given a [list](infra-spec-whatwg-org.md#51-lists) of [nodes](#42-node-tree) and strings nodes, and [document](#45-interface-document) document:
1. Replace each string in nodes with the result of [creating a text node](#411-interface-text) given document and the string.
2. If nodes’s [size](infra-spec-whatwg-org.md#51-lists) is 1, then return nodes\[0\].
3. Let fragment be the result of [creating a document fragment](#47-interface-documentfragment) given document.
4. For each node of nodes: [append](#423-mutation-algorithms) node to fragment.
5. Return fragment.

```webidl
interface mixin ParentNode {
  [SameObject] readonly attribute HTMLCollection children;
  readonly attribute Element? firstElementChild;
  readonly attribute Element? lastElementChild;
  readonly attribute unsigned long childElementCount;

  [CEReactions, Unscopable] undefined prepend((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined append((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined replaceChildren((Node or DOMString)... nodes);

  [CEReactions] undefined moveBefore(Node node, Node? child);

  Element? querySelector(DOMString selectors);
  [NewObject] NodeList querySelectorAll(DOMString selectors);
};
Document includes ParentNode;
DocumentFragment includes ParentNode;
Element includes ParentNode;

```

`` collection = node . `children` ``

Returns the [child](#11-trees) [elements](#49-interface-element).

`` element = node . `firstElementChild` ``

Returns the first [child](#11-trees) that is an [element](#49-interface-element); otherwise null.

`` element = node . `lastElementChild` ``

Returns the last [child](#11-trees) that is an [element](#49-interface-element); otherwise null.

`node . prepend(nodes)`

Inserts nodes before the [first child](#11-trees) of node, while replacing strings in nodes with equivalent [`Text`](#411-interface-text) [nodes](#42-node-tree).

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated.

`node . append(nodes)`

Inserts nodes after the [last child](#11-trees) of node, while replacing strings in nodes with equivalent [`Text`](#411-interface-text) [nodes](#42-node-tree).

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated.

`node . replaceChildren(nodes)`

Replace all [children](#11-trees) of node with nodes, while replacing strings in nodes with equivalent [`Text`](#411-interface-text) [nodes](#42-node-tree).

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated.

`node . moveBefore(movedNode, child)`

Moves, without first removing, movedNode into node after child if child is non-null; otherwise after the [last child](#11-trees) of node. This method preserves state associated with movedNode.

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated, or the state associated with the moved node cannot be preserved.

`node . querySelector(selectors)`

Returns the first [element](#49-interface-element) that is a [descendant](#11-trees) of node that matches selectors.

`node . querySelectorAll(selectors)`

Returns all [element](#49-interface-element) [descendants](#11-trees) of node that match selectors.

The `children` getter steps are to return an [`HTMLCollection`](#42102-interface-htmlcollection) [collection](#4210-old-style-collections-nodelist-and-htmlcollection) rooted at [this](https://webidl.spec.whatwg.org/#this) matching only [element](#49-interface-element) [children](#11-trees).

The `firstElementChild` getter steps are to return the first [child](#11-trees) that is an [element](#49-interface-element); otherwise null.

The `lastElementChild` getter steps are to return the last [child](#11-trees) that is an [element](#49-interface-element); otherwise null.

The `childElementCount` getter steps are to return the number of [children](#11-trees) of [this](https://webidl.spec.whatwg.org/#this) that are [elements](#49-interface-element).

The `prepend(nodes)` method steps are:
1. Let node be the result of [converting nodes into a node](#426-mixin-parentnode) given nodes and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).
2. [Pre-insert](#423-mutation-algorithms) node into [this](https://webidl.spec.whatwg.org/#this) before [this](https://webidl.spec.whatwg.org/#this)’s [first child](#11-trees).

The `append(nodes)` method steps are:
1. Let node be the result of [converting nodes into a node](#426-mixin-parentnode) given nodes and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).
2. [Append](#423-mutation-algorithms) node to [this](https://webidl.spec.whatwg.org/#this).

The `replaceChildren(nodes)` method steps are:
1. Let node be the result of [converting nodes into a node](#426-mixin-parentnode) given nodes and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).
2. [Ensure pre-insert validity](#423-mutation-algorithms) given node, [this](https://webidl.spec.whatwg.org/#this), null, and [this](https://webidl.spec.whatwg.org/#this)’s [children](#11-trees).
3. [Replace all](#423-mutation-algorithms) with node within [this](https://webidl.spec.whatwg.org/#this).

The `moveBefore(node, child)` method steps are:
1. Let referenceChild be child.
2. If referenceChild is node, then set referenceChild to node’s [next sibling](#11-trees).
3. [Move](#423-mutation-algorithms) node into [this](https://webidl.spec.whatwg.org/#this) before referenceChild.

The `querySelector(selectors)` method steps are to return the first result of running [scope-match a selectors string](#13-selectors) selectors against [this](https://webidl.spec.whatwg.org/#this), if the result is not an empty list; otherwise null.

The `querySelectorAll(selectors)` method steps are to return the [static](#4210-old-style-collections-nodelist-and-htmlcollection) result of running [scope-match a selectors string](#13-selectors) selectors against [this](https://webidl.spec.whatwg.org/#this).

#### 4.2.7. Mixin [`NonDocumentTypeChildNode`](#427-mixin-nondocumenttypechildnode)

> [!note]
> Web compatibility prevents the [`previousElementSibling`](#427-mixin-nondocumenttypechildnode) and [`nextElementSibling`](#427-mixin-nondocumenttypechildnode) attributes from being exposed on [doctypes](#46-interface-documenttype) (and therefore on [`ChildNode`](#428-mixin-childnode)).

```webidl
interface mixin NonDocumentTypeChildNode {
  readonly attribute Element? previousElementSibling;
  readonly attribute Element? nextElementSibling;
};
Element includes NonDocumentTypeChildNode;
CharacterData includes NonDocumentTypeChildNode;

```

`` element = node . `previousElementSibling` ``

Returns the first [preceding](#11-trees) [sibling](#11-trees) that is an [element](#49-interface-element); otherwise null.

`` element = node . `nextElementSibling` ``

Returns the first [following](#11-trees) [sibling](#11-trees) that is an [element](#49-interface-element); otherwise null.

The `previousElementSibling` getter steps are to return the first [preceding](#11-trees) [sibling](#11-trees) that is an [element](#49-interface-element); otherwise null.

The `nextElementSibling` getter steps are to return the first [following](#11-trees) [sibling](#11-trees) that is an [element](#49-interface-element); otherwise null.

#### 4.2.8. Mixin [`ChildNode`](#428-mixin-childnode)

```webidl
interface mixin ChildNode {
  [CEReactions, Unscopable] undefined before((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined after((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined replaceWith((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined remove();
};
DocumentType includes ChildNode;
Element includes ChildNode;
CharacterData includes ChildNode;

```

`` node . `before(...nodes)` ``

Inserts nodes just before node, while replacing strings in nodes with equivalent [`Text`](#411-interface-text) [nodes](#42-node-tree).

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated.

`` node . `after(...nodes)` ``

Inserts nodes just after node, while replacing strings in nodes with equivalent [`Text`](#411-interface-text) [nodes](#42-node-tree).

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated.

`` node . `replaceWith(...nodes)` ``

Replaces node with nodes, while replacing strings in nodes with equivalent [`Text`](#411-interface-text) [nodes](#42-node-tree).

[Throws](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if the constraints of the [node tree](#42-node-tree) are violated.

`` node . `remove()` ``

Removes node.

The `before(nodes)` method steps are:
1. Let parent be [this](https://webidl.spec.whatwg.org/#this)’s [parent](#11-trees).
2. If parent is null, then return.
3. Let viablePreviousSibling be [this](https://webidl.spec.whatwg.org/#this)’s first [preceding](#11-trees) [sibling](#11-trees) not in nodes; otherwise null.
4. Let node be the result of [converting nodes into a node](#426-mixin-parentnode), given nodes and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).
5. If viablePreviousSibling is null, then set it to parent’s [first child](#11-trees); otherwise to viablePreviousSibling’s [next sibling](#11-trees).
6. [Pre-insert](#423-mutation-algorithms) node into parent before viablePreviousSibling.

The `after(nodes)` method steps are:
1. Let parent be [this](https://webidl.spec.whatwg.org/#this)’s [parent](#11-trees).
2. If parent is null, then return.
3. Let viableNextSibling be [this](https://webidl.spec.whatwg.org/#this)’s first [following](#11-trees) [sibling](#11-trees) not in nodes; otherwise null.
4. Let node be the result of [converting nodes into a node](#426-mixin-parentnode), given nodes and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).
5. [Pre-insert](#423-mutation-algorithms) node into parent before viableNextSibling.

The `replaceWith(nodes)` method steps are:
1. Let parent be [this](https://webidl.spec.whatwg.org/#this)’s [parent](#11-trees).
2. If parent is null, then return.
3. Let viableNextSibling be [this](https://webidl.spec.whatwg.org/#this)’s first [following](#11-trees) [sibling](#11-trees) not in nodes; otherwise null.
4. Let node be the result of [converting nodes into a node](#426-mixin-parentnode), given nodes and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).
5. If [this](https://webidl.spec.whatwg.org/#this)’s [parent](#11-trees) is parent, [replace](#423-mutation-algorithms) [this](https://webidl.spec.whatwg.org/#this) with node within parent.

   > [!note]
   > [This](https://webidl.spec.whatwg.org/#this) could have been inserted into node.

6. Otherwise, [pre-insert](#423-mutation-algorithms) node into parent before viableNextSibling.

The `remove()` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this)’s [parent](#11-trees) is null, then return.
2. [Remove](#423-mutation-algorithms) [this](https://webidl.spec.whatwg.org/#this).

#### 4.2.9. Mixin [`Slottable`](#429-mixin-slottable)

```webidl
interface mixin Slottable {
  readonly attribute HTMLSlotElement? assignedSlot;
};
Element includes Slottable;
Text includes Slottable;

```

The `assignedSlot` getter steps are to return the result of [find a slot](#4223-finding-slots-and-slottables) given [this](https://webidl.spec.whatwg.org/#this) and true.

#### 4.2.10. Old-style collections: [`NodeList`](#42101-interface-nodelist) and [`HTMLCollection`](#42102-interface-htmlcollection)

A collection is an object that represents a list of [nodes](#42-node-tree). A [collection](#4210-old-style-collections-nodelist-and-htmlcollection) can be either live or static. Unless otherwise stated, a [collection](#4210-old-style-collections-nodelist-and-htmlcollection) must be [live](#4210-old-style-collections-nodelist-and-htmlcollection).

If a [collection](#4210-old-style-collections-nodelist-and-htmlcollection) is [live](#4210-old-style-collections-nodelist-and-htmlcollection), then the attributes and methods on that object must operate on the actual underlying data, not a snapshot of the data.

When a [collection](#4210-old-style-collections-nodelist-and-htmlcollection) is created, a filter and a root are associated with it.

The [collection](#4210-old-style-collections-nodelist-and-htmlcollection) then represents a view of the subtree rooted at the [collection’s](#4210-old-style-collections-nodelist-and-htmlcollection) root, containing only nodes that match the given filter. The view is linear. In the absence of specific requirements to the contrary, the nodes within the [collection](#4210-old-style-collections-nodelist-and-htmlcollection) must be sorted in [tree order](#11-trees).

##### 4.2.10.1. Interface [`NodeList`](#42101-interface-nodelist)

A [`NodeList`](#42101-interface-nodelist) object is a [collection](#4210-old-style-collections-nodelist-and-htmlcollection) of [nodes](#42-node-tree).

```webidl
[Exposed=Window]
interface NodeList {
  getter Node? item(unsigned long index);
  readonly attribute unsigned long length;
  iterable<Node>;
};

```

collection . [`length`](#42101-interface-nodelist)

Returns the number of [nodes](#42-node-tree) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection).

element = collection . [`item(index)`](#42101-interface-nodelist)

element = collection\[index\]

Returns the [node](#42-node-tree) with index index from the [collection](#4210-old-style-collections-nodelist-and-htmlcollection). The [nodes](#42-node-tree) are sorted in [tree order](#11-trees).

The object’s [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices) are the numbers in the range zero to one less than the number of nodes [represented by the collection](#4210-old-style-collections-nodelist-and-htmlcollection). If there are no such elements, then there are no [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices).

The `length` attribute must return the number of nodes [represented by the collection](#4210-old-style-collections-nodelist-and-htmlcollection).

The `item(index)` method must return the indexth [node](#42-node-tree) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection). If there is no indexth [node](#42-node-tree) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection), then the method must return null.

##### 4.2.10.2. Interface [`HTMLCollection`](#42102-interface-htmlcollection)

```webidl
[Exposed=Window, LegacyUnenumerableNamedProperties]
interface HTMLCollection {
  readonly attribute unsigned long length;
  getter Element? item(unsigned long index);
  getter Element? namedItem(DOMString name);
};

```

An [`HTMLCollection`](#42102-interface-htmlcollection) object is a [collection](#4210-old-style-collections-nodelist-and-htmlcollection) of [elements](#49-interface-element).

> [!note]
> [`HTMLCollection`](#42102-interface-htmlcollection) is a historical artifact we cannot rid the web of. While developers are of course welcome to keep using it, new API standard designers ought not to use it (use `sequence<T>` in IDL instead).

collection . [`length`](#42102-interface-htmlcollection)

Returns the number of [elements](#49-interface-element) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection).

element = collection . [`item(index)`](#42102-interface-htmlcollection)

element = collection\[index\]

Returns the [element](#49-interface-element) with index index from the [collection](#4210-old-style-collections-nodelist-and-htmlcollection). The [elements](#49-interface-element) are sorted in [tree order](#11-trees).

element = collection . [`namedItem(name)`](#42102-interface-htmlcollection)

element = collection\[name\]

Returns the first [element](#49-interface-element) with [ID](#49-interface-element) or name name from the collection.

The object’s [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices) are the numbers in the range zero to one less than the number of elements [represented by the collection](#4210-old-style-collections-nodelist-and-htmlcollection). If there are no such elements, then there are no [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices).

The `length` getter steps are to return the number of nodes [represented by the collection](#4210-old-style-collections-nodelist-and-htmlcollection).

The `item(index)` method steps are to return the indexth [element](#49-interface-element) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection). If there is no indexth [element](#49-interface-element) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection), then the method must return null.

The [supported property names](https://webidl.spec.whatwg.org/#dfn-supported-property-names) are the values from the list returned by these steps:
1. Let result be an empty list.
2. For each element [represented by the collection](#4210-old-style-collections-nodelist-and-htmlcollection), in [tree order](#11-trees):
   1. If element has an [ID](#49-interface-element) which is not in result, append element’s [ID](#49-interface-element) to result.
   2. If element is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and [has](#49-interface-element) a [`name` attribute](#492-interface-attr) whose [value](#492-interface-attr) is neither the empty string nor is in result, append element’s [`name` attribute](#492-interface-attr) [value](#492-interface-attr) to result.
3. Return result.

The `namedItem(key)` method steps are:
1. If key is the empty string, return null.
2. Return the first [element](#49-interface-element) in the [collection](#4210-old-style-collections-nodelist-and-htmlcollection) for which at least one of the following is true:
   - it has an [ID](#49-interface-element) which is key;
   - it is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and [has](#49-interface-element) a [`name` attribute](#492-interface-attr) whose [value](#492-interface-attr) is key;

   or null if there is no such [element](#49-interface-element).

### 4.3. Mutation observers

Each [similar-origin window agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism) has a mutation observer microtask queued (a boolean), which is initially false. [\[HTML\]](#normative-references)

Each [similar-origin window agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism) also has pending mutation observers (a [set](infra-spec-whatwg-org.md#513-sets) of zero or more [`MutationObserver`](#431-interface-mutationobserver) objects), which is initially empty.

Each [similar-origin window agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism) also has a mutation observer counter (a number), which is initially 0.

To queue a mutation observer microtask:
1. If the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [mutation observer microtask queued](#43-mutation-observers) is true, then return.
2. Set the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [mutation observer microtask queued](#43-mutation-observers) to true.
3. [Queue](html-spec-whatwg-org.md#8172-queuing-tasks) a [microtask](html-spec-whatwg-org.md#8171-definitions) to [notify mutation observers](#43-mutation-observers).

To notify mutation observers:
1. Set the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [mutation observer microtask queued](#43-mutation-observers) to false.
2. Let notifyList be the result of [sorting](infra-spec-whatwg-org.md#51-lists) the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [pending mutation observers](#43-mutation-observers) in ascending order, with a being less than b if a’s [creation index](#431-interface-mutationobserver) is less than b’s [creation index](#431-interface-mutationobserver).
3. [Empty](infra-spec-whatwg-org.md#51-lists) the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [pending mutation observers](#43-mutation-observers).
4. Let signalSet be a [clone](infra-spec-whatwg-org.md#51-lists) of the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [signal slots](#4225-signaling-slot-change).
5. [Empty](infra-spec-whatwg-org.md#51-lists) the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [signal slots](#4225-signaling-slot-change).
6. [For each](infra-spec-whatwg-org.md#51-lists) mo of notifyList:
   1. Let records be a [clone](infra-spec-whatwg-org.md#51-lists) of mo’s [record queue](#431-interface-mutationobserver).
   2. [Empty](infra-spec-whatwg-org.md#51-lists) mo’s [record queue](#431-interface-mutationobserver).
   3. [Remove transient registered observers](#43-mutation-observers) for mo.
   4. If records [is not empty](infra-spec-whatwg-org.md#51-lists), then [invoke](https://webidl.spec.whatwg.org/#invoke-a-callback-function) mo’s [callback](#431-interface-mutationobserver) with « records, mo » and "`report`", and with [callback this value](https://webidl.spec.whatwg.org/#dfn-callback-this-value) mo.
7. [For each](infra-spec-whatwg-org.md#51-lists) slot of signalSet: [fire an event](#210-firing-events) named `slotchange`, with its [`bubbles`](#22-interface-event) attribute set to true, at slot.

---

Each [node](#42-node-tree) has a registered observer list (a [list](infra-spec-whatwg-org.md#51-lists) of zero or more [registered observers](#43-mutation-observers)), which is initially empty.

A registered observer consists of an observer (a [`MutationObserver`](#431-interface-mutationobserver) object) and options (a [`MutationObserverInit`](#431-interface-mutationobserver) dictionary).

A transient registered observer is a [registered observer](#43-mutation-observers) that also consists of a source (a [registered observer](#43-mutation-observers) that is not a [transient registered observer](#43-mutation-observers)).

> [!note]
> [Transient registered observers](#43-mutation-observers) are used to track mutations within a given [node](#42-node-tree)’s [descendants](#11-trees) after [node](#42-node-tree) has been removed or moved so they do not get lost when [`subtree`](#431-interface-mutationobserver) is set to true on [node](#42-node-tree)’s former [parent](#11-trees). They are removed the next time mutation observers are notified.

To add transient registered observers given a [node](#42-node-tree) node and a [node](#42-node-tree) parent:
1. For each [inclusive ancestor](#11-trees) inclusiveAncestor of parent, and then [for each](infra-spec-whatwg-org.md#51-lists) registered of inclusiveAncestor’s [registered observer list](#43-mutation-observers):
   1. If registered’s [options](#43-mutation-observers)\["[`subtree`](#431-interface-mutationobserver)"\] is false, then [continue](infra-spec-whatwg-org.md#39-iteration).
   2. Let observer be registered’s [observer](#43-mutation-observers).
   3. Let source be registered’s [source](#43-mutation-observers) if registered is a [transient registered observer](#43-mutation-observers); otherwise registered.
   4. If node’s [registered observer list](#43-mutation-observers) [contains](infra-spec-whatwg-org.md#51-lists) a [transient registered observer](#43-mutation-observers) whose [source](#43-mutation-observers) is source, then [continue](infra-spec-whatwg-org.md#39-iteration).
   5. [Append](infra-spec-whatwg-org.md#51-lists) a new [transient registered observer](#43-mutation-observers) whose [observer](#43-mutation-observers) is observer, [options](#43-mutation-observers) is source’s [options](#43-mutation-observers), and [source](#43-mutation-observers) is source to node’s [registered observer list](#43-mutation-observers).
   6. [Append](infra-spec-whatwg-org.md#513-sets) a weak reference to node to observer’s [transient node set](#431-interface-mutationobserver).
   7. [Append](infra-spec-whatwg-org.md#513-sets) observer to the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [pending mutation observers](#43-mutation-observers).

      > [!note]
      > This ensures node’s [transient registered observers](#43-mutation-observers) are removed the next time mutation observers are notified, even if no [`MutationRecord`](#433-interface-mutationrecord) object is queued for observer.

   8. [Queue a mutation observer microtask](#43-mutation-observers).

To remove transient registered observers for a [`MutationObserver`](#431-interface-mutationobserver) object observer:
1. [For each](infra-spec-whatwg-org.md#51-lists) node of observer’s [transient node set](#431-interface-mutationobserver): [remove](infra-spec-whatwg-org.md#51-lists) all [transient registered observers](#43-mutation-observers) whose [observer](#43-mutation-observers) is observer from node’s [registered observer list](#43-mutation-observers).
2. [Empty](infra-spec-whatwg-org.md#51-lists) observer’s [transient node set](#431-interface-mutationobserver).

#### 4.3.1. Interface [`MutationObserver`](#431-interface-mutationobserver)

```webidl
[Exposed=Window]
interface MutationObserver {
  constructor(MutationCallback callback);

  undefined observe(Node target, optional MutationObserverInit options = {});
  undefined disconnect();
  sequence<MutationRecord> takeRecords();
};

callback MutationCallback = undefined (sequence<MutationRecord> mutations, MutationObserver observer);

dictionary MutationObserverInit {
  boolean childList = false;
  boolean attributes;
  boolean characterData;
  boolean subtree = false;
  boolean attributeOldValue;
  boolean characterDataOldValue;
  sequence<DOMString> attributeFilter;
};

```

A [`MutationObserver`](#431-interface-mutationobserver) object can be used to observe mutations to the [tree](#11-trees) of [nodes](#42-node-tree).

Each [`MutationObserver`](#431-interface-mutationobserver) object has these associated concepts:
- A callback set on creation.
- A creation index (a number) set on creation.
- A node list (a [list](infra-spec-whatwg-org.md#51-lists) of weak references to [nodes](#42-node-tree)), which is initially empty.
- A transient node set (a [set](infra-spec-whatwg-org.md#513-sets) of weak references to [nodes](#42-node-tree)), which is initially empty.
- A record queue (a [queue](infra-spec-whatwg-org.md#512-queues) of zero or more [`MutationRecord`](#433-interface-mutationrecord) objects), which is initially empty.

`` observer = new `MutationObserver(callback)` ``

Constructs a [`MutationObserver`](#431-interface-mutationobserver) object and sets its [callback](#431-interface-mutationobserver) to callback. The callback is invoked with a list of [`MutationRecord`](#433-interface-mutationrecord) objects as first argument and the constructed [`MutationObserver`](#431-interface-mutationobserver) object as second argument. It is invoked after [nodes](#42-node-tree) registered with the [`observe()`](#431-interface-mutationobserver) method, are mutated.

`` observer . `observe(target, options)` ``

Instructs the user agent to observe a given target (a [node](#42-node-tree)) and report any mutations based on the criteria given by options (an object).

The options argument allows for setting mutation observation options via object members. These are the object members that can be used:

[`childList`](#431-interface-mutationobserver)

Set to true if mutations to target’s [children](#11-trees) are to be observed.

[`attributes`](#431-interface-mutationobserver)

Set to true if mutations to target’s [attributes](#492-interface-attr) are to be observed. Can be omitted if [`attributeOldValue`](#431-interface-mutationobserver) or [`attributeFilter`](#431-interface-mutationobserver) is specified.

[`characterData`](#431-interface-mutationobserver)

Set to true if mutations to target’s [data](#410-interface-characterdata) are to be observed. Can be omitted if [`characterDataOldValue`](#431-interface-mutationobserver) is specified.

[`subtree`](#431-interface-mutationobserver)

Set to true if mutations to not just target, but also target’s [descendants](#11-trees) are to be observed.

[`attributeOldValue`](#431-interface-mutationobserver)

Set to true if [`attributes`](#431-interface-mutationobserver) is true or omitted and target’s [attribute](#492-interface-attr) [value](#492-interface-attr) before the mutation needs to be recorded.

[`characterDataOldValue`](#431-interface-mutationobserver)

Set to true if [`characterData`](#431-interface-mutationobserver) is set to true or omitted and target’s [data](#410-interface-characterdata) before the mutation needs to be recorded.

[`attributeFilter`](#431-interface-mutationobserver)

Set to a list of [attribute](#492-interface-attr) [local names](#492-interface-attr) (without [namespace](#492-interface-attr)) if not all [attribute](#492-interface-attr) mutations need to be observed and [`attributes`](#431-interface-mutationobserver) is true or omitted.

`` observer . `disconnect()` ``

Stops observer from observing any mutations. Until the [`observe()`](#431-interface-mutationobserver) method is used again, observer’s [callback](#431-interface-mutationobserver) will not be invoked.

`` observer . `takeRecords()` ``

Empties the [record queue](#431-interface-mutationobserver) and returns what was in there.

The `new MutationObserver(callback)` constructor steps are:
1. Set [this](https://webidl.spec.whatwg.org/#this)’s [callback](#431-interface-mutationobserver) to callback.
2. Set [this](https://webidl.spec.whatwg.org/#this)’s [creation index](#431-interface-mutationobserver) to [this](https://webidl.spec.whatwg.org/#this)’s [relevant agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism)’s [mutation observer counter](#43-mutation-observers).
3. Increase [this](https://webidl.spec.whatwg.org/#this)’s [relevant agent](html-spec-whatwg-org.md#8121-integration-with-the-javascript-agent-formalism)’s [mutation observer counter](#43-mutation-observers) by 1.

The `observe(target, options)` method steps are:
1. If either options\["[`attributeOldValue`](#431-interface-mutationobserver)"\] or options\["[`attributeFilter`](#431-interface-mutationobserver)"\] [exists](infra-spec-whatwg-org.md#52-maps), and options\["[`attributes`](#431-interface-mutationobserver)"\] does not [exist](infra-spec-whatwg-org.md#52-maps), then set options\["[`attributes`](#431-interface-mutationobserver)"\] to true.
2. If options\["[`characterDataOldValue`](#431-interface-mutationobserver)"\] [exists](infra-spec-whatwg-org.md#52-maps) and options\["[`characterData`](#431-interface-mutationobserver)"\] does not [exist](infra-spec-whatwg-org.md#52-maps), then set options\["[`characterData`](#431-interface-mutationobserver)"\] to true.
3. If none of options\["[`childList`](#431-interface-mutationobserver)"\], options\["[`attributes`](#431-interface-mutationobserver)"\], and options\["[`characterData`](#431-interface-mutationobserver)"\] is true, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a `TypeError`.
4. If options\["[`attributeOldValue`](#431-interface-mutationobserver)"\] is true and options\["[`attributes`](#431-interface-mutationobserver)"\] is false, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a `TypeError`.
5. If options\["[`attributeFilter`](#431-interface-mutationobserver)"\] [exists](infra-spec-whatwg-org.md#52-maps) and options\["[`attributes`](#431-interface-mutationobserver)"\] is false, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a `TypeError`.
6. If options\["[`characterDataOldValue`](#431-interface-mutationobserver)"\] is true and options\["[`characterData`](#431-interface-mutationobserver)"\] is false, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a `TypeError`.
7. Let registered be the [registered observer](#43-mutation-observers) in target’s [registered observer list](#43-mutation-observers) that is not a [transient registered observer](#43-mutation-observers) and whose [observer](#43-mutation-observers) is [this](https://webidl.spec.whatwg.org/#this), if any; otherwise null.

   > [!note]
   > If target was in a subtree that [this](https://webidl.spec.whatwg.org/#this) observes and was removed or moved, target’s [registered observer list](#43-mutation-observers) can also contain [transient registered observers](#43-mutation-observers) whose [observer](#43-mutation-observers) is [this](https://webidl.spec.whatwg.org/#this). These are ignored, as they are removed the next time mutation observers are notified.

8. If registered is non-null:
   1. [For each](infra-spec-whatwg-org.md#51-lists) node of [this](https://webidl.spec.whatwg.org/#this)’s [transient node set](#431-interface-mutationobserver): [remove](infra-spec-whatwg-org.md#51-lists) all [transient registered observers](#43-mutation-observers) whose [source](#43-mutation-observers) is registered from node’s [registered observer list](#43-mutation-observers).
   2. Set registered’s [options](#43-mutation-observers) to options.
9. Otherwise:
   1. [Append](infra-spec-whatwg-org.md#51-lists) a new [registered observer](#43-mutation-observers) whose [observer](#43-mutation-observers) is [this](https://webidl.spec.whatwg.org/#this) and [options](#43-mutation-observers) is options to target’s [registered observer list](#43-mutation-observers).
   2. [Append](infra-spec-whatwg-org.md#51-lists) a weak reference to target to [this](https://webidl.spec.whatwg.org/#this)’s [node list](#431-interface-mutationobserver).

The `disconnect()` method steps are:
1. [For each](infra-spec-whatwg-org.md#51-lists) node of [this](https://webidl.spec.whatwg.org/#this)’s [node list](#431-interface-mutationobserver): [remove](infra-spec-whatwg-org.md#51-lists) any [registered observer](#43-mutation-observers) from node’s [registered observer list](#43-mutation-observers) for which [this](https://webidl.spec.whatwg.org/#this) is the [observer](#43-mutation-observers).
2. [Remove transient registered observers](#43-mutation-observers) for [this](https://webidl.spec.whatwg.org/#this).
3. [Empty](infra-spec-whatwg-org.md#51-lists) [this](https://webidl.spec.whatwg.org/#this)’s [node list](#431-interface-mutationobserver).
4. [Empty](infra-spec-whatwg-org.md#51-lists) [this](https://webidl.spec.whatwg.org/#this)’s [record queue](#431-interface-mutationobserver).

The `takeRecords()` method steps are:
1. Let records be a [clone](infra-spec-whatwg-org.md#51-lists) of [this](https://webidl.spec.whatwg.org/#this)’s [record queue](#431-interface-mutationobserver).
2. [Empty](infra-spec-whatwg-org.md#51-lists) [this](https://webidl.spec.whatwg.org/#this)’s [record queue](#431-interface-mutationobserver).
3. Return records.

#### 4.3.2. Queuing a mutation record

To queue a mutation record of type for target with name, namespace, oldValue, addedNodes, removedNodes, previousSibling, and nextSibling:
1. Let interestedObservers be an empty [map](infra-spec-whatwg-org.md#52-maps).
2. Let nodes be the [inclusive ancestors](#11-trees) of target.
3. For each node of nodes, and then [for each](infra-spec-whatwg-org.md#51-lists) registered of node’s [registered observer list](#43-mutation-observers):
   1. Let options be registered’s [options](#43-mutation-observers).
   2. If none of the following are true
      - node is not target and options\["[`subtree`](#431-interface-mutationobserver)"\] is false
      - type is "`attributes`" and options\["[`attributes`](#431-interface-mutationobserver)"\] either does not [exist](infra-spec-whatwg-org.md#52-maps) or is false
      - type is "`attributes`", options\["[`attributeFilter`](#431-interface-mutationobserver)"\] [exists](infra-spec-whatwg-org.md#52-maps), and options\["[`attributeFilter`](#431-interface-mutationobserver)"\] does not [contain](infra-spec-whatwg-org.md#51-lists) name or namespace is non-null
      - type is "`characterData`" and options\["[`characterData`](#431-interface-mutationobserver)"\] either does not [exist](infra-spec-whatwg-org.md#52-maps) or is false
      - type is "`childList`" and options\["[`childList`](#431-interface-mutationobserver)"\] is false

      then:
      1. Let mo be registered’s [observer](#43-mutation-observers).
      2. If interestedObservers\[mo\] does not [exist](infra-spec-whatwg-org.md#52-maps), then [set](infra-spec-whatwg-org.md#52-maps) interestedObservers\[mo\] to null.
      3. If either type is "`attributes`" and options\["[`attributeOldValue`](#431-interface-mutationobserver)"\] is true, or type is "`characterData`" and options\["[`characterDataOldValue`](#431-interface-mutationobserver)"\] is true, then [set](infra-spec-whatwg-org.md#52-maps) interestedObservers\[mo\] to oldValue.

4. If interestedObservers [is empty](infra-spec-whatwg-org.md#52-maps), then return.
5. [For each](infra-spec-whatwg-org.md#52-maps) observer → mappedOldValue of interestedObservers:
   1. Let record be a new [`MutationRecord`](#433-interface-mutationrecord) object with its [`type`](#433-interface-mutationrecord) set to type, [`target`](#433-interface-mutationrecord) set to target, [`attributeName`](#433-interface-mutationrecord) set to name, [`attributeNamespace`](#433-interface-mutationrecord) set to namespace, [`oldValue`](#433-interface-mutationrecord) set to mappedOldValue, [`addedNodes`](#433-interface-mutationrecord) set to addedNodes, [`removedNodes`](#433-interface-mutationrecord) set to removedNodes, [`previousSibling`](#433-interface-mutationrecord) set to previousSibling, and [`nextSibling`](#433-interface-mutationrecord) set to nextSibling.
   2. [Enqueue](infra-spec-whatwg-org.md#512-queues) record to observer’s [record queue](#431-interface-mutationobserver).
   3. [Append](infra-spec-whatwg-org.md#513-sets) observer to the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [pending mutation observers](#43-mutation-observers).
6. [Queue a mutation observer microtask](#43-mutation-observers).

To queue a tree mutation record for target with addedNodes, removedNodes, previousSibling, and nextSibling:
1. [Assert](infra-spec-whatwg-org.md#310-assertions): either addedNodes or removedNodes [is not empty](infra-spec-whatwg-org.md#51-lists).
2. [Queue a mutation record](#432-queuing-a-mutation-record) of "`childList`" for target with null, null, null, addedNodes, removedNodes, previousSibling, and nextSibling.

#### 4.3.3. Interface [`MutationRecord`](#433-interface-mutationrecord)

```webidl
[Exposed=Window]
interface MutationRecord {
  readonly attribute DOMString type;
  [SameObject] readonly attribute Node target;
  [SameObject] readonly attribute NodeList addedNodes;
  [SameObject] readonly attribute NodeList removedNodes;
  readonly attribute Node? previousSibling;
  readonly attribute Node? nextSibling;
  readonly attribute DOMString? attributeName;
  readonly attribute DOMString? attributeNamespace;
  readonly attribute DOMString? oldValue;
};

```

`` record . `type` ``

Returns "`attributes`" if it was an [attribute](#492-interface-attr) mutation. "`characterData`" if it was a mutation to a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree). And "`childList`" if it was a mutation to the [tree](#11-trees) of [nodes](#42-node-tree).

`` record . `target` ``

Returns the [node](#42-node-tree) the mutation affected, depending on the [`type`](#433-interface-mutationrecord). For "`attributes`", it is the [element](#49-interface-element) whose [attribute](#492-interface-attr) changed. For "`characterData`", it is the [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree). For "`childList`", it is the [node](#42-node-tree) whose [children](#11-trees) changed.

`` record . `addedNodes` ``

`` record . `removedNodes` ``

Return the [nodes](#42-node-tree) added and removed respectively.

`` record . `previousSibling` ``

`` record . `nextSibling` ``

Return the [previous](#11-trees) and [next sibling](#11-trees) respectively of the added or removed [nodes](#42-node-tree); otherwise null.

`` record . `attributeName` ``

Returns the [local name](#492-interface-attr) of the changed [attribute](#492-interface-attr); otherwise null.

`` record . `attributeNamespace` ``

Returns the [namespace](#492-interface-attr) of the changed [attribute](#492-interface-attr); otherwise null.

`` record . `oldValue` ``

The return value depends on [`type`](#433-interface-mutationrecord). For "`attributes`", it is the [value](#492-interface-attr) of the changed [attribute](#492-interface-attr) before the change. For "`characterData`", it is the [data](#410-interface-characterdata) of the changed [node](#42-node-tree) before the change. For "`childList`", it is null.

The `type`, `target`, `addedNodes`, `removedNodes`, `previousSibling`, `nextSibling`, `attributeName`, `attributeNamespace`, and `oldValue` attributes must return the values they were initialized to.

### 4.4. Interface [`Node`](#44-interface-node)

```webidl
[Exposed=Window]
interface Node : EventTarget {
  const unsigned short ELEMENT_NODE = 1;
  const unsigned short ATTRIBUTE_NODE = 2;
  const unsigned short TEXT_NODE = 3;
  const unsigned short CDATA_SECTION_NODE = 4;
  const unsigned short ENTITY_REFERENCE_NODE = 5; // legacy
  const unsigned short ENTITY_NODE = 6; // legacy
  const unsigned short PROCESSING_INSTRUCTION_NODE = 7;
  const unsigned short COMMENT_NODE = 8;
  const unsigned short DOCUMENT_NODE = 9;
  const unsigned short DOCUMENT_TYPE_NODE = 10;
  const unsigned short DOCUMENT_FRAGMENT_NODE = 11;
  const unsigned short NOTATION_NODE = 12; // legacy
  readonly attribute unsigned short nodeType;
  readonly attribute DOMString nodeName;

  readonly attribute USVString baseURI;

  readonly attribute boolean isConnected;
  readonly attribute Document? ownerDocument;
  Node getRootNode(optional GetRootNodeOptions options = {});
  readonly attribute Node? parentNode;
  readonly attribute Element? parentElement;
  boolean hasChildNodes();
  [SameObject] readonly attribute NodeList childNodes;
  readonly attribute Node? firstChild;
  readonly attribute Node? lastChild;
  readonly attribute Node? previousSibling;
  readonly attribute Node? nextSibling;

  [CEReactions] attribute DOMString? nodeValue;
  [CEReactions] attribute DOMString? textContent;
  [CEReactions] undefined normalize();

  [CEReactions, NewObject] Node cloneNode(optional boolean subtree = false);
  boolean isEqualNode(Node? otherNode);
  boolean isSameNode(Node? otherNode); // legacy alias of ===

  const unsigned short DOCUMENT_POSITION_DISCONNECTED = 0x01;
  const unsigned short DOCUMENT_POSITION_PRECEDING = 0x02;
  const unsigned short DOCUMENT_POSITION_FOLLOWING = 0x04;
  const unsigned short DOCUMENT_POSITION_CONTAINS = 0x08;
  const unsigned short DOCUMENT_POSITION_CONTAINED_BY = 0x10;
  const unsigned short DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC = 0x20;
  unsigned short compareDocumentPosition(Node other);
  boolean contains(Node? other);

  DOMString? lookupPrefix(DOMString? namespace);
  DOMString? lookupNamespaceURI(DOMString? prefix);
  boolean isDefaultNamespace(DOMString? namespace);

  [CEReactions] Node insertBefore(Node node, Node? child);
  [CEReactions] Node appendChild(Node node);
  [CEReactions] Node replaceChild(Node node, Node child);
  [CEReactions] Node removeChild(Node child);
};

dictionary GetRootNodeOptions {
  boolean composed = false;
};

```

> [!note]
> [`Node`](#44-interface-node) is an abstract interface that is used by all [nodes](#42-node-tree). You cannot get a direct instance of it.

Each [node](#42-node-tree) has an associated node document, set upon creation, that is a [document](#45-interface-document).

> [!note]
> A [node](#42-node-tree)’s [node document](#44-interface-node) can be changed by the [adopt](#45-interface-document) algorithm.

A [node](#42-node-tree)’s [get the parent](#27-interface-eventtarget) algorithm, given an event, returns the [node](#42-node-tree)’s [assigned slot](#4222-slottables), if [node](#42-node-tree) is [assigned](#4222-slottables); otherwise [node](#42-node-tree)’s [parent](#11-trees).

> [!note]
> Each [node](#42-node-tree) also has a [registered observer list](#43-mutation-observers).

To create a node that implements an interface interface, given a [document](#45-interface-document) document:
1. [Assert](infra-spec-whatwg-org.md#310-assertions): interface is neither [`Document`](#45-interface-document) nor an interface that inherits from [`Document`](#45-interface-document). To create a [document](#45-interface-document), use [create a document](#45-interface-document) instead.
2. Return a new [node](#42-node-tree) that [implements](https://webidl.spec.whatwg.org/#implements) interface, in document’s [relevant realm](html-spec-whatwg-org.md#81334-relevant), with its [node document](#44-interface-node) set to document.

---

`` node . `nodeType` ``

Returns a number appropriate for the type of node, as follows:

[`Element`](#49-interface-element)

`` `Node` . `ELEMENT_NODE` `` (1).

[`Attr`](#492-interface-attr)

`` `Node` . `ATTRIBUTE_NODE` `` (2).

An [exclusive `Text` node](#411-interface-text)

`` `Node` . `TEXT_NODE` `` (3).

[`CDATASection`](#412-interface-cdatasection)

`` `Node` . `CDATA_SECTION_NODE` `` (4).

[`ProcessingInstruction`](#413-interface-processinginstruction)

`` `Node` . `PROCESSING_INSTRUCTION_NODE` `` (7).

[`Comment`](#414-interface-comment)

`` `Node` . `COMMENT_NODE` `` (8).

[`Document`](#45-interface-document)

`` `Node` . `DOCUMENT_NODE` `` (9).

[`DocumentType`](#46-interface-documenttype)

`` `Node` . `DOCUMENT_TYPE_NODE` `` (10).

[`DocumentFragment`](#47-interface-documentfragment)

`` `Node` . `DOCUMENT_FRAGMENT_NODE` `` (11).

`` node . `nodeName` ``

Returns a string appropriate for the type of node, as follows:

[`Element`](#49-interface-element)

Its [HTML-uppercased qualified name](#49-interface-element).

[`Attr`](#492-interface-attr)

Its [qualified name](#492-interface-attr).

An [exclusive `Text` node](#411-interface-text)

"`#text`".

[`CDATASection`](#412-interface-cdatasection)

"`#cdata-section`".

[`ProcessingInstruction`](#413-interface-processinginstruction)

Its [target](#413-interface-processinginstruction).

[`Comment`](#414-interface-comment)

"`#comment`".

[`Document`](#45-interface-document)

"`#document`".

[`DocumentType`](#46-interface-documenttype)

Its [name](#46-interface-documenttype).

[`DocumentFragment`](#47-interface-documentfragment)

"`#document-fragment`".

The `nodeType` getter steps are to return the first matching statement, switching on the interface [this](https://webidl.spec.whatwg.org/#this) [implements](https://webidl.spec.whatwg.org/#implements):

[`Element`](#49-interface-element)

`ELEMENT_NODE` (1)

[`Attr`](#492-interface-attr)

`ATTRIBUTE_NODE` (2);

An [exclusive `Text` node](#411-interface-text)

`TEXT_NODE` (3);

[`CDATASection`](#412-interface-cdatasection)

`CDATA_SECTION_NODE` (4);

[`ProcessingInstruction`](#413-interface-processinginstruction)

`PROCESSING_INSTRUCTION_NODE` (7);

[`Comment`](#414-interface-comment)

`COMMENT_NODE` (8);

[`Document`](#45-interface-document)

`DOCUMENT_NODE` (9);

[`DocumentType`](#46-interface-documenttype)

`DOCUMENT_TYPE_NODE` (10);

[`DocumentFragment`](#47-interface-documentfragment)

`DOCUMENT_FRAGMENT_NODE` (11).

The `nodeName` getter steps are to return the first matching statement, switching on the interface [this](https://webidl.spec.whatwg.org/#this) [implements](https://webidl.spec.whatwg.org/#implements):

[`Element`](#49-interface-element)

Its [HTML-uppercased qualified name](#49-interface-element).

[`Attr`](#492-interface-attr)

Its [qualified name](#492-interface-attr).

An [exclusive `Text` node](#411-interface-text)

"`#text`".

[`CDATASection`](#412-interface-cdatasection)

"`#cdata-section`".

[`ProcessingInstruction`](#413-interface-processinginstruction)

Its [target](#413-interface-processinginstruction).

[`Comment`](#414-interface-comment)

"`#comment`".

[`Document`](#45-interface-document)

"`#document`".

[`DocumentType`](#46-interface-documenttype)

Its [name](#46-interface-documenttype).

[`DocumentFragment`](#47-interface-documentfragment)

"`#document-fragment`".

---

`` node . `baseURI` ``

Returns node’s [node document](#44-interface-node)’s [document base URL](html-spec-whatwg-org.md#243-document-base-urls).

The `baseURI` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node)’s [document base URL](html-spec-whatwg-org.md#243-document-base-urls), [serialized](https://url.spec.whatwg.org/#concept-url-serializer).

---

`` node . `isConnected` ``

Returns true if node is [connected](#422-shadow-tree); otherwise false.

`` node . `ownerDocument` ``

Returns the [node document](#44-interface-node). Returns null for [documents](#45-interface-document).

`` node . `getRootNode()` ``

Returns node’s [root](#11-trees).

`node . getRootNode({ composed:true })`

Returns node’s [shadow-including root](#48-interface-shadowroot).

`` node . `parentNode` ``

Returns the [parent](#11-trees).

`` node . `parentElement` ``

Returns the [parent element](#49-interface-element).

`` node . `hasChildNodes()` ``

Returns whether node has [children](#11-trees).

`` node . `childNodes` ``

Returns the [children](#11-trees).

`` node . `firstChild` ``

Returns the [first child](#11-trees).

`` node . `lastChild` ``

Returns the [last child](#11-trees).

`` node . `previousSibling` ``

Returns the [previous sibling](#11-trees).

`` node . `nextSibling` ``

Returns the [next sibling](#11-trees).

The `isConnected` getter steps are to return true, if [this](https://webidl.spec.whatwg.org/#this) is [connected](#422-shadow-tree); otherwise false.

The `ownerDocument` getter steps are to return null, if [this](https://webidl.spec.whatwg.org/#this) is a [document](#45-interface-document); otherwise [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node).

> [!note]
> The [node document](#44-interface-node) of a [document](#45-interface-document) is that [document](#45-interface-document) itself. All [nodes](#42-node-tree) have a [node document](#44-interface-node) at all times.

The `getRootNode(options)` method steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [shadow-including root](#48-interface-shadowroot) if options\["[`composed`](#44-interface-node)"\] is true; otherwise [this](https://webidl.spec.whatwg.org/#this)’s [root](#11-trees).

The `parentNode` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [parent](#11-trees).

The `parentElement` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [parent element](#49-interface-element).

The `hasChildNodes()` method steps are to return true if [this](https://webidl.spec.whatwg.org/#this) has [children](#11-trees); otherwise false.

The `childNodes` getter steps are to return a [`NodeList`](#42101-interface-nodelist) rooted at [this](https://webidl.spec.whatwg.org/#this) matching only [children](#11-trees).

The `firstChild` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [first child](#11-trees).

The `lastChild` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [last child](#11-trees).

The `previousSibling` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [previous sibling](#11-trees).

The `nextSibling` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [next sibling](#11-trees).

---

The `nodeValue` getter steps are to return the following, switching on the interface [this](https://webidl.spec.whatwg.org/#this) [implements](https://webidl.spec.whatwg.org/#implements):

[`Attr`](#492-interface-attr)

[this](https://webidl.spec.whatwg.org/#this)’s [value](#492-interface-attr).

[`CharacterData`](#410-interface-characterdata)

[this](https://webidl.spec.whatwg.org/#this)’s [data](#410-interface-characterdata).

Otherwise

Null.

The [`nodeValue`](#44-interface-node) setter steps are to, if the given value is null, act as if it was the empty string instead, and then do as described below, switching on the interface [this](https://webidl.spec.whatwg.org/#this) [implements](https://webidl.spec.whatwg.org/#implements):

[`Attr`](#492-interface-attr)

[Set an existing attribute value](#492-interface-attr) with [this](https://webidl.spec.whatwg.org/#this) and the given value.

[`CharacterData`](#410-interface-characterdata)

[Replace data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with 0, [this](https://webidl.spec.whatwg.org/#this)’s [length](#42-node-tree), and the given value.

Otherwise

Do nothing.

To get text content with a [node](#42-node-tree) node, return the following, switching on the interface node [implements](https://webidl.spec.whatwg.org/#implements):

[`DocumentFragment`](#47-interface-documentfragment)

[`Element`](#49-interface-element)

The [descendant text content](#411-interface-text) of node.

[`Attr`](#492-interface-attr)

node’s [value](#492-interface-attr).

[`CharacterData`](#410-interface-characterdata)

node’s [data](#410-interface-characterdata).

Otherwise

Null.

The `textContent` getter steps are to return the result of running [get text content](#44-interface-node) with [this](https://webidl.spec.whatwg.org/#this).

To string replace all with a string string within a [node](#42-node-tree) parent, run these steps:
1. Let node be null.
2. If string is not the empty string, then set node to the result of [creating a text node](#411-interface-text) given parent’s [node document](#44-interface-node) and string.
3. [Replace all](#423-mutation-algorithms) with node within parent.

To set text content with a [node](#42-node-tree) node and a string value, do as defined below, switching on the interface node [implements](https://webidl.spec.whatwg.org/#implements):

[`DocumentFragment`](#47-interface-documentfragment)

[`Element`](#49-interface-element)

[String replace all](#44-interface-node) with value within node.

[`Attr`](#492-interface-attr)

[Set an existing attribute value](#492-interface-attr) with node and value.

[`CharacterData`](#410-interface-characterdata)

[Replace data](#410-interface-characterdata) of node with 0, node’s [length](#42-node-tree), and value.

Otherwise

Do nothing.

The [`textContent`](#44-interface-node) setter steps are to, if the given value is null, act as if it was the empty string instead, and then run [set text content](#44-interface-node) with [this](https://webidl.spec.whatwg.org/#this) and the given value.

---

`` node . `normalize()` ``

Removes [empty](#42-node-tree) [exclusive `Text` nodes](#411-interface-text) and concatenates the [data](#410-interface-characterdata) of remaining [contiguous exclusive `Text` nodes](#411-interface-text) into the first of their [nodes](#42-node-tree).

The `normalize()` method steps are to run these steps for each [descendant](#11-trees) [exclusive `Text` node](#411-interface-text) node of [this](https://webidl.spec.whatwg.org/#this):
1. Let length be node’s [length](#42-node-tree).
2. If length is zero, then [remove](#423-mutation-algorithms) node and continue with the next [exclusive `Text` node](#411-interface-text), if any.
3. Let data be the [concatenation](infra-spec-whatwg-org.md#47-strings) of the [data](#410-interface-characterdata) of node’s [contiguous exclusive `Text` nodes](#411-interface-text) (excluding itself), in [tree order](#11-trees).
4. [Replace data](#410-interface-characterdata) of node with length, 0, and data.
5. Let currentNode be node’s [next sibling](#11-trees).
6. While currentNode is an [exclusive `Text` node](#411-interface-text):
   1. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is currentNode: add length to its [start offset](#53-interface-abstractrange) and set its [start node](#53-interface-abstractrange) to node.
   2. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is currentNode: add length to its [end offset](#53-interface-abstractrange) and set its [end node](#53-interface-abstractrange) to node.
   3. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is currentNode’s [parent](#11-trees) and [start offset](#53-interface-abstractrange) is currentNode’s [index](#11-trees): set its [start node](#53-interface-abstractrange) to node and its [start offset](#53-interface-abstractrange) to length.
   4. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is currentNode’s [parent](#11-trees) and [end offset](#53-interface-abstractrange) is currentNode’s [index](#11-trees): set its [end node](#53-interface-abstractrange) to node and its [end offset](#53-interface-abstractrange) to length.
   5. Add currentNode’s [length](#42-node-tree) to length.
   6. Set currentNode to its [next sibling](#11-trees).
7. [Remove](#423-mutation-algorithms) node’s [contiguous exclusive `Text` nodes](#411-interface-text) (excluding itself), in [tree order](#11-trees).

---

`node . cloneNode([subtree = false])`

Returns a copy of node. If subtree is true, the copy also includes the node’s [descendants](#11-trees).

`node . isEqualNode(otherNode)`

Returns whether node and otherNode have the same properties.

[Specifications](#1-infrastructure) may define cloning steps for all or some [nodes](#42-node-tree). The algorithm is passed node, copy, and subtree as indicated in the [clone a node](#44-interface-node) algorithm.

> [!note]
> HTML defines [cloning steps](#44-interface-node) for several elements, such as [`input`](html-spec-whatwg-org.md#4105-the-input-element), [`script`](html-spec-whatwg-org.md#4121-the-script-element), and [`template`](html-spec-whatwg-org.md#4123-the-template-element). SVG ought to do the same for its [`script`](html-spec-whatwg-org.md#4121-the-script-element) elements, but does not.

To clone a node given a [node](#42-node-tree) node and an optional [document](#45-interface-document) document (default node’s [node document](#44-interface-node)), boolean subtree (default false), [node](#42-node-tree)-or-null parent (default null), and null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object fallbackRegistry (default null):
1. [Assert](infra-spec-whatwg-org.md#310-assertions): node is not a [document](#45-interface-document) or node is document.
2. Let copy be the result of [cloning a single node](#44-interface-node) given node, document, and fallbackRegistry.
3. Run any [cloning steps](#44-interface-node) defined for node in [other applicable specifications](#1-infrastructure) and pass node, copy, and subtree as parameters.
4. If parent is non-null, then [append](#423-mutation-algorithms) copy to parent.
5. If subtree is true, then for each child of node’s [children](#11-trees), in [tree order](#11-trees): [clone a node](#44-interface-node) given child with [*document*](#44-interface-node) set to document, [*subtree*](#44-interface-node) set to subtree, [*parent*](#44-interface-node) set to copy, and [*fallbackRegistry*](#44-interface-node) set to fallbackRegistry.
6. If node is an [element](#49-interface-element), node is a [shadow host](#49-interface-element), and node’s [shadow root](#49-interface-element)’s [clonable](#48-interface-shadowroot) is true:
   1. [Assert](infra-spec-whatwg-org.md#310-assertions): copy is not a [shadow host](#49-interface-element).
   2. Let shadowRootRegistry be node’s [shadow root](#49-interface-element)’s [custom element registry](#48-interface-shadowroot).
   3. If shadowRootRegistry [is a global custom element registry](#45-interface-document), then set shadowRootRegistry to document’s [custom element registry](#45-interface-document)’s [effective global custom element registry](#45-interface-document).
   4. [Attach a shadow root](#49-interface-element) with copy, node’s [shadow root](#49-interface-element)’s [mode](#48-interface-shadowroot), node’s [shadow root](#49-interface-element)’s [delegates focus](#48-interface-shadowroot), node’s [shadow root](#49-interface-element)’s [serializable](#48-interface-shadowroot), node’s [shadow root](#49-interface-element)’s [slot assignment](#48-interface-shadowroot), true, and shadowRootRegistry.
   5. Set copy’s [shadow root](#49-interface-element)’s [declarative](#48-interface-shadowroot) to node’s [shadow root](#49-interface-element)’s [declarative](#48-interface-shadowroot).
   6. Set copy’s [shadow root](#49-interface-element)’s [keep custom element registry null](#48-interface-shadowroot) to node’s [shadow root](#49-interface-element)’s [keep custom element registry null](#48-interface-shadowroot).
   7. For each child of node’s [shadow root](#49-interface-element)’s [children](#11-trees), in [tree order](#11-trees): [clone a node](#44-interface-node) given child with [*document*](#44-interface-node) set to document, [*subtree*](#44-interface-node) set to true, and [*parent*](#44-interface-node) set to copy’s [shadow root](#49-interface-element).

      > [!note]
      > This intentionally does not pass the [*fallbackRegistry*](#44-interface-node) argument.

7. Return copy.

To clone a single node given a [node](#42-node-tree) node, [document](#45-interface-document) document, and null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object fallbackRegistry:
1. Let copy be null.
2. If node is an [element](#49-interface-element):
   1. Let registry be node’s [custom element registry](#49-interface-element).
   2. If registry is null, then set registry to fallbackRegistry.
   3. If registry [is a global custom element registry](#45-interface-document), then set registry to document’s [custom element registry](#45-interface-document)’s [effective global custom element registry](#45-interface-document).
   4. Set copy to the result of [creating an element](#49-interface-element), given document, node’s [local name](#49-interface-element), node’s [namespace](#49-interface-element), node’s [namespace prefix](#49-interface-element), node’s [`is` value](#49-interface-element), false, and registry.
   5. [For each](infra-spec-whatwg-org.md#51-lists) attribute of node’s [attribute list](#49-interface-element):
      1. Let copyAttribute be the result of [cloning a single node](#44-interface-node) given attribute, document, and null.
      2. [Append](#49-interface-element) copyAttribute to copy.
3. Otherwise, if node is a [document](#45-interface-document), set copy to the result of [creating a document](#45-interface-document) that implements the same interfaces as node, given document’s [relevant realm](html-spec-whatwg-org.md#81334-relevant).
4. Otherwise, set copy to the result of [creating a node](#44-interface-node) that [implements](https://webidl.spec.whatwg.org/#implements) the same interfaces as node, given document.
5. Fulfill these additional requirements, switching on the interface node [implements](https://webidl.spec.whatwg.org/#implements):

   [`Document`](#45-interface-document)
   1. Set copy’s [encoding](#45-interface-document), [content type](#45-interface-document), [URL](#45-interface-document), [origin](#45-interface-document), [type](#45-interface-document), [mode](#45-interface-document), and [allow declarative shadow roots](#45-interface-document), to those of node.
   2. If node’s [custom element registry](#45-interface-document)’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is true, then set copy’s [custom element registry](#45-interface-document) to node’s [custom element registry](#45-interface-document).

   [`DocumentType`](#46-interface-documenttype)

   Set copy’s [name](#46-interface-documenttype), [public ID](#46-interface-documenttype), and [system ID](#46-interface-documenttype) to those of node.

   [`Attr`](#492-interface-attr)

   Set copy’s [namespace](#492-interface-attr), [namespace prefix](#492-interface-attr), [local name](#492-interface-attr), and [value](#492-interface-attr) to those of node.

   [`Text`](#411-interface-text)

   [`Comment`](#414-interface-comment)

   Set copy’s [data](#410-interface-characterdata) to that of node.

   [`ProcessingInstruction`](#413-interface-processinginstruction)

   Set copy’s [target](#413-interface-processinginstruction) and [data](#410-interface-characterdata) to those of node.

   Otherwise

   Do nothing.

6. [Assert](infra-spec-whatwg-org.md#310-assertions): copy is a [node](#42-node-tree).
7. If node is a [document](#45-interface-document), then set document to copy.
8. Set copy’s [node document](#44-interface-node) to document.
9. Return copy.

The `cloneNode(subtree)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this) is a [shadow root](#48-interface-shadowroot), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Return the result of [cloning a node](#44-interface-node) given [this](https://webidl.spec.whatwg.org/#this) with [*subtree*](#44-interface-node) set to subtree.

A [node](#42-node-tree) A equals a [node](#42-node-tree) B if all of the following conditions are true:
- A and B [implement](https://webidl.spec.whatwg.org/#implements) the same interfaces.
- The following are equal, switching on the interface A [implements](https://webidl.spec.whatwg.org/#implements):

  [`DocumentType`](#46-interface-documenttype)

  Its [name](#46-interface-documenttype), [public ID](#46-interface-documenttype), and [system ID](#46-interface-documenttype).

  [`Element`](#49-interface-element)

  Its [namespace](#49-interface-element), [namespace prefix](#49-interface-element), [local name](#49-interface-element), and its [attribute list](#49-interface-element)’s [size](infra-spec-whatwg-org.md#51-lists).

  [`Attr`](#492-interface-attr)

  Its [namespace](#492-interface-attr), [local name](#492-interface-attr), and [value](#492-interface-attr).

  [`ProcessingInstruction`](#413-interface-processinginstruction)

  Its [target](#413-interface-processinginstruction) and [data](#410-interface-characterdata).

  [`Text`](#411-interface-text)

  [`Comment`](#414-interface-comment)

  Its [data](#410-interface-characterdata).

  Otherwise

  —

- If A is an [element](#49-interface-element), each [attribute](#492-interface-attr) in its [attribute list](#49-interface-element) [equals](#44-interface-node) an [attribute](#492-interface-attr) in B’s [attribute list](#49-interface-element).
- A and B have the same number of [children](#11-trees).
- Each [child](#11-trees) of A [equals](#44-interface-node) the [child](#11-trees) of B at the identical [index](#11-trees).

The `isEqualNode(otherNode)` method steps are to return true if otherNode is non-null and [this](https://webidl.spec.whatwg.org/#this) [equals](#44-interface-node) otherNode; otherwise false.

The `isSameNode(otherNode)` method steps are to return true if otherNode is [this](https://webidl.spec.whatwg.org/#this); otherwise false.

---

`` node . `compareDocumentPosition(other)` ``

Returns a bitmask indicating the position of other relative to node. These are the bits that can be set:

`` `Node` . `DOCUMENT_POSITION_DISCONNECTED` `` (1)

Set when node and other are not in the same [tree](#11-trees).

`` `Node` . `DOCUMENT_POSITION_PRECEDING` `` (2)

Set when other is [preceding](#11-trees) node.

`` `Node` . `DOCUMENT_POSITION_FOLLOWING` `` (4)

Set when other is [following](#11-trees) node.

`` `Node` . `DOCUMENT_POSITION_CONTAINS` `` (8)

Set when other is an [ancestor](#11-trees) of node.

`` `Node` . `DOCUMENT_POSITION_CONTAINED_BY` `` (16, 10 in hexadecimal)

Set when other is a [descendant](#11-trees) of node.

`` node . `contains(other)` ``

Returns true if other is an [inclusive descendant](#11-trees) of node; otherwise false.

These are the constants [`compareDocumentPosition()`](#44-interface-node) returns as mask:
- `DOCUMENT_POSITION_DISCONNECTED` (1);
- `DOCUMENT_POSITION_PRECEDING` (2);
- `DOCUMENT_POSITION_FOLLOWING` (4);
- `DOCUMENT_POSITION_CONTAINS` (8);
- `DOCUMENT_POSITION_CONTAINED_BY` (16, 10 in hexadecimal);
- `DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC` (32, 20 in hexadecimal).

The `compareDocumentPosition(other)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this) is other, then return zero.
2. Let node1 be other and node2 be [this](https://webidl.spec.whatwg.org/#this).
3. Let attr1 and attr2 be null.
4. If node1 is an [attribute](#492-interface-attr), then set attr1 to node1 and node1 to attr1’s [element](#492-interface-attr).
5. If node2 is an [attribute](#492-interface-attr):
   1. Set attr2 to node2 and node2 to attr2’s [element](#492-interface-attr).
   2. If attr1 and node1 are non-null, and node2 is node1:
      1. [For each](infra-spec-whatwg-org.md#51-lists) attr of node2’s [attribute list](#49-interface-element):
         1. If attr [equals](#44-interface-node) attr1, then return the result of adding [`DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC`](#44-interface-node) and [`DOCUMENT_POSITION_PRECEDING`](#44-interface-node).
         2. If attr [equals](#44-interface-node) attr2, then return the result of adding [`DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC`](#44-interface-node) and [`DOCUMENT_POSITION_FOLLOWING`](#44-interface-node).
6. If node1 or node2 is null, or node1’s [root](#11-trees) is not node2’s [root](#11-trees), then return the result of adding [`DOCUMENT_POSITION_DISCONNECTED`](#44-interface-node), [`DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC`](#44-interface-node), and either [`DOCUMENT_POSITION_PRECEDING`](#44-interface-node) or [`DOCUMENT_POSITION_FOLLOWING`](#44-interface-node), with the constraint that this is to be consistent, together.

   > [!note]
   > Whether to return [`DOCUMENT_POSITION_PRECEDING`](#44-interface-node) or [`DOCUMENT_POSITION_FOLLOWING`](#44-interface-node) is typically implemented via pointer comparison. In JavaScript implementations a cached `Math.random()` value can be used.

7. If node1 is an [ancestor](#11-trees) of node2 and attr1 is null, or node1 is node2 and attr2 is non-null, then return the result of adding [`DOCUMENT_POSITION_CONTAINS`](#44-interface-node) to [`DOCUMENT_POSITION_PRECEDING`](#44-interface-node).
8. If node1 is a [descendant](#11-trees) of node2 and attr2 is null, or node1 is node2 and attr1 is non-null, then return the result of adding [`DOCUMENT_POSITION_CONTAINED_BY`](#44-interface-node) to [`DOCUMENT_POSITION_FOLLOWING`](#44-interface-node).
9. If node1 is [preceding](#11-trees) node2, then return [`DOCUMENT_POSITION_PRECEDING`](#44-interface-node).

   > [!note]
   > Due to the way [attributes](#492-interface-attr) are handled in this algorithm this results in a [node](#42-node-tree)’s [attributes](#492-interface-attr) counting as [preceding](#11-trees) that [node](#42-node-tree)’s [children](#11-trees), despite [attributes](#492-interface-attr) not [participating](#11-trees) in the same [tree](#11-trees).

10. Return [`DOCUMENT_POSITION_FOLLOWING`](#44-interface-node).

The `contains(other)` method steps are to return true if other is an [inclusive descendant](#11-trees) of [this](https://webidl.spec.whatwg.org/#this); otherwise false (including when other is null).

---

To locate a namespace prefix for an element using namespace, run these steps:
1. If element’s [namespace](#49-interface-element) is namespace and its [namespace prefix](#49-interface-element) is non-null, then return its [namespace prefix](#49-interface-element).
2. If element [has](#49-interface-element) an [attribute](#492-interface-attr) whose [namespace prefix](#492-interface-attr) is "`xmlns`" and [value](#492-interface-attr) is namespace, then return element’s first such [attribute](#492-interface-attr)’s [local name](#492-interface-attr).
3. If element’s [parent element](#49-interface-element) is non-null, then return the result of running [locate a namespace prefix](#44-interface-node) on that [element](#49-interface-element) using namespace.
4. Return null.

To locate a namespace for a node using prefix, switch on the interface node [implements](https://webidl.spec.whatwg.org/#implements):

[`Element`](#49-interface-element)
1. If prefix is "`xml`", then return the [XML namespace](infra-spec-whatwg-org.md#8-namespaces).
2. If prefix is "`xmlns`", then return the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces).
3. If its [namespace](#49-interface-element) is non-null and its [namespace prefix](#49-interface-element) is prefix, then return [namespace](#49-interface-element).
4. If it [has](#49-interface-element) an [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces), [namespace prefix](#492-interface-attr) is "`xmlns`", and [local name](#492-interface-attr) is prefix, or if prefix is null and it [has](#49-interface-element) an [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces), [namespace prefix](#492-interface-attr) is null, and [local name](#492-interface-attr) is "`xmlns`", then return its [value](#492-interface-attr) if it is not the empty string, and null otherwise.
5. If its [parent element](#49-interface-element) is null, then return null.
6. Return the result of running [locate a namespace](#44-interface-node) on its [parent element](#49-interface-element) using prefix.

[`Document`](#45-interface-document)
1. If its [document element](#421-document-tree) is null, then return null.
2. Return the result of running [locate a namespace](#44-interface-node) on its [document element](#421-document-tree) using prefix.

[`DocumentType`](#46-interface-documenttype)

[`DocumentFragment`](#47-interface-documentfragment)

Return null.

[`Attr`](#492-interface-attr)
1. If its [element](#492-interface-attr) is null, then return null.
2. Return the result of running [locate a namespace](#44-interface-node) on its [element](#492-interface-attr) using prefix.

Otherwise
1. If its [parent element](#49-interface-element) is null, then return null.
2. Return the result of running [locate a namespace](#44-interface-node) on its [parent element](#49-interface-element) using prefix.

The `lookupPrefix(namespace)` method steps are:
1. If namespace is null or the empty string, then return null.
2. Switch on the interface [this](https://webidl.spec.whatwg.org/#this) [implements](https://webidl.spec.whatwg.org/#implements):

   [`Element`](#49-interface-element)

   Return the result of [locating a namespace prefix](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this) using namespace.

   [`Document`](#45-interface-document)
   1. If [this](https://webidl.spec.whatwg.org/#this)’s [document element](#421-document-tree) is null, then return null.
   2. Return the result of [locating a namespace prefix](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this)’s [document element](#421-document-tree) using namespace.

   [`DocumentType`](#46-interface-documenttype)

   [`DocumentFragment`](#47-interface-documentfragment)

   Return null.

   [`Attr`](#492-interface-attr)
   1. If [this](https://webidl.spec.whatwg.org/#this)’s [element](#492-interface-attr) is null, then return null.
   2. Return the result of [locating a namespace prefix](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this)’s [element](#492-interface-attr) using namespace.

   Otherwise
   1. If [this](https://webidl.spec.whatwg.org/#this)’s [parent element](#49-interface-element) is null, then return null.
   2. Return the result of [locating a namespace prefix](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this)’s [parent element](#49-interface-element) using namespace.

The `lookupNamespaceURI(prefix)` method steps are:
1. If prefix is the empty string, then set it to null.
2. Return the result of running [locate a namespace](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this) using prefix.

The `isDefaultNamespace(namespace)` method steps are:
1. If namespace is the empty string, then set it to null.
2. Let defaultNamespace be the result of running [locate a namespace](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this) using null.
3. Return true if defaultNamespace is the same as namespace; otherwise false.

---

The `insertBefore(node, child)` method steps are to return the result of [pre-inserting](#423-mutation-algorithms) node into [this](https://webidl.spec.whatwg.org/#this) before child.

The `appendChild(node)` method steps are to return the result of [appending](#423-mutation-algorithms) node to [this](https://webidl.spec.whatwg.org/#this).

The `replaceChild(node, child)` method steps are to return the result of [replacing](#423-mutation-algorithms) child with node within [this](https://webidl.spec.whatwg.org/#this).

The `removeChild(child)` method steps are to return the result of [pre-removing](#423-mutation-algorithms) child from [this](https://webidl.spec.whatwg.org/#this).

---

The list of elements with qualified name qualifiedName for a [node](#42-node-tree) root is the [`HTMLCollection`](#42102-interface-htmlcollection) returned by the following algorithm:
1. If qualifiedName is U+002A (\*), then return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches only [descendant](#11-trees) [elements](#49-interface-element).
2. Otherwise, if root’s [node document](#44-interface-node) is an [HTML document](#45-interface-document), return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches the following [descendant](#11-trees) [elements](#49-interface-element):
   - Whose [namespace](#49-interface-element) is the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and whose [qualified name](#49-interface-element) is qualifiedName, in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
   - Whose [namespace](#49-interface-element) is *not* the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and whose [qualified name](#49-interface-element) is qualifiedName.
3. Otherwise, return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches [descendant](#11-trees) [elements](#49-interface-element) whose [qualified name](#49-interface-element) is qualifiedName.

When invoked with the same argument, and as long as root’s [node document](#44-interface-node)’s [type](#45-interface-document) has not changed, the same [`HTMLCollection`](#42102-interface-htmlcollection) object may be returned as returned by an earlier call.

The list of elements with namespace namespace and local name localName for a [node](#42-node-tree) root is the [`HTMLCollection`](#42102-interface-htmlcollection) returned by the following algorithm:
1. If namespace is the empty string, then set it to null.
2. If both namespace and localName are U+002A (\*), then return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches [descendant](#11-trees) [elements](#49-interface-element).
3. If namespace is U+002A (\*), then return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches [descendant](#11-trees) [elements](#49-interface-element) whose [local name](#49-interface-element) is localName.
4. If localName is U+002A (\*), then return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches [descendant](#11-trees) [elements](#49-interface-element) whose [namespace](#49-interface-element) is namespace.
5. Return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches [descendant](#11-trees) [elements](#49-interface-element) whose [namespace](#49-interface-element) is namespace and [local name](#49-interface-element) is localName.

When invoked with the same arguments, the same [`HTMLCollection`](#42102-interface-htmlcollection) object may be returned as returned by an earlier call.

The list of elements with class names classNames for a [node](#42-node-tree) root is the [`HTMLCollection`](#42102-interface-htmlcollection) returned by the following algorithm:
1. Let classes be the result of running the [ordered set parser](#12-ordered-sets) on classNames.
2. If classes is the empty set, return an empty [`HTMLCollection`](#42102-interface-htmlcollection).
3. Return an [`HTMLCollection`](#42102-interface-htmlcollection) rooted at root, whose filter matches [descendant](#11-trees) [elements](#49-interface-element) that have all their [classes](#49-interface-element) in classes.

   The comparisons for the [classes](#49-interface-element) must be done in an [ASCII case-insensitive](infra-spec-whatwg-org.md#47-strings) manner if root’s [node document](#44-interface-node)’s [mode](#45-interface-document) is "`quirks`"; otherwise in an [identical to](infra-spec-whatwg-org.md#47-strings) manner.

When invoked with the same argument, the same [`HTMLCollection`](#42102-interface-htmlcollection) object may be returned as returned by an earlier call.

### 4.5. Interface [`Document`](#45-interface-document)

```webidl
[Exposed=Window]
interface Document : Node {
  constructor();

  [SameObject] readonly attribute DOMImplementation implementation;
  readonly attribute USVString URL;
  readonly attribute USVString documentURI;
  readonly attribute DOMString compatMode;
  readonly attribute DOMString characterSet;
  readonly attribute DOMString charset; // legacy alias of .characterSet
  readonly attribute DOMString inputEncoding; // legacy alias of .characterSet
  readonly attribute DOMString contentType;

  readonly attribute DocumentType? doctype;
  readonly attribute Element? documentElement;
  HTMLCollection getElementsByTagName(DOMString qualifiedName);
  HTMLCollection getElementsByTagNameNS(DOMString? namespace, DOMString localName);
  HTMLCollection getElementsByClassName(DOMString classNames);

  [CEReactions, NewObject] Element createElement(DOMString localName, optional (DOMString or ElementCreationOptions) options = {});
  [CEReactions, NewObject] Element createElementNS(DOMString? namespace, DOMString qualifiedName, optional (DOMString or ElementCreationOptions) options = {});
  [NewObject] DocumentFragment createDocumentFragment();
  [NewObject] Text createTextNode(DOMString data);
  [NewObject] CDATASection createCDATASection(DOMString data);
  [NewObject] Comment createComment(DOMString data);
  [NewObject] ProcessingInstruction createProcessingInstruction(DOMString target, DOMString data);

  [CEReactions, NewObject] Node importNode(Node node, optional (boolean or ImportNodeOptions) options = false);
  [CEReactions] Node adoptNode(Node node);

  [NewObject] Attr createAttribute(DOMString localName);
  [NewObject] Attr createAttributeNS(DOMString? namespace, DOMString qualifiedName);

  [NewObject] Event createEvent(DOMString interface); // legacy

  [NewObject] Range createRange();

  // NodeFilter.SHOW_ALL = 0xFFFFFFFF
  [NewObject] NodeIterator createNodeIterator(Node root, optional unsigned long whatToShow = 0xFFFFFFFF, optional NodeFilter? filter = null);
  [NewObject] TreeWalker createTreeWalker(Node root, optional unsigned long whatToShow = 0xFFFFFFFF, optional NodeFilter? filter = null);
};

[Exposed=Window]
interface XMLDocument : Document {};

dictionary ElementCreationOptions {
  CustomElementRegistry? customElementRegistry;
  DOMString is;
};

dictionary ImportNodeOptions {
  CustomElementRegistry customElementRegistry;
  boolean selfOnly = false;
};

```

[`Document`](#45-interface-document) [nodes](#42-node-tree) are simply known as documents.

A [document](#45-interface-document)’s [node document](#44-interface-node) is itself.

Each [document](#45-interface-document) has an associated encoding (an [encoding](https://encoding.spec.whatwg.org/#encoding)), content type (a string), URL (a [URL](https://url.spec.whatwg.org/#concept-url)), origin (an [origin](html-spec-whatwg-org.md#711-origins)), type ("`xml`" or "`html`"), mode ("`no-quirks`", "`quirks`", or "`limited-quirks`"), allow declarative shadow roots (a boolean), and custom element registry (null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object). [\[ENCODING\]](#normative-references) [\[URL\]](#normative-references) [\[HTML\]](#normative-references)

Unless stated otherwise, a [document](#45-interface-document)’s [encoding](#45-interface-document) is the [utf-8](https://encoding.spec.whatwg.org/#utf-8) [encoding](https://encoding.spec.whatwg.org/#encoding), [content type](#45-interface-document) is "`application/xml`", [URL](#45-interface-document) is "`about:blank`", [origin](#45-interface-document) is an [opaque origin](html-spec-whatwg-org.md#711-origins), [type](#45-interface-document) is "`xml`", [mode](#45-interface-document) is "`no-quirks`", [allow declarative shadow roots](#45-interface-document) is false, and [custom element registry](#45-interface-document) is null.

A [document](#45-interface-document) is said to be an XML document if its [type](#45-interface-document) is "`xml`"; otherwise an HTML document. Whether a [document](#45-interface-document) is an [HTML document](#45-interface-document) or an [XML document](#45-interface-document) affects the behavior of certain APIs.

A [document](#45-interface-document) is said to be in no-quirks mode if its [mode](#45-interface-document) is "`no-quirks`", quirks mode if its [mode](#45-interface-document) is "`quirks`", and limited-quirks mode if its [mode](#45-interface-document) is "`limited-quirks`".

> [!note]
> The [mode](#45-interface-document) is only ever changed from the default for [documents](#45-interface-document) created by the [HTML parser](html-spec-whatwg-org.md#132-parsing-html-documents) based on the presence, absence, or value of the DOCTYPE string, and by a new [browsing context](html-spec-whatwg-org.md#732-browsing-contexts) (initial "`about:blank`"). [\[HTML\]](#normative-references)
> 
> [No-quirks mode](#45-interface-document) was originally known as "standards mode" and [limited-quirks mode](#45-interface-document) was once known as "almost standards mode". They have been renamed because their details are now defined by standards. (And because Ian Hickson vetoed their original names on the basis that they are nonsensical.)

A [document](#45-interface-document)’s [get the parent](#27-interface-eventtarget) algorithm, given an event, returns null if event’s [`type`](#22-interface-event) attribute value is "`load`" or [document](#45-interface-document) does not have a [browsing context](html-spec-whatwg-org.md#732-browsing-contexts); otherwise the [document](#45-interface-document)’s [relevant global object](html-spec-whatwg-org.md#81334-relevant).

To create a document that implements an interface interface, given a [realm](https://tc39.es/ecma262/#realm) realm:
1. [Assert](infra-spec-whatwg-org.md#310-assertions): interface is [`Document`](#45-interface-document) or an interface that inherits from [`Document`](#45-interface-document).
2. Return a new [node](#42-node-tree) that [implements](https://webidl.spec.whatwg.org/#implements) interface, in realm.

---

`` document = new `Document()` ``

Returns a new [document](#45-interface-document).

`` document . `implementation` ``

Returns document’s [`DOMImplementation`](#451-interface-domimplementation) object.

`` document . `URL` ``

`` document . `documentURI` ``

Returns document’s [URL](#45-interface-document).

`` document . `compatMode` ``

Returns the string "`BackCompat`" if document’s [mode](#45-interface-document) is "`quirks`"; otherwise "`CSS1Compat`".

`` document . `characterSet` ``

Returns document’s [encoding](#45-interface-document).

`` document . `contentType` ``

Returns document’s [content type](#45-interface-document).

The `new Document()` constructor steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [origin](#45-interface-document) to the [origin](#45-interface-document) of [current global object](html-spec-whatwg-org.md#81333-current)’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object). [\[HTML\]](#normative-references)

> [!note]
> Unlike [`createDocument()`](#451-interface-domimplementation), this constructor does not return an [`XMLDocument`](#45-interface-document) object, but a [document](#45-interface-document) ([`Document`](#45-interface-document) object).

The `implementation` getter steps are to return the [`DOMImplementation`](#451-interface-domimplementation) object that is associated with [this](https://webidl.spec.whatwg.org/#this).

The `URL` and `documentURI` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [URL](#45-interface-document), [serialized](https://url.spec.whatwg.org/#concept-url-serializer).

The `compatMode` getter steps are to return "`BackCompat`" if [this](https://webidl.spec.whatwg.org/#this)’s [mode](#45-interface-document) is "`quirks`"; otherwise "`CSS1Compat`".

The `characterSet`, `charset`, and `inputEncoding` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [encoding](#45-interface-document)’s [name](https://encoding.spec.whatwg.org/#name).

The `contentType` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [content type](#45-interface-document).

---

document . [`doctype`](#45-interface-document)

Returns the [doctype](#46-interface-documenttype) or null if there is none.

document . [`documentElement`](#45-interface-document)

Returns the [document element](#421-document-tree).

`collection = document . getElementsByTagName(qualifiedName)`

If qualifiedName is "`*`" returns an [`HTMLCollection`](#42102-interface-htmlcollection) of all [descendant](#11-trees) [elements](#49-interface-element).

Otherwise, returns an [`HTMLCollection`](#42102-interface-htmlcollection) of all [descendant](#11-trees) [elements](#49-interface-element) whose [qualified name](#49-interface-element) is qualifiedName. (Matches case-insensitively against [elements](#49-interface-element) in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) within an [HTML document](#45-interface-document).)

`collection = document . getElementsByTagNameNS(namespace, localName)`

If namespace and localName are "`*`", returns an [`HTMLCollection`](#42102-interface-htmlcollection) of all [descendant](#11-trees) [elements](#49-interface-element).

If only namespace is "`*`", returns an [`HTMLCollection`](#42102-interface-htmlcollection) of all [descendant](#11-trees) [elements](#49-interface-element) whose [local name](#49-interface-element) is localName.

If only localName is "`*`", returns an [`HTMLCollection`](#42102-interface-htmlcollection) of all [descendant](#11-trees) [elements](#49-interface-element) whose [namespace](#49-interface-element) is namespace.

Otherwise, returns an [`HTMLCollection`](#42102-interface-htmlcollection) of all [descendant](#11-trees) [elements](#49-interface-element) whose [namespace](#49-interface-element) is namespace and [local name](#49-interface-element) is localName.

`collection = document . getElementsByClassName(classNames)`

`collection = element . getElementsByClassName(classNames)`

Returns an [`HTMLCollection`](#42102-interface-htmlcollection) of the [elements](#49-interface-element) in the object on which the method was invoked (a [document](#45-interface-document) or an [element](#49-interface-element)) that have all the classes given by classNames. The classNames argument is interpreted as a space-separated list of classes.

The `doctype` getter steps are to return the [child](#11-trees) of [this](https://webidl.spec.whatwg.org/#this) that is a [doctype](#46-interface-documenttype); otherwise null.

The `documentElement` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [document element](#421-document-tree).

The `getElementsByTagName(qualifiedName)` method steps are to return the [list of elements with qualified name qualifiedName](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this).

> [!note]
> Thus, in an [HTML document](#45-interface-document), `document.getElementsByTagName("FOO")` will match `<FOO>` elements that are not in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), and `<foo>` elements that are in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), but not `<FOO>` elements that are in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces).

The `getElementsByTagNameNS(namespace, localName)` method steps are to return the [list of elements with namespace namespace and local name localName](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this).

The `getElementsByClassName(classNames)` method steps are to return the [list of elements with class names classNames](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this).

> [!example]
> Given the following XHTML fragment:
> 
> ```html
> <div id="example">
>   <p id="p1" class="aaa bbb"/>
>   <p id="p2" class="aaa ccc"/>
>   <p id="p3" class="bbb ccc"/>
> </div>
> ```
> 
> A call to `document.getElementById("example").getElementsByClassName("aaa")` would return an [`HTMLCollection`](#42102-interface-htmlcollection) with the two paragraphs `p1` and `p2` in it.
> 
> A call to `getElementsByClassName("ccc bbb")` would only return one node, however, namely `p3`. A call to `document.getElementById("example").getElementsByClassName("bbb  ccc ")` would return the same thing.
> 
> A call to `getElementsByClassName("aaa,bbb")` would return no nodes; none of the elements above are in the `aaa,bbb` class.

---

`element = document . createElement(localName [, options])`

Returns an [element](#49-interface-element) with localName as [local name](#49-interface-element) (if document is an [HTML document](#45-interface-document), localName gets lowercased). The [element](#49-interface-element)’s [namespace](#49-interface-element) is the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) when document is an [HTML document](#45-interface-document) or document’s [content type](#45-interface-document) is "`application/xhtml+xml`"; otherwise null.

When supplied, options’s [`customElementRegistry`](#45-interface-document) can be used to set the [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface).

When supplied, options’s [`is`](#45-interface-document) can be used to create a [customized built-in element](html-spec-whatwg-org.md#4133-core-concepts).

If localName is not a [valid element local name](#14-name-validation) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown.

When both options’s [`customElementRegistry`](#45-interface-document) and options’s [`is`](#45-interface-document) are supplied, a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown.

`element = document . createElementNS(namespace, qualifiedName [, options])`

Returns an [element](#49-interface-element) with [namespace](#49-interface-element) namespace. Its [namespace prefix](#49-interface-element) will be everything before U+003A (:) in qualifiedName or null. Its [local name](#49-interface-element) will be everything after U+003A (:) in qualifiedName or qualifiedName.

When supplied, options’s [`customElementRegistry`](#45-interface-document) can be used to set the [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface).

When supplied, options’s [`is`](#45-interface-document) can be used to create a [customized built-in element](html-spec-whatwg-org.md#4133-core-concepts).

If qualifiedName is not a (possibly-prefixed) [valid element local name](#14-name-validation) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown.

If one of the following conditions is true a "[`NamespaceError`](https://webidl.spec.whatwg.org/#namespaceerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown:
- [Namespace prefix](#49-interface-element) is non-null and namespace is the empty string.
- [Namespace prefix](#49-interface-element) is "`xml`" and namespace is not the [XML namespace](infra-spec-whatwg-org.md#8-namespaces).
- qualifiedName or [namespace prefix](#49-interface-element) is "`xmlns`" and namespace is not the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces).
- namespace is the [XMLNS namespace](infra-spec-whatwg-org.md#8-namespaces) and neither qualifiedName nor [namespace prefix](#49-interface-element) is "`xmlns`".

When both options’s [`customElementRegistry`](#45-interface-document) and options’s [`is`](#45-interface-document) are supplied, a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown.

`` documentFragment = document . `createDocumentFragment()` ``

Returns a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree).

`` text = document . `createTextNode(data)` ``

Returns a [`Text`](#411-interface-text) [node](#42-node-tree) whose [data](#410-interface-characterdata) is data.

`` text = document . `createCDATASection(data)` ``

Returns a [`CDATASection`](#412-interface-cdatasection) [node](#42-node-tree) whose [data](#410-interface-characterdata) is data.

`` comment = document . `createComment(data)` ``

Returns a [`Comment`](#414-interface-comment) [node](#42-node-tree) whose [data](#410-interface-characterdata) is data.

`` processingInstruction = document . `createProcessingInstruction(target, data)` ``

Returns a [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) whose [target](#413-interface-processinginstruction) is target and [data](#410-interface-characterdata) is data. If target does not match the [`Name`](https://www.w3.org/TR/xml/#NT-Name) production an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown. If data contains "`?>`" an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) will be thrown.

The element interface for any name and namespace is [`Element`](#49-interface-element), unless stated otherwise.

> [!note]
> The HTML Standard will, e.g., define that for `html` and the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), the [`HTMLHtmlElement`](html-spec-whatwg-org.md#411-the-html-element) interface is used. [\[HTML\]](#normative-references)

The `createElement(localName, options)` method steps are:
1. If localName is not a [valid element local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If [this](https://webidl.spec.whatwg.org/#this) is an [HTML document](#45-interface-document), then set localName to localName in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
3. Let registry and is be the result of [flattening element creation options](#45-interface-document) given options and [this](https://webidl.spec.whatwg.org/#this).
4. Let namespace be the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), if [this](https://webidl.spec.whatwg.org/#this) is an [HTML document](#45-interface-document) or [this](https://webidl.spec.whatwg.org/#this)’s [content type](#45-interface-document) is "`application/xhtml+xml`"; otherwise null.
5. Return the result of [creating an element](#49-interface-element) given [this](https://webidl.spec.whatwg.org/#this), localName, namespace, null, is, true, and registry.

The internal `createElementNS` steps, given document, namespace, qualifiedName, and options, are as follows:
1. Let (namespace, prefix, localName) be the result of [validating and extracting](#14-name-validation) namespace and qualifiedName given "`element`".
2. Let registry and is be the result of [flattening element creation options](#45-interface-document) given options and [this](https://webidl.spec.whatwg.org/#this).
3. Return the result of [creating an element](#49-interface-element) given document, localName, namespace, prefix, is, true, and registry.

The `createElementNS(namespace, qualifiedName, options)` method steps are to return the result of running the [internal `createElementNS` steps](#45-interface-document), given [this](https://webidl.spec.whatwg.org/#this), namespace, qualifiedName, and options.

To flatten element creation options, given a string or [`ElementCreationOptions`](#45-interface-document) dictionary options and a [document](#45-interface-document) document:
1. Let registry be the result of [looking up a custom element registry](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) given document.
2. Let is be null.
3. If options is a dictionary:
   1. If options\["[`is`](#45-interface-document)"\] [exists](infra-spec-whatwg-org.md#52-maps), then set is to it.
   2. If options\["[`customElementRegistry`](#45-interface-document)"\] [exists](infra-spec-whatwg-org.md#52-maps):
      1. If is is non-null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
      2. Set registry to options\["[`customElementRegistry`](#45-interface-document)"\].
   3. If registry is non-null, registry’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is false, and registry is not document’s [custom element registry](#45-interface-document), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. Return registry and is.

> [!note]
> [`createElement()`](#45-interface-document) and [`createElementNS()`](#45-interface-document)’s options parameter is allowed to be a string for web compatibility.

The `createDocumentFragment()` method steps are to return the result of [creating a document fragment](#47-interface-documentfragment) given [this](https://webidl.spec.whatwg.org/#this).

The `createTextNode(data)` method steps are to return the result of [creating a text node](#411-interface-text) given [this](https://webidl.spec.whatwg.org/#this) and data.

The `createCDATASection(data)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this) is an [HTML document](#45-interface-document), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If data contains the string "`]]>`", then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Return the result of [creating a CDATA section node](#412-interface-cdatasection) given [this](https://webidl.spec.whatwg.org/#this) and data.

The `createComment(data)` method steps are to return the result of [creating a comment node](#414-interface-comment) given [this](https://webidl.spec.whatwg.org/#this) and data.

The `createProcessingInstruction(target, data)` method steps are to return the result of [creating a processing instruction node](#413-interface-processinginstruction) given [this](https://webidl.spec.whatwg.org/#this), target, and data.

---

`clone = document . importNode(node [, options = false])`

Returns a copy of node. If options is true or options is a dictionary whose [`selfOnly`](#45-interface-document) is false, the copy also includes the node’s [descendants](#11-trees).

options’s [`customElementRegistry`](#45-interface-document) can be used to set the [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) of elements that have none.

If node is a [document](#45-interface-document) or a [shadow root](#48-interface-shadowroot), throws a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

`node = document . adoptNode(node)`

Moves node from another [document](#45-interface-document) and returns it.

If node is a [document](#45-interface-document), throws a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) or, if node is a [shadow root](#48-interface-shadowroot), throws a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

The `importNode(node, options)` method steps are:
1. If node is a [document](#45-interface-document) or [shadow root](#48-interface-shadowroot), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Let subtree be false.
3. Let registry be null.
4. If options is a boolean, then set subtree to options.
5. Otherwise:
   1. Set subtree to the negation of options\["[`selfOnly`](#45-interface-document)"\].
   2. If options\["[`customElementRegistry`](#45-interface-document)"\] [exists](infra-spec-whatwg-org.md#52-maps), then set registry to it.
   3. If registry’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is false and registry is not [this](https://webidl.spec.whatwg.org/#this)’s [custom element registry](#45-interface-document), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
6. If registry is null, then set registry to the result of [looking up a custom element registry](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) given [this](https://webidl.spec.whatwg.org/#this).
7. Return the result of [cloning a node](#44-interface-node) given node with [*document*](#44-interface-node) set to [this](https://webidl.spec.whatwg.org/#this), [*subtree*](#44-interface-node) set to subtree, and [*fallbackRegistry*](#44-interface-node) set to registry.

[Specifications](#1-infrastructure) may define adopting steps for all or some [nodes](#42-node-tree). The algorithm is passed node and oldDocument, as indicated in the [adopt](#45-interface-document) algorithm.

To adopt a [node](#42-node-tree) node into a [document](#45-interface-document) document:
1. Let oldDocument be node’s [node document](#44-interface-node).
2. If node’s [parent](#11-trees) is non-null, then [remove](#423-mutation-algorithms) node.
3. If document is not oldDocument, then for each inclusiveDescendant of node’s [shadow-including inclusive descendants](#48-interface-shadowroot), in [shadow-including tree order](#48-interface-shadowroot):
   1. Set inclusiveDescendant’s [node document](#44-interface-node) to document.
   2. If inclusiveDescendant is a [shadow root](#48-interface-shadowroot) and if any of the following are true:
      - inclusiveDescendant’s [custom element registry](#48-interface-shadowroot) is null and inclusiveDescendant’s [keep custom element registry null](#48-interface-shadowroot) is false; or
      - inclusiveDescendant’s [custom element registry](#48-interface-shadowroot) [is a global custom element registry](#45-interface-document),

      then set inclusiveDescendant’s [custom element registry](#48-interface-shadowroot) to document’s [custom element registry](#45-interface-document)’s [effective global custom element registry](#45-interface-document).

   3. Otherwise, if inclusiveDescendant is an [element](#49-interface-element):
      1. Set the [node document](#44-interface-node) of each [attribute](#492-interface-attr) in inclusiveDescendant’s [attribute list](#49-interface-element) to document.
      2. If inclusiveDescendant’s [custom element registry](#49-interface-element) is null or inclusiveDescendant’s [custom element registry](#49-interface-element)’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is false:
         1. Let registry be null.
         2. If inclusiveDescendant’s [custom element registry](#49-interface-element) is non-null, inclusiveDescendant’s [parent](#11-trees) is null, or inclusiveDescendant’s [parent](#11-trees) is an [exclusive `DocumentFragment` node](#47-interface-documentfragment), then set registry to document’s [custom element registry](#45-interface-document).
         3. Otherwise, set registry to the result of [looking up a custom element registry](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) given inclusiveDescendant’s [parent](#11-trees).
         4. Set inclusiveDescendant’s [custom element registry](#49-interface-element) to registry’s [effective global custom element registry](#45-interface-document).
      3. If inclusiveDescendant is [custom](#49-interface-element), then [enqueue a custom element callback reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) with inclusiveDescendant, callback name "`adoptedCallback`", and « oldDocument, document ».
   4. Run the [adopting steps](#45-interface-document) with inclusiveDescendant and oldDocument.

The `adoptNode(node)` method steps are:
1. If node is a [document](#45-interface-document), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If node is a [shadow root](#48-interface-shadowroot), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. [Adopt](#45-interface-document) node into [this](https://webidl.spec.whatwg.org/#this).
4. Return node.

---

Null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object registry is a global custom element registry if registry is non-null and registry’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is false.

Null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object registry’s effective global custom element registry is:
1. If registry [is a global custom element registry](#45-interface-document), then return registry.
2. Return null.

---

The `createAttribute(localName)` method steps are:
1. If localName is not a [valid attribute local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If [this](https://webidl.spec.whatwg.org/#this) is an [HTML document](#45-interface-document), then set localName to localName in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
3. Return the result of [creating an attribute](#492-interface-attr) given [this](https://webidl.spec.whatwg.org/#this) and localName.

The `createAttributeNS(namespace, qualifiedName)` method steps are:
1. Let (namespace, prefix, localName) be the result of [validating and extracting](#14-name-validation) namespace and qualifiedName given "`attribute`".
2. Return the result of [creating an attribute](#492-interface-attr) given [this](https://webidl.spec.whatwg.org/#this), localName, namespace, and prefix.

---

The `createEvent(interface)` method steps are:
1. Let constructor be null.
2. If interface is an [ASCII case-insensitive](infra-spec-whatwg-org.md#47-strings) match for any of the strings in the first column in the following table, then set constructor to the interface in the second column on the same row as the matching string:

   | "`beforeunloadevent`" | [`BeforeUnloadEvent`](html-spec-whatwg-org.md#7277-the-beforeunloadevent-interface) | [\[HTML\]](#normative-references) |
   | --- | --- | --- |
   | "`compositionevent`" | [`CompositionEvent`](https://w3c.github.io/uievents/#compositionevent) | [\[UIEVENTS\]](#normative-references) |
   | "`customevent`" | [`CustomEvent`](#24-interface-customevent) |  |
   | "`devicemotionevent`" | [`DeviceMotionEvent`](https://w3c.github.io/deviceorientation/spec-source-orientation.html#devicemotion) | [\[DEVICE-ORIENTATION\]](#normative-references) |
   | "`deviceorientationevent`" | [`DeviceOrientationEvent`](https://w3c.github.io/deviceorientation/spec-source-orientation.html#devicemotion) |
   | "`dragevent`" | [`DragEvent`](html-spec-whatwg-org.md#6114-the-dragevent-interface) | [\[HTML\]](#normative-references) |
   | "`event`" | [`Event`](#22-interface-event) |  |
   | "`events`" |
   | "`focusevent`" | [`FocusEvent`](https://w3c.github.io/uievents/#focusevent) | [\[UIEVENTS\]](#normative-references) |
   | "`hashchangeevent`" | [`HashChangeEvent`](html-spec-whatwg-org.md#7273-the-hashchangeevent-interface) | [\[HTML\]](#normative-references) |
   | "`htmlevents`" | [`Event`](#22-interface-event) |  |
   | "`keyboardevent`" | [`KeyboardEvent`](https://w3c.github.io/uievents/#keyboardevent) | [\[UIEVENTS\]](#normative-references) |
   | "`messageevent`" | [`MessageEvent`](html-spec-whatwg-org.md#91-the-messageevent-interface) | [\[HTML\]](#normative-references) |
   | "`mouseevent`" | [`MouseEvent`](https://w3c.github.io/pointerevents/#dom-mouseevent) | [\[UIEVENTS\]](#normative-references) |
   | "`mouseevents`" |
   | "`storageevent`" | [`StorageEvent`](html-spec-whatwg-org.md#1224-the-storageevent-interface) | [\[HTML\]](#normative-references) |
   | "`svgevents`" | [`Event`](#22-interface-event) |  |
   | "`textevent`" | [`TextEvent`](https://w3c.github.io/uievents/#textevent) | [\[UIEVENTS\]](#normative-references) |
   | "`touchevent`" | [`TouchEvent`](https://w3c.github.io/touch-events/#idl-def-touchevent) | [\[TOUCH-EVENTS\]](#normative-references) |
   | "`uievent`" | [`UIEvent`](https://w3c.github.io/uievents/#uievent) | [\[UIEVENTS\]](#normative-references) |
   | "`uievents`" |

   Notes

3. If constructor is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. If the interface indicated by constructor is not exposed on the [relevant global object](html-spec-whatwg-org.md#81334-relevant) of [this](https://webidl.spec.whatwg.org/#this), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   > [!note]
   > Typically user agents disable support for touch events in some configurations, in which case this clause would be triggered for the interface [`TouchEvent`](https://w3c.github.io/touch-events/#idl-def-touchevent).

5. Let event be the result of [creating an event](#25-constructing-events) given constructor.
6. Initialize event’s [`type`](#22-interface-event) attribute to the empty string.
7. Initialize event’s [`timeStamp`](#22-interface-event) attribute to the result of calling [current high resolution time](https://w3c.github.io/hr-time/#dfn-current-high-resolution-time) with [this](https://webidl.spec.whatwg.org/#this)’s [relevant global object](html-spec-whatwg-org.md#81334-relevant).
8. Initialize event’s [`isTrusted`](#22-interface-event) attribute to false.
9. Unset event’s [initialized flag](#22-interface-event).
10. Return event.

> [!note]
> [Event](#22-interface-event) constructors ought to be used instead.

---

The `createRange()` method steps are to return a new [live range](#55-interface-range) with ([this](https://webidl.spec.whatwg.org/#this), 0) as its [start](#53-interface-abstractrange) an [end](#53-interface-abstractrange).

> [!note]
> The [`Range()`](#55-interface-range) constructor can be used instead.

---

The `createNodeIterator(root, whatToShow, filter)` method steps are:
1. Let iterator be a new [`NodeIterator`](#61-interface-nodeiterator) object.
2. Set iterator’s [root](#6-traversal) to root.
3. Set iterator’s [reference](#61-interface-nodeiterator) to (root, true).
4. Set iterator’s [whatToShow](#6-traversal) to whatToShow.
5. Set iterator’s [filter](#6-traversal) to filter.
6. Return iterator.

The `createTreeWalker(root, whatToShow, filter)` method steps are:
1. Let walker be a new [`TreeWalker`](#62-interface-treewalker) object.
2. Set walker’s [root](#6-traversal) and walker’s [current](#62-interface-treewalker) to root.
3. Set walker’s [whatToShow](#6-traversal) to whatToShow.
4. Set walker’s [filter](#6-traversal) to filter.
5. Return walker.

#### 4.5.1. Interface [`DOMImplementation`](#451-interface-domimplementation)

User agents must create a [`DOMImplementation`](#451-interface-domimplementation) object whenever a [document](#45-interface-document) is created and associate it with that [document](#45-interface-document).

```webidl
[Exposed=Window]
interface DOMImplementation {
  [NewObject] DocumentType createDocumentType(DOMString name, DOMString publicId, DOMString systemId);
  [NewObject] XMLDocument createDocument(DOMString? namespace, [LegacyNullToEmptyString] DOMString qualifiedName, optional DocumentType? doctype = null);
  [NewObject] Document createHTMLDocument(optional DOMString title);

  boolean hasFeature(); // historical; always returns true
};

```

`` doctype = document . `implementation` . `createDocumentType(name, publicId, systemId)` ``

Returns a [doctype](#46-interface-documenttype), with the given name, publicId, and systemId.

If name is not a [valid doctype name](#14-name-validation), an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) is thrown.

`` doc = document . `implementation` . createDocument(namespace, qualifiedName [, doctype = null]) ``

Returns an [`XMLDocument`](#45-interface-document), with a [document element](#421-document-tree) whose [local name](#49-interface-element) is qualifiedName and whose [namespace](#49-interface-element) is namespace (unless qualifiedName is the empty string), and with doctype, if it is given, as its [doctype](#46-interface-documenttype).

This method throws the same exceptions as the [`createElementNS()`](#45-interface-document) method, when invoked with namespace and qualifiedName.

`` doc = document . `implementation` . createHTMLDocument([title]) ``

Returns a [document](#45-interface-document), with a basic [tree](#11-trees) already constructed including a [`title`](html-spec-whatwg-org.md#422-the-title-element) element, unless the title argument is omitted.

The `createDocumentType(name, publicId, systemId)` method steps are:
1. If name is not a [valid doctype name](#14-name-validation), then throw an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Return the result of [creating a doctype](#46-interface-documenttype) given the associated [document](#45-interface-document) of [this](https://webidl.spec.whatwg.org/#this), name, publicId, and systemId.

The `createDocument(namespace, qualifiedName, doctype)` method steps are:
1. Let document be the result of [creating a document](#45-interface-document) that implements [`XMLDocument`](#45-interface-document), given [this](https://webidl.spec.whatwg.org/#this)’s [relevant realm](html-spec-whatwg-org.md#81334-relevant).
2. Let element be null.
3. If qualifiedName is not the empty string, then set element to the result of running the [internal `createElementNS` steps](#45-interface-document), given document, namespace, qualifiedName, and an empty dictionary.
4. If doctype is non-null, [append](#423-mutation-algorithms) doctype to document.
5. If element is non-null, [append](#423-mutation-algorithms) element to document.
6. document’s [origin](#45-interface-document) is [this](https://webidl.spec.whatwg.org/#this)’s associated [document](#45-interface-document)’s [origin](#45-interface-document).
7. document’s [content type](#45-interface-document) is determined by namespace:

   [HTML namespace](infra-spec-whatwg-org.md#8-namespaces)

   `application/xhtml+xml`

   [SVG namespace](infra-spec-whatwg-org.md#8-namespaces)

   `image/svg+xml`

   Any other namespace

   `application/xml`

8. Return document.

The `createHTMLDocument(title)` method steps are:
1. Let doc be the result of [creating a document](#45-interface-document) that implements [`Document`](#45-interface-document), given [this](https://webidl.spec.whatwg.org/#this)’s [relevant realm](html-spec-whatwg-org.md#81334-relevant).
2. Set doc’s [type](#45-interface-document) to "`html`" and [content type](#45-interface-document) to "`text/html`".
3. Let doctype be the result of [creating a doctype](#46-interface-documenttype) given doc and "`html`".
4. [Append](#423-mutation-algorithms) doctype to doc.
5. [Append](#423-mutation-algorithms) the result of [creating an element](#49-interface-element) given doc, "`html`", and the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), to doc.
6. [Append](#423-mutation-algorithms) the result of [creating an element](#49-interface-element) given doc, "`head`", and the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), to the [`html`](html-spec-whatwg-org.md#411-the-html-element) element created earlier.
7. If title is given:
   1. [Append](#423-mutation-algorithms) the result of [creating an element](#49-interface-element) given doc, "`title`", and the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), to the [`head`](html-spec-whatwg-org.md#421-the-head-element) element created earlier.
   2. Let text be the result of [creating a text node](#411-interface-text) given doc and title (which could be the empty string).
   3. [Append](#423-mutation-algorithms) text to the [`title`](html-spec-whatwg-org.md#422-the-title-element) element created earlier.
8. [Append](#423-mutation-algorithms) the result of [creating an element](#49-interface-element) given doc, "`body`", and the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), to the [`html`](html-spec-whatwg-org.md#411-the-html-element) element created earlier.
9. doc’s [origin](#45-interface-document) is [this](https://webidl.spec.whatwg.org/#this)’s associated [document](#45-interface-document)’s [origin](#45-interface-document).
10. Return doc.

The `hasFeature()` method steps are to return true.

> [!note]
> [`hasFeature()`](#451-interface-domimplementation) originally would report whether the user agent claimed to support a given DOM feature, but experience proved it was not nearly as reliable or granular as simply checking whether the desired objects, attributes, or methods existed. As such, it is no longer to be used, but continues to exist (and simply returns true) so that old pages don’t stop working.

### 4.6. Interface [`DocumentType`](#46-interface-documenttype)

```webidl
[Exposed=Window]
interface DocumentType : Node {
  readonly attribute DOMString name;
  readonly attribute DOMString publicId;
  readonly attribute DOMString systemId;
};

```

[`DocumentType`](#46-interface-documenttype) [nodes](#42-node-tree) are simply known as doctypes.

[Doctypes](#46-interface-documenttype) have an associated name (a string), public ID (a string), and system ID (a string).

To create a doctype given a [document](#45-interface-document) document, a string name, and optionally a string publicId (default the empty string) and a string systemId (default the empty string):
1. Let doctype be the result of [creating a node](#44-interface-node) that implements [`DocumentType`](#46-interface-documenttype), given document.
2. Set doctype’s [name](#46-interface-documenttype) to name, [public ID](#46-interface-documenttype) to publicId, and [system ID](#46-interface-documenttype) to systemId.
3. Return doctype.

The `name` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [name](#46-interface-documenttype).

The `publicId` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [public ID](#46-interface-documenttype).

The `systemId` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [system ID](#46-interface-documenttype).

### 4.7. Interface [`DocumentFragment`](#47-interface-documentfragment)

```webidl
[Exposed=Window]
interface DocumentFragment : Node {
  constructor();
};

```

`` tree = new `DocumentFragment()` ``

Returns a new [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree).

---

An exclusive [`DocumentFragment`](#47-interface-documentfragment) node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree) that is not a [`ShadowRoot`](#48-interface-shadowroot) [node](#42-node-tree).

A [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree) has an associated host (null or an [element](#49-interface-element) in a different [node tree](#42-node-tree)). It is null unless otherwise stated.

An object A is a host-including inclusive ancestor of an object B, if either A is an [inclusive ancestor](#11-trees) of B, or if B’s [root](#11-trees) has a non-null [host](#47-interface-documentfragment) and A is a [host-including inclusive ancestor](#47-interface-documentfragment) of B’s [root](#11-trees)’s [host](#47-interface-documentfragment).

> [!note]
> The [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree)’s [host](#47-interface-documentfragment) concept is useful for HTML’s [`template`](html-spec-whatwg-org.md#4123-the-template-element) element and for [shadow roots](#48-interface-shadowroot), and impacts the [pre-insert](#423-mutation-algorithms) and [replace](#423-mutation-algorithms) algorithms.

To create a document fragment given a [document](#45-interface-document) document: return the result of [creating a node](#44-interface-node) that implements [`DocumentFragment`](#47-interface-documentfragment), given document.

The `new DocumentFragment()` constructor steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node) to [current global object](html-spec-whatwg-org.md#81333-current)’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object).

### 4.8. Interface [`ShadowRoot`](#48-interface-shadowroot)

```webidl
[Exposed=Window]
interface ShadowRoot : DocumentFragment {
  readonly attribute ShadowRootMode mode;
  readonly attribute boolean delegatesFocus;
  readonly attribute boolean serializable;
  readonly attribute SlotAssignmentMode slotAssignment;
  readonly attribute boolean clonable;
  readonly attribute Element host;

  attribute EventHandler onslotchange;
};

enum ShadowRootMode { "open", "closed" };
enum SlotAssignmentMode { "manual", "named" };

```

[`ShadowRoot`](#48-interface-shadowroot) [nodes](#42-node-tree) are simply known as shadow roots.

[Shadow roots](#48-interface-shadowroot)’s associated [host](#47-interface-documentfragment) is never null.

[Shadow roots](#48-interface-shadowroot) have an associated mode ("`open`" or "`closed`").

[Shadow roots](#48-interface-shadowroot) have an associated delegates focus (a boolean). It is initially set to false.

[Shadow roots](#48-interface-shadowroot) have an associated available to element internals (a boolean). It is initially set to false.

[Shadow roots](#48-interface-shadowroot) have an associated declarative (a boolean). It is initially set to false.

[Shadow roots](#48-interface-shadowroot) have an associated serializable (a boolean). It is initially set to false.

[Shadow roots](#48-interface-shadowroot) have an associated slot assignment ("`manual`" or "`named`").

[Shadow roots](#48-interface-shadowroot) have an associated clonable (a boolean). It is initially set to false.

[Shadow roots](#48-interface-shadowroot) have an associated custom element registry (null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object). It is initially null.

[Shadow roots](#48-interface-shadowroot) have an associated keep custom element registry null (a boolean). It is initially false.

> [!note]
> This can only ever be true in combination with declarative shadow roots. And it only matters for as long as the [shadow root](#48-interface-shadowroot)’s [custom element registry](#48-interface-shadowroot) is null.

---

A [shadow root](#48-interface-shadowroot)’s [get the parent](#27-interface-eventtarget) algorithm, given an event, returns null if event’s [composed flag](#22-interface-event) is unset and [shadow root](#48-interface-shadowroot) is the [root](#11-trees) of event’s [path](#22-interface-event)’s first [event path item](#22-interface-event)’s [invocation target](#22-interface-event); otherwise [shadow root](#48-interface-shadowroot)’s [host](#47-interface-documentfragment).

---

The `mode` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [mode](#48-interface-shadowroot).

The `delegatesFocus` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [delegates focus](#48-interface-shadowroot).

The `serializable` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [serializable](#48-interface-shadowroot).

The `slotAssignment` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [slot assignment](#48-interface-shadowroot).

The `clonable` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [clonable](#48-interface-shadowroot).

The `host` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [host](#47-interface-documentfragment).

---

The `onslotchange` attribute is an [event handler IDL attribute](html-spec-whatwg-org.md#8181-event-handlers) for the `onslotchange` [event handler](html-spec-whatwg-org.md#8181-event-handlers), whose [event handler event type](html-spec-whatwg-org.md#8181-event-handlers) is [`slotchange`](#43-mutation-observers).

---

In shadow-including tree order is [shadow-including preorder, depth-first traversal](#48-interface-shadowroot) of a [node tree](#42-node-tree). Shadow-including preorder, depth-first traversal of a [node tree](#42-node-tree) tree is preorder, depth-first traversal of tree, with for each [shadow host](#49-interface-element) encountered in tree, [shadow-including preorder, depth-first traversal](#48-interface-shadowroot) of that [element](#49-interface-element)’s [shadow root](#49-interface-element)’s [node tree](#42-node-tree) just after it is encountered.

The shadow-including root of an object is its [root](#11-trees)’s [host](#47-interface-documentfragment)’s [shadow-including root](#48-interface-shadowroot), if the object’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot); otherwise its [root](#11-trees).

An object A is a shadow-including descendant of an object B, if A is a [descendant](#11-trees) of B, or A’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot) and A’s [root](#11-trees)’s [host](#47-interface-documentfragment) is a [shadow-including inclusive descendant](#48-interface-shadowroot) of B.

A shadow-including inclusive descendant is an object or one of its [shadow-including descendants](#48-interface-shadowroot).

An object A is a shadow-including ancestor of an object B, if and only if B is a [shadow-including descendant](#48-interface-shadowroot) of A.

A shadow-including inclusive ancestor is an object or one of its [shadow-including ancestors](#48-interface-shadowroot).

A [node](#42-node-tree) A is closed-shadow-hidden from a [node](#42-node-tree) B if all of the following conditions are true:
- A’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot).
- A’s [root](#11-trees) is not a [shadow-including inclusive ancestor](#48-interface-shadowroot) of B.
- A’s [root](#11-trees) is a [shadow root](#48-interface-shadowroot) whose [mode](#48-interface-shadowroot) is "`closed`" or A’s [root](#11-trees)’s [host](#47-interface-documentfragment) is [closed-shadow-hidden](#48-interface-shadowroot) from B.

To retarget an object A against an object B, repeat these steps until they return an object:
1. If one of the following is true
   - A is not a [node](#42-node-tree)
   - A’s [root](#11-trees) is not a [shadow root](#48-interface-shadowroot)
   - B is a [node](#42-node-tree) and A’s [root](#11-trees) is a [shadow-including inclusive ancestor](#48-interface-shadowroot) of B

   then return A.

2. Set A to A’s [root](#11-trees)’s [host](#47-interface-documentfragment).

> [!note]
> The [retargeting](#48-interface-shadowroot) algorithm is used by [event dispatch](#29-dispatching-events) as well as other specifications, such as Fullscreen. [\[FULLSCREEN\]](#non-normative-references)

### 4.9. Interface [`Element`](#49-interface-element)

```webidl
[Exposed=Window]
interface Element : Node {
  readonly attribute DOMString? namespaceURI;
  readonly attribute DOMString? prefix;
  readonly attribute DOMString localName;
  readonly attribute DOMString tagName;

  [CEReactions] attribute DOMString id;
  [CEReactions] attribute DOMString className;
  [SameObject, PutForwards=value] readonly attribute DOMTokenList classList;
  [CEReactions, Unscopable] attribute DOMString slot;

  boolean hasAttributes();
  [SameObject] readonly attribute NamedNodeMap attributes;
  sequence<DOMString> getAttributeNames();
  DOMString? getAttribute(DOMString qualifiedName);
  DOMString? getAttributeNS(DOMString? namespace, DOMString localName);
  [CEReactions] undefined setAttribute(DOMString qualifiedName, (TrustedType or DOMString) value);
  [CEReactions] undefined setAttributeNS(DOMString? namespace, DOMString qualifiedName, (TrustedType or DOMString) value);
  [CEReactions] undefined removeAttribute(DOMString qualifiedName);
  [CEReactions] undefined removeAttributeNS(DOMString? namespace, DOMString localName);
  [CEReactions] boolean toggleAttribute(DOMString qualifiedName, optional boolean force);
  boolean hasAttribute(DOMString qualifiedName);
  boolean hasAttributeNS(DOMString? namespace, DOMString localName);

  Attr? getAttributeNode(DOMString qualifiedName);
  Attr? getAttributeNodeNS(DOMString? namespace, DOMString localName);
  [CEReactions] Attr? setAttributeNode(Attr attr);
  [CEReactions] Attr? setAttributeNodeNS(Attr attr);
  [CEReactions] Attr removeAttributeNode(Attr attr);

  ShadowRoot attachShadow(ShadowRootInit init);
  readonly attribute ShadowRoot? shadowRoot;

  readonly attribute CustomElementRegistry? customElementRegistry;

  Element? closest(DOMString selectors);
  boolean matches(DOMString selectors);
  boolean webkitMatchesSelector(DOMString selectors); // legacy alias of .matches

  HTMLCollection getElementsByTagName(DOMString qualifiedName);
  HTMLCollection getElementsByTagNameNS(DOMString? namespace, DOMString localName);
  HTMLCollection getElementsByClassName(DOMString classNames);

  [CEReactions] Element? insertAdjacentElement(DOMString where, Element element); // legacy
  undefined insertAdjacentText(DOMString where, DOMString data); // legacy
};

dictionary ShadowRootInit {
  required ShadowRootMode mode;
  boolean delegatesFocus = false;
  boolean serializable = false;
  SlotAssignmentMode slotAssignment = "named";
  boolean clonable = false;
  CustomElementRegistry? customElementRegistry;
};

```

> [!note]
> [`ShadowRootInit`](#49-interface-element) somewhat unusually allows both `undefined` and `null` to be passed to its [`customElementRegistry`](#49-interface-element) member to allow web developers to pass a [`ShadowRoot`](#48-interface-shadowroot) node instead of a dictionary to [`attachShadow()`](#49-interface-element).

[`Element`](#49-interface-element) [nodes](#42-node-tree) are simply known as elements.

[Elements](#49-interface-element) have an associated:

namespace

Null or a non-empty string.

namespace prefix

Null or a non-empty string.

local name

A non-empty string.

custom element registry

Null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object.

custom element state

"`undefined`", "`failed`", "`uncustomized`", "`precustomized`", or "`custom`".

custom element definition

Null or a [custom element definition](html-spec-whatwg-org.md#4133-core-concepts).

`is` value

Null or a [valid custom element name](html-spec-whatwg-org.md#4133-core-concepts).

When an [element](#49-interface-element) is [created](#49-interface-element), all of these values are initialized.

An [element](#49-interface-element) whose [custom element state](#49-interface-element) is "`uncustomized`" or "`custom`" is said to be defined. An [element](#49-interface-element) whose [custom element state](#49-interface-element) is "`custom`" is said to be custom.

> [!note]
> Whether or not an element is [defined](#49-interface-element) is used to determine the behavior of the [:defined](https://drafts.csswg.org/selectors-4/#defined-pseudo) pseudo-class. Whether or not an element is [custom](#49-interface-element) is used to determine the behavior of the [mutation algorithms](#423-mutation-algorithms). The "`failed`" and "`precustomized`" states are used to ensure that if a [custom element constructor](html-spec-whatwg-org.md#4133-core-concepts) fails to execute correctly the first time, it is not executed again by an [upgrade](html-spec-whatwg-org.md#4135-upgrades).

> [!example]
> The following code illustrates elements in each of these four states:
> 
> ```html
> <!DOCTYPE html>
> <script>
>   window.customElements.define("sw-rey", class extends HTMLElement {})
>   window.customElements.define("sw-finn", class extends HTMLElement {}, { extends: "p" })
>   window.customElements.define("sw-kylo", class extends HTMLElement {
>     constructor() {
>       // super() intentionally omitted for this example
>     }
>   })
> </script>
> 
> <!-- "undefined" (not defined, not custom) -->
> <sw-han></sw-han>
> <p is="sw-luke"></p>
> <p is="asdf"></p>
> 
> <!-- "failed" (not defined, not custom) -->
> <sw-kylo></sw-kylo>
> 
> <!-- "uncustomized" (defined, not custom) -->
> <p></p>
> <asdf></asdf>
> 
> <!-- "custom" (defined, custom) -->
> <sw-rey></sw-rey>
> <p is="sw-finn"></p>
> 
> ```

[Elements](#49-interface-element) also have an associated shadow root (null or a [shadow root](#48-interface-shadowroot)). It is null unless otherwise stated. An [element](#49-interface-element) is a shadow host if its [shadow root](#49-interface-element) is non-null.

An [element](#49-interface-element)’s qualified name is its [local name](#49-interface-element) if its [namespace prefix](#49-interface-element) is null; otherwise its [namespace prefix](#49-interface-element), followed by "`:`", followed by its [local name](#49-interface-element).

An [element](#49-interface-element)’s HTML-uppercased qualified name is the return value of these steps:
1. Let qualifiedName be [this](https://webidl.spec.whatwg.org/#this)’s [qualified name](#49-interface-element).
2. If [this](https://webidl.spec.whatwg.org/#this) is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and its [node document](#44-interface-node) is an [HTML document](#45-interface-document), then return qualifiedName in [ASCII uppercase](infra-spec-whatwg-org.md#47-strings).
3. Return qualifiedName.

> [!note]
> User agents could optimize [qualified name](#49-interface-element) and [HTML-uppercased qualified name](#49-interface-element) by storing them in internal slots.

To create an element, given a [document](#45-interface-document) document, string localName, string-or-null namespace, and optionally a string-or-null prefix (default null), string-or-null is (default null), boolean synchronousCustomElements (default false), and "`default`", null, or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object registry (default "`default`"):
1. Let result be null.
2. If registry is "`default`", then set registry to the result of [looking up a custom element registry](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) given document.
3. Let definition be the result of [looking up a custom element definition](html-spec-whatwg-org.md#4133-core-concepts) given registry, namespace, localName, and is.
4. If definition is non-null, and definition’s [name](html-spec-whatwg-org.md#4133-core-concepts) is not equal to its [local name](html-spec-whatwg-org.md#4133-core-concepts) (i.e., definition represents a [customized built-in element](html-spec-whatwg-org.md#4133-core-concepts)):
   1. Let interface be the [element interface](#45-interface-document) for localName and the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces).
   2. Set result to the result of [creating an element internal](#49-interface-element) given document, interface, localName, the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), prefix, "`undefined`", is, and registry.
   3. If synchronousCustomElements is true, then run this step while catching any exceptions:
      1. [Upgrade](html-spec-whatwg-org.md#4135-upgrades) result using definition.

      If this step threw an exception exception:
      1. [Report](html-spec-whatwg-org.md#8146-runtime-script-errors) exception for definition’s [constructor](html-spec-whatwg-org.md#4133-core-concepts)’s corresponding JavaScript object’s [associated realm](https://webidl.spec.whatwg.org/#dfn-associated-realm)’s [global object](html-spec-whatwg-org.md#8133-realms-settings-objects-and-global-objects).
      2. Set result’s [custom element state](#49-interface-element) to "`failed`".

   4. Otherwise, [enqueue a custom element upgrade reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) given result and definition.

5. Otherwise, if definition is non-null:
   1. If synchronousCustomElements is true:
      1. Let C be definition’s [constructor](html-spec-whatwg-org.md#4133-core-concepts).
      2. Let previousRegistry be the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [active custom element constructor map](html-spec-whatwg-org.md#4134-the-customelementregistry-interface)\[C\] [with default](infra-spec-whatwg-org.md#52-maps) null.
      3. [Set](infra-spec-whatwg-org.md#52-maps) the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [active custom element constructor map](html-spec-whatwg-org.md#4134-the-customelementregistry-interface)\[C\] to registry.
      4. Run these steps while catching any exceptions:
         1. Set result to the result of [constructing](https://webidl.spec.whatwg.org/#construct-a-callback-function) C, with no arguments.
         2. [Assert](infra-spec-whatwg-org.md#310-assertions): one of the following is true:
            - result’s [custom element state](#49-interface-element) is "`custom`" and its [custom element definition](#49-interface-element) is non-null;
            - result’s [custom element state](#49-interface-element) is "`precustomized`"; or
            - result’s [custom element state](#49-interface-element) is neither "`custom`" nor "`precustomized`" and its [custom element definition](#49-interface-element) is null.

            > [!example]
            > ```javascript
            > customElements.define("x-example", class extends HTMLElement {
            >   constructor() {
            >     // Non-conformant: returns an existing element instead of calling super().
            >     return document.createElement("p");
            >   }
            > });
            > 
            > document.createElement("x-example");
            > 
            > ```
            > 
            > Here result is the `p` [element](#49-interface-element), whose [custom element state](#49-interface-element) is "`uncustomized`" and whose [custom element definition](#49-interface-element) is null.

         3. Assert: result’s [namespace](#49-interface-element) is the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces).

            > [!note]
            > IDL enforces that result is an [`HTMLElement`](html-spec-whatwg-org.md#322-elements-in-the-dom) object, which all use the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces).

         4. If result’s [attribute list](#49-interface-element) [is not empty](infra-spec-whatwg-org.md#51-lists), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
         5. If result has [children](#11-trees), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
         6. If result’s [parent](#11-trees) is non-null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
         7. If result’s [node document](#44-interface-node) is not document, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
         8. If result’s [local name](#49-interface-element) is not equal to localName, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
         9. Set result’s [namespace prefix](#49-interface-element) to prefix.
         10. Set result’s [`is` value](#49-interface-element) to null.
         11. Set result’s [custom element registry](#49-interface-element) to registry.

         If any of these steps threw an exception exception:
         1. [Report](html-spec-whatwg-org.md#8146-runtime-script-errors) exception for definition’s [constructor](html-spec-whatwg-org.md#4133-core-concepts)’s corresponding JavaScript object’s [associated realm](https://webidl.spec.whatwg.org/#dfn-associated-realm)’s [global object](html-spec-whatwg-org.md#8133-realms-settings-objects-and-global-objects).
         2. Set result to the result of [creating an element internal](#49-interface-element) given document, [`HTMLUnknownElement`](html-spec-whatwg-org.md#322-elements-in-the-dom), localName, the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), prefix, "`failed`", null, and registry.

      5. If previousRegistry is null, then [remove](infra-spec-whatwg-org.md#52-maps) the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [active custom element constructor map](html-spec-whatwg-org.md#4134-the-customelementregistry-interface)\[C\].
      6. Otherwise, [set](infra-spec-whatwg-org.md#52-maps) the [surrounding agent](https://tc39.es/ecma262/#surrounding-agent)’s [active custom element constructor map](html-spec-whatwg-org.md#4134-the-customelementregistry-interface)\[C\] to previousRegistry.

   2. Otherwise:
      1. Set result to the result of [creating an element internal](#49-interface-element) given document, [`HTMLElement`](html-spec-whatwg-org.md#322-elements-in-the-dom), localName, the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), prefix, "`undefined`", null, and registry.
      2. [Enqueue a custom element upgrade reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) given result and definition.

6. Otherwise:
   1. Let interface be the [element interface](#45-interface-document) for localName and namespace.
   2. Set result to the result of [creating an element internal](#49-interface-element) given document, interface, localName, namespace, prefix, "`uncustomized`", is, and registry.
   3. If namespace is the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), and either localName is a [valid custom element name](html-spec-whatwg-org.md#4133-core-concepts) or is is non-null, then set result’s [custom element state](#49-interface-element) to "`undefined`".
7. Return result.

To create an element internal given a [document](#45-interface-document) document, an interface interface a string localName, a string-or-null namespace, a string-or-null prefix, a string state, a string-or-null is, and null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object registry:
1. Let element be the result of [creating a node](#44-interface-node) that implements interface, given document.
2. Set element’s [namespace](#49-interface-element) to namespace, [namespace prefix](#49-interface-element) to prefix, [local name](#49-interface-element) to localName, [custom element registry](#49-interface-element) to registry, [custom element state](#49-interface-element) to state, [custom element definition](#49-interface-element) to null, and [`is` value](#49-interface-element) to is.
3. [Assert](infra-spec-whatwg-org.md#310-assertions): element’s [attribute list](#49-interface-element) [is empty](infra-spec-whatwg-org.md#51-lists).
4. Return element.

[Elements](#49-interface-element) also have an attribute list, which is a [list](infra-spec-whatwg-org.md#51-lists) exposed through a [`NamedNodeMap`](#491-interface-namednodemap). Unless explicitly given when an [element](#49-interface-element) is created, its [attribute list](#49-interface-element) [is empty](infra-spec-whatwg-org.md#51-lists).

An [element](#49-interface-element) has an [attribute](#492-interface-attr) A if its [attribute list](#49-interface-element) [contains](infra-spec-whatwg-org.md#51-lists) A.

This and [other specifications](#1-infrastructure) may define attribute change steps for [elements](#49-interface-element). The algorithm is passed element, localName, oldValue, value, and namespace.

To handle attribute changes for an [attribute](#492-interface-attr) attribute with element, oldValue, and newValue, run these steps:
1. [Queue a mutation record](#432-queuing-a-mutation-record) of "`attributes`" for element with attribute’s [local name](#492-interface-attr), attribute’s [namespace](#492-interface-attr), oldValue, « », « », null, and null.
2. If element is [custom](#49-interface-element), then [enqueue a custom element callback reaction](html-spec-whatwg-org.md#4136-custom-element-reactions) with element, callback name "`attributeChangedCallback`", and « attribute’s [local name](#492-interface-attr), oldValue, newValue, attribute’s [namespace](#492-interface-attr) ».
3. Run the [attribute change steps](#49-interface-element) with element, attribute’s [local name](#492-interface-attr), oldValue, newValue, and attribute’s [namespace](#492-interface-attr).

To change an [attribute](#492-interface-attr) attribute to value:
1. Let oldValue be attribute’s [value](#492-interface-attr).
2. Set attribute’s [value](#492-interface-attr) to value.
3. [Handle attribute changes](#49-interface-element) for attribute with attribute’s [element](#492-interface-attr), oldValue, and value.

To append an [attribute](#492-interface-attr) attribute to an [element](#49-interface-element) element:
1. [Append](infra-spec-whatwg-org.md#51-lists) attribute to element’s [attribute list](#49-interface-element).
2. Set attribute’s [element](#492-interface-attr) to element.
3. Set attribute’s [node document](#44-interface-node) to element’s [node document](#44-interface-node).
4. [Handle attribute changes](#49-interface-element) for attribute with element, null, and attribute’s [value](#492-interface-attr).

To remove an [attribute](#492-interface-attr) attribute:
1. Let element be attribute’s [element](#492-interface-attr).
2. [Remove](infra-spec-whatwg-org.md#51-lists) attribute from element’s [attribute list](#49-interface-element).
3. Set attribute’s [element](#492-interface-attr) to null.
4. [Handle attribute changes](#49-interface-element) for attribute with element, attribute’s [value](#492-interface-attr), and null.

To replace an [attribute](#492-interface-attr) oldAttribute with an [attribute](#492-interface-attr) newAttribute:
1. Let element be oldAttribute’s [element](#492-interface-attr).
2. [Replace](infra-spec-whatwg-org.md#51-lists) oldAttribute by newAttribute in element’s [attribute list](#49-interface-element).
3. Set newAttribute’s [element](#492-interface-attr) to element.
4. Set newAttribute’s [node document](#44-interface-node) to element’s [node document](#44-interface-node).
5. Set oldAttribute’s [element](#492-interface-attr) to null.
6. [Handle attribute changes](#49-interface-element) for oldAttribute with element, oldAttribute’s [value](#492-interface-attr), and newAttribute’s [value](#492-interface-attr).

---

To get an attribute by name given a string qualifiedName and an [element](#49-interface-element) element:
1. If element is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and its [node document](#44-interface-node) is an [HTML document](#45-interface-document), then set qualifiedName to qualifiedName in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
2. Return the first [attribute](#492-interface-attr) in element’s [attribute list](#49-interface-element) whose [qualified name](#492-interface-attr) is qualifiedName; otherwise null.

To get an attribute by namespace and local name given null or a string namespace, a string localName, and an [element](#49-interface-element) element:
1. If namespace is the empty string, then set it to null.
2. Return the [attribute](#492-interface-attr) in element’s [attribute list](#49-interface-element) whose [namespace](#492-interface-attr) is namespace and [local name](#492-interface-attr) is localName, if any; otherwise null.

To get an attribute value given an [element](#49-interface-element) element, a string localName, and an optional null or string namespace (default null):
1. Let attr be the result of [getting an attribute](#49-interface-element) given namespace, localName, and element.
2. If attr is null, then return the empty string.
3. Return attr’s [value](#492-interface-attr).

To set an attribute given an [attribute](#492-interface-attr) attr and an [element](#49-interface-element) element:
1. Let verifiedValue be the result of calling [get trusted type compliant attribute value](https://w3c.github.io/trusted-types/dist/spec/#get-trusted-type-compliant-attribute-value) with attr’s [local name](#492-interface-attr), attr’s [namespace](#492-interface-attr), element, and attr’s [value](#492-interface-attr). [\[TRUSTED-TYPES\]](#normative-references)
2. If attr’s [element](#492-interface-attr) is neither null nor element, [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InUseAttributeError`](https://webidl.spec.whatwg.org/#inuseattributeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let oldAttr be the result of [getting an attribute](#49-interface-element) given attr’s [namespace](#492-interface-attr), attr’s [local name](#492-interface-attr), and element.
4. If oldAttr is attr, return attr.
5. Set attr’s [value](#492-interface-attr) to verifiedValue.
6. If oldAttr is non-null, then [replace](#49-interface-element) oldAttr with attr.
7. Otherwise, [append](#49-interface-element) attr to element.
8. Return oldAttr.

To set an attribute value given an [element](#49-interface-element) element, a string localName, a string value, an optional null or string prefix (default null), and an optional null or string namespace (default null):
1. Let attribute be the result of [getting an attribute](#49-interface-element) given namespace, localName, and element.
2. If attribute is null, then [append](#49-interface-element) the result of [creating an attribute](#492-interface-attr) given element’s [node document](#44-interface-node), localName, namespace, prefix, and value to element, and then return.
3. [Change](#49-interface-element) attribute to value.

To remove an attribute by name given a string qualifiedName and an [element](#49-interface-element) element:
1. Let attr be the result of [getting an attribute](#49-interface-element) given qualifiedName and element.
2. If attr is non-null, then [remove](#49-interface-element) attr.
3. Return attr.

To remove an attribute by namespace and local name given null or a string namespace, a string localName, and an [element](#49-interface-element) element:
1. Let attr be the result of [getting an attribute](#49-interface-element) given namespace, localName, and element.
2. If attr is non-null, then [remove](#49-interface-element) attr.
3. Return attr.

---

An [element](#49-interface-element) can have an associated unique identifier (ID)

> [!note]
> Historically [elements](#49-interface-element) could have multiple identifiers e.g., by using the HTML `id` [attribute](#492-interface-attr) and a DTD. This specification makes [ID](#49-interface-element) a concept of the DOM and allows for only one per [element](#49-interface-element), given by an [`id` attribute](#492-interface-attr).

Use these [attribute change steps](#49-interface-element) to update an [element](#49-interface-element)’s [ID](#49-interface-element):
1. If localName is `id`, namespace is null, and value is null or the empty string, then unset element’s [ID](#49-interface-element).
2. Otherwise, if localName is `id`, namespace is null, then set element’s [ID](#49-interface-element) to value.

> [!note]
> While this specification defines requirements for `class`, `id`, and `slot` [attributes](#492-interface-attr) on any [element](#49-interface-element), it makes no claims as to whether using them is conforming or not.

---

A [node](#42-node-tree)’s [parent](#11-trees) of type [`Element`](#49-interface-element) is known as its parent element. If the [node](#42-node-tree) has a [parent](#11-trees) of a different type, its [parent element](#49-interface-element) is null.

---

namespace = element . [`namespaceURI`](#49-interface-element)

Returns the [namespace](#49-interface-element).

prefix = element . [`prefix`](#49-interface-element)

Returns the [namespace prefix](#49-interface-element).

localName = element . [`localName`](#49-interface-element)

Returns the [local name](#49-interface-element).

qualifiedName = element . [`tagName`](#49-interface-element)

Returns the [HTML-uppercased qualified name](#49-interface-element).

The `namespaceURI` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [namespace](#49-interface-element).

The `prefix` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [namespace prefix](#49-interface-element).

The `localName` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [local name](#49-interface-element).

The `tagName` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [HTML-uppercased qualified name](#49-interface-element).

---

`element . id [ = value ]`

Returns the value of element’s `id` content attribute. Can be set to change it.

`element . className [ = value ]`

Returns the value of element’s `class` content attribute. Can be set to change it.

`element . classList`

Allows for manipulation of element’s `class` content attribute as a set of whitespace-separated tokens through a [`DOMTokenList`](#71-interface-domtokenlist) object.

`element . slot [ = value ]`

Returns the value of element’s `slot` content attribute. Can be set to change it.

IDL attributes that are defined to reflect a string name, must have these getter and setter steps:

getter steps

Return the result of running [get an attribute value](#49-interface-element) given [this](https://webidl.spec.whatwg.org/#this) and name.

setter steps

[Set an attribute value](#49-interface-element) for [this](https://webidl.spec.whatwg.org/#this) using name and the given value.

The `id` attribute must [reflect](#49-interface-element) "`id`".

The `className` attribute must [reflect](#49-interface-element) "`class`".

The `classList` getter steps are to return a [`DOMTokenList`](#71-interface-domtokenlist) object whose associated [element](#49-interface-element) is [this](https://webidl.spec.whatwg.org/#this) and whose associated [attribute](#492-interface-attr)’s [local name](#492-interface-attr) is `class`. The [token set](#71-interface-domtokenlist) of this particular [`DOMTokenList`](#71-interface-domtokenlist) object are also known as the [element](#49-interface-element)’s classes.

The `slot` attribute must [reflect](#49-interface-element) "`slot`".

> [!note]
> `id`, `class`, and `slot` are effectively superglobal attributes as they can appear on any element, regardless of that element’s namespace.

---

`element . hasAttributes()`

Returns true if element has attributes; otherwise false.

`element . getAttributeNames()`

Returns the [qualified names](#492-interface-attr) of all element’s [attributes](#492-interface-attr). Can contain duplicates.

`element . getAttribute(qualifiedName)`

Returns element’s first [attribute](#492-interface-attr) whose [qualified name](#492-interface-attr) is qualifiedName, and null if there is no such [attribute](#492-interface-attr) otherwise.

`element . getAttributeNS(namespace, localName)`

Returns element’s [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is namespace and [local name](#492-interface-attr) is localName, and null if there is no such [attribute](#492-interface-attr) otherwise.

`element . setAttribute(qualifiedName, value)`

Sets the [value](#492-interface-attr) of element’s first [attribute](#492-interface-attr) whose [qualified name](#492-interface-attr) is qualifiedName to value.

`element . setAttributeNS(namespace, localName, value)`

Sets the [value](#492-interface-attr) of element’s [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is namespace and [local name](#492-interface-attr) is localName to value.

`element . removeAttribute(qualifiedName)`

Removes element’s first [attribute](#492-interface-attr) whose [qualified name](#492-interface-attr) is qualifiedName.

`element . removeAttributeNS(namespace, localName)`

Removes element’s [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is namespace and [local name](#492-interface-attr) is localName.

`element . toggleAttribute(qualifiedName [, force])`

If force is not given, "toggles" qualifiedName, removing it if it is present and adding it if it is not present. If force is true, adds qualifiedName. If force is false, removes qualifiedName.

Returns true if qualifiedName is now present; otherwise false.

`element . hasAttribute(qualifiedName)`

Returns true if element has an [attribute](#492-interface-attr) whose [qualified name](#492-interface-attr) is qualifiedName; otherwise false.

`element . hasAttributeNS(namespace, localName)`

Returns true if element has an [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is namespace and [local name](#492-interface-attr) is localName.

The `hasAttributes()` method steps are to return false if [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#49-interface-element) [is empty](infra-spec-whatwg-org.md#51-lists); otherwise true.

The `attributes` getter steps are to return the associated [`NamedNodeMap`](#491-interface-namednodemap).

The `getAttributeNames()` method steps are to return the [qualified names](#492-interface-attr) of the [attributes](#492-interface-attr) in [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#49-interface-element), in order; otherwise a new [list](infra-spec-whatwg-org.md#51-lists).

> [!note]
> These are not guaranteed to be unique.

The `getAttribute(qualifiedName)` method steps are:
1. Let attr be the result of [getting an attribute](#49-interface-element) given qualifiedName and [this](https://webidl.spec.whatwg.org/#this).
2. If attr is null, return null.
3. Return attr’s [value](#492-interface-attr).

The `getAttributeNS(namespace, localName)` method steps are:
1. Let attr be the result of [getting an attribute](#49-interface-element) given namespace, localName, and [this](https://webidl.spec.whatwg.org/#this).
2. If attr is null, return null.
3. Return attr’s [value](#492-interface-attr).

The `setAttribute(qualifiedName, value)` method steps are:
1. If qualifiedName is not a [valid attribute local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   > [!note]
   > Despite the parameter naming, qualifiedName is only used as a [qualified name](#492-interface-attr) if an [attribute](#492-interface-attr) already exists with that qualified name. Otherwise, it is used as the [local name](#492-interface-attr) of the new attribute. We only need to validate it for the latter case.

2. If [this](https://webidl.spec.whatwg.org/#this) is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and its [node document](#44-interface-node) is an [HTML document](#45-interface-document), then set qualifiedName to qualifiedName in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
3. Let verifiedValue be the result of calling [get trusted type compliant attribute value](https://w3c.github.io/trusted-types/dist/spec/#get-trusted-type-compliant-attribute-value) with qualifiedName, null, [this](https://webidl.spec.whatwg.org/#this), and value. [\[TRUSTED-TYPES\]](#normative-references)
4. Let attribute be the first [attribute](#492-interface-attr) in [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#49-interface-element) whose [qualified name](#492-interface-attr) is qualifiedName, and null otherwise.
5. If attribute is non-null, then [change](#49-interface-element) attribute to verifiedValue and return.
6. Set attribute to the result of [creating an attribute](#492-interface-attr) given [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node), qualifiedName, null, null, and verifiedValue.
7. [Append](#49-interface-element) attribute to [this](https://webidl.spec.whatwg.org/#this).

The `setAttributeNS(namespace, qualifiedName, value)` method steps are:
1. Let (namespace, prefix, localName) be the result of [validating and extracting](#14-name-validation) namespace and qualifiedName given "`attribute`".
2. Let verifiedValue be the result of calling [get trusted type compliant attribute value](https://w3c.github.io/trusted-types/dist/spec/#get-trusted-type-compliant-attribute-value) with localName, namespace, [this](https://webidl.spec.whatwg.org/#this), and value. [\[TRUSTED-TYPES\]](#normative-references)
3. [Set an attribute value](#49-interface-element) for [this](https://webidl.spec.whatwg.org/#this) using localName, verifiedValue, prefix, and namespace.

The `removeAttribute(qualifiedName)` method steps are to [remove an attribute](#49-interface-element) given qualifiedName and [this](https://webidl.spec.whatwg.org/#this), and then return undefined.

The `removeAttributeNS(namespace, localName)` method steps are to [remove an attribute](#49-interface-element) given namespace, localName, and [this](https://webidl.spec.whatwg.org/#this), and then return undefined.

The `hasAttribute(qualifiedName)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this) is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and its [node document](#44-interface-node) is an [HTML document](#45-interface-document), then set qualifiedName to qualifiedName in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
2. Return true if [this](https://webidl.spec.whatwg.org/#this) [has](#49-interface-element) an [attribute](#492-interface-attr) whose [qualified name](#492-interface-attr) is qualifiedName; otherwise false.

The `toggleAttribute(qualifiedName, force)` method steps are:
1. If qualifiedName is not a [valid attribute local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   > [!note]
   > See [the discussion above](#49-interface-element) about why we validate it as a local name, instead of a qualified name.

2. If [this](https://webidl.spec.whatwg.org/#this) is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and its [node document](#44-interface-node) is an [HTML document](#45-interface-document), then set qualifiedName to qualifiedName in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
3. Let attribute be the first [attribute](#492-interface-attr) in [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#49-interface-element) whose [qualified name](#492-interface-attr) is qualifiedName, and null otherwise.
4. If attribute is null:
   1. If force is not given or is true, then [append](#49-interface-element) the result of [creating an attribute](#492-interface-attr) given [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node) and qualifiedName to [this](https://webidl.spec.whatwg.org/#this), and then return true.
   2. Return false.
5. If force is not given or is false, [remove an attribute](#49-interface-element) given qualifiedName and [this](https://webidl.spec.whatwg.org/#this), and then return false.
6. Return true.

The `hasAttributeNS(namespace, localName)` method steps are:
1. If namespace is the empty string, then set it to null.
2. Return true if [this](https://webidl.spec.whatwg.org/#this) [has](#49-interface-element) an [attribute](#492-interface-attr) whose [namespace](#492-interface-attr) is namespace and [local name](#492-interface-attr) is localName; otherwise false.

---

The `getAttributeNode(qualifiedName)` method steps are to return the result of [getting an attribute](#49-interface-element) given qualifiedName and [this](https://webidl.spec.whatwg.org/#this).

The `getAttributeNodeNS(namespace, localName)` method steps are to return the result of [getting an attribute](#49-interface-element) given namespace, localName, and [this](https://webidl.spec.whatwg.org/#this).

The `setAttributeNode(attr)` and `setAttributeNodeNS(attr)` methods steps are to return the result of [setting an attribute](#49-interface-element) given attr and [this](https://webidl.spec.whatwg.org/#this).

The `removeAttributeNode(attr)` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#49-interface-element) does not [contain](infra-spec-whatwg-org.md#51-lists) attr, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotFoundError`](https://webidl.spec.whatwg.org/#notfounderror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. [Remove](#49-interface-element) attr.
3. Return attr.

---

`` shadow = element . `attachShadow(init)` ``

Creates a [shadow root](#48-interface-shadowroot) for element and returns it.

`` shadow = element . `shadowRoot` ``

Returns element’s [shadow root](#49-interface-element), if any, and if [shadow root](#48-interface-shadowroot)’s [mode](#48-interface-shadowroot) is "`open`"; otherwise null.

A valid shadow host name is:
- a [valid custom element name](html-spec-whatwg-org.md#4133-core-concepts)
- "`article`", "`aside`", "`blockquote`", "`body`", "`div`", "`footer`", "`h1`", "`h2`", "`h3`", "`h4`", "`h5`", "`h6`", "`header`", "`main`", "`nav`", "`p`", "`section`", or "`span`"

> [!note]
> This list is intentionally limited so that built-in elements can gain internal [shadow trees](#422-shadow-tree) over time as needed.

The `attachShadow(init)` method steps are:
1. Let registry be [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node)’s [custom element registry](#45-interface-document).
2. If init\["[`customElementRegistry`](#49-interface-element)"\] [exists](infra-spec-whatwg-org.md#52-maps), then set registry to it.
3. If registry is non-null, registry’s [is scoped](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) is false, and registry is not [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node)’s [custom element registry](#45-interface-document), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. Run [attach a shadow root](#49-interface-element) with [this](https://webidl.spec.whatwg.org/#this), init\["[`mode`](#49-interface-element)"\], init\["[`delegatesFocus`](#49-interface-element)"\], init\["[`serializable`](#49-interface-element)"\], init\["[`slotAssignment`](#49-interface-element)"\], init\["[`clonable`](#49-interface-element)"\], and registry.
5. Return [this](https://webidl.spec.whatwg.org/#this)’s [shadow root](#49-interface-element).

To attach a shadow root, given an [element](#49-interface-element) element, a string mode, a boolean delegatesFocus, a boolean serializable, a string slotAssignment, a boolean clonable, and null or a [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object registry:
1. If element’s [namespace](#49-interface-element) is not the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If element’s [local name](#49-interface-element) is not a [valid shadow host name](#49-interface-element), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If element’s [local name](#49-interface-element) is a [valid custom element name](html-spec-whatwg-org.md#4133-core-concepts), or element’s [`is` value](#49-interface-element) is non-null:
   1. Let definition be the result of [looking up a custom element definition](html-spec-whatwg-org.md#4133-core-concepts) given element’s [custom element registry](#49-interface-element), its [namespace](#49-interface-element), its [local name](#49-interface-element), and its [`is` value](#49-interface-element).
   2. If definition is non-null and definition’s [disable shadow](html-spec-whatwg-org.md#4133-core-concepts) is true, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. If element is a [shadow host](#49-interface-element):
   1. Let currentShadowRoot be element’s [shadow root](#49-interface-element).
   2. If any of the following are true:
      - currentShadowRoot’s [declarative](#48-interface-shadowroot) is false; or
      - currentShadowRoot’s [mode](#48-interface-shadowroot) is not mode,

      then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   3. [Remove](#423-mutation-algorithms) all of currentShadowRoot’s [children](#11-trees), in [tree order](#11-trees).
   4. Set currentShadowRoot’s [declarative](#48-interface-shadowroot) to false.
   5. Return.

5. Let shadow be the result of [creating a node](#44-interface-node) that implements [`ShadowRoot`](#48-interface-shadowroot), given element’s [node document](#44-interface-node).
6. Set shadow’s [host](#47-interface-documentfragment) to element.
7. Set shadow’s [mode](#48-interface-shadowroot) to mode.
8. Set shadow’s [delegates focus](#48-interface-shadowroot) to delegatesFocus.
9. If element’s [custom element state](#49-interface-element) is "`precustomized`" or "`custom`", then set shadow’s [available to element internals](#48-interface-shadowroot) to true.
10. Set shadow’s [declarative](#48-interface-shadowroot) to false.
11. Set shadow’s [serializable](#48-interface-shadowroot) to serializable.
12. Set shadow’s [slot assignment](#48-interface-shadowroot) to slotAssignment.
13. Set shadow’s [clonable](#48-interface-shadowroot) to clonable.
14. Set shadow’s [custom element registry](#48-interface-shadowroot) to registry.
15. Set element’s [shadow root](#49-interface-element) to shadow.

The `shadowRoot` getter steps are:
1. Let shadow be [this](https://webidl.spec.whatwg.org/#this)’s [shadow root](#49-interface-element).
2. If shadow is null or its [mode](#48-interface-shadowroot) is "`closed`", then return null.
3. Return shadow.

---

`` registry = element . `customElementRegistry` ``

Returns element’s [`CustomElementRegistry`](html-spec-whatwg-org.md#4134-the-customelementregistry-interface) object, if any; otherwise null.

The `customElementRegistry` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [custom element registry](#49-interface-element).

---

`` element . `closest(selectors)` ``

Returns the first (starting at element) [inclusive ancestor](#11-trees) that matches selectors, and null otherwise.

`` element . `matches(selectors)` ``

Returns true if matching selectors against element’s [root](#11-trees) yields element; otherwise false.

The `closest(selectors)` method steps are:
1. Let selector be the result of [parse a selector](https://drafts.csswg.org/selectors-4/#parse-a-selector) from selectors. [\[SELECTORS4\]](#normative-references)
2. If selector is failure, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let elements be [this](https://webidl.spec.whatwg.org/#this)’s [inclusive ancestors](#11-trees) that are [elements](#49-interface-element), in reverse [tree order](#11-trees).
4. For each element of elements: if [match a selector against an element](https://drafts.csswg.org/selectors-4/#match-a-selector-against-an-element), using selector, element, and [scoping root](https://drafts.csswg.org/selectors-4/#scoping-root) [this](https://webidl.spec.whatwg.org/#this), returns success, return element. [\[SELECTORS4\]](#normative-references)
5. Return null.

The `matches(selectors)` and `webkitMatchesSelector(selectors)` method steps are:
1. Let selector be the result of [parse a selector](https://drafts.csswg.org/selectors-4/#parse-a-selector) from selectors. [\[SELECTORS4\]](#normative-references)
2. If selector is failure, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If the result of [match a selector against an element](https://drafts.csswg.org/selectors-4/#match-a-selector-against-an-element), using selector, [this](https://webidl.spec.whatwg.org/#this), and [scoping root](https://drafts.csswg.org/selectors-4/#scoping-root) [this](https://webidl.spec.whatwg.org/#this), returns success, then return true; otherwise, return false. [\[SELECTORS4\]](#normative-references)

---

The `getElementsByTagName(qualifiedName)` method steps are to return the [list of elements with qualified name qualifiedName](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this).

The `getElementsByTagNameNS(namespace, localName)` method steps are to return the [list of elements with namespace namespace and local name localName](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this).

The `getElementsByClassName(classNames)` method steps are to return the [list of elements with class names classNames](#44-interface-node) for [this](https://webidl.spec.whatwg.org/#this).

---

To insert adjacent, given an [element](#49-interface-element) element, string where, and a [node](#42-node-tree) node, run the steps associated with the first [ASCII case-insensitive](infra-spec-whatwg-org.md#47-strings) match for where:

"`beforebegin`"

If element’s [parent](#11-trees) is null, return null.

Return the result of [pre-inserting](#423-mutation-algorithms) node into element’s [parent](#11-trees) before element.

"`afterbegin`"

Return the result of [pre-inserting](#423-mutation-algorithms) node into element before element’s [first child](#11-trees).

"`beforeend`"

Return the result of [pre-inserting](#423-mutation-algorithms) node into element before null.

"`afterend`"

If element’s [parent](#11-trees) is null, return null.

Return the result of [pre-inserting](#423-mutation-algorithms) node into element’s [parent](#11-trees) before element’s [next sibling](#11-trees).

Otherwise

[Throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

The `insertAdjacentElement(where, element)` method steps are to return the result of running [insert adjacent](#49-interface-element), give [this](https://webidl.spec.whatwg.org/#this), where, and element.

The `insertAdjacentText(where, data)` method steps are:
1. Let text be the result of [creating a text node](#411-interface-text) given [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node) and data.
2. Run [insert adjacent](#49-interface-element), given [this](https://webidl.spec.whatwg.org/#this), where, and text.

> [!note]
> This method returns nothing because it existed before we had a chance to design it.

#### 4.9.1. Interface [`NamedNodeMap`](#491-interface-namednodemap)

```webidl
[Exposed=Window,
 LegacyUnenumerableNamedProperties]
interface NamedNodeMap {
  readonly attribute unsigned long length;
  getter Attr? item(unsigned long index);
  getter Attr? getNamedItem(DOMString qualifiedName);
  Attr? getNamedItemNS(DOMString? namespace, DOMString localName);
  [CEReactions] Attr? setNamedItem(Attr attr);
  [CEReactions] Attr? setNamedItemNS(Attr attr);
  [CEReactions] Attr removeNamedItem(DOMString qualifiedName);
  [CEReactions] Attr removeNamedItemNS(DOMString? namespace, DOMString localName);
};

```

A [`NamedNodeMap`](#491-interface-namednodemap) has an associated element (an [element](#49-interface-element)).

A [`NamedNodeMap`](#491-interface-namednodemap) object’s attribute list is its [element](#491-interface-namednodemap)’s [attribute list](#49-interface-element).

---

A [`NamedNodeMap`](#491-interface-namednodemap) object’s [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices) are the numbers in the range zero to its [attribute list](#491-interface-namednodemap)’s [size](infra-spec-whatwg-org.md#51-lists) − 1, unless the [attribute list](#491-interface-namednodemap) [is empty](infra-spec-whatwg-org.md#51-lists), in which case there are no [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices).

The `length` getter steps are to return the [attribute list](#491-interface-namednodemap)’s [size](infra-spec-whatwg-org.md#51-lists).

The `item(index)` method steps are:
1. If index is equal to or greater than [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#491-interface-namednodemap)’s [size](infra-spec-whatwg-org.md#51-lists), then return null.
2. Otherwise, return [this](https://webidl.spec.whatwg.org/#this)’s [attribute list](#491-interface-namednodemap)\[index\].

A [`NamedNodeMap`](#491-interface-namednodemap) object’s [supported property names](https://webidl.spec.whatwg.org/#dfn-supported-property-names) are the return value of running these steps:
1. Let names be the [qualified names](#492-interface-attr) of the [attributes](#492-interface-attr) in this [`NamedNodeMap`](#491-interface-namednodemap) object’s [attribute list](#491-interface-namednodemap), with duplicates omitted, in order.
2. If this [`NamedNodeMap`](#491-interface-namednodemap) object’s [element](#491-interface-namednodemap) is in the [HTML namespace](infra-spec-whatwg-org.md#8-namespaces) and its [node document](#44-interface-node) is an [HTML document](#45-interface-document), then [for each](infra-spec-whatwg-org.md#51-lists) name of names:
   1. Let lowercaseName be name, in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
   2. If lowercaseName is not equal to name, remove name from names.
3. Return names.

The `getNamedItem(qualifiedName)` method steps are to return the result of [getting an attribute](#49-interface-element) given qualifiedName and [element](#491-interface-namednodemap).

The `getNamedItemNS(namespace, localName)` method steps are to return the result of [getting an attribute](#49-interface-element) given namespace, localName, and [element](#491-interface-namednodemap).

The `setNamedItem(attr)` and `setNamedItemNS(attr)` method steps are to return the result of [setting an attribute](#49-interface-element) given attr and [element](#491-interface-namednodemap).

The `removeNamedItem(qualifiedName)` method steps are:
1. Let attr be the result of [removing an attribute](#49-interface-element) given qualifiedName and [element](#491-interface-namednodemap).
2. If attr is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotFoundError`](https://webidl.spec.whatwg.org/#notfounderror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Return attr.

The `removeNamedItemNS(namespace, localName)` method steps are:
1. Let attr be the result of [removing an attribute](#49-interface-element) given namespace, localName, and [element](#491-interface-namednodemap).
2. If attr is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotFoundError`](https://webidl.spec.whatwg.org/#notfounderror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Return attr.

#### 4.9.2. Interface [`Attr`](#492-interface-attr)

```webidl
[Exposed=Window]
interface Attr : Node {
  readonly attribute DOMString? namespaceURI;
  readonly attribute DOMString? prefix;
  readonly attribute DOMString localName;
  readonly attribute DOMString name;
  [CEReactions] attribute DOMString value;

  readonly attribute Element? ownerElement;

  readonly attribute boolean specified; // historical; always returns true
};
```

[`Attr`](#492-interface-attr) [nodes](#42-node-tree) are simply known as attributes. They are sometimes referred to as *content attributes* to avoid confusion with IDL attributes.

[Attributes](#492-interface-attr) have a namespace (null or a non-empty string), namespace prefix (null or a non-empty string), local name (a non-empty string), value (a string), and element (null or an [element](#49-interface-element)).

> [!note]
> If designed today they would just have a name and value. ☹

An [attribute](#492-interface-attr)’s qualified name is its [local name](#492-interface-attr) if its [namespace prefix](#492-interface-attr) is null, and its [namespace prefix](#492-interface-attr), followed by "`:`", followed by its [local name](#492-interface-attr), otherwise.

> [!note]
> User agents could have this as an internal slot as an optimization.

To create an attribute given a [document](#45-interface-document) document, a string localName, and optionally a string-or-null namespace (default null), a string-or-null prefix (default null), and a string value (default the empty string):
1. Let attribute be the result of [creating a node](#44-interface-node) that implements [`Attr`](#492-interface-attr), given document.
2. Set attribute’s [namespace](#492-interface-attr) to namespace, [namespace prefix](#492-interface-attr) to prefix, [local name](#492-interface-attr) to localName, and [value](#492-interface-attr) to value.
3. Return attribute.

An `A` attribute is an [attribute](#492-interface-attr) whose [local name](#492-interface-attr) is `A` and whose [namespace](#492-interface-attr) and [namespace prefix](#492-interface-attr) are null.

---

The `namespaceURI` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [namespace](#492-interface-attr).

The `prefix` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [namespace prefix](#492-interface-attr).

The `localName` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [local name](#492-interface-attr).

The `name` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [qualified name](#492-interface-attr).

The `value` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [value](#492-interface-attr).

To set an existing attribute value, given an [attribute](#492-interface-attr) attribute and string value, run these steps:
1. If attribute’s [element](#492-interface-attr) is null, then set attribute’s [value](#492-interface-attr) to value and return.
2. Let element be attribute’s [element](#492-interface-attr).
3. Let verifiedValue be the result of calling [get trusted type compliant attribute value](https://w3c.github.io/trusted-types/dist/spec/#get-trusted-type-compliant-attribute-value) with attribute’s [local name](#492-interface-attr), attribute’s [namespace](#492-interface-attr), element, and value. [\[TRUSTED-TYPES\]](#normative-references)
4. If attribute’s [element](#492-interface-attr) is null, then set attribute’s [value](#492-interface-attr) to verifiedValue and return.
5. [Change](#49-interface-element) attribute to verifiedValue.

The [`value`](#492-interface-attr) setter steps are to [set an existing attribute value](#492-interface-attr) with [this](https://webidl.spec.whatwg.org/#this) and the given value.

---

The `ownerElement` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [element](#492-interface-attr).

---

The `specified` getter steps are to return true.

### 4.10. Interface [`CharacterData`](#410-interface-characterdata)

```webidl
[Exposed=Window]
interface CharacterData : Node {
  attribute [LegacyNullToEmptyString] DOMString data;
  readonly attribute unsigned long length;
  DOMString substringData(unsigned long offset, unsigned long count);
  undefined appendData(DOMString data);
  undefined insertData(unsigned long offset, DOMString data);
  undefined deleteData(unsigned long offset, unsigned long count);
  undefined replaceData(unsigned long offset, unsigned long count, DOMString data);
};

```

> [!note]
> [`CharacterData`](#410-interface-characterdata) is an abstract interface. You cannot get a direct instance of it. It is used by [`Text`](#411-interface-text), [`ProcessingInstruction`](#413-interface-processinginstruction), and [`Comment`](#414-interface-comment) [nodes](#42-node-tree).

Each [node](#42-node-tree) inheriting from the [`CharacterData`](#410-interface-characterdata) interface has an associated mutable string called data.

To replace data of a [node](#42-node-tree) node with an integer offset, integer count, string data, and an optional boolean piAttributesAlreadyUpdated (default false):
1. Let length be node’s [length](#42-node-tree).
2. If offset is greater than length, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`IndexSizeError`](https://webidl.spec.whatwg.org/#indexsizeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If offset + count is greater than length, then set count to length − offset.
4. [Queue a mutation record](#432-queuing-a-mutation-record) of "`characterData`" for node with null, null, node’s [data](#410-interface-characterdata), « », « », null, and null.
5. Insert data into node’s [data](#410-interface-characterdata) after offset [code units](infra-spec-whatwg-org.md#47-strings).
6. Let deleteOffset be offset + data’s [length](infra-spec-whatwg-org.md#47-strings).
7. Starting from deleteOffset [code units](infra-spec-whatwg-org.md#47-strings), remove count [code units](infra-spec-whatwg-org.md#47-strings) from node’s [data](#410-interface-characterdata).
8. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is node and [start offset](#53-interface-abstractrange) is greater than offset but less than or equal to offset + count: set its [start offset](#53-interface-abstractrange) to offset.
9. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is node and [end offset](#53-interface-abstractrange) is greater than offset but less than or equal to offset + count: set its [end offset](#53-interface-abstractrange) to offset.
10. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is node and [start offset](#53-interface-abstractrange) is greater than offset + count: increase its [start offset](#53-interface-abstractrange) by data’s [length](infra-spec-whatwg-org.md#47-strings) and decrease it by count.
11. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is node and [end offset](#53-interface-abstractrange) is greater than offset + count: increase its [end offset](#53-interface-abstractrange) by data’s [length](infra-spec-whatwg-org.md#47-strings) and decrease it by count.
12. If node is a [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) and piAttributesAlreadyUpdated is false, then [update attributes from data](#413-interface-processinginstruction) given node.
13. If node’s [parent](#11-trees) is non-null, then run the [children changed steps](#423-mutation-algorithms) for node’s [parent](#11-trees).

To substring data of a [node](#42-node-tree) node with an integer offset and integer count:
1. Let length be node’s [length](#42-node-tree).
2. If offset is greater than length, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`IndexSizeError`](https://webidl.spec.whatwg.org/#indexsizeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If offset + count is greater than length, then return a string whose value is the [code units](infra-spec-whatwg-org.md#47-strings) from the offsetth [code unit](infra-spec-whatwg-org.md#47-strings) to the end of node’s [data](#410-interface-characterdata).
4. Return a string whose value is the [code units](infra-spec-whatwg-org.md#47-strings) from the offsetth [code unit](infra-spec-whatwg-org.md#47-strings) to the offset+countth [code unit](infra-spec-whatwg-org.md#47-strings) in node’s [data](#410-interface-characterdata).

The `data` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [data](#410-interface-characterdata). Its setter steps are to [replace data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with 0, [this](https://webidl.spec.whatwg.org/#this)’s [length](#42-node-tree), and the given value.

The `length` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [length](#42-node-tree).

The `substringData(offset, count)` method steps are to return the result of [substringing data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with offset and count.

The `appendData(data)` method steps are to [replace data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with [this](https://webidl.spec.whatwg.org/#this)’s [length](#42-node-tree), 0, and data.

The `insertData(offset, data)` method steps are to [replace data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with offset, 0, and data.

The `deleteData(offset, count)` method steps are to [replace data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with offset, count, and the empty string.

The `replaceData(offset, count, data)` method steps are to [replace data](#410-interface-characterdata) of [this](https://webidl.spec.whatwg.org/#this) with offset, count, and data.

### 4.11. Interface [`Text`](#411-interface-text)

```webidl
[Exposed=Window]
interface Text : CharacterData {
  constructor(optional DOMString data = "");

  [NewObject] Text splitText(unsigned long offset);
  readonly attribute DOMString wholeText;
};

```

`text = new Text([data = ""])`

Returns a new [`Text`](#411-interface-text) [node](#42-node-tree) whose [data](#410-interface-characterdata) is data.

`` text . `splitText(offset)` ``

Splits [data](#410-interface-characterdata) at the given offset and returns the remainder as [`Text`](#411-interface-text) [node](#42-node-tree).

`` text . `wholeText` ``

Returns the combined [data](#410-interface-characterdata) of all direct [`Text`](#411-interface-text) [node](#42-node-tree) [siblings](#11-trees).

---

An exclusive [`Text`](#411-interface-text) node is a [`Text`](#411-interface-text) [node](#42-node-tree) that is not a [`CDATASection`](#412-interface-cdatasection) [node](#42-node-tree).

The contiguous [`Text`](#411-interface-text) nodes of a [node](#42-node-tree) node are node, node’s [previous sibling](#11-trees) [`Text`](#411-interface-text) [node](#42-node-tree), if any, and its [contiguous `Text` nodes](#411-interface-text), and node’s [next sibling](#11-trees) [`Text`](#411-interface-text) [node](#42-node-tree), if any, and its [contiguous `Text` nodes](#411-interface-text), avoiding any duplicates.

The contiguous exclusive [`Text`](#411-interface-text) nodes of a [node](#42-node-tree) node are node, node’s [previous sibling](#11-trees) [exclusive `Text` node](#411-interface-text), if any, and its [contiguous exclusive `Text` nodes](#411-interface-text), and node’s [next sibling](#11-trees) [exclusive `Text` node](#411-interface-text), if any, and its [contiguous exclusive `Text` nodes](#411-interface-text), avoiding any duplicates.

The child text content of a [node](#42-node-tree) node is the [concatenation](infra-spec-whatwg-org.md#47-strings) of the [data](#410-interface-characterdata) of all the [`Text`](#411-interface-text) [node](#42-node-tree) [children](#11-trees) of node, in [tree order](#11-trees).

The descendant text content of a [node](#42-node-tree) node is the [concatenation](infra-spec-whatwg-org.md#47-strings) of the [data](#410-interface-characterdata) of all the [`Text`](#411-interface-text) [node](#42-node-tree) [descendants](#11-trees) of node, in [tree order](#11-trees).

To create a text node given a [document](#45-interface-document) document and a string data:
1. Let text be the result of [creating a node](#44-interface-node) that implements [`Text`](#411-interface-text), given document.
2. Set text’s [data](#410-interface-characterdata) to data.
3. Return text.

---

The `new Text(data)` constructor steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [data](#410-interface-characterdata) to data and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node) to [current global object](html-spec-whatwg-org.md#81333-current)’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object).

To split a [`Text`](#411-interface-text) [node](#42-node-tree) node with integer offset:
1. Let length be node’s [length](#42-node-tree).
2. If offset is greater than length, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`IndexSizeError`](https://webidl.spec.whatwg.org/#indexsizeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let count be length − offset.
4. Let newData be the result of [substringing data](#410-interface-characterdata) of node with offset and count.
5. Let newNode be the result of [creating a text node](#411-interface-text) given node’s [node document](#44-interface-node) and newData.
6. Let parent be node’s [parent](#11-trees).
7. If parent is non-null:
   1. [Insert](#423-mutation-algorithms) newNode into parent before node’s [next sibling](#11-trees).
   2. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is node and [start offset](#53-interface-abstractrange) is greater than offset, set its [start node](#53-interface-abstractrange) to newNode and decrease its [start offset](#53-interface-abstractrange) by offset.
   3. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is node and [end offset](#53-interface-abstractrange) is greater than offset, set its [end node](#53-interface-abstractrange) to newNode and decrease its [end offset](#53-interface-abstractrange) by offset.
   4. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is parent and [start offset](#53-interface-abstractrange) is equal to the [index](#11-trees) of node plus 1, increase its [start offset](#53-interface-abstractrange) by 1.
   5. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is parent and [end offset](#53-interface-abstractrange) is equal to the [index](#11-trees) of node plus 1, increase its [end offset](#53-interface-abstractrange) by 1.
8. [Replace data](#410-interface-characterdata) of node with offset, count, and the empty string.
9. Return newNode.

The `splitText(offset)` method steps are to [split](#411-interface-text) [this](https://webidl.spec.whatwg.org/#this) with offset offset.

The `wholeText` getter steps are to return the [concatenation](infra-spec-whatwg-org.md#47-strings) of the [data](#410-interface-characterdata) of the [contiguous `Text` nodes](#411-interface-text) of [this](https://webidl.spec.whatwg.org/#this), in [tree order](#11-trees).

### 4.12. Interface [`CDATASection`](#412-interface-cdatasection)

```webidl
[Exposed=Window]
interface CDATASection : Text {
};
```

To create a CDATA section node given a [document](#45-interface-document) document and a string data:
1. Let node be the result of [creating a node](#44-interface-node) that implements [`CDATASection`](#412-interface-cdatasection), given document.
2. Set node’s [data](#410-interface-characterdata) to data.
3. Return node.

### 4.13. Interface [`ProcessingInstruction`](#413-interface-processinginstruction)

```webidl
[Exposed=Window]
interface ProcessingInstruction : CharacterData {
  constructor(DOMString target, optional DOMString data = "");

  readonly attribute DOMString target;

  boolean hasAttributes();
  sequence<DOMString> getAttributeNames();
  DOMString? getAttribute(DOMString name);
  undefined setAttribute(DOMString name, DOMString value);
  undefined removeAttribute(DOMString name);
  boolean toggleAttribute(DOMString name, optional boolean force);
  boolean hasAttribute(DOMString name);
};
```

`pi = new ProcessingInstruction(target [, data = ""])`

Returns a new [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) whose [target](#413-interface-processinginstruction) is target and [data](#410-interface-characterdata) is data.

`` pi . `target` ``

Returns the [target](#413-interface-processinginstruction).

`pi . hasAttributes()`

Returns true if pi has attributes; otherwise false.

`pi . getAttributeNames()`

Returns the names of all of pi’s attributes. Cannot contain duplicates.

`pi . getAttribute(name)`

Returns the value of pi’s attribute named name, and null if there is no such attribute.

`pi . setAttribute(name, value)`

Sets pi’s attribute named name to value.

`pi . removeAttribute(name)`

Removes pi’s attribute named name.

`pi . toggleAttribute(name [, force])`

If force is not given, "toggles" name, removing it if it is present and adding it if it is not present. If force is true, adds name. If force is false, removes name.

Returns true if name is now present; otherwise false.

`pi . hasAttribute(name)`

Returns true if pi has an attribute named name; otherwise false.

[`ProcessingInstruction`](#413-interface-processinginstruction) [nodes](#42-node-tree) have an associated target.

[`ProcessingInstruction`](#413-interface-processinginstruction) [nodes](#42-node-tree) have an associated attribute map, which is a [map](infra-spec-whatwg-org.md#52-maps), initially empty.

To create a processing instruction node given a [document](#45-interface-document) document, a string target, and a string data:
1. Let pi be the result of [creating a node](#44-interface-node) that implements [`ProcessingInstruction`](#413-interface-processinginstruction), given document.
2. [Initialize](#413-interface-processinginstruction) pi with target and data.
3. Return pi.

To initialize a [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) pi, with target and data:
1. If target does not match the [`Name`](https://www.w3.org/TR/xml/#NT-Name) production, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If data contains the string "`?>`", then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Set pi’s [target](#413-interface-processinginstruction) to target.
4. Set pi’s [data](#410-interface-characterdata) to data.
5. [Update attributes from data](#413-interface-processinginstruction) given pi.

To update attributes from data, given a [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) pi:
1. [Clear](infra-spec-whatwg-org.md#52-maps) pi’s [attribute map](#413-interface-processinginstruction).
2. Let result be the [parsing result](https://www.w3.org/TR/xml-stylesheet/#dt-parsing-result) of invoking the [rules for parsing pseudo-attributes from a string](https://www.w3.org/TR/xml-stylesheet/#dt-parsing) given pi’s [data](#410-interface-characterdata).
3. If result is an error, then return.
4. For each [pseudo-attribute](https://www.w3.org/TR/xml-stylesheet/#dt-pseudo-attribute) pseudoAttr of result: [set](infra-spec-whatwg-org.md#52-maps) pi’s [attribute map](#413-interface-processinginstruction)\[pseudoAttr’s [name](https://www.w3.org/TR/xml-stylesheet/#dt-name)\] to pseudoAttr’s [value](https://www.w3.org/TR/xml-stylesheet/#dt-value).

To update data from attributes, given a [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) pi:
1. Let data be the empty string.
2. [For each](infra-spec-whatwg-org.md#52-maps) name → value of pi’s [attribute map](#413-interface-processinginstruction):
   1. If data is not the empty string, then append U+0020 SPACE to data.
   2. Append name to data.
   3. Append U+003D (=) to data.
   4. Append U+0022 (") to data.
   5. Replace any U+0026 (&) in value with "`&amp;`".
   6. Replace any U+003C (<) in value with "`&lt;`".
   7. Replace any U+003E (>) in value with "`&gt;`".
   8. Replace any U+0022 (") in value with "`&quot;`".
   9. Append value to data.
   10. Append U+0022 (") to data.
3. [Replace data](#410-interface-characterdata) of pi with 0, pi’s [length](#42-node-tree), data, and true.

To get a processing instruction attribute, given a [`ProcessingInstruction`](#413-interface-processinginstruction) [node](#42-node-tree) pi and a string name: return pi’s [attribute map](#413-interface-processinginstruction)\[name\] [with default](infra-spec-whatwg-org.md#52-maps) null.

---

The `new ProcessingInstruction(target, data)` constructor steps are:
1. Set [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node) to [current global object](html-spec-whatwg-org.md#81333-current)’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object).
2. [Initialize](#413-interface-processinginstruction) [this](https://webidl.spec.whatwg.org/#this) with target and data.

The `target` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [target](#413-interface-processinginstruction).

The `hasAttributes()` method steps are to return false if [this](https://webidl.spec.whatwg.org/#this)’s [attribute map](#413-interface-processinginstruction) [is empty](infra-spec-whatwg-org.md#52-maps); otherwise true.

The `getAttributeNames()` method steps are to return the result of [getting the keys](infra-spec-whatwg-org.md#52-maps) of [this](https://webidl.spec.whatwg.org/#this)’s [attribute map](#413-interface-processinginstruction).

The `getAttribute(name)` method steps are to return the result of [getting a processing instruction attribute](#413-interface-processinginstruction) given [this](https://webidl.spec.whatwg.org/#this) and name.

The `setAttribute(name, value)` method steps are:
1. If name is not a [valid attribute local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. [Set](infra-spec-whatwg-org.md#52-maps) [this](https://webidl.spec.whatwg.org/#this)’s [attribute map](#413-interface-processinginstruction)\[name\] to value.
3. [Update data from attributes](#413-interface-processinginstruction) given [this](https://webidl.spec.whatwg.org/#this).

The `removeAttribute(name)` method steps are:
1. [Remove](infra-spec-whatwg-org.md#52-maps) [this](https://webidl.spec.whatwg.org/#this)’s [attribute map](#413-interface-processinginstruction)\[name\].
2. [Update data from attributes](#413-interface-processinginstruction) given [this](https://webidl.spec.whatwg.org/#this).

The `toggleAttribute(name, force)` method steps are:
1. If name is not a [valid attribute local name](#14-name-validation), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Let attributes be [this](https://webidl.spec.whatwg.org/#this)’s [attribute map](#413-interface-processinginstruction).
3. If attributes\[name\] does not [exist](infra-spec-whatwg-org.md#52-maps):
   1. If force is not given or is true, [set](infra-spec-whatwg-org.md#52-maps) attributes\[name\] to the empty string, [update data from attributes](#413-interface-processinginstruction) given [this](https://webidl.spec.whatwg.org/#this), and then return true.
   2. Return false.
4. If force is not given or is false, [remove](infra-spec-whatwg-org.md#52-maps) attributes\[name\], [update data from attributes](#413-interface-processinginstruction) given [this](https://webidl.spec.whatwg.org/#this), and then return false.
5. Return true.

The `hasAttribute(name)` method steps are to return true if [this](https://webidl.spec.whatwg.org/#this)’s [attribute map](#413-interface-processinginstruction)\[name\] [exists](infra-spec-whatwg-org.md#51-lists); otherwise false.

### 4.14. Interface [`Comment`](#414-interface-comment)

```webidl
[Exposed=Window]
interface Comment : CharacterData {
  constructor(optional DOMString data = "");
};

```

`comment = new Comment([data = ""])`

Returns a new [`Comment`](#414-interface-comment) [node](#42-node-tree) whose [data](#410-interface-characterdata) is data.

To create a comment node given a [document](#45-interface-document) document and a string data:
1. Let comment be the result of [creating a node](#44-interface-node) that implements [`Comment`](#414-interface-comment), given document.
2. Set comment’s [data](#410-interface-characterdata) to data.
3. Return comment.

The `new Comment(data)` constructor steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [data](#410-interface-characterdata) to data and [this](https://webidl.spec.whatwg.org/#this)’s [node document](#44-interface-node) to [current global object](html-spec-whatwg-org.md#81333-current)’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object).

## 5. Ranges

### 5.1. Introduction to "DOM Ranges"

[`StaticRange`](#54-interface-staticrange) and [`Range`](#55-interface-range) objects ([ranges](#53-interface-abstractrange)) represent a sequence of content within a [node tree](#42-node-tree). Each [range](#53-interface-abstractrange) has a [start](#53-interface-abstractrange) and an [end](#53-interface-abstractrange) which are [boundary points](#52-boundary-points). A [boundary point](#52-boundary-points) is a [tuple](infra-spec-whatwg-org.md#531-tuples) consisting of a [node](#52-boundary-points) and an [offset](#52-boundary-points). So in other words, a [range](#53-interface-abstractrange) represents a piece of content within a [node tree](#42-node-tree) between two [boundary points](#52-boundary-points).

[Ranges](#53-interface-abstractrange) are frequently used in editing for selecting and copying content.
- [`Element`](#49-interface-element): `p`
  - [`Element`](#49-interface-element): `<img src="insanity-wolf" alt="Little-endian BOM; decode as big-endian!">`
  - [`Text`](#411-interface-text):  CSS 2.1 syndata is 
  - [`Element`](#49-interface-element): `<em>`
    - [`Text`](#411-interface-text): awesome
  - [`Text`](#411-interface-text): !

In the [node tree](#42-node-tree) above, a [range](#53-interface-abstractrange) can be used to represent the sequence “syndata is awes”. Assuming p is assigned to the `p` [element](#49-interface-element), and em to the `em` [element](#49-interface-element), this would be done as follows:

```
var range = new Range(),
    firstText = p.childNodes[1],
    secondText = em.firstChild
range.setStart(firstText, 9) // do not forget the leading space
range.setEnd(secondText, 4)
// range now stringifies to the aforementioned quote

```

> [!note]
> [Attributes](#492-interface-attr) such as `src` and `alt` in the [node tree](#42-node-tree) above cannot be represented by a [range](#53-interface-abstractrange). [Ranges](#53-interface-abstractrange) are only useful for [nodes](#42-node-tree).

[`Range`](#55-interface-range) objects, unlike [`StaticRange`](#54-interface-staticrange) objects, are affected by mutations to the [node tree](#42-node-tree). Therefore they are also known as [live ranges](#55-interface-range). Such mutations will not invalidate them and will try to ensure that it still represents the same piece of content. Necessarily, a [live range](#55-interface-range) might itself be modified as part of the mutation to the [node tree](#42-node-tree) when, e.g., part of the content it represents is mutated.

> [!note]
> See the [insert](#423-mutation-algorithms) and [remove](#423-mutation-algorithms) algorithms, the [`normalize()`](#44-interface-node) method, and the [replace data](#410-interface-characterdata) and [split](#411-interface-text) algorithms for details.

Updating [live ranges](#55-interface-range) in response to [node tree](#42-node-tree) mutations can be expensive. For every [node tree](#42-node-tree) change, all affected [`Range`](#55-interface-range) objects need to be updated. Even if the application is uninterested in some [live ranges](#55-interface-range), it still has to pay the cost of keeping them up-to-date when a mutation occurs.

A [`StaticRange`](#54-interface-staticrange) object is a lightweight [range](#53-interface-abstractrange) that does not update when the [node tree](#42-node-tree) mutates. It is therefore not subject to the same maintenance cost as [live ranges](#55-interface-range).

### 5.2. Boundary points

A boundary point is a [tuple](infra-spec-whatwg-org.md#531-tuples) consisting of a node (a [node](#42-node-tree)) and an offset (a non-negative integer).

> [!note]
> A correct [boundary point](#52-boundary-points)’s [offset](#52-boundary-points) will be between 0 and the [boundary point](#52-boundary-points)’s [node](#52-boundary-points)’s [length](#42-node-tree), inclusive.

The position of a [boundary point](#52-boundary-points) (nodeA, offsetA) relative to a [boundary point](#52-boundary-points) (nodeB, offsetB) is before, equal, or after, as returned by these steps:
1. Assert: nodeA and nodeB have the same [root](#11-trees).
2. If nodeA is nodeB, then return [equal](#52-boundary-points) if offsetA is offsetB, [before](#52-boundary-points) if offsetA is less than offsetB, and [after](#52-boundary-points) if offsetA is greater than offsetB.
3. If nodeA is [following](#11-trees) nodeB, then if the [position](#52-boundary-points) of (nodeB, offsetB) relative to (nodeA, offsetA) is [before](#52-boundary-points), return [after](#52-boundary-points), and if it is [after](#52-boundary-points), return [before](#52-boundary-points).
4. If nodeA is an [ancestor](#11-trees) of nodeB:
   1. Let child be nodeB.
   2. While child is not a [child](#11-trees) of nodeA, set child to its [parent](#11-trees).
   3. If child’s [index](#11-trees) is less than offsetA, then return [after](#52-boundary-points).
5. Return [before](#52-boundary-points).

### 5.3. Interface [`AbstractRange`](#53-interface-abstractrange)

```webidl
[Exposed=Window]
interface AbstractRange {
  readonly attribute Node startContainer;
  readonly attribute unsigned long startOffset;
  readonly attribute Node endContainer;
  readonly attribute unsigned long endOffset;
  readonly attribute boolean collapsed;
};

```

Objects implementing the [`AbstractRange`](#53-interface-abstractrange) interface are known as ranges.

A [range](#53-interface-abstractrange) has two associated [boundary points](#52-boundary-points) — a start and end.

For convenience, a [range](#53-interface-abstractrange)’s start node is its [start](#53-interface-abstractrange)’s [node](#52-boundary-points), its start offset is its [start](#53-interface-abstractrange)’s [offset](#52-boundary-points), its end node is its [end](#53-interface-abstractrange)’s [node](#52-boundary-points), and its end offset is its [end](#53-interface-abstractrange)’s [offset](#52-boundary-points).

A [range](#53-interface-abstractrange) is collapsed if its [start node](#53-interface-abstractrange) is its [end node](#53-interface-abstractrange) and its [start offset](#53-interface-abstractrange) is its [end offset](#53-interface-abstractrange).

`node = range . startContainer`

Returns range’s [start node](#53-interface-abstractrange).

`offset = range . startOffset`

Returns range’s [start offset](#53-interface-abstractrange).

`node = range . endContainer`

Returns range’s [end node](#53-interface-abstractrange).

`offset = range . endOffset`

Returns range’s [end offset](#53-interface-abstractrange).

`collapsed = range . collapsed`

Returns true if range is [collapsed](#53-interface-abstractrange); otherwise false.

The `startContainer` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [start node](#53-interface-abstractrange).

The `startOffset` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [start offset](#53-interface-abstractrange).

The `endContainer` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [end node](#53-interface-abstractrange).

The `endOffset` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [end offset](#53-interface-abstractrange).

The `collapsed` getter steps are to return true if [this](https://webidl.spec.whatwg.org/#this) is [collapsed](#53-interface-abstractrange); otherwise false.

### 5.4. Interface [`StaticRange`](#54-interface-staticrange)

```webidl
dictionary StaticRangeInit {
  required Node startContainer;
  required unsigned long startOffset;
  required Node endContainer;
  required unsigned long endOffset;
};

[Exposed=Window]
interface StaticRange : AbstractRange {
  constructor(StaticRangeInit init);
};

```

`staticRange = new StaticRange(init)`

Returns a new [range](#53-interface-abstractrange) object that does not update when the [node tree](#42-node-tree) mutates.

The `new StaticRange(init)` constructor steps are:
1. If init\["[`startContainer`](#54-interface-staticrange)"\] or init\["[`endContainer`](#54-interface-staticrange)"\] is a [`DocumentType`](#46-interface-documenttype) or [`Attr`](#492-interface-attr) [node](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Set [this](https://webidl.spec.whatwg.org/#this)’s [start](#53-interface-abstractrange) to (init\["[`startContainer`](#54-interface-staticrange)"\], init\["[`startOffset`](#54-interface-staticrange)"\]) and [end](#53-interface-abstractrange) to (init\["[`endContainer`](#54-interface-staticrange)"\], init\["[`endOffset`](#54-interface-staticrange)"\]).

A [`StaticRange`](#54-interface-staticrange) is valid if all of the following are true:
- Its [start](#53-interface-abstractrange) and [end](#53-interface-abstractrange) are in the same [node tree](#42-node-tree).
- Its [start offset](#53-interface-abstractrange) is between 0 and its [start node](#53-interface-abstractrange)’s [length](#42-node-tree), inclusive.
- Its [end offset](#53-interface-abstractrange) is between 0 and its [end node](#53-interface-abstractrange)’s [length](#42-node-tree), inclusive.
- Its [start](#53-interface-abstractrange) is [before](#52-boundary-points) or [equal](#52-boundary-points) to its [end](#53-interface-abstractrange).

### 5.5. Interface [`Range`](#55-interface-range)

```webidl
[Exposed=Window]
interface Range : AbstractRange {
  constructor();

  readonly attribute Node commonAncestorContainer;

  undefined setStart(Node node, unsigned long offset);
  undefined setEnd(Node node, unsigned long offset);
  undefined setStartBefore(Node node);
  undefined setStartAfter(Node node);
  undefined setEndBefore(Node node);
  undefined setEndAfter(Node node);
  undefined collapse(optional boolean toStart = false);
  undefined selectNode(Node node);
  undefined selectNodeContents(Node node);

  const unsigned short START_TO_START = 0;
  const unsigned short START_TO_END = 1;
  const unsigned short END_TO_END = 2;
  const unsigned short END_TO_START = 3;
  short compareBoundaryPoints(unsigned short how, Range sourceRange);

  [CEReactions] undefined deleteContents();
  [CEReactions, NewObject] DocumentFragment extractContents();
  [CEReactions, NewObject] DocumentFragment cloneContents();
  [CEReactions] undefined insertNode(Node node);
  [CEReactions] undefined surroundContents(Node newParent);

  [NewObject] Range cloneRange();
  undefined detach();

  boolean isPointInRange(Node node, unsigned long offset);
  short comparePoint(Node node, unsigned long offset);

  boolean intersectsNode(Node node);

  stringifier;
};

```

Objects implementing the [`Range`](#55-interface-range) interface are known as live ranges.

> [!note]
> Algorithms that modify a [tree](#11-trees) (in particular the [insert](#423-mutation-algorithms), [remove](#423-mutation-algorithms), [move](#423-mutation-algorithms), [replace data](#410-interface-characterdata), and [split](#411-interface-text) algorithms) modify [live ranges](#55-interface-range) associated with that [tree](#11-trees).

The root of a [live range](#55-interface-range) is the [root](#11-trees) of its [start node](#53-interface-abstractrange).

A [node](#42-node-tree) node is contained in a [live range](#55-interface-range) range if node’s [root](#11-trees) is range’s [root](#55-interface-range), and (node, 0) is [after](#52-boundary-points) range’s [start](#53-interface-abstractrange), and (node, node’s [length](#42-node-tree)) is [before](#52-boundary-points) range’s [end](#53-interface-abstractrange).

A [node](#42-node-tree) is partially contained in a [live range](#55-interface-range) if it’s an [inclusive ancestor](#11-trees) of the [live range](#55-interface-range)’s [start node](#53-interface-abstractrange) but not its [end node](#53-interface-abstractrange), or vice versa.

> [!note]
> Some facts to better understand these definitions:
> - The content that one would think of as being within the [live range](#55-interface-range) consists of all [contained](#55-interface-range) [nodes](#42-node-tree), plus possibly some of the contents of the [start node](#53-interface-abstractrange) and [end node](#53-interface-abstractrange) if those are [`CharacterData`](#410-interface-characterdata) [nodes](#42-node-tree).
> - The [nodes](#42-node-tree) that are contained in a [live range](#55-interface-range) will generally not be contiguous, because the [parent](#11-trees) of a [contained](#55-interface-range) [node](#42-node-tree) will not always be [contained](#55-interface-range).
> - However, the [descendants](#11-trees) of a [contained](#55-interface-range) [node](#42-node-tree) are [contained](#55-interface-range), and if two [siblings](#11-trees) are [contained](#55-interface-range), so are any [siblings](#11-trees) that lie between them.
> - The [start node](#53-interface-abstractrange) and [end node](#53-interface-abstractrange) of a [live range](#55-interface-range) are never [contained](#55-interface-range) within it.
> - The first [contained](#55-interface-range) [node](#42-node-tree) (if there are any) will always be after the [start node](#53-interface-abstractrange), and the last [contained](#55-interface-range) [node](#42-node-tree) will always be equal to or before the [end node](#53-interface-abstractrange)’s last [descendant](#11-trees).
> - There exists a [partially contained](#55-interface-range) [node](#42-node-tree) if and only if the [start node](#53-interface-abstractrange) and [end node](#53-interface-abstractrange) are different.
> - The [`commonAncestorContainer`](#55-interface-range) attribute value is neither [contained](#55-interface-range) nor [partially contained](#55-interface-range).
> - If the [start node](#53-interface-abstractrange) is an [ancestor](#11-trees) of the [end node](#53-interface-abstractrange), the common [inclusive ancestor](#11-trees) will be the [start node](#53-interface-abstractrange). Exactly one of its [children](#11-trees) will be [partially contained](#55-interface-range), and a [child](#11-trees) will be [contained](#55-interface-range) if and only if it [precedes](#11-trees) the [partially contained](#55-interface-range) [child](#11-trees). If the [end node](#53-interface-abstractrange) is an [ancestor](#11-trees) of the [start node](#53-interface-abstractrange), the opposite holds.
> - If the [start node](#53-interface-abstractrange) is not an [inclusive ancestor](#11-trees) of the [end node](#53-interface-abstractrange), nor vice versa, the common [inclusive ancestor](#11-trees) will be distinct from both of them. Exactly two of its [children](#11-trees) will be [partially contained](#55-interface-range), and a [child](#11-trees) will be contained if and only if it lies between those two.

The live range pre-remove steps given a [node](#42-node-tree) node, are:
1. Let parent be node’s [parent](#11-trees).
2. [Assert](infra-spec-whatwg-org.md#310-assertions): parent is non-null.
3. Let index be node’s [index](#11-trees).
4. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is an [inclusive descendant](#11-trees) of node, set its [start](#53-interface-abstractrange) to (parent, index).
5. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is an [inclusive descendant](#11-trees) of node, set its [end](#53-interface-abstractrange) to (parent, index).
6. For each [live range](#55-interface-range) whose [start node](#53-interface-abstractrange) is parent and [start offset](#53-interface-abstractrange) is greater than index, decrease its [start offset](#53-interface-abstractrange) by 1.
7. For each [live range](#55-interface-range) whose [end node](#53-interface-abstractrange) is parent and [end offset](#53-interface-abstractrange) is greater than index, decrease its [end offset](#53-interface-abstractrange) by 1.

---

`range = new Range()`

Returns a new [live range](#55-interface-range).

The `new Range()` constructor steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [start](#53-interface-abstractrange) and [end](#53-interface-abstractrange) to ([current global object](html-spec-whatwg-org.md#81333-current)’s [associated `Document`](html-spec-whatwg-org.md#722-the-window-object), 0).

---

container = range . [`commonAncestorContainer`](#55-interface-range)

Returns the [node](#42-node-tree), furthest away from the [document](#45-interface-document), that is an [ancestor](#11-trees) of both range’s [start node](#53-interface-abstractrange) and [end node](#53-interface-abstractrange).

To get the common ancestor of a [live range](#55-interface-range) range:
1. Let container be range’s [start node](#53-interface-abstractrange).
2. While container is not an [inclusive ancestor](#11-trees) of range’s [end node](#53-interface-abstractrange): set container to container’s [parent](#11-trees).
3. Return container.

The `commonAncestorContainer` getter steps are to return the result of [getting the common ancestor](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this).

---

To set the start or end of a range to a [boundary point](#52-boundary-points) (node, offset):
1. If node is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If offset is greater than node’s [length](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`IndexSizeError`](https://webidl.spec.whatwg.org/#indexsizeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let boundaryPoint be the [boundary point](#52-boundary-points) (node, offset).
4. If these steps were invoked as "set the start"
   1. If range’s [root](#55-interface-range) is not node’s [root](#11-trees) or boundaryPoint is [after](#52-boundary-points) range’s [end](#53-interface-abstractrange), then set range’s [end](#53-interface-abstractrange) to boundaryPoint.
   2. Set range’s [start](#53-interface-abstractrange) to boundaryPoint.

   If these steps were invoked as "set the end"
   1. If range’s [root](#55-interface-range) is not node’s [root](#11-trees) or boundaryPoint is [before](#52-boundary-points) range’s [start](#53-interface-abstractrange), then set range’s [start](#53-interface-abstractrange) to boundaryPoint.
   2. Set range’s [end](#53-interface-abstractrange) to boundaryPoint.

The `setStart(node, offset)` method steps are to [set the start](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this) to [boundary point](#52-boundary-points) (node, offset).

The `setEnd(node, offset)` method steps are to [set the end](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this) to [boundary point](#52-boundary-points) (node, offset).

The `setStartBefore(node)` method steps are:
1. Let parent be node’s [parent](#11-trees).
2. If parent is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. [Set the start](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this) to [boundary point](#52-boundary-points) (parent, node’s [index](#11-trees)).

The `setStartAfter(node)` method steps are:
1. Let parent be node’s [parent](#11-trees).
2. If parent is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. [Set the start](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this) to [boundary point](#52-boundary-points) (parent, node’s [index](#11-trees) plus 1).

The `setEndBefore(node)` method steps are:
1. Let parent be node’s [parent](#11-trees).
2. If parent is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. [Set the end](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this) to [boundary point](#52-boundary-points) (parent, node’s [index](#11-trees)).

The `setEndAfter(node)` method steps are:
1. Let parent be node’s [parent](#11-trees).
2. If parent is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. [Set the end](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this) to [boundary point](#52-boundary-points) (parent, node’s [index](#11-trees) plus 1).

The `collapse(toStart)` method steps are to, if toStart is true, set [end](#53-interface-abstractrange) to [start](#53-interface-abstractrange); otherwise set [start](#53-interface-abstractrange) to [end](#53-interface-abstractrange).

To select a [node](#42-node-tree) node within a [range](#53-interface-abstractrange) range:
1. Let parent be node’s [parent](#11-trees).
2. If parent is null, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let index be node’s [index](#11-trees).
4. Set range’s [start](#53-interface-abstractrange) to [boundary point](#52-boundary-points) (parent, index).
5. Set range’s [end](#53-interface-abstractrange) to [boundary point](#52-boundary-points) (parent, index plus 1).

The `selectNode(node)` method steps are to [select](#55-interface-range) node within [this](https://webidl.spec.whatwg.org/#this).

The `selectNodeContents(node)` method steps are:
1. If node is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Let length be the [length](#42-node-tree) of node.
3. Set [start](#53-interface-abstractrange) to the [boundary point](#52-boundary-points) (node, 0).
4. Set [end](#53-interface-abstractrange) to the [boundary point](#52-boundary-points) (node, length).

---

The `compareBoundaryPoints(how, sourceRange)` method steps are:
1. If how is not one of
   - [`START_TO_START`](#55-interface-range),
   - [`START_TO_END`](#55-interface-range),
   - [`END_TO_END`](#55-interface-range), and
   - [`END_TO_START`](#55-interface-range),

   then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`NotSupportedError`](https://webidl.spec.whatwg.org/#notsupportederror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

2. If [this](https://webidl.spec.whatwg.org/#this)’s [root](#55-interface-range) is not sourceRange’s [root](#55-interface-range), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`WrongDocumentError`](https://webidl.spec.whatwg.org/#wrongdocumenterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. Let thisPoint and sourcePoint be null.
4. Switch on how:

   [`START_TO_START`](#55-interface-range):

   Set thisPoint to [this](https://webidl.spec.whatwg.org/#this)’s [start](#53-interface-abstractrange) and sourcePoint to sourceRange’s [start](#53-interface-abstractrange).

   [`START_TO_END`](#55-interface-range):

   Set thisPoint to [this](https://webidl.spec.whatwg.org/#this)’s [end](#53-interface-abstractrange) and sourcePoint to sourceRange’s [start](#53-interface-abstractrange).

   [`END_TO_END`](#55-interface-range):

   Set thisPoint to [this](https://webidl.spec.whatwg.org/#this)’s [end](#53-interface-abstractrange) and sourcePoint to sourceRange’s [end](#53-interface-abstractrange).

   [`END_TO_START`](#55-interface-range):

   Set thisPoint to [this](https://webidl.spec.whatwg.org/#this)’s [start](#53-interface-abstractrange) and sourcePoint to sourceRange’s [end](#53-interface-abstractrange).

5. Switch on the [position](#52-boundary-points) of thisPoint relative to sourcePoint:

   [before](#52-boundary-points)

   Return −1.

   [equal](#52-boundary-points)

   Return 0.

   [after](#52-boundary-points)

   Return 1.

The `deleteContents()` method steps are:
1. If [this](https://webidl.spec.whatwg.org/#this) is [collapsed](#53-interface-abstractrange), then return.
2. Let originalStartNode, originalStartOffset, originalEndNode, and originalEndOffset be [this](https://webidl.spec.whatwg.org/#this)’s [start node](#53-interface-abstractrange), [start offset](#53-interface-abstractrange), [end node](#53-interface-abstractrange), and [end offset](#53-interface-abstractrange), respectively.
3. If originalStartNode is originalEndNode and it is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):
   1. [Replace data](#410-interface-characterdata) of originalStartNode with originalStartOffset, originalEndOffset − originalStartOffset, and the empty string.
   2. Return.
4. Let nodesToRemove be a list of all the [nodes](#42-node-tree) that are [contained](#55-interface-range) in [this](https://webidl.spec.whatwg.org/#this), in [tree order](#11-trees), omitting any [node](#42-node-tree) whose [parent](#11-trees) is also [contained](#55-interface-range) in [this](https://webidl.spec.whatwg.org/#this).
5. Let newNode and newOffset be null.
6. If originalStartNode is an [inclusive ancestor](#11-trees) of originalEndNode, then set newNode to originalStartNode and newOffset to originalStartOffset.
7. Otherwise:
   1. Let referenceNode be originalStartNode.
   2. While referenceNode’s [parent](#11-trees) is non-null and is not an [inclusive ancestor](#11-trees) of originalEndNode: set referenceNode to its [parent](#11-trees).
   3. Set newNode to referenceNode’s [parent](#11-trees) and newOffset to referenceNode’s [index](#11-trees) + 1.

      > [!note]
      > If referenceNode’s [parent](#11-trees) were null, it would be the [root](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this). And then it would be an [inclusive ancestor](#11-trees) of originalEndNode and we could not reach this point.

8. Set [this](https://webidl.spec.whatwg.org/#this)’s [start](#53-interface-abstractrange) and [end](#53-interface-abstractrange) to (newNode, newOffset).
9. If originalStartNode is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree), then [replace data](#410-interface-characterdata) of originalStartNode with originalStartOffset, originalStartNode’s [length](#42-node-tree) − originalStartOffset, and the empty string.
10. For each node of nodesToRemove, in [tree order](#11-trees): [remove](#423-mutation-algorithms) node.
11. If originalEndNode is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree), then [replace data](#410-interface-characterdata) of originalEndNode with 0, originalEndOffset, and the empty string.

To extract a [live range](#55-interface-range) range:
1. Let fragment be the result of [creating a document fragment](#47-interface-documentfragment) given range’s [start node](#53-interface-abstractrange)’s [node document](#44-interface-node).
2. If range is [collapsed](#53-interface-abstractrange), then return fragment.
3. Let originalStartNode, originalStartOffset, originalEndNode, and originalEndOffset be range’s [start node](#53-interface-abstractrange), [start offset](#53-interface-abstractrange), [end node](#53-interface-abstractrange), and [end offset](#53-interface-abstractrange), respectively.
4. If originalStartNode is originalEndNode and it is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):
   1. Let clone be a [clone](#44-interface-node) of originalStartNode.
   2. Set clone’s [data](#410-interface-characterdata) to the result of [substringing data](#410-interface-characterdata) of originalStartNode with originalStartOffset and originalEndOffset − originalStartOffset.
   3. [Append](#423-mutation-algorithms) clone to fragment.
   4. [Replace data](#410-interface-characterdata) of originalStartNode with originalStartOffset, originalEndOffset − originalStartOffset, and the empty string.
   5. Return fragment.
5. Let commonAncestor be the result of [getting the common ancestor](#55-interface-range) of range.
6. Let firstPartiallyContainedChild be null.
7. If originalStartNode is not an [inclusive ancestor](#11-trees) of originalEndNode, then set firstPartiallyContainedChild to the first [child](#11-trees) of commonAncestor that is [partially contained](#55-interface-range) in range.
8. Let lastPartiallyContainedChild be null.
9. If originalEndNode is not an [inclusive ancestor](#11-trees) of originalStartNode, then set lastPartiallyContainedChild to the last [child](#11-trees) of commonAncestor that is [partially contained](#55-interface-range) in range.

   > [!note]
   > These variable assignments do actually always make sense. For instance, if originalStartNode is not an [inclusive ancestor](#11-trees) of originalEndNode, originalStartNode is itself [partially contained](#55-interface-range) in range, and so are all its [ancestors](#11-trees) up until a [child](#11-trees) of commonAncestor. commonAncestor cannot be originalStartNode, because it has to be an [inclusive ancestor](#11-trees) of originalEndNode. The other case is similar. Also, notice that the two [children](#11-trees) will never be equal if both are defined.

10. Let containedChildren be a list of all [children](#11-trees) of commonAncestor that are [contained](#55-interface-range) in range, in [tree order](#11-trees).
11. If any member of containedChildren is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

    > [!note]
    > We do not have to worry about the first or last partially contained node, because a [doctype](#46-interface-documenttype) can never be partially contained. It cannot be a boundary point of a range, and it cannot be the ancestor of anything.

12. Let newNode and newOffset be null.
13. If originalStartNode is an [inclusive ancestor](#11-trees) of originalEndNode, then set newNode to originalStartNode and newOffset to originalStartOffset.
14. Otherwise:
    1. Let referenceNode be originalStartNode.
    2. While referenceNode’s [parent](#11-trees) is non-null and is not an [inclusive ancestor](#11-trees) of originalEndNode: set referenceNode to its [parent](#11-trees).
    3. Set newNode to the [parent](#11-trees) of referenceNode, and newOffset to referenceNode’s [index](#11-trees) + 1.

       > [!note]
       > If referenceNode’s [parent](#11-trees) is null, it would be the [root](#55-interface-range) of range. And then it would be an [inclusive ancestor](#11-trees) of originalEndNode and we could not reach this point.

15. Set range’s [start](#53-interface-abstractrange) and [end](#53-interface-abstractrange) to (newNode, newOffset).
16. If firstPartiallyContainedChild is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):

    > [!note]
    > In this case, firstPartiallyContainedChild is originalStartNode.
    1. Let clone be a [clone](#44-interface-node) of originalStartNode.
    2. Set the [data](#410-interface-characterdata) of clone to the result of [substringing data](#410-interface-characterdata) of originalStartNode with originalStartOffset and originalStartNode’s [length](#42-node-tree) − originalStartOffset.
    3. [Append](#423-mutation-algorithms) clone to fragment.
    4. [Replace data](#410-interface-characterdata) of originalStartNode with originalStartOffset, originalStartNode’s [length](#42-node-tree) − originalStartOffset, and the empty string.

17. Otherwise, if firstPartiallyContainedChild is non-null:
    1. Let clone be a [clone](#44-interface-node) of firstPartiallyContainedChild.
    2. [Append](#423-mutation-algorithms) clone to fragment.
    3. Let subrange be a new [live range](#55-interface-range) whose [start](#53-interface-abstractrange) is (originalStartNode, originalStartOffset) and whose [end](#53-interface-abstractrange) is (firstPartiallyContainedChild, firstPartiallyContainedChild’s [length](#42-node-tree)).
    4. Let subfragment be the result of [extracting](#55-interface-range) subrange.
    5. [Append](#423-mutation-algorithms) subfragment to clone.
18. For each contained child of containedChildren: [append](#423-mutation-algorithms) contained child to fragment.
19. If lastPartiallyContainedChild is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):

    > [!note]
    > In this case, lastPartiallyContainedChild is originalEndNode.
    1. Let clone be a [clone](#44-interface-node) of originalEndNode.
    2. Set clone’s [data](#410-interface-characterdata) to the result of [substringing data](#410-interface-characterdata) of originalEndNode with 0 and originalEndOffset.
    3. [Append](#423-mutation-algorithms) clone to fragment.
    4. [Replace data](#410-interface-characterdata) of originalEndNode with 0, originalEndOffset, and the empty string.

20. Otherwise, if lastPartiallyContainedChild is non-null:
    1. Let clone be a [clone](#44-interface-node) of lastPartiallyContainedChild.
    2. [Append](#423-mutation-algorithms) clone to fragment.
    3. Let subrange be a new [live range](#55-interface-range) whose [start](#53-interface-abstractrange) is (lastPartiallyContainedChild, 0) and whose [end](#53-interface-abstractrange) is (originalEndNode, originalEndOffset).
    4. Let subfragment be the result of [extracting](#55-interface-range) subrange.
    5. [Append](#423-mutation-algorithms) subfragment to clone.
21. Return fragment.

The `extractContents()` method steps are to return the result of [extracting](#55-interface-range) [this](https://webidl.spec.whatwg.org/#this).

To clone the contents of a [live range](#55-interface-range) range:
1. Let fragment be the result of [creating a document fragment](#47-interface-documentfragment) given range’s [start node](#53-interface-abstractrange)’s [node document](#44-interface-node).
2. If range is [collapsed](#53-interface-abstractrange), then return fragment.
3. Let originalStartNode, originalStartOffset, originalEndNode, and originalEndOffset be range’s [start node](#53-interface-abstractrange), [start offset](#53-interface-abstractrange), [end node](#53-interface-abstractrange), and [end offset](#53-interface-abstractrange), respectively.
4. If originalStartNode is originalEndNode and it is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):
   1. Let clone be a [clone](#44-interface-node) of originalStartNode.
   2. Set clone’s [data](#410-interface-characterdata) to the result of [substringing data](#410-interface-characterdata) of originalStartNode with originalStartOffset and originalEndOffset − originalStartOffset.
   3. [Append](#423-mutation-algorithms) clone to fragment.
   4. Return fragment.
5. Let commonAncestor be the result of [getting the common ancestor](#55-interface-range) of range.
6. Let firstPartiallyContainedChild be null.
7. If originalStartNode is not an [inclusive ancestor](#11-trees) of originalEndNode, then set firstPartiallyContainedChild to the first [child](#11-trees) of commonAncestor that is [partially contained](#55-interface-range) in range.
8. Let lastPartiallyContainedChild be null.
9. If originalEndNode is not an [inclusive ancestor](#11-trees) of originalStartNode, then set lastPartiallyContainedChild to the last [child](#11-trees) of commonAncestor that is [partially contained](#55-interface-range) in range.

   > [!note]
   > These variable assignments do actually always make sense. For instance, if originalStartNode is not an [inclusive ancestor](#11-trees) of originalEndNode, originalStartNode is itself [partially contained](#55-interface-range) in range, and so are all its [ancestors](#11-trees) up until a [child](#11-trees) of commonAncestor. commonAncestor cannot be originalStartNode, because it has to be an [inclusive ancestor](#11-trees) of originalEndNode. The other case is similar. Also, notice that the two [children](#11-trees) will never be equal if both are defined.

10. Let containedChildren be a list of all [children](#11-trees) of commonAncestor that are [contained](#55-interface-range) in range, in [tree order](#11-trees).
11. If any member of containedChildren is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

    > [!note]
    > We do not have to worry about the first or last partially contained node, because a [doctype](#46-interface-documenttype) can never be partially contained. It cannot be a boundary point of a range, and it cannot be the ancestor of anything.

12. If firstPartiallyContainedChild is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):

    > [!note]
    > In this case, firstPartiallyContainedChild is originalStartNode.
    1. Let clone be a [clone](#44-interface-node) of originalStartNode.
    2. Set the [data](#410-interface-characterdata) of clone to the result of [substringing data](#410-interface-characterdata) of originalStartNode with originalStartOffset and originalStartNode’s [length](#42-node-tree) − originalStartOffset.
    3. [Append](#423-mutation-algorithms) clone to fragment.

13. Otherwise, if firstPartiallyContainedChild is non-null:
    1. Let clone be a [clone](#44-interface-node) of firstPartiallyContainedChild.
    2. [Append](#423-mutation-algorithms) clone to fragment.
    3. Let subrange be a new [live range](#55-interface-range) whose [start](#53-interface-abstractrange) is (originalStartNode, originalStartOffset) and whose [end](#53-interface-abstractrange) is (firstPartiallyContainedChild, firstPartiallyContainedChild’s [length](#42-node-tree)).
    4. Let subfragment be the result of [cloning the contents](#55-interface-range) of subrange.
    5. [Append](#423-mutation-algorithms) subfragment to clone.
14. For each contained child of containedChildren:
    1. Let clone be a [clone](#44-interface-node) of contained child with [*subtree*](#44-interface-node) set to true.
    2. [Append](#423-mutation-algorithms) clone to fragment.
15. If lastPartiallyContainedChild is a [`CharacterData`](#410-interface-characterdata) [node](#42-node-tree):

    > [!note]
    > In this case, lastPartiallyContainedChild is originalEndNode.
    1. Let clone be a [clone](#44-interface-node) of originalEndNode.
    2. Set clone’s [data](#410-interface-characterdata) to the result of [substringing data](#410-interface-characterdata) of originalEndNode with 0 and originalEndOffset.
    3. [Append](#423-mutation-algorithms) clone to fragment.

16. Otherwise, if lastPartiallyContainedChild is non-null:
    1. Let clone be a [clone](#44-interface-node) of lastPartiallyContainedChild.
    2. [Append](#423-mutation-algorithms) clone to fragment.
    3. Let subrange be a new [live range](#55-interface-range) whose [start](#53-interface-abstractrange) is (lastPartiallyContainedChild, 0) and whose [end](#53-interface-abstractrange) is (originalEndNode, originalEndOffset).
    4. Let subfragment be the result of [cloning the contents](#55-interface-range) of subrange.
    5. [Append](#423-mutation-algorithms) subfragment to clone.
17. Return fragment.

The `cloneContents()` method steps are to return the result of [cloning the contents](#55-interface-range) of [this](https://webidl.spec.whatwg.org/#this).

To insert a [node](#42-node-tree) node into a [live range](#55-interface-range) range:
1. If range’s [start node](#53-interface-abstractrange) is a [`ProcessingInstruction`](#413-interface-processinginstruction) or [`Comment`](#414-interface-comment) [node](#42-node-tree), is a [`Text`](#411-interface-text) [node](#42-node-tree) whose [parent](#11-trees) is null, or is node, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`HierarchyRequestError`](https://webidl.spec.whatwg.org/#hierarchyrequesterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Let referenceNode be null.
3. If range’s [start node](#53-interface-abstractrange) is a [`Text`](#411-interface-text) [node](#42-node-tree), then set referenceNode to that [`Text`](#411-interface-text) [node](#42-node-tree).
4. Otherwise, set referenceNode to the [child](#11-trees) of range’s [start node](#53-interface-abstractrange) whose [index](#11-trees) is range’s [start offset](#53-interface-abstractrange) if there is such a [child](#11-trees); otherwise null.
5. Let parent be range’s [start node](#53-interface-abstractrange) if referenceNode is null; otherwise referenceNode’s [parent](#11-trees).
6. [Ensure pre-insert validity](#423-mutation-algorithms) given node, parent, referenceNode, and « ».
7. If range’s [start node](#53-interface-abstractrange) is a [`Text`](#411-interface-text) [node](#42-node-tree), then set referenceNode to the result of [splitting](#411-interface-text) it with offset range’s [start offset](#53-interface-abstractrange).
8. If node is referenceNode, then set referenceNode to its [next sibling](#11-trees).
9. If node’s [parent](#11-trees) is non-null, then [remove](#423-mutation-algorithms) node.
10. Let newOffset be parent’s [length](#42-node-tree) if referenceNode is null; otherwise referenceNode’s [index](#11-trees).
11. Increase newOffset by node’s [length](#42-node-tree) if node is a [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree); otherwise 1.
12. [Pre-insert](#423-mutation-algorithms) node into parent before referenceNode.
13. If range is [collapsed](#53-interface-abstractrange), then set range’s [end](#53-interface-abstractrange) to (parent, newOffset).

The `insertNode(node)` method steps are to [insert](#55-interface-range) node into [this](https://webidl.spec.whatwg.org/#this).

The `surroundContents(newParent)` method steps are:
1. If a non-[`Text`](#411-interface-text) [node](#42-node-tree) is [partially contained](#55-interface-range) in [this](https://webidl.spec.whatwg.org/#this), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidStateError`](https://webidl.spec.whatwg.org/#invalidstateerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If newParent is a [`Document`](#45-interface-document), [`DocumentType`](#46-interface-documenttype), or [`DocumentFragment`](#47-interface-documentfragment) [node](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).

   > [!note]
   > For historical reasons [`CharacterData`](#410-interface-characterdata) [nodes](#42-node-tree) are not checked here and end up throwing later on as a side effect.

3. Let fragment be the result of [extracting](#55-interface-range) [this](https://webidl.spec.whatwg.org/#this).
4. If newParent has [children](#11-trees), then [replace all](#423-mutation-algorithms) with null within newParent.
5. [Insert](#55-interface-range) newParent into [this](https://webidl.spec.whatwg.org/#this).
6. [Append](#423-mutation-algorithms) fragment to newParent.
7. [Select](#55-interface-range) newParent within [this](https://webidl.spec.whatwg.org/#this).

The `cloneRange()` method steps are to return a new [live range](#55-interface-range) with the same [start](#53-interface-abstractrange) and [end](#53-interface-abstractrange) as [this](https://webidl.spec.whatwg.org/#this).

The `detach()` method steps are to do nothing. Its functionality (disabling a [`Range`](#55-interface-range) object) was removed, but the method itself is preserved for compatibility.

---

position = range . [`comparePoint(node, offset)`](#55-interface-range)

Returns −1 if the point is before the range, 0 if the point is in the range, and 1 if the point is after the range.

intersects = range . [`intersectsNode(node)`](#55-interface-range)

Returns whether range intersects node.

The `isPointInRange(node, offset)` method steps are:
1. If node’s [root](#11-trees) is not [this](https://webidl.spec.whatwg.org/#this)’s [root](#55-interface-range), then return false.
2. If node is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If offset is greater than node’s [length](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`IndexSizeError`](https://webidl.spec.whatwg.org/#indexsizeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. If (node, offset) is [before](#52-boundary-points) [start](#53-interface-abstractrange) or [after](#52-boundary-points) [end](#53-interface-abstractrange), then return false.
5. Return true.

The `comparePoint(node, offset)` method steps are:
1. If node’s [root](#11-trees) is not [this](https://webidl.spec.whatwg.org/#this)’s [root](#55-interface-range), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`WrongDocumentError`](https://webidl.spec.whatwg.org/#wrongdocumenterror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If node is a [doctype](#46-interface-documenttype), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidNodeTypeError`](https://webidl.spec.whatwg.org/#invalidnodetypeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If offset is greater than node’s [length](#42-node-tree), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`IndexSizeError`](https://webidl.spec.whatwg.org/#indexsizeerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
4. If (node, offset) is [before](#52-boundary-points) [start](#53-interface-abstractrange), then return −1.
5. If (node, offset) is [after](#52-boundary-points) [end](#53-interface-abstractrange), then return 1.
6. Return 0.

---

The `intersectsNode(node)` method steps are:
1. If node’s [root](#11-trees) is not [this](https://webidl.spec.whatwg.org/#this)’s [root](#55-interface-range), then return false.
2. Let parent be node’s [parent](#11-trees).
3. If parent is null, then return true.
4. Let offset be node’s [index](#11-trees).
5. If (parent, offset) is [before](#52-boundary-points) [end](#53-interface-abstractrange) and (parent, offset + 1) is [after](#52-boundary-points) [start](#53-interface-abstractrange), then return true.
6. Return false.

---

The stringification behavior must run these steps:
1. Let string be the empty string.
2. If [this](https://webidl.spec.whatwg.org/#this)’s [start node](#53-interface-abstractrange) is [this](https://webidl.spec.whatwg.org/#this)’s [end node](#53-interface-abstractrange) and it is a [`Text`](#411-interface-text) [node](#42-node-tree), then return the substring of that [`Text`](#411-interface-text) [node](#42-node-tree)’s [data](#410-interface-characterdata) beginning at [this](https://webidl.spec.whatwg.org/#this)’s [start offset](#53-interface-abstractrange) and ending at [this](https://webidl.spec.whatwg.org/#this)’s [end offset](#53-interface-abstractrange).
3. If [this](https://webidl.spec.whatwg.org/#this)’s [start node](#53-interface-abstractrange) is a [`Text`](#411-interface-text) [node](#42-node-tree), then append the substring of that [node](#42-node-tree)’s [data](#410-interface-characterdata) from [this](https://webidl.spec.whatwg.org/#this)’s [start offset](#53-interface-abstractrange) until the end to string.
4. Append the [concatenation](infra-spec-whatwg-org.md#47-strings) of the [data](#410-interface-characterdata) of all [`Text`](#411-interface-text) [nodes](#42-node-tree) that are [contained](#55-interface-range) in [this](https://webidl.spec.whatwg.org/#this), in [tree order](#11-trees), to string.
5. If [this](https://webidl.spec.whatwg.org/#this)’s [end node](#53-interface-abstractrange) is a [`Text`](#411-interface-text) [node](#42-node-tree), then append the substring of that [node](#42-node-tree)’s [data](#410-interface-characterdata) from its start until [this](https://webidl.spec.whatwg.org/#this)’s [end offset](#53-interface-abstractrange) to string.
6. Return string.

---

> [!note]
> The [`createContextualFragment()`](https://w3c.github.io/DOM-Parsing/#dom-range-createcontextualfragment), [`getClientRects()`](https://drafts.csswg.org/cssom-view-1/#dom-range-getclientrects), and [`getBoundingClientRect()`](https://drafts.csswg.org/cssom-view-1/#dom-range-getboundingclientrect) methods are defined in other specifications. [\[DOM-Parsing\]](#non-normative-references) [\[CSSOM-VIEW\]](#non-normative-references)

## 6. Traversal

[`NodeIterator`](#61-interface-nodeiterator) and [`TreeWalker`](#62-interface-treewalker) objects can be used to filter and traverse [node](#42-node-tree) [trees](#11-trees).

Each [`NodeIterator`](#61-interface-nodeiterator) and [`TreeWalker`](#62-interface-treewalker) object has an associated boolean is active to avoid recursive invocations. It is initially false.

Each [`NodeIterator`](#61-interface-nodeiterator) and [`TreeWalker`](#62-interface-treewalker) object also has an associated root (a [node](#42-node-tree)), a whatToShow (a bitmask), and a filter (a callback).

To filter a [node](#42-node-tree) node within a [`NodeIterator`](#61-interface-nodeiterator) or [`TreeWalker`](#62-interface-treewalker) object traverser:
1. If traverser’s [is active](#6-traversal) is true, then throw an "[`InvalidStateError`](https://webidl.spec.whatwg.org/#invalidstateerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. Let n be node’s [`nodeType`](#44-interface-node) attribute value − 1.
3. If the nth bit (where 0 is the least significant bit) of traverser’s [whatToShow](#6-traversal) is not set, then return [`FILTER_SKIP`](#63-interface-nodefilter).
4. If traverser’s [filter](#6-traversal) is null, then return [`FILTER_ACCEPT`](#63-interface-nodefilter).
5. Set traverser’s [is active](#6-traversal) to true.
6. Let result be the return value of [call a user object’s operation](https://webidl.spec.whatwg.org/#call-a-user-objects-operation) with traverser’s [filter](#6-traversal), "`acceptNode`", and « node ». If this throws an exception, then set traverser’s [is active](#6-traversal) to false and rethrow the exception.
7. Set traverser’s [is active](#6-traversal) to false.
8. Return result.

### 6.1. Interface [`NodeIterator`](#61-interface-nodeiterator)

```webidl
[Exposed=Window]
interface NodeIterator {
  [SameObject] readonly attribute Node root;
  readonly attribute Node referenceNode;
  readonly attribute boolean pointerBeforeReferenceNode;
  readonly attribute unsigned long whatToShow;
  readonly attribute NodeFilter? filter;

  Node? nextNode();
  Node? previousNode();

  undefined detach();
};

```

> [!note]
> [`NodeIterator`](#61-interface-nodeiterator) objects can be created using the [`createNodeIterator()`](#45-interface-document) method on [`Document`](#45-interface-document) objects.

Each [`NodeIterator`](#61-interface-nodeiterator) object has an associated iterator collection, which is a [collection](#4210-old-style-collections-nodelist-and-htmlcollection) rooted at the [`NodeIterator`](#61-interface-nodeiterator) object’s [root](#6-traversal), whose filter matches any [node](#42-node-tree).

A node pointer is a [tuple](infra-spec-whatwg-org.md#531-tuples) consisting of a node (a [node](#42-node-tree)) and a pointer before (a boolean).

Each [`NodeIterator`](#61-interface-nodeiterator) object also has an associated reference (a [node pointer](#61-interface-nodeiterator)) and candidate reference (null or a [node pointer](#61-interface-nodeiterator), and initially null).

> [!note]
> As mentioned earlier, [`NodeIterator`](#61-interface-nodeiterator) objects have an associated [is active](#6-traversal), [root](#6-traversal), [whatToShow](#6-traversal), and [filter](#6-traversal) as well.

The `NodeIterator` pre-remove steps given a [`NodeIterator`](#61-interface-nodeiterator) object nodeIterator and [node](#42-node-tree) toBeRemovedNode, are:
1. Set nodeIterator’s [reference](#61-interface-nodeiterator) to the result of [adjusting a node pointer](#61-interface-nodeiterator) given nodeIterator’s [reference](#61-interface-nodeiterator), nodeIterator, and toBeRemovedNode.
2. If nodeIterator’s [candidate reference](#61-interface-nodeiterator) is non-null, then set nodeIterator’s [candidate reference](#61-interface-nodeiterator) to the result of [adjusting a node pointer](#61-interface-nodeiterator) given nodeIterator’s [candidate reference](#61-interface-nodeiterator), nodeIterator, and toBeRemovedNode.

---

To adjust a node pointer given a [node pointer](#61-interface-nodeiterator) nodePointer, a [`NodeIterator`](#61-interface-nodeiterator) object nodeIterator, and a [node](#42-node-tree) toBeRemovedNode, perform the following steps. They return a [node pointer](#61-interface-nodeiterator).
1. If toBeRemovedNode is not an [inclusive ancestor](#11-trees) of nodePointer’s [node](#61-interface-nodeiterator), or toBeRemovedNode is an [inclusive ancestor](#11-trees) of nodeIterator’s [root](#6-traversal), then return nodePointer.
2. If nodePointer’s [pointer before](#61-interface-nodeiterator) is true:
   1. Let next be toBeRemovedNode’s first [following](#11-trees) [node](#42-node-tree) that is an [inclusive descendant](#11-trees) of nodeIterator’s [root](#6-traversal) and is not an [inclusive descendant](#11-trees) of toBeRemovedNode, if there is such a [node](#42-node-tree); otherwise null.
   2. If next is non-null, then return (next, true).
3. Let newNode be toBeRemovedNode’s [parent](#11-trees), if toBeRemovedNode’s [previous sibling](#11-trees) is null; otherwise the [inclusive descendant](#11-trees) of toBeRemovedNode’s [previous sibling](#11-trees) that appears last in [tree order](#11-trees).
4. Return (newNode, false).

---

The `root` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [root](#6-traversal).

The `referenceNode` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [reference](#61-interface-nodeiterator)’s [node](#61-interface-nodeiterator).

The `pointerBeforeReferenceNode` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [reference](#61-interface-nodeiterator)’s [pointer before](#61-interface-nodeiterator).

The `whatToShow` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [whatToShow](#6-traversal).

The `filter` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [filter](#6-traversal).

To traverse, given a [`NodeIterator`](#61-interface-nodeiterator) object iterator and "`next`" or "`previous`" type:
1. Set iterator’s [candidate reference](#61-interface-nodeiterator) to iterator’s [reference](#61-interface-nodeiterator).
2. Let result be null.
3. While true:
   1. If type is "`next`":
      1. If iterator’s [candidate reference](#61-interface-nodeiterator)’s [pointer before](#61-interface-nodeiterator) is false:
         1. Let following be the first [node](#42-node-tree) [following](#11-trees) iterator’s [candidate reference](#61-interface-nodeiterator)’s [node](#61-interface-nodeiterator) in iterator’s [iterator collection](#61-interface-nodeiterator). If there is no such [node](#42-node-tree), then [break](infra-spec-whatwg-org.md#39-iteration).
         2. Set iterator’s [candidate reference](#61-interface-nodeiterator) to (following, false).
      2. Otherwise, set iterator’s [candidate reference](#61-interface-nodeiterator) to (iterator’s [candidate reference](#61-interface-nodeiterator)’s [node](#61-interface-nodeiterator), false).
   2. Otherwise:
      1. If iterator’s [candidate reference](#61-interface-nodeiterator)’s [pointer before](#61-interface-nodeiterator) is true:
         1. Let preceding be the first [node](#42-node-tree) [preceding](#11-trees) iterator’s [candidate reference](#61-interface-nodeiterator)’s [node](#61-interface-nodeiterator) in iterator’s [iterator collection](#61-interface-nodeiterator). If there is no such [node](#42-node-tree), then [break](infra-spec-whatwg-org.md#39-iteration).
         2. Set iterator’s [candidate reference](#61-interface-nodeiterator) to (preceding, true).
      2. Otherwise, set iterator’s [candidate reference](#61-interface-nodeiterator) to (iterator’s [candidate reference](#61-interface-nodeiterator)’s [node](#61-interface-nodeiterator), true).
   3. Let node be iterator’s [candidate reference](#61-interface-nodeiterator)’s [node](#61-interface-nodeiterator).
   4. Let filterResult be the result of [filtering](#6-traversal) node within iterator. If this throws an exception, then set iterator’s [candidate reference](#61-interface-nodeiterator) to null and rethrow that exception.
   5. If filterResult is [`FILTER_ACCEPT`](#63-interface-nodefilter):
      1. Set iterator’s [reference](#61-interface-nodeiterator) to iterator’s [candidate reference](#61-interface-nodeiterator).
      2. Set result to node.
      3. [Break](infra-spec-whatwg-org.md#39-iteration).
4. Set iterator’s [candidate reference](#61-interface-nodeiterator) to null.
5. Return result.

The `nextNode()` method steps are to return the result of [traversing](#61-interface-nodeiterator) with [this](https://webidl.spec.whatwg.org/#this) and "`next`".

The `previousNode()` method steps are to return the result of [traversing](#61-interface-nodeiterator) with [this](https://webidl.spec.whatwg.org/#this) and "`previous`".

The `detach()` method steps are to do nothing. Its functionality (disabling a [`NodeIterator`](#61-interface-nodeiterator) object) was removed, but the method itself is preserved for compatibility.

### 6.2. Interface [`TreeWalker`](#62-interface-treewalker)

```webidl
[Exposed=Window]
interface TreeWalker {
  [SameObject] readonly attribute Node root;
  readonly attribute unsigned long whatToShow;
  readonly attribute NodeFilter? filter;
           attribute Node currentNode;

  Node? parentNode();
  Node? firstChild();
  Node? lastChild();
  Node? previousSibling();
  Node? nextSibling();
  Node? previousNode();
  Node? nextNode();
};
```

> [!note]
> [`TreeWalker`](#62-interface-treewalker) objects can be created using the [`createTreeWalker()`](#45-interface-document) method on [`Document`](#45-interface-document) objects.

Each [`TreeWalker`](#62-interface-treewalker) object has an associated current (a [node](#42-node-tree)).

> [!note]
> As mentioned earlier [`TreeWalker`](#62-interface-treewalker) objects have an associated [root](#6-traversal), [whatToShow](#6-traversal), and [filter](#6-traversal) as well.

The `root` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [root](#6-traversal).

The `whatToShow` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [whatToShow](#6-traversal).

The `filter` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [filter](#6-traversal).

The `currentNode` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker).

The [`currentNode`](#62-interface-treewalker) setter steps are to set [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker) to the given value.

---

The `parentNode()` method steps are:
1. Let node be [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker).
2. While node is non-null and is not [this](https://webidl.spec.whatwg.org/#this)’s [root](#6-traversal):
   1. Set node to node’s [parent](#11-trees).
   2. If node is non-null and [filtering](#6-traversal) node within [this](https://webidl.spec.whatwg.org/#this) returns [`FILTER_ACCEPT`](#63-interface-nodefilter), then set [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker) to node and return node.
3. Return null.

To traverse children, given a [`TreeWalker`](#62-interface-treewalker) object walker and "`first`" or "`last`" type:
1. Let node be walker’s [current](#62-interface-treewalker).
2. Set node to node’s [first child](#11-trees) if type is "`first`"; otherwise to node’s [last child](#11-trees).
3. While node is non-null:
   1. Let result be the result of [filtering](#6-traversal) node within walker.
   2. If result is [`FILTER_ACCEPT`](#63-interface-nodefilter), then set walker’s [current](#62-interface-treewalker) to node and return node.
   3. If result is [`FILTER_SKIP`](#63-interface-nodefilter):
      1. Let child be node’s [first child](#11-trees) if type is "`first`"; otherwise node’s [last child](#11-trees).
      2. If child is non-null, then set node to child and [continue](infra-spec-whatwg-org.md#39-iteration).
   4. While node is non-null:
      1. Let sibling be node’s [next sibling](#11-trees) if type is "`first`"; otherwise node’s [previous sibling](#11-trees).
      2. If sibling is non-null, then set node to sibling and [break](infra-spec-whatwg-org.md#39-iteration).
      3. Let parent be node’s [parent](#11-trees).
      4. If parent is null, walker’s [root](#6-traversal), or walker’s [current](#62-interface-treewalker), then return null.
      5. Set node to parent.
4. Return null.

The `firstChild()` method steps are to [traverse children](#62-interface-treewalker) with [this](https://webidl.spec.whatwg.org/#this) and "`first`".

The `lastChild()` method steps are to [traverse children](#62-interface-treewalker) with [this](https://webidl.spec.whatwg.org/#this) and "`last`".

To traverse siblings, given a [`TreeWalker`](#62-interface-treewalker) object walker and "`next`" or "`previous`" type:
1. Let node be walker’s [current](#62-interface-treewalker).
2. If node is [root](#6-traversal), then return null.
3. While true:
   1. Let sibling be node’s [next sibling](#11-trees) if type is "`next`"; otherwise node’s [previous sibling](#11-trees).
   2. While sibling is non-null:
      1. Set node to sibling.
      2. Let result be the result of [filtering](#6-traversal) node within walker.
      3. If result is [`FILTER_ACCEPT`](#63-interface-nodefilter), then set walker’s [current](#62-interface-treewalker) to node and return node.
      4. Set sibling to node’s [first child](#11-trees) if type is "`next`"; otherwise to node’s [last child](#11-trees).
      5. If result is [`FILTER_REJECT`](#63-interface-nodefilter) or sibling is null, then set sibling to node’s [next sibling](#11-trees) if type is "`next`"; otherwise to node’s [previous sibling](#11-trees).
   3. Set node to node’s [parent](#11-trees).
   4. If node is null or walker’s [root](#6-traversal), then return null.
   5. If the return value of [filtering](#6-traversal) node within walker is [`FILTER_ACCEPT`](#63-interface-nodefilter), then return null.

The `nextSibling()` method steps are to [traverse siblings](#62-interface-treewalker) with [this](https://webidl.spec.whatwg.org/#this) and "`next`".

The `previousSibling()` method steps are to [traverse siblings](#62-interface-treewalker) with [this](https://webidl.spec.whatwg.org/#this) and "`previous`".

The `previousNode()` method steps are:
1. Let node be [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker).
2. While node is not [this](https://webidl.spec.whatwg.org/#this)’s [root](#6-traversal):
   1. Let sibling be node’s [previous sibling](#11-trees).
   2. While sibling is non-null:
      1. Set node to sibling.
      2. Let result be the result of [filtering](#6-traversal) node within [this](https://webidl.spec.whatwg.org/#this).
      3. While result is not [`FILTER_REJECT`](#63-interface-nodefilter) and node has a [child](#11-trees):
         1. Set node to node’s [last child](#11-trees).
         2. Set result to the result of [filtering](#6-traversal) node within [this](https://webidl.spec.whatwg.org/#this).
      4. If result is [`FILTER_ACCEPT`](#63-interface-nodefilter), then set [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker) to node and return node.
      5. Set sibling to node’s [previous sibling](#11-trees).
   3. If node is [this](https://webidl.spec.whatwg.org/#this)’s [root](#6-traversal) or node’s [parent](#11-trees) is null, then return null.
   4. Set node to node’s [parent](#11-trees).
   5. If the return value of [filtering](#6-traversal) node within [this](https://webidl.spec.whatwg.org/#this) is [`FILTER_ACCEPT`](#63-interface-nodefilter), then set [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker) to node and return node.
3. Return null.

The `nextNode()` method steps are:
1. Let node be [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker).
2. Let result be [`FILTER_ACCEPT`](#63-interface-nodefilter).
3. While true:
   1. While result is not [`FILTER_REJECT`](#63-interface-nodefilter) and node has a [child](#11-trees):
      1. Set node to its [first child](#11-trees).
      2. Set result to the result of [filtering](#6-traversal) node within [this](https://webidl.spec.whatwg.org/#this).
      3. If result is [`FILTER_ACCEPT`](#63-interface-nodefilter), then set [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker) to node and return node.
   2. Let sibling be null.
   3. Let temporary be node.
   4. While temporary is non-null:
      1. If temporary is [this](https://webidl.spec.whatwg.org/#this)’s [root](#6-traversal), then return null.
      2. Set sibling to temporary’s [next sibling](#11-trees).
      3. If sibling is non-null, then [break](infra-spec-whatwg-org.md#39-iteration).
      4. Set temporary to temporary’s [parent](#11-trees).
   5. If sibling is null, then return null.
   6. Set node to sibling.
   7. Set result to the result of [filtering](#6-traversal) node within [this](https://webidl.spec.whatwg.org/#this).
   8. If result is [`FILTER_ACCEPT`](#63-interface-nodefilter), then set [this](https://webidl.spec.whatwg.org/#this)’s [current](#62-interface-treewalker) to node and return node.

### 6.3. Interface [`NodeFilter`](#63-interface-nodefilter)

```webidl
[Exposed=Window]
callback interface NodeFilter {
  // Constants for acceptNode()
  const unsigned short FILTER_ACCEPT = 1;
  const unsigned short FILTER_REJECT = 2;
  const unsigned short FILTER_SKIP = 3;

  // Constants for whatToShow
  const unsigned long SHOW_ALL = 0xFFFFFFFF;
  const unsigned long SHOW_ELEMENT = 0x1;
  const unsigned long SHOW_ATTRIBUTE = 0x2;
  const unsigned long SHOW_TEXT = 0x4;
  const unsigned long SHOW_CDATA_SECTION = 0x8;
  const unsigned long SHOW_ENTITY_REFERENCE = 0x10; // legacy
  const unsigned long SHOW_ENTITY = 0x20; // legacy
  const unsigned long SHOW_PROCESSING_INSTRUCTION = 0x40;
  const unsigned long SHOW_COMMENT = 0x80;
  const unsigned long SHOW_DOCUMENT = 0x100;
  const unsigned long SHOW_DOCUMENT_TYPE = 0x200;
  const unsigned long SHOW_DOCUMENT_FRAGMENT = 0x400;
  const unsigned long SHOW_NOTATION = 0x800; // legacy

  unsigned short acceptNode(Node node);
};

```

> [!note]
> [`NodeFilter`](#63-interface-nodefilter) objects can be used as [filter](#6-traversal) for [`NodeIterator`](#61-interface-nodeiterator) and [`TreeWalker`](#62-interface-treewalker) objects and also provide constants for their [whatToShow](#6-traversal) bitmask. A [`NodeFilter`](#63-interface-nodefilter) object is typically implemented as a JavaScript function.

These constants can be used as [filter](#6-traversal) return value:
- `FILTER_ACCEPT` (1);
- `FILTER_REJECT` (2);
- `FILTER_SKIP` (3).

These constants can be used for [whatToShow](#6-traversal):
- `SHOW_ALL` (4294967295, FFFFFFFF in hexadecimal);
- `SHOW_ELEMENT` (1);
- `SHOW_ATTRIBUTE` (2);
- `SHOW_TEXT` (4);
- `SHOW_CDATA_SECTION` (8);
- `SHOW_PROCESSING_INSTRUCTION` (64, 40 in hexadecimal);
- `SHOW_COMMENT` (128, 80 in hexadecimal);
- `SHOW_DOCUMENT` (256, 100 in hexadecimal);
- `SHOW_DOCUMENT_TYPE` (512, 200 in hexadecimal);
- `SHOW_DOCUMENT_FRAGMENT` (1024, 400 in hexadecimal).

## 7. Sets

> [!note]
> Yes, the name [`DOMTokenList`](#71-interface-domtokenlist) is an unfortunate legacy mishap.

### 7.1. Interface [`DOMTokenList`](#71-interface-domtokenlist)

```webidl
[Exposed=Window]
interface DOMTokenList {
  readonly attribute unsigned long length;
  getter DOMString? item(unsigned long index);
  boolean contains(DOMString token);
  [CEReactions] undefined add(DOMString... tokens);
  [CEReactions] undefined remove(DOMString... tokens);
  [CEReactions] boolean toggle(DOMString token, optional boolean force);
  [CEReactions] boolean replace(DOMString token, DOMString newToken);
  boolean supports(DOMString token);
  [CEReactions] stringifier attribute DOMString value;
  iterable<DOMString>;
};

```

A [`DOMTokenList`](#71-interface-domtokenlist) object has an associated token set (a [set](infra-spec-whatwg-org.md#513-sets)), which is initially empty.

A [`DOMTokenList`](#71-interface-domtokenlist) object also has an associated element (an [element](#49-interface-element)) and an attribute name (an [attribute](#492-interface-attr)’s [local name](#492-interface-attr)).

[Specifications](#1-infrastructure) may define supported tokens for a [`DOMTokenList`](#71-interface-domtokenlist)’s [element](#71-interface-domtokenlist) and [attribute name](#71-interface-domtokenlist).

A [`DOMTokenList`](#71-interface-domtokenlist) object set’s validation steps for a given token are:
1. If set’s [element](#71-interface-domtokenlist) and [attribute name](#71-interface-domtokenlist) does not define [supported tokens](#71-interface-domtokenlist), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a `TypeError`.
2. Let lowercaseToken be token, in [ASCII lowercase](infra-spec-whatwg-org.md#47-strings).
3. If lowercaseToken is present in the [supported tokens](#71-interface-domtokenlist) of set’s [element](#71-interface-domtokenlist) and [attribute name](#71-interface-domtokenlist), then return true.
4. Return false.

A [`DOMTokenList`](#71-interface-domtokenlist) object set’s update steps are:
1. If [get an attribute by namespace and local name](#49-interface-element) given null, set’s [attribute name](#71-interface-domtokenlist), and set’s [element](#71-interface-domtokenlist) returns null and set’s [token set](#71-interface-domtokenlist) is empty, then return.
2. [Set an attribute value](#49-interface-element) given set’s [element](#71-interface-domtokenlist), set’s [attribute name](#71-interface-domtokenlist), and the result of running the [ordered set serializer](#12-ordered-sets) for set’s [token set](#71-interface-domtokenlist).

A [`DOMTokenList`](#71-interface-domtokenlist) object set’s serialize steps are to return the result of running [get an attribute value](#49-interface-element) given set’s [element](#71-interface-domtokenlist) and set’s [attribute name](#71-interface-domtokenlist).

---

A [`DOMTokenList`](#71-interface-domtokenlist) object set has these [attribute change steps](#49-interface-element) for set’s [element](#71-interface-domtokenlist):
1. If localName is set’s [attribute name](#71-interface-domtokenlist), namespace is null, and value is null, then [empty](infra-spec-whatwg-org.md#51-lists) [token set](#71-interface-domtokenlist).
2. Otherwise, if localName is set’s [attribute name](#71-interface-domtokenlist) and namespace is null, then set set’s [token set](#71-interface-domtokenlist) to value, [parsed](#12-ordered-sets).

When a [`DOMTokenList`](#71-interface-domtokenlist) object set is created:
1. Let element be set’s [element](#71-interface-domtokenlist).
2. Let attributeName be set’s [attribute name](#71-interface-domtokenlist).
3. Let value be the result of [getting an attribute value](#49-interface-element) given element and attributeName.
4. Run the [attribute change steps](#49-interface-element) for element, attributeName, value, value, and null.

`` tokenlist . `length` ``

Returns the number of tokens.

`` tokenlist . `item(index)` ``

`tokenlist[index]`

Returns the token with index index.

`` tokenlist . `contains(token)` ``

Returns true if token is present; otherwise false.

`tokenlist . add(tokens…)`

Adds all arguments passed, except those already present.

Throws a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if one of the arguments is the empty string.

Throws an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if one of the arguments contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points).

`tokenlist . remove(tokens…)`

Removes arguments passed, if they are present.

Throws a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if one of the arguments is the empty string.

Throws an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if one of the arguments contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points).

`tokenlist . toggle(token [, force])`

If force is not given, "toggles" token, removing it if it’s present and adding it if it’s not present. If force is true, adds token (same as [`add()`](#71-interface-domtokenlist)). If force is false, removes token (same as [`remove()`](#71-interface-domtokenlist)).

Returns true if token is now present; otherwise false.

Throws a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if token is empty.

Throws an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if token contains any spaces.

`tokenlist . replace(token, newToken)`

Replaces token with newToken.

Returns true if token was replaced with newToken; otherwise false.

Throws a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if one of the arguments is the empty string.

Throws an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException) if one of the arguments contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points).

`tokenlist . supports(token)`

Returns true if token is in the associated attribute’s supported tokens. Returns false otherwise.

Throws a `TypeError` if the associated attribute has no supported tokens defined.

`` tokenlist . `value` ``

Returns the associated set as string.

Can be set, to change the associated attribute.

The `length` getter steps are to return [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist)’s [size](infra-spec-whatwg-org.md#51-lists).

The object’s [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices) are the numbers in the range zero to object’s [token set](#71-interface-domtokenlist)’s [size](infra-spec-whatwg-org.md#51-lists) − 1, unless [token set](#71-interface-domtokenlist) [is empty](infra-spec-whatwg-org.md#51-lists), in which case there are no [supported property indices](https://webidl.spec.whatwg.org/#dfn-supported-property-indices).

The `item(index)` method steps are:
1. If index is equal to or greater than [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist)’s [size](infra-spec-whatwg-org.md#51-lists), then return null.
2. Return [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist)\[index\].

The `contains(token)` method steps are to return true if [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist)\[token\] [exists](infra-spec-whatwg-org.md#51-lists); otherwise false.

The `add(tokens…)` method steps are:
1. [For each](infra-spec-whatwg-org.md#51-lists) token of tokens:
   1. If token is the empty string, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
   2. If token contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. [For each](infra-spec-whatwg-org.md#51-lists) token of tokens: [append](infra-spec-whatwg-org.md#513-sets) token to [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist).
3. Run the [update steps](#71-interface-domtokenlist).

The `remove(tokens…)` method steps are:
1. [For each](infra-spec-whatwg-org.md#51-lists) token of tokens:
   1. If token is the empty string, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
   2. If token contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. For each token of tokens: [remove](infra-spec-whatwg-org.md#51-lists) token from [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist).
3. Run the [update steps](#71-interface-domtokenlist).

The `toggle(token, force)` method steps are:
1. If token is the empty string, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If token contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist)\[token\] [exists](infra-spec-whatwg-org.md#51-lists):
   1. If force is either not given or is false, then [remove](infra-spec-whatwg-org.md#51-lists) token from [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist), run the [update steps](#71-interface-domtokenlist) and return false.
   2. Return true.
4. Otherwise, if force not given or is true, [append](infra-spec-whatwg-org.md#513-sets) token to [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist), run the [update steps](#71-interface-domtokenlist), and return true.
5. Return false.

> [!note]
> The [update steps](#71-interface-domtokenlist) are not always run for [`toggle()`](#71-interface-domtokenlist) for web compatibility.

The `replace(token, newToken)` method steps are:
1. If either token or newToken is the empty string, then [throw](https://webidl.spec.whatwg.org/#dfn-throw) a "[`SyntaxError`](https://webidl.spec.whatwg.org/#syntaxerror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
2. If either token or newToken contains any [ASCII whitespace](infra-spec-whatwg-org.md#46-code-points), then [throw](https://webidl.spec.whatwg.org/#dfn-throw) an "[`InvalidCharacterError`](https://webidl.spec.whatwg.org/#invalidcharactererror)" [`DOMException`](https://webidl.spec.whatwg.org/#idl-DOMException).
3. If [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist) does not [contain](infra-spec-whatwg-org.md#51-lists) token, then return false.
4. [Replace](infra-spec-whatwg-org.md#513-sets) token in [this](https://webidl.spec.whatwg.org/#this)’s [token set](#71-interface-domtokenlist) with newToken.
5. Run the [update steps](#71-interface-domtokenlist).
6. Return true.

> [!note]
> The [update steps](#71-interface-domtokenlist) are not always run for [`replace()`](#71-interface-domtokenlist) for web compatibility.

The `supports(token)` method steps are:
1. Let result be the return value of [validation steps](#71-interface-domtokenlist) called with token.
2. Return result.

The `value` getter steps are to return the result of running [this](https://webidl.spec.whatwg.org/#this)’s [serialize steps](#71-interface-domtokenlist).

The [`value`](#71-interface-domtokenlist) setter steps are to [set an attribute value](#49-interface-element) for [this](https://webidl.spec.whatwg.org/#this)’s [element](#71-interface-domtokenlist) using [this](https://webidl.spec.whatwg.org/#this)’s [attribute name](#71-interface-domtokenlist) and the given value.

## 8. XPath

> [!warning]
> DOM Level 3 XPath defined an API for evaluating XPath 1.0 expressions. These APIs are widely implemented, but have not been maintained. The interface definitions are maintained here so that they can be updated when Web IDL changes. Complete definitions of these APIs remain necessary and such work is tracked and can be contributed to in [whatwg/dom#67](https://github.com/whatwg/dom/issues/67). [\[DOM-Level-3-XPath\]](#non-normative-references) [\[XPath\]](#non-normative-references) [\[WEBIDL\]](#normative-references)

### 8.1. Interface [`XPathResult`](#81-interface-xpathresult)

```webidl
[Exposed=Window]
interface XPathResult {
  const unsigned short ANY_TYPE = 0;
  const unsigned short NUMBER_TYPE = 1;
  const unsigned short STRING_TYPE = 2;
  const unsigned short BOOLEAN_TYPE = 3;
  const unsigned short UNORDERED_NODE_ITERATOR_TYPE = 4;
  const unsigned short ORDERED_NODE_ITERATOR_TYPE = 5;
  const unsigned short UNORDERED_NODE_SNAPSHOT_TYPE = 6;
  const unsigned short ORDERED_NODE_SNAPSHOT_TYPE = 7;
  const unsigned short ANY_UNORDERED_NODE_TYPE = 8;
  const unsigned short FIRST_ORDERED_NODE_TYPE = 9;

  readonly attribute unsigned short resultType;
  readonly attribute unrestricted double numberValue;
  readonly attribute DOMString stringValue;
  readonly attribute boolean booleanValue;
  readonly attribute Node? singleNodeValue;
  readonly attribute boolean invalidIteratorState;
  readonly attribute unsigned long snapshotLength;

  Node? iterateNext();
  Node? snapshotItem(unsigned long index);
};

```

### 8.2. Interface [`XPathExpression`](#82-interface-xpathexpression)

```webidl
[Exposed=Window]
interface XPathExpression {
  // XPathResult.ANY_TYPE = 0
  XPathResult evaluate(Node contextNode, optional unsigned short type = 0, optional XPathResult? result = null);
};

```

### 8.3. Mixin [`XPathEvaluatorBase`](#83-mixin-xpathevaluatorbase)

```webidl
callback interface XPathNSResolver {
  DOMString? lookupNamespaceURI(DOMString? prefix);
};

interface mixin XPathEvaluatorBase {
  [NewObject] XPathExpression createExpression(DOMString expression, optional XPathNSResolver? resolver = null);
  Node createNSResolver(Node nodeResolver); // legacy
  // XPathResult.ANY_TYPE = 0
  XPathResult evaluate(DOMString expression, Node contextNode, optional XPathNSResolver? resolver = null, optional unsigned short type = 0, optional XPathResult? result = null);
};
Document includes XPathEvaluatorBase;

```

The `createNSResolver(nodeResolver)` method steps are to return nodeResolver.

> [!note]
> This method exists only for historical reasons.

### 8.4. Interface [`XPathEvaluator`](#84-interface-xpathevaluator)

```webidl
[Exposed=Window]
interface XPathEvaluator {
  constructor();
};

XPathEvaluator includes XPathEvaluatorBase;

```

> [!note]
> For historical reasons you can both construct [`XPathEvaluator`](#84-interface-xpathevaluator) and access the same methods on [`Document`](#45-interface-document).

## 9. XSLT

> [!danger]
> Avoid using client-side XSLT in browsers. The browser implementations of XSLT are highly susceptible to memory safety vulnerabilities, and the web platform has evolved toward JavaScript as the safe replacement. For these reasons, this feature is in the process of being removed from the web platform. (This is a long process that takes many years.)

> [!warning]
> XSL Transformations (XSLT) is a language for transforming XML documents into other XML documents. The APIs defined in this section have been widely implemented, and are maintained here so that they can be updated when Web IDL changes. Complete definitions of these APIs remain necessary and such work is tracked and can be contributed to in [whatwg/dom#181](https://github.com/whatwg/dom/issues/181). [\[XSLT\]](#non-normative-references)

### 9.1. Interface [`XSLTProcessor`](#91-interface-xsltprocessor)

```webidl
[Exposed=Window]
interface XSLTProcessor {
  constructor();
  undefined importStylesheet(Node style);
  [CEReactions] DocumentFragment transformToFragment(Node source, Document output);
  [CEReactions] Document transformToDocument(Node source);
  undefined setParameter([LegacyNullToEmptyString] DOMString namespaceURI, DOMString localName, any value);
  any getParameter([LegacyNullToEmptyString] DOMString namespaceURI, DOMString localName);
  undefined removeParameter([LegacyNullToEmptyString] DOMString namespaceURI, DOMString localName);
  undefined clearParameters();
  undefined reset();
};

```

## 10. Security and privacy considerations

There are no known security or privacy considerations for this standard.

## 11. Historical

This standard used to contain several interfaces and interface members that have been removed.

These interfaces have been removed:
- `DOMConfiguration`
- `DOMError`
- `DOMErrorHandler`
- `DOMImplementationList`
- `DOMImplementationSource`
- `DOMLocator`
- `DOMObject`
- `DOMUserData`
- `Entity`
- `EntityReference`
- `MutationEvent`
- `MutationNameEvent`
- `NameList`
- `Notation`
- `RangeException`
- `TypeInfo`
- `UserDataHandler`

And these interface members have been removed:

[`Attr`](#492-interface-attr)
- `schemaTypeInfo`
- `isId`

[`Document`](#45-interface-document)
- `createEntityReference()`
- `xmlEncoding`
- `xmlStandalone`
- `xmlVersion`
- `strictErrorChecking`
- `domConfig`
- `normalizeDocument()`
- `renameNode()`

[`DocumentType`](#46-interface-documenttype)
- `entities`
- `notations`
- `internalSubset`

[`DOMImplementation`](#451-interface-domimplementation)
- `getFeature()`

[`Element`](#49-interface-element)
- `schemaTypeInfo`
- `setIdAttribute()`
- `setIdAttributeNS()`
- `setIdAttributeNode()`

[`Node`](#44-interface-node)
- `isSupported`
- `getFeature()`
- `getUserData()`
- `setUserData()`

[`NodeIterator`](#61-interface-nodeiterator)
- `expandEntityReferences`

[`Text`](#411-interface-text)
- `isElementContentWhitespace`
- `replaceWholeText()`

[`TreeWalker`](#62-interface-treewalker)
- `expandEntityReferences`

## Acknowledgments

There have been a lot of people that have helped make DOM more interoperable over the years and thereby furthered the goals of this standard. Likewise many people have helped making this standard what it is today.

With that, many thanks to Adam Klein, Adrian Bateman, Ahmid *snuggs*, Alex Komoroske, Alex Russell, Alexey Shvayka, Andreas Kling, Andreu Botella, Anthony Ramine, Arkadiusz Michalski, Armen Michaeli, Arnaud Le Hors, Arun Ranganathan, Benjamin Gruenbaum, Björn Höhrmann, Boris Zbarsky, Brandon Payton, Brandon Slade, Brandon Wallace, Brian Kardell, C. Scott Ananian, Cameron McCormack, Chris Dumez, Chris Paris, Chris Rebert, Cyrille Tuzi, Dan Burzo, Daniel Clark, Daniel Glazman, Darien Maillet Valentine, Darin Fisher, David Baron, David Bruant, David Flanagan, David Håsäther, David Hyatt, Deepak Sherveghar, Dethe Elza, Dimitri Glazkov, Domenic Denicola, Dominic Cooney, Dominique Hazaël-Massieux, Don Jordan, Doug Schepers, Edgar Chen, Elisée Maurer, Elliott Sprehn, Emilio Cobos Álvarez, Eric Bidelman, Erik Arvidsson, Evgeny Kapun, François Daoust, François Remy, Gary Kacmarcik, Gavin Nicol, Giorgio Liscio, Glen Huang, Glenn Adams, Glenn Maynard, Hajime Morrita, Harald Alvestrand, Hayato Ito, Henri Sivonen, Hongchan Choi, Hunan Rostomyan, Ian Hickson, Igor Bukanov, Jacob Rossi, Jake Archibald, Jake Verbaten, James Graham, James Greene, James M Snell, James Robinson, Jayson Chen, Jeffrey Yasskin, Jens Lindström, Jeremy Davis, Jesse McCarthy, Jinho Bang, João Eiras, Joe Kesselman, John Atkins, John Dai, Jonas Sicking, Jonathan Kingston, Jonathan Robie, Joris van der Wel, Joshua Bell, J. S. Choi, Jungkee Song, Justin Summerlin, Kagami Sascha Rosylight, 呂康豪 (Kang-Hao Lu), 田村健人 (Kent TAMURA), Kevin J. Sung, Kevin Sweeney, Kirill Topolyan, Koji Ishii, Lachlan Hunt, Lauren Wood, Luca Casonato, Luke Zielinski, Magne Andersson, Majid Valipour, Malte Ubl, Manish Goregaokar, Manish Tripathi, Marcos Caceres, Mark Miller, Martijn van der Ven, Mason Freed, Mats Palmgren, Mounir Lamouri, Michael Stramel, Michael™ Smith, Mike Champion, Mike Taylor, Mike West, Nicolás Peña Moreno, Nidhi Jaju, Ojan Vafai, Oliver Nightingale, Olli Pettay, Ondřej Žára, Peter Sharpe, Philip Jägenstedt, Philippe Le Hégaret, Piers Wombwell, Pierre-Marie Dartus, prosody—Gab Vereable Context(, Rafael Weinstein, Rakina Zata Amni, Richard Bradshaw, Rick Byers, Rick Waldron, Robbert Broersma, Robin Berjon, Roland Steiner, Rune F. Halvorsen, Russell Bicknell, Ruud Steltenpool, Ryosuke Niwa, Sam Dutton, Sam Sneddon, Samuel Giles, Sanket Joshi, Scott Haseley, Sebastian Mayr, Seo Sanghyeon, Sergey G. Grekhov, Shiki Okasaka, Shinya Kawanaka, Simon Pieters, Simon Wülker, Stef Busking, Steve Byrne, Steven Obiajulu, Stig Halvorsen, Tab Atkins, Takashi Sakamoto, Takayoshi Kochi, Theresa O’Connor, Theodore Dubois, *timeless*, Timo Tijhof, Tobie Langel, Tom Pixley, Travis Leithead, Trevor Rowbotham, *triple-underscore*, Tristan Fraipont, Veli Şenol, Vidur Apparao, Warren He, Xidorn Quan, Yash Handa, Yehuda Katz, Yoav Weiss, Yoichi Osato, Yoshinori Sano, Yu Han, Yusuke Abe, and Zack Weinberg for being awesome!

This standard is written by [Anne van Kesteren](https://annevankesteren.nl/) ([Apple](https://www.apple.com/), [annevk@annevk.nl](mailto:annevk@annevk.nl)) with substantial contributions from Aryeh Gregor ([ayg@aryeh.name](mailto:ayg@aryeh.name)) and Ms2ger ([ms2ger@gmail.com](mailto:ms2ger@gmail.com)).

## Intellectual property rights

Part of the revision history of the integration points related to [custom](#49-interface-element) elements can be found in [the w3c/webcomponents repository](https://github.com/w3c/webcomponents), which is available under the [W3C Software and Document License](https://www.w3.org/Consortium/Legal/2015/copyright-software-and-document).

Copyright © WHATWG (Apple, Google, Mozilla, Microsoft). This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). To the extent portions of it are incorporated into source code, such portions in the source code are licensed under the [BSD 3-Clause License](https://opensource.org/licenses/BSD-3-Clause) instead.

This is the Living Standard. Those interested in the patent-review version should view the [Living Standard Review Draft](https://dom.spec.whatwg.org/review-drafts/2026-06/).

## Index

### Terms defined by this specification
- [abort](#32-interface-abortsignal), in § 3.2
- abort()
  - [method for AbortController](#31-interface-abortcontroller), in § 3.1
  - [method for AbortSignal](#32-interface-abortsignal), in § 3.2
- [abort algorithms](#32-interface-abortsignal), in § 3.2
- [AbortController](#31-interface-abortcontroller), in § 3.1
- [AbortController()](#31-interface-abortcontroller), in § 3.1
- aborted
  - [attribute for AbortSignal](#32-interface-abortsignal), in § 3.2
  - [dfn for AbortSignal](#32-interface-abortsignal), in § 3.2
- [abort reason](#32-interface-abortsignal), in § 3.2
- abort(reason)
  - [method for AbortController](#31-interface-abortcontroller), in § 3.1
  - [method for AbortSignal](#32-interface-abortsignal), in § 3.2
- [AbortSignal](#32-interface-abortsignal), in § 3.2
- [AbstractRange](#53-interface-abstractrange), in § 5.3
- [acceptNode(node)](#63-interface-nodefilter), in § 6.3
- [activation behavior](#27-interface-eventtarget), in § 2.7
- [add](#32-interface-abortsignal), in § 3.2
- [add()](#71-interface-domtokenlist), in § 7.1
- [add an event listener](#27-interface-eventtarget), in § 2.7
- [addedNodes](#433-interface-mutationrecord), in § 4.3.3
- [AddEventListenerOptions](#27-interface-eventtarget), in § 2.7
- [addEventListener(type, callback)](#27-interface-eventtarget), in § 2.7
- [addEventListener(type, callback, options)](#27-interface-eventtarget), in § 2.7
- [add(...tokens)](#71-interface-domtokenlist), in § 7.1
- [add(tokens)](#71-interface-domtokenlist), in § 7.1
- [add transient registered observers](#43-mutation-observers), in § 4.3
- [adjust a node pointer](#61-interface-nodeiterator), in § 6.1
- [adopt](#45-interface-document), in § 4.5
- [adopting steps](#45-interface-document), in § 4.5
- [adoptNode(node)](#45-interface-document), in § 4.5
- [after](#52-boundary-points), in § 5.2
- [after()](#428-mixin-childnode), in § 4.2.8
- [after(...nodes)](#428-mixin-childnode), in § 4.2.8
- [allow declarative shadow roots](#45-interface-document), in § 4.5
- [ancestor](#11-trees), in § 1.1
- [any(signals)](#32-interface-abortsignal), in § 3.2
- [ANY\_TYPE](#81-interface-xpathresult), in § 8.1
- [ANY\_UNORDERED\_NODE\_TYPE](#81-interface-xpathresult), in § 8.1
- [append](#423-mutation-algorithms), in § 4.2.3
- [append()](#426-mixin-parentnode), in § 4.2.6
- [append an attribute](#49-interface-element), in § 4.9
- [appendChild(node)](#44-interface-node), in § 4.4
- [appendData(data)](#410-interface-characterdata), in § 4.10
- [append(...nodes)](#426-mixin-parentnode), in § 4.2.6
- [append to an event path](#29-dispatching-events), in § 2.9
- [assign a slot](#4224-assigning-slottables-and-slots), in § 4.2.2.4
- [assigned](#4222-slottables), in § 4.2.2.2
- [assigned nodes](#4221-slots), in § 4.2.2.1
- [assigned slot](#4222-slottables), in § 4.2.2.2
- [assignedSlot](#429-mixin-slottable), in § 4.2.9
- [assign slottables](#4224-assigning-slottables-and-slots), in § 4.2.2.4
- [assign slottables for a tree](#4224-assigning-slottables-and-slots), in § 4.2.2.4
- [attach a shadow root](#49-interface-element), in § 4.9
- [attachShadow(init)](#49-interface-element), in § 4.9
- [AT\_TARGET](#22-interface-event), in § 2.2
- [Attr](#492-interface-attr), in § 4.9.2
- [attribute](#492-interface-attr), in § 4.9.2
- [attribute change steps](#49-interface-element), in § 4.9
- [attributeFilter](#431-interface-mutationobserver), in § 4.3.1
- attribute list
  - [dfn for Element](#49-interface-element), in § 4.9
  - [dfn for NamedNodeMap](#491-interface-namednodemap), in § 4.9.1
- [attribute map](#413-interface-processinginstruction), in § 4.13
- [attribute name](#71-interface-domtokenlist), in § 7.1
- [attributeName](#433-interface-mutationrecord), in § 4.3.3
- [attributeNamespace](#433-interface-mutationrecord), in § 4.3.3
- [ATTRIBUTE\_NODE](#44-interface-node), in § 4.4
- [attributeOldValue](#431-interface-mutationobserver), in § 4.3.1
- attributes
  - [attribute for Element](#49-interface-element), in § 4.9
  - [dict-member for MutationObserverInit](#431-interface-mutationobserver), in § 4.3.1
- [available to element internals](#48-interface-shadowroot), in § 4.8
- [baseURI](#44-interface-node), in § 4.4
- [before](#52-boundary-points), in § 5.2
- [before()](#428-mixin-childnode), in § 4.2.8
- [before(...nodes)](#428-mixin-childnode), in § 4.2.8
- [BOOLEAN\_TYPE](#81-interface-xpathresult), in § 8.1
- [booleanValue](#81-interface-xpathresult), in § 8.1
- [boundary point](#52-boundary-points), in § 5.2
- bubbles
  - [attribute for Event](#22-interface-event), in § 2.2
  - [dict-member for EventInit](#22-interface-event), in § 2.2
- [BUBBLING\_PHASE](#22-interface-event), in § 2.2
- callback
  - [dfn for MutationObserver](#431-interface-mutationobserver), in § 4.3.1
  - [dfn for event listener](#27-interface-eventtarget), in § 2.7
- cancelable
  - [attribute for Event](#22-interface-event), in § 2.2
  - [dict-member for EventInit](#22-interface-event), in § 2.2
- [cancelBubble](#22-interface-event), in § 2.2
- [canceled flag](#22-interface-event), in § 2.2
- [candidate reference](#61-interface-nodeiterator), in § 6.1
- capture
  - [dfn for event listener](#27-interface-eventtarget), in § 2.7
  - [dict-member for EventListenerOptions](#27-interface-eventtarget), in § 2.7
- [CAPTURING\_PHASE](#22-interface-event), in § 2.2
- [CDATASection](#412-interface-cdatasection), in § 4.12
- [CDATA\_SECTION\_NODE](#44-interface-node), in § 4.4
- [change an attribute](#49-interface-element), in § 4.9
- [CharacterData](#410-interface-characterdata), in § 4.10
- [characterData](#431-interface-mutationobserver), in § 4.3.1
- [characterDataOldValue](#431-interface-mutationobserver), in § 4.3.1
- [characterSet](#45-interface-document), in § 4.5
- [charset](#45-interface-document), in § 4.5
- [child](#11-trees), in § 1.1
- [childElementCount](#426-mixin-parentnode), in § 4.2.6
- [childList](#431-interface-mutationobserver), in § 4.3.1
- [ChildNode](#428-mixin-childnode), in § 4.2.8
- [childNodes](#44-interface-node), in § 4.4
- children
  - [attribute for ParentNode](#426-mixin-parentnode), in § 4.2.6
  - [dfn for tree](#11-trees), in § 1.1
- [children changed steps](#423-mutation-algorithms), in § 4.2.3
- [child text content](#411-interface-text), in § 4.11
- [class](#49-interface-element), in § 4.9
- [classList](#49-interface-element), in § 4.9
- [className](#49-interface-element), in § 4.9
- [clearParameters()](#91-interface-xsltprocessor), in § 9.1
- clonable
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dfn for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dict-member for ShadowRootInit](#49-interface-element), in § 4.9
- [clone a node](#44-interface-node), in § 4.4
- [clone a single node](#44-interface-node), in § 4.4
- [cloneContents()](#55-interface-range), in § 5.5
- [cloneNode()](#44-interface-node), in § 4.4
- [cloneNode(subtree)](#44-interface-node), in § 4.4
- [cloneRange()](#55-interface-range), in § 5.5
- [clone the contents](#55-interface-range), in § 5.5
- [cloning steps](#44-interface-node), in § 4.4
- [cloning the contents](#55-interface-range), in § 5.5
- ["closed"](#48-interface-shadowroot), in § 4.8
- [closed-shadow-hidden](#48-interface-shadowroot), in § 4.8
- [closest(selectors)](#49-interface-element), in § 4.9
- [collapse()](#55-interface-range), in § 5.5
- collapsed
  - [attribute for AbstractRange](#53-interface-abstractrange), in § 5.3
  - [dfn for range](#53-interface-abstractrange), in § 5.3
- [collapse(toStart)](#55-interface-range), in § 5.5
- [collection](#4210-old-style-collections-nodelist-and-htmlcollection), in § 4.2.10
- [Comment](#414-interface-comment), in § 4.14
- [Comment()](#414-interface-comment), in § 4.14
- [Comment(data)](#414-interface-comment), in § 4.14
- [COMMENT\_NODE](#44-interface-node), in § 4.4
- [commonAncestorContainer](#55-interface-range), in § 5.5
- [compareBoundaryPoints(how, sourceRange)](#55-interface-range), in § 5.5
- [compareDocumentPosition(other)](#44-interface-node), in § 4.4
- [comparePoint(node, offset)](#55-interface-range), in § 5.5
- [compatMode](#45-interface-document), in § 4.5
- composed
  - [attribute for Event](#22-interface-event), in § 2.2
  - [dict-member for EventInit](#22-interface-event), in § 2.2
  - [dict-member for GetRootNodeOptions](#44-interface-node), in § 4.4
- [composed flag](#22-interface-event), in § 2.2
- [composedPath()](#22-interface-event), in § 2.2
- [connected](#422-shadow-tree), in § 4.2.2
- [constructor](#25-constructing-events), in § 2.5
- constructor()
  - [constructor for AbortController](#31-interface-abortcontroller), in § 3.1
  - [constructor for Comment](#414-interface-comment), in § 4.14
  - [constructor for Document](#45-interface-document), in § 4.5
  - [constructor for DocumentFragment](#47-interface-documentfragment), in § 4.7
  - [constructor for EventTarget](#27-interface-eventtarget), in § 2.7
  - [constructor for Range](#55-interface-range), in § 5.5
  - [constructor for Text](#411-interface-text), in § 4.11
  - [constructor for XPathEvaluator](#84-interface-xpathevaluator), in § 8.4
  - [constructor for XSLTProcessor](#91-interface-xsltprocessor), in § 9.1
- [constructor(callback)](#431-interface-mutationobserver), in § 4.3.1
- constructor(data)
  - [constructor for Comment](#414-interface-comment), in § 4.14
  - [constructor for Text](#411-interface-text), in § 4.11
- [constructor(init)](#54-interface-staticrange), in § 5.4
- [constructor(target)](#413-interface-processinginstruction), in § 4.13
- [constructor(target, data)](#413-interface-processinginstruction), in § 4.13
- constructor(type)
  - [constructor for CustomEvent](#24-interface-customevent), in § 2.4
  - [constructor for Event](#22-interface-event), in § 2.2
- constructor(type, eventInitDict)
  - [constructor for CustomEvent](#24-interface-customevent), in § 2.4
  - [constructor for Event](#22-interface-event), in § 2.2
- [contained](#55-interface-range), in § 5.5
- [contains(other)](#44-interface-node), in § 4.4
- [contains(token)](#71-interface-domtokenlist), in § 7.1
- [content type](#45-interface-document), in § 4.5
- [contentType](#45-interface-document), in § 4.5
- [contiguous exclusive Text nodes](#411-interface-text), in § 4.11
- [contiguous Text nodes](#411-interface-text), in § 4.11
- [convert nodes into a node](#426-mixin-parentnode), in § 4.2.6
- [create a CDATA section node](#412-interface-cdatasection), in § 4.12
- [create a comment node](#414-interface-comment), in § 4.14
- [create a dependent abort signal](#32-interface-abortsignal), in § 3.2
- [create a doctype](#46-interface-documenttype), in § 4.6
- [create a document](#45-interface-document), in § 4.5
- [create a document fragment](#47-interface-documentfragment), in § 4.7
- [create an attribute](#492-interface-attr), in § 4.9.2
- [create an element](#49-interface-element), in § 4.9
- [create an element internal](#49-interface-element), in § 4.9
- [create an event](#25-constructing-events), in § 2.5
- [create a node](#44-interface-node), in § 4.4
- [create a processing instruction node](#413-interface-processinginstruction), in § 4.13
- [create a text node](#411-interface-text), in § 4.11
- [createAttribute(localName)](#45-interface-document), in § 4.5
- [createAttributeNS(namespace, qualifiedName)](#45-interface-document), in § 4.5
- [createCDATASection(data)](#45-interface-document), in § 4.5
- [createComment(data)](#45-interface-document), in § 4.5
- [createDocumentFragment()](#45-interface-document), in § 4.5
- [createDocument(namespace, qualifiedName)](#451-interface-domimplementation), in § 4.5.1
- [createDocument(namespace, qualifiedName, doctype)](#451-interface-domimplementation), in § 4.5.1
- [createDocumentType(name, publicId, systemId)](#451-interface-domimplementation), in § 4.5.1
- [createElement(localName)](#45-interface-document), in § 4.5
- [createElement(localName, options)](#45-interface-document), in § 4.5
- [createElementNS(namespace, qualifiedName)](#45-interface-document), in § 4.5
- [createElementNS(namespace, qualifiedName, options)](#45-interface-document), in § 4.5
- [createEntityReference()](#11-historical), in § 11
- [createEvent(interface)](#45-interface-document), in § 4.5
- [createExpression(expression)](#83-mixin-xpathevaluatorbase), in § 8.3
- [createExpression(expression, resolver)](#83-mixin-xpathevaluatorbase), in § 8.3
- [createHTMLDocument()](#451-interface-domimplementation), in § 4.5.1
- [createHTMLDocument(title)](#451-interface-domimplementation), in § 4.5.1
- [createNodeIterator(root)](#45-interface-document), in § 4.5
- [createNodeIterator(root, whatToShow)](#45-interface-document), in § 4.5
- [createNodeIterator(root, whatToShow, filter)](#45-interface-document), in § 4.5
- [createNSResolver(nodeResolver)](#83-mixin-xpathevaluatorbase), in § 8.3
- [createProcessingInstruction(target, data)](#45-interface-document), in § 4.5
- [createRange()](#45-interface-document), in § 4.5
- [createTextNode(data)](#45-interface-document), in § 4.5
- [createTreeWalker(root)](#45-interface-document), in § 4.5
- [createTreeWalker(root, whatToShow)](#45-interface-document), in § 4.5
- [createTreeWalker(root, whatToShow, filter)](#45-interface-document), in § 4.5
- [creating an event](#25-constructing-events), in § 2.5
- [creation index](#431-interface-mutationobserver), in § 4.3.1
- [current](#62-interface-treewalker), in § 6.2
- [current event](#23-legacy-extensions-to-the-window-interface), in § 2.3
- [currentNode](#62-interface-treewalker), in § 6.2
- [currentTarget](#22-interface-event), in § 2.2
- [custom](#49-interface-element), in § 4.9
- [custom element definition](#49-interface-element), in § 4.9
- custom element registry
  - [dfn for Document](#45-interface-document), in § 4.5
  - [dfn for Element](#49-interface-element), in § 4.9
  - [dfn for ShadowRoot](#48-interface-shadowroot), in § 4.8
- customElementRegistry
  - [attribute for DocumentOrShadowRoot](#425-mixin-documentorshadowroot), in § 4.2.5
  - [attribute for Element](#49-interface-element), in § 4.9
  - [dict-member for ElementCreationOptions](#45-interface-document), in § 4.5
  - [dict-member for ImportNodeOptions](#45-interface-document), in § 4.5
  - [dict-member for ShadowRootInit](#49-interface-element), in § 4.9
- [custom element state](#49-interface-element), in § 4.9
- [CustomEvent](#24-interface-customevent), in § 2.4
- [CustomEventInit](#24-interface-customevent), in § 2.4
- [CustomEvent(type)](#24-interface-customevent), in § 2.4
- [CustomEvent(type, eventInitDict)](#24-interface-customevent), in § 2.4
- data
  - [attribute for CharacterData](#410-interface-characterdata), in § 4.10
  - [dfn for CharacterData](#410-interface-characterdata), in § 4.10
- [declarative](#48-interface-shadowroot), in § 4.8
- [default passive value](#27-interface-eventtarget), in § 2.7
- [defaultPrevented](#22-interface-event), in § 2.2
- [defined](#49-interface-element), in § 4.9
- [delegates focus](#48-interface-shadowroot), in § 4.8
- delegatesFocus
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dict-member for ShadowRootInit](#49-interface-element), in § 4.9
- [deleteContents()](#55-interface-range), in § 5.5
- [deleteData(offset, count)](#410-interface-characterdata), in § 4.10
- [dependent](#32-interface-abortsignal), in § 3.2
- [dependent signals](#32-interface-abortsignal), in § 3.2
- [descendant](#11-trees), in § 1.1
- [descendant text content](#411-interface-text), in § 4.11
- detach()
  - [method for NodeIterator](#61-interface-nodeiterator), in § 6.1
  - [method for Range](#55-interface-range), in § 5.5
- detail
  - [attribute for CustomEvent](#24-interface-customevent), in § 2.4
  - [dict-member for CustomEventInit](#24-interface-customevent), in § 2.4
- [disconnect()](#431-interface-mutationobserver), in § 4.3.1
- [dispatch](#29-dispatching-events), in § 2.9
- [dispatchEvent(event)](#27-interface-eventtarget), in § 2.7
- [dispatch flag](#22-interface-event), in § 2.2
- doctype
  - [attribute for Document](#45-interface-document), in § 4.5
  - [definition of](#46-interface-documenttype), in § 4.6
- [Document](#45-interface-document), in § 4.5
- document
  - [definition of](#45-interface-document), in § 4.5
  - [dfn for clone a node](#44-interface-node), in § 4.4
- [Document()](#45-interface-document), in § 4.5
- [document element](#421-document-tree), in § 4.2.1
- [documentElement](#45-interface-document), in § 4.5
- [DocumentFragment](#47-interface-documentfragment), in § 4.7
- [DocumentFragment()](#47-interface-documentfragment), in § 4.7
- [DOCUMENT\_FRAGMENT\_NODE](#44-interface-node), in § 4.4
- [DOCUMENT\_NODE](#44-interface-node), in § 4.4
- [DocumentOrShadowRoot](#425-mixin-documentorshadowroot), in § 4.2.5
- [DOCUMENT\_POSITION\_CONTAINED\_BY](#44-interface-node), in § 4.4
- [DOCUMENT\_POSITION\_CONTAINS](#44-interface-node), in § 4.4
- [DOCUMENT\_POSITION\_DISCONNECTED](#44-interface-node), in § 4.4
- [DOCUMENT\_POSITION\_FOLLOWING](#44-interface-node), in § 4.4
- [DOCUMENT\_POSITION\_IMPLEMENTATION\_SPECIFIC](#44-interface-node), in § 4.4
- [DOCUMENT\_POSITION\_PRECEDING](#44-interface-node), in § 4.4
- [document tree](#421-document-tree), in § 4.2.1
- [DocumentType](#46-interface-documenttype), in § 4.6
- [DOCUMENT\_TYPE\_NODE](#44-interface-node), in § 4.4
- [documentURI](#45-interface-document), in § 4.5
- [domConfig](#11-historical), in § 11
- [DOMConfiguration](#11-historical), in § 11
- [DOMError](#11-historical), in § 11
- [DOMErrorHandler](#11-historical), in § 11
- [DOMImplementation](#451-interface-domimplementation), in § 4.5.1
- [DOMImplementationList](#11-historical), in § 11
- [DOMImplementationSource](#11-historical), in § 11
- [DOMLocator](#11-historical), in § 11
- [DOMObject](#11-historical), in § 11
- [DOMTokenList](#71-interface-domtokenlist), in § 7.1
- [DOMUserData](#11-historical), in § 11
- [effective global custom element registry](#45-interface-document), in § 4.5
- [Element](#49-interface-element), in § 4.9
- element
  - [definition of](#49-interface-element), in § 4.9
  - [dfn for Attr](#492-interface-attr), in § 4.9.2
  - [dfn for DOMTokenList](#71-interface-domtokenlist), in § 7.1
  - [dfn for NamedNodeMap](#491-interface-namednodemap), in § 4.9.1
- [ElementCreationOptions](#45-interface-document), in § 4.5
- [element interface](#45-interface-document), in § 4.5
- [ELEMENT\_NODE](#44-interface-node), in § 4.4
- [empty](#42-node-tree), in § 4.2
- [encoding](#45-interface-document), in § 4.5
- [end](#53-interface-abstractrange), in § 5.3
- endContainer
  - [attribute for AbstractRange](#53-interface-abstractrange), in § 5.3
  - [dict-member for StaticRangeInit](#54-interface-staticrange), in § 5.4
- [end node](#53-interface-abstractrange), in § 5.3
- [end offset](#53-interface-abstractrange), in § 5.3
- endOffset
  - [attribute for AbstractRange](#53-interface-abstractrange), in § 5.3
  - [dict-member for StaticRangeInit](#54-interface-staticrange), in § 5.4
- [END\_TO\_END](#55-interface-range), in § 5.5
- [END\_TO\_START](#55-interface-range), in § 5.5
- [ensure pre-insert validity](#423-mutation-algorithms), in § 4.2.3
- [entities](#11-historical), in § 11
- [Entity](#11-historical), in § 11
- [ENTITY\_NODE](#44-interface-node), in § 4.4
- [EntityReference](#11-historical), in § 11
- [ENTITY\_REFERENCE\_NODE](#44-interface-node), in § 4.4
- [equal](#52-boundary-points), in § 5.2
- [equals](#44-interface-node), in § 4.4
- [evaluate(contextNode)](#82-interface-xpathexpression), in § 8.2
- [evaluate(contextNode, type)](#82-interface-xpathexpression), in § 8.2
- [evaluate(contextNode, type, result)](#82-interface-xpathexpression), in § 8.2
- [evaluate(expression, contextNode)](#83-mixin-xpathevaluatorbase), in § 8.3
- [evaluate(expression, contextNode, resolver)](#83-mixin-xpathevaluatorbase), in § 8.3
- [evaluate(expression, contextNode, resolver, type)](#83-mixin-xpathevaluatorbase), in § 8.3
- [evaluate(expression, contextNode, resolver, type, result)](#83-mixin-xpathevaluatorbase), in § 8.3
- [Event](#22-interface-event), in § 2.2
- event
  - [attribute for Window](#23-legacy-extensions-to-the-window-interface), in § 2.3
  - [definition of](#22-interface-event), in § 2.2
- [event constructing steps](#25-constructing-events), in § 2.5
- [EventInit](#22-interface-event), in § 2.2
- [event listener](#27-interface-eventtarget), in § 2.7
- [EventListener](#27-interface-eventtarget), in § 2.7
- [event listener list](#27-interface-eventtarget), in § 2.7
- [EventListenerOptions](#27-interface-eventtarget), in § 2.7
- [event path item](#22-interface-event), in § 2.2
- [eventPhase](#22-interface-event), in § 2.2
- [EventTarget](#27-interface-eventtarget), in § 2.7
- [EventTarget()](#27-interface-eventtarget), in § 2.7
- [Event(type)](#22-interface-event), in § 2.2
- [Event(type, eventInitDict)](#22-interface-event), in § 2.2
- [exclusive DocumentFragment node](#47-interface-documentfragment), in § 4.7
- [exclusive Text node](#411-interface-text), in § 4.11
- expandEntityReferences
  - [attribute for NodeIterator](#11-historical), in § 11
  - [attribute for TreeWalker](#11-historical), in § 11
- [extract](#55-interface-range), in § 5.5
- [extractContents()](#55-interface-range), in § 5.5
- [fallbackRegistry](#44-interface-node), in § 4.4
- filter
  - [attribute for NodeIterator](#61-interface-nodeiterator), in § 6.1
  - [attribute for TreeWalker](#62-interface-treewalker), in § 6.2
  - [definition of](#6-traversal), in § 6
  - [dfn for traversal](#6-traversal), in § 6
- [FILTER\_ACCEPT](#63-interface-nodefilter), in § 6.3
- [FILTER\_REJECT](#63-interface-nodefilter), in § 6.3
- [FILTER\_SKIP](#63-interface-nodefilter), in § 6.3
- [find a slot](#4223-finding-slots-and-slottables), in § 4.2.2.3
- [find flattened slottables](#4223-finding-slots-and-slottables), in § 4.2.2.3
- [find slottables](#4223-finding-slots-and-slottables), in § 4.2.2.3
- [fire an event](#210-firing-events), in § 2.10
- [first child](#11-trees), in § 1.1
- [firstChild](#44-interface-node), in § 4.4
- [firstChild()](#62-interface-treewalker), in § 6.2
- [firstElementChild](#426-mixin-parentnode), in § 4.2.6
- [FIRST\_ORDERED\_NODE\_TYPE](#81-interface-xpathresult), in § 8.1
- [flatten](#27-interface-eventtarget), in § 2.7
- [flatten element creation options](#45-interface-document), in § 4.5
- [flatten more](#27-interface-eventtarget), in § 2.7
- [following](#11-trees), in § 1.1
- [get an attribute by name](#49-interface-element), in § 4.9
- [get an attribute by namespace and local name](#49-interface-element), in § 4.9
- [get an attribute value](#49-interface-element), in § 4.9
- [get an element by ID](#424-mixin-nonelementparentnode), in § 4.2.4
- [get a processing instruction attribute](#413-interface-processinginstruction), in § 4.13
- [getAttribute(name)](#413-interface-processinginstruction), in § 4.13
- getAttributeNames()
  - [method for Element](#49-interface-element), in § 4.9
  - [method for ProcessingInstruction](#413-interface-processinginstruction), in § 4.13
- [getAttributeNodeNS(namespace, localName)](#49-interface-element), in § 4.9
- [getAttributeNode(qualifiedName)](#49-interface-element), in § 4.9
- [getAttributeNS(namespace, localName)](#49-interface-element), in § 4.9
- [getAttribute(qualifiedName)](#49-interface-element), in § 4.9
- [getElementById(elementId)](#424-mixin-nonelementparentnode), in § 4.2.4
- getElementsByClassName(classNames)
  - [method for Document](#45-interface-document), in § 4.5
  - [method for Element](#49-interface-element), in § 4.9
- getElementsByTagNameNS(namespace, localName)
  - [method for Document](#45-interface-document), in § 4.5
  - [method for Element](#49-interface-element), in § 4.9
- getElementsByTagName(qualifiedName)
  - [method for Document](#45-interface-document), in § 4.5
  - [method for Element](#49-interface-element), in § 4.9
- getFeature()
  - [method for DOMImplementation](#11-historical), in § 11
  - [method for Node](#11-historical), in § 11
- [getNamedItemNS(namespace, localName)](#491-interface-namednodemap), in § 4.9.1
- [getNamedItem(qualifiedName)](#491-interface-namednodemap), in § 4.9.1
- [getParameter(namespaceURI, localName)](#91-interface-xsltprocessor), in § 9.1
- [getRootNode()](#44-interface-node), in § 4.4
- [getRootNode(options)](#44-interface-node), in § 4.4
- [GetRootNodeOptions](#44-interface-node), in § 4.4
- [get text content](#44-interface-node), in § 4.4
- [get the common ancestor](#55-interface-range), in § 5.5
- [get the parent](#27-interface-eventtarget), in § 2.7
- [getUserData()](#11-historical), in § 11
- [handle attribute changes](#49-interface-element), in § 4.9
- [handleEvent(event)](#27-interface-eventtarget), in § 2.7
- [has an attribute](#49-interface-element), in § 4.9
- [hasAttribute(name)](#413-interface-processinginstruction), in § 4.13
- [hasAttributeNS(namespace, localName)](#49-interface-element), in § 4.9
- [hasAttribute(qualifiedName)](#49-interface-element), in § 4.9
- hasAttributes()
  - [method for Element](#49-interface-element), in § 4.9
  - [method for ProcessingInstruction](#413-interface-processinginstruction), in § 4.13
- [hasChildNodes()](#44-interface-node), in § 4.4
- [hasFeature()](#451-interface-domimplementation), in § 4.5.1
- host
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dfn for DocumentFragment](#47-interface-documentfragment), in § 4.7
- [host-including inclusive ancestor](#47-interface-documentfragment), in § 4.7
- [HTMLCollection](#42102-interface-htmlcollection), in § 4.2.10.2
- [HTML document](#45-interface-document), in § 4.5
- [HTML-uppercased qualified name](#49-interface-element), in § 4.9
- [ID](#49-interface-element), in § 4.9
- [id](#49-interface-element), in § 4.9
- [implementation](#45-interface-document), in § 4.5
- [importNode(node)](#45-interface-document), in § 4.5
- [importNode(node, options)](#45-interface-document), in § 4.5
- [ImportNodeOptions](#45-interface-document), in § 4.5
- [importStylesheet(style)](#91-interface-xsltprocessor), in § 9.1
- [in a document](#421-document-tree), in § 4.2.1
- [in a document tree](#421-document-tree), in § 4.2.1
- [inclusive ancestor](#11-trees), in § 1.1
- [inclusive descendant](#11-trees), in § 1.1
- [inclusive sibling](#11-trees), in § 1.1
- [index](#11-trees), in § 1.1
- [initCustomEvent(type)](#24-interface-customevent), in § 2.4
- [initCustomEvent(type, bubbles)](#24-interface-customevent), in § 2.4
- [initCustomEvent(type, bubbles, cancelable)](#24-interface-customevent), in § 2.4
- [initCustomEvent(type, bubbles, cancelable, detail)](#24-interface-customevent), in § 2.4
- [initEvent(type)](#22-interface-event), in § 2.2
- [initEvent(type, bubbles)](#22-interface-event), in § 2.2
- [initEvent(type, bubbles, cancelable)](#22-interface-event), in § 2.2
- initialize
  - [dfn for Event](#22-interface-event), in § 2.2
  - [dfn for ProcessingInstruction](#413-interface-processinginstruction), in § 4.13
- [initialized flag](#22-interface-event), in § 2.2
- [inner event creation steps](#25-constructing-events), in § 2.5
- [inner invoke](#29-dispatching-events), in § 2.9
- [in passive listener flag](#22-interface-event), in § 2.2
- [inputEncoding](#45-interface-document), in § 4.5
- insert
  - [definition of](#423-mutation-algorithms), in § 4.2.3
  - [dfn for live range](#55-interface-range), in § 5.5
- [insert adjacent](#49-interface-element), in § 4.9
- [insertAdjacentElement(where, element)](#49-interface-element), in § 4.9
- [insertAdjacentText(where, data)](#49-interface-element), in § 4.9
- [insertBefore(node, child)](#44-interface-node), in § 4.4
- [insertData(offset, data)](#410-interface-characterdata), in § 4.10
- [insertion steps](#423-mutation-algorithms), in § 4.2.3
- [insertNode(node)](#55-interface-range), in § 5.5
- [internal createElementNS steps](#45-interface-document), in § 4.5
- [internalSubset](#11-historical), in § 11
- [intersectsNode(node)](#55-interface-range), in § 5.5
- [invalidIteratorState](#81-interface-xpathresult), in § 8.1
- [invocation target](#22-interface-event), in § 2.2
- [invocation-target-in-shadow-tree](#22-interface-event), in § 2.2
- [invoke](#29-dispatching-events), in § 2.9
- [is](#45-interface-document), in § 4.5
- [is active](#6-traversal), in § 6
- [is a global custom element registry](#45-interface-document), in § 4.5
- [isConnected](#44-interface-node), in § 4.4
- [isDefaultNamespace(namespace)](#44-interface-node), in § 4.4
- [isElementContentWhitespace](#11-historical), in § 11
- [isEqualNode(otherNode)](#44-interface-node), in § 4.4
- [isId](#11-historical), in § 11
- [isPointInRange(node, offset)](#55-interface-range), in § 5.5
- [isSameNode(otherNode)](#44-interface-node), in § 4.4
- [isSupported](#11-historical), in § 11
- [isTrusted](#22-interface-event), in § 2.2
- [is value](#49-interface-element), in § 4.9
- item(index)
  - [method for DOMTokenList](#71-interface-domtokenlist), in § 7.1
  - [method for HTMLCollection](#42102-interface-htmlcollection), in § 4.2.10.2
  - [method for NamedNodeMap](#491-interface-namednodemap), in § 4.9.1
  - [method for NodeList](#42101-interface-nodelist), in § 4.2.10.1
- [iterateNext()](#81-interface-xpathresult), in § 8.1
- [iterator collection](#61-interface-nodeiterator), in § 6.1
- [keep custom element registry null](#48-interface-shadowroot), in § 4.8
- [last child](#11-trees), in § 1.1
- [lastChild](#44-interface-node), in § 4.4
- [lastChild()](#62-interface-treewalker), in § 6.2
- [lastElementChild](#426-mixin-parentnode), in § 4.2.6
- [legacy-canceled-activation behavior](#27-interface-eventtarget), in § 2.7
- [legacy-obtain service worker fetch event listener callbacks](#28-observing-event-listeners), in § 2.8
- [legacy-pre-activation behavior](#27-interface-eventtarget), in § 2.7
- length
  - [attribute for CharacterData](#410-interface-characterdata), in § 4.10
  - [attribute for DOMTokenList](#71-interface-domtokenlist), in § 7.1
  - [attribute for HTMLCollection](#42102-interface-htmlcollection), in § 4.2.10.2
  - [attribute for NamedNodeMap](#491-interface-namednodemap), in § 4.9.1
  - [attribute for NodeList](#42101-interface-nodelist), in § 4.2.10.1
  - [dfn for Node](#42-node-tree), in § 4.2
- [light tree](#422-shadow-tree), in § 4.2.2
- [limited-quirks mode](#45-interface-document), in § 4.5
- [list of elements with class names classNames](#44-interface-node), in § 4.4
- [list of elements with namespace namespace and local name localName](#44-interface-node), in § 4.4
- [list of elements with qualified name qualifiedName](#44-interface-node), in § 4.4
- [live](#4210-old-style-collections-nodelist-and-htmlcollection), in § 4.2.10
- [live collection](#4210-old-style-collections-nodelist-and-htmlcollection), in § 4.2.10
- [live range pre-remove steps](#55-interface-range), in § 5.5
- [live ranges](#55-interface-range), in § 5.5
- local name
  - [dfn for Attr](#492-interface-attr), in § 4.9.2
  - [dfn for Element](#49-interface-element), in § 4.9
- localName
  - [attribute for Attr](#492-interface-attr), in § 4.9.2
  - [attribute for Element](#49-interface-element), in § 4.9
- [locate a namespace](#44-interface-node), in § 4.4
- [locate a namespace prefix](#44-interface-node), in § 4.4
- [locating a namespace prefix](#44-interface-node), in § 4.4
- lookupNamespaceURI(prefix)
  - [method for Node](#44-interface-node), in § 4.4
  - [method for XPathNSResolver](#83-mixin-xpathevaluatorbase), in § 8.3
- [lookupPrefix(namespace)](#44-interface-node), in § 4.4
- ["manual"](#48-interface-shadowroot), in § 4.8
- [manual slot assignment](#4222-slottables), in § 4.2.2.2
- [matches(selectors)](#49-interface-element), in § 4.9
- mode
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dfn for Document](#45-interface-document), in § 4.5
  - [dfn for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dict-member for ShadowRootInit](#49-interface-element), in § 4.9
- [move](#423-mutation-algorithms), in § 4.2.3
- [moveBefore(node, child)](#426-mixin-parentnode), in § 4.2.6
- [moving steps](#423-mutation-algorithms), in § 4.2.3
- [MutationCallback](#431-interface-mutationobserver), in § 4.3.1
- [MutationEvent](#11-historical), in § 11
- [MutationNameEvent](#11-historical), in § 11
- [MutationObserver](#431-interface-mutationobserver), in § 4.3.1
- [MutationObserver(callback)](#431-interface-mutationobserver), in § 4.3.1
- [mutation observer counter](#43-mutation-observers), in § 4.3
- [MutationObserverInit](#431-interface-mutationobserver), in § 4.3.1
- [mutation observer microtask queued](#43-mutation-observers), in § 4.3
- [MutationRecord](#433-interface-mutationrecord), in § 4.3.3
- name
  - [attribute for Attr](#492-interface-attr), in § 4.9.2
  - [attribute for DocumentType](#46-interface-documenttype), in § 4.6
  - [dfn for DocumentType](#46-interface-documenttype), in § 4.6
  - [dfn for slot](#4221-slots), in § 4.2.2.1
  - [dfn for slottable](#4222-slottables), in § 4.2.2.2
- ["named"](#48-interface-shadowroot), in § 4.8
- [named attribute](#492-interface-attr), in § 4.9.2
- [namedItem(key)](#42102-interface-htmlcollection), in § 4.2.10.2
- [namedItem(name)](#42102-interface-htmlcollection), in § 4.2.10.2
- [NamedNodeMap](#491-interface-namednodemap), in § 4.9.1
- [NameList](#11-historical), in § 11
- namespace
  - [dfn for Attr](#492-interface-attr), in § 4.9.2
  - [dfn for Element](#49-interface-element), in § 4.9
- namespace prefix
  - [dfn for Attr](#492-interface-attr), in § 4.9.2
  - [dfn for Element](#49-interface-element), in § 4.9
- namespaceURI
  - [attribute for Attr](#492-interface-attr), in § 4.9.2
  - [attribute for Element](#49-interface-element), in § 4.9
- [nextElementSibling](#427-mixin-nondocumenttypechildnode), in § 4.2.7
- nextNode()
  - [method for NodeIterator](#61-interface-nodeiterator), in § 6.1
  - [method for TreeWalker](#62-interface-treewalker), in § 6.2
- [next sibling](#11-trees), in § 1.1
- nextSibling
  - [attribute for MutationRecord](#433-interface-mutationrecord), in § 4.3.3
  - [attribute for Node](#44-interface-node), in § 4.4
- [nextSibling()](#62-interface-treewalker), in § 6.2
- [Node](#44-interface-node), in § 4.4
- node
  - [dfn for boundary point](#52-boundary-points), in § 5.2
  - [dfn for node pointer](#61-interface-nodeiterator), in § 6.1
- [node document](#44-interface-node), in § 4.4
- [NodeFilter](#63-interface-nodefilter), in § 6.3
- [NodeIterator](#61-interface-nodeiterator), in § 6.1
- [NodeIterator pre-remove steps](#61-interface-nodeiterator), in § 6.1
- [node list](#431-interface-mutationobserver), in § 4.3.1
- [NodeList](#42101-interface-nodelist), in § 4.2.10.1
- [nodeName](#44-interface-node), in § 4.4
- [node pointer](#61-interface-nodeiterator), in § 6.1
- [Nodes](#42-node-tree), in § 4.2
- [node tree](#42-node-tree), in § 4.2
- [nodeType](#44-interface-node), in § 4.4
- [nodeValue](#44-interface-node), in § 4.4
- [NonDocumentTypeChildNode](#427-mixin-nondocumenttypechildnode), in § 4.2.7
- [NONE](#22-interface-event), in § 2.2
- [NonElementParentNode](#424-mixin-nonelementparentnode), in § 4.2.4
- [no-quirks mode](#45-interface-document), in § 4.5
- [normalize()](#44-interface-node), in § 4.4
- [normalizeDocument()](#11-historical), in § 11
- [Notation](#11-historical), in § 11
- [NOTATION\_NODE](#44-interface-node), in § 4.4
- [notations](#11-historical), in § 11
- [notify mutation observers](#43-mutation-observers), in § 4.3
- [NUMBER\_TYPE](#81-interface-xpathresult), in § 8.1
- [numberValue](#81-interface-xpathresult), in § 8.1
- [observer](#43-mutation-observers), in § 4.3
- [observe(target)](#431-interface-mutationobserver), in § 4.3.1
- [observe(target, options)](#431-interface-mutationobserver), in § 4.3.1
- [offset](#52-boundary-points), in § 5.2
- [oldValue](#433-interface-mutationrecord), in § 4.3.3
- onabort
  - [attribute for AbortSignal](#32-interface-abortsignal), in § 3.2
  - [dfn for AbortSignal](#32-interface-abortsignal), in § 3.2
- once
  - [dfn for event listener](#27-interface-eventtarget), in § 2.7
  - [dict-member for AddEventListenerOptions](#27-interface-eventtarget), in § 2.7
- onslotchange
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dfn for ShadowRoot](#48-interface-shadowroot), in § 4.8
- ["open"](#48-interface-shadowroot), in § 4.8
- [options](#43-mutation-observers), in § 4.3
- [ORDERED\_NODE\_ITERATOR\_TYPE](#81-interface-xpathresult), in § 8.1
- [ORDERED\_NODE\_SNAPSHOT\_TYPE](#81-interface-xpathresult), in § 8.1
- [ordered set parser](#12-ordered-sets), in § 1.2
- [ordered set serializer](#12-ordered-sets), in § 1.2
- [origin](#45-interface-document), in § 4.5
- [other applicable specifications](#1-infrastructure), in § 1
- [ownerDocument](#44-interface-node), in § 4.4
- [ownerElement](#492-interface-attr), in § 4.9.2
- parent
  - [dfn for clone a node](#44-interface-node), in § 4.4
  - [dfn for tree](#11-trees), in § 1.1
- [parent element](#49-interface-element), in § 4.9
- [parentElement](#44-interface-node), in § 4.4
- [ParentNode](#426-mixin-parentnode), in § 4.2.6
- [parentNode](#44-interface-node), in § 4.4
- [parentNode()](#62-interface-treewalker), in § 6.2
- [partially contained](#55-interface-range), in § 5.5
- [participate](#11-trees), in § 1.1
- [participate in a tree](#11-trees), in § 1.1
- [participates in a tree](#11-trees), in § 1.1
- passive
  - [dfn for event listener](#27-interface-eventtarget), in § 2.7
  - [dict-member for AddEventListenerOptions](#27-interface-eventtarget), in § 2.7
- [path](#22-interface-event), in § 2.2
- [pending mutation observers](#43-mutation-observers), in § 4.3
- [pointer before](#61-interface-nodeiterator), in § 6.1
- [pointerBeforeReferenceNode](#61-interface-nodeiterator), in § 6.1
- [position](#52-boundary-points), in § 5.2
- [post-connection steps](#423-mutation-algorithms), in § 4.2.3
- [potential event target](#22-interface-event), in § 2.2
- [preceding](#11-trees), in § 1.1
- prefix
  - [attribute for Attr](#492-interface-attr), in § 4.9.2
  - [attribute for Element](#49-interface-element), in § 4.9
- [pre-insert](#423-mutation-algorithms), in § 4.2.3
- [prepend()](#426-mixin-parentnode), in § 4.2.6
- [prepend(...nodes)](#426-mixin-parentnode), in § 4.2.6
- [pre-remove](#423-mutation-algorithms), in § 4.2.3
- [preventDefault()](#22-interface-event), in § 2.2
- [previousElementSibling](#427-mixin-nondocumenttypechildnode), in § 4.2.7
- previousNode()
  - [method for NodeIterator](#61-interface-nodeiterator), in § 6.1
  - [method for TreeWalker](#62-interface-treewalker), in § 6.2
- [previous sibling](#11-trees), in § 1.1
- previousSibling
  - [attribute for MutationRecord](#433-interface-mutationrecord), in § 4.3.3
  - [attribute for Node](#44-interface-node), in § 4.4
- [previousSibling()](#62-interface-treewalker), in § 6.2
- [ProcessingInstruction](#413-interface-processinginstruction), in § 4.13
- [PROCESSING\_INSTRUCTION\_NODE](#44-interface-node), in § 4.4
- [ProcessingInstruction(target)](#413-interface-processinginstruction), in § 4.13
- [ProcessingInstruction(target, data)](#413-interface-processinginstruction), in § 4.13
- [public ID](#46-interface-documenttype), in § 4.6
- [publicId](#46-interface-documenttype), in § 4.6
- qualified name
  - [dfn for Attr](#492-interface-attr), in § 4.9.2
  - [dfn for Element](#49-interface-element), in § 4.9
- [querySelectorAll(selectors)](#426-mixin-parentnode), in § 4.2.6
- [querySelector(selectors)](#426-mixin-parentnode), in § 4.2.6
- [queue a mutation observer microtask](#43-mutation-observers), in § 4.3
- [queue a mutation record](#432-queuing-a-mutation-record), in § 4.3.2
- [queue a tree mutation record](#432-queuing-a-mutation-record), in § 4.3.2
- [quirks mode](#45-interface-document), in § 4.5
- [Range](#55-interface-range), in § 5.5
- [range](#53-interface-abstractrange), in § 5.3
- [Range()](#55-interface-range), in § 5.5
- [RangeException](#11-historical), in § 11
- [reason](#32-interface-abortsignal), in § 3.2
- [record queue](#431-interface-mutationobserver), in § 4.3.1
- [reference](#61-interface-nodeiterator), in § 6.1
- [referenceNode](#61-interface-nodeiterator), in § 6.1
- [reflect](#49-interface-element), in § 4.9
- [registered observer](#43-mutation-observers), in § 4.3
- [registered observer list](#43-mutation-observers), in § 4.3
- relatedTarget
  - [dfn for Event](#22-interface-event), in § 2.2
  - [dfn for event path item](#22-interface-event), in § 2.2
- remove
  - [definition of](#423-mutation-algorithms), in § 4.2.3
  - [dfn for AbortSignal](#32-interface-abortsignal), in § 3.2
- remove()
  - [method for ChildNode](#428-mixin-childnode), in § 4.2.8
  - [method for DOMTokenList](#71-interface-domtokenlist), in § 7.1
- [remove all event listeners](#27-interface-eventtarget), in § 2.7
- [remove an attribute](#49-interface-element), in § 4.9
- [remove an attribute by name](#49-interface-element), in § 4.9
- [remove an attribute by namespace and local name](#49-interface-element), in § 4.9
- [remove an event listener](#27-interface-eventtarget), in § 2.7
- [removeAttribute(name)](#413-interface-processinginstruction), in § 4.13
- [removeAttributeNode(attr)](#49-interface-element), in § 4.9
- [removeAttributeNS(namespace, localName)](#49-interface-element), in § 4.9
- [removeAttribute(qualifiedName)](#49-interface-element), in § 4.9
- [removeChild(child)](#44-interface-node), in § 4.4
- [removed](#27-interface-eventtarget), in § 2.7
- [removedNodes](#433-interface-mutationrecord), in § 4.3.3
- [removeEventListener(type, callback)](#27-interface-eventtarget), in § 2.7
- [removeEventListener(type, callback, options)](#27-interface-eventtarget), in § 2.7
- [removeNamedItemNS(namespace, localName)](#491-interface-namednodemap), in § 4.9.1
- [removeNamedItem(qualifiedName)](#491-interface-namednodemap), in § 4.9.1
- [removeParameter(namespaceURI, localName)](#91-interface-xsltprocessor), in § 9.1
- [remove(...tokens)](#71-interface-domtokenlist), in § 7.1
- [remove(tokens)](#71-interface-domtokenlist), in § 7.1
- [remove transient registered observers](#43-mutation-observers), in § 4.3
- [removing steps](#423-mutation-algorithms), in § 4.2.3
- [renameNode()](#11-historical), in § 11
- [replace](#423-mutation-algorithms), in § 4.2.3
- [replace all](#423-mutation-algorithms), in § 4.2.3
- [replace an attribute](#49-interface-element), in § 4.9
- [replaceChild(node, child)](#44-interface-node), in § 4.4
- [replaceChildren()](#426-mixin-parentnode), in § 4.2.6
- [replaceChildren(...nodes)](#426-mixin-parentnode), in § 4.2.6
- [replace data](#410-interface-characterdata), in § 4.10
- [replaceData(offset, count, data)](#410-interface-characterdata), in § 4.10
- [replace(token, newToken)](#71-interface-domtokenlist), in § 7.1
- [replaceWholeText()](#11-historical), in § 11
- [replaceWith()](#428-mixin-childnode), in § 4.2.8
- [replaceWith(...nodes)](#428-mixin-childnode), in § 4.2.8
- [represented by the collection](#4210-old-style-collections-nodelist-and-htmlcollection), in § 4.2.10
- [reset()](#91-interface-xsltprocessor), in § 9.1
- [resultType](#81-interface-xpathresult), in § 8.1
- [retarget](#48-interface-shadowroot), in § 4.8
- [retargeting](#48-interface-shadowroot), in § 4.8
- [returnValue](#22-interface-event), in § 2.2
- root
  - [attribute for NodeIterator](#61-interface-nodeiterator), in § 6.1
  - [attribute for TreeWalker](#62-interface-treewalker), in § 6.2
  - [dfn for live range](#55-interface-range), in § 5.5
  - [dfn for traversal](#6-traversal), in § 6
  - [dfn for tree](#11-trees), in § 1.1
- [root-of-closed-tree](#22-interface-event), in § 2.2
- [run the abort steps](#32-interface-abortsignal), in § 3.2
- schemaTypeInfo
  - [attribute for Attr](#11-historical), in § 11
  - [attribute for Element](#11-historical), in § 11
- [scope-match a selectors string](#13-selectors), in § 1.3
- [select](#55-interface-range), in § 5.5
- [selectNodeContents(node)](#55-interface-range), in § 5.5
- [selectNode(node)](#55-interface-range), in § 5.5
- [selfOnly](#45-interface-document), in § 4.5
- serializable
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dfn for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dict-member for ShadowRootInit](#49-interface-element), in § 4.9
- [serialize steps](#71-interface-domtokenlist), in § 7.1
- [set an attribute](#49-interface-element), in § 4.9
- [set an attribute value](#49-interface-element), in § 4.9
- [set an existing attribute value](#492-interface-attr), in § 4.9.2
- [setAttribute(name, value)](#413-interface-processinginstruction), in § 4.13
- [setAttributeNode(attr)](#49-interface-element), in § 4.9
- [setAttributeNodeNS(attr)](#49-interface-element), in § 4.9
- [setAttributeNS(namespace, qualifiedName, value)](#49-interface-element), in § 4.9
- [setAttribute(qualifiedName, value)](#49-interface-element), in § 4.9
- [setEndAfter(node)](#55-interface-range), in § 5.5
- [setEndBefore(node)](#55-interface-range), in § 5.5
- [setEnd(node, offset)](#55-interface-range), in § 5.5
- [setIdAttribute()](#11-historical), in § 11
- [setIdAttributeNode()](#11-historical), in § 11
- [setIdAttributeNS()](#11-historical), in § 11
- [setNamedItem(attr)](#491-interface-namednodemap), in § 4.9.1
- [setNamedItemNS(attr)](#491-interface-namednodemap), in § 4.9.1
- [setParameter(namespaceURI, localName, value)](#91-interface-xsltprocessor), in § 9.1
- [setStartAfter(node)](#55-interface-range), in § 5.5
- [setStartBefore(node)](#55-interface-range), in § 5.5
- [setStart(node, offset)](#55-interface-range), in § 5.5
- [set text content](#44-interface-node), in § 4.4
- [set the canceled flag](#22-interface-event), in § 2.2
- [set the end](#55-interface-range), in § 5.5
- [set the start](#55-interface-range), in § 5.5
- [setUserData()](#11-historical), in § 11
- [shadow-adjusted target](#22-interface-event), in § 2.2
- [shadow host](#49-interface-element), in § 4.9
- [shadow-including ancestor](#48-interface-shadowroot), in § 4.8
- [shadow-including descendant](#48-interface-shadowroot), in § 4.8
- [shadow-including inclusive ancestor](#48-interface-shadowroot), in § 4.8
- [shadow-including inclusive descendant](#48-interface-shadowroot), in § 4.8
- [Shadow-including preorder, depth-first traversal](#48-interface-shadowroot), in § 4.8
- [shadow-including root](#48-interface-shadowroot), in § 4.8
- [shadow-including tree order](#48-interface-shadowroot), in § 4.8
- shadow root
  - [definition of](#48-interface-shadowroot), in § 4.8
  - [dfn for Element](#49-interface-element), in § 4.9
- [ShadowRoot](#48-interface-shadowroot), in § 4.8
- [shadowRoot](#49-interface-element), in § 4.9
- [ShadowRootInit](#49-interface-element), in § 4.9
- [ShadowRootMode](#48-interface-shadowroot), in § 4.8
- [shadow tree](#422-shadow-tree), in § 4.2.2
- [SHOW\_ALL](#63-interface-nodefilter), in § 6.3
- [SHOW\_ATTRIBUTE](#63-interface-nodefilter), in § 6.3
- [SHOW\_CDATA\_SECTION](#63-interface-nodefilter), in § 6.3
- [SHOW\_COMMENT](#63-interface-nodefilter), in § 6.3
- [SHOW\_DOCUMENT](#63-interface-nodefilter), in § 6.3
- [SHOW\_DOCUMENT\_FRAGMENT](#63-interface-nodefilter), in § 6.3
- [SHOW\_DOCUMENT\_TYPE](#63-interface-nodefilter), in § 6.3
- [SHOW\_ELEMENT](#63-interface-nodefilter), in § 6.3
- [SHOW\_ENTITY](#63-interface-nodefilter), in § 6.3
- [SHOW\_ENTITY\_REFERENCE](#63-interface-nodefilter), in § 6.3
- [SHOW\_NOTATION](#63-interface-nodefilter), in § 6.3
- [SHOW\_PROCESSING\_INSTRUCTION](#63-interface-nodefilter), in § 6.3
- [SHOW\_TEXT](#63-interface-nodefilter), in § 6.3
- [sibling](#11-trees), in § 1.1
- signal
  - [attribute for AbortController](#31-interface-abortcontroller), in § 3.1
  - [dfn for AbortController](#31-interface-abortcontroller), in § 3.1
  - [dfn for event listener](#27-interface-eventtarget), in § 2.7
  - [dict-member for AddEventListenerOptions](#27-interface-eventtarget), in § 2.7
- signal abort
  - [dfn for AbortController](#31-interface-abortcontroller), in § 3.1
  - [dfn for AbortSignal](#32-interface-abortsignal), in § 3.2
- [signal a slot change](#4225-signaling-slot-change), in § 4.2.2.5
- [signal slots](#4225-signaling-slot-change), in § 4.2.2.5
- [singleNodeValue](#81-interface-xpathresult), in § 8.1
- slot
  - [attribute for Element](#49-interface-element), in § 4.9
  - [definition of](#4221-slots), in § 4.2.2.1
- [slot assignment](#48-interface-shadowroot), in § 4.8
- slotAssignment
  - [attribute for ShadowRoot](#48-interface-shadowroot), in § 4.8
  - [dict-member for ShadowRootInit](#49-interface-element), in § 4.9
- [SlotAssignmentMode](#48-interface-shadowroot), in § 4.8
- [slotchange](#43-mutation-observers), in § 4.3
- [slot-in-closed-tree](#22-interface-event), in § 2.2
- [Slottable](#429-mixin-slottable), in § 4.2.9
- [slottable](#4222-slottables), in § 4.2.2.2
- [snapshotItem(index)](#81-interface-xpathresult), in § 8.1
- [snapshotLength](#81-interface-xpathresult), in § 8.1
- [source](#43-mutation-observers), in § 4.3
- [source signals](#32-interface-abortsignal), in § 3.2
- [specified](#492-interface-attr), in § 4.9.2
- [split a Text node](#411-interface-text), in § 4.11
- [splitText(offset)](#411-interface-text), in § 4.11
- [srcElement](#22-interface-event), in § 2.2
- [start](#53-interface-abstractrange), in § 5.3
- startContainer
  - [attribute for AbstractRange](#53-interface-abstractrange), in § 5.3
  - [dict-member for StaticRangeInit](#54-interface-staticrange), in § 5.4
- [start node](#53-interface-abstractrange), in § 5.3
- [start offset](#53-interface-abstractrange), in § 5.3
- startOffset
  - [attribute for AbstractRange](#53-interface-abstractrange), in § 5.3
  - [dict-member for StaticRangeInit](#54-interface-staticrange), in § 5.4
- [START\_TO\_END](#55-interface-range), in § 5.5
- [START\_TO\_START](#55-interface-range), in § 5.5
- [static collection](#4210-old-style-collections-nodelist-and-htmlcollection), in § 4.2.10
- [StaticRange](#54-interface-staticrange), in § 5.4
- [StaticRange(init)](#54-interface-staticrange), in § 5.4
- [StaticRangeInit](#54-interface-staticrange), in § 5.4
- [stopImmediatePropagation()](#22-interface-event), in § 2.2
- [stop immediate propagation flag](#22-interface-event), in § 2.2
- [stopPropagation()](#22-interface-event), in § 2.2
- [stop propagation flag](#22-interface-event), in § 2.2
- [strictErrorChecking](#11-historical), in § 11
- [stringification behavior](#71-interface-domtokenlist), in § 7.1
- [stringificationbehavior](#55-interface-range), in § 5.5
- [string replace all](#44-interface-node), in § 4.4
- [STRING\_TYPE](#81-interface-xpathresult), in § 8.1
- [stringValue](#81-interface-xpathresult), in § 8.1
- [substring data](#410-interface-characterdata), in § 4.10
- [substringData(offset, count)](#410-interface-characterdata), in § 4.10
- subtree
  - [dfn for clone a node](#44-interface-node), in § 4.4
  - [dict-member for MutationObserverInit](#431-interface-mutationobserver), in § 4.3.1
- [supported tokens](#71-interface-domtokenlist), in § 7.1
- [supports(token)](#71-interface-domtokenlist), in § 7.1
- suppressObservers
  - [dfn for insert](#423-mutation-algorithms), in § 4.2.3
  - [dfn for remove](#423-mutation-algorithms), in § 4.2.3
- [surroundContents(newParent)](#55-interface-range), in § 5.5
- [system ID](#46-interface-documenttype), in § 4.6
- [systemId](#46-interface-documenttype), in § 4.6
- [tagName](#49-interface-element), in § 4.9
- [takeRecords()](#431-interface-mutationobserver), in § 4.3.1
- target
  - [attribute for Event](#22-interface-event), in § 2.2
  - [attribute for MutationRecord](#433-interface-mutationrecord), in § 4.3.3
  - [attribute for ProcessingInstruction](#413-interface-processinginstruction), in § 4.13
  - [dfn for Event](#22-interface-event), in § 2.2
  - [dfn for ProcessingInstruction](#413-interface-processinginstruction), in § 4.13
- [Text](#411-interface-text), in § 4.11
- [Text()](#411-interface-text), in § 4.11
- [textContent](#44-interface-node), in § 4.4
- [Text(data)](#411-interface-text), in § 4.11
- [TEXT\_NODE](#44-interface-node), in § 4.4
- [throwIfAborted()](#32-interface-abortsignal), in § 3.2
- [timeout(milliseconds)](#32-interface-abortsignal), in § 3.2
- [timeStamp](#22-interface-event), in § 2.2
- [toggleAttribute(name)](#413-interface-processinginstruction), in § 4.13
- [toggleAttribute(name, force)](#413-interface-processinginstruction), in § 4.13
- [toggleAttribute(qualifiedName)](#49-interface-element), in § 4.9
- [toggleAttribute(qualifiedName, force)](#49-interface-element), in § 4.9
- [toggle(token)](#71-interface-domtokenlist), in § 7.1
- [toggle(token, force)](#71-interface-domtokenlist), in § 7.1
- [token set](#71-interface-domtokenlist), in § 7.1
- touch target list
  - [dfn for Event](#22-interface-event), in § 2.2
  - [dfn for event path item](#22-interface-event), in § 2.2
- [transformToDocument(source)](#91-interface-xsltprocessor), in § 9.1
- [transformToFragment(source, output)](#91-interface-xsltprocessor), in § 9.1
- [transient node set](#431-interface-mutationobserver), in § 4.3.1
- [transient registered observer](#43-mutation-observers), in § 4.3
- [traverse](#61-interface-nodeiterator), in § 6.1
- [traverse children](#62-interface-treewalker), in § 6.2
- [traverse siblings](#62-interface-treewalker), in § 6.2
- [tree](#11-trees), in § 1.1
- [tree order](#11-trees), in § 1.1
- [TreeWalker](#62-interface-treewalker), in § 6.2
- type
  - [attribute for Event](#22-interface-event), in § 2.2
  - [attribute for MutationRecord](#433-interface-mutationrecord), in § 4.3.3
  - [dfn for Document](#45-interface-document), in § 4.5
  - [dfn for event listener](#27-interface-eventtarget), in § 2.7
- [TypeInfo](#11-historical), in § 11
- [UNORDERED\_NODE\_ITERATOR\_TYPE](#81-interface-xpathresult), in § 8.1
- [UNORDERED\_NODE\_SNAPSHOT\_TYPE](#81-interface-xpathresult), in § 8.1
- [update attributes from data](#413-interface-processinginstruction), in § 4.13
- [update data from attributes](#413-interface-processinginstruction), in § 4.13
- [update steps](#71-interface-domtokenlist), in § 7.1
- URL
  - [attribute for Document](#45-interface-document), in § 4.5
  - [dfn for Document](#45-interface-document), in § 4.5
- [UserDataHandler](#11-historical), in § 11
- [valid](#54-interface-staticrange), in § 5.4
- [validate and extract](#14-name-validation), in § 1.4
- [validation steps](#71-interface-domtokenlist), in § 7.1
- [valid attribute local name](#14-name-validation), in § 1.4
- [valid doctype name](#14-name-validation), in § 1.4
- [valid element local name](#14-name-validation), in § 1.4
- [valid namespace prefix](#14-name-validation), in § 1.4
- [valid shadow host name](#49-interface-element), in § 4.9
- value
  - [attribute for Attr](#492-interface-attr), in § 4.9.2
  - [attribute for DOMTokenList](#71-interface-domtokenlist), in § 7.1
  - [dfn for Attr](#492-interface-attr), in § 4.9.2
- [webkitMatchesSelector(selectors)](#49-interface-element), in § 4.9
- whatToShow
  - [attribute for NodeIterator](#61-interface-nodeiterator), in § 6.1
  - [attribute for TreeWalker](#62-interface-treewalker), in § 6.2
  - [dfn for traversal](#6-traversal), in § 6
- [wholeText](#411-interface-text), in § 4.11
- [XML document](#45-interface-document), in § 4.5
- [XMLDocument](#45-interface-document), in § 4.5
- [xmlEncoding](#11-historical), in § 11
- [xmlStandalone](#11-historical), in § 11
- [xmlVersion](#11-historical), in § 11
- [XPathEvaluator](#84-interface-xpathevaluator), in § 8.4
- [XPathEvaluator()](#84-interface-xpathevaluator), in § 8.4
- [XPathEvaluatorBase](#83-mixin-xpathevaluatorbase), in § 8.3
- [XPathExpression](#82-interface-xpathexpression), in § 8.2
- [XPathNSResolver](#83-mixin-xpathevaluatorbase), in § 8.3
- [XPathResult](#81-interface-xpathresult), in § 8.1
- [XSLTProcessor](#91-interface-xsltprocessor), in § 9.1
- [XSLTProcessor()](#91-interface-xsltprocessor), in § 9.1

### Terms defined by reference
- \[\] defines the following terms:
  - DeviceMotionEvent
  - DeviceOrientationEvent
  - TouchEvent
  - createContextualFragment()
- \[CONSOLE\] defines the following terms:
  - report a warning to the console
- \[CSSOM-VIEW\] defines the following terms:
  - getBoundingClientRect()
  - getClientRects()
- \[ECMASCRIPT\] defines the following terms:
  - current realm
  - realm
  - surrounding agent
- \[ENCODING\] defines the following terms:
  - encoding
  - name
  - UTF-8
- \[HR-TIME-3\] defines the following terms:
  - DOMHighResTimeStamp
  - current high resolution time
  - relative high resolution coarse time
- \[HTML\] defines the following terms:
  - BeforeUnloadEvent
  - CEReactions
  - CustomElementRegistry
  - DragEvent
  - EventHandler
  - HTMLAnchorElement
  - HTMLElement
  - HTMLHtmlElement
  - HTMLSlotElement
  - HTMLUnknownElement
  - HashChangeEvent
  - MessageEvent
  - StorageEvent
  - Window
  - active custom element constructor map
  - area
  - associated Document
  - browsing context
  - browsing context (for Document)
  - click()
  - constructor
  - current global object
  - custom element constructor
  - custom element definition
  - customized built-in element
  - disable shadow
  - document base URL
  - enqueue a custom element callback reaction
  - enqueue a custom element upgrade reaction
  - event handler
  - event handler event type
  - event handler IDL attribute
  - fully active
  - global object
  - head
  - html
  - HTML parser
  - in parallel
  - input
  - is scoped
  - local name
  - look up a custom element definition
  - look up a custom element registry
  - manually assigned nodes
  - microtask
  - name
  - opaque origin
  - origin
  - queue a global task
  - queue a microtask
  - relevant agent
  - relevant global object
  - relevant realm
  - report an exception
  - run steps after a timeout
  - scoped document set
  - script
  - similar-origin window agent
  - slot
  - style
  - template
  - the body element
  - timer task source
  - title
  - try to upgrade an element
  - upgrade an element
  - valid custom element name
- \[INFRA\] defines the following terms:
  - append (for list)
  - append (for set)
  - ASCII alpha
  - ASCII case-insensitive
  - ASCII digit
  - ASCII lowercase
  - ASCII uppercase
  - ASCII whitespace
  - assert
  - break
  - clear
  - clone
  - code point
  - code unit
  - concatenation
  - contain
  - continue
  - empty
  - enqueue
  - exist (for list)
  - exist (for map)
  - for each (for list)
  - for each (for map)
  - getting the keys
  - HTML namespace
  - identical to
  - insert
  - is empty (for list)
  - is empty (for map)
  - is not empty
  - length
  - list
  - map
  - ordered set
  - prepend
  - queue
  - remove (for list)
  - remove (for map)
  - replace (for list)
  - replace (for set)
  - set
  - set (for map)
  - size
  - sorting
  - split on ASCII whitespace
  - string
  - struct
  - SVG namespace
  - tuple
  - with default
  - XML namespace
  - XMLNS namespace
- \[LONG-ANIMATION-FRAMES\] defines the following terms:
  - record timing info for event listener
- \[POINTEREVENTS3\] defines the following terms:
  - MouseEvent
- \[SELECTORS4\] defines the following terms:
  - :defined
  - match a selector against a tree
  - match a selector against an element
  - parse a selector
  - scoping root
- \[SERVICE-WORKERS\] defines the following terms:
  - ServiceWorkerGlobalScope
  - has ever been evaluated flag
  - script resource
  - service worker
  - service worker events
  - set of event types to handle
- \[TRUSTED-TYPES\] defines the following terms:
  - TrustedType
  - get trusted type compliant attribute value
- \[UIEVENTS\] defines the following terms:
  - CompositionEvent
  - FocusEvent
  - KeyboardEvent
  - TextEvent
  - UIEvent
  - detail
- \[URL\] defines the following terms:
  - URL
  - URL serializer
- \[WEBIDL\] defines the following terms:
  - AbortError
  - DOMException
  - DOMString
  - EnforceRange
  - Exposed
  - HierarchyRequestError
  - InUseAttributeError
  - IndexSizeError
  - InvalidCharacterError
  - InvalidNodeTypeError
  - InvalidStateError
  - LegacyNullToEmptyString
  - LegacyUnenumerableNamedProperties
  - LegacyUnforgeable
  - NamespaceError
  - NewObject
  - NotFoundError
  - NotSupportedError
  - PutForwards
  - Replaceable
  - SameObject
  - SyntaxError
  - TimeoutError
  - USVString
  - Unscopable
  - WrongDocumentError
  - a new promise
  - any
  - associated realm
  - boolean
  - call a user object's operation
  - callback this value
  - construct
  - converted to an IDL value
  - dictionary
  - identifier
  - implements
  - invoke
  - iterable
  - new
  - primary interface
  - reject
  - resolve
  - sequence
  - short
  - supported property indices
  - supported property names
  - this
  - throw
  - undefined
  - unrestricted double
  - unsigned long
  - unsigned long long
  - unsigned short
- \[XML\] defines the following terms:
  - Name
- \[XML-STYLESHEET\] defines the following terms:
  - name
  - parsing result
  - pseudo-attribute
  - rules for parsing pseudo-attributes from a string
  - value

## References

### Normative References

\[CONSOLE\]

Dominic Farolino; Robert Kowalski; Terin Stock. [Console Standard](https://console.spec.whatwg.org/). Living Standard. URL: [https://console.spec.whatwg.org/](https://console.spec.whatwg.org/)

\[DEVICE-ORIENTATION\]

Reilly Grant; Marcos Caceres. [Device Orientation and Motion](https://w3c.github.io/deviceorientation/). URL: [https://w3c.github.io/deviceorientation/](https://w3c.github.io/deviceorientation/)

\[ECMASCRIPT\]

[ECMAScript Language Specification](https://tc39.es/ecma262/multipage/). URL: [https://tc39.es/ecma262/multipage/](https://tc39.es/ecma262/multipage/)

\[ENCODING\]

Anne van Kesteren. [Encoding Standard](https://encoding.spec.whatwg.org/). Living Standard. URL: [https://encoding.spec.whatwg.org/](https://encoding.spec.whatwg.org/)

\[HR-TIME-3\]

Yoav Weiss. [High Resolution Time](https://w3c.github.io/hr-time/). URL: [https://w3c.github.io/hr-time/](https://w3c.github.io/hr-time/)

\[HTML\]

Anne van Kesteren; et al. [HTML Standard](html-spec-whatwg-org.md). Living Standard. URL: [https://html.spec.whatwg.org/multipage/](html-spec-whatwg-org.md)

\[INFRA\]

Anne van Kesteren; Domenic Denicola. [Infra Standard](infra-spec-whatwg-org.md). Living Standard. URL: [https://infra.spec.whatwg.org/](infra-spec-whatwg-org.md)

\[LONG-ANIMATION-FRAMES\]

Noam Rosenthal. [Long Animation Frames API](https://w3c.github.io/long-animation-frames/). URL: [https://w3c.github.io/long-animation-frames/](https://w3c.github.io/long-animation-frames/)

\[POINTEREVENTS3\]

Patrick Lauke; Robert Flack. [Pointer Events](https://w3c.github.io/pointerevents/). URL: [https://w3c.github.io/pointerevents/](https://w3c.github.io/pointerevents/)

\[SELECTORS4\]

Elika Etemad; Tab Atkins Jr.. [Selectors Level 4](https://drafts.csswg.org/selectors/). URL: [https://drafts.csswg.org/selectors/](https://drafts.csswg.org/selectors/)

\[SERVICE-WORKERS\]

Monica CHINTALA; Yoshisato Yanagisawa. [Service Workers Nightly](https://w3c.github.io/ServiceWorker/). URL: [https://w3c.github.io/ServiceWorker/](https://w3c.github.io/ServiceWorker/)

\[TOUCH-EVENTS\]

Doug Schepers; et al. [Touch Events](https://w3c.github.io/touch-events/). URL: [https://w3c.github.io/touch-events/](https://w3c.github.io/touch-events/)

\[TRUSTED-TYPES\]

Krzysztof Kotowicz. [Trusted Types](https://w3c.github.io/trusted-types/dist/spec/). URL: [https://w3c.github.io/trusted-types/dist/spec/](https://w3c.github.io/trusted-types/dist/spec/)

\[UIEVENTS\]

Xiaoqian Wu. [UI Events](https://w3c.github.io/uievents/). URL: [https://w3c.github.io/uievents/](https://w3c.github.io/uievents/)

\[URL\]

Anne van Kesteren. [URL Standard](https://url.spec.whatwg.org/). Living Standard. URL: [https://url.spec.whatwg.org/](https://url.spec.whatwg.org/)

\[WEBIDL\]

Edgar Chen; Timothy Gu. [Web IDL Standard](https://webidl.spec.whatwg.org/). Living Standard. URL: [https://webidl.spec.whatwg.org/](https://webidl.spec.whatwg.org/)

\[XML\]

Tim Bray; et al. [Extensible Markup Language (XML) 1.0 (Fifth Edition)](https://www.w3.org/TR/xml/). 26 November 2008. REC. URL: [https://www.w3.org/TR/xml/](https://www.w3.org/TR/xml/)

\[XML-NAMES\]

Tim Bray; et al. [Namespaces in XML 1.0 (Third Edition)](https://www.w3.org/TR/xml-names/). 8 December 2009. REC. URL: [https://www.w3.org/TR/xml-names/](https://www.w3.org/TR/xml-names/)

\[XML-STYLESHEET\]

James Clark; Simon Pieters; Henry Thompson. [Associating Style Sheets with XML documents 1.0 (Second Edition)](https://www.w3.org/TR/xml-stylesheet/). 28 October 2010. REC. URL: [https://www.w3.org/TR/xml-stylesheet/](https://www.w3.org/TR/xml-stylesheet/)

### Non-Normative References

\[CSSOM-VIEW\]

Simon Fraser; Emilio Cobos Álvarez. [CSSOM View Module](https://drafts.csswg.org/cssom-view/). URL: [https://drafts.csswg.org/cssom-view/](https://drafts.csswg.org/cssom-view/)

\[DOM-Level-3-XPath\]

Ray Whitmer. [Document Object Model (DOM) Level 3 XPath Specification](https://www.w3.org/TR/DOM-Level-3-XPath/). 3 November 2020. NOTE. URL: [https://www.w3.org/TR/DOM-Level-3-XPath/](https://www.w3.org/TR/DOM-Level-3-XPath/)

\[DOM-Parsing\]

Travis Leithead. [DOM Parsing and Serialization](https://w3c.github.io/DOM-Parsing/). URL: [https://w3c.github.io/DOM-Parsing/](https://w3c.github.io/DOM-Parsing/)

\[FULLSCREEN\]

Philip Jägenstedt. [Fullscreen API Standard](https://fullscreen.spec.whatwg.org/). Living Standard. URL: [https://fullscreen.spec.whatwg.org/](https://fullscreen.spec.whatwg.org/)

\[INDEXEDDB\]

Nikunj Mehta; et al. [Indexed Database API](https://w3c.github.io/IndexedDB/). URL: [https://w3c.github.io/IndexedDB/](https://w3c.github.io/IndexedDB/)

\[XPath\]

James Clark; Steven DeRose. [XML Path Language (XPath) Version 1.0](https://www.w3.org/TR/xpath-10/). 16 November 1999. REC. URL: [https://www.w3.org/TR/xpath-10/](https://www.w3.org/TR/xpath-10/)

\[XSLT\]

James Clark. [XSL Transformations (XSLT) Version 1.0](https://www.w3.org/TR/xslt-10/). 16 November 1999. REC. URL: [https://www.w3.org/TR/xslt-10/](https://www.w3.org/TR/xslt-10/)

## IDL Index

```webidl
[Exposed=*]
interface Event {
  constructor(DOMString type, optional EventInit eventInitDict = {});

  readonly attribute DOMString type;
  readonly attribute EventTarget? target;
  readonly attribute EventTarget? srcElement; // legacy
  readonly attribute EventTarget? currentTarget;
  sequence<EventTarget> composedPath();

  const unsigned short NONE = 0;
  const unsigned short CAPTURING_PHASE = 1;
  const unsigned short AT_TARGET = 2;
  const unsigned short BUBBLING_PHASE = 3;
  readonly attribute unsigned short eventPhase;

  undefined stopPropagation();
           attribute boolean cancelBubble; // legacy alias of .stopPropagation()
  undefined stopImmediatePropagation();

  readonly attribute boolean bubbles;
  readonly attribute boolean cancelable;
           attribute boolean returnValue;  // legacy
  undefined preventDefault();
  readonly attribute boolean defaultPrevented;
  readonly attribute boolean composed;

  [LegacyUnforgeable] readonly attribute boolean isTrusted;
  readonly attribute DOMHighResTimeStamp timeStamp;

  undefined initEvent(DOMString type, optional boolean bubbles = false, optional boolean cancelable = false); // legacy
};

dictionary EventInit {
  boolean bubbles = false;
  boolean cancelable = false;
  boolean composed = false;
};

partial interface Window {
  [Replaceable] readonly attribute (Event or undefined) event; // legacy
};

[Exposed=*]
interface CustomEvent : Event {
  constructor(DOMString type, optional CustomEventInit eventInitDict = {});

  readonly attribute any detail;

  undefined initCustomEvent(DOMString type, optional boolean bubbles = false, optional boolean cancelable = false, optional any detail = null); // legacy
};

dictionary CustomEventInit : EventInit {
  any detail = null;
};

[Exposed=*]
interface EventTarget {
  constructor();

  undefined addEventListener(DOMString type, EventListener? callback, optional (AddEventListenerOptions or boolean) options = {});
  undefined removeEventListener(DOMString type, EventListener? callback, optional (EventListenerOptions or boolean) options = {});
  boolean dispatchEvent(Event event);
};

callback interface EventListener {
  undefined handleEvent(Event event);
};

dictionary EventListenerOptions {
  boolean capture = false;
};

dictionary AddEventListenerOptions : EventListenerOptions {
  boolean passive;
  boolean once = false;
  AbortSignal signal;
};

[Exposed=*]
interface AbortController {
  constructor();

  [SameObject] readonly attribute AbortSignal signal;

  undefined abort(optional any reason);
};

[Exposed=*]
interface AbortSignal : EventTarget {
  [NewObject] static AbortSignal abort(optional any reason);
  [Exposed=(Window,Worker), NewObject] static AbortSignal timeout([EnforceRange] unsigned long long milliseconds);
  [NewObject] static AbortSignal _any(sequence<AbortSignal> signals);

  readonly attribute boolean aborted;
  readonly attribute any reason;
  undefined throwIfAborted();

  attribute EventHandler onabort;
};
interface mixin NonElementParentNode {
  Element? getElementById(DOMString elementId);
};
Document includes NonElementParentNode;
DocumentFragment includes NonElementParentNode;

interface mixin DocumentOrShadowRoot {
  readonly attribute CustomElementRegistry? customElementRegistry;
};
Document includes DocumentOrShadowRoot;
ShadowRoot includes DocumentOrShadowRoot;

interface mixin ParentNode {
  [SameObject] readonly attribute HTMLCollection children;
  readonly attribute Element? firstElementChild;
  readonly attribute Element? lastElementChild;
  readonly attribute unsigned long childElementCount;

  [CEReactions, Unscopable] undefined prepend((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined append((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined replaceChildren((Node or DOMString)... nodes);

  [CEReactions] undefined moveBefore(Node node, Node? child);

  Element? querySelector(DOMString selectors);
  [NewObject] NodeList querySelectorAll(DOMString selectors);
};
Document includes ParentNode;
DocumentFragment includes ParentNode;
Element includes ParentNode;

interface mixin NonDocumentTypeChildNode {
  readonly attribute Element? previousElementSibling;
  readonly attribute Element? nextElementSibling;
};
Element includes NonDocumentTypeChildNode;
CharacterData includes NonDocumentTypeChildNode;

interface mixin ChildNode {
  [CEReactions, Unscopable] undefined before((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined after((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined replaceWith((Node or DOMString)... nodes);
  [CEReactions, Unscopable] undefined remove();
};
DocumentType includes ChildNode;
Element includes ChildNode;
CharacterData includes ChildNode;

interface mixin Slottable {
  readonly attribute HTMLSlotElement? assignedSlot;
};
Element includes Slottable;
Text includes Slottable;

[Exposed=Window]
interface NodeList {
  getter Node? item(unsigned long index);
  readonly attribute unsigned long length;
  iterable<Node>;
};

[Exposed=Window, LegacyUnenumerableNamedProperties]
interface HTMLCollection {
  readonly attribute unsigned long length;
  getter Element? item(unsigned long index);
  getter Element? namedItem(DOMString name);
};

[Exposed=Window]
interface MutationObserver {
  constructor(MutationCallback callback);

  undefined observe(Node target, optional MutationObserverInit options = {});
  undefined disconnect();
  sequence<MutationRecord> takeRecords();
};

callback MutationCallback = undefined (sequence<MutationRecord> mutations, MutationObserver observer);

dictionary MutationObserverInit {
  boolean childList = false;
  boolean attributes;
  boolean characterData;
  boolean subtree = false;
  boolean attributeOldValue;
  boolean characterDataOldValue;
  sequence<DOMString> attributeFilter;
};

[Exposed=Window]
interface MutationRecord {
  readonly attribute DOMString type;
  [SameObject] readonly attribute Node target;
  [SameObject] readonly attribute NodeList addedNodes;
  [SameObject] readonly attribute NodeList removedNodes;
  readonly attribute Node? previousSibling;
  readonly attribute Node? nextSibling;
  readonly attribute DOMString? attributeName;
  readonly attribute DOMString? attributeNamespace;
  readonly attribute DOMString? oldValue;
};

[Exposed=Window]
interface Node : EventTarget {
  const unsigned short ELEMENT_NODE = 1;
  const unsigned short ATTRIBUTE_NODE = 2;
  const unsigned short TEXT_NODE = 3;
  const unsigned short CDATA_SECTION_NODE = 4;
  const unsigned short ENTITY_REFERENCE_NODE = 5; // legacy
  const unsigned short ENTITY_NODE = 6; // legacy
  const unsigned short PROCESSING_INSTRUCTION_NODE = 7;
  const unsigned short COMMENT_NODE = 8;
  const unsigned short DOCUMENT_NODE = 9;
  const unsigned short DOCUMENT_TYPE_NODE = 10;
  const unsigned short DOCUMENT_FRAGMENT_NODE = 11;
  const unsigned short NOTATION_NODE = 12; // legacy
  readonly attribute unsigned short nodeType;
  readonly attribute DOMString nodeName;

  readonly attribute USVString baseURI;

  readonly attribute boolean isConnected;
  readonly attribute Document? ownerDocument;
  Node getRootNode(optional GetRootNodeOptions options = {});
  readonly attribute Node? parentNode;
  readonly attribute Element? parentElement;
  boolean hasChildNodes();
  [SameObject] readonly attribute NodeList childNodes;
  readonly attribute Node? firstChild;
  readonly attribute Node? lastChild;
  readonly attribute Node? previousSibling;
  readonly attribute Node? nextSibling;

  [CEReactions] attribute DOMString? nodeValue;
  [CEReactions] attribute DOMString? textContent;
  [CEReactions] undefined normalize();

  [CEReactions, NewObject] Node cloneNode(optional boolean subtree = false);
  boolean isEqualNode(Node? otherNode);
  boolean isSameNode(Node? otherNode); // legacy alias of ===

  const unsigned short DOCUMENT_POSITION_DISCONNECTED = 0x01;
  const unsigned short DOCUMENT_POSITION_PRECEDING = 0x02;
  const unsigned short DOCUMENT_POSITION_FOLLOWING = 0x04;
  const unsigned short DOCUMENT_POSITION_CONTAINS = 0x08;
  const unsigned short DOCUMENT_POSITION_CONTAINED_BY = 0x10;
  const unsigned short DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC = 0x20;
  unsigned short compareDocumentPosition(Node other);
  boolean contains(Node? other);

  DOMString? lookupPrefix(DOMString? namespace);
  DOMString? lookupNamespaceURI(DOMString? prefix);
  boolean isDefaultNamespace(DOMString? namespace);

  [CEReactions] Node insertBefore(Node node, Node? child);
  [CEReactions] Node appendChild(Node node);
  [CEReactions] Node replaceChild(Node node, Node child);
  [CEReactions] Node removeChild(Node child);
};

dictionary GetRootNodeOptions {
  boolean composed = false;
};

[Exposed=Window]
interface Document : Node {
  constructor();

  [SameObject] readonly attribute DOMImplementation implementation;
  readonly attribute USVString URL;
  readonly attribute USVString documentURI;
  readonly attribute DOMString compatMode;
  readonly attribute DOMString characterSet;
  readonly attribute DOMString charset; // legacy alias of .characterSet
  readonly attribute DOMString inputEncoding; // legacy alias of .characterSet
  readonly attribute DOMString contentType;

  readonly attribute DocumentType? doctype;
  readonly attribute Element? documentElement;
  HTMLCollection getElementsByTagName(DOMString qualifiedName);
  HTMLCollection getElementsByTagNameNS(DOMString? namespace, DOMString localName);
  HTMLCollection getElementsByClassName(DOMString classNames);

  [CEReactions, NewObject] Element createElement(DOMString localName, optional (DOMString or ElementCreationOptions) options = {});
  [CEReactions, NewObject] Element createElementNS(DOMString? namespace, DOMString qualifiedName, optional (DOMString or ElementCreationOptions) options = {});
  [NewObject] DocumentFragment createDocumentFragment();
  [NewObject] Text createTextNode(DOMString data);
  [NewObject] CDATASection createCDATASection(DOMString data);
  [NewObject] Comment createComment(DOMString data);
  [NewObject] ProcessingInstruction createProcessingInstruction(DOMString target, DOMString data);

  [CEReactions, NewObject] Node importNode(Node node, optional (boolean or ImportNodeOptions) options = false);
  [CEReactions] Node adoptNode(Node node);

  [NewObject] Attr createAttribute(DOMString localName);
  [NewObject] Attr createAttributeNS(DOMString? namespace, DOMString qualifiedName);

  [NewObject] Event createEvent(DOMString interface); // legacy

  [NewObject] Range createRange();

  // NodeFilter.SHOW_ALL = 0xFFFFFFFF
  [NewObject] NodeIterator createNodeIterator(Node root, optional unsigned long whatToShow = 0xFFFFFFFF, optional NodeFilter? filter = null);
  [NewObject] TreeWalker createTreeWalker(Node root, optional unsigned long whatToShow = 0xFFFFFFFF, optional NodeFilter? filter = null);
};

[Exposed=Window]
interface XMLDocument : Document {};

dictionary ElementCreationOptions {
  CustomElementRegistry? customElementRegistry;
  DOMString is;
};

dictionary ImportNodeOptions {
  CustomElementRegistry customElementRegistry;
  boolean selfOnly = false;
};

[Exposed=Window]
interface DOMImplementation {
  [NewObject] DocumentType createDocumentType(DOMString name, DOMString publicId, DOMString systemId);
  [NewObject] XMLDocument createDocument(DOMString? namespace, [LegacyNullToEmptyString] DOMString qualifiedName, optional DocumentType? doctype = null);
  [NewObject] Document createHTMLDocument(optional DOMString title);

  boolean hasFeature(); // historical; always returns true
};

[Exposed=Window]
interface DocumentType : Node {
  readonly attribute DOMString name;
  readonly attribute DOMString publicId;
  readonly attribute DOMString systemId;
};

[Exposed=Window]
interface DocumentFragment : Node {
  constructor();
};

[Exposed=Window]
interface ShadowRoot : DocumentFragment {
  readonly attribute ShadowRootMode mode;
  readonly attribute boolean delegatesFocus;
  readonly attribute boolean serializable;
  readonly attribute SlotAssignmentMode slotAssignment;
  readonly attribute boolean clonable;
  readonly attribute Element host;

  attribute EventHandler onslotchange;
};

enum ShadowRootMode { "open", "closed" };
enum SlotAssignmentMode { "manual", "named" };

[Exposed=Window]
interface Element : Node {
  readonly attribute DOMString? namespaceURI;
  readonly attribute DOMString? prefix;
  readonly attribute DOMString localName;
  readonly attribute DOMString tagName;

  [CEReactions] attribute DOMString id;
  [CEReactions] attribute DOMString className;
  [SameObject, PutForwards=value] readonly attribute DOMTokenList classList;
  [CEReactions, Unscopable] attribute DOMString slot;

  boolean hasAttributes();
  [SameObject] readonly attribute NamedNodeMap attributes;
  sequence<DOMString> getAttributeNames();
  DOMString? getAttribute(DOMString qualifiedName);
  DOMString? getAttributeNS(DOMString? namespace, DOMString localName);
  [CEReactions] undefined setAttribute(DOMString qualifiedName, (TrustedType or DOMString) value);
  [CEReactions] undefined setAttributeNS(DOMString? namespace, DOMString qualifiedName, (TrustedType or DOMString) value);
  [CEReactions] undefined removeAttribute(DOMString qualifiedName);
  [CEReactions] undefined removeAttributeNS(DOMString? namespace, DOMString localName);
  [CEReactions] boolean toggleAttribute(DOMString qualifiedName, optional boolean force);
  boolean hasAttribute(DOMString qualifiedName);
  boolean hasAttributeNS(DOMString? namespace, DOMString localName);

  Attr? getAttributeNode(DOMString qualifiedName);
  Attr? getAttributeNodeNS(DOMString? namespace, DOMString localName);
  [CEReactions] Attr? setAttributeNode(Attr attr);
  [CEReactions] Attr? setAttributeNodeNS(Attr attr);
  [CEReactions] Attr removeAttributeNode(Attr attr);

  ShadowRoot attachShadow(ShadowRootInit init);
  readonly attribute ShadowRoot? shadowRoot;

  readonly attribute CustomElementRegistry? customElementRegistry;

  Element? closest(DOMString selectors);
  boolean matches(DOMString selectors);
  boolean webkitMatchesSelector(DOMString selectors); // legacy alias of .matches

  HTMLCollection getElementsByTagName(DOMString qualifiedName);
  HTMLCollection getElementsByTagNameNS(DOMString? namespace, DOMString localName);
  HTMLCollection getElementsByClassName(DOMString classNames);

  [CEReactions] Element? insertAdjacentElement(DOMString where, Element element); // legacy
  undefined insertAdjacentText(DOMString where, DOMString data); // legacy
};

dictionary ShadowRootInit {
  required ShadowRootMode mode;
  boolean delegatesFocus = false;
  boolean serializable = false;
  SlotAssignmentMode slotAssignment = "named";
  boolean clonable = false;
  CustomElementRegistry? customElementRegistry;
};

[Exposed=Window,
 LegacyUnenumerableNamedProperties]
interface NamedNodeMap {
  readonly attribute unsigned long length;
  getter Attr? item(unsigned long index);
  getter Attr? getNamedItem(DOMString qualifiedName);
  Attr? getNamedItemNS(DOMString? namespace, DOMString localName);
  [CEReactions] Attr? setNamedItem(Attr attr);
  [CEReactions] Attr? setNamedItemNS(Attr attr);
  [CEReactions] Attr removeNamedItem(DOMString qualifiedName);
  [CEReactions] Attr removeNamedItemNS(DOMString? namespace, DOMString localName);
};

[Exposed=Window]
interface Attr : Node {
  readonly attribute DOMString? namespaceURI;
  readonly attribute DOMString? prefix;
  readonly attribute DOMString localName;
  readonly attribute DOMString name;
  [CEReactions] attribute DOMString value;

  readonly attribute Element? ownerElement;

  readonly attribute boolean specified; // historical; always returns true
};
[Exposed=Window]
interface CharacterData : Node {
  attribute [LegacyNullToEmptyString] DOMString data;
  readonly attribute unsigned long length;
  DOMString substringData(unsigned long offset, unsigned long count);
  undefined appendData(DOMString data);
  undefined insertData(unsigned long offset, DOMString data);
  undefined deleteData(unsigned long offset, unsigned long count);
  undefined replaceData(unsigned long offset, unsigned long count, DOMString data);
};

[Exposed=Window]
interface Text : CharacterData {
  constructor(optional DOMString data = "");

  [NewObject] Text splitText(unsigned long offset);
  readonly attribute DOMString wholeText;
};

[Exposed=Window]
interface CDATASection : Text {
};
[Exposed=Window]
interface ProcessingInstruction : CharacterData {
  constructor(DOMString target, optional DOMString data = "");

  readonly attribute DOMString target;

  boolean hasAttributes();
  sequence<DOMString> getAttributeNames();
  DOMString? getAttribute(DOMString name);
  undefined setAttribute(DOMString name, DOMString value);
  undefined removeAttribute(DOMString name);
  boolean toggleAttribute(DOMString name, optional boolean force);
  boolean hasAttribute(DOMString name);
};
[Exposed=Window]
interface Comment : CharacterData {
  constructor(optional DOMString data = "");
};

[Exposed=Window]
interface AbstractRange {
  readonly attribute Node startContainer;
  readonly attribute unsigned long startOffset;
  readonly attribute Node endContainer;
  readonly attribute unsigned long endOffset;
  readonly attribute boolean collapsed;
};

dictionary StaticRangeInit {
  required Node startContainer;
  required unsigned long startOffset;
  required Node endContainer;
  required unsigned long endOffset;
};

[Exposed=Window]
interface StaticRange : AbstractRange {
  constructor(StaticRangeInit init);
};

[Exposed=Window]
interface Range : AbstractRange {
  constructor();

  readonly attribute Node commonAncestorContainer;

  undefined setStart(Node node, unsigned long offset);
  undefined setEnd(Node node, unsigned long offset);
  undefined setStartBefore(Node node);
  undefined setStartAfter(Node node);
  undefined setEndBefore(Node node);
  undefined setEndAfter(Node node);
  undefined collapse(optional boolean toStart = false);
  undefined selectNode(Node node);
  undefined selectNodeContents(Node node);

  const unsigned short START_TO_START = 0;
  const unsigned short START_TO_END = 1;
  const unsigned short END_TO_END = 2;
  const unsigned short END_TO_START = 3;
  short compareBoundaryPoints(unsigned short how, Range sourceRange);

  [CEReactions] undefined deleteContents();
  [CEReactions, NewObject] DocumentFragment extractContents();
  [CEReactions, NewObject] DocumentFragment cloneContents();
  [CEReactions] undefined insertNode(Node node);
  [CEReactions] undefined surroundContents(Node newParent);

  [NewObject] Range cloneRange();
  undefined detach();

  boolean isPointInRange(Node node, unsigned long offset);
  short comparePoint(Node node, unsigned long offset);

  boolean intersectsNode(Node node);

  stringifier;
};

[Exposed=Window]
interface NodeIterator {
  [SameObject] readonly attribute Node root;
  readonly attribute Node referenceNode;
  readonly attribute boolean pointerBeforeReferenceNode;
  readonly attribute unsigned long whatToShow;
  readonly attribute NodeFilter? filter;

  Node? nextNode();
  Node? previousNode();

  undefined detach();
};

[Exposed=Window]
interface TreeWalker {
  [SameObject] readonly attribute Node root;
  readonly attribute unsigned long whatToShow;
  readonly attribute NodeFilter? filter;
           attribute Node currentNode;

  Node? parentNode();
  Node? firstChild();
  Node? lastChild();
  Node? previousSibling();
  Node? nextSibling();
  Node? previousNode();
  Node? nextNode();
};
[Exposed=Window]
callback interface NodeFilter {
  // Constants for acceptNode()
  const unsigned short FILTER_ACCEPT = 1;
  const unsigned short FILTER_REJECT = 2;
  const unsigned short FILTER_SKIP = 3;

  // Constants for whatToShow
  const unsigned long SHOW_ALL = 0xFFFFFFFF;
  const unsigned long SHOW_ELEMENT = 0x1;
  const unsigned long SHOW_ATTRIBUTE = 0x2;
  const unsigned long SHOW_TEXT = 0x4;
  const unsigned long SHOW_CDATA_SECTION = 0x8;
  const unsigned long SHOW_ENTITY_REFERENCE = 0x10; // legacy
  const unsigned long SHOW_ENTITY = 0x20; // legacy
  const unsigned long SHOW_PROCESSING_INSTRUCTION = 0x40;
  const unsigned long SHOW_COMMENT = 0x80;
  const unsigned long SHOW_DOCUMENT = 0x100;
  const unsigned long SHOW_DOCUMENT_TYPE = 0x200;
  const unsigned long SHOW_DOCUMENT_FRAGMENT = 0x400;
  const unsigned long SHOW_NOTATION = 0x800; // legacy

  unsigned short acceptNode(Node node);
};

[Exposed=Window]
interface DOMTokenList {
  readonly attribute unsigned long length;
  getter DOMString? item(unsigned long index);
  boolean contains(DOMString token);
  [CEReactions] undefined add(DOMString... tokens);
  [CEReactions] undefined remove(DOMString... tokens);
  [CEReactions] boolean toggle(DOMString token, optional boolean force);
  [CEReactions] boolean replace(DOMString token, DOMString newToken);
  boolean supports(DOMString token);
  [CEReactions] stringifier attribute DOMString value;
  iterable<DOMString>;
};

[Exposed=Window]
interface XPathResult {
  const unsigned short ANY_TYPE = 0;
  const unsigned short NUMBER_TYPE = 1;
  const unsigned short STRING_TYPE = 2;
  const unsigned short BOOLEAN_TYPE = 3;
  const unsigned short UNORDERED_NODE_ITERATOR_TYPE = 4;
  const unsigned short ORDERED_NODE_ITERATOR_TYPE = 5;
  const unsigned short UNORDERED_NODE_SNAPSHOT_TYPE = 6;
  const unsigned short ORDERED_NODE_SNAPSHOT_TYPE = 7;
  const unsigned short ANY_UNORDERED_NODE_TYPE = 8;
  const unsigned short FIRST_ORDERED_NODE_TYPE = 9;

  readonly attribute unsigned short resultType;
  readonly attribute unrestricted double numberValue;
  readonly attribute DOMString stringValue;
  readonly attribute boolean booleanValue;
  readonly attribute Node? singleNodeValue;
  readonly attribute boolean invalidIteratorState;
  readonly attribute unsigned long snapshotLength;

  Node? iterateNext();
  Node? snapshotItem(unsigned long index);
};

[Exposed=Window]
interface XPathExpression {
  // XPathResult.ANY_TYPE = 0
  XPathResult evaluate(Node contextNode, optional unsigned short type = 0, optional XPathResult? result = null);
};

callback interface XPathNSResolver {
  DOMString? lookupNamespaceURI(DOMString? prefix);
};

interface mixin XPathEvaluatorBase {
  [NewObject] XPathExpression createExpression(DOMString expression, optional XPathNSResolver? resolver = null);
  Node createNSResolver(Node nodeResolver); // legacy
  // XPathResult.ANY_TYPE = 0
  XPathResult evaluate(DOMString expression, Node contextNode, optional XPathNSResolver? resolver = null, optional unsigned short type = 0, optional XPathResult? result = null);
};
Document includes XPathEvaluatorBase;

[Exposed=Window]
interface XPathEvaluator {
  constructor();
};

XPathEvaluator includes XPathEvaluatorBase;

[Exposed=Window]
interface XSLTProcessor {
  constructor();
  undefined importStylesheet(Node style);
  [CEReactions] DocumentFragment transformToFragment(Node source, Document output);
  [CEReactions] Document transformToDocument(Node source);
  undefined setParameter([LegacyNullToEmptyString] DOMString namespaceURI, DOMString localName, any value);
  any getParameter([LegacyNullToEmptyString] DOMString namespaceURI, DOMString localName);
  undefined removeParameter([LegacyNullToEmptyString] DOMString namespaceURI, DOMString localName);
  undefined clearParameters();
  undefined reset();
};


```
