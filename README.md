# crud-protocol
Contains the specification of a basic CRUD protocol. 


## Description

Simple CRUD editors are sometimes needed, and often we wish to spend as little time as possible to develop those. Typically we build these in three layers: a SPA
for the UI, a service to encapsulate the resource(s) and some kind of storage. Each team is free to implement this as they see fit, but since there's often
quite some similarities in what they need, it makes sense to offer some level of code re-use.

This repository contains only a description of a possible CRUD protocol, which is an iteration over the work of a particular team. The idea is that all the basic operations
are consistently implemented in the same way. This allows us to use simple tools like
`ng-admin` to quickly build on top of it.

At the same time, the protocol is not set in stone because often there are specific business rules that make the editors just a little more complex than these
basic operations. These can be things like 'deletes are not allowed' (simply don't implement the delete operation) to more complex cases where specific UI
controls and API operations need to be implemented.

Some implementations:
* Go [github.com/Travix-International/crud-go](https://github.com/Travix-International/crud-go)
* .NET Core _(not publicly available yet)_

Usage of `ng-admin` is currently available in our private repos only.

The protocol offers guidance on the basic structure for:
* Basic operations (getting a list, getting an item by ID, creating, updating and deleting)
* Paging, multi-field filtering, sorting
* Usage of HTTP status codes
* Structured error reporting


### [Crud Protocol](https://github.com/Travix-International/crud-protocol/blob/master/CrudProtocol.md)
