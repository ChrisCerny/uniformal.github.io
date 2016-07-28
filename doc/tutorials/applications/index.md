---
layout: doc
title: Application Development with MMT
---

In this tutorial, we show how to build a few minimal applications on top of the MMT library.
We will not build the applications step by step. But they are chosen to be easy to understand, reproduce, and play with.
They cover various but not all of the [extension interfaces](../api/extensions/) that MMT provides to application developers.

The following assumes that

* MMT has been [installed](../../setup),
* archives are placed in some folder, which is refered to as `CONTENT`,
* [jEdit](../../applications/jedit) is used for editing mmt files. <span class="detail">Other editors will work but might make editing awkward.</span>

<hr/>

### A Web-Based Editor

This mini-application shows how to easily integrate MMT with HTML pages.
It uses

* the core algorithms of MMT,
* the MMT HTTP server,
* the MMT query language,
* and the Javascript interface to MMT.

#### Behavior

First we start an MMT server:

 1. run `mmt.jar`
 1. enter `server on 8080`

Now download the file
[src/mmt-api/resources/mmt-web/editing-example.html](https://github.com/UniFormal/MMT/blob/master/src/mmt-api/resources/mmt-web/editing-example.html)
which is provided as part of the MMT sources.

Opening the file in a browser shows two input fields for

 * the URI of an MMT theory
 * an MMT expression relative to that theory

Clicking the commit button shows the same expression in MathML obtained by

 1. parsing
 1. type reconstruction
 1. simplification
 1. conversion to MathML

Best results of MathML display are obtained in Firefox.

#### Implementation

The html file is self-documenting. Open it in a text editor to see how it works.

You can also use your browser's inspector to see the Ajax request and response that the submit button generates.

<hr/>

### An OpenMath Content Dictionary Editor

This mini-application shows how to use MMT as an editor for OpenMath content dictionaries.
It uses

* the MMT build system,
* the [Exporter extension](../api/extensions/) for defining new build targets,
* the meta-data annotations to MMT content,
* the extensible MMT parser.

Concretely, it exports MMT theories as content dictionaries.

#### Behavior

Consider the archive `MMT/examples`, which was cloned automatically during setup.
In it, consider the files in the folder `source/tutorial`.

 1. Run `mmt.jar`
 1. Enter the commands
    
    ```
    extension info.kwarc.mmt.openmath.Exporter
    build MMT/examples openmath tutorial
    ```

The first command registers the exporter with MMT. <span class="detail" markdown="1">There are several ways to automate this registration. For example, you can script MMT by putting the commands in an `msl` or permanently add the exporter by adding an entry to your `mmtrc` file.</span>
The second one runs the build targatproduces OpenMath content dictionaries in the folder `export/openmath` of the archive.

The types and definitions are used to generate FMPs. The meta-data key `@_description` is used to give descriptions.

#### Implementation

The implemenation is part of the MMT sources in the project `mmt-openmath`.
The only file of this project is [src/mmt-openmath/src/info/kwarc/mmt/openmath/Exporter.scala](https://github.com/UniFormal/MMT/blob/master/src/mmt-openmath/src/info/kwarc/mmt/openmath/Exporter.scala).
It is self-documenting.

<hr/>

### Using a Rewrite