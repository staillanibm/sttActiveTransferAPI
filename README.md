#   webMethods Active Transfer API

This repo provides information to use the Active Transfer API in order to automate the management of assets.  
The assets in question are described in [this document](./assets.md)

##  API overview

The API can be used to:
-   export the assets to XML documents
-   import the assets from XML documents
-   perform CRUD (Create / Read / Update / Delete) operations on most of the asset types
-   manage the status of some of the assets
-   generate PGP key pairs
  
All these APIs call flow services that are deployed in the Integration Server that supports Active Transfer. Most of these services are documented in the [IBM documentation portal](https://www.ibm.com/docs/en/webmethods-activetransfer/11.1.0?topic=activetransfer-introduction-webmethodsactivetransfer-built-inservices-reference)  
This official documentation does not explicitely mention APIs, but we rely here on a built-in Integration Server feature that makes it possible to invoke a flow service using HTTP and JSON.

##  Configuration as code objectives

The XML documents can be used to manage the assets in a "configuration as code" approach:
-   the XML documents are descriptors of the assets
-   they are placed in version control
-   each time we deploy an Active Transfer, we import the assets' XMl files to reflect what's in version control
-   to change these assets, we modify the XML files and perform the imports again

However these XML documents have a limitation: they cannot be used to set passwords and other secrets. The export and import APIs only work with encrypted password, and the encryption keys vary from one environment to the other.  
Three resource types are concerned:
-   Certificates (passwords used to protect the keys)
-   Virtual Folders (passwords and other tokens used to connect to external storage systems)
-   Users (passwords), although the good practice as far as users are concerned is to delegate authentication to a third party LDAP / AD / IdP

To deal with passwords of these asset types, we can use the CRUD APIs.  

##  Postman collection and environment

[Postman collection](./webMethodsMFT.postman_collection.json)
[Postman environment](./webMethodsMFT.postman_environment.json) 


