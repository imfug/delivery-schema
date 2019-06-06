
# IMF Delivery Schema

## Introduction

TBD  

## Scope

TBD  

## Normative References

1. SMPTE ST 2067-2 Interoperable Master Format - Core Constraints
2. SMPTE ST 2067-3 Interoperable Master Format - Composition Playlist
3. SMPTE ST 2067-5 Interoperable Master Format - Essence Component
4. SMPTE ST 2067-8 Interoperable Master Format - Common Audio Labels

5. SMPTE ST 2067-20 Interoperable Master Format - Application #2
6. SMPTE ST 2067-21 Interoperable Master Format - Application #2E
7. SMPTE ST 2067-30 Interoperable Master Format - Application #3
8. SMPTE ST 2067-40 Interoperable Master Format - Application #4 Cinema Mezzanine
9. SMPTE ST 2067-50 Interoperable Master Format - Application #5 ACES

10. SMPTE ST 2067-100 Interoperable Master Format - Output Profile List
11. SMPTE ST 2067-102 Interoperable Master Format - Common Image Pixel Color Schemes
12. SMPTE ST 2067-103 Interoperable Master Format - Output Profile List - Common Audio Definition and Macros

13. SMPTE RDD 45-2017 Interoperable Master Format - Apple ProRes

14. SMPTE ST 428-12-2013 D-Cinema - Distribution Master Common Audio Channels and Soundfield Groups

## Glossary

|Term|Definition  |
|----|------------|
|Composition  |Embodies a version of a complete work, combining metadata and essence  |
|Essence     |Content, e.g. image, audio or data essence, meant for presentation.|
|IMF         |Acronym for Interoperable Master Format.|
|Resource    |A portion of an Asset selected for reproduction on the Composition timeline.|
|Sequence    |An ordered collection of Resources to be reproduced sequentially.|
|Segment     |A collection of Sequences intended to be reproduced in parallel.|
|UUID        |Acronym for Universal Unique Identifier.|
|XML         |Acronym for extensible Markup Language.|

## Instance

A Delivery Specification List instance shall be an XML document, as specified in [XML], that consists of a single DeliverySpecificationList element.

## Schema

Each Delivery Specification List instance shall conform to the XML schema definitions (see [XML Schema]) found in this specification. In the event of a conflict between schema definitions and the prose, the prose shall take precedence.

## XML Schema root element definition
```xml
<xs:schema
  xmlns:xs="http://www.w3.org/2001/XMLSchema"
  xmlns:dcml="http://www.smpte-ra.org/schemas/433/2008/dcmlTypes/">
  <!-- schema definitions found in this document excluding this one -->
</xs:schema>
```

The namespace prefixes used in XML Schema definitions herein are not normative values and implementations shall perform correctly with any XML compliant prefix values. The XML Schema definitions found in this specification include elements specified in [XML Digital Signature] and [SMPTE ST 433].

A schema instance that consolidates all inline schema definitions made in this document is provided for convenience in Annex B. In case of conflict, the schema definitions included herein shall take precedence.

## Character Encoding

Delivery Specification List instances shall be encoded using the UTF-8 character encoding.

## MIME Type

The MIME type, as defined in IETF RFC 2046, of a Delivery Specification List instance shall be `text/xml`.

## Structure Versioning

The target namespace specified in Section 5.1, i.e. the value of the targetNamespace attribute of the schema element, shall only be used by Delivery Specification List instances that conform to this specification as expressed by the combination of its prose and schema definitions.

Instances using specifications that modify the schema definitions or the semantics of the elements defined herein, including future versions of this specification, shall use a different namespace and no two distinct schemas shall have the same target namespace. As such, the target namespace allows implementations to unambiguously identify the defining specification of a Delivery Specification List instance.

## Structure

In order to avoid duplication between text and schema, the cardinality and default values of elements are specified in the schema only.

## Schema

The schema can be found [here](../schema/IMF_DeliverySchema.xsd)

##### Id

The Id element shall uniquely identify the Delivery Specification List instance. Any two Delivery Specification List instances may have identical Id values if and only if the two Delivery Specification List instances are identical.

##### Annotation

The Annotation element shall be a free-form, human-readable annotation describing the composition. It is meant strictly as a display hint to the user.

##### IssueDate

The IssueDate element shall indicate the time and date at which the Delivery Specification List was issued.

##### Issuer

The Issuer element shall be a free-form, human-readable annotation that identifies the entity that created the Delivery Specification List. It is meant strictly for display to the user.

Note: The Signer element defined in Section 6.1.17 is used to identify the entity that digitally signed the Delivery Specification List.

##### Creator

The Creator element shall be a free-form, human-readable annotation that identifies the device or software program used to create the Delivery Specification List, the facility that created the Delivery Specification List and the operator that created the Delivery Specification List. It is meant strictly for display to the user.

##### DeliverableList

The DeliverableList element contains a list of Deliverable elements that fully describe individual specifications for delivery.

##### Deliverable

The Deliverable element describes the various constraints that a deliverable should be compliant with.

##### CompositionPlaylistConstraints

The CompositionPlaylistConstraints element contains a collection of various elements describing constraints that are applicable to the Composition.

##### OwnerId

The OwnerId element is used by the creator/publisher/owner of the delivery specification
to carry a globally unique identifier that is assigned to the deliverable. The unicity of 
the identifier can be guaranteed by the owner using a variety of methods. 

It is strongly recommended that the owner uses a DNS-based (Domain Name System) identifier 
such as: 

http://www.example.com/myDelivery_v1

The OwnerId is used by information systems to uniquely identify the Deliverable. The handling of identifier collisions is beyond the scope of this specification.


##### ApplicationIdentificationList

The ApplicationIdentificationList element contains a list of identifiers that a Composition conforms to.

##### ApplicationIdentification

The ApplicationIdentification element shall identify an Application to which a Composition
conforms. The specification for this element is defined in the following table:

.XML Schema definition for ApplicationIdentification element

```xml
<xs:element 
  name="ApplicationIdentification" 
  type="xs:anyURI" 
  minOccurs="1" 
  maxOccurs="unbounded" 
/>
```

##### MatchType

The MatchType element defines the matching algorithm to be used to match values available in a list. The following values are allowed

|Value|Meaning|
|-----|-------|
|exclusive | one and only one value must be present|
|inclusive | one or more values may be present|

For example, when using the MatchType with the ApplicationIdentification items in the ApplicationIdentificationList element, the following behavior is expected:

MatchType is exclusive: among the values present in the list, only one of them can be present in the CPL. The CPL is expected to carry one and only one instance of ApplicationIdentification.

MatchType is inclusive: one or more of the values listed can be present in the CPL. The CPL is expected to carry one or more instances of ApplicationIdentification.

##### ValueList

The ValueList element contains one or more elements of the same type, describing a list of possible values.

##### VirtualTrackList

The VirtualTrackList element is a list of elements derived from the abstract GenericVirtualTrackType type. These elements represent the virtual tracks that must exist in the CompositionPlaylist. In the absence of further indication, the order of the elements in the list is meaningless.

The following concrete virtual tracks can be used:

|Element                |Definition                                                            |
|-----------------------|----------------------------------------------------------------------|
| ImageVirtualTrack     | defines a MainImageSequence virtual track in the CompositionPlaylist |
| AudioVirtualTrack     | defines a MainAudioSequence virtual track in the CompositionPlaylist |
| MarkerVirtualTrack    | defines a MarkerSequence virtual track in the CompositionPlaylist    |
| TimedTextVirtualTrack | defines a timed-text virtual track in the CompositionPlaylist        |

*Note:* the VirtualTrackList can be empty, which implies that the Deliverable is not specifying any constrains on the virtual tracks in the CompositionPlaylist.

#### Virtual Tracks

Virtual tracks are defined per kind of essence. All virtual track definitions are derived from a GenericVirtualTrackType which specifies a set of common properties, described in the following sections. Specialized virtual tracks (e.g. ImageVirtualtrack, AudioVirtualTrack, etc) have additional elements required to specify additional constraints on the essence they reference.

#### Generic Virtual Track Elements

##### EssenceEncodingConstraintList

The EssenceEncodingConstraintList element is an optional list of EssenceEncodingConstraint designed to carry custom constraints. Each EssenceEncodingConstraintList is to be considered in a specific context defined by the scope attribute. The scope attribute is a generic URI that is entirely controlled by the entity which specifies the list of constraints. 

##### EssenceEncodingConstraint

Each EssenceEncodingConstraint element is defined by a name and a list of properties. Each property of the list is a Name/Value pair, each being defined as a string. Their values and use depend entirely on the specification represented by the scope attribute of the EssenceEncodingConstraintList.

##### TimelineComplexity

The TimelineComplexity element describes the cardinality and temporal constraints of its components.

##### Segment

The Segment element describes the cardinality and temporal constraints of its components.

##### Sequence

The Sequence element describes the cardinality and temporal constraints of its components.

##### Resource

The Sequence element describes the cardinality and temporal constraints of its components.

##### Cardinality

The Cardinality element defines in the minimum and maximum number of objects of a class. The cardinality range is defined by the MinItem and MaxItem elements.

##### MinItem

The MinItem element defines the minimum number of objects of a class.

##### MaxItem

The MaxItem element defines the maximum number of objects of a class

#### Marker Virtual Track Elements

TBD

#### Image Virtual Track Elements

##### EssenceEncoding

The EssenceEncoding element defines the encoding method and/or algorithm used to encode the essence used by a specific virtual track.

##### Colorimetry

The Colorimetry element defines the combination of Color Primaries, Transfer Characteristic and potentially Coding Equations to be used for describing the color information in a Trackfile.

The allowed values depend on the Application being targetted. The syntax of the values shall use the following pattern:

###### COLOR.x

where x is an alpha-numercial expression defined in the Application specification documents. Currently the following values are supported:

|Value|Definition|
|-----|-------|
|COLOR.1| see ST2067-20, Table 3|
|COLOR.2| see ST2067-20, Table 3|
|COLOR.3| see ST2067-20, Table 3|
|COLOR.4| see ST2067-21, Table 4|
|COLOR.5| see ST2067-21, Table 4|
|COLOR.6| see ST2067-21, Table 4|
|COLOR.7| see ST2067-21, Table 4|
|COLOR.APP5.AP0| see ST2067-50, Table 3|
|COLOR.8DPP| see TSP2121-1, Table 2|
|XYZ|missing ref.|

##### Sampling

The Sampling element defines the sampling of the color components in the image essence. The following table describes the allowed values:

|Value|
|-----|
|4:2:2|
|4:4:4|
|4:4:4:4 |

##### Quantization

The Quantization element defines the signal quantization system used to encode the normalized signal values into code values. The allowed values depend on the Application being targetted and they are listed in the table below:

|Value|Definition|
|-----|-------|
|QE.1| see ST2067-20, Table 4|
|QE.2| see ST2067-20, Table 4|

##### FrameStructure

The FrameStructure element definies the raster scanning method. Its value must be one of the following:

|Value|Meaning|
|-----|-------|
|Progressive |Used for material that uses progressive raster scanning
|Interlaced  |Used for material that uses interlaced raster scanning

##### Stereoscopy

The Stereoscopy element defines the monoscopic or stereoscopic nature of the essence referenced by the ImageVirtualTrack. The currently supported values are defined in the table below:

|Value|Meaning|
|-----|-------|
|Monoscopic |The image track essence contains a single point-of-view, targeting both the left and right eyes.
|Stereoscopic  |The image track essence contains two points-of-view, targeting the left and right eyes respectively.

##### ColorComponents

The ColorComponents element defines the interpretation of the color channels used for the image essence. The order that the color components have in the essence is defined by the Application specification documents. The following table describes the allowed values:

|Values|
|------|
|RGB|	
|RGBA|
|XYZ|
|YCbCr|

##### PixelBitDepthList

The PixelBitDepthList contains one or more PixelBitDepth elements that define the possible values for the pixel bitdepths

##### PixelBitDepth

The PixelBitDepth defines the pixel bitdepth value for the deliverable

##### ImageFrameWidthList

The ImageFrameWidthList contains one or more ImageFrameWidth elements that define the possible values for the image width. The ImageFrameWidthList element is optional. 

If absent, then the Deliverable sets no constraints on the horizonal resolution of the essence referenced by the ImageVirtualTrack. In this case, the constraints defined by the Application identified by the ApplicationIdentification elements are applicable.

If present, the Deliverable limits the horizontal resolution of the essence referenced by the ImageVirtualTrack to the values defined by the ImageFrameWidth elements.

##### ImageFrameWidth

The ImageFrameWidth defines the intended display width, or horizontal resolution, in pixels. Please note that values that do not fall in the ranges defined by the Application identified by the ApplicationIdentification elements are not valid.

##### ImageFrameHeightList

The ImageFrameHeightList contains one or more ImageFrameHeight elements that define the possible values for the image height. The ImageFrameHeightList element is optional. 

If absent, then the Deliverable sets no constraints on the vertical resolution of the essence referenced by the ImageVirtualTrack. In this case, the constraints defined by the Application identified by the ApplicationIdentification elements are applicable.

If present, the Deliverable limits the vertical resolution of the essence referenced by the ImageVirtualTrack to the values defined by the ImageFrameHeight elements.

##### ImageFrameHeight

The ImageFrameHeight defines the intended display height, or vertical resolution, in pixels. Please note that values that do not fall in the ranges defined by the Application identified by the ApplicationIdentification elements are not valid.

##### FrameRateList

The FrameRateList contains one or more FrameRate elements that define the possible values for the video frame rate.

##### FrameRate   

The FrameRate defines the intended video frame rate.

#### Audio Virtual Track Elements

##### SoundfieldGroupConfiguration

The SoundfieldGroupConfiguration element defines the soundfield configuration for the audio channels in the group. The configuration is signaled via the MCATagSymbol child element.

##### AudioChannelMapping

The AudioChannelMapping element is a list of ordered AudioChannel elements that explicit the audio channel layout in the soundfield group defined by the SoundfieldGroupConfiguration.

The order in which the AudioChannel elements are listed must correspond to the order in which the actual channels appear in the trackfile.

##### AudioChannel

The AudioChannel element defines the constraints on a single audio channel that participates in the soundfield group defined by the SoundfieldGroupConfiguration element.

The routing destination is signaled via the MCATagSymbol child element.

##### MCATagSymbol

The MCATagSymbol element is a human readable mnemonic that uniquely identifies the audio channel or soundfield group. The values of the MCATagSymbol element are restricted to the list of values defined in SMPTE ST2067-8 and ST428-12.

An addistional constraint is applied to the list of possible values, based on the parent element (i.e. SoundfieldGroupConfiguration or AudioChannel).

##### SampleRateList

The SampleRateList contains one or more SampleRate elements that define the possible values for the audio sample rate.

##### SampleRate   

The SampleRate defines the intended audio sample rate. Currently only the following values are supported by the ST2067 family of standards:

|Values|Meaning|
|------|-------|
|48000 1|	represents an audio sampling rate of 48kHz|
|96000 1|	represents an audio sampling rate of 96kHz|

#### Timed Text Virtual Track Elements

##### UCSEncoding

TBD

##### NamespaceURI

TBD

#### Digital Signature

##### Signer

The Signer element shall uniquely identify the entity that digitally signed the Delivery Specification List. If the Signer element is present, then the Signature element shall also be present.

If X.509 certificates are used as specified in [XML Digital Signature](https://www.w3.org/TR/xmldsig-core1/), then the Signer element shall contain one X509Data element containing one X509IssuerSerial element, which uniquely identifies the certificate used to sign the Delivery Specification List.

##### Signature

The Signature element shall contain a digital signature authenticating the Delivery Specification List.
If the Signature element is present, then the Signer element shall be present.
The digital signature shall be enveloped, as specified in [XML Digital Signature](https://www.w3.org/TR/xmldsig-core1/), and apply to the entire Delivery Specification List. The signature is generated by the signer, as identified by the Signer element.

### Annex A Bibliography (Informative)

TBD

### Annex B Consolidated Schema (Informative)

This specification is accompanied by the following element, which is an XML schema document as specified in [XML Schema Part 1: Structures](https://www.w3.org/TR/xmlschema-1/).

The schema can be found [here](../schema/IMF_DeliverySchema.xsd)

This element collects the XML schema definitions defined in this specification. It is informative and, in case of conflict, this specification takes precedence.

### Annex D Considerations for Applications (Informative)

TBD

### Annex E Sample Instance (Informative)

This specification is accompanied by the following element, which is an XML document that contains a sample instance of the DeliverySpecificationList element.

#### Sample

[Netflix Original specification 3.0 UHD 4K HDR](../examples/Netflix/DRAFT_Netflix_OriginalsSpec_3.0_UHD_4K_SDR.xml)

This element is for illustration only, and is neither intended to capture current or future practice, nor exercise all normative language contained in this specification.



