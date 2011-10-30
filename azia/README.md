Azia User Interface Library
---------------------------

*Compositional architecture and transactional execution for Java* 
*desktop applications.*

The **azia** project is the parent of 3 Java modules that comprise 
the prototype implementation of the [Azia User Interface Library]
[website].

[website]: http://www.hawkinssoftware.net/oss/azia

1. [azia-core], a transaction framework 
2. [azia-input], native keyboard and mouse processor
3. [azia-ui], user interface components

[azia-core]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-core/blob/master/azia-core/README.md
[azia-input]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-input/blob/master/azia-input/README.md
[azia-ui]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-ui/blob/master/azia-ui/README.md

#### Usage

1. Add the 3 Azia modules as project dependencies 
1. Deploy the [native library] to the `java.library.path`
1. Integrate [Role Normalization and Synthesis] [rns] 

[native library]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-input/tree/master/azia-input/src/main/resources/native
[rns]: https://github.com/byron-hawkins/org.hawkinssoftware.rns/blob/master/rns/README.md

For an example of Azia usage, see the [Scrap Menagerie]
[scrap-menagerie], a simple clipboard management utilty.

[scrap-menagerie]: https://github.com/byron-hawkins/org.hawkinssoftware.scrap-menagerie/blob/master/scrap-menagerie/README.md

#### Resources

1. All artifacts are made available under the accompanying
   [Eclipse Public License v1.0][License]
2. Source code may be obtained from [GitHub]
3. Snapshots are available from my [Maven repository][snapshots]
4. Documentation can be found at [HawkinsSoftware][website]   

[License]: http://www.eclipse.org/legal/epl-v10.html
[GitHub]: https://www.github.com/byron-hawkins
[snapshots]: https://www.github.com/byron-hawkins/snapshots

#### Features

1. Compositional Architecture
    * User interface components built with simple, reusable parts
    * <code>[CompositionRegistry]</code> simplifies wiring by
      transparently integrating components
    * Minimal differences between simple components, compound
      components, cell renderers and cell editors
    * Supports instance-per-cell or flyweight tables and lists
1. Transactional Execution
    * All mutable fields locked under semaphores
        + Field access monitored at runtime by RNS
        + Automatic lock acquisition by azia-core transactions
        + Cross-lock conditions detected and resolved internally
    * Valid transaction usage maintained by RNS
    * All threads eligible for transactions and screen painting
    * Any object may join any transaction
        + Developer may restrict participation using RNS
    * Every action published to every paritcipant before commit
    * Transaction may sequence, consolidate, or otherwise adjust
      its actions before commit
1. Universal component access 
    * <code>[ComponentRegistry]</code> provides global component
      lookup from the application code 
        + e.g., a selection controller may look up its list
    * <code>[CompositionRegistry]</code> provides context-relevant
      lookup from within application-generic component code 
        + e.g., scrollbar button may look up its scroll pane
1. Instrumentation of message routing for cast-free type safety
1. Stack-based rendering API
    * Maintains correct Graphics pipeline state
        + User changes automatically reverted on method exit
    * Guarantees strictly narrowing clip bounds
1. <code>[PainterRegistry]</code> supports deployment-time
   configuration of component appearance
    * Component sizing is specified by the painters, allowing each
      painter implementation to have dimensional variations
1. Access to raw OS mouse and keyboard input messages
1. System clipboard changes are broadcast to listeners

[ComponentRegistry]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-ui/blob/master/azia-ui/src/main/java/org/hawkinssoftware/azia/ui/component/ComponentRegistry.java
[CompositionRegistry]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-ui/blob/master/azia-ui/src/main/java/org/hawkinssoftware/azia/ui/component/composition/CompositionRegistry.java
[PainterRegistry]: https://github.com/byron-hawkins/org.hawkinssoftware.azia-ui/blob/master/azia-ui/src/main/java/org/hawkinssoftware/azia/ui/paint/PainterRegistry.java
