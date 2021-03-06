---
layout: doc
title: Structural Features
---

Structural features can be used to extend the declaration-level MMT syntax. They elaborate derived declarations to an elaboration, a list of so-called external declarations. Their syntax and semantics (i.e. elaboration) are defined by their implementation. Structural features are usually implemented as extensions to the MMT API. 

In particular, they define a validity predicate allowing to check the well-formedness of a derived declaration of the structural feature and the elaboration function for well-formed derived declarations of the feature.

Examples of structural features include [Inductive Types](inductive.md) and [Record Types](records.md).

