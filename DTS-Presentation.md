<style>
pre { font-size: 14px!important; margin:-5PX; padding:5px; }
</style>
<!-- Build to PDF using Marp -->

Distributed Text Services 
========

A presentation for the Pelagios Text Reuse Working Group

---

# Plan

- (Really) Quick history
- Objectives
- Team
- Principles
- Current status
- Implementations

---

# (Really) Quick history

- Started in a workshop about Canonical Text Services (CTS) future in 2015
- Alternative to CTS to fit more needs, more technical realities. 
- Ups and downs, real speed up over the last academic year

---

# Objectives

- Open group for contributions, not a one-person project
- Scalable API : does well for 10 texts as much as 1M
- Linked Open Data
	- no access barrier
	- controlled vocabularies
- Identifier agnostic
- CTS retro compatible
- Focused on serving and retrieval for the first lot 
	- Search might come later ?
- URI scheme should be flexible (not everybody can have reroute)
- No catalogue hierarchy should be forced upon implementers
	- Freedom of catalogue architecture (details, depth, etc.)

----

# Team

- Bridget Almas 
- Hugh Cayless
- Thibault Clérice
- Jeffrey C. Witt
- Vincent Jolivet
- Pietro Luzzo 
- Emmanuelle Morlock
- Jonathan Robie
- Matteo Romanello
- James Tauber
- and the list goes on and I probably forgot people here.

Core of 4 to 5 peoples meeting every two weeks for the past year.
Latinists and hellenists but  other periods and languages as well

----

# Principles

Three main functions turned into endpoint :
- Collection browsing (*Collection Endpoint*)
  - JSON-LD, Hydra-based answers, DC as core metadata vocabulary
  - Restful
- Navigation Endpoint
	- JSON (*endpoint to be in discussion soon*)
- Document Endpoint
	- XML-TEI

----

# Principles (2)

- Endpoints do not need to be all available.
- Endpoints should be usable without the need to browse from the top down
	- I know you have this text, please just give me its available pages.
	- I know your Victor Hugo's Misérables has paragraph 5 from chapter 3. Give it to me.
- Freedom of other output type for the document endpoints (you can allow people to get plain text). But you **have to** serve TEI XML.


----


# Collection Endpoint

```json
{
    "@context": {
        "@vocab": "https://www.w3.org/ns/hydra/core#",
        "dc": "http://purl.org/dc/terms/",
        "dts": "https://w3id.org/dts/api#"
    },
    "@id": "general",
    "@type": "Collection",
    "totalItems": "2",
    "title": "Collection Générale de l'École Nationale des Chartes",
    "dts:dublincore": {
        "dc:publisher": ["École Nationale des Chartes", "https://viaf.org/viaf/167874585"],
        "dc:title": [
            {"fr" : "Collection Générale de l'École Nationale des Chartes"}
        ]
    },
    "member": [
        {
             "@id" : "cartulaires",
             "title" : "Cartulaires",
             "description": "Collection de cartulaires d'Île-de-France et de ses environs",
             "@type" : "Collection",
             "totalItems" : "10"
        },
        {
             "@id" : "lasciva_roma",
             "title" : "Lasciva Roma",
             "description": "Collection of primary sources of interest in [...]",
             "@type" : "Collection",
             "totalItems" : "1"
        },
        {
             "@id" : "lettres_de_poilus",
             "title" : "Correspondance des poilus",
             "description": "Collection de lettres de poilus entre 1917 et 1918",
             "@type" : "Collection",
             "totalItems" : "10000"
        }
    ]
}
```
----

# Navigation endpoint

**Warning:** definitely a draft, not discussed in depth
```json
{
    "@context": {
        "passage": "https://w3id.org/dts/api#/#passage"
    },
    "@base": "/dts/api/document/",
    "@id":"urn:cts:greekLit:tlg0012.tlg001.opp-grc5",
    "passage": ["1", "2", "3"]
}
```
---

# Document Endpoint


```xml
<?xml version="1.0" encoding="UTF-8"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0">
   <teiHeader>
      <fileDesc>
         <titleStmt>
            <title>bgu.11.2029</title>
         </titleStmt>
         <publicationStmt>
            <authority>Duke Collaboratory for Classics Computing (DC3)</authority>
            <idno type="filename">bgu.11.2029</idno>
            <idno type="ddb-perseus-style">0001;11;2029</idno>
            <idno type="ddb-hybrid">bgu;11;2029</idno>
            <idno type="HGV">9566</idno>
            <idno type="TM">9566</idno>
            <availability>
               <p>© Duke Databank of Documentary Papyri. This work is licensed under a 
               <ref type="license" target="http://creativecommons.org/licenses/by/3.0/">Creative 
               Commons Attribution 3.0 License</ref>.</p>
            </availability>
         </publicationStmt>
      </fileDesc>
   </teiHeader>
   <dts:fragment xmlns:dts="https://w3id.org/dts/api#">
    <lb n="1"/><expan>τετελ<ex>ώνηται</ex></expan> 
    <expan>δι<ex>ὰ</ex></expan> <expan>πύλ<ex>ης</ex></expan> Διονυσιάδος 
   </dts:fragment>
</TEI>
```

---

# Current status

- Collection endpoint (= catalogue browsing) is close to a good first draft. Some discussion remaining, mostly due to first implementation giving us feedback on this.
- Navigation endpoint to be the next one to be looked at, should be shorted than collection (hopefully)
- Document API already discussed a lot, not finalized

---

# Implementations

- *SCTA* by Jeffrey C Witt
- *Beta maṣāḥǝft* by Pietro Luzzo
- *Capitains* 
	- web client, (Python)
	- web server, (Python)
	- local client, (Python, hopefully JS ?) 
	- guidelines to encode for the server part (TEI + *proprietary* metadata scheme)

---

# Thanks
*If I forgot something, we have more than 3 members of DTS here, maybe they'd like to add something ?*
