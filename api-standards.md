# Victorian Government API design standards - DRAFT FOR REVIEW

Design standards for Whole of Victorian Government (WoVG) Application Programming Interfaces (API)s. 

**Draft under review** from the Department of Premier and Cabinet API Team.

# Introduction
The goal of this document is to ensure consistency and standardisation when designing and building APIs to be used by agencies across the whole of Victorian Government (WoVG). Our mission is to ensure the highest standards are obtained by defining a base level of delivery and only describing expansion when further comment is required.

The intent is to maintain a living document that adapts to changes in the landscape of web API delivery but at the same time being mindful of established standards presently adopted inside and outside the WoVG.

It is expected that anything not described in this document is to be implemented from best practices with a view of interoperability, maintainability and future direction. Gaps, errors or new best practices should be brought to the attention of The API Team [apiteam@dpc.vic.gov.au](mailto:apiteam@dpc.vic.gov.au).

<br />
### Document audience
The audience for this document is API developers, solution architects and business analysts designing a new API or making changes to an existing service in order to improve aspects of usability, readability or security.

This document has been written for use principally within the Victorian Government. However, it is being released for broader adoption by individuals or organisations wanting to build APIs that are interoperable with the WoVG standard.

<br />
### Document semantics, formatting, and naming
The keywords `MUST`, `MUST NOT`, `REQUIRED`, `SHALL`, `SHALL NOT`, `SHOULD`, `SHOULD NOT`, `RECOMMENDED`, `MAY`, and `OPTIONAL` in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

The words `REST` and `RESTful` **MUST** be written as presented here, representing the acronym as all upper-case letters. This is also true of `JSON`, `XML` and other acronyms.

Machine-readable text, such as URLs, HTTP verbs and source code, are represented using a fixed-width font.

<br />
______________________________________________________________________________
# Contact information

API Team<br/>
Digital, Design and Innovation<br/>
Department of Premier and Cabinet<br/>
[apiteam@dpc.vic.gov.au](mailto:apiteam@dpc.vic.gov.au)

<br />
______________________________________________________________________________
# Table of contents

* [1. Getting Started: Building an API](#1) 
  * [1.1 Building APIs in Government](#1-1) 
  * [1.2 API as a Product](#1-2) 
  * [1.3 Applying the standard](#1-3) 
  * [1.4 Privacy and Security](#1-4) 
  * [1.5 Sample Swagger Definition](#1-5) 
  * [1.6 The choice behind REST](#1-6) 
* [2. Interpreting These Guidelines](#2) 
  * [2.1 Terms Used](#2-1) 
    * [2.1.1 API](#2-1-1) 
    * [2.1.2 Resource](#2-1-2) 
    * [2.1.3 Resource Identifier](#2-1-3) 
    * [2.1.4 Representation](#2-1-4) 
    * [2.1.5 Namespace](#2-1-5) 
    * [2.1.6 Operation](#2-1-6) 
* [3. WoVG API Requirements](#3) 
    * [3.1 API Documentation](#3-1) 
    * [3.2 API Development](#3-2) 
    * [3.3 API Developer Experience & Ease of Use](#3-3) 
    * [3.4 API Stability](#3-4) 
* [4. Naming Conventions](#4) 
  * [4.1 Message Format](#4-1) 
  * [4.2 URI Component Names](#4-2) 
    * [4.2.1 URI Components](#4-2-1) 
    * [4.2.2 URI Naming Conventions](#4-2-2) 
    * [4.2.3 Resource Names](#4-2-3) 
    * [4.2.4 Query Parameter Names](#4-2-4) 
  * [4.3 Field Names](#4-3) 
  * [4.4 Link Relation Names](#4-4) 
  * [4.5 Request Headers](#4-5) 
  * [4.6 Examples](#4-6) 
    * [4.6.1 Good URL examples](#4-6-1) 
    * [4.6.2 Bad URL examples](#4-6-2) 
* [5. API Versioning](#5) 
  * [5.1 Versioning Scheme](#5-1) 
  * [5.2 Major Version](#5-2) 
    * [5.2.1 Minimise New Major Versions](#5-2-1) 
  * [5.3 Minor Version](#5-3) 
  * [5.4 Minor and Patch Documentation](#5-4) 
  * [5.5 Backwards Compatibility](#5-5) 
  * [5.6 End of Life Policy](#5-6) 
    * [5.6.1 Minor API Version EOL](#5-6-1) 
    * [5.6.2 Major API Version EOL](#5-6-2) 
    * [5.6.3 Replacement Major API Version](#5-6-3) 
  * [5.7 API Deprecation](#5-7) 
* [6. API Request](#6) 
  * [6.1 Request Headers](#6-1) 
  * [6.2 HTTP Request Methods](#6-2) 
    * [6.2.1 Supported HTTP request methods](#6-2-1) 
    * [6.2.2 Collection of Resources](#6-2-2) 
    * [6.2.3 Single Resource](#6-2-3) 
  * [6.3 Request Payload Formats](#6-3) 
* [7. Query Parameters](#7) 
  * [7.1 Pagination](#7-1) 
    * [7.1.1 Parameters](#7-1-1) 
    * [7.1.2 Metadata](#7-1-2) 
  * [7.2 Filtering and Sorting](#7-2) 
    * [7.2.1 Output Selection](#7-2-1) 
    * [7.2.2 Simple Filtering](#7-2-2) 
    * [7.2.3 Advanced Filtering](#7-2-3) 
    * [7.2.4 Match Case Sensitivity](#7-2-4) 
    * [7.2.5 Sorting](#7-2-5) 
* [8. API Responses](#8) 
  * [8.1 Response Headers](#8-1) 
  * [8.2 HTTP Response Codes](#8-2) 
  * [8.3 Response Payload](#8-3) 
    * [8.3.1 Single Resource](#8-3-1) 
    * [8.3.2 Collection of Resources](#8-3-2) 
* [9. Error Handling](#9) 
  * [9.1 Error Response Payload](#9-1) 
  * [9.2 Input Validation](#9-2) 
  * [9.3 Error Samples](#9-3) 
* [10. API Security](#10) 
  * [10.1 API Design](#10-1) 
  * [10.2 Transport Security](#10-2) 
  * [10.3 Authentication and Authorization](#10-3) 
  * [10.4 Abstraction](#10-4) 
  * [10.5 Rate Limiting](#10-5) 
  * [10.6 Error Handling](#10-6) 
  * [10.7 Audit Logs](#10-7) 
  * [10.8 Input Validation](#10-8) 
  * [10.9 Content Type Validation](#10-9) 
  * [10.10 Gateway Security Features](#10-10) 
* [11. Hypermedia](#11) 
  * [11.1 Hypermedia - Linked Data](#11-1) 
  * [11.2 HATEOAS](#11-2) 
  * [11.3 Hypermedia Compliant API](#11-3) 
  * [11.4 Link Description Object](#11-4) 
  * [11.5 Link Relation Type](#11-5) 
* [12. Networking](#12) 
  * [12.1 Caching](#12-1) 
    * [12.1.1 Cache-Control](#12-1-1) 
    * [12.1.2 Expires](#12-1-2) 
    * [12.1.3 Caching in the API Gateway](#12-1-3) 
* [13. Webhooks](#13) 
  * [13.1 Current Guidance](#13-1) 
* [14. Testing](#14) 
  * [14.1 Testing Tools](#14-1) 
* [References](#refs)

<br />
______________________________________________________________________________
<h1 id="1">1. Getting started: Building an API</h1>
<h2 id="1-1">1.1 Building APIs in government</h2>

Government services are increasingly becoming digitised vastly increasing challenges like connectivity, service interoperability and data security. These challenges ensure departmental executives require API and integrations strategies as critical components of their technology arsenal in order to streamline services, simplify existing environments and de-risk implementations.

A number of online resources exist that teams, agencies and departments can utilise when looking to building and launch APIs and integrations - there was however a gap in official, ratified standards in the API and integration space and even more so within the Product Management community around APIs in government.

To address these challenges in March 2018 the Digital Engagement group as part of the Department of Premier and Cabinet formed the Whole of Victorian Government (WoVG) API Gateway team. This team is charged with:

- Creation of technology to support the development and exposure of APIs across the Victorian Government
- Creation and collaboration holistic API design standards to be used across the WoVG
- Consultation, training and support to improve overall literacy around APIs and Integrations
- Engagement and evangelism of APIs and integrations both internally in government and out to partners and the community

The sections that follow describe a high-level overview of the engagement process that the API Team works through with agencies that are looking to launch API capabilities across the WoVG. These can be referenced here or from the API Team directly at [apiteam@dpc.vic.gov.au](mailto:apiteam@dpc.vic.gov.au).

<h2 id="1-2">1.2 API as a product</h2>

APIs facilitate information sharing both within an organisation and outside of the organisation. Careful design considerations must be applied to ensure APIs are fit for purpose and can be easily consumed. One method to achieve this is to treat any API as a product within an organisation and manage it appropriately.

To productise an API, it requires an API owner who will act as an advocate for the customers. Someone who will work closely with the API designer to seek out opportunities for continual improvement in the API.

APIs should be customer-centric – engage with the customer early in the design process to have a clear understanding of the customer needs. The design should follow user experience principles. Perform usability testing and address gaps as needed.

Below is a brief description of the phases of the API life cycle:   

- **Define** – Working with various stakeholders to identify the APIs to deliver the business requirements. Typically, the API abstraction requirement (BASIC, INTERMEDIATE, ADVANCED), specification and data model forms the output of this life cycle. 
 
- **Develop** – Design and develop the APIs. Design consideration should be given to; security, performance, policy requirement, error handling, scalability and monitoring. API mock services should be developed in parallel to allow early integration with the API consumers. A working API and continuous integration are outputs of this phase
  
- **Test** – Multiple test phases are applied to ensure the APIs are developed with the required quality and standards. Underpinning this can be continuous integration used with other test automation tools. 
  
- **Publish** – Follows continuous delivery principles to deploy the APIs to a secure environment and publish them to the consumers. Support plans and operational guides are produced. 
  
- **Support** – Provide community forums for consumers to interact, collaborate, and request for change/enhancement.  
  
- **Governance** – is applied to all phases to ensure accuracy, consistency, security, standards and principles requirements are met. A catalogue system can be used to assist the API lifecycle.
  
- **Monitor** – Monitor the APIs in real time with alerts being raised directly or via a network management system (NMS). Trends analysis can be derived from historical data and aggregated transaction logs to discover usage and adoption.
  
- **Operations** – Follows release and change management processes to ensure approved version of APIs are deployed to production. 
  
- **Retire** – Formal announcements and notifications to be sent to the API consumers. Announcement strategy can include a sunset timestamp in the HTTP Response header. Decommissioned APIs should return an HTTP 410 status code and include an end-of-life response message.

<h2 id="1-3">1.3 Applying the standard</h2>

Knowing how and when to apply the API Design Standards will significantly influence the API Solution Design approach that you will take as an API Designer.  

Determining when to use the standard is based on the API Category and the required level of abstraction required. 

|Factor|Description|
|---|---|
|API Category | An API will generally fall into one of the following categories:<br/><br/>**System Level APIs**: These are low-level system APIs that are exposed directly by an application.<br/><br/>**Process Level APIs**: These are APIs composed of other system APIs through orchestration and choreography.<br/><br/>**Experience Level APIs**: These are APIs intended to ease the adoption of API integration between an organisation and its external consumers. 

The level of abstraction applied to an API will vary depending on its intended reusability and the number of consumers.  

If there is no intention to reuse the API interface (i.e. point to point), then a **BASIC** level of abstraction is sufficient. If the number of consumers is likely to be high, then an **ADVANCED** level of abstraction is required to minimise impact to consumers when underlying systems are changed. Refer to the [Abstraction](#10-4) section of this standard for further information.

**Notes:**

- If your API falls into the System level API and is custom developed, it is **RECOMMENDED** that you use the standard as this will assist in developing Process or Experience level APIs if they are required in future.

- If your API is a Process Level API, it is **HIGHLY RECOMMENDED** that you apply the standard as more often than not, a process level API will be tailored for re-usability. 

- If your API is an Experience Level API, then the standards **MUST** be applied.

This design guide itself does NOT apply to third-party System level APIs such as those available as ‘out-of-the-box’ or as part of SaaS platform (eg Salesforce APIs or ArcGIS APIs). However, the standard may apply if you were looking to re-expose these APIs as experience-level APIs for wider consumption.

<h2 id="1-4">1.4 Privacy and security</h2>

The security of the API must take a risk-based approach to determine the level of security controls required (based on the security classification of the information being exchanged).  

It is highly recommended that a security classification is conducted on the information data model during the design of the API so that the appropriate security controls can be taken into consideration early.  

The data classification model used by the Victorian Government currently includes:

- UNOFFICIAL
- PUBLIC
- UNCLASSIFIED
- FOR OFFICIAL USE ONLY
- PROTECTED

All APIs published through the platform (at a minimum), **MUST** have a policy that only allows access based on a valid API key. As the level of classification increases stricter security policies and controls need to be applied - both within the platform as well as within the back-end API system itself.  

For example if the data classification resulted in PROTECTED, digital certificates may be required between the API and the API Consumer for authentication, encryption and non-repudiation. 

It is important to note the types of data you will be sharing and what protective markings are required to ensure this is shared appropriately.

<h2 id="1-5">1.5 Sample Swagger definition</h2>
A sample Swagger template that exposes APIs methods and conforms to the Service Design Guide is provided here to help API Designers get started.

The template is available in [JSON format](api-example-swagger-v1.4.json). 

API Designers can use this template as a basis to start their API definition from a standards-compliant starting point.

Once the Swagger definition has been copied, designers can perform the following tasks:

1. Provide a relevant description of the API – Refer to line number 5.
2. Review and update the description
3. For each method:

    - Update the field definition
    - Update the description
    - Provide examples
    - Review the status codes and error messages and update as required

**NB. This Swagger example demonstrates how an API could be defined. Always check the the repository for the latest copy of the template and examples.**

<h2 id="1-6">1.6 The choice behind REST</h2>

Modern developers have largely accepted REST as the de-facto mechanism of data representation and transfer to/and from systems on the internet.

REST performs well when modelling systems and data. The principles can be applied to systems that are both large and small and the tooling available to developers largely supports data access out of the box.

REST APIs typically are not good for streaming data (websockets) nor are they the best use for largely function based APIs (JSON-RPC). GraphQL is an alternative that handles these aspects of development in a different way and was considered as an option for WoVG standards.

As the tooling for REST APIs is far more advanced, and the general technology literacy across government is already reasonably versed with REST APIs and design principles, it was determined that REST would be the de-facto standard for APIs in the Victorian Government.

______________________________________________________________________________
<h1 id="2">2. Interpreting these guidelines</h1>
<h2 id="2-1">2.1 Terms used</h2>
<h3 id="2-1-1">2.1.1 API</h3>
In the context of this Service Design Guide an API (Application Programming Interface) is defined as a RESTful API.  

A RESTful API is a style of communication between systems where resources are defined by URI and its operations are defined by the use of HTTP methods. 

A RESTful API adopts many HTTP standards such as response codes and methods.

<h3 id="2-1-2">2.1.2 Resource</h3>

In order to design a useful and clean API your system should be broken down into logical groupings (often called Models or Resources). In most cases the resources are the 'nouns' of your system.

In the example of an HR system, the resources would be things like `employees`, `positions` and `leaverequests`.

By breaking systems down into these logical areas it allows a clean separation of concerns (eg employee functions only work on `employees` and only `employees` can apply for `leaverequests`). It also ensures that each piece of data that is returned from your API is the smallest that it needs to be to fulfil the client requirement (eg when asking for `employees` you don't also receive back `familymembers`).

<h3 id="2-1-3">2.1.3 Resource identifier</h3>

Every _resource_ that is available within your system (eg every `employee` or every `leaverequest`) must be identifiable uniquely within the system. This is a key element of the RESTful style of APIs; the ability to individually address any item within your system and store these identifiers for later use.

Resource identifiers can be any of the following:

Name|Example|
--- | --- |
Numeric|`/employees/12389`
String|`/employees/john-smith`
GUID | `/employees/0d047d80-eb69-4665-9395-6df5a5e569a4`
Date (Short form) | `/dates/2018-09-17`

As long as the identifier is unique within your application it can be any string of characters or numbers. It is RECOMMENDED that if numeric IDs are used, they are not sequential (eg it is not trivial to guess the next ID).

<br /><br />
<h3 id="2-1-4">2.1.4 Representation</h3>

A key concept in RESTful API design is the idea of the representation of a resource at any particular time.

When you ask the system for employee information you will receive a representation of that employee.

Example: 

```
HTTP 1.1 GET /employees/john-smith
Accept: application/json

200 OK
Content-Type: application/json

{
  "_embedded" : {
    "name" : "John Smith",
    "empId" : "123456",
    "position" : "Manager",
    "onLeave" : false
  }
}
```

The intent is this representation can change over time as the system and data within changes. A future call to this same endpoint may yield a different representation possibly if the employee is now on leave or their position within the organisation has changed.

It is also possible to request an entirely different representation of this same resource if the system supports it. For example, there may be a case where you require a PDF version of this employee and this could be facilitated with a request for a different representation through the `Accept` header:

```
HTTP 1.1 GET /employees/john-smith
Accept: application/pdf

200 OK
Content-Type: application/pdf

...<BINARY CODE>...
```

More information about representations and how to support them is provided in the [Hypermedia](#11) section of this document.

<h3 id="2-1-5">2.1.5 Namespace</h3>

The namespace for a service defines the grouping of related functions within. Namespaces could be quite high level (eg an agency or department name) or quite low level (eg a project, team or service being exposed).

Namespaces are useful when providing consumers access to related functions through gateway technologies. Once a consumer has an access token to a particular namespace it is likely (though not always required) that they will get access to all functions supplied within that namespace.

To get a namespace allocated to your team or project please speak to the API Team [apiteam@dpc.vic.gov.au](mailto:apiteam@dpc.vic.gov.au).

<h3 id="2-1-6">2.1.6 Operation</h3>

To make use of any of the namespaces, resources and resource identifiers, developers must make use of Operations.

An operation is defined by the use of:

- an HTTP method; and
- a resource path.
  
Examples:
```javascript
GET /employees
DELETE /employees/john-smith
GET /employees/john-smith
```

______________________________________________________________________________
<h1 id="3">3. WoVG API requirements</h1>
<h2 id="3-1">3.1 API documentation</h2>

Well-documented APIs are a critical component of a successful API programme. All APIs created for the Victorian government **MUST** specify a valid OpenAPI v2 document. 

This assists with the interoperability of services through a common descriptive document. Where possible the structure, methods, naming conventions and responses will also be standardised to ensure a common experience for developers accessing services from a range of publishers.

The API description document is **RECOMMENDED** to contain the following sections:

- About
- Legals
  - Terms of Use
  - License
  - Data Classification
  - Copyright
  - Attribution
- Authentication Requirements
- Data Model
- Contact Us

Agencies can engage the services of the DPC WoVG API Team to assist with authoring this document if required [apiteam@dpc.vic.gov.au](mailto:apiteam@dpc.vic.gov.au).

<h2 id="3-2">3.2 API development</h2>

The following guidelines are **RECOMMENDED** be followed when developing APIs:

- The API description documents **SHOULD** contain the API documentation (high level information and descriptions) and version controlled accordingly. 
  
- They **MUST** be considered as technical contracts between designers and developers and between consumers and providers. 
  
- Mock APIs **SHOULD** be created using the API description to allow early code integration for development
  
- The behaviour and intent of the API **SHOULD** be described with as much information as possible.
  
- The descriptions **SHOULD** contain example of request and responses
  
- Documentation **SHOULD** be public where possible and easily accessible to those that require it
  
- Example request and response bodies **SHOULD** be provided in full - not truncated
  
- Expected response codes and error messages **SHOULD** be provided in full
  
- Correct response codes **SHOULD** be used (ref: [Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes))
  
- Known issues or limitations **SHOULD** be clearly documented
  
- Expected performance, uptime and SLA/OLA **SHOULD** be clearly documented
  
- If known, a timeline when methods will be deprecated **SHOULD** be provided
  
- Documentations **SHOULD** be printable or exportable

#### Packaging

The Swagger description files must be available:

- **Online** : Serve as part of the product API under `/<namespace>/<project>/v<x>/api-docs`
- **Offline** : As part of the product packaging.

#### File Format

The required file format for the API Description is JSON since its most widely supported.

#### Versioning

In order to follow the versioning recommendations in this standard there must be one Swagger description per major version.

For example; if your API product exposes and maintains 3 major versions of its REST API then you must provide 3 Swagger descriptions (one for each version: v1, v2 and v3).

<h2 id="3-3">3.3 API developer experience and ease of use</h2>

An API that is difficult to use reduces the likelihood that consumers will continue to use it and will therefore seek alternatives. They will also be unlikely to recommend the API to others.

APIs that are being designed are **RECOMMENDED** to be tested with real consumers. Any feedback provided **SHOULD** be considered for incorporation into the API to ensure the best possible outcome.

The WoVG API Team provides an API review process to ensure APIs meet a baseline level of usability prior to them being published to potential consumers for feedback.

<h2 id="3-4">3.4 API stability</h2>

APIs **MUST** be designed with backwards compatibility in mind as when changes are introduced it is not likely that consumers will introduce these into their applications immediately.

In most cases introducing new fields to an API or adding new endpoints is a non-breaking change and can be introduced with a patch version update.

Should the API contract need to change in a manner that breaks the consumers contract this **SHOULD** be communicated clearly.

  1. API Product owners **SHOULD** document the support lifespan for API services (eg how long they will be supported).
  2. New functionality **MUST** be introduced in a way that does not impact existing consumers.
  3. Any deprecation activities **MUST** be known to consumers prior to them being put into effect.

______________________________________________________________________________
<h1 id="4">4. Naming conventions</h1>
<h2 id="4-1">4.1 Message format</h2>
For request and response body and query parameter names the message format is **RECOMMENDED** to use snake case:

Example:

```javascript
// this_is_snake_case

{
  "employee_id" : "AB1837" 
}
```

If snake case is not available, it is then **RECOMMENDED** to use camel case.

Example:

```javascript
// thisIsCamelCase

{
  "employeeId" : "AB1837" 
}
```

In either case the object and field definition must be the same for the request and response body and query parameters.

<h2 id="4-2">4.2 URI component names</h2>

URIs follow [RFC 3986](https://tools.ietf.org/html/rfc3986) specification. This specification simplifies REST API service development and consumption. 

The guidelines in this section govern your URI structure and semantics following the [RFC 3986](https://tools.ietf.org/html/rfc3986) constraints.

<h3 id="4-2-1">4.2.1 URI components</h3>

The structure of the URLs used within APIs **SHOULD** be meaningful to the consumers. URLs **SHOULD** follow a predictable, hierarchical structure to enhance understandability and therefore usability. 

URLs **MUST** follow the standard naming convention as described below:

```
   https://gw.api.vic.gov.au/namespace/v1/project-name?attributes=first_name,last_name
   \___/   \_______________/\________________________/\______________________________/
     |           |                |                   |                                   
  scheme     authority           path               query                             
```

<h3 id="4-2-2">4.2.2 URI naming conventions</h3>

URLs **MUST** follow the standard naming convention as described below:
- the URI **MUST** be specified in all lower case
- only hyphens '-' can be used to separate words or path parameters for readability (no spaces or underscores)
- only underscores '\_' can be used to separate words in query parameter names but not as part of the base URI

The following table provides a breakdown of how to construct the API URI.

| URI element | Description | Example |
| --- | --- | --- |
| Protocol | All APIs **MUST** be exposed using HTTPS. | `https:// `|
| Authority \> Environment | The domain of where the API endpoint will be exposed. Refer to the 'DNS' standard section for details. | `gw.api.vic.gov.au` |
| Path \> API | The API name which is derived from the business domain. | eg: `/namespace/project-name` <br />Any agency/department can specify the API name that they would like to expose their services on. |
| Path \> Version | The version of the API that is desired to be accessed by the consumer. | eg: `/v1` <br/> All APIs must specify a version that follow the versioning scheme as specified in 'versioning' below. |
| Path \> Collection | The collection identifies a list of resources. The collection **MUST** be named using the **plural** representation of a noun. | eg: As part of the workforce API - a resource could be a list of `employees`. |
| Path \> Resource | The resource identifier which corresponds to an instance of the resource. | eg: As part of the **project-name** API - if there was a specific employee with id E13454. <br />These details can be retrieved using `GET` `/project-name/v1/employees/E13455` |
| Query String \> Parameters/Filters | Query parameters **MUST** NOT be used to transport payload or actual data. <br/><br/>The following query parameters **SHOULD** be supported by your API where they would be useful:<br/><br/>**attributes** - specify or restrict the attributes to be returned<br/><br/>**filters** – conditions to restrict/filter the collection list<br/><br/>**sort** – specify the sort requirement<br/><br/>**page** – specify which pagination index to be return in a collection set | eg: `attributes=first_name,last_name` <br /> returns data element with only the `first_name` and `last_name` attributes<br/><br/>`filters=creation_date => 2001-09-20T13:00:00 and creation_date <= 2001-09-21T13:00:00 and first_name like 'fred' and post_code=3000` - return a collection of resources where the creation date is between 2001-09-20 1pm and 2001-09-21 1pm and first-name like 'fred' and post_code is 3000.<br/><br/>`sort=date_of_birth desc` - return a collection where the resources are sorted by date_of_birth in descending order.<br/><br/>`page=10` – returns the 10th page index

<h3 id="4-2-3">4.2.3 Resource names</h3>

API Designers **MUST** follow these principles when creating a REST API:
- Nouns **MUST** be used - not verbs for names.
- Resource names **MUST** be singular for singletons; collections' names **MUST** be plural.
- Resource names **MUST** be lower-case and use only alphabetic characters and hyphens.
- The hyphen character ( - ), MUST be used as a word separator in URI path parameters. 

**Note** that this is the only place where hyphens are used as a word separator. In nearly all other situations the underscore character ( _ ), **MUST** be used.

<h3 id="4-2-4">4.2.4 Query parameter names</h3>

- Literals/expressions in query strings **SHOULD** be separated using underscore ( _ ).
- Query parameters values **MUST** be percent-encoded.
- Query parameters **MUST** start with a letter and **SHOULD** be all in lower case. Only alpha characters, digits and the underscore ( _ ) character **SHALL** be used.
- Query parameters **SHOULD** be optional.
- Query parameters **SHOULD** not contain characters that are not URL safe.

<h2 id="4-3">4.3 Field names</h2>

The data model for the representation **MUST** conform to the `JSON` specification. 

The values may themselves be objects, strings, numbers, booleans, or arrays of objects.

- Key names MUST be lower-case words, separated by an underscore character ( _ ).
   - `foo`
   - `bar_baz`
- Prefix such as `is_` or `has_` **SHOULD NOT** be used for keys of type boolean.
- Fields that represent arrays **SHOULD** be named using plural nouns (eg authenticators - contains one or more authenticators, products - contains one or more products).

<h2 id="4-4">4.4 Link relation names</h2>

To help guide users through your API, relational links **MUST** be provided. These links act as the navigation of your API advising users of where they can go to next.

A `links` array **MUST** be provided for resources. This contains link objects that can refer to related resources in the system.

A link relation **MUST** contain the following elements:
- href - string containing the absolute or relative URL to the resource
- rel - the textual string describing what this entity is
- method - the HTTP method that **SHOULD** be used when using this related resource.

Example:

```javascript
"links": [
    {
        "href": "/v1/customer/partner-referrals/ALT-JFWXHGUV7VI",
        "rel": "_self",
        "method": "GET"
    }
]
```

<h2 id="4-5">4.5 Request headers</h2>

The following headers **SHOULD** be assumed by default on all requests.

|Header | Default value|
|---|---|
|Accept|`application/json`|

<h2 id="4-6">4.6 Examples</h2>
<h3 id="4-6-1">4.6.1 Examples of good URLs</h3>

List of employees:<br />
  `GET` https://gw.api.vic.gov.au/e09284/v1/employees<br />
Filtering is a query:<br />
  `GET` https://gw.api.vic.gov.au/e09284/v1/employees?year=2011&sort=desc<br />
  `GET` https://gw.api.vic.gov.au/e09284/v1/employees?section=economy&year=2011<br />
A single employee in JSON format:<br />
  `GET` https://gw.api.vic.gov.au/e09284/v1/employees/1234<br />
All locations this employee works in:<br />
  `GET` https://gw.api.vic.gov.au/e09284/v1/employees/1234/locations<br />
Specify optional fields in a comma separated list:<br />
  `GET` https://gw.api.vic.gov.au/e09284/v1/employees/1234?fields=job_title,start_date<br />
Add a new location to a particular employee:<br />
  `POST` https://gw.api.vic.gov.au/e09284/v1/employees/1234/locations<br />

<br />
<h3 id="4-6-2">4.6.2 Examples of bad URLs</h3>
Non-plural endpoint:<br />

  https://gw.api.vic.gov.au/e09284/v1/employee<br />
  https://gw.api.vic.gov.au/e09284/v1/employee/1234<br />
  https://gw.api.vic.gov.au/e09284/v1/employee/1234/location<br />

Verb in the URL:<br />
  https://gw.api.vic.gov.au/e09284/v1/employee/1234/create<br />

Filtering outside in the URL instead of the query string<br />
  https://gw.api.vic.gov.au/e09284/v1/employee/1234/desc<br />

______________________________________________________________________________
<h1 id="5">5. API Versioning</h1>
<h2 id="5-1">5.1 Versioning scheme</h2>

All APIs **MUST** adhere to [semantic versioning](https://semver.org/):

{MAJOR}.{MINOR}.{PATCH}

The first version of an API **MUST** always start with a MAJOR version of 1.

Use the following guidelines when incrementing the API version number:
- **MAJOR** version when you make **incompatible** or **breaking** API changes
- **MINOR** version when you add functionality in a backwards-compatible manner
- **PATCH** version when you make backwards-compatible bug fixes

<h2 id="5-2">5.2 Major version</h2>

All APIs **MUST** only include the MAJOR version as part of the URI in the format of 'v{MAJOR}' (eg
https://api.vic.gov.au/namespace/v1/employees).

The minor and patch version numbering is NOT required in the URI as the changes are backwards-compatible.

<h3 id="5-2-1">5.2.1 Minimise new major versions</h3>

With each new major version of the API, the older versions are required until all the consumers are uplifted to use the new versions. This adds to the overall maintenance and support requirements.

Use API keys to identify consumers and decommission older version(s) of the API with sufficient notification.

When new major versions are published the older version must be deprecated following the deprecation process in [5.7](#5-7)

<h2 id="5-3">5.3 Minor version</h2>

Minor version numbers are displayed on the API documentation page or part of a special management call to the API URI itself. To support this your API **MUST** implement a response to a GET request to the base URI of the API and return the following metadata in the response:
- **api_name:** The API name
- **api_version:** The API version with major and minor versions
- **api_released:** The date the API was released
- **api_documentation:** Links to the API documentation
- **api_status:** To indicate whether an API is still active or has been deprecated

Additional metadata can be added to the response if required.

Example:

```javascript
GET /namespace/v1/

//HTTP 200 OK

{
  "api_name": "namespace",
  "api_version": "1.0.3"
  "api_released": "2018-08-10"
  "api_documentation": "https://gw.api.vic.gov.au/namespace/v1/docs"
  "api_status": "active"
}

```

<h2 id="5-4">5.4 Minor and patch documentation</h2>

The Swagger definition **SHOULD** also contain the minor and patch version.

API product version and API implementation version are **NOT** the same. 

A product version is the logical version that is applied to the API for documentation and reference purpose. The implementation version is the physical build version that was created.

For example:

| Product version | API implementation version | Change Type | Version Change |
| --- | --- | --- | --- |
| 17.04.xx | 1.29.xx | Bug Fixes | Product version will be changed to **17.04.02** if changes are related to product. API implementation version will be changed to **1.29.02** if changes are related to API |
| 17.04.xx | 1.29.xx | Backward Compatible | Product version will be changed to **17.05.xx** if changes are related to product. API implementation version will be changed to **1.30.x** if changes are related to API |
| 17.04.xx | 1.29.xx | Non-Backward Compatible | Product version will be changed to **18.01.x** if changes are related to product. API implementation version will be changed to **2.00.x** if changes are related to API |

A patch update (patch or service pack) **MUST** have backward compatibility.

<h2 id="5-5">5.5 Backwards compatibility</h2>

It is critical that APIs are developed with loose coupling in mind to ensure backwards compatibility for consumers.

The following changes are deemed to be backwards compatible:

- Addition of a new field to a representation
- Addition of a new link to the `_links` array of a representation
- Addition of a new endpoint to an API
- Additional support of a new media type (eg `Accept: application/pdf`)

The following changes are **NOT** deemed to be backwards compatible:

- Removal of fields from representations
- Changes of data types on fields (eg string to boolean)
- Removal of endpoints or functions
- Removal of media type support

Any of these changes **MUST** require a major version update so these should be managed with caution.

<h2 id="5-6">5.6 End of life policy</h2>

When designing new APIs, one of the most important dates to consider is when the API will be retired.

APIs are not intended to last forever. Some APIs are retired after a short time as they may be proving a use-case, others may be removed when better options are available for users.

The End-of-life (EOL) policy determines the process that APIs go through to move through their workflow from `LIVE` to the `RETIRED` state. 

The EOL policy is designed to ensure a consistent and reasonable transition period for API customers who need to migrate from the old API version to the new API version while enabling a healthy process to retire technical debt.

<h3 id="5-6-1">5.6.1 Minor API version EOL</h3>

Per versioning policy, minor API versions MUST be backwards compatible with preceding minor versions within the same major version. Therfore minor API versions are `RETIRED` immediately after a newer minor version of the same major version becomes `LIVE`. This change should have no impact on existing subscribers so there is no need to transition through a `DEPRECATED` state to facilitate client migration.

<h3 id="5-6-2">5.6.2 Major API version EOL</h3>

Major API versions **MAY** be backwards compatible with preceding major versions. The following rules apply when retiring a major API version.

1. A major API **MUST NOT** be `DEPRECATED` state until a replacement service is `LIVE` that provides a clear migration path for all functionality that will be retained moving forward. This **SHOULD** include documentation and migration tools/sample code that provide users what they need to make a clean migration.
 
2. The deprecated API version **MUST** be in the `DEPRECATED` state for a minimum period of 60 days to give users adequate notice to migrate.
 
3. Deprecation of API versions with external users **SHOULD** be considered on a case-by-case basis and may require additional deprecation time and/or constraints to minimise impact to users.
 
4. If a versioned API in `LIVE` or `DEPRECATED` state has no registered users, it **MAY** move to the `RETIRED` state immediately.

<h3 id="5-6-3">5.6.3 Replacement major API version</h3>

Since a new major API version that results in deprecation of a pre-existing API version is a significant product investment API owners **MUST** justify the new major version before beginning significant design and development work.

API owners **SHOULD** explore all possible alternatives to introducing a new major API version with the objective of minimizing the impact on customers before deciding to introduce a new version. 

Justification **SHOULD** include the following:

#### Business case

1. Customer value delivered by new version that is not possible with existing version.
2. Cost-benefit analysis of deprecated version versus the new version.
3. Explanation of alternatives to introducing an new major version and why those were not chosen.
4. If a backwards incompatible change is required to address a critical security issue items 1 and 2 (above) are not required.

#### API design

1. A domain model of all resources in the new API version and how they compare to the domain model of the previous major API version.
2. Description of APIs operations and use cases they implement.
3. Definition of service level objectives for performance and availability that are equal or better to the major API version to be deprecated.

#### Migration strategy

1. Number of existing customers impacted; internal, external and partners.
2. Communication and support plan to inform existing customers of new version, value and migration path.

<h2 id="5-7">5.7 API deprecation</h2>

When a newer API is available API owners are **RECOMMENDED** to provide two headers in the response when old versions are used:

- X-API-Deprecated - boolean field advising that this has been deprecated
- X-API-Retire-Time - ISO8601 date advising when it will be deprecated

For example:

```
GET `/namespace/v1`

// 200 OK
Content-Type: application/json; charset=utf-8
X-API-Deprecated: true
X-API-Retire-Time: 2018-11-17T13:00:00Z
```

This provides consumers with a constant reminder that the API is marked to be deprecated and there is likely another version available for them to migrate to.

______________________________________________________________________________
<h1 id="6">6. API request</h1>
<h2 id="6-1">6.1 Request headers</h2>

All APIs **MUST** support the following request headers:

| Header | Value |
| --- | --- |
| Authorisation / Identification | One of:<br/>- API Key <br/>- Basic Auth (APIKey + Secret) <br/>- Username + Password <br/>- Bearer {token} |

The following request headers are optional:

| Header | Value |
| --- | --- |
| Content-Type | A choice of: <br/>- `application/json` (required)<br/>- `application/xml` (optional for xml)<br/> - `multipart/form-data` (optional for files) <br/>- `application/x-www-form-urlencoded` (optional for form data) |
| Accept | Content-Types that are acceptable for the response. Choice of: <br/> - `application/json` (required)<br/>- `application/xml` (optional for xml)
| Connection | Control options for the current connection (eg keep-alive) |
| Date | The date and time that the message was originated (eg Tue, 15 Nov 1994 08:12:31 GMT) |
| Cookie | An HTTP cookie previously sent by the server |
| Cache-Control | Used to specify directives that must be obeyed by all caching mechanisms (eg no-cache) |
| ETag | Used to identify the particular version of a resource being updated to prevent multiple user updates. This should match what is currently stored on the server.|

Payload data **MUST** NOT be used in HTTP headers. They are reserved for transversal information (authentication token, monitoring token, request properties etc).

<h2 id="6-2">6.2 HTTP request methods</h2>

RESTful APIs operations are based on the HTTP request method standard.
<h3 id="6-2-1">6.2.1 Supported HTTP request methods</h3>

|HTTP method|Description|
|---|---|
| `GET`| To _retrieve_ a resource. |
| `POST`| To _create_ a new resource, or to _execute_ an operation on a resource that changes the state of the system (eg send a message). |
| `PUT`| To _replace_ a resource with another supplied in the request. |
| `PATCH`| To perform a _partial update_ to a resource. |
| `DELETE`| To _delete_ a resource. |
| `HEAD`| For retrieving metadata about the request. For example, how many results _would_ a query return (without actually performing the query)? |
| `OPTIONS`| Used to determine if a CORS (cross-origin resource sharing) request can be made. This is primarily used in front-end web applications to determine if they can use APIs directly. |

A request to retrieve resources can be made for a single resource or a collection of resources.

Consider the following example:

```
https://gw.api.vic.gov.au/agency/v1/customers/{id}
```

To retrieve a collection of customers, a request is sent to the URN `/customers`.

To retrieve a single "customer", a request is sent to the URN `/customers/{id}`.

<h3 id="6-2-2">6.2.2 Collection of resources</h3>

The following operations are applicable for a collection of resources:

| HTTP method | Resource Path | Operation | Examples |
| --- | --- | --- | --- |
| GET | `/resources` | Get a collection of the resource | GET `/employees` or GET `/employees?status=open` |
| POST | `/resources` | Create a new instance of this resource.|

**Note:**

Creating or updating multiple resource instances in the same request is currently not standardised. There are factors such as receipt acknowledgement and how to handle partial success in a set of batches that must be considered on a case-by-case basis.

Future versions of the specification may address batch processing using APIs.

<h3 id="6-2-3">6.2.3 Single resource</h3>

The following operations are applicable for a single resource:

| HTTP method | Resource path | Operation |
| --- | --- | --- |
| GET | `/resources/{id}` | Get the instance corresponding to the resource ID. |
| PUT | `/resources/{id}` | To update a resource instance by replacing it – <br />"_Take this new thing and_ _ **put** _ _it there_". |
| DELETE | `/resources/{id}` | To delete the resource instance based on the resource (eg id). |
| PATCH | `/resources/{id}` | Perform changes such as add, update, and delete to the specified attribute(s). Is used often to perform partial updates on a resource. |

<h2 id="6-3">6.3 Request payload formats</h2>

At minimum the API **MUST** support a `JSON` formatted payload when supplied.

Other payload format such as `XML`, `CSV` and `YAML` may be supported as needed.

The additional format support must be documented in your API design (Swagger definition).

______________________________________________________________________________
<h1 id="7">7. Query parameters</h1>
<h2 id="7-1">7.1 Pagination</h2>

WoVG APIs **SHOULD** follow a "pagination first" policy.

Pagination is **RECOMMENDED** to:

1. serve requests in a timely manner (eg > 2s)
2. ensure the amount of data returned remains within a manageable payload (eg > 500kb)
3. ensure the data in the response is easily manageable to improve the user experience.

<h3 id="7-1-1">7.1.1 Parameters</h3>

When pagination is implemented, the following parameters **MUST** be used:

| Query parameter | Description | Example |
| --- | --- | --- |
| `page` | The page that the user wants to return. | `page=1` (default: 1)|
| `limit` | The number of results per page the user wants to return. | `limit=10` (default: 10)|

This creates a URI structure as follows:

Page 1: `/customers?page=1&limit=10`<br/>
Page 2: `/customers?page=2&limit=10`<br/>
...<br/>
Page 50: `/customers?page=50&limit=10`<br/>

This structure is useful as it is easy to understand and can be directly included in a UI.

**Common terms**

The following parameters are also common across REST APIs, but are **not** to be used in this specification.

- `offset` and `limit`. This is common in SQL databases and is a good option when you need stable permalinks to result sets. However, usability of the `offset` parameter can be difficult so `page` is preferred.
 
- `since` and `limit`. Get everything "since" some ID or timestamp. These are useful when it is a priority to let clients efficiently stay "in sync" with data. However, they generally require the result set order to be very stable.

<h3 id="7-1-2">7.1.2 Metadata</h3>
When pagination is included it is **RECOMMENDED** for APIs to advise the user in the response body what page they are on. If not included, the user is forced to inspect the request often requiring unnecessary code to parse query parameters.

An example of this is as follows:

```javascript
{
  "total_records" : 2340,
  "_meta": {
    "processing_time" : 120,
    "page": 4,
    "limit": 20
  },
  "_links" : {
    "_self": "/namespace/v1/employees?page=2&limit=1",
    "_prev": "/namespace/v1/employees?page=1&limit=1",
    "_next": "/namespace/v1/employees?page=3&limit=1"
  },
  "_embedded" : {
    "count" : 20,
    "employees" : [//...actual data here...]
  }
}
```

<h2 id="7-2">7.2 Filtering and sorting</h2>

Providing the ability to filter and sort collections in your API allows your consumers greater flexibility and controls on how they choose to consume your API. 

There are number of techniques on how to do this and further explanations are provided below however **DO NOT** define filter and sort parameters as part of the API URI (eg `/employees/age/from/20/to/30`). 

Filter parameters are not part of the resource definition. Instead use query parameters to specify the filter and sort requirements.

Below are the different techniques used when applying filtering and sorting:

<h3 id="7-2-1">7.2.1 Output selection</h3>

Consumers can specify the attributes they wish to return in the [response payload](#8-3) by specifying the attributes in the [query parameters](#7).

Example that returns only the `first_name` and `last_name` fields in the response.

```
?attributes=first_name,last_name
```

<h3 id="7-2-2">7.2.2 Simple filtering</h3>

Attributes can be used to filter a collection of resources.

Example:

```
?last_name=Citizen
```

will filter out the collection of resources with the attribute `last_name` that matches `Citizen`.

Example:

```
?last_name=Citizen&date_of_birth=1999-12-31
```

will filter out the collection of resources with the attribute `last_name` that matches `Citizen` and `date_of_birth` that matches 31st of December, 1999.

The equal (=) operator is the only supported operator when used in this technique. For other operators and conditions see the 'Advanced filtering' technique.

<h3 id="7-2-3">7.2.3 Advanced filtering</h3>

There are situations where simple filtering does not meet the user's needs and a more comprehensive approach is required. Use the reserved keyword filters to define a more complex filtering logic.

Multiple attributes with different operator and condition can be defined in the filter query parameter.

The following operators are supported:

1. \>= Greater than or equal to
2. => Equal to or greater than
3. \> Greater than
4. < Less than
5. <= Less than or equal to
6. =< Equal to or less than
7. = Equal
8. != Not equal

The AND, OR conditions are supported.

Example:

```
?filters=creation_date =\> 2001-09-20T13:00:00 and creation_date \<= 2001-09-21T13:00:00 and first_name like 'fred' and post_code=3000
```

Return a collection of resources where the `creation_date` is between `2001-09-20 1pm` and `2001-09-21 1pm` and `first-name` like "fred" and `post_code` is 3000.

<h3 id="7-2-4">7.2.4 Match case sensitivity</h3>

As a general guide it is better to return similar matches than to return no matches at all.

**The preference is to filter with case insensitivity**.

Whether you choose to filter with case insensitivity or not should be clearly documented.

<h3 id="7-2-5">7.2.5 Sorting</h3>

Providing data in specific order is often the requirement from client applications and hence it is important to provide the flexibility for clients to retrieve the data in the order they need it.

The two parameters that make up sorting are as follows:

| Query Parameter | Description |
| --- | --- | 
| `sort` | The direction to sort (eg `asc` or `desc`) |
| `sort_fields` | The fields to sort by (eg `id` or `name`) |

`sort_fields` is plural as the following options are both available:

Examples:

- `?sort=asc&sort_fields=name,last_modified`<br/>
- `?sort=desc&sort_fields=name&sort_fields=last_modified`

Both of these queries should sort first by name and then by last modified date.

______________________________________________________________________________
<h1 id="8">8. API responses</h1>
<h2 id="8-1">8.1 Response headers</h2>

The recommended content type is `JSON` (`application/json`).

The following response headers **MAY** be included in all responses:

| Header | Value |
| --- | --- |
| Access-Control-Allow-Origin | The URL that is allowed to access this service from javascript and browser based clients directly. <br/><br/>**Note:** Never use wildcard (*) URLs unless the REST resource is truly public. |
| Access-Control-Allow-Methods | The methods that are allowed to be accessed from javascript and browser based clients directly. |
| Access-Control-Allow-Headers | The headers that are allowed to be accessed from javascript and browser based clients directly. |
| Content-Type | Choice of: <br/> - `application/json` (required)<br/> - `application/xml` (optional for `xml`)<br/> - `multipart/form-data` (optional for files) <br/> - `text/html` (optional for `html`)
| Cache-Control | Informs the caching mechanisms. It is measured in seconds.max-age=3600 |
| Date | The date and time that the message was originated Date (eg Tue, 15 Nov 1994 08:12:31 GMT) |
| Expires | Gives the date/time after which the response is considered stale (eg Thu, 01 Dec 1994 16:00:00 GMT) |
| ETag | Used to identify the particular version of a resource. The client should include this in any update requests to make sure it is unchanged.|

<h2 id="8-2">8.2 HTTP response codes</h2>

The following table defines the responses that **MUST** be supported by your API.

| Request method | Status | Code | When to use |
| --- | --- | --- | --- |
| GET | OK | 200 | The request was successfully processed |
| GET | Bad Request | 400 | The server cannot process the request (such as malformed request syntax, size too large, invalid request message framing, or deceptive request routing, invalid values in the request) |
|GET| Unauthorised | 401 | The request could not be authenticated. |
|GET| Forbidden | 403 | The request was authenticated but is not authorised to access the resource. |
|GET| Not found | 404 | The resource was not found. |
|GET| Not Allowed | 405 | The method is not implemented for this resource. The response may include an Allow header containing a list of valid methods for the resource. |
|GET| Unsupported Media Type | 415 | This status code indicates that the server refuses to accept the request because the content type specified in the request is not supported by the server |
|GET| Internal Server error | 500 | An internal server error. The response body may contain error messages. |

<br />
| Request method | Status | Code | When to use |
| --- | --- | --- | --- |
| POST | Created | 201 | The resource was created. The Response Location HTTP header **SHOULD** be returned to indicate where the newly created resource is accessible. |
|POST| Accepted | 202 | Is used for asynchronous processing to indicate that the server has accepted the request but the result is not available yet. The Response Location HTTP header may be returned to indicate where the created resource will be accessible. |
|POST| Bad Request | 400 | The server cannot process the request (such as malformed request syntax, size too large, invalid request message framing, or deceptive request routing, invalid values in the request) For example, the API requires a numerical identifier and the client sent a text value instead, the server will return this status code. |
|POST| Unauthorised | 401 | The request could not be authenticated. |
|POST| Forbidden | 403 | The request was authenticated but is not authorised to access the resource. |
|POST| Not found | 404 | The resource was not found. |
|POST| Not Allowed | 405 | The method is not implemented for this resource. The response may include an Allow header containing a list of valid methods for the resource. |
|POST| Unsupported Media Type | 415 | This status code indicates that the server refuses to accept the request because the content type specified in the request is not supported by the server |
|POST| Unprocessable Entity | 422 | This status code indicates that the server received the request but it did not fulfil the requirements of the back end. An example is a mandatory field was not provided in the payload. |
|POST| Internal Server error | 500 | An internal server error. The response body may contain error messages. |

<br />
| Request method | Status | Code | When to use |
| --- | --- | --- | --- |
| PUT | Accepted | 202 | Is used for asynchronous processing to indicate that the server has accepted the request but the result is not available yet. |
|PUT| No content | 204 | The server successfully processed the request and is not returning any content |
|PUT| Bad Request | 400 | The server cannot process the request (such as malformed request syntax, size too large, invalid request message framing, or deceptive request routing, invalid values in the request)For example, the API requires a numerical identifier and the client sent a text value instead, the server will return this status code. |
|PUT| Unauthorised | 401 | The request could not be authenticated. |
|PUT| Forbidden | 403 | The request was authenticated but is not authorised to access the resource. |
|PUT| Not found | 404 | The resource was not found. |
|PUT| Not Allowed | 405 | The method is not implemented for this resource. The response may include an Allow header containing a list of valid methods for the resource. |
|PUT| Unsupported Media Type | 415 | This status code indicates that the server refuses to accept the request because the content type specified in the request is not supported by the server |
|PUT| Unprocessable Entity | 422 | This status code indicates that the server received the request but it did not fulfil the requirements of the back end. An example is a mandatory field was not provided in the payload. |
|PUT| Internal Server error | 500 | An internal server error. The response body may contain error messages. |

<br />
| Request method | Status | Code | When to use |
| --- | --- | --- | --- |
| DELETE | Accepted | 202 | Is used for asynchronous processing to indicate that the server has accepted the request but the result is not available yet. |
|DELETE| No content | 204 | The server successfully processed the request and is not returning any content |
|DELETE| Bad Request | 400 | The server cannot process the request (such as malformed request syntax, size too large, invalid request message framing, or deceptive request routing, invalid values in the request) |
|DELETE| Unauthorised | 401 | The request could not be authenticated. |
|DELETE| Forbidden | 403 | The request was authenticated but is not authorised to access the resource. |
|DELETE| Not found | 404 | The resource was not found. |
|DELETE| Not Allowed | 405 | Method not allowed on resource. The response may include an Allow header containing a list of valid methods for the resource. |
|DELETE| Unsupported Media Type | 415 | This status code indicates that the server refuses to accept the request because the content type specified in the request is not supported by the server |
|DELETE| Internal Server error | 500 | An internal server error. The response body may contain error messages. |

<br />
| Request method | Status | Code | When to use |
| --- | --- | --- | --- |
| PATCH | Accepted | 202 | Is used for asynchronous processing to indicate that the server has accepted the request, but the result is not available yet. |
|PATCH| No content | 204 | The server successfully processed the request and is not returning any content |
|PATCH| Bad Request | 400 | The server cannot process the request (such as malformed request syntax, size too large, invalid request message framing, or deceptive request routing, invalid values in the request) For example, the API requires a numerical identifier and the client sent a text value instead, the server will return this status code. |
|PATCH| Unauthorised | 401 | The request could not be authenticated. |
|PATCH| Forbidden | 403 | The request was authenticated but is not authorised to access the resource. |
|PATCH| Not found | 404 | The resource was not found. |
|PATCH| Not Allowed | 405 | The method is not implemented for this resource. The response may include an Allow header containing a list of valid methods for the resource. |
|PATCH| Unsupported Media Type | 415 | It indicates that the server refuses to accept the request because the content type specified in the request is not supported by the server |
|PATCH| Unprocessable Entity | 422 | This status code indicates that the server received the request but it did not fulfil the requirements of the back end. An example is a mandatory field was not provided in the payload. |
|PATCH| Internal Server error | 500 | An internal server error. The response body may contain error messages. |

<br />
This table highlights the status codes that are applicable for all HTTP methods

| Request method | Status | Code | When to use |
| --- | --- | --- | --- |
| All | Request Timeout | 408 | The request timed out before a response was received. |
| All | Method Not Implemented | 501 | It indicates that the request method is not supported by the server and cannot be handled for **any** resource. For example, the server supports GET, POST, PUT, DELETE, and PATCH but not OPTIONS methods. |

<h2 id="8-3">8.3 Response payload</h2>

The response payload for an API can be for a single resource or a collection of resources.

When the response format is `JSON`, the following response standards apply:

<h3 id="8-3-1">8.3.1 Single resource</h3>

The following status codes represent appropriate responses to the different operations that can be performed on a single resource within the system.

| Request method | Resource path | Status | Code |
| --- | --- | --- | --- |
| POST | `/resources/{id}` | Created | 201 | 
||| Accepted | 202 |
||| Bad request | 400 |
||| Unauthorised | 401 | 
||| Forbidden | 403 | 
||| Not found | 404 | 
||| Not allowed | 405 | 
||| Unsupported media type | 415 | 
||| Unprocessable entity | 422 |
||| Internal server error | 500 | 
| PUT | `/resources/{id}` | OK | 200 |
||| Accepted | 202 |
||| No content | 204 | 
||| Bad request | 400 | 
||| Unauthorised | 401 | 
||| Forbidden | 403 | 
||| Not found | 404 | 
||| Not allowed | 405 | 
||| Unsupported media type | 415 | 
||| Unprocessable entity | 422 |
||| Internal server error | 500 | 
| DELETE | `/resources/{id}` | Accepted | 202 | 
||| No content | 204 |
||| Bad request | 400 | 
||| Unauthorised | 401 | 
||| Forbidden | 403 | 
||| Not found | 404 | 
||| Not allowed | 405 | 
||| Internal server error | 500 | 
| PATCH | `/resources/{id}` | Accepted | 202 | 
||| No content | 204 | 
||| Bad request | 400 | 
||| Unauthorised | 401 | 
||| Forbidden | 403 | 
||| Not found | 404 | 
||| Not allowed | 405 | 
||| Unsupported media type | 415 | 
||| Unprocessable entity | 422 |
||| Internal server error | 500 |

<h3 id="8-3-2">8.3.2 Collection of resources</h3>

The following status codes represent appropriate responses to the different operations that can be performed on a collection resource within the system.

| Request method | Resource path | Status | Code |
| --- | --- | --- | --- | --- |
| GET | `/resources/` | OK | 200 |
||| Bad request | 400 | 
||| Unauthorised | 401 | 
||| Forbidden | 403 | 
||| Not found | 404 | 
||| Not allowed | 405 | 
||| Unsupported media type | 415 | 
||| Internal server error | 500 |

______________________________________________________________________________
<h1 id="9">9. Error handling</h1>
<h2 id="9-1">9.1 Error response payload</h2>

For some errors, returning the HTTP status code is enough to convey the response. Additional error information can be supplemented in the response body. For example, HTTP 400 Bad request is considered to be too generic for a validation error and more information must be provided in the response body.

The attributes of the error object are defined here:

| Error attributes | Description | Mandatory? |
| --- | --- | --- |
| `id` | Identifier of the specific error | Optional |
| `detail` | A human-readable explanation specific to this occurrence of the problem. | Mandatory |
| `code` | An application-specific error code. | Mandatory |
| `source` | An object containing references to the source of the error, optionally including any of the following members:pointer: a JSON Pointer [RFC6901] to the associated entity in the request document [eg "/data" for a primary data object, or "/data/attributes/title" for a specific attribute].parameter: a string indicating which URI query parameter caused the error. | Optional |
| `source > pointer` | JSON Pointer [RFC6901] to the associated entity in the request document [eg "/data" for a primary data object, or "/data/attributes/title" for a specific attribute]. | Optional |
| `source > parameter` | A string indicating which URI query parameter caused the error. | Optional |

The returned error objects must be in a collection (array) – see the examples for details.

<h2 id="9-2">9.2 Input validation</h3>

There are two types of input validation errors

|Request validation issue | HTTP status code|
|------------- | -------------|
|Not well-formed JSON | `400 Bad Request`|
|Contains validation errors that the client can change (eg missing a mandatory field) | `422 Unprocessable Entity`|

<h2 id="9-3">9.3 Error Samples</h2>

A sample 400 Bad Request error response:

```javascript
{
  "errors": [{
    "id": "86032cbe-a804-4c3b-86ce-ec3041e3effc",
    "detail": "Invalid value(s) in request input",
    "code" : "19283",
    "source": {
      "parameter": "postcode"
    },{
    "id": "45786a8f-452e-492f-a779-801b5d0bd0a7",
    "detail": "Input value(s) exceeded maximum length",
    "code" : "19284",
    "source": {
      "parameter": "last_name"
    }
  }]
}
```
A sample 500 Internal Server error:

```javascript
{
  "errors": [{
    "id": "86032cbe-a804-4c3b-86ce-ec3041e3effc",
    "detail": "Downstream system is not responding correctly"
    "code" : "500",
  }]
}
```

______________________________________________________________________________
<h1 id="10">10. API security</h1>
<h2 id="10-1">10.1 API design</h2>

Applying the right level of security will allow your APIs to perform well without compromising on the security risk.

To secure your APIs the security standards are grouped into three categories: Design, Transport, and Authentication and authorisation.

At minimum the security standards that are defined here **MUST** be applied. Further security considerations may apply depending on the API design and requirements – refer to our [API Design Considerations section](#1-4) for more details.

<h2 id="10-2">10.2 Transport security</h2>

- ALL transport **MUST** occur over HTTPS using TLS 1.2.
- ALL certificates must be SHA256 with minimum key length of 2048.
- ALL publicly accessible endpoints **MUST** use a digital certificate that has been signed by an approved certificate authority.
- Internal facing endpoints **MAY** use self-signed digital certificates.
- Do not redirect HTTP traffic to HTTPS - reject these requests.
- Unused HTTP methods **SHOULD** be disabled and return HTTP 405.
- ALL requests must be validated.

Depending on the security classification you may be required to establish the following controls above and beyond the standard controls:

- Mutual authentication between the consumer and the API gateway
- Mutual authentication between the API gateway and the back-end API
- IP whitelisting of API consumers using either API gateway policy or firewall configurations
- IP whitelisting of API publishers using either API gateway policy or firewall configurations
- Payload encryption while in transit
- Payload signing for integrity and verification

<h2 id="10-3">10.3 Authentication and authorisation</h2>

- Basic or digest authentication **MUST NOT** be used.
- The `Authorization: Bearer` header **MUST** be used for authentication/authorisation (eg using a JWT).
- Always set a reasonable expiration date for tokens. JWT lifetime suggested default is 15 minutes.
- All APIs **MUST** have a policy that only allows access based on a valid API key.
- API keys **MUST** be used for client authentication. Use of API keys should only be permitted when TLS is enabled. Rotation policy for API key should be implemented as well.
- API keys **MUST NOT** be included in the URL or query string. API keys **MUST** be included in the HTTP header (as query strings are not encrypted by TLS - headers are.)
- CORS headers should only be used when necessary as it reduce overall security mechanisms built into web browsers by selectively relaxing cross-origin restrictions.
- A request from Domain A is considered cross-origin when it tries to make a request to an API that is hosted in Domain B.
- For security reasons, browsers restrict cross-origin HTTP requests.
- The Cross-origin resource sharing standard works by adding new HTTP headers (i.e. Access-Control-Allow-Origin) that allow servers to describe the set of origins that are permitted to access the API
- Never use wildcard (\*) URLs in the response headers (i.e. Access-Control-Allow-Origin) unless the REST resource is truly public and requires little or no authorisation for use.

<h3>OAuth 2.0</h3>

OAuth 2.0 can be used for authorisation. OAuth is an authorisation protocol that securely delegates authorisation to another resource. It allows users to approve applications to act on their behalf without sharing their password.

OpenID Connect extends the OAuth 2.0 protocol to receive information about the authenticated users such as their username and is useful when dealing with federated identity providers.

The API Team provides an OAuth service that can be used by WoVG APIs. Alternatively, API Providers can link into Open ID Providers to delegate authorisation. This process can be facilitated by the WoVG API Gateway.

<h2 id="10-4">10.4 Abstraction</h2>

There are multiple levels of abstraction and determining the level of abstraction is largely based on the number of consumers and the cost to change the system in response to an API change.

As a general principle there should be a level of abstraction of the source system data and business logic in your API design to decouple the consumers and the API service provider(s). Applying BASIC abstraction to a SaaS API (such as an Azure API) is recommended. For example; if there are changes in the SaaS authentication schema it could be handled within the API. 

A higher level of abstraction would be required for APIs that have multiple consumers and the cost of change to the API consumers is greater than the cost to change the backend systems / service providers.

The varying levels of abstraction are as follows:

| Abstraction level | Description |
| --- | --- |
| `BASIC` | **Basic abstraction level** <br />Represents the minimum abstraction required for all APIs (including point-to-point): <br /><br /> - Use `JSON` as your default representation. <br /> - Always provide a version number in the URL to facilitate change. <br /> - Always use an API Key ID <br /> - Little or no abstraction of the data model and expose data as required
| `INTERMEDIATE` | APIs which aim for re-use should consider Intermediate levels of abstraction: <br /><br /> **Payload abstraction** <br /> - Represent resources from the consumer view point and be independent of the underlying system. NEVER directly expose the internal database table structure as is in your API. <br /> - Error abstraction <br /> – Handle source system errors and represent the errors in a consistent and informative. <br /><br />**System IDs abstraction** <br /> – Avoid exposing and sharing internal system identifiers (such as a database ID) with your consumers. Use a candidate key or a secondary identifier.
| `ADVANCED` | The highest level of abstraction and it encompasses all the other levels.<br /><br /> - Use the API gateway pattern to take care of cross-cutting concerns such as security, traffic management and analytics/monitoring. <br /> - Use linked data hypermedia to promote "discoverability" of your API resources and relationships. <br /> - Consider using HATEOAS to abstract allowable actions.

<h2 id="10-5">10.5 Rate limiting</h2>

Apply rate limiting and throttling policies to prevent abuse of your API. Ensure appropriate alerts are implemented and respond with informative errors when thresholds are nearing or have been exceeded.

The following headers will be returned when rate limits are in place:

| Header | Description |
| --- | --- | 
| `X-Rate-Limit-Limit` | Rate limit ceiling for the given request (for example, 100 messages). |
| `X-Rate-Limit-Remaining` | Number of requests left for the time window (for example, 45 messages). | 
| `X-Rate-Limit-Reset` | Remaining time window before the rate limit resets in UTC epoch seconds (for example, 1353517297). |

<h2 id="10-6">10.6 Error handling</h2>

When your application displays error messages, it should not expose information that could be used to attack your system. You should establish the following controls when providing error messages:

- Your API **MUST** mask any system related errors behind standard HTTP status responses and error messages (eg do not expose system level information in your error response).
- Your API **MUST NOT** pass technical details (eg call stacks or other internal hints) to the client.

<h2 id="10-7">10.7 Audit logs</h2>

An important aspect of security is to be notified when something wrong occurs, and to be able to investigate it. It is **RECOMMENDED** to define the right level of logging and audit and to set the right alerts.
- Write audit logs before and after security related events which can trigger the alerts
- Sanitising the log data to prevent log injection attacks

<h2 id="10-8">10.8 Input validation</h2>

Input validation is performed to ensure only properly formed data is received by your system, this helps to prevent malicious attacks.

- Input validation should happen as early as possible, preferably as soon as the data is received from the external party.
- Define an appropriate request size limit and reject requests exceeding the limit.
- Validate input: (eg length / range / format and type).
- Consider logging input validation failures. Assume that someone who is performing hundreds of failed input validations per second has a malicious intent.
- Constrain string inputs with regular expression where appropriate.

<h2 id="10-9">10.9 Content type validation</h2>

Honour the specified content-type. Reject requests containing unexpected or missing content type headers with HTTP response status `415 Unsupported Media Type`.

<h2 id="10-10">10.10 Gateway security features</h2>

It is preferable to use the security policy features available in the WoVG API gateway platform than to implement the policies in your back-end API.

| Security | API gateway component | Comment | Implementation required |
| --- | --- | --- | --- |
| HTTP verbs | Listeners-\>Path | HTTP verbs can be selected when defining the path for the API | Recommended |
| Input Validation | Filter -\> Content Filtering | Various filters can be used for validating the input i.e. message size, schema validation, validate headers, validate query strings etc. | Recommended |
| SSL | Listeners | SSL protocol (i.e. TLS 1.2 etc.) can be selected at listener level | Recommended |
| Digital Certificate | Filter -\> Integrity | Various filters can be used for creating and validating the signature i.e. XML signature, JWT sign | Optional depends on business requirements |
| JWT | Filter -\> Integrity | Message can be signed using JWT | Optional depends on business requirements |
| API Keys | Filter -\> Authentication | Various filters can be used for authenticating the consumers i.e. API Keys etc. | Recommended |
| OAUTH | Filter -\> OAUTH | OAUTH can be used for authorizing the consumers | Optional as it depends on business requirements |
| CORS | Listeners-\>Path | CORS can be restricted at path level | Recommended |

The WOVG API Team can provide advice on which API Gateway security policies should be applied.

______________________________________________________________________________
<h1 id="11">11. Hypermedia</h1>
<h2 id="11-1">11.1 Hypermedia - linked data</h2>

Hypermedia links in APIs are links in the response payload that inform the consumers to what contents can be retrieved. Though simple in concept hypermedia links in APIs allow consumers to locate resource without the need to have an upfront understanding of the resource and its relationship.

This is similar to the navigation of a web page. The user is not expected to know the structure of the web page prior to visting. They can simply browse to the home page and the navigation lets them browse the site as required.

APIs that do not provide links are difficult to use and expect the consumer to refer to the documentation.

#### Example:

```javascript

GET /namespace/v1/employees

//200 OK

{
  "total_records" : "1",
  "_links": [{
      "href" : "/namespace/v1/employees",
      "rel" : "self"
    },
  }],
  "_embedded": {
    "employees": [{
      "name" : "John Smith",
      "_links": [{
        "self": {
          "href" : "/namespace/v1/employees/john-smith"
        }
      }]
    }]
  }
}
```

<h2 id="11-2">11.2 HATEOAS</h2>

`Hypermedia as the engine of application state` is the concept of representing allowable actions as hyperlinks associated with resource. Similar to the hypermedia linked data concept, the links defined in the response data represents state transitions that are available from that current state to adjacent states.

```javascript
{
  "account_number":"12345",
  "balance": 100.00,
  "_links":[
    {"rel": " **deposit**", "href":"/account/12345/deposit"},
    {"rel": " **withdraw**", "href":"/account/12345/withdraw"},
    {"rel": " **transfer**", "href":"/account/12345/transfer"}
  ]
}

```

But if the same account is overdrawn by 25, then the only allowed action is deposit:

```javascript
{
  "account_number":"12345",
  "balance": -25.00,
  "_links":[{
    "rel": "deposit",
    "href":"/account/12345/deposit"
  }]
}

```

Deciding to implement HATEOAS designs in your API is dependent on the readiness of the clients to consume HATEOAS and the design and implementation effort.

<h2 id="11-3">11.3 Hypermedia-compliant API</h2>

A hypermedia-compliant API provides consumers with an accessible a state machine of the transitions that are available for them to use. 

In APIs, request methods such as `DELETE`, `PATCH`, `POST` and `PUT` initiate a transition in the state of a resource. A `GET` request **MUST** never change the state of the resource that is retrieved.

In order to provide a better experience for API consumers, API designers **SHOULD** provide a list of state transitions that are available for each resource in the `_links` array. 

An example of an API that exposes a set of operations to manage a user account lifecycle and implements the HATEOAS interface constraint is as follows:

A client starts their interaction with a service through the URI `/users`. This fixed URI supports both `GET` and `POST` operations. The client decides to do a `POST` operation to create a user in the system.

#### Request:

```
POST https://gw.api.vic.gov.au/dept-xyz/v1/users

{
    "first_name": "John",
    "last_name" : "smith",
    ...
}
```

#### Response:

The API creates a new user from the input and returns the following links to the client in the response.

- A link to the created resource in the `Location` header (to comply with the 201 response spec).
- A link to retrieve the complete representation of the user (aka `self` link) (`GET`).
- A link to update the user (`PUT`).
- A link to partially update the user (`PATCH`).
- A link to delete the user (`DELETE`).


```
HTTP/1.1 201 CREATED
Content-Type: application/json
Location: https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI
...

{
  "links": [
      {
          "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
          "rel": "self",
          "method" : "GET"
      },
      {
          "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
          "rel": "delete",
          "method": "DELETE"
      },
      {
          "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
          "rel": "replace",
          "method": "PUT"
      },
      {
          "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
          "rel": "edit",
          "method": "PATCH"
      }
  ]
}

```

A client can store these links in its database for later use.

A client may then want to display a set of users and their details before the admin decides to delete one of the users. So the client does a `GET` to the same fixed URI `/users`.

#### Request:

```
GET https://gw.api.vic.gov.au/dept-xyz/v1/users
```

The API returns all the users in the system with respective `self` links.

#### Response:

```
HTTP/1.1 200 OK
Content-Type: application/json
...

{
    "total_records": "2",
    "embedded" : {
      "users": [
      {
          "first_name": "John",
          "last_name": "Greenwood",
          ...
          "links": [
              {
                  "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
                  "rel": "self"
              }
          ]
      },
      {
          "first_name": "David",
          "last_name": "Brown",
          ...
          "links": [
              {
                  "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-MDFSKFGIFJ86DSF",
                  "rel": "self"
              }
          ]
      }]
    }
}

```

The client MAY follow the `self` link of each user and figure out all the possible operations that it can perform on the user resource.

#### Request:

```
GET https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI
```

#### Response:

```
HTTP/1.1 200 OK
Content-Type: application/json
...
{
    "first_name": "John",
    "last_name": "Smith",
    ...
    "links": [
    {
        "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
        "rel": "self",

    },
    {
        "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
        "rel": "delete",
        "method": "DELETE"
    },
    {
        "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
        "rel": "replace",
        "method": "PUT"
    },
    {
        "href": "https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI",
        "rel": "edit",
        "method": "PATCH"
    }
}
```
To delete the user, the client retrieves the URI of the link relation type `delete` from its data store and performs a delete operation on the URI.

#### Request:

```
DELETE https://gw.api.vic.gov.au/dept-xyz/v1/users/ALT-JFWXHGUV7VI

```

In summary:
- There is a well defined index or navigation entry point for evert API which a client navigates to in order to access all other resources.
- The client does not need to build the logic of composing URIs to execute different requests or code any kind of business rule by looking into the response details that may be associated with the URIs and state changes.
- The client acknowledges the fact that the process of creating URIs belongs to the server.
- Client treats URIs as opaque identifiers.
- APIs using hypermedia in representations could be extended seamlessly. As new methods are introduced responses could be extended with relevant HATEOAS links. This way clients could take advantage of the functionality in incremental fashion. For example; if the API starts supporting a new `PATCH` operation then clients could use it to do partial updates.

The mere presence of links does not decouple a client from having to learn the data required to make requests for a transition and all associated link semantics particularly for `POST`/`PUT`/`PATCH` operations. An API **MUST** provide documentation to clearly describe all the links, link relation types and request response formats for each of the URIs.

<h2 id="11-4">11.4 Link description object</h2>

Links **MUST** be described using the [Link Description Object (LDO)](http://json-schema.org/latest/json-schema-hypermedia.html#anchor17) schema. An LDO describes a single link relation in the links array. Following is brief description for properties of Link Description Object.

#### href:

* A value for the `href` property **MUST** be provided.

* The value of the `href` property **MUST** be a [URI template](https://tools.ietf.org/html/rfc6570) used to determine the target URI of the related resource. It **SHOULD** be resolved as a URI template per [RFC 6570](https://tools.ietf.org/html/rfc6570).

* Use **ONLY** absolute URIs as a value for `href` property. Clients usually bookmark the absolute URI of a link relation type from the representation to make API requests later. Developers **MUST** use the URI Component Naming Conventions to construct absolute URIs. The value from the incoming `Host` header (eg gw.api.vic.gov.au) MUST be used as the `host` field of the absolute URI.

#### rel:
* `rel` stands for relation as defined in link relation type.

* The value of the `rel` property indicates the name of the relation to the target resource. 

* A value for the `rel` property MUST be provided. 

#### method:
* The `method` property identifies the HTTP verb that **MUST** be used to make a request to the target of the link. The `method` property assumes a default value of `GET` if it is omitted.

#### title:
* The `title` property provides a title for the link and is a helpful documentation tool to facilitate understanding by the end clients. This property is **NOT REQUIRED**.

<h2 id="11-5">11.5 Link relation type</h2>

A `Link Relation Type` serves as an identifier for a link. An API **MUST** assign a meaningful link relation type that unambiguously describes the semantics of the link. Clients use the relevant link relation type in order to identify the link to use from a representation.

When the semantics of a link relation type defined in [IANA's list of standardised link relations](http://www.iana.org/assignments/link-relations/link-relations.xhtml) matches with the one you want to define then it **MUST** be used. 

The table below describes some of the commonly used link relation types. It also lists some additional link relation types defined by these guidelines.

|Link relation type | Description|
|---------|------------|
|`self` | Conveys an identifier for the link's context. Usually a link pointing to the resource itself.|
|`create` | Refers to a link that can be used to create a new resource.|
|`edit` | Refers to editing (or partially updating) the representation identified by the link. Use this to represent a `PATCH` operation link.|
|`delete` | Refers to deleting a resource identified by the link. Use this `Extended link relation type` to represent a `DELETE` operation link.|
|`replace` | Refers to completely update (or replace) the representation identified by the link. Use this `Extended link relation type` to represent a `PUT` operation link.|
|`first` | Refers to the first page of the result list.|
|`last` | Refers to the last page of the result list provided `total_required` is specified as a query parameter.|
|`next` | Refers to the next page of the result list.|
|`prev` | Refers to the previous page of the result list.|
|`collection` | Refers to a collections resource (e.g /v1/users).|
|`latest-version` | Points to a resource containing the latest (eg current) version.|
|`search` | Refers to a resource that can be used to search through the link's context and related resources.|
|`up` | Refers to a parent resource in a hierarchy of resources.|

For all `controller` style complex operations, the controller `action` name must be used as the link relation type (eg `activate`,`cancel`,`send`).

______________________________________________________________________________
<h1 id="12">12. Networking</h1>
<h2 id="12-1">12.1 Caching</h2>

Implementing caching is not a one size fit all approach. Caching can occur in many parts of the network and can happen with unwanted and unintended results.

Not all APIs require caching such as serving live data fields (a stock market price) API may desire no caching. It is important to understand how HTTP caching can impact your API.

There are two HTTP cache headers: `Cache-Control` and `Expires`.

<h3 id="12-1-1">12.1.1 Cache-Control</h3>

`Cache-Control` notifies if the client agent should cache. It supports three main values:
- `public`
- `private`
- `no-cache`

If set to `public`; caching can occur anywhere within the network traffic such as intermediate proxies.

If set to `private`; only the client agent is allowed to cache.

If set to `no-cache`; no caching should be done - though this is not always the case due to the complexity of the network.

Accompanying `Cache-Control`; is the `max-age`. The `max-age` is defined in seconds and how long the response can be cached before it is considered stale.

#### Example: 

– Any part of the network can cache the content for one hour:

```
Cache-Control: public, max-age=3600
```

<h3 id="12-1-2">12.1.2 Expires</h3>

The `Expires` directive when used alongside `Cache-Control` sets a date when the content is considered stale.

If both `Expires` and `max-age` is specified `max-age` will take precedence.

#### Example: 

- `Cache-Control` with `Expires`

```
Cache-Control: public

Expires: Mon, 25 Jun 2019 21:31:12 GMT

```

<h3 id="12-1-3">12.1.3 Caching in the API gateway</h3>

To reduce load the API gateway offers a manage cache service.

The API gateway provides its own local copy of the cache but registers a cache event listener that replicates messages to the other caches across the WoVG API gateway network so that put, remove, expiry and delete events on a single cache are duplicated across all other caches.

Further information about caching in your API can be discussed with the WoVG API team at [apiteam@dpc.vic.gov.au](apiteam@dpc.vic.gov.au).

______________________________________________________________________________
<h1 id="13">13. Webhooks</h1>
<h2 id="13-1">13.1 Current guidance</h2>

Webhooks allow API consumers to be notified of when a specific event occurs within an API interface. To implement this the API consumer must establish a URL endpoint that can receive and process a HTTP POST request. The endpoint must also be registered with the API publisher along with the events that the API consumer is interested in subscribing to.

In a basic implementation an API webhook payload is usually sent as a JSON document and will only provide enough information about the event that occurred. For example, the message can contain just the reference ID of the resource that has been updated. As a result, the consumer will have to make a subsequent call to the API interface to retrieve the updated resource.

In a more sophisticated scenario, an API webhook payload can provide the details of the updates that have occurred without the API consumer having to make a subsequent call to retrieve the updated resource. This reduces the network traffic but is likely to add additional complexity to the API interface design.

The following design guidelines should be considered when implementing webhooks for your API:

- If you are sending sensitive data in your webhook then consider encrypting/signing the webhook POST request for message integrity and verification.
- Within your webhook POST request it is useful to include a unique event ID for troubleshooting and auditing purposes.
- Your API should implement a retry mechanism in case the destination URL is not available.
- The API platform does not have existing capabilities to register webhook endpoints, so onboarding/offboarding will need to be considered separately.
- Webhooks require additional infrastructure from your API consumers so consider their needs and capabilities when designing your solution

______________________________________________________________________________
<h1 id="14">14. Testing</h1>
<h2 id="14-1">14.1 Testing tools</h2>

There are a wide variety of free (open source) testing tools available for API testing:

- **SoapUI** - the open source functional testing tool for API testing. It supports multiple protocols including SOAP, REST, HTTP and JMS. You can download the SoapUI from [https://www.soapui.org/downloads/soapui.html](https://www.soapui.org/downloads/soapui.html).
- **Postman** - an application for interacting with HTTP APIs. It presents you with a friendly GUI for constructing requests and reading responses. You can download Postman from [https://www.getpostman.com/](https://www.getpostman.com/).
- **cURL** - a tool for working with URLs. cURL lets us query a URL from the command line. It lets us post form data. With cURL we can try out new APIs easily. You can download the curl from the command line on Linux by typing "sudo yum install curl".
- **ApacheBench (ab)** - can load-test servers by sending an arbitrary number of concurrent requests. You can download ApacheBench from the command line on Linux by typing "yum install httpd-tools".
- **Swagger** – can be used to validate your Swagger definition prior to importing it into API manager.

______________________________________________________________________________
<h1 id="refs">References</h1>

> [Fielding's dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_2)

> [https://swagger.io/swagger-editor/](https://swagger.io/swagger-editor/)

> [RFC 3986](https://tools.ietf.org/html/rfc3986)

> [Semantic Versioning](https://semver.org/)

> [HTTP Status Codes - Wikipedia](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

> [https://tools.ietf.org/html/rfc2119](https://tools.ietf.org/html/rfc2119)

> [IANA's list of standardized link relations](http://www.iana.org/assignments/link-relations/link-relations.xhtml)

> [https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)

> [https://tools.ietf.org/html/draft-kelly-json-hal-08](https://tools.ietf.org/html/draft-kelly-json-hal-08)

> [json:api - A Specification for building APIs in JSON](https://jsonapi.org/)

> [https://www.soapui.org/downloads/soapui.html](https://www.soapui.org/downloads/soapui.html)

> [https://www.getpostman.com/](https://www.getpostman.com/)


<h1 id="standards"2>API standards referenced</h1>
> [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md)

> [White House Web API Standards](https://github.com/WhiteHouse/api-standards)

> [18F API Standards](https://github.com/18F/api-standards)

> [Gov.UK API Service Manual](https://www.gov.uk/service-manual/technology/application-programming-interfaces-apis)

> [Government of Canada Web API Standard](https://github.com/wet-boew/wet-boew-api-standards#style-guide)

> [US Department of Labor API Standards](https://github.com/USDepartmentofLabor/api-standards)

> [PayPal API Design Guidelines](https://github.com/paypal/api-standards/blob/master/api-style-guide.md)

> [Refinery29 API Standards](https://github.com/refinery29/api-standards#url-structure-and-versioning)

> [LeaseWeb API Design Standards](https://github.com/LeaseWeb/api-standards)
