# APIs

## Acryonyms

- SOAP: Simple Object Access Protocol
- RPC:  Remote Procedure Call
- REST: Representational State Transfer

- WSDL: Web Service Definition Language
- XML:  Extensible Markup Language
- JSON: Javascript Object Notation
- URI:  Uniform Resource Identifier
- YAML: YAML Ain't Markup Language

- HATEOAS:  Hypermedia As The Engine Of Application State

## SOAP (Simple Objective Access Protocol)

- developed by MS in 1998
- aimed at web applications
- relies on WSDL and XML
- SOAP calls can retain state, something that REST is not designed to do

## JSON

- introduced in 2002

## RPC (Remote Procedure Call)

- faster and easier to implement than SOAP
- however, RPC calls are tightly coupled and require the user to know the procedure name and order of parameters
- suffers from tightly-coupled URIs

## Stateless

API calls are made independently of each other, and each call contains all the necessary data to complete itself. The (REST) API should not rely on data being stored on the server or sessions to process a call, but rather, solely rely on the data in the call to function.


