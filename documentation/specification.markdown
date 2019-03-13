**

## IMF Delivery Specification List

**

**History**
|Date|Author|Change|
|--|--|--|
|2018-05-12 | Dan Tatut | Initial draft|
|2018-08-13	| Dan Tatut | Initial ASCIIdoc version|
|2019-03-13 | Dan Tatut | Initial StackEdit version|

**Foreword**

TBD


**Intellectual Property**

TBD


**Introduction**

TBD


**Scope**

TBD


**Conformance Notation**

TBD


**Normative References**

TBD


**Glossary**

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

**Instance**

A Delivery Specification List instance shall be an XML document, as specified in [XML], that consists of a single DeliverySpecificationList element.

**Schema**

Each Delivery Specification List instance shall conform to the XML schema definitions (see [XML Schema]) found in this specification. In the event of a conflict between schema definitions and the prose, the prose shall take precedence.


**XML Schema root element definition**

    <xs:schema
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        xmlns:dcml="http://www.smpte-ra.org/schemas/433/2008/dcmlTypes/">
    <!-- schema definitions found in this document excluding this one -->
    </xs:schema>

The namespace prefixes used in XML Schema definitions herein are not normative values and implementations shall perform correctly with any XML compliant prefix values. The XML Schema definitions found in this specification include elements specified in [XML Digital Signature] and [SMPTE ST 433].

A schema instance that consolidates all inline schema definitions made in this document is provided for convenience in Annex B. In case of conflict, the schema definitions included herein shall take precedence.

**Character Encoding**

Delivery Specification List instances shall be encoded using the UTF-8 character encoding.

**MIME Type**

The MIME type, as defined in IETF RFC 2046, of a Delivery Specification List instance shall be 

    text/xml.

**Structure Versioning**

The target namespace specified in Section 5.1, i.e. the value of the targetNamespace attribute of the schema element, shall only be used by Delivery Specification List instances that conform to this specification as expressed by the combination of its prose and schema definitions.

Instances using specifications that modify the schema definitions or the semantics of the elements defined herein, including future versions of this specification, shall use a different namespace and no two distinct schemas shall have the same target namespace. As such, the target namespace allows implementations to unambiguously identify the defining specification of a Delivery Specification List instance.

**Structure**

In order to avoid duplication between text and schema, the cardinality and default values of elements are specified in the schema only.

**Schema**

https://github.com/imfug/delivery-schema/blob/master/schema/IMF_DeliverySchema.xsd

=== Id

The Id element shall uniquely identify the Delivery Specification List instance. Any two Delivery Specification List instances may have identical Id values if and only if the two Delivery Specification List instances are identical.

=== Annotation

The Annotation element shall be a free-form, human-readable annotation describing the composition. It is meant strictly as a display hint to the user.

=== IssueDate

The IssueDate element shall indicate the time and date at which the Delivery Specification List was issued.

=== Issuer

The Issuer element shall be a free-form, human-readable annotation that identifies the entity that created the Delivery Specification List. It is meant strictly for display to the user.

Note: The Signer element defined in Section 6.1.17 is used to identify the entity that digitally signed the Delivery Specification List.

=== Creator

The Creator element shall be a free-form, human-readable annotation that identifies the device or software program used to create the Delivery Specification List, the facility that created the Delivery Specification List and the operator that created the Delivery Specification List. It is meant strictly for display to the user.

=== DeliverableList

The DeliverableList element contains a list of Deliverable elements that fully describe individual specifications for delivery.

=== Deliverable

The Deliverable element describes the various constraints that a deliverable should be compliant with.

=== CompositionPlaylistConstraints

The CompositionPlaylistConstraints element contains a collection of various elements describing constraints that are applicable to the Composition.

=== ApplicationIdentificationList

The ApplicationIdentificationList element contains a list of identifiers that a Composition conforms to.

=== ApplicationIdentification

The ApplicationIdentification element shall identify an Application to which a Composition
conforms. The specification for this element is defined in the following table:

.XML Schema definition for ApplicationIdentification element
[source,xml]
----
<xs:element 
	name="ApplicationIdentification" 
	type="xs:anyURI" 
	minOccurs="1" 
	maxOccurs="unbounded" 
/>
----

=== MatchType

The MatchType element defines the matching algorithm to be used to values available in a list. The following values are allowed

|==================================================
|exlcusive | one and only one value must be present
|inclusive | one or more values may be present
|==================================================

=== ValueList

The ValueList element contains one or more elements of the same type, describing a list of possible values.

=== VirtualTrackList

The VirtualTrackList element is an ordered list of VirtualTrack elements that represent the virtual tracks used in the composition in the exact order as they should appear in the CompositionPlaylist.

=== VirtualTrack

The VirtualTrack element describes the kind of track as well as the track essence properties.

=== Kind

The Kind element represents the class that the virtual track belongs to. The values of the Kind element use the exact name of the element used in the CompositionPlaylist to signal the virtual track (e.g. MainImageSequence for the main image virtual track, MainAudioSequence for the audio tracks, etc).

=== TimelineComplexity

The TimelineComplexity element describes the cardinality and temporal constraints of its components.

=== Segment

The Segment element describes the cardinality and temporal constraints of its components.

=== Sequence

The Sequence element describes the cardinality and temporal constraints of its components.

=== Resource

The Sequence element describes the cardinality and temporal constraints of its components.

=== Cardinality

The Cardinality element defines in the minimum and maximum number of objects of a class. The cardinality range is defined by the MinItem and MaxItem elements.

=== MinItem

The MinItem element defines the minimum number of objects of a class.

=== MaxItem

The MaxItem element defines the maximum number of objects of a class

=== EssenceEncoding

The EssenceEncoding element defines the encoding method and/or algorithm used to encode the essence used by a specific virtual track.

=== Colorimetry

The Colorimetry element defines the combination of Color Primaries, Transfer Characteristic and potentially Coding Equations to be used for describing the color information in a Trackfile

The allowed values depend on the Application being targetted. The syntax of the values shall use the following pattern:

COLOR.x

where x is an alpha-numercial expression defined in the Application specification documents.

=== Sampling

The Sampling element defines the sampling of the color components in the image essence. The following table describes the allowed values:

.Sampling values
|===============
|4:2:2   |
|4:4:4   |
|4:4:4:4 |
|===============

=== Quantization

The Quantization element defines the signal quantization system used to encode the normalized signal values into code values. The allowed values depend on the Application being targetted. The syntax of the 

values shall use the following pattern:

QE.x

where x is an alpha-numercial value defined in the Application specification documents.

=== FrameStructure

The FrameStructure element definies the raster scanning method. Its value must be one of the following:

.FrameStructure values
|====================================================================
|Progressive |Used for material that uses progressive raster scanning
|Interlaced  |Used for material that uses interlaced raster scanning
|====================================================================

=== Stereoscopy

<Stereoscopy>Monoscopic</Stereoscopy>

=== ColorComponents

The ColorComponents element defines the interpretation of the color channels used for the image essence. The order that the color components have in the essence is defined by the Application specification documents. The following table describes the allowed values:

.ColorComponents values
|===============
|RGB	
|RGBA	
|XYZ	
|YCbCr	
|===============

=== PixelBitDepthList

The PixelBitDepthList contains one or more PixelBitDepth elements that define the possible values for the pixel bitdepths

=== PixelBitDepth

The PixelBitDepth defines the pixel bitdepth value for the deliverable

=== ImageFrameWidthList

The ImageFrameWidthList contains one or more ImageFrameWidth elements that define the possible values for the image width.

=== ImageFrameWidth

The ImageFrameWidth defines the intended display width.

=== ImageFrameHeightList

The ImageFrameHeightList contains one or more ImageFrameHeight elements that define the possible values for the image height.

=== ImageFrameHeight

The ImageFrameHeight defines the intended display height.

=== FrameRateList

The FrameRateList contains one or more FrameRate elements that define the possible values for the video frame rate.

=== FrameRate   

The FrameRate defines the intended video frame rate.

=== SoundfieldGroupConfiguration

TBD

=== AudioChannelMapping

TBD

=== AudioChannel

TBD

=== MCATagSymbol

TBD

=== UCSEncoding

TBD

=== NamespaceURI

TBD

=== Signer

The Signer element shall uniquely identify the entity that digitally signed the Delivery Specification List. If the Signer element is present, then the Signature element shall also be present.

If X.509 certificates are used as specified in [XML Digital Signature], then the Signer element shall contain one X509Data element containing one X509IssuerSerial element, which uniquely identifies the certificate used to sign the Delivery Specification List.

=== Signature

The Signature element shall contain a digital signature authenticating the Delivery Specification List.
If the Signature element is present, then the Signer element shall be present.
The digital signature shall be enveloped, as specified in [XML Digital Signature], and apply to the entire Delivery Specification List. The signature is generated by the signer, as identified by the Signer element.

= Annex A Bibliography (Informative)

TBD

= Annex B Consolidated Schema (Informative)

This specification is accompanied by the following element, which is an XML schema document as specified in [XML Schema Part 1: Structures].

imf-cpl-20160411.xsd

This element collects the XML schema definitions defined in this specification. It is informative and, in case of conflict, this specification takes precedence.

= Annex D Considerations for Applications (Informative)

TBD

= Annex E Sample Instance (Informative)

This specification is accompanied by the following element, which is an XML document that contains a sample instance of the DeliverySpecificationList element.

**Sample**

https://github.com/imfug/delivery-schema/blob/master/examples/Netflix/DRAFT_Netflix_OriginalsSpec_3.0_UHD_4K_SDR.xml

This element is for illustration only, and is neither intended to capture current or future practice, nor exercise all normative language contained in this specification.



