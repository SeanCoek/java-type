## An Implementation of Type Based Information Flow Analysis in Java

This work aims to implement a type based analysis based on the Checker Framework (https://checkerframework.org). The project consists of two components.

#### A simple type based points-to analysis

Some relatively complete Java syntax can be found at (https://users-cs.au.dk/amoeller/RegAut/JavaBNF.html) or (http://homepage.cs.uiowa.edu/~fleck/JavaBNF.htm), as specified in BNF.

The analysis produces a mapping that assigns a reference-typed variable to a set of heap objects, usually indicated by their creation sites in the program. We focus on two categories of variables --- local variables and fields. The initial type can be either null, as indicated by an empty set, or be a new statement "var = new C(...)" at line number abc which gives a singleton set {abc}. This set of points-to is propagated through assignments, as method call parameters, or as method call return values. We join the types in spirit of Andersen's subset based construction.

#### Inference of information flow types on top of the points-to analysis

