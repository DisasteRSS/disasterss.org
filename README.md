DisasteRSS
==============

## Purpose
DisasteRSS is a open, distributed standard for discovering and sharing disaster related content and data across the Internet.

## Overview
DisasteRSS is focused on creating simple and easy to implement standards to enable decentralized sharing of data similar to how RSS enabled decentralized sharing of site content and blog posts without dependencies on singular implementations or individual online services.

## Discovery (disasters.txt)
In order to support dynamic distributed discovery of references to links to content and drss feeds across the internet, DisasteRSS specifies the implementation of a disasters.txt file addressed under the root of a website (e.g. http://topix.com/disasters.txt).

Inspired by robots.txt, this allows any drss aware consumer to discover content and drss feeds that a given website may reference by checking for the existence of a disasters.txt file and then parsing its contents per the specification below.

### Sample disasters.txt file
	# example.com disasters.txt
	# updated 8/27/2013
	http://www.topix.com/hurricane/hurricane-sandy
	content http://www.example.com/webpage tag1,tag2,tag3,"tag 4"`
	feed http://www.example.com/drss


### disasters.txt specification (todo: formalize specification)
**resource name:** disasters.txt  
**location:** root url of web site (e.g. http://example.com/disasters.txt)  
**content-type:** text/plain  

**contents:**
text file containing zero or more lines in the following formats:

1. empty or whitespace only - ignored
2. *#* prefixed lines are comments - ignored
3. *[type]* *url* *[csv tags]* - parsed per below

*[type]* = *content* | *feed* (optional defaulting to content)

*content* denotes link to content that is human readable and viewable in a web browser (e.g. html or pdf formatted content)  

*feed* denotes link to drss feed formatted to drss feed specification

*url* = standard internet url (citation?) location for reference

*csv tags* = optional list of tags associated with the content in comma seperated format (citation for csv).  Example: big, small, round, square, "Chicago, IL", Illinois, Midwest

> This specification provides no guidance or restriction to the meaning or format of these tags and therefore supports open innovation in choosing tags and their formats and presumes that common patterns and practices for tagging will emerge accross implementations over time.

## Data feeds (DisasteRSS Sharing Specification)
DisasteRSS specifies a standardized data exchange format for the sharing of disaster related data between websites and applications on the Internet.

Inspired by rss, atom and other similar formats, the DisasteRSS Sharing Specification (DRSS) provides a format for the exchange of both the data itself and related metadata.
### Sample DRSS Data Feed
		<feed>
			<name></name>
			<link></link>

			<item>
				<id></id>
				<timestamp></timestamp>
				<geolocation></geolocation>
				<description></description>
				<entityref></entityref>
				<source id="" href="" record="" />
				<supercedes id="" />
			</item>
			...
		
		</feed>

### DRSS 0.1 Specification
#### What is DRSS
DRSS is a web format for the exchange of disaster related data and is a shortened version of DisasteRSS Sharing Specification.

DRSS can be expressed both as a dialect of XML and as JSON.  All RSS XML files must conform to the XML 1.0 specification as published on the World Wide Web Consortium (W3C) website. The current version of this specification, 1.0, only specifies the xml specification for DRSS.

At the top level, a DRSS document is a &lt;drss&gt; element with a mandatory attribute version that specifies the version of DRSS that the document conforms to.  For this specification, the version attribute must be 0.1.

Below the &lt;drss&gt; element is a single &lt;feed&gt; element which contains information about the metadata for the feed and its data items.
#### Required feed elements
The following are required elements below the *feed* element of DRSS.

**name:** (single) The name of the disaster data feed

**link:** (single) The url to a human readable website related to this data feed

**item:** (1 or more) individual data items shared via this feed

#### Optional feed elements
The following are optional elements below the *feed* element of DRSS specified by DRSS.

> Additional elements can also be included below the feed element provided they are scoped within an XML namespace outside of this specification.

### Elements of item
A feed contains one or more &lt;item&gt; element each representing a data item shared by the feed.  This specification prescribes no taxonomy, content type or ‘sizing’ guidance for the data represented by the item and therefore may represent any data item including (but not limited to) individual numerical data points, images or documents to broad aggregation of information.

The elements below are required to be present singularly for the item element of DRSS unless otherwise noted.

**id:**  string that uniquely identifies the item

**timestamp:** date formated in XXXX format indicating time metadata for the item

**geolocation:** (optional) location metadata for the data item (formats TBD but inclusive of Lat/Long as well as hierachy of government borders such as Country, State, County, City, ZipCode)

**type:** indication of disaster related data type for this item (choice of need, resource, hazard, other)

**description:** (optional) text summary of item

**entityref:** (optional) reference to entity representing this data item located at the url value of the “href” attribute.  No prescription is made for the content or format of the referenced entity.

**source:** indication of the authoritative source for this data item named by the “id” attribute and located at the “href” attribute url value.  Optionally contains a “record” attribute with a string representing a record identifier for this item at the source.  No prescription is made for the values of the id or record attributes nor the content or format of the referenced url of the href attribute.

**supercedes:** indication that this data element replaces and supercedes a previous data item provided by this feed with the *id* of the value of the “id” attribute of this <supercedes> element.

>  Additional elements can also be included below the item element provided they are scoped within an XML namespace outside of this specification.



