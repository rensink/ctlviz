CTLViz: Visualising CTL evidence
================================

This artefact accompanies the SPIN 2026 submission "Visualising CTL witnesses and counterexamples". It contains a demonstrator for the visualisation ideas described in the paper.


Installation and usage
----------------------

The artefact consists of a single `.jar` file, compiled under Java 21, which includes all necessary dependencies and hence can be run simply as

    java -jar ctlviz-obf-1.0.0
	
This will invoke the main class, `nl.utwente.ctlviz.GameDemo` (functionality described below).

The suffix `-obf` stands for "obfuscated": the graph visualisation engine uses [YFiles for Java](https://www.yfiles.com/?utm_source=groove&utm_medium=web&utm_campaign=promo); the tool has been developed using an [academic licence](https://www.yworks.com/products/yfiles-for-java/sla) that stipulates that it may only be distributed in this way.

Functionality
-------------

This demonstrator allows you to run and visualise a number of pre-programmed CTL queries on the simple game model described in the paper. The queries are:

1. `AF(win|los|ini)`: Every path reaches a winning state, a losing state, or the initial state

2. `EF win`: Winning is reachable

3. `E !d2 U win`: Winning is reachable without throwing 2

4. `EF(trw & AF win)`: There is a reachable state in which you are about to throw and will always win

5. `EF(trw & AF los)`: There is a reachable state in which you are about to throw and will always lost

6. `EX EF ini`: There is a cycle back to the initial state

7. `A (EF los) U win`: Losing always remains reachable until you win

8. `AX (d1 -> AF los)`: If you initially throw 1, you will certainly loas

9. `AG EF (win|los)`: Winning or losing always remains reachable

10. `AG (trw -> EG !(win|los))`: In every reachable state where you are about to throw, it is possible that you will never win or lose

11. `trw -> !(win|los)`: If you are abole to throw, then you have neither won nor lost

12. `E !d1 U win`: It is possible to win without throwing 1

13. `E !d1 U los`: It is possible to lose without throwing 1

14. `EG (EF win) & !win`: There is a path along which winning remains reachable but is never reached

To visualise one or more of these queries, put their number(s) as arguments in the invocation, e.g.:

    java -jar ctlviz-obf-1.0.0 13 14

Without arguments, the invocation will only show the Kripke model on which the queries are checked, and a usage message with the above content.

License
-------

With the exception of the (obfuscated) YFiles library, the code is open souce, and available under the Apache License, Version 2.0. The source files under the Apache license are included in the `.jar`

In particular, from the `GameDemo` class it is straightforward to see how you can create your own Kripke model and queries in a Java source file, and invoke the visualisation. This can then be run using `ctlviz-obj-1.0.0` as a library.

