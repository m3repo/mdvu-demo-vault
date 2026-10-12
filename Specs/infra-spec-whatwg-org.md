---
title: Infra Standard
source: https://infra.spec.whatwg.org/
snapshot: https://infra.spec.whatwg.org/commit-snapshots/c67ae1fb1d161b23d0f8c9bf9917ea1993f7b19a/
retrieved: 2026-10-10
converted: 2026-10-10
author: WHATWG
license: CC BY 4.0
tags:
  - spec
  - whatwg
---

# Infra

> [!info] Unofficial copy
> This page is an unofficial, non-normative copy of the [Infra Standard](https://infra.spec.whatwg.org/), based on the [snapshot of commit c67ae1f](https://infra.spec.whatwg.org/commit-snapshots/c67ae1fb1d161b23d0f8c9bf9917ea1993f7b19a/), retrieved on 2026-10-10. It is not reviewed or endorsed by the WHATWG; for the authoritative text see the original.
> 
> Copyright © WHATWG (Apple, Google, Mozilla, Microsoft). Licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
> 
> Changes: converted automatically from HTML to Markdown with mdVü on 2026-10-10; the WHATWG logo and the MDN browser-support boxes were removed, notes, warnings and examples became callouts, relative links and image addresses were made absolute, and links between the HTML, DOM and Infra standards point to the local copies.

Living Standard — Last Updated 5 October 2026

Participate:

[GitHub whatwg/infra](https://github.com/whatwg/infra) ([new issue](https://github.com/whatwg/infra/issues/new/choose), [open issues](https://github.com/whatwg/infra/issues))

[Chat on Matrix](https://whatwg.org/chat)

Commits:

[GitHub whatwg/infra/commits](https://github.com/whatwg/infra/commits)

[Snapshot as of this commit](https://infra.spec.whatwg.org/commit-snapshots/c67ae1fb1d161b23d0f8c9bf9917ea1993f7b19a/)

Tests:

[web-platform-tests infra/](https://github.com/web-platform-tests/wpt/tree/master/infra) ([ongoing work](https://github.com/web-platform-tests/wpt/labels/infra))

Translations (non-normative):

[日本語](https://triple-underscore.github.io/infra-ja.html)

[简体中文](https://htmlspecs.com/infra/)

[한국어](https://ko.htmlspecs.com/infra/)

## Abstract

The Infra Standard aims to define the fundamental concepts upon which standards are built.

## Table of Contents
1. [Goals](#goals)
2. [1 Usage](#1-usage)
3. [2 Conventions](#2-conventions)
   1. [2.1 Conformance](#21-conformance)
   2. [2.2 Compliance with other specifications](#22-compliance-with-other-specifications)
   3. [2.3 Terminology](#23-terminology)
   4. [2.4 Privacy concerns](#24-privacy-concerns)
4. [3 Algorithms](#3-algorithms)
   1. [3.1 Conformance](#31-conformance)
   2. [3.2 Avoid limits on algorithm inputs](#32-avoid-limits-on-algorithm-inputs)
   3. [3.3 Declaration](#33-declaration)
   4. [3.4 Parameters](#34-parameters)
   5. [3.5 Variables](#35-variables)
   6. [3.6 Control flow](#36-control-flow)
   7. [3.7 Conditional abort](#37-conditional-abort)
   8. [3.8 Conditional statements](#38-conditional-statements)
   9. [3.9 Iteration](#39-iteration)
   10. [3.10 Assertions](#310-assertions)
   11. [3.11 Identity and equality](#311-identity-and-equality)
5. [4 Primitive data types](#4-primitive-data-types)
   1. [4.1 Nulls](#41-nulls)
   2. [4.2 Booleans](#42-booleans)
   3. [4.3 Numbers](#43-numbers)
   4. [4.4 Bytes](#44-bytes)
   5. [4.5 Byte sequences](#45-byte-sequences)
   6. [4.6 Code points](#46-code-points)
   7. [4.7 Strings](#47-strings)
   8. [4.8 Time](#48-time)
   9. [4.9 Singletons](#49-singletons)
6. [5 Data structures](#5-data-structures)
   1. [5.1 Lists](#51-lists)
      1. [5.1.1 Stacks](#511-stacks)
      2. [5.1.2 Queues](#512-queues)
      3. [5.1.3 Sets](#513-sets)
   2. [5.2 Maps](#52-maps)
   3. [5.3 Structs](#53-structs)
      1. [5.3.1 Tuples](#531-tuples)
7. [6 JSON](#6-json)
8. [7 Forgiving base64](#7-forgiving-base64)
9. [8 Namespaces](#8-namespaces)
10. [Acknowledgments](#acknowledgments)
11. [Intellectual property rights](#intellectual-property-rights)
12. [Index](#index)
    1. [Terms defined by this specification](#terms-defined-by-this-specification)
    2. [Terms defined by reference](#terms-defined-by-reference)
13. [References](#references)
    1. [Normative References](#normative-references)
    2. [Non-Normative References](#non-normative-references)

## Goals
- Deduplicate boilerplate in standards.
- Align standards on conventions, terminology, and data structures.
- Be a place for concepts used by multiple standards without a good home.
- Help write clear and readable algorithmic prose by clarifying otherwise ambiguous concepts.

Suggestions for more goals welcome.

## 1. Usage

To make use of this standard in a document titled X, use:

X depends on Infra. [\[Infra\]](#normative-references)

Additionally, cross-referencing all terminology is strongly encouraged to avoid ambiguity.

## 2. Conventions

### 2.1. Conformance

All assertions, diagrams, examples, and notes are non-normative, as are all sections explicitly marked non-normative. Everything else is normative.

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" are to be interpreted as described in RFC 2119. [\[RFC2119\]](#normative-references)

These keywords have equivalent meaning when written in lowercase and cannot appear in non-normative content.

> [!note]
> This is a [willful violation](#22-compliance-with-other-specifications) of RFC 8174, motivated by legibility and a desire to preserve long-standing practice in many non-IETF-published pre-RFC 8174 documents. [\[RFC8174\]](#non-normative-references)

All of the above is applicable to both this standard and any document that uses this standard. Documents using this standard are encouraged to limit themselves to "must", "must not", "should", and "may", and to use these in their lowercase form as that is generally considered to be more readable.

For non-normative content "strongly encouraged", "strongly discouraged", "encouraged", "discouraged", "can", "cannot", "could", "could not", "might", and "might not" can be used instead.

### 2.2. Compliance with other specifications

In general, specifications interact with and rely on a wide variety of other specifications. In certain circumstances, unfortunately, conflicting needs require a specification to violate the requirements of other specifications. When this occurs, a document using the Infra Standard should denote such transgressions as a willful violation, and note the reason for that violation.

> [!example]
> The previous section, [§ 2.1 Conformance](#21-conformance), documents a [willful violation](#22-compliance-with-other-specifications) of RFC 8174 committed by Infra.

### 2.3. Terminology

The word "or", in cases where both inclusive "or" and exclusive "or" are possible (e.g., "if either width or height is zero"), means an inclusive "or" (implying "or both"), unless it is called out as being exclusive (with "but not both").

---

A user agent is any software entity that acts on behalf of a user, for example by retrieving and rendering web content and facilitating end user interaction with it. In specifications using the Infra Standard, the user agent is generally an instance of the client software that implements the specification. The client software itself is known as an implementation. A person can use many different [user agents](#23-terminology) in their day-to-day life, including by configuring an [implementation](#23-terminology) to act as several [user agents](#23-terminology) at once, for example by using multiple profiles or the implementation’s private browsing mode.

If something is said to be implementation-defined, the particulars of what is said to be [implementation-defined](#23-terminology) are up to the [implementation](#23-terminology). In the absence of such language, the reverse holds: [implementations](#23-terminology) have to follow the rules laid out in documents using this standard.

> [!example]
> Insert U+000A (LF) code points into input in an [implementation-defined](#23-terminology) manner such that each resulting line has no more than width code points. For the purposes of this requirement, lines are delimited by the start of input, the end of input, and U+000A (LF).

### 2.4. Privacy concerns

Some features that are defined in documents using the Infra Standard might trade user convenience for a measure of user privacy.

In general, due to the internet’s architecture, a user can be distinguished from another by the user’s IP address. IP addresses do not perfectly match to a user; as a user moves from device to device, or from network to network, their IP address will change; similarly, NAT routing, proxy servers, and shared computers enable packets that appear to all come from a single IP address to actually map to multiple users. Technologies such as onion routing can be used to further anonymize requests so that requests from a single user at one node on the internet appear to come from many disparate parts of the network. [\[RFC791\]](#non-normative-references)

However, the IP address used for a user’s requests is not the only mechanism by which a user’s requests could be related to each other. Cookies, for example, are designed specifically to enable this, and are the basis of most of the web’s session features that enable you to log into a site with which you have an account. More generally, any kind of cache mechanism or shared state, including but not limited to HSTS, the HTTP cache, grouping of connections, storage APIs, can and ought to be expected to be abused. [\[COOKIES\]](#non-normative-references) [\[RFC6797\]](#non-normative-references) [\[STORAGE\]](#non-normative-references)

There are other mechanisms that are more subtle. Certain characteristics of a user’s system can be used to distinguish groups of users from each other. By collecting enough such information, an individual user’s browser’s "digital fingerprint" can be computed, which can be better than an IP address in ascertaining which requests are from the same user.

Grouping requests in this manner, especially across multiple sites, can be used for malevolent purposes, e.g., governments combining information such as the person’s home address (determined from the addresses they use when getting driving directions on one site) with their apparent political affiliations (determined by examining the forum sites that they participate in) to determine whether the person should be prevented from voting in an election.

Since the malevolent purposes can be remarkably evil, user agent implementors and specification authors are strongly encouraged to minimize leaking information that could be used to fingerprint or track a user.

Unfortunately, as the first paragraph in this section implies, sometimes there is great benefit to be derived from exposing APIs that can also be abused for fingerprinting and tracking purposes, so it’s not as easy as blocking all possible leaks. For instance, the ability to log into a site to post under a specific identity requires that the user’s requests be identifiable as all being from the same user, more or less by definition. More subtly, though, information such as how wide text is, which is necessary for many effects that involve drawing text onto a canvas (e.g., any effect that involves drawing a border around the text) also leaks information that can be used to group a user’s requests. (In this case, by potentially exposing, via a brute force search, which fonts a user has installed, information which can vary considerably from user to user.)

[![(This is a tracking vector.)](https://resources.whatwg.org/tracking-vector.svg "There is a tracking vector here.")](#24-privacy-concerns) Features that are defined in documents using the Infra Standard that can be used as a tracking vector are marked as this paragraph is.

Other features in the platform can be used for the same purpose, including, but not limited to:
- The exact list of which features a user agents supports.
- The maximum allowed stack depth for recursion in script.
- Features that describe the user’s environment.
- The user’s time zone.
- HTTP request headers.

## 3. Algorithms

### 3.1. Conformance

Algorithms, and requirements phrased in the imperative as part of algorithms (such as "strip any leading spaces" or "return false") are to be interpreted with the meaning of the keyword (e.g., "must") used in introducing the algorithm or step. If no such keyword is used, must is implied.

> [!example]
> For example, were the spec to say:
> 
> To eat an orange, the user must:
> 1. Peel the orange.
> 2. Separate each slice of the orange.
> 3. Eat the orange slices.
> 
> it would be equivalent to the following:
> 
> To eat an orange:
> 1. The user must peel the orange.
> 2. The user must separate each slice of the orange.
> 3. The user must eat the orange slices.
> 
> Here the key word is "must".
> 
> Modifying the above example, if the algorithm was introduced only with "To eat an orange:", it would still have the same meaning, as "must" is implied.

Conformance requirements phrased as algorithms or specific steps may be implemented in any manner, so long as the end result is equivalent. (In particular, the algorithms are intended to be easy to follow, and not intended to be performant.)

> [!note]
> Performance is tricky to get correct as it is influenced by user perception, computer architectures, and different types of input that can change over time in how common they are. For instance, a JavaScript engine likely has many different code paths for what is standardized as a single algorithm, in order to optimize for speed or memory consumption. Standardizing all those code paths would be an insurmountable task and not productive as they would not stand the test of time as well as the single algorithm would. Therefore performance is best left as a field to compete over.

### 3.2. Avoid limits on algorithm inputs

A document using the Infra Standard generally should not enforce specific limits on algorithm inputs with regards to their size, resource usage, or equivalent. This allows for competition among user agents and avoids constraining the potential computing needs of the future.

[![(This is a tracking vector.)](https://resources.whatwg.org/tracking-vector.svg "There is a tracking vector here.")](#24-privacy-concerns) Nevertheless, user agents may impose [implementation-defined](#23-terminology) limits on otherwise unconstrained inputs. E.g., to prevent denial of service attacks, to guard against running out of memory, or to work around platform-specific limitations.

> [!note]
> Global resource limits can be used as side channels through a variant on a resource exhaustion attack, whereby the attacker can observe whether a victim application reaches the global limit. Limits could also be used to fingerprint the user agent, but only if they make the user agent more unique in some manner, e.g., if they are specific to the underlying hardware.

> [!example]
> An API that allows creating an in-memory bitmap might be specified to allow any dimensions, or any dimensions up to some large limit like JavaScript’s `Number.MAX_SAFE_INTEGER`. However, implementations can choose to impose some [implementation-defined](#23-terminology) (and thus not specified) limit on the dimensions, instead of attempting to allocate huge amounts of memory.

> [!example]
> A programming language might not have a maximum call stack size specified. However, implementations could choose to impose one for practical reasons.

As code can end up depending on a particular limit, it can be useful to define a limit for interoperability. Sometimes, embracing that is not problematic for the future, and can make the code run in more user agents.

It can also be useful to constrain an [implementation-defined](#23-terminology) limit with a lower limit. I.e., ensuring all implementations can handle inputs of a given minimum size.

### 3.3. Declaration

Algorithm names are usually verb phrases, but sometimes are given names that emphasize their standalone existence, so that standards and readers can refer to the algorithm more idiomatically.

> [!example]
> Some algorithm names in the latter category include "attribute change steps", "internal module script graph fetching procedure", and "overload resolution algorithm".

Declare algorithms by stating their name, parameters, and return type, in the following form:

To \[algorithm name\], given a \[type1\] \[parameter1\], a \[type2\] \[parameter2\], …, perform the following steps. They return a \[return type\].

(For non-verb phrase algorithm names, use "To perform the \[algorithm name\]…". See also [§ 3.4 Parameters](#34-parameters) for more complicated parameter-declaration forms.)

> [!example]
> To parse an awesome format given a [byte sequence](#45-byte-sequences) bytes, perform the following steps. They return a [string](#47-strings) or null.

Algorithms which do not return a value use a shorter form. This same shorter form can be used even for algorithms that do return a value if the return type is relatively easy to infer from the algorithm steps:

To \[algorithm name\], given a \[type1\] \[parameter1\], a \[type2\] \[parameter2\], …:

> [!example]
> To parse an awesome format given a [byte sequence](#45-byte-sequences) bytes:

Very short algorithms can be declared and specified using a single sentence:

> [!example]
> To parse an awesome format given a [byte sequence](#45-byte-sequences) bytes, return the result of [ASCII uppercasing](#47-strings) the [isomorphic decoding](#45-byte-sequences) of bytes.

Types should be included in algorithm declarations, but may be omitted if the parameter name is clear enough, or if they are otherwise clear from context. (For example, because the algorithm is a simple wrapper around another one.)

> [!example]
> To load a classic script given url, return the result of performing the internal script-loading algorithm given url and "`classic`".

### 3.4. Parameters

Algorithm parameters are usually listed sequentially, in the fashion described in [§ 3.3 Declaration](#33-declaration). However, there are some more complicated cases.

Algorithm parameters can be optional, in which case the algorithm declaration must list them as such, and list them after any non-optional parameters. They can either be given a default value, or the algorithm body can check whether or not the argument was given. Concretely, use the following forms:

… an optional \[type\] \[parameter\] …

… an optional \[type\] \[parameter\] (default \[default value\]) …

Optional [boolean](#42-booleans) parameters must have a default value specified, and that default must be false.

> [!example]
> To navigate to a resource resource, with an optional string navigationType and an optional boolean exceptionsEnabled (default false):
> 1. …
> 2. If navigationType was given, then do something with navigationType.
> 3. …

To call algorithms with such optional positional parameters, the optional argument values can be omitted, but only the trailing ones.

> [!example]
> Call sites to the previous example’s algorithm would look like one of:
> - [Navigate](#34-parameters) to resource.
> - [Navigate](#34-parameters) to resource with "`form submission`".
> - [Navigate](#34-parameters) to resource with "`form submission`" and true.
> 
> But, there would be no way to supply a non-default value for the third (exceptionsEnabled) argument, while leaving the second (navigationType) argument as not-given. Additionally, the last of these calls is fairly unclear for readers, as the fact that "true" means "exceptions enabled" requires going back to the algorithm’s declaration and counting parameters. Read on for how to fix these issues!

Optional named parameters, instead of positional ones, can be used to increase clarity and flexibility at the call site. Such parameters are marked up as both variables and definitions, and linked to from their call sites.

> [!example]
> To navigate to a resource resource, with an optional string navigationType and an optional boolean exceptionsEnabled (default false):
> 1. …
> 2. If navigationType was given, then do something with navigationType.
> 3. …
> 
> Call sites would then look like one of:
> - [Navigate](#34-parameters) to resource.
> - [Navigate](#34-parameters) to resource with [*navigationType*](#34-parameters) set to "`form-submission`".
> - [Navigate](#34-parameters) to resource with [*exceptionsEnabled*](#34-parameters) set to true.
> - [Navigate](#34-parameters) to resource with [*navigationType*](#34-parameters) set to "`form-submission`" and [*exceptionsEnabled*](#34-parameters) set to true.

> [!note]
> Note how within the algorithm steps, the argument value is not linked to the parameter declaration; it remains just a variable reference. Linking to the parameter declaration is done only at the call sites.

Non-optional named parameters may also be used, using the same convention of marking them up as both variables and definitions, and linking to them from call sites. This can improve clarity at the call sites.

> [!example]
> [Boolean](#42-booleans) parameters are a case where naming the parameter can be significantly clearer than leaving it as positional, regardless of optionality. See [The Pitfalls of Boolean Trap](https://ariya.io/2011/08/hall-of-api-shame-boolean-trap) for discussion of this in the context of programming languages.

Another complementary technique for improving clarity is to package up related values into a [struct](#53-structs), and pass that struct as a parameter. This is especially applicable when the same set of related values is used as the input to multiple algorithms.

### 3.5. Variables

A variable is declared with "let" and changed with "set".

> [!example]
> Let list be a new [list](#51-lists).

> [!example]
> 1. Let value be null.
> 2. If input is a [string](#47-strings), then set value to input.
> 3. Otherwise, set value to input, [UTF-8 decoded](https://encoding.spec.whatwg.org/#utf-8-decode).
> 4. [Assert](#310-assertions): value is a [string](#47-strings).

> [!example]
> Let activationTarget be target if isActivationEvent is true and target has activation behavior; otherwise null.

Variables must not be used before they are declared. Variables are [block scoped](<https://en.wikipedia.org/wiki/Scope_(computer_science)#Block_scope>). Variables must not be declared more than once per algorithm.

A multiple assignment syntax can be used to assign multiple variables to the [tuple](#531-tuples)’s [items](#53-structs), by surrounding the variable names with U+0028 LEFT PARENTHESIS and U+0029 RIGHT PARENTHESIS, and separating each variable name with U+002C (,). The number of variables assigned cannot differ from the number of [items](#53-structs) in the [tuple](#531-tuples).

> [!example]
> 1. Let statusInstance be the status (200, \``OK`\`).
> 2. Let (status, statusMessage) be statusInstance.
> 
> Assigning status and statusMessage could be written as two separate steps that use an index or [name](#53-structs) to access the [tuple](#531-tuples)’s [items](#53-structs).

### 3.6. Control flow

The control flow of algorithms is such that a requirement to "return" or "throw" terminates the algorithm the statement was in. "Return" will hand the given value, if any, to its caller. "Throw" will make the caller automatically rethrow the given value, if any, and thereby terminate the caller’s algorithm. Using prose the caller has the ability to "catch" the exception and perform another action.

### 3.7. Conditional abort

Sometimes it is useful to stop performing a series of steps once a condition becomes true.

To do this, state that a given series of steps will abort when a specific condition is reached. This indicates that the specified steps must be evaluated, not as-written, but by additionally inserting a step before each of them that evaluates condition, and if condition evaluates to true, skips the remaining steps.

In such algorithms, the subsequent step can be annotated to run if aborted, in which case it must run if any of the preceding steps were skipped due to the condition of the preceding [abort when](#37-conditional-abort) step evaluated to true.

> [!example]
> The following algorithm
> 1. Let result be an empty [list](#51-lists).
> 2. Run these steps, but [abort when](#37-conditional-abort) the user clicks the "Cancel" button:
>    1. Compute the first million digits of π, and [append](#51-lists) the result to result.
>    2. Compute the first million digits of e, and [append](#51-lists) the result to result.
>    3. Compute the first million digits of φ, and [append](#51-lists) the result to result.
> 3. [If aborted](#37-conditional-abort), [append](#51-lists) "`Didn’t finish!`" to result.
> 
> is equivalent to the more verbose formulation
> 1. Let result be an empty [list](#51-lists).
> 2. If the user has not clicked the "Cancel" button:
>    1. Compute the first million digits of π, and [append](#51-lists) the result to result.
>    2. If the user has not clicked the "Cancel" button:
>       1. Compute the first million digits of e, and [append](#51-lists) the result to result.
>       2. If the user has not clicked the "Cancel" button, then compute the first million digits of φ, and [append](#51-lists) the result to result.
> 3. If the user clicked the "Cancel" button, then [append](#51-lists) "`Didn’t finish!`" to result.

> [!note]
> Whenever this construct is used, implementations are allowed to evaluate condition during the specified steps rather than before and after each step, as long as the end result is indistinguishable. For instance, as long as result in the above example is not mutated during a compute operation, the user agent could stop the computation.

### 3.8. Conditional statements

Algorithms with conditional statements should use the keywords "if", "then", and "otherwise".

> [!example]
> 1. Let value be null.
> 2. If input is a [string](#47-strings), then set value to input.
> 3. Return value.

Once the keyword "otherwise" is used, the keyword "then" is omitted.

> [!example]
> 1. Let value be null.
> 2. If input is a [string](#47-strings), then set value to input.
> 3. Otherwise, set value to failure.
> 4. Return value.

> [!example]
> 1. Let value be null.
> 2. If input is a [string](#47-strings), then set value to input.
> 3. Otherwise, if input is a [list](#51-lists) of [strings](#47-strings), set value to input\[0\].
> 4. Otherwise, throw a [`TypeError`](https://webidl.spec.whatwg.org/#exceptiondef-typeerror).
> 5. Return value.

### 3.9. Iteration

There’s a variety of ways to repeat a set of steps until a condition is reached.

> [!note]
> The Infra Standard is not (yet) exhaustive on this; please file an issue if you need something.

For each

As defined for [lists](#51-lists) (and derivatives) and [maps](#52-maps).

While

An instruction to repeat a set of steps as long as a condition is met.

> [!example]
> While condition is "`met`":
> 1. …

An iteration’s flow can be controlled via requirements to continue or break. [Continue](#39-iteration) will skip over any remaining steps in an iteration, proceeding to the next item. If no further items remain, the iteration will stop. [Break](#39-iteration) will skip over any remaining steps in an iteration, and skip over any remaining items as well, stopping the iteration.

> [!example]
> Let example be the [list](#51-lists) « 1, 2, 3, 4 ». The following prose would perform operation upon 1, then 2, then 3, then 4:
> 1. [For each](#51-lists) item of example:
>    1. Perform operation on item.
> 
> The following prose would perform operation upon 1, then 2, then 4. 3 would be skipped.
> 1. [For each](#51-lists) item of example:
>    1. If item is 3, then [continue](#39-iteration).
>    2. Perform operation on item.
> 
> The following prose would perform operation upon 1, then 2. 3 and 4 would be skipped.
> 1. [For each](#51-lists) item of example:
>    1. If item is 3, then [break](#39-iteration).
>    2. Perform operation on item.

### 3.10. Assertions

To improve readability, it can sometimes help to add assertions to algorithms, stating invariants. To do this, write "Assert:", followed by a statement that must be true. If the statement ends up being false that indicates an issue with the document using the Infra Standard that should be reported and addressed.

> [!note]
> Since the statement can only ever be true, it has no implications for implementations.

> [!example]
> 1. Let x be "`Aperture Science`".
> 2. [Assert](#310-assertions): x is "`Aperture Science`".

### 3.11. Identity and equality

A value a is (or is [identical to](#311-identity-and-equality)) a value b if they are the same value. For values of primitive data types this means that they have the same contents, e.g., two [strings](#47-strings) are identical when they consist of the same sequence of [code units](#47-strings). For values of other data types, such as [lists](#51-lists), [maps](#52-maps), and [structs](#53-structs), this means that they are the same instance; two such values that were created separately are never identical to each other, even if their contents are the same.

A data type has an equality, which is an algorithm that takes two values of that data type and returns a [boolean](#42-booleans). Unless defined otherwise, a data type’s [equality](#311-identity-and-equality) returns true if the two values are [identical to](#311-identity-and-equality) each other; otherwise false. This standard defines a different [equality](#311-identity-and-equality) for [lists](#51-lists), [maps](#52-maps), and [tuples](#531-tuples).

A value a equals (or is [equal](#311-identity-and-equality) to) a value b if a [is](#311-identity-and-equality) b, or if a and b are of the same data type and that data type’s [equality](#311-identity-and-equality) returns true given a and b.

> [!example]
> A key value is an example [tuple](#531-tuples) consisting of a key (a [string](#47-strings)) and a value (a [list](#51-lists) of numbers).
> 1. Let original be the key value ("`x`", « 1, 2, 3, 4 »).
> 2. Let alsoOriginal be original.
> 3. Let copy be the key value ("`x`", « 1, 2, 3, 4 »).
> 4. [Assert](#310-assertions): original [is](#311-identity-and-equality) alsoOriginal.
> 5. [Assert](#310-assertions): original [is](#311-identity-and-equality) not copy.
> 6. [Assert](#310-assertions): original [equals](#311-identity-and-equality) copy, as their keys are [identical to](#311-identity-and-equality) each other and their values are [equal](#311-identity-and-equality).
> 
> As the [equality](#311-identity-and-equality) of [lists](#51-lists), [maps](#52-maps), and [tuples](#531-tuples) compares their contents using [equals](#311-identity-and-equality), comparing values that contain themselves, directly or indirectly, is to be avoided, as it can result in an infinite loop:
> 1. Let a be « ».
> 2. [Append](#51-lists) a to a.
> 3. Let b be « ».
> 4. [Append](#51-lists) b to b.
> 5. If a [equals](#311-identity-and-equality) b, then …
> 
> The last step never finishes: a and b are not [identical to](#311-identity-and-equality) each other and have the same [size](#51-lists), so determining whether they are [equal](#311-identity-and-equality) requires determining whether a\[0\] [equals](#311-identity-and-equality) b\[0\], which is the same question, as a\[0\] [is](#311-identity-and-equality) a and b\[0\] [is](#311-identity-and-equality) b.

## 4. Primitive data types

### 4.1. Nulls

The value null is used to indicate the lack of a value. It can be used interchangeably with the JavaScript **null** value. [\[ECMA-262\]](#normative-references)

> [!example]
> Let element be null.

> [!example]
> If input is the empty string, then return null.

### 4.2. Booleans

A boolean is either true or false.

> [!example]
> Let elementSeen be false.

### 4.3. Numbers

> [!warning]
> Numbers are complicated; please see [issue #87](https://github.com/whatwg/infra/issues/87). In due course we hope to offer more guidance here around types and mathematical operations. Help appreciated!

---

An 8-bit unsigned integer is an integer in the range 0 to 255 (0 to 28 − 1), inclusive.

A 16-bit unsigned integer is an integer in the range 0 to 65535 (0 to 216 − 1), inclusive.

A 32-bit unsigned integer is an integer in the range 0 to 4294967295 (0 to 232 − 1), inclusive.

A 64-bit unsigned integer is an integer in the range 0 to 18446744073709551615 (0 to 264 − 1), inclusive.

A 128-bit unsigned integer is an integer in the range 0 to 340282366920938463463374607431768211455 (0 to 2128 − 1), inclusive.

> [!example]
> An IPv6 address is an [128-bit unsigned integer](#43-numbers).

---

An 8-bit signed integer is an integer in the range −128 to 127 (−27 to 27 − 1), inclusive.

A 16-bit signed integer is an integer in the range −32768 to 32767 (−215 to 215 − 1), inclusive.

A 32-bit signed integer is an integer in the range −2147483648 to 2147483647 (−231 to 231 − 1), inclusive.

A 64-bit signed integer is an integer in the range −9223372036854775808 to 9223372036854775807 (−263 to 263 − 1), inclusive.

---

Two numbers are [identical to](#311-identity-and-equality) each other if they are the same mathematical value.

### 4.4. Bytes

A byte is a sequence of eight bits and is represented as "`0x`" followed by two [ASCII upper hex digits](#46-code-points), in the range 0x00 to 0xFF, inclusive. A [byte](#44-bytes)’s value is its underlying number.

> [!example]
> 0x40 is a [byte](#44-bytes) whose [value](#44-bytes) is 64.

An ASCII byte is a [byte](#44-bytes) in the range 0x00 (NUL) to 0x7F (DEL), inclusive. As illustrated, an [ASCII byte](#44-bytes), excluding 0x28 and 0x29, may be followed by the representation outlined in the [Standard Code](https://tools.ietf.org/html/rfc20#section-2) section of ASCII format for Network Interchange, between parentheses. [\[RFC20\]](#normative-references)

0x28 may be followed by "(left parenthesis)" and 0x29 by "(right parenthesis)".

> [!example]
> 0x49 (I) when [UTF-8 decoded](https://encoding.spec.whatwg.org/#utf-8-decode) becomes the [code point](#46-code-points) U+0049 (I).

### 4.5. Byte sequences

A byte sequence is a sequence of [bytes](#44-bytes), represented as a space-separated sequence of bytes. Byte sequences with bytes in the range 0x20 (SP) to 0x7E (~), inclusive, can alternately be written as a string, but using backticks instead of quotation marks, to avoid confusion with an actual [string](#47-strings).

> [!example]
> 0x48 0x49 can also be represented as \``HI`\`.
> 
> Headers, such as \``Content-Type`\`, are [byte sequences](#45-byte-sequences).

> [!note]
> To get a [byte sequence](#45-byte-sequences) out of a [string](#47-strings), using [UTF-8 encode](https://encoding.spec.whatwg.org/#utf-8-encode) from Encoding is encouraged. In rare circumstances [isomorphic encode](#47-strings) might be needed. [\[ENCODING\]](#normative-references)

A [byte sequence](#45-byte-sequences)’s length is the number of [bytes](#44-bytes) it contains.

To byte-lowercase a [byte sequence](#45-byte-sequences), increase each [byte](#44-bytes) it contains, in the range 0x41 (A) to 0x5A (Z), inclusive, by 0x20.

To byte-uppercase a [byte sequence](#45-byte-sequences), subtract each [byte](#44-bytes) it contains, in the range 0x61 (a) to 0x7A (z), inclusive, by 0x20.

A [byte sequence](#45-byte-sequences) A is a byte-case-insensitive match for a [byte sequence](#45-byte-sequences) B, if the [byte-lowercase](#45-byte-sequences) of A is the [byte-lowercase](#45-byte-sequences) of B.

Two [byte sequences](#45-byte-sequences) are [identical to](#311-identity-and-equality) each other if they consist of the same sequence of [bytes](#44-bytes).

---

A [byte sequence](#45-byte-sequences) potentialPrefix is a prefix of a [byte sequence](#45-byte-sequences) input if the following steps return true:
1. Let i be 0.
2. [While](#39-iteration) true:
   1. If i is greater than or equal to potentialPrefix’s [length](#45-byte-sequences), then return true.
   2. If i is greater than or equal to input’s [length](#45-byte-sequences), then return false.
   3. Let potentialPrefixByte be the ith [byte](#44-bytes) of potentialPrefix.
   4. Let inputByte be the ith [byte](#44-bytes) of input.
   5. Return false if potentialPrefixByte is not inputByte.
   6. Set i to i + 1.

"input starts with potentialPrefix" can be used as a synonym for "potentialPrefix is a [prefix](#45-byte-sequences) of input".

A [byte sequence](#45-byte-sequences) a is byte less than a [byte sequence](#45-byte-sequences) b if the following steps return true:
1. If b is a [prefix](#45-byte-sequences) of a, then return false.
2. If a is a [prefix](#45-byte-sequences) of b, then return true.
3. Let n be the smallest index such that the nth [byte](#44-bytes) of a is different from the nth byte of b. (There has to be such an index, since neither byte sequence is a prefix of the other.)
4. If the nth byte of a is less than the nth byte of b, then return true.
5. Return false.

---

To isomorphic decode a [byte sequence](#45-byte-sequences) input, return a [string](#47-strings) whose [code point length](#47-strings) is equal to input’s [length](#45-byte-sequences) and whose [code points](#46-code-points) have the same [values](#46-code-points) as the [values](#44-bytes) of input’s [bytes](#44-bytes), in the same order.

### 4.6. Code points

A code point is a Unicode code point and is represented as "U+" followed by four-to-six [ASCII upper hex digits](#46-code-points), in the range U+0000 to U+10FFFF, inclusive. A [code point](#46-code-points)’s value is its underlying number.

A [code point](#46-code-points) may be followed by its name, by its rendered form between parentheses when it is not U+0028 or U+0029, or by both. Documents using the Infra Standard are encouraged to follow [code points](#46-code-points) by their name when they cannot be rendered or are U+0028 or U+0029; otherwise, follow them by their rendered form between parentheses, for legibility.

A [code point](#46-code-points)’s name is defined in Unicode and represented in [ASCII uppercase](#47-strings). [\[UNICODE\]](#normative-references)

> [!example]
> The [code point](#46-code-points) rendered as 🤔 is represented as U+1F914.
> 
> When referring to that [code point](#46-code-points), we might say "U+1F914 (🤔)", to provide extra context. Documents are allowed to use "U+1F914 THINKING FACE (🤔)" as well, though this is somewhat verbose.

> [!example]
> [Code points](#46-code-points) that are difficult to render unambigiously, such as U+000A, can be referred to as "U+000A LF". U+0029 can be referred to as "U+0029 RIGHT PARENTHESIS", because even though it renders, this avoids unmatched parentheses.

[Code points](#46-code-points) are sometimes referred to as [characters](#46-code-points) and in certain contexts are prefixed with "0x" rather than "U+".

A leading surrogate is a [code point](#46-code-points) that is in the range U+D800 to U+DBFF, inclusive.

A trailing surrogate is a [code point](#46-code-points) that is in the range U+DC00 to U+DFFF, inclusive.

A surrogate is a [leading surrogate](#46-code-points) or a [trailing surrogate](#46-code-points).

A scalar value is a [code point](#46-code-points) that is not a [surrogate](#46-code-points).

A noncharacter is a [code point](#46-code-points) that is in the range U+FDD0 to U+FDEF, inclusive, or U+FFFE, U+FFFF, U+1FFFE, U+1FFFF, U+2FFFE, U+2FFFF, U+3FFFE, U+3FFFF, U+4FFFE, U+4FFFF, U+5FFFE, U+5FFFF, U+6FFFE, U+6FFFF, U+7FFFE, U+7FFFF, U+8FFFE, U+8FFFF, U+9FFFE, U+9FFFF, U+AFFFE, U+AFFFF, U+BFFFE, U+BFFFF, U+CFFFE, U+CFFFF, U+DFFFE, U+DFFFF, U+EFFFE, U+EFFFF, U+FFFFE, U+FFFFF, U+10FFFE, or U+10FFFF.

An ASCII code point is a [code point](#46-code-points) in the range U+0000 NULL to U+007F DELETE, inclusive.

An ASCII tab or newline is U+0009 TAB, U+000A LF, or U+000D CR.

ASCII whitespace is U+0009 TAB, U+000A LF, U+000C FF, U+000D CR, or U+0020 SPACE.

> [!note]
> "Whitespace" is a mass noun.

> [!note]
> The XML, JSON, and parts of the HTTP specifications exclude U+000C FF in their definition of whitespace:
> - [XML’s S production](https://www.w3.org/TR/xml/#NT-S)
> - [JSON’s ws production](https://www.rfc-editor.org/info/rfc8259/#section-2)
> - [HTTP whitespace](https://fetch.spec.whatwg.org/#http-whitespace)
> 
> Prefer using Infra’s [ASCII whitespace](#46-code-points) definition for new features, unless your specification deals exclusively with XML/JSON/HTTP.

A C0 control is a [code point](#46-code-points) in the range U+0000 NULL to U+001F INFORMATION SEPARATOR ONE, inclusive.

A C0 control or space is a [C0 control](#46-code-points) or U+0020 SPACE.

A control is a [C0 control](#46-code-points) or a [code point](#46-code-points) in the range U+007F DELETE to U+009F APPLICATION PROGRAM COMMAND, inclusive.

An ASCII digit is a [code point](#46-code-points) in the range U+0030 (0) to U+0039 (9), inclusive.

An ASCII upper hex digit is an [ASCII digit](#46-code-points) or a [code point](#46-code-points) in the range U+0041 (A) to U+0046 (F), inclusive.

An ASCII lower hex digit is an [ASCII digit](#46-code-points) or a [code point](#46-code-points) in the range U+0061 (a) to U+0066 (f), inclusive.

An ASCII hex digit is an [ASCII upper hex digit](#46-code-points) or [ASCII lower hex digit](#46-code-points).

An ASCII upper alpha is a [code point](#46-code-points) in the range U+0041 (A) to U+005A (Z), inclusive.

An ASCII lower alpha is a [code point](#46-code-points) in the range U+0061 (a) to U+007A (z), inclusive.

An ASCII alpha is an [ASCII upper alpha](#46-code-points) or [ASCII lower alpha](#46-code-points).

An ASCII alphanumeric is an [ASCII digit](#46-code-points) or [ASCII alpha](#46-code-points).

### 4.7. Strings

A string is a sequence of [16-bit unsigned integers](#43-numbers), also known as code units. A [string](#47-strings) is also known as a [JavaScript string](#47-strings). [Strings](#47-strings) are denoted by double quotes and monospace font.

> [!example]
> "`Hello, world!`" is a string.

> [!note]
> This is different from how Unicode defines "code unit". In particular it refers exclusively to how Unicode defines it for Unicode 16-bit strings. [\[UNICODE\]](#normative-references)

A [string](#47-strings) can also be interpreted as containing [code points](#46-code-points), per the conversion defined in [The String Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-string-type) section of the JavaScript specification. [\[ECMA-262\]](#normative-references)

> [!note]
> This conversion process converts surrogate pairs into their corresponding [scalar value](#46-code-points) and maps any remaining surrogates to their corresponding [code point](#46-code-points), leaving them effectively as-is.

> [!example]
> A [string](#47-strings) consisting of the [code units](#47-strings) 0xD83D, 0xDCA9, and 0xD800, when interpreted as containing [code points](#46-code-points), would consist of the [code points](#46-code-points) U+1F4A9 and U+D800.

A [string](#47-strings)’s length is the number of [code units](#47-strings) it contains.

A [string](#47-strings)’s code point length is the number of [code points](#46-code-points) it contains.

---

To signify [strings](#47-strings) with additional restrictions on the [code points](#46-code-points) they can contain this specification defines [ASCII strings](#47-strings), [isomorphic strings](#47-strings), and [scalar value strings](#47-strings). Using these improves clarity in specifications.

An ASCII string is a [string](#47-strings) whose [code points](#46-code-points) are all [ASCII code points](#46-code-points).

An isomorphic string is a [string](#47-strings) whose [code points](#46-code-points) are all in the range U+0000 NULL to U+00FF (ÿ), inclusive.

A scalar value string is a [string](#47-strings) whose [code points](#46-code-points) are all [scalar values](#46-code-points).

> [!note]
> A [scalar value string](#47-strings) is useful for any kind of I/O or other kind of operation where [UTF-8 encode](https://encoding.spec.whatwg.org/#utf-8-encode) comes into play.

---

To convert a [string](#47-strings) into a [scalar value string](#47-strings), replace any [surrogates](#46-code-points) with U+FFFD (�).

> [!note]
> The replaced surrogates are never part of surrogate pairs, since the process of interpreting the string as containing [code points](#46-code-points) will have converted surrogate pairs into [scalar values](#46-code-points).
> 
> A [scalar value string](#47-strings) can always be used as a [string](#47-strings) implicitly since every [scalar value string](#47-strings) is a [string](#47-strings). On the other hand, a [string](#47-strings) can only be implicitly used as a [scalar value string](#47-strings) if it is known to not contain [surrogates](#46-code-points); otherwise a [conversion](#47-strings) is to be performed.
> 
> An implementation likely has to perform explicit conversion, depending on how it actually ends up representing [strings](#47-strings) and [scalar value strings](#47-strings). It is fairly typical for implementations to have multiple implementations of [strings](#47-strings) alone for performance and memory reasons.

---

A [string](#47-strings) a is or is [identical to](#47-strings) a [string](#47-strings) b if it consists of the same sequence of [code units](#47-strings).

Except where otherwise stated, all string comparisons use [is](#47-strings).

> [!note]
> This type of [string](#47-strings) comparison was formerly known as a "case-sensitive" comparison in HTML. Strings that compare as [identical to](#47-strings) one another are not only sensitive to case variation (such as UPPER and lower case), but also to other code point encoding choices, such as normalization form or the order of combining marks. Two strings that are visually or even canonically equivalent according to Unicode might still not be [identical to](#47-strings) each other. [\[HTML\]](#non-normative-references) [\[UNICODE\]](#normative-references)

A [string](#47-strings) potentialPrefix is a code unit prefix of a [string](#47-strings) input if the following steps return true:
1. Let i be 0.
2. [While](#39-iteration) true:
   1. If i is greater than or equal to potentialPrefix’s [length](#47-strings), then return true.
   2. If i is greater than or equal to input’s [length](#47-strings), then return false.
   3. Let potentialPrefixCodeUnit be the ith [code unit](#47-strings) of potentialPrefix.
   4. Let inputCodeUnit be the ith [code unit](#47-strings) of input.
   5. Return false if potentialPrefixCodeUnit is not inputCodeUnit.
   6. Set i to i + 1.

When it is clear from context that [code units](#47-strings) are in play, e.g., because one of the strings is a literal containing only characters that are in the range U+0020 SPACE to U+007E (~), "input starts with potentialPrefix" can be used as a synonym for "potentialPrefix is a [code unit prefix](#47-strings) of input".

> [!example]
> With unknown values, it is good to be explicit: targetString is a [code unit prefix](#47-strings) of userInput. But with a literal, we can use plainer language: userInput [starts with](#47-strings) "`!`".

A [string](#47-strings) potentialSuffix is a code unit suffix of a [string](#47-strings) input if the following steps return true:
1. Let i be 1.
2. [While](#39-iteration) true:
   1. Let potentialSuffixIndex be potentialSuffix’s [length](#47-strings) − i.
   2. Let inputIndex be input’s [length](#47-strings) − i.
   3. If potentialSuffixIndex is less than 0, then return true.
   4. If inputIndex is less than 0, then return false.
   5. Let potentialSuffixCodeUnit be the potentialSuffixIndexth [code unit](#47-strings) of potentialSuffix.
   6. Let inputCodeUnit be the inputIndexth [code unit](#47-strings) of input.
   7. Return false if potentialSuffixCodeUnit is not inputCodeUnit.
   8. Set i to i + 1.

When it is clear from context that [code units](#47-strings) are in play, e.g., because one of the strings is a literal containing only characters that are in the range U+0020 SPACE to U+007E (~), "input ends with potentialSuffix" can be used as a synonym for "potentialSuffix is a [code unit suffix](#47-strings) of input".

> [!example]
> With unknown values, it is good to be explicit: targetString is a [code unit suffix](#47-strings) of domain. But with a literal, we can use plainer language: domain [ends with](#47-strings) "`.`".

---

A [string](#47-strings) a is code unit less than a [string](#47-strings) b if the following steps return true:
1. If b is a [code unit prefix](#47-strings) of a, then return false.
2. If a is a [code unit prefix](#47-strings) of b, then return true.
3. Let n be the smallest index such that the nth [code unit](#47-strings) of a is different from the nth code unit of b. (There has to be such an index, since neither string is a prefix of the other.)
4. If the nth code unit of a is less than the nth code unit of b, then return true.
5. Return false.

> [!note]
> This matches the ordering used by JavaScript’s `<` operator, and its [`sort()`](https://tc39.github.io/ecma262/#sec-array.prototype.sort) method on an array of strings. This ordering compares the 16-bit code units in each string, producing a highly efficient, consistent, and deterministic sort order. The resulting ordering will not match any particular alphabet or lexicographic order, particularly for [code points](#46-code-points) represented by a surrogate pair. [\[ECMA-262\]](#normative-references)

> [!example]
> For example, the code point U+FF5E FULLWIDTH TILDE (～) is obviously less than the code point U+1F600 (😀), but the tilde is composed of a single code unit 0xFF5E, while the smiley is composed of two code units 0xD83D and 0XDE00, so the smiley is [code unit less than](#47-strings) the tilde.

---

The code unit substring from start with length length within a [string](#47-strings) string is determined as follows:
1. [Assert](#310-assertions): start and length are nonnegative.
2. [Assert](#310-assertions): start + length is less than or equal to string’s [length](#47-strings).
3. Let result be the empty string.
4. [For each](#51-lists) i of [the range](#513-sets) from start to start + length, exclusive: append the ith [code unit](#47-strings) of string to result.
5. Return result.

The code unit substring from start to end within a [string](#47-strings) string is the [code unit substring](#47-strings) from start with length end − start within string.

The code unit substring from start to the end of a [string](#47-strings) string is the [code unit substring](#47-strings) from start to string’s [length](#47-strings) within string.

> [!example]
> The [code unit substring](#47-strings) from 1 with length 3 within "`Hello world`" is "`ell`". This can also be expressed as the [code unit substring](#47-strings) from 1 to 4.

> [!note]
> The numbers given to these algorithms are best thought of as positions *between* [code units](#47-strings), not indices of the code units themselves. The substring returned is then formed by the code units between these positions. That explains why, for example, the [code unit substring](#47-strings) from 0 to 0 within the empty string is the empty string, even though there is no code unit at index 0 within the empty string.

The code point substring within a [string](#47-strings) string from start with length length is determined as follows:
1. [Assert](#310-assertions): start and length are nonnegative.
2. [Assert](#310-assertions): start + length is less than or equal to string’s [code point length](#47-strings).
3. Let result be the empty string.
4. [For each](#51-lists) i of [the range](#513-sets) from start to start + length, exclusive: append the ith [code point](#46-code-points) of string to result.
5. Return result.

The code point substring from start to end within a [string](#47-strings) string is the [code point substring](#47-strings) within string from start with length end − start.

The code point substring from start to the end of a [string](#47-strings) string is the [code point substring](#47-strings) from start to string’s [code point length](#47-strings) within string.

> [!example]
> Generally, [code unit substring](#47-strings) is used when given developer-supplied positions or lengths, since that is how string indexing works in JavaScript. See, for example, the methods of the [`CharacterData`](dom-spec-whatwg-org.md#410-interface-characterdata) class. [\[DOM\]](#non-normative-references)
> 
> Otherwise, [code point substring](#47-strings) is likely to be better. For example, the [code point substring](#47-strings) from 0 with length 1 within "`👽`" is "`👽`", whereas the [code unit substring](#47-strings) from 0 with length 1 within "`👽`" is the [string](#47-strings) containing the single [surrogate](#46-code-points) U+D83B.

---

To isomorphic encode an [isomorphic string](#47-strings) input: return a [byte sequence](#45-byte-sequences) whose [length](#45-byte-sequences) is equal to input’s [code point length](#47-strings) and whose [bytes](#44-bytes) have the same [values](#44-bytes) as the [values](#46-code-points) of input’s [code points](#46-code-points), in the same order.

---

To ASCII lowercase a [string](#47-strings), replace all [ASCII upper alphas](#46-code-points) in the [string](#47-strings) with their corresponding [code point](#46-code-points) in [ASCII lower alpha](#46-code-points).

To ASCII uppercase a [string](#47-strings), replace all [ASCII lower alphas](#46-code-points) in the [string](#47-strings) with their corresponding [code point](#46-code-points) in [ASCII upper alpha](#46-code-points).

A [string](#47-strings) A is an ASCII case-insensitive match for a [string](#47-strings) B, if the [ASCII lowercase](#47-strings) of A is the [ASCII lowercase](#47-strings) of B.

To ASCII encode an [ASCII string](#47-strings) input: return the [isomorphic encoding](#47-strings) of input.

> [!note]
> [Isomorphic encode](#47-strings) and [UTF-8 encode](https://encoding.spec.whatwg.org/#utf-8-encode) return the same [byte sequence](#45-byte-sequences) for input.

To ASCII decode a [byte sequence](#45-byte-sequences) input, run these steps:
1. [Assert](#310-assertions): all bytes in input are [ASCII bytes](#44-bytes).

   > [!note]
   > Note: This precondition ensures that [isomorphic decode](#45-byte-sequences) and [UTF-8 decode](https://encoding.spec.whatwg.org/#utf-8-decode) return the same [string](#47-strings) for this input.

2. Return the [isomorphic decoding](#45-byte-sequences) of input.

---

To strip newlines from a [string](#47-strings), remove any U+000A LF and U+000D CR [code points](#46-code-points) from the [string](#47-strings).

To normalize newlines in a [string](#47-strings), replace every U+000D CR U+000A LF [code point](#46-code-points) pair with a single U+000A LF [code point](#46-code-points), and then replace every remaining U+000D CR [code point](#46-code-points) with a U+000A LF [code point](#46-code-points).

To strip leading and trailing ASCII whitespace from a [string](#47-strings), remove all [ASCII whitespace](#46-code-points) that are at the start or the end of the [string](#47-strings).

To strip and collapse ASCII whitespace in a [string](#47-strings), replace any sequence of one or more consecutive [code points](#46-code-points) that are [ASCII whitespace](#46-code-points) in the [string](#47-strings) with a single U+0020 SPACE [code point](#46-code-points), and then remove any leading and trailing [ASCII whitespace](#46-code-points) from that string.

---

To collect a sequence of [code points](#46-code-points) meeting a condition condition from a [string](#47-strings) input, given a position variable position tracking the position of the calling algorithm within input:
1. Let result be the empty [string](#47-strings).
2. While position doesn’t point past the end of input and the [code point](#46-code-points) at position within input meets the condition condition:
   1. Append that [code point](#46-code-points) to the end of result.
   2. Advance position by 1.
3. Return result.

> [!note]
> In addition to returning the collected [code points](#46-code-points), this algorithm updates the [position variable](#47-strings) in the calling algorithm.

To skip ASCII whitespace within a [string](#47-strings) input given a [position variable](#47-strings) position, [collect a sequence of code points](#47-strings) that are [ASCII whitespace](#46-code-points) from input given position. The collected [code points](#46-code-points) are not used, but position is still updated.

---

To strictly split a [string](#47-strings) input on a particular delimiter [code point](#46-code-points) delimiter:
1. Let position be a [position variable](#47-strings) for input, initially pointing at the start of input.
2. Let tokens be a [list](#51-lists) of [strings](#47-strings), initially empty.
3. Let token be the result of [collecting a sequence of code points](#47-strings) that are not equal to delimiter from input, given position.
4. [Append](#51-lists) token to tokens.
5. While position is not past the end of input:
   1. [Assert](#310-assertions): the [code point](#46-code-points) at position within input is delimiter.
   2. Advance position by 1.
   3. Let token be the result of [collecting a sequence of code points](#47-strings) that are not equal to delimiter from input, given position.
   4. [Append](#51-lists) token to tokens.
6. Return tokens.

> [!note]
> This algorithm is a "strict" split, as opposed to the commonly-used variants [for ASCII whitespace](#47-strings) and [for commas](#47-strings) below, which are both more lenient in various ways involving interspersed [ASCII whitespace](#46-code-points).

To split a [string](#47-strings) input on ASCII whitespace:
1. Let position be a [position variable](#47-strings) for input, initially pointing at the start of input.
2. Let tokens be a [list](#51-lists) of [strings](#47-strings), initially empty.
3. [Skip ASCII whitespace](#47-strings) within input given position.
4. While position is not past the end of input:
   1. Let token be the result of [collecting a sequence of code points](#47-strings) that are not [ASCII whitespace](#46-code-points) from input, given position.
   2. [Append](#51-lists) token to tokens.
   3. [Skip ASCII whitespace](#47-strings) within input given position.
5. Return tokens.

To split a [string](#47-strings) input on commas:
1. Let position be a [position variable](#47-strings) for input, initially pointing at the start of input.
2. Let tokens be a [list](#51-lists) of [strings](#47-strings), initially empty.
3. While position is not past the end of input:
   1. Let token be the result of [collecting a sequence of code points](#47-strings) that are not U+002C (,) from input, given position.

      > [!note]
      > token might be the empty string.

   2. [Strip leading and trailing ASCII whitespace](#47-strings) from token.
   3. [Append](#51-lists) token to tokens.
   4. If position is not past the end of input:
      1. [Assert](#310-assertions): the [code point](#46-code-points) at position within input is U+002C (,).
      2. Advance position by 1.

4. Return tokens.

To concatenate a [list](#51-lists) of [strings](#47-strings) list, using an optional separator string separator, run these steps:
1. If list [is empty](#51-lists), then return the empty string.
2. If separator is not given, then set separator to the empty string.
3. Return a [string](#47-strings) whose contents are list’s [items](#51-lists), in order, separated from each other by separator.

> [!example]
> To serialize a set set, return the [concatenation](#47-strings) of set using U+0020 SPACE.

### 4.8. Time

Represent time using the [moment](https://w3c.github.io/hr-time/#dfn-moment) and [duration](https://w3c.github.io/hr-time/#dfn-duration) specification types. Follow the advice in [High Resolution Time § 3 Tools for Specification Authors](https://w3c.github.io/hr-time/#sec-tools) when creating these and exchanging them with JavaScript. [\[HR-TIME\]](#normative-references)

### 4.9. Singletons

The following types can be used as inputs or outputs of algorithmic prose to improve comprehension. They have no observable representation beyond their effect on the flow of any given algorithm, and they can only be compared with "is".

allowed

Indicates that some operation is permitted, often used in opposition to [blocked](#49-singletons).

blocked

Indicates that some operation is not permitted, often used in opposition to [allowed](#49-singletons).

failure

Indicates that some operation did not proceed as expected, often used in opposition to [success](#49-singletons) or in combination with a more concrete type.

success

Indicates that some operation proceeded as expected, often used in opposition to [failure](#49-singletons).

> [!example]
> The following algorithm returns [success](#49-singletons) or [failure](#49-singletons):
> 1. If something unexpectedly bad happened, then return [failure](#49-singletons).
> 2. Return [success](#49-singletons).
> 
> Callers of that algorithm might evaluate the result as follows:
> 1. If result is [failure](#49-singletons), then shut everything down gracefully and abort.
> 2. [Assert](#310-assertions): result is [success](#49-singletons).
> 3. …

> [!example]
> [Failure](#49-singletons) is often used as the result of an algorithm that can fail or return a value:
> 1. If status is less than 200 or greater than 599, then return [failure](#49-singletons).
> 2. Return status.

## 5. Data structures

Conventionally, specifications have operated on a variety of vague specification-level data structures, based on shared understanding of their semantics. This generally works well, but can lead to ambiguities around edge cases, such as iteration order or what happens when you [append](#513-sets) an [item](#51-lists) to an [ordered set](#513-sets) that the set already [contains](#51-lists). It has also led to a variety of divergent notation and phrasing, especially around more complex data structures such as [maps](#52-maps).

This standard provides a small set of common data structures, along with notation and phrasing for working with them, in order to create common ground.

### 5.1. Lists

A list is a specification type consisting of a finite ordered sequence of items.

For notational convenience, a literal syntax can be used to express [lists](#51-lists), by surrounding the list with U+00AB («) and U+00BB (»), and separating its [items](#51-lists) with U+002C (,). An indexing syntax can be used by providing a zero-based index into a list inside square brackets. The index cannot be out-of-bounds, except when used with [exists](#51-lists).

> [!example]
> Let example be the [list](#51-lists) « "`a`", "`b`", "`c`", "`a`" ». Then example\[1\] is the [string](#47-strings) "`b`".

For notational convenience, a multiple assignment syntax may be used to assign multiple variables to the [list](#51-lists)’s [items](#51-lists), by surrounding the variables to be assigned with U+00AB («) and U+00BB (») (same as lists), and separating each variable name with U+002C (,). The [list](#51-lists)’s [size](#51-lists) must be the same as the number of variables to be assigned. Each variable given is then set to the value of the [list](#51-lists)’s [item](#51-lists) at the corresponding index.

> [!example]
> 1. Let value be the [list](#51-lists) « "`a`", "`b`", "`c`" ».
> 2. Let « a, b, c » be value.
> 3. [Assert](#310-assertions): a is "`a`".
> 4. [Assert](#310-assertions): b is "`b`".
> 5. [Assert](#310-assertions): c is "`c`".

When a [list](#51-lists)’s contents are not fully controlled, as is the case for lists from user input, the [list](#51-lists)’s [size](#51-lists) should be checked to ensure it is the expected size before list multiple assignment syntax is used.

> [!example]
> 1. If list’s [size](#51-lists) is not `3`, then return failure.
> 2. Let « a, b, c » be list.

A [list](#51-lists)’s [equality](#311-identity-and-equality), given [lists](#51-lists) a and b, returns true if a’s [size](#51-lists) is b’s [size](#51-lists) and a\[i\] [equals](#311-identity-and-equality) b\[i\] for each i of a’s [indices](#51-lists); otherwise false.

---

To append to a [list](#51-lists) that is not an [ordered set](#513-sets) is to add the given [item](#51-lists) to the end of the list.

To extend a [list](#51-lists) that is not an [ordered set](#513-sets) A with a [list](#51-lists) B, [for each](#51-lists) item of B, [append](#51-lists) item to A.

> [!example]
> 1. Let ghostbusters be « "`Erin Gilbert`", "`Abby Yates`" ».
> 2. [Extend](#51-lists) ghostbusters with « "`Jillian Holtzmann`", "`Patty Tolan`" ».
> 3. [Assert](#310-assertions): ghostbusters’s [size](#51-lists) is 4.
> 4. [Assert](#310-assertions): ghostbusters\[2\] is "`Jillian Holtzmann`".

To prepend to a [list](#51-lists) that is not an [ordered set](#513-sets) is to add the given [item](#51-lists) to the beginning of the list.

To replace within a [list](#51-lists) that is not an [ordered set](#513-sets) is to replace all items from the list that match a given condition with the given [item](#51-lists), or do nothing if none do.

> [!note]
> The above definitions are modified when the [list](#51-lists) is an [ordered set](#513-sets); see below for [ordered set append](#513-sets), [prepend](#513-sets), and [replace](#513-sets).

To insert an [item](#51-lists) into a [list](#51-lists) before an index is to add the given item to the list between the given index − 1 and the given index. If the given index is 0, then [prepend](#51-lists) the given item to the list.

To remove zero or more [items](#51-lists) from a [list](#51-lists):
1. Let sizeBefore be list’s [size](#51-lists).
2. Remove all items from the list that match a given condition, or do nothing if none do.
3. Return true if list’s [size](#51-lists) is less than sizeBefore; otherwise false.

> [!example]
> [Removing](#51-lists) x from the [list](#51-lists) « x, y, z, x » is to remove all items from the list that are equal to x. The list now is equivalent to « y, z ».
> 
> [Removing](#51-lists) all items that start with the [string](#47-strings) "`a`" from the [list](#51-lists) « "`a`", "`b`", "`ab`", "`ba`" » is to remove the items "`a`" and "`ab`". The list is now equivalent to « "`b`", "`ba`" ».

To empty a [list](#51-lists) is to [remove](#51-lists) all of its [items](#51-lists).

A [list](#51-lists) contains an [item](#51-lists) if one of the list’s [items](#51-lists) [equals](#311-identity-and-equality) that item. We can also denote this by saying that, for a [list](#51-lists) list and an index index, "list\[index\] [exists](#51-lists)".

A [list](#51-lists)’s size is the number of [items](#51-lists) the list [contains](#51-lists).

A [list](#51-lists) is empty if its [size](#51-lists) is zero.

To get the indices of a [list](#51-lists), return [the range](#513-sets) from 0 to the list’s [size](#51-lists), exclusive.

To iterate over a [list](#51-lists), performing a set of steps on each [item](#51-lists) in order, use phrasing of the form "[For each](#51-lists) item of list", and then operate on item in the subsequent prose.

To slice a [list](#51-lists) list, with an optional integer from (default 0) and an optional integer to (default list’s [size](#51-lists)), perform the following steps. They return a [list](#51-lists) of the same designation as list.
1. [Assert](#310-assertions): from is greater than or equal to 0.
2. [Assert](#310-assertions): to is less than or equal to list’s [size](#51-lists).
3. [Assert](#310-assertions): to is greater than or equal to from.
4. Let slice be a new [list](#51-lists) of the same designation as list.
5. [For each](#51-lists) i of [the range](#513-sets) from to to, exclusive: [append](#51-lists) list\[i\] to slice.
6. Return slice.

To check if a [list](#51-lists) list has duplicates:
1. Let seenItems be « ».
2. [For each](#51-lists) item of list:
   1. If seenItems [contains](#51-lists) item, then return true.
   2. [Append](#51-lists) item to seenItems.
3. Return false.

To clone a [list](#51-lists) list is to return a [slice](#51-lists) of list.

> [!note]
> This is a "shallow clone", as the [items](#51-lists) themselves are not cloned in any way.

> [!example]
> Let original be the [ordered set](#513-sets) « "`a`", "`b`", "`c`" ». [Cloning](#51-lists) original creates a new [ordered set](#513-sets) clone, so that [replacing](#513-sets) "`a`" with "`foo`" in clone gives « "`foo`", "`b`", "`c`" », while original\[0\] is still the [string](#47-strings) "`a`".

To reverse a [list](#51-lists) list is to create a new [list](#51-lists) reversed, of the same designation, and, [for each](#51-lists) item of list, [prepend](#51-lists) item to reversed.

To sort in ascending order a [list](#51-lists) list, with a less than algorithm lessThanAlgo, is to create a new [list](#51-lists) sorted, containing the same [items](#51-lists) as list but sorted so that according to lessThanAlgo, each item is less than the one following it, if any. For items that sort the same (i.e., for which lessThanAlgo returns false for both comparisons), their relative order in sorted must be the same as it was in list.

To sort in descending order a [list](#51-lists) list, with a less than algorithm lessThanAlgo, is to create a new [list](#51-lists) sorted, containing the same [items](#51-lists) as list but sorted so that according to lessThanAlgo, each item is less than the one preceding it, if any. For items that sort the same (i.e., for which lessThanAlgo returns false for both comparisons), their relative order in sorted must be the same as it was in list.

> [!example]
> Let original be the [list](#51-lists) « (200, "`OK`"), (404, "`Not Found`"), (null, "`OK`") ». [Sorting](#51-lists) original in ascending order, with a being less than b if a’s second [item](#53-structs) is [code unit less than](#47-strings) b’s second [item](#53-structs), gives the result « (404, "`Not Found`"), (200, "`OK`"), (null, "`OK`") ».

---

The [list](#51-lists) type originates from the JavaScript specification (where it is capitalized, as [List](https://tc39.github.io/ecma262/#sec-list-and-record-specification-type)); we repeat some elements of its definition here for ease of reference, and provide an expanded vocabulary for manipulating [lists](#51-lists). Whenever JavaScript expects a [List](https://tc39.github.io/ecma262/#sec-list-and-record-specification-type), a [list](#51-lists) as defined here can be used; they are the same type. [\[ECMA-262\]](#normative-references)

#### 5.1.1. Stacks

Some [lists](#51-lists) are designated as stacks. A stack is a [list](#51-lists), but conventionally, the following operations are used to operate on it, instead of using [append](#51-lists), [prepend](#51-lists), or [remove](#51-lists).

To push onto a [stack](#511-stacks) is to [append](#51-lists) to it.

To pop from a [stack](#511-stacks): if the [stack](#511-stacks) [is not empty](#51-lists), then [remove](#51-lists) its last [item](#51-lists) and return it; otherwise, return nothing.

To peek into a [stack](#511-stacks): if the [stack](#511-stacks) [is not empty](#51-lists), then return its last [item](#51-lists); otherwise, return nothing.

Although [stacks](#511-stacks) are [lists](#51-lists), [for each](#51-lists) must not be used with them; instead, a combination of [while](#39-iteration) and [pop](#511-stacks) is more appropriate.

#### 5.1.2. Queues

Some [lists](#51-lists) are designated as queues. A queue is a [list](#51-lists), but conventionally, the following operations are used to operate on it, instead of using [append](#51-lists), [prepend](#51-lists), or [remove](#51-lists).

To enqueue in a [queue](#512-queues) is to [append](#51-lists) to it.

To dequeue from a [queue](#512-queues) is to [remove](#51-lists) its first [item](#51-lists) and return it, if the [queue](#512-queues) [is not empty](#51-lists), or to return nothing if it is.

Although [queues](#512-queues) are [lists](#51-lists), [for each](#51-lists) must not be used with them; instead, a combination of [while](#39-iteration) and [dequeue](#512-queues) is more appropriate.

#### 5.1.3. Sets

Some [lists](#51-lists) are designated as ordered sets. An ordered set is a [list](#51-lists) with the additional semantic that it must not contain two [items](#51-lists) that are [equal](#311-identity-and-equality).

> [!note]
> Almost all cases on the web platform require an *ordered* set, instead of an unordered one, since interoperability requires that any developer-exposed enumeration of the set’s contents be consistent between browsers. In those cases where order is not important, we still use ordered sets; implementations can optimize based on the fact that the order is not observable.

To create a [set](#513-sets), given a [list](#51-lists) input:
1. Let result be an empty [set](#513-sets).
2. [For each](#51-lists) item of input, [append](#513-sets) item to result.
3. Return result.

To append to an [ordered set](#513-sets): if the set [contains](#51-lists) the given [item](#51-lists), then do nothing; otherwise, perform the normal [list](#51-lists) [append](#51-lists) operation.

To extend an [ordered set](#513-sets) A with a [list](#51-lists) B, [for each](#51-lists) item of B, [append](#513-sets) item to A.

To prepend to an [ordered set](#513-sets): if the set [contains](#51-lists) the given [item](#51-lists), then do nothing; otherwise, perform the normal [list](#51-lists) [prepend](#51-lists) operation.

To replace within an [ordered set](#513-sets) set, given item and replacement: if set [contains](#51-lists) item or replacement, then replace the first instance of either with replacement and [remove](#51-lists) all other instances.

> [!example]
> [Replacing](#513-sets) "a" with "c" within the [ordered set](#513-sets) « "a", "b", "c" » gives « "c", "b" ». Within « "c", "b", "a" » it gives « "c", "b" » as well.

An [ordered set](#513-sets) set is a subset of another [ordered set](#513-sets) superset (and conversely, superset is a superset of set) if, [for each](#51-lists) item of set, superset [contains](#51-lists) item.

> [!note]
> This implies that an [ordered set](#513-sets) is both a [subset](#513-sets) and a [superset](#513-sets) of itself.

A [set](#513-sets) A is unordered equal to a [set](#513-sets) B if A is a [subset](#513-sets) of B and A is a [superset](#513-sets) of B.

> [!example]
> The [ordered sets](#513-sets) « 1, 2 » and « 2, 1 » are [unordered equal](#513-sets), but they are not [equal](#311-identity-and-equality), as the [equality](#311-identity-and-equality) of [lists](#51-lists) takes the order of their [items](#51-lists) into account.

The intersection of [ordered sets](#513-sets) A and B, is the result of creating a new [ordered set](#513-sets) set and, [for each](#51-lists) item of A, if B [contains](#51-lists) item, [appending](#513-sets) item to set.

The union of [ordered sets](#513-sets) A and B, is the result of [cloning](#51-lists) A as set and, [for each](#51-lists) item of B, [appending](#513-sets) item to set.

The difference of [ordered sets](#513-sets) A and B, is the result of creating a new [ordered set](#513-sets) set and, [for each](#51-lists) item of A, if B [does not contain](#51-lists) item, [appending](#513-sets) item to set.

---

The range n to m, inclusive, creates a new [ordered set](#513-sets) containing all of the integers from n up to and including m in consecutively increasing order, as long as m is greater than or equal to n.

The range n to m, exclusive, creates a new [ordered set](#513-sets) containing all of the integers from n up to and including m − 1 in consecutively increasing order, as long as m is greater than n. If m equals n, then it creates an empty [ordered set](#513-sets).

> [!example]
> [For each](#51-lists) n of [the range](#513-sets) 1 to 4, inclusive, …

### 5.2. Maps

An ordered map, or sometimes just "map", is a specification type consisting of a finite ordered sequence of [tuples](#531-tuples), each consisting of a key and a value, with no two keys being [equal](#311-identity-and-equality). Each such tuple is called an entry.

> [!note]
> As with [ordered sets](#513-sets), by default we assume that maps need to be ordered for interoperability among implementations.

A literal syntax can be used to express [ordered maps](#52-maps), by starting an ordered map with U+00AB («) and U+005B (\[), ending it with U+005D (\]) and U+00BB (»), separating each [entry](#52-maps)’s key and value with U+2192 (→), and separating its entries with U+002C (,).

> [!example]
> Let example be the [ordered map](#52-maps) «\[ "`a`" → \``x`\`, "`b`" → \``y`\` \]». Then example\["`a`"\] is the [byte sequence](#45-byte-sequences) \``x`\`.

An [ordered map](#52-maps)’s [equality](#311-identity-and-equality), given [ordered maps](#52-maps) a and b, returns true if a’s [size](#52-maps) is b’s [size](#52-maps) and each [entry](#52-maps) of a has a [key](#52-maps) and a [value](#52-maps) that [equal](#311-identity-and-equality) the [key](#52-maps) and the [value](#52-maps) of the [entry](#52-maps) of b at the same position; otherwise false.

---

To get the value of an entry in an [ordered map](#52-maps) map given a [key](#52-maps) key and an optional default:
1. If map does not [contain](#52-maps) key and default is given, then return default.
2. [Assert](#310-assertions): map [contains](#52-maps) key.
3. Return the [value](#52-maps) of the [entry](#52-maps) in map whose [key](#52-maps) [equals](#311-identity-and-equality) key.

We can also denote [getting the value of an entry](#52-maps) using an indexing syntax, by providing a [key](#52-maps) inside square brackets directly following a [map](#52-maps). A default can be given by adding the phrase with default followed by the default value.

> [!example]
> If map\["`test`"\] [exists](#52-maps), then return map\["`test`"\].

> [!example]
> Let example be the [ordered map](#52-maps) «\[ "`a`" → "`x`", "`b`" → "`y`" \]». Then example\["`a`"\] is the same as example\["`a`"\] [with default](#52-maps) "`z`", namely "`x`". example\["`c`"\] would hit an assert. example\["`c`"\] [with default](#52-maps) "`z`" is "`z`".

To set the value of an entry in an [ordered map](#52-maps) to a given [value](#52-maps) is to update the value of any existing [entry](#52-maps) if the map [contains](#52-maps) an entry with the given [key](#52-maps), or if none such exists, to add a new entry with the given key/value to the end of the map. We can also denote this by saying, for an [ordered map](#52-maps) map, key key, and value value, "[set](#52-maps) map\[key\] to value".

To remove an entry from an [ordered map](#52-maps) is to remove all [entries](#52-maps) from the map that match a given condition, or do nothing if none do. If the condition is having a certain [key](#52-maps), then we can also denote this by saying, for an [ordered map](#52-maps) map and key key, "[remove](#52-maps) map\[key\]".

To clear an [ordered map](#52-maps) is to remove all [entries](#52-maps) from the map.

An [ordered map](#52-maps) contains an [entry](#52-maps) with a given key if there exists an entry whose [key](#52-maps) [equals](#311-identity-and-equality) that key. We can also denote this by saying that, for an [ordered map](#52-maps) map and key key, "map\[key\] [exists](#52-maps)".

To get the keys of an [ordered map](#52-maps), return a new [ordered set](#513-sets) whose [items](#51-lists) are each of the [keys](#52-maps) in the map’s [entries](#52-maps).

To get the values of an [ordered map](#52-maps), return a new [list](#51-lists) whose [items](#51-lists) are each of the [values](#52-maps) in the map’s [entries](#52-maps).

An [ordered map](#52-maps)’s size is the [size](#51-lists) of the result of running [get the keys](#52-maps) on the map.

An [ordered map](#52-maps) is empty if its [size](#52-maps) is zero.

To iterate over an [ordered map](#52-maps), performing a set of steps on each [entry](#52-maps) in order, use phrasing of the form "[For each](#52-maps) key → value of map", and then operate on key and value in the subsequent prose.

To clone an [ordered map](#52-maps) map is to create a new [ordered map](#52-maps) clone, and, [for each](#52-maps) key → value of map, [set](#52-maps) clone\[key\] to value.

> [!note]
> This is a "shallow clone", as the [keys](#52-maps) and [values](#52-maps) themselves are not cloned in any way.

> [!example]
> Let original be the [ordered map](#52-maps) «\[ "`a`" → «1, 2, 3», "`b`" → «» \]». [Cloning](#51-lists) original creates a new [ordered map](#52-maps) clone, so that [setting](#52-maps) clone\["`a`"\] to «-1, -2, -3» gives «\[ "`a`" → «-1, -2, -3», "`b`" → «» \]» and leaves original unchanged. However, [appending](#51-lists) 4 to clone\["`b`"\] will modify the corresponding [value](#52-maps) in both clone and original, as they both point to the same [list](#51-lists).

To sort in ascending order a [map](#52-maps) map, with a less than algorithm lessThanAlgo, is to create a new [map](#52-maps) sorted, containing the same [entries](#52-maps) as map but sorted so that according to lessThanAlgo, each entry is less than the one following it, if any. For entries that sort the same (i.e., for which lessThanAlgo returns false for both comparisons), their relative order in sorted must be the same as it was in map.

To sort in descending order a [map](#52-maps) map, with a less than algorithm lessThanAlgo, is to create a new [map](#52-maps) sorted, containing the same [entries](#52-maps) as map but sorted so that according to lessThanAlgo, each entry is less than the one preceding it, if any. For entries that sort the same (i.e., for which lessThanAlgo returns false for both comparisons), their relative order in sorted must be the same as it was in map.

### 5.3. Structs

A struct is a specification type consisting of a finite set of items, each of which has a unique and immutable name. An [item](#53-structs) holds a value of a defined type.

> [!example]
> An email is an example [struct](#53-structs) consisting of a local part (a string) and a host (a [host](https://url.spec.whatwg.org/#concept-host)).
> 
> A nonsense algorithm might use this definition as follows:
> 1. Let email be an email whose local part is "`hostmaster`" and host is `infra.example`.
> 2. …

Unless its definition specifies otherwise, a [struct](#53-structs) that is not a [tuple](#531-tuples) only [equals](#311-identity-and-equality) itself: its [equality](#311-identity-and-equality) returns true if the two structs are [identical to](#311-identity-and-equality) each other; otherwise false.

The itemwise equality, given [structs](#53-structs) a and b, returns true if each [item](#53-structs) of a [equals](#311-identity-and-equality) the [item](#53-structs) of b with the same [name](#53-structs); otherwise false. A [struct](#53-structs)’s definition can specify that its [equality](#311-identity-and-equality) is [itemwise equality](#53-structs).

> [!example]
> Using the definition of email above:
> 1. Let email be an email whose local part is "`hostmaster`" and host is `infra.example`.
> 2. Let sameEmail be email.
> 3. Let otherEmail be an email whose local part is "`hostmaster`" and host is `infra.example`.
> 4. [Assert](#310-assertions): email [equals](#311-identity-and-equality) sameEmail, as they are [identical to](#311-identity-and-equality) each other.
> 5. [Assert](#310-assertions): email does not [equal](#311-identity-and-equality) otherEmail, as they are not [identical to](#311-identity-and-equality) each other.
> 
> If the definition of email instead specified that an email’s [equality](#311-identity-and-equality) is [itemwise equality](#53-structs), email would [equal](#311-identity-and-equality) otherEmail, as their local parts are [identical to](#311-identity-and-equality) each other and their hosts are [equal](#311-identity-and-equality).

> [!note]
> Thus, if a [struct](#53-structs) whose definition does not specify its [equality](#311-identity-and-equality) is used as a [key](#52-maps) of an [ordered map](#52-maps) or as an [item](#51-lists) of an [ordered set](#513-sets), it can only be found again using that very same struct. If that is not desired, its definition needs to specify its [equality](#311-identity-and-equality), e.g., as [itemwise equality](#53-structs).

#### 5.3.1. Tuples

A tuple is a [struct](#53-structs) whose [items](#53-structs) are ordered. For notational convenience, a literal syntax can be used to express [tuples](#531-tuples), by surrounding the tuple with parentheses and separating its [items](#53-structs) with U+002C (,). To use this notation, the [names](#53-structs) need to be clear from context. This can be done by preceding the first instance with the name given to the [tuple](#531-tuples). An indexing syntax can be used by providing a zero-based index into a [tuple](#531-tuples) inside square brackets. The index cannot be out-of-bounds.

> [!example]
> A status is an example [tuple](#531-tuples) consisting of a code (a number) and text (a byte sequence).
> 
> A nonsense algorithm that manipulates status tuples for the purpose of demonstrating their usage is:
> 1. Let statusInstance be the status (200, \``OK`\`).
> 2. Set statusInstance to (301, \``FOO BAR`\`).
> 3. If statusInstance’s code is 404, then …
> 
> The last step could also be written as "If statusInstance\[0\] is 404, then …". This might be preferable if the [tuple](#531-tuples) [names](#53-structs) do not have explicit definitions.

> [!note]
> It is intentional that not all [structs](#53-structs) are [tuples](#531-tuples). Documents using the Infra Standard might need the flexibility to add new [names](#53-structs) to their struct without breaking literal syntax used by their dependencies. In that case a tuple is not appropriate.

A [tuple](#531-tuples)’s [equality](#311-identity-and-equality) is [itemwise equality](#53-structs), unless its definition specifies otherwise.

> [!note]
> Changing a [tuple](#531-tuples) into a [struct](#53-structs) that is not a [tuple](#531-tuples) also means it no longer has [itemwise equality](#53-structs), unless its definition then specifies it.

## 6. JSON

> [!note]
> The conventions used in the algorithms in this section are those of the JavaScript specification. [\[ECMA-262\]](#normative-references)

To parse a JSON string to a JavaScript value, given a [string](#47-strings) string:
1. Return ? [Call](https://tc39.github.io/ecma262/#sec-call)([%JSON.parse%](https://tc39.github.io/ecma262/#sec-json.parse), undefined, « string »).

To parse JSON bytes to a JavaScript value, given a [byte sequence](#45-byte-sequences) bytes:
1. Let string be the result of running [UTF-8 decode](https://encoding.spec.whatwg.org/#utf-8-decode) on bytes. [\[ENCODING\]](#normative-references)
2. Return the result of [parsing a JSON string to a JavaScript value](#6-json) given string.

To serialize a JavaScript value to a JSON string, given a JavaScript value value:
1. Let result be ? [Call](https://tc39.github.io/ecma262/#sec-call)([%JSON.stringify%](https://tc39.github.io/ecma262/#sec-json.stringify), undefined, « value »).

   > [!note]
   > Since no additional arguments are passed to [%JSON.stringify%](https://tc39.github.io/ecma262/#sec-json.stringify), the resulting string will have no whitespace inserted.

2. If result is undefined, then throw a [`TypeError`](https://webidl.spec.whatwg.org/#exceptiondef-typeerror).

   > [!note]
   > This can happen if value does not have a JSON representation, e.g., if it is undefined or a function.

3. [Assert](#310-assertions): result is a [string](#47-strings).
4. Return result.

To serialize a JavaScript value to JSON bytes, given a JavaScript value value:
1. Let string be the result of [serializing a JavaScript value to a JSON string](#6-json) given value.
2. Return the result of running [UTF-8 encode](https://encoding.spec.whatwg.org/#utf-8-encode) on string. [\[ENCODING\]](#normative-references)

---

The above operations operate on JavaScript values directly; in particular, this means that the involved objects or arrays are tied to a particular [JavaScript realm](https://tc39.github.io/ecma262/#realm). In standards, it is often more convenient to convert between JSON and realm-independent [maps](#52-maps), [lists](#51-lists), [strings](#47-strings), [booleans](#42-booleans), numbers, and nulls.

To parse a JSON string to an Infra value, given a [string](#47-strings) string:
1. Let jsValue be ? [Call](https://tc39.github.io/ecma262/#sec-call)([%JSON.parse%](https://tc39.github.io/ecma262/#sec-json.parse), undefined, « string »).
2. Return the result of [converting a JSON-derived JavaScript value to an Infra value](#6-json), given jsValue.

To parse JSON bytes to an Infra value, given a [byte sequence](#45-byte-sequences) bytes:
1. Let string be the result of running [UTF-8 decode](https://encoding.spec.whatwg.org/#utf-8-decode) on bytes. [\[ENCODING\]](#normative-references)
2. Return the result of [parsing a JSON string to an Infra value](#6-json) given string.

To convert a JSON-derived JavaScript value to an Infra value, given a JavaScript value jsValue:
1. If jsValue is null, jsValue [is a Boolean](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-boolean-type), jsValue [is a String](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-string-type), or jsValue [is a Number](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-number-type), then return jsValue.
2. If [IsArray](https://tc39.github.io/ecma262/#sec-isarray)(jsValue) is true:
   1. Let result be an empty [list](#51-lists).
   2. Let length be ! [ToLength](https://tc39.github.io/ecma262/#sec-tolength)(! [Get](https://tc39.github.io/ecma262/#sec-get-o-p)(jsValue, "`length`")).
   3. [For each](#51-lists) index of [the range](#513-sets) 0 to length − 1, inclusive:
      1. Let indexName be ! [ToString](https://tc39.github.io/ecma262/#sec-tostring)(index).
      2. Let jsValueAtIndex be ! [Get](https://tc39.github.io/ecma262/#sec-get-o-p)(jsValue, indexName).
      3. Let infraValueAtIndex be the result of [converting a JSON-derived JavaScript value to an Infra value](#6-json), given jsValueAtIndex.
      4. [Append](#51-lists) infraValueAtIndex to result.
   4. Return result.
3. Let result be an empty [ordered map](#52-maps).
4. [For each](#51-lists) key of ! jsValue.\[\[OwnPropertyKeys\]\]():
   1. Let jsValueAtKey be ! [Get](https://tc39.github.io/ecma262/#sec-get-o-p)(jsValue, key).
   2. Let infraValueAtKey be the result of [converting a JSON-derived JavaScript value to an Infra value](#6-json), given jsValueAtKey.
   3. [Set](#52-maps) result\[key\] to infraValueAtKey.
5. Return result.

To serialize an Infra value to a JSON string, given a [string](#47-strings), [boolean](#42-booleans), number, null, [list](#51-lists), or [string](#47-strings)-keyed [map](#52-maps) value:
1. Let jsValue be the result of [converting an Infra value to a JSON-compatible JavaScript value](#6-json), given value.
2. Return ! [Call](https://tc39.github.io/ecma262/#sec-call)([%JSON.stringify%](https://tc39.github.io/ecma262/#sec-json.stringify), undefined, « jsValue »).

   > [!note]
   > Since no additional arguments are passed to [%JSON.stringify%](https://tc39.github.io/ecma262/#sec-json.stringify), the resulting string will have no whitespace inserted.

To serialize an Infra value to JSON bytes, given a [string](#47-strings), [boolean](#42-booleans), number, null, [list](#51-lists), or [string](#47-strings)-keyed [map](#52-maps) value:
1. Let string be the result of [serializing an Infra value to a JSON string](#6-json), given value.
2. Return the result of running [UTF-8 encode](https://encoding.spec.whatwg.org/#utf-8-encode) on string. [\[ENCODING\]](#normative-references)

To convert an Infra value to a JSON-compatible JavaScript value, given value:
1. If value is a [string](#47-strings), [boolean](#42-booleans), number, or null, then return value.
2. If value is a [list](#51-lists):
   1. Let jsValue be ! [ArrayCreate](https://tc39.github.io/ecma262/#sec-arraycreate)(0).
   2. Let i be 0.
   3. [For each](#51-lists) listItem of value:
      1. Let listItemJSValue be the result of [converting an Infra value to a JSON-compatible JavaScript value](#6-json), given listItem.
      2. Perform ! [CreateDataPropertyOrThrow](https://tc39.github.io/ecma262/#sec-createdatapropertyorthrow)(jsValue, ! [ToString](https://tc39.github.io/ecma262/#sec-tostring)(i), listItemJSValue).
      3. Set i to i + 1.
   4. Return jsValue.
3. [Assert](#310-assertions): value is a [map](#52-maps).
4. Let jsValue be ! [OrdinaryObjectCreate](https://tc39.github.io/ecma262/#sec-ordinaryobjectcreate)(null).
5. [For each](#51-lists) mapKey → mapValue of value:
   1. [Assert](#310-assertions): mapKey is a [string](#47-strings).
   2. Let mapValueJSValue be the result of [converting an Infra value to a JSON-compatible JavaScript value](#6-json), given mapValue.
   3. Perform ! [CreateDataPropertyOrThrow](https://tc39.github.io/ecma262/#sec-createdatapropertyorthrow)(jsValue, mapKey, mapValueJSValue).
6. Return jsValue.

> [!warning]
> Because it is rarely appropriate to manipulate JavaScript values directly in specifications, prefer using [serialize an Infra value to a JSON string](#6-json) or [serialize an Infra value to JSON bytes](#6-json) instead of using this algorithm. Please [file an issue](https://github.com/whatwg/infra/issues/new) to discuss your use case if you believe you need to use [convert an Infra value to a JSON-compatible JavaScript value](#6-json).

## 7. Forgiving base64

To forgiving-base64 encode given a [byte sequence](#45-byte-sequences) data, apply the base64 algorithm defined in section 4 of RFC 4648 to data and return the result. [\[RFC4648\]](#normative-references)

> [!note]
> This is named [forgiving-base64 encode](#7-forgiving-base64) for symmetry with [forgiving-base64 decode](#7-forgiving-base64), which is different from the RFC as it defines error handling for certain inputs.

To forgiving-base64 decode given a string data, run these steps:
1. Remove all [ASCII whitespace](#46-code-points) from data.
2. If data’s [code point length](#47-strings) divides by 4 leaving no remainder:
   1. If data ends with one or two U+003D (=) [code points](#46-code-points), then remove them from data.
3. If data’s [code point length](#47-strings) divides by 4 leaving a remainder of 1, then return failure.
4. If data contains a [code point](#46-code-points) that is not one of
   - U+002B (+)
   - U+002F (/)
   - [ASCII alphanumeric](#46-code-points)

   then return failure.

5. Let output be an empty [byte sequence](#45-byte-sequences).
6. Let buffer be an empty buffer that can have bits appended to it.
7. Let position be a [position variable](#47-strings) for data, initially pointing at the start of data.
8. While position does not point past the end of data:
   1. Find the [code point](#46-code-points) pointed to by position in the second column of Table 1: The Base 64 Alphabet of RFC 4648. Let n be the number given in the first cell of the same row. [\[RFC4648\]](#normative-references)
   2. Append the six bits corresponding to n, most significant bit first, to buffer.
   3. If buffer has accumulated 24 bits, interpret them as three 8-bit big-endian numbers. Append three bytes with values equal to those numbers to output, in the same order, and then empty buffer.
   4. Advance position by 1.
9. If buffer is not empty, it contains either 12 or 18 bits. If it contains 12 bits, then discard the last four and interpret the remaining eight as an 8-bit big-endian number. If it contains 18 bits, then discard the last two and interpret the remaining 16 as two 8-bit big-endian numbers. Append the one or two bytes with values equal to those one or two numbers to output, in the same order.

   > [!note]
   > The discarded bits mean that, for instance, "`YQ`" and "`YR`" both return \``a`\`.

10. Return output.

## 8. Namespaces

The HTML namespace is "`http://www.w3.org/1999/xhtml`".

The MathML namespace is "`http://www.w3.org/1998/Math/MathML`".

The SVG namespace is "`http://www.w3.org/2000/svg`".

The XLink namespace is "`http://www.w3.org/1999/xlink`".

The XML namespace is "`http://www.w3.org/XML/1998/namespace`".

The XMLNS namespace is "`http://www.w3.org/2000/xmlns/`".

## Acknowledgments

Many thanks to Addison Phillips, Andreu Botella, Aryeh Gregor, Ben Kelly, Chris Rebert, Daniel Ehrenberg, Dominic Farolino, Gabriel Pivovarov, Ian Hickson, Jakob Ackermann, Jake Archibald, Jeff Hodges, Jeffrey Yasskin, Jungkee Song, Leonid Vasilyev, Maciej Stachowiak, Malika Aubakirova, Martin Thomson, Michael™ Smith, Mike West, Mike Taylor, Ms2ger, Noam Rosenthal, Pavel "Al Arz" Kurochkin, Philip Jägenstedt, Rashaun "Snuggs" Stovall, Sergey Shekyan, Simon Pieters, Tab Atkins, Tobie Langel, triple-underscore, Wolf Lammen, and Xue Fuqiao for being awesome!

This standard is written by [Anne van Kesteren](https://annevankesteren.nl/) ([Apple](https://www.apple.com/), [annevk@annevk.nl](mailto:annevk@annevk.nl)) and [Domenic Denicola](https://domenic.me/) ([Google](https://www.google.com/), [d@domenic.me](mailto:d@domenic.me)).

## Intellectual property rights

Copyright © WHATWG (Apple, Google, Mozilla, Microsoft). This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). To the extent portions of it are incorporated into source code, such portions in the source code are licensed under the [BSD 3-Clause License](https://opensource.org/licenses/BSD-3-Clause) instead.

This is the Living Standard. Those interested in the patent-review version should view the [Living Standard Review Draft](https://infra.spec.whatwg.org/review-drafts/2026-07/).

## Index

### Terms defined by this specification
- [128-bit unsigned integer](#43-numbers), in § 4.3
- [16-bit signed integer](#43-numbers), in § 4.3
- [16-bit unsigned integer](#43-numbers), in § 4.3
- [32-bit signed integer](#43-numbers), in § 4.3
- [32-bit unsigned integer](#43-numbers), in § 4.3
- [64-bit signed integer](#43-numbers), in § 4.3
- [64-bit unsigned integer](#43-numbers), in § 4.3
- [8-bit signed integer](#43-numbers), in § 4.3
- [8-bit unsigned integer](#43-numbers), in § 4.3
- [abort when](#37-conditional-abort), in § 3.7
- [allowed](#49-singletons), in § 4.9
- append
  - [dfn for list](#51-lists), in § 5.1
  - [dfn for set](#513-sets), in § 5.1.3
- [ASCII alpha](#46-code-points), in § 4.6
- [ASCII alphanumeric](#46-code-points), in § 4.6
- [ASCII byte](#44-bytes), in § 4.4
- [ASCII case-insensitive](#47-strings), in § 4.7
- [ASCII code point](#46-code-points), in § 4.6
- [ASCII decode](#47-strings), in § 4.7
- [ASCII digit](#46-code-points), in § 4.6
- [ASCII encode](#47-strings), in § 4.7
- [ASCII hex digit](#46-code-points), in § 4.6
- [ASCII lower alpha](#46-code-points), in § 4.6
- [ASCII lowercase](#47-strings), in § 4.7
- [ASCII lower hex digit](#46-code-points), in § 4.6
- [ASCII string](#47-strings), in § 4.7
- [ASCII tab or newline](#46-code-points), in § 4.6
- [ASCII tabs or newlines](#46-code-points), in § 4.6
- [ASCII upper alpha](#46-code-points), in § 4.6
- [ASCII uppercase](#47-strings), in § 4.7
- [ASCII upper hex digit](#46-code-points), in § 4.6
- [ASCII whitespace](#46-code-points), in § 4.6
- [Assert](#310-assertions), in § 3.10
- [blocked](#49-singletons), in § 4.9
- [boolean](#42-booleans), in § 4.2
- [break](#39-iteration), in § 3.9
- [byte](#44-bytes), in § 4.4
- [byte-case-insensitive](#45-byte-sequences), in § 4.5
- [byte less than](#45-byte-sequences), in § 4.5
- [byte-lowercase](#45-byte-sequences), in § 4.5
- [byte sequence](#45-byte-sequences), in § 4.5
- [byte-uppercase](#45-byte-sequences), in § 4.5
- [C0 control](#46-code-points), in § 4.6
- [C0 control or space](#46-code-points), in § 4.6
- [C0 controls or spaces](#46-code-points), in § 4.6
- [character](#46-code-points), in § 4.6
- [clear](#52-maps), in § 5.2
- clone
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [code point](#46-code-points), in § 4.6
- [code point length](#47-strings), in § 4.7
- [code point substring](#47-strings), in § 4.7
- [code point substring by positions](#47-strings), in § 4.7
- [code point substring to the end of the string](#47-strings), in § 4.7
- [code unit](#47-strings), in § 4.7
- [code unit less than](#47-strings), in § 4.7
- [code unit prefix](#47-strings), in § 4.7
- [code unit substring](#47-strings), in § 4.7
- [code unit substring by positions](#47-strings), in § 4.7
- [code unit substring to the end of the string](#47-strings), in § 4.7
- [code unit suffix](#47-strings), in § 4.7
- [collect a sequence of code points](#47-strings), in § 4.7
- [collecting a sequence of code points](#47-strings), in § 4.7
- [concatenate](#47-strings), in § 4.7
- [concatenation](#47-strings), in § 4.7
- contain
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [continue](#39-iteration), in § 3.9
- [control](#46-code-points), in § 4.6
- [convert](#47-strings), in § 4.7
- [convert a JSON-derived JavaScript value to an Infra value](#6-json), in § 6
- [convert an Infra value to a JSON-compatible JavaScript value](#6-json), in § 6
- [create](#513-sets), in § 5.1.3
- [dequeue](#512-queues), in § 5.1.2
- [difference](#513-sets), in § 5.1.3
- [empty](#51-lists), in § 5.1
- [ends with](#47-strings), in § 4.7
- [enqueue](#512-queues), in § 5.1.2
- [entry](#52-maps), in § 5.2
- equal
  - [definition of](#311-identity-and-equality), in § 3.11
  - [dfn for set](#513-sets), in § 5.1.3
- [equality](#311-identity-and-equality), in § 3.11
- [equals](#311-identity-and-equality), in § 3.11
- exist
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- extend
  - [dfn for list](#51-lists), in § 5.1
  - [dfn for set](#513-sets), in § 5.1.3
- [failure](#49-singletons), in § 4.9
- for each
  - [dfn for list, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [forgiving-base64 decode](#7-forgiving-base64), in § 7
- [forgiving-base64 encode](#7-forgiving-base64), in § 7
- [from](#51-lists), in § 5.1
- [get](#52-maps), in § 5.2
- [get the indices](#51-lists), in § 5.1
- [get the keys](#52-maps), in § 5.2
- [get the value](#52-maps), in § 5.2
- [get the values](#52-maps), in § 5.2
- [getting the keys](#52-maps), in § 5.2
- [getting the values](#52-maps), in § 5.2
- [has duplicates](#51-lists), in § 5.1
- [HTML namespace](#8-namespaces), in § 8
- identical to
  - [definition of](#311-identity-and-equality), in § 3.11
  - [dfn for string](#47-strings), in § 4.7
- [if aborted](#37-conditional-abort), in § 3.7
- [implementation](#23-terminology), in § 2.3
- [implementation-defined](#23-terminology), in § 2.3
- [indices](#51-lists), in § 5.1
- [insert](#51-lists), in § 5.1
- [intersection](#513-sets), in § 5.1.3
- is
  - [definition of](#311-identity-and-equality), in § 3.11
  - [dfn for string](#47-strings), in § 4.7
- is empty
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- is not empty
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [isomorphic decode](#45-byte-sequences), in § 4.5
- [isomorphic encode](#47-strings), in § 4.7
- [isomorphic string](#47-strings), in § 4.7
- item
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for struct, tuple](#53-structs), in § 5.3
- [itemwise equality](#53-structs), in § 5.3
- iterate
  - [dfn for list, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [JavaScript string](#47-strings), in § 4.7
- [key](#52-maps), in § 5.2
- [keys](#52-maps), in § 5.2
- [leading surrogate](#46-code-points), in § 4.6
- length
  - [dfn for byte sequence](#45-byte-sequences), in § 4.5
  - [dfn for string, JavaScript string, ASCII string, isomorphic string, scalar value string](#47-strings), in § 4.7
- [list](#51-lists), in § 5.1
- [map](#52-maps), in § 5.2
- [MathML namespace](#8-namespaces), in § 8
- [name](#53-structs), in § 5.3
- [noncharacter](#46-code-points), in § 4.6
- [normalize newlines](#47-strings), in § 4.7
- [ordered map](#52-maps), in § 5.2
- [ordered set](#513-sets), in § 5.1.3
- [parse a JSON string to a JavaScript value](#6-json), in § 6
- [parse a JSON string to an Infra value](#6-json), in § 6
- [parse JSON bytes to a JavaScript value](#6-json), in § 6
- [parse JSON bytes to an Infra value](#6-json), in § 6
- [parse JSON from bytes](#6-json), in § 6
- [parse JSON into Infra values](#6-json), in § 6
- [peek](#511-stacks), in § 5.1.1
- [pop](#511-stacks), in § 5.1.1
- [position variable](#47-strings), in § 4.7
- [prefix](#45-byte-sequences), in § 4.5
- prepend
  - [dfn for list](#51-lists), in § 5.1
  - [dfn for set](#513-sets), in § 5.1.3
- [push](#511-stacks), in § 5.1.1
- [queue](#512-queues), in § 5.1.2
- remove
  - [dfn for list, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- replace
  - [dfn for list](#51-lists), in § 5.1
  - [dfn for set](#513-sets), in § 5.1.3
- [replacing](#513-sets), in § 5.1.3
- [reverse](#51-lists), in § 5.1
- [scalar value](#46-code-points), in § 4.6
- [scalar value string](#47-strings), in § 4.7
- [serialize a JavaScript value to a JSON string](#6-json), in § 6
- [serialize a JavaScript value to JSON bytes](#6-json), in § 6
- [serialize an Infra value to a JSON string](#6-json), in § 6
- [serialize an Infra value to JSON bytes](#6-json), in § 6
- [serialize JSON to bytes](#6-json), in § 6
- set
  - [definition of](#513-sets), in § 5.1.3
  - [dfn for map](#52-maps), in § 5.2
- [set the value](#52-maps), in § 5.2
- size
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [skip ASCII whitespace](#47-strings), in § 4.7
- [slice](#51-lists), in § 5.1
- sort
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- sort in ascending order
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- sort in descending order
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- sorting
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- sorting in ascending order
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- sorting in descending order
  - [dfn for list, stack, queue, set](#51-lists), in § 5.1
  - [dfn for map](#52-maps), in § 5.2
- [split a string on ASCII whitespace](#47-strings), in § 4.7
- [split a string on commas](#47-strings), in § 4.7
- [split on ASCII whitespace](#47-strings), in § 4.7
- [split on commas](#47-strings), in § 4.7
- [stack](#511-stacks), in § 5.1.1
- starts with
  - [dfn for byte sequence](#45-byte-sequences), in § 4.5
  - [dfn for string](#47-strings), in § 4.7
- [start with](#45-byte-sequences), in § 4.5
- [strictly split](#47-strings), in § 4.7
- [strictly split a string](#47-strings), in § 4.7
- [string](#47-strings), in § 4.7
- [strip and collapse ASCII whitespace](#47-strings), in § 4.7
- [strip leading and trailing ASCII whitespace](#47-strings), in § 4.7
- [strip newlines](#47-strings), in § 4.7
- [struct](#53-structs), in § 5.3
- [subset](#513-sets), in § 5.1.3
- [success](#49-singletons), in § 4.9
- [superset](#513-sets), in § 5.1.3
- [surrogate](#46-code-points), in § 4.6
- [SVG namespace](#8-namespaces), in § 8
- [the exclusive range](#513-sets), in § 5.1.3
- [the inclusive range](#513-sets), in § 5.1.3
- [the range](#513-sets), in § 5.1.3
- [to](#51-lists), in § 5.1
- [tracking vector](#24-privacy-concerns), in § 2.4
- [trailing surrogate](#46-code-points), in § 4.6
- [tuple](#531-tuples), in § 5.3.1
- [union](#513-sets), in § 5.1.3
- [unordered equal](#513-sets), in § 5.1.3
- [user agent](#23-terminology), in § 2.3
- value
  - [dfn for byte](#44-bytes), in § 4.4
  - [dfn for code point](#46-code-points), in § 4.6
  - [dfn for map](#52-maps), in § 5.2
- [values](#52-maps), in § 5.2
- [while](#39-iteration), in § 3.9
- [willful violation](#22-compliance-with-other-specifications), in § 2.2
- [with default](#52-maps), in § 5.2
- [XLink namespace](#8-namespaces), in § 8
- [XML namespace](#8-namespaces), in § 8
- [XMLNS namespace](#8-namespaces), in § 8

### Terms defined by reference
- \[DOM\] defines the following terms:
  - CharacterData
- \[ECMA-262\] defines the following terms:
  - %JSON.parse%
  - %JSON.stringify%
  - ArrayCreate
  - Call
  - CreateDataPropertyOrThrow
  - Get
  - IsArray
  - OrdinaryObjectCreate
  - ToLength
  - ToString
  - is a Boolean
  - is a Number
  - is a String
  - List
  - realm
  - sort()
  - The String Type
- \[ENCODING\] defines the following terms:
  - UTF-8 decode
  - UTF-8 encode
- \[FETCH\] defines the following terms:
  - HTTP whitespace
- \[HR-TIME\] defines the following terms:
  - duration
  - moment
- \[URL\] defines the following terms:
  - host
- \[WEBIDL\] defines the following terms:
  - TypeError

## References

### Normative References

\[ECMA-262\]

[ECMAScript Language Specification](https://tc39.es/ecma262/multipage/). URL: [https://tc39.es/ecma262/multipage/](https://tc39.es/ecma262/multipage/)

\[ENCODING\]

Anne van Kesteren. [Encoding Standard](https://encoding.spec.whatwg.org/). Living Standard. URL: [https://encoding.spec.whatwg.org/](https://encoding.spec.whatwg.org/)

\[HR-TIME\]

Yoav Weiss. [High Resolution Time](https://w3c.github.io/hr-time/). URL: [https://w3c.github.io/hr-time/](https://w3c.github.io/hr-time/)

\[Infra\]

Anne van Kesteren; Domenic Denicola. [Infra Standard](https://infra.spec.whatwg.org/). Living Standard. URL: [https://infra.spec.whatwg.org/](https://infra.spec.whatwg.org/)

\[RFC20\]

V.G. Cerf. [ASCII format for network interchange](https://www.rfc-editor.org/info/rfc20/). October 1969. Internet Standard. URL: [https://www.rfc-editor.org/info/rfc20/](https://www.rfc-editor.org/info/rfc20/)

\[RFC2119\]

S. Bradner. [Key words for use in RFCs to Indicate Requirement Levels](https://datatracker.ietf.org/doc/html/rfc2119). March 1997. Best Current Practice. URL: [https://datatracker.ietf.org/doc/html/rfc2119](https://datatracker.ietf.org/doc/html/rfc2119)

\[RFC4648\]

S. Josefsson. [The Base16, Base32, and Base64 Data Encodings](https://www.rfc-editor.org/info/rfc4648/). October 2006. Proposed Standard. URL: [https://www.rfc-editor.org/info/rfc4648/](https://www.rfc-editor.org/info/rfc4648/)

\[UNICODE\]

[The Unicode Standard](https://www.unicode.org/versions/latest/). URL: [https://www.unicode.org/versions/latest/](https://www.unicode.org/versions/latest/)

\[WEBIDL\]

Edgar Chen; Timothy Gu. [Web IDL Standard](https://webidl.spec.whatwg.org/). Living Standard. URL: [https://webidl.spec.whatwg.org/](https://webidl.spec.whatwg.org/)

### Non-Normative References

\[COOKIES\]

A. Barth. [HTTP State Management Mechanism](https://httpwg.org/specs/rfc6265.html). April 2011. Proposed Standard. URL: [https://httpwg.org/specs/rfc6265.html](https://httpwg.org/specs/rfc6265.html)

\[DOM\]

Anne van Kesteren. [DOM Standard](dom-spec-whatwg-org.md). Living Standard. URL: [https://dom.spec.whatwg.org/](dom-spec-whatwg-org.md)

\[FETCH\]

Anne van Kesteren. [Fetch Standard](https://fetch.spec.whatwg.org/). Living Standard. URL: [https://fetch.spec.whatwg.org/](https://fetch.spec.whatwg.org/)

\[HTML\]

Anne van Kesteren; et al. [HTML Standard](html-spec-whatwg-org.md). Living Standard. URL: [https://html.spec.whatwg.org/multipage/](html-spec-whatwg-org.md)

\[RFC6797\]

J. Hodges; C. Jackson; A. Barth. [HTTP Strict Transport Security (HSTS)](https://www.rfc-editor.org/info/rfc6797/). November 2012. Proposed Standard. URL: [https://www.rfc-editor.org/info/rfc6797/](https://www.rfc-editor.org/info/rfc6797/)

\[RFC791\]

J. Postel. [Internet Protocol](https://www.rfc-editor.org/info/rfc791/). September 1981. Internet Standard. URL: [https://www.rfc-editor.org/info/rfc791/](https://www.rfc-editor.org/info/rfc791/)

\[RFC8174\]

B. Leiba. [Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words](https://www.rfc-editor.org/info/rfc8174/). May 2017. Best Current Practice. URL: [https://www.rfc-editor.org/info/rfc8174/](https://www.rfc-editor.org/info/rfc8174/)

\[RFC8259\]

T. Bray, Ed.. [The JavaScript Object Notation (JSON) Data Interchange Format](https://www.rfc-editor.org/info/rfc8259/). December 2017. Internet Standard. URL: [https://www.rfc-editor.org/info/rfc8259/](https://www.rfc-editor.org/info/rfc8259/)

\[STORAGE\]

Anne van Kesteren. [Storage Standard](https://storage.spec.whatwg.org/). Living Standard. URL: [https://storage.spec.whatwg.org/](https://storage.spec.whatwg.org/)

\[URL\]

Anne van Kesteren. [URL Standard](https://url.spec.whatwg.org/). Living Standard. URL: [https://url.spec.whatwg.org/](https://url.spec.whatwg.org/)

\[XML\]

Tim Bray; et al. [Extensible Markup Language (XML) 1.0 (Fifth Edition)](https://www.w3.org/TR/xml/). 26 November 2008. REC. URL: [https://www.w3.org/TR/xml/](https://www.w3.org/TR/xml/)
