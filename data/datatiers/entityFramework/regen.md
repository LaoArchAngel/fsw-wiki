# Regenerating Entity Framework Data Tiers

This document goes over the steps of regenerating an
[Entity Framework](https://msdn.microsoft.com/en-us/data/ee712907) data tier.
These instructions are generic to most entity framework setups, but more
detailed or specific instructions may be available or necessary for the data
tier of specific domains.

## Overview

1. Create a [data tier regeneration branch](1).
* Load a [clean solution](2).
* Refresh the Entity Framework model.
* Regenerate entity files.
* Merge Request.

## Procedure

### Data Tier Regeneration Branch

There are plenty of different situations that require a data tier regeneration.
The branching strategies for these situations are mainly going to be the same,
but will occasionally differ greatly.  Identifying those situations and their
branching strategies are beyond the scope of this document.  Please see the
[git Data Tier Regeneration Branching](1) document.

In any case, it is highly recommended that a clean branch be created solely for
data tier regenerations.  This will provide greater flexibility and problem
resolution strategies should something be wrong with the regeneration.

### Load a Clean Solution

Ensuring that the repository is clean during a data tier regeneration ensures
that regeneration and merging can be done ans quickly and flexibly as possible.
Should a problem occur with the data tier regeneration, even if it has nothing
to do with changes being inadvertently included with the regeneration, it will
make keeping both the regeneration and the extra changes extremely painful.

Please read the instructions for [cleaning your repository](2) to ensure you
are not in danger of including unrelated changes.

### Refresh the Entity Framework model

1. Find and open the EDMX file associated to your specific Entity Framework
model.
  * For example, the Fsw4.0 solution, the *Main* data model is
  `$/Core/Domain/Fsw3/Domain/Entities/Main/FswModel.edmx`.
  * Opening the EDMX file will likely result in one of the model diagrams being
  open.  If no diagram is available, an empty-looking tab will load.
* Right-click in the EDMX tab and select **Update Model from Database...**.
* An Update Wizard will appear.  He is level 15, has a 28 Charisma and knows
three level 8 spells.
  * In the **Add** tab, expand and select any *Tables*, *Views*,
  *Stored Procedures* and *Functions* that you added to the database.
    * Do not worry about adding parts that were added by other people.
    * Ensure that the three checkboxes under the list objects are checked.
  * In the **Refresh** tab, ensure that your database objects that were already
  in the database appear in the list.
  * In the **Delete** tab, ensure that the objects you removed from the database
  are on the list and no other objects.
    * If objects you did not delete from the database appear in this list, inform
    your team lead and try to determine if someone else is making similar changes
  * Click the **Finish** button at the bottom and wait for the process to finish.
  to the database.  Coordinate these changes as much as possible.


[1]: ../git/branching/dataTierRegen
[2]: ../git/cleanRepo
