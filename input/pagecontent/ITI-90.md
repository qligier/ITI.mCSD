
### 2:3.90.1 Scope

The Find Matching Care Services transaction returns a list of matching
care services resources based on the query sent. A Care Services
Selective Consumer initiates a Find Matching Care Services transaction
against a Care Services Selective Supplier.

### 2:3.90.2 Actor Roles

| **Actor** | **Role** |
| ----- | ---- |
| Care Services Selective Consumer  | Requests a list of resources from the Care Services Selective Supplier based on query parameters |
| Care Services Selective Supplier  | Accepts the query request and returns a list of matching resources.                              |
{: .grid}

### 2:3.90.3 Referenced Standards

  - HL7 FHIR standard Release 4 [http://hl7.org/fhir/R4/index.html](http://hl7.org/fhir/R4/index.html)

### 2:3.90.4 Messages

<div>
{%include ITI-90-seq.svg%}
</div>
<br clear="all">

**Figure 2:3.90.4-1: Interaction Diagram**

#### 2:3.90.4.1 Find Matching Care Services Request Message

The Find Matching Care Services message is a FHIR search operation on
the Organization, Location, Practitioner, PractitionerRole, and/or
HealthcareService Resources.

##### 2:3.90.4.1.1 Trigger Events

A Care Services Selective Consumer triggers a Find Matching Care
Services Request to a Care Services Selective Supplier according to the
business rules for the query. These business rules are outside the scope
of this transaction.

##### 2:3.90.4.1.2 Message Semantics

A Care Services Selective Consumer initiates a search request using HTTP
GET as defined at [http://hl7.org/fhir/R4/http.html#search](http://hl7.org/fhir/R4/http.html#search) on the
Organization, Location, Practitioner, PractitionerRole, or
HealthcareService Resources. The query parameters are identified below.
A Care Services Selective Consumer may query any combination or subset
of the parameters.

A Care Services Selective Supplier shall support combinations of search
parameters as defined at [http://hl7.org/fhir/R4/search.html#combining](http://hl7.org/fhir/R4/search.html#combining),
“Composite Search Parameters.”

A Care Services Selective Supplier shall support responding to a request
for both the JSON and the XML messaging formats as defined in FHIR. A
Care Services Selective Consumer shall accept either the JSON or the XML
messaging formats as defined in FHIR. See [ITI TF-2x: Z.6](https://profiles.ihe.net/ITI/TF/Volume2/ch-Z.html#z.6-populating-the-expected-response-format) for
more details.

A Care Services Selective Supplier shall implement the parameters
described below. A Care Services Selective Supplier may choose to
support additional query parameters beyond the subset listed below. Any
additional query parameters supported shall be supported according to
the core FHIR specification.

See [ITI TF-2x: Appendix W](https://profiles.ihe.net/ITI/TF/Volume2/ch-W.html) for informative implementation material for
this transaction.

###### 2:3.90.4.1.2.1 Common Parameters

The Care Services Selective Supplier shall support the `:contains` and
`:exact` modifiers in all of the string query parameters below.

The Care Services Selective Supplier shall support the following search
parameters as defined at [http://hl7.org/fhir/R4/search.html#all](http://hl7.org/fhir/R4/search.html#all).

```
_id
_lastUpdated
_profile
```

The Care Services Selective Supplier shall also support the following
prefixes for the `_lastUpdated` parameter: `gt`, `lt`, `ge`, `le`, `sa`, and `eb`.

###### 2:3.90.4.1.2.2 Organization Resource Message Semantics

The Care Services Selective Supplier shall support the following search
parameters on the Organization Resource as defined at
[http://hl7.org/fhir/R4/organization.html#search](http://hl7.org/fhir/R4/organization.html#search). String parameter
modifiers are defined at [http://hl7.org/fhir/R4/search.html#string](http://hl7.org/fhir/R4/search.html#string).
The `ihe-mcsd-hierarchy-\*` search parameters query the hierarchy
extension identified by the following canonical URI
`http://ihe.net/fhir/StructureDefinition/IHE\_mCSD\_hierarchy\_extension`.

```
active
identifier
name
partof
partof:above
partof:below
type
partof.identifier
partof.name
_revInclude=Location:organization
ihe-mcsd-hierarchy-type
ihe-mcsd-hierarchy-partof
ihe-mcsd-hierarchy-partof:above
ihe-mcsd-hierarchy-partof:below
```

###### 2:3.90.4.1.2.3 Location Resource Message Semantics

The Care Services Selective Supplier shall support the following search
parameters on the Location Resource as defined at
[http://hl7.org/fhir/R4/location.html#search](http://hl7.org/fhir/R4/location.html#search). String parameter
modifiers are defined at [http://hl7.org/fhir/R4/search.html#string](http://hl7.org/fhir/R4/search.html#string).

```
identifier
name
organization
partof
partof:above
partof:below
status
type
partof.identifier
partof.name
organization.active
organization.identifier
organization.name
_include=Location:organization
```

###### 2:3.90.4.1.2.4 Practitioner Resource Message Semantics

The Care Services Selective Supplier shall support the following search
parameters on the Practitioner Resource as defined at
[http://hl7.org/fhir/R4/practitioner.html#search](http://hl7.org/fhir/R4/practitioner.html#search). String parameter
modifiers are defined at [http://hl7.org/fhir/R4/search.html#string](http://hl7.org/fhir/R4/search.html#string).

```
active
identifier
name
given
family
```

###### 2:3.90.4.1.2.5 PractitionerRole Resource Message Semantics

The Care Services Selective Supplier shall support the following search
parameters on the PractitionerRole Resource as defined at
[http://hl7.org/fhir/R4/practitionerrole.html#search](http://hl7.org/fhir/R4/practitionerrole.html#search).

```
active
location
organization
practitioner
role
service
specialty
practitioner.identifier
practitioner.name
practitioner.given
practitioner.family
_include=PractitionerRole:practitioner
organization.active
organization.identifier
organization.name
location.status
location.identifier
location.name
service.active
service.indentifier
service.location
service.name
service.organization
```

###### 2:3.90.4.1.2.6 HealthcareService Resource Message Semantics

The Care Services Selective Supplier shall support the following search
parameters on the HealthcareService Resource as defined at
[http://hl7.org/fhir/R4/healthcareservice.html#search](http://hl7.org/fhir/R4/healthcareservice.html#search). String parameter
modifiers are defined at [http://hl7.org/fhir/R4/search.html#string](http://hl7.org/fhir/R4/search.html#string).

```
active
identifier
location
name
organization
service-type
organization.active
organization.identifier
organization.name
location.status
location.identifier
location.name
```

###### 2:3.90.4.1.2.7 Location Distance Option Message Semantics

The Care Services Selective Supplier supporting the Location Distance
Option shall support the following search parameters on the Location
Resource as defined at [http://hl7.org/fhir/R4/location.html#search](http://hl7.org/fhir/R4/location.html#search).

```
near
```

##### 2:3.90.4.1.3 Expected Actions

The Care Services Selective Supplier shall process the query to discover
the resources that match the search parameters given, and return a
response as per Section 2:3.90.4.2 or an error as per
[http://hl7.org/fhir/R4/search.html#errors](http://hl7.org/fhir/R4/search.html#errors).

#### 2:3.90.4.2 Find Matching Care Services Response Message

##### 2:3.90.4.2.1 Trigger Events

The Care Services Selective Supplier sends the Find Matching Care
Services Response to the Care Services Selective Consumer when results
to the query are ready.

##### 2:3.90.4.2.2 Message Semantics

The Care Services Selective Supplier shall support the search response
message as defined at [http://hl7.org/fhir/R4/http.html#search](http://hl7.org/fhir/R4/http.html#search) on the
following Resources.

  - Organization, as defined at
    [http://hl7.org/fhir/R4/organization.html](http://hl7.org/fhir/R4/organization.html)

  - Location, as defined at [http://hl7.org/fhir/R4/location.html](http://hl7.org/fhir/R4/location.html)

  - Practitioner, as defined at
    [http://hl7.org/fhir/R4/practitioner.html](http://hl7.org/fhir/R4/practitioner.html)

  - PractitionerRole, as defined at
    [http://hl7.org/fhir/R4/practitionerrole.html](http://hl7.org/fhir/R4/practitionerrole.html)

  - HealthcareService, as defined at
    [http://hl7.org/fhir/R4/healthcareservice.html](http://hl7.org/fhir/R4/healthcareservice.html)
    
All References (reference.reference element) to Resources defined in
this transaction shall be populated with an accessible URL (see
[https://www.hl7.org/fhir/references-definitions.html#Reference.reference](https://www.hl7.org/fhir/references-definitions.html#Reference.reference)), unless the referenced resource is not present on a server accessible
to the client.

###### 2:3.90.4.2.2.1 FHIR Organization Resource Constraints

A Care Services Selective Consumer may query on Organization Resources.
A Care Services Selective Supplier shall return a Bundle of matching
Organization Resources. The Organization Resource shall be further
constrained as described in [Table 2:3.90.4.2.2.1-1](#table2.3.90.4.2.2.1-1). The Element column in
[Table 2:3.90.4.2.2.1-1](#table2.3.90.4.2.2.1-1) references the object model defined at
[http://hl7.org/fhir/R4/organization.html#resource](http://hl7.org/fhir/R4/organization.html#resource).

<a name="table2.3.90.4.2.2.1-1"></a>**Table 2:3.90.4.2.2.1-1: Organization Resource Constraints**

| Element &amp; Cardinality | Data Type |
| ------------------------- | --------- |
| `meta.profile`<br />`[1..*]` | There shall be at least one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_Organization` |
| `type`<br />`[1..*]` | A code that describes the type of Organization.<br />`CodeableConcept` |
| `name`<br />`[1..1]` | `string` |
| `partOf`<br />`[0..1]` | If the Organization belongs to a single hierarchy, the partOf element shall be used.<br />`Reference (Organization)` |
| `extension`<br />`[0..*]` | If there are additional hierarchies (such as funding source), include them in the extension with the following details:<br />Set the url to the canonical URI for this extension<br />`url = "http://ihe.net/fhir/StructureDefinition/IHE_mCSD_hierarchy_extension"`<br />Set the sub-extension values<br />`hierarchy-type = valueCodeableConcept`<br />`part-of = valueReference(Organization)` |
{: .grid .table-striped}

A Care Services Selective Consumer may query on Organization Resources
when working with Facilities. A Care Services Selective Supplier shall
return a Bundle of matching Organization Resources when working with
Facilities. In addition to the constraints in [Table 2:3.90.4.2.2.1-1](#table2.3.90.4.2.2.1-1), the
FHIR Organization Resource shall be further constrained as described in
[Table 2:3.90.4.2.2.1-2](#table2.3.90.4.2.2.1-2). The Element column in [Table 2:3.90.4.2.2.1-2](#table2.3.90.4.2.2.1-2)
references the object model defined at
[http://hl7.org/fhir/R4/organization.html#resource](http://hl7.org/fhir/R4/organization.html#resource).

<a name="table2.3.90.4.2.2.1-2"></a>**Table 2:3.90.4.2.2.1-2: Additional Organization Resource Constraints for
Facilities**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[2..*]` | In addition, there shall be one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_FacilityOrganization` |
| `type`<br />`[2..*]` | In addition, there shall be one type with the following value:<br />`system = "urn:ietf:rfc:3986"`<br />`code = "urn:ihe:iti:mcsd:2019:facility"` |
{: .grid .table-striped}

A Care Services Selective Consumer may query on Organization Resources when working with Jurisdictions. A Care Services Selective Supplier shall return a Bundle of matching Organization Resources when working with Jurisdictions. In addition to the constraints in [Table 3.90.4.2.2.1-1](#table2.3.90.4.2.2.1-1), the FHIR Organization Resource shall be further constrained as described in [Table 3.90.4.2.2.1-3](#table2.3.90.4.2.2.1-3). The Element column in [Table 3.90.4.2.2.1-3](#table2.3.90.4.2.2.1-3) references the object model defined at [http://hl7.org/fhir/R4/organization.html#resource](http://hl7.org/fhir/R4/organization.html#resource).

<a name="table2.3.90.4.2.2.1-3"></a>**Table 2:3.90.4.2.2.1-3: Additional Organization Resource Constraints for
Jurisdictions**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[2..*]` | In addition, there shall be one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_JurisdictionOrganization` |
| `type`<br />`[2..*]` | In addition, there shall be one type with the following value:<br />`system = "urn:ietf:rfc:3986"`<br />`code = "urn:ihe:iti:mcsd:2019:jurisdiction"` |
{: .grid .table-striped}

###### 2:3.90.4.2.2.2 FHIR Location Resource Constraints

A Care Services Selective Consumer may query on Location Resources. A
Care Services Selective Supplier shall return a Bundle of matching
Location Resources. The Location Resource shall be further constrained
as described in [Table 2:3.90.4.2.2.2-1](#table2.3.90.4.2.2.2-1). The Element column in [Table
2:3.90.4.2.2.2-1](#table2.3.90.4.2.2.2-1) references the object model defined at
[http://hl7.org/fhir/R4/location.html#resource](http://hl7.org/fhir/R4/location.html#resource).

<a name="table2.3.90.4.2.2.2-1"></a>**Table 2:3.90.4.2.2.2-1: Location Resource Constraints**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[1..*]` | There shall be at least one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_Location` |
| `type`<br />`[1..*]` | A code that describes the type of Organization.<br />`CodeableConcept` |
| `physicalType`<br />`[1..1]` | A code that describes the physical type of Organization.<br />`CodeableConcept` |
| `name`<br />`[1..1]` | `string` |
| `status`<br />`[1..1]` | `code (active| suspended| inactive)` |
{ .grid .table-striped}

When the resource is a Facility, the Location Resource shall be paired
with an Organization Resource using the managingOrganization element in
Location. A Care Services Selective Consumer may query on Location
Resources when working with Facilities. A Care Services Selective
Supplier shall return a Bundle of matching Location Resources when
working with Facilities. In addition to the constraints in [Table
2:3.90.4.2.2.2-1](#table2.3.90.4.2.2.2-1), the FHIR Location Resource shall be further constrained
as described in [Table 2:3.90.4.2.2.2-2](#table2.3.90.4.2.2.2-2). The Element column in [Table
2:3.90.4.2.2.2-2](#table2.3.90.4.2.2.2-2) references the object model defined at
[http://hl7.org/fhir/R4/location.html#resource](http://hl7.org/fhir/R4/location.html#resource).

<a name="table2.3.90.4.2.2.2-2"></a>**Table 2:3.90.4.2.2.2-2: Additional Location Resource Constraints for
Facilities**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[2..*]` | In addition, there shall be one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_FacilityLocation` |
| `type`<br />`[2..*]` | In addition, there shall be one type with the following value:<br />`system = "urn:ietf:rfc:3986"`<br />`code = "urn:ihe:iti:mcsd:2019:facility"` |
| `managingOrganization`<br />`[1..1]` | The reference to the Organization resource for this facility.<br />`Reference(Organization)` |
{: .grid .table-striped}

When the resource is a Jurisdiction, the Location Resource shall be paired with an Organization
Resource using the managingOrganization element in Location. A Care Services Selective Consumer 
may query on Location Resources when working with Jurisdictions. A Care Services Selective Supplier 
shall return a Bundle of matching Location Resources when working with Jurisdictions. In addition to 
the constraints in [Table 3.90.4.2.2.2-1](#table2.3.90.4.2.2.2-1), the FHIR Location Resource shall be further constrained as 
described in [Table 3.90.4.2.2.2-3](#table2.3.90.4.2.2.2-3). The Element column in [Table 3.90.4.2.2.2-3](#table2.3.90.4.2.2.2-3) references the object 
model defined at [http://hl7.org/fhir/R4/location.html#resource](http://hl7.org/fhir/R4/location.html#resource).  

When a geographic boundary is available for the Jurisdiction Location, the location-boundary-geojson extension defined at 
[http://hl7.org/fhir/extension-location-boundary-geojson.html](http://hl7.org/fhir/extension-location-boundary-geojson.html) shall be used to store this information.

<a name="table2.3.90.4.2.2.2-3"></a>**Table 2:3.90.4.2.2.2-3: Additional Location Resource Constraints for
Jurisdictions**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[2..*]` | In addition, there shall be one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_JurisdictionLocation` |
| `extension`<br />`[0..*]` | When a boundary is available, the location-boundary-geojson extension should be used with the given url, contentType, and data:<br />`url = http://hl7.org/fhir/StructureDefinition/location-boundary-geojson`<br />`valueAttachment.contentType = "application/geo+json"`<br />`valueAttachment.data = base64 encoded GeoJSON boundary data` |
| `type`<br />`[2..*]` | In addition, there shall be one type with the following value:<br />`system = "urn:ietf:rfc:3986"`<br />`code = "urn:ihe:iti:mcsd:2019:facijurisdictionlity"` |
| `managingOrganization`<br />`[1..1]` | The reference to the Organization resource for this jurisdiction.<br />`Reference(Organization)` |
{: .grid .table-striped}

When supporting the Location Distance Option. The Location Resource
shall be further constrained as described in [Table 2:3.90.4.2.2.2-4](#table2.3.90.4.2.2.2-4). The
Element column in [Table 2:3.90.4.2.2.2-4](#table2.3.90.4.2.2.2-4) references the object model
defined at [http://hl7.org/fhir/R4/location.html#resource](http://hl7.org/fhir/R4/location.html#resource).

<a name="table2.3.90.4.2.2.2-4"></a>**Table 2:3.90.4.2.2.2-4: Location Resource Constraints with Location
Distance Option**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[2..*]` | There shall be at least one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_LocationDistance` |
| `position`<br />`[1..1]` | `BackboneElement` |
{: .grid .table-striped}

###### 2:3.90.4.2.2.3 FHIR Practitioner Resource Constraints

A Care Services Selective Consumer may query on Practitioner Resources.
A Care Services Selective Supplier shall return a Bundle of matching
Practitioner Resources. The Practitioner Resource shall be further
constrained as described in [Table 2:3.90.4.2.2.3-1](#table2.3.90.4.2.2.3-1). The Element column in
[Table 2:3.90.4.2.2.3-1](#table2.3.90.4.2.2.3-1) references the object model defined at
[http://hl7.org/fhir/R4/practitioner.html#resource](http://hl7.org/fhir/R4/practitioner.html#resource).

<a name="table2.3.90.4.2.2.3-1"></a>**Table 2:3.90.4.2.2.3-1: Practitioner Resource Constraints**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[1..*]` | There shall be at least one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_Practitioner` |
| `name`<br />`[1..*]` | `HumanName` |
{: .grid .table-striped}

###### 2:3.90.4.2.2.4 FHIR PractitionerRole Resource Constraints

A Care Services Selective Consumer may query on PractitionerRole
Resources. A Care Services Selective Supplier shall return a Bundle of
matching PractitionerRole Resources. The PractitionerRole Resource shall
be further constrained as described in [Table 2:3.90.4.2.2.4-1](#table2.3.90.4.2.2.4-1). The Element
column in [Table 2:3.90.4.2.2.4-1](#table2.3.90.4.2.2.4-1) references the object model defined at
[http://hl7.org/fhir/R4/practitionerrole.html#resource](http://hl7.org/fhir/R4/practitionerrole.html#resource).

<a name="table2.3.90.4.2.2.4-1"></a>**Table 2:3.90.4.2.2.4-1: PractitionerRole Resource Constraints**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[1..*]` | There shall be at least one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_PractitionerRole` |
| `code`<br />`[1..*]` | `CodeableConcept` |
{: .grid .table-striped}

###### 2:3.90.4.2.2.5 FHIR HealthcareService Resource Constraints

A Care Services Selective Consumer may query on HealthcareService
Resources. A Care Services Selective Supplier shall return a Bundle of
matching HealthcareService Resources. The HealthcareService Resource
shall be further constrained as described in [Table 2:3.90.4.2.2.5-1](#table2.3.90.4.2.2.5-1). The
Element column in [Table 2:3.90.4.2.2.5-1](#table2.3.90.4.2.2.5-1) references the object model
defined at [http://hl7.org/fhir/R4/healthcareservice.html#resource](http://hl7.org/fhir/R4/healthcareservice.html#resource).

<a name="table2.3.90.4.2.2.5-1"></a>**Table 2:3.90.4.2.2.5-1: HealthcareService Resource Constraints**

| Element &amp; Cardinality | Data Type
| ------------------------- | --------- |
| `meta.profile`<br />`[1..*]` | There shall be at least one entry with the value:<br />`http://ihe.net/fhir/StructureDefinition/IHE_mCSD_HealthcareService` |
| `type`<br />[1..*]` | `CodeableConcept` |
| `name`<br />`[1..1]` | `string` |
{: .grid .table-striped}

##### 2:3.90.4.2.3 Expected Actions

The Care Services Selective Consumer has received the response and
continues with its workflow.

### 2:3.90.5 Security Considerations

See [ITI TF-1: 46.5](volume-1.html#1465-mcsd-security-considerations) for security considerations for the mCSD Profile.

See [ITI TF-2x: Appendix Z.8](https://profiles.ihe.net/ITI/TF/Volume2/ch-Z.html#z.8-mobile-security-considerations) for common mobile security considerations.