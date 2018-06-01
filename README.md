## An Implementation of Type Based Information Flow Analysis in Java

This work aims to implement a type based analysis based on the Checker Framework (https://checkerframework.org). The project consists of two components.

#### A simple type based points-to analysis

Some relatively complete Java syntax can be found at (https://users-cs.au.dk/amoeller/RegAut/JavaBNF.html) or (http://homepage.cs.uiowa.edu/~fleck/JavaBNF.htm), as specified in BNF.

The analysis produces a mapping that assigns a reference-typed variable to a set of heap objects, usually indicated by their creation sites in the program. We focus on two categories of variables --- local variables and fields. The initial type can be either null, as indicated by an empty set, or be a new statement "var = new C(...)" at line number abc which gives a singleton set {abc}. This set of points-to is propagated through assignments, as method call parameters, or as method call return values. We join the types in spirit of Andersen's subset based construction.

#### Inference of information flow types on top of the points-to analysis

The algorithm for information flow analysis is based on the Dual-Access Labels (DAL), so that an object o can be labelled by a pair of access privileges (Acc, Cap), specifying the accessiblity (the privilege required to access o) and the capability (the privilege that is owned by o). When two labels (Acc<sub>1</sub>, Cap<sub>1</sub>) and (Acc<sub>2</sub>, Cap<sub>2</sub>) are joined, the combined accessibility may become larger (practically, it may be defined as the set union of Acc<sub>1</sub> and Acc<sub>2</sub>), while the combined capability may shrink (may be defined as the set intersection of Cap<sub>1</sub> and  Cap<sub>2</sub>). 

When computing the DAL on reference objects, the collects points-to information for a given reference typed variable, and applies the join operation on all the objects that are pointed-to as a conservative approximation. For the details we refer to the technical report that is being developed in this repo.
