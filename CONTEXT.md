# Checklist Management

The checklist-management context defines versioned checklist templates and their runtime instances for a single organisation.

## Language

**Administrator**:
A User authorised to author and maintain Checklist Templates.
_Avoid_: Admin application, template owner

**User**:
A registered person who may be eligible to action or approve Checklist Items.
_Avoid_: Account, assignee

**Checklist Template**:
A versioned definition of a checklist, including its item structure, eligibility rules, and dependencies.
_Avoid_: Checklist instance, checklist

**Checklist Template Version**:
An immutable published snapshot of a Checklist Template.
_Avoid_: Template revision, mutable template

**Checklist Item Definition**:
An item declared in a Checklist Template Version, including its action mode, eligibility, and prerequisites.
_Avoid_: Checklist Item, task

**Checklist Instance**:
A runtime checklist created from one specific Checklist Template version.
_Avoid_: Template, checklist

**Checklist Item**:
The runtime work item created from a Checklist Item Definition within a Checklist Instance.
_Avoid_: Checklist Item Definition, task

**Successful Terminal State**:
The completed or approved state that satisfies a Checklist Item's dependents.
_Avoid_: Completion, terminal state

**Action Record**:
An append-only auditable record of an action or approval performed by a User on a Checklist Item.
_Avoid_: Audit log, history entry
