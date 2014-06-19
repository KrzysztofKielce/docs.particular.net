title: Message Handling Pipeline
summary: Overview of the message handling pipeline 
tags:
- Pipeline
- NServiceBus
---

NServiceBus v5 introduces a new message handling pipeline whose role is to allow end users to easily extend and replace built-in behaviors.

The pipeline is focused on the message lifecycle and is composed of `behaviors` whose role is to manage every single aspect of the message lifecycle during the incoming phase and during the outgoing phase.

The default pipeline is composed of several behaviors, each one dedicated to a specific aspect of the message lifecycle, the default behaviors are the following:

###Incoming Message Behaviors

* CreateChildContainer, typeof(ChildContainerBehavior), "Creates the child container");
* ExecuteUnitOfWork, typeof(UnitOfWorkBehavior), "Executes the UoW");
            
###Outgoing Message Behaviors

* EnforceBestPractices, typeof(SendValidatorBehavior), "Enforces messaging best practices");

The following picture summurize the message lifecycle pipeline:

![001_pipeline.jpg](message lifecycle pipeline)

###Anatomy of a Message Behaviors




I behavior possono essere rimpiazzati, aggiunti o rimossi, un bejavior implementa IBehavior<TContext> dove TContext determina se il bejavior è outgoing o incoming

di default l'aggiunta di un behavior lo piazza in coda a quelli esistenti, per poter determinare dove inserirlo è necessario creare un RegisterBehavior custom che possa definire le dipendenze, e quindi chi deve venire prima chi dopo o entrambi

al fine di iniettare roba nella pipeline: INeedInitialization