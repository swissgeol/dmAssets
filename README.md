# dmAsset
Datenmodell Asset zur Beschreibung der Metadaten von geologischen Assets

Asset = Medium, Dokument 

Das Modell setzt sich aus zwei Teilmodellen zusammen mit jeweils einem Modell und einem Katalog mit den Attributlistenwerten. GeolAsset und LG_GeolAsset beschreiben die Modelle. Eine Graphik des uml-Schemas bildet die Verhältnisse bildlich ab und ist abgelegt als ***cd_LG_GeolAssets_V1.jpg*** im Ordner `doc`.   

### Modell GeolAsset: 

Das Topic Kernmodell (*CoreGeolAsset*) besteht aus den Klassen `AssetBase`, `AssetItem`, `AssetPackage`, `GeometryOfInterest`, `Contact` und den Geometrieklassen `StudyLocation`, `StudyTrace`, `StudyArea`. Die Strukturen `ID`, `Adress` und die Domänen `Line` und `Surface` werden zur Vordefintion benötigt. 

`AssetBase` bildet die Basisklasse der Metadaten mit den Erweiterungen `AssetItem` und `AssetPackage`. AssetBase allein beschreibt die minimalen Angaben eines Assets und enthält den öffentlichen Titel ohne sensible Daten. 

`AssetItem` erweitert die Klasse AssetBase und ergänzt diese um Informationen zum Asset-Typ. Verschiedene Dokumentformen wie Bild- und Videomaterial, Feldaufnahmen und prozessierte Daten stehen zur Verfügung. Das Objekt wird mit einem geologischen Fachbereich in Verbindung gebracht und Format und Sprache werden beschrieben. Zudem können Informationen zu den Autoren und Textkörper aus OCR-Erkennung ergänzt werden. Sofern sich das Asset um ein `AssetItemMain` handelt, können andere `AssetItemParts` via der Art des Dokuments angehängt werden. Sollte das Asset nur Teil eines Assets sein, kann dies via Boolean "IsPart" gekennzeichnet werden. Die Assoziation `AssetItemMain_AssetItemPart` beschreibt diese Beziehung zwischen Hauptobjekt und Teilobjekt. Die Assoziation `AssetItemX_AssetItemY` dient zur Verbindung von Objekten der gleichen hierarchischen Stufe wie bspw. verschiedene Parts. 

`AssetPackage` kann keine bis mehrere AssetItems zu einem Paket schnüren. Die Assoziation beschreibt die Verbindung zwischen Objekt und Paket. 

`GeometryOfInterest` bildet eine Geometrieverknüpfung, bei welcher Punkt, Linien und Flächengeometrien gleichzeitig einem Objekt der Klasse AssetBase zugeordnet werden können. 

`Contact` umfasst die Information zur Art des Kontaktes, woher das AssetObject stammt. Minimalangabe dazu ist die Bewilligungsbehörde. Die Assoziationen `Author`, `Initiator` und `Supplier` trennen die Kontaktangabe  in Author, Rechte-Inhaber und Lieferant des Asset-Objekts auf. 



### Modell LG_GeolAsset
 
Das Topic LGGeolAsset versteht sich als Erweiterung des Kernmodells GeolAsset. Es ist um die Klassen `LGContact`, `LGAssetBase`, `LGAssetItem`, `LGAssetPackage` und `Publication` ergänzt. Die Klassen entsprechen mehrheitlich ihrem Pendant im Modell GeolAsset, weisen jedoch teils noch zusätzliche Attribute oder Klassenerweiterungen abgestimmt auf die Arbeiten der Landesgeologie auf. 

`LGAssetBase` beschreibt Restriktionseigenschaften des Objekts und Ablageinformationen sowohl im internen Server, als auch im Web. Weiter werden das Eingangsdatum des Objekts, rechtliche Unterlagen mittels der Struktur `LegalDoc` und die Einschätzung der nationalen Relevanz definiert. Verknüpfungen mit der swissgeol-DB, Gemeinde und weitere Bemerkungen können ergänzt werden. Die Benutzung des Objekts in verschiedenen Projekten wird in der Struktur `UsedBy` beschrieben. 

`LGAssetItem` enthält administrative Metadaten zum Objekt, darunter die swisstopo-interne ID, Informationen zur Texterkennung und Klasse von GAIA in einer separaten Struktur `OCRInfo` und den Lagerort des physischen Originals des Dokuments. Über die Assoziation `AssetItem_LGAssetItem` können die Assets, welche spezifisch in Projekten und Archiven der Landesgeologie vorkommen mit der Beschreibung von allgemeinen Asset-Objekten verknüpft werden. Analog vorliegende Objekte müssen zwingend einen physischen Lagerort vorweisen. Es können wiederum `LGAssetItemParts` verlinkt werden, müssen dann aber auch näher definiert werden in der Struktur `AssetPartInfo`. 

`LGAssetPackage` bildet ein Paket von Objekten. Hier sind noch LG-Projekt und Restriktionsinformationen zusätzlich angegeben. Durch die Assoziation `AssetPackage_LGAssetPackage` können Pakete verbunden werden. 

`Publication` beschreibt Zeitpunkt und Medienkanal der Veröffentlichung des Asset-Objekts. Publikationen können mit Asset-Objekten durch die Assoziation `LGAssetBase_Publication` verbunden werden. 


----


# dmAsset
Asset data model for describing the metadata of geological assets

Asset = medium, document 

The model is composed of two sub-models, each with a model and a catalogue containing the attribute list values. GeolAsset and LG_GeolAsset describe the models. A graphic of the uml scheme depicts the relationships pictorially and is stored as ***cd_LG_GeolAssets_V1.jpg*** in the `doc` folder.   

### GeolAsset model: 

  The Topic core model (*CoreGeolAsset*) consists of the classes `AssetBase`, `AssetItem`, `AssetPackage`, `GeometryOfInterest`, `Contact` and the geometry classes `StudyLocation`, `StudyTrace`, `StudyArea`. The structures `ID`, `Address` and the domains `Line` and `Surface` are required for predefinition. 

`AssetBase` forms the base class of the metadata with the extensions `AssetItem` and `AssetPackage`. AssetBase alone describes the minimal details of an asset and contains the public title without sensitive data. 

`AssetItem` extends the AssetBase class and adds information about the asset type. Different document forms such as image and video material, field recordings and processed data are available. The asset is associated with a geological subject area and the format and language are described. In addition, information on authors and text bodies from OCR recognition can be added. If the asset is an `AssetItemMain`, other `AssetItemParts` can be attached via the type of document. If the asset is only part of an asset, this can be marked via the Boolean "IsPart". The association `AssetItemMain_AssetItemPart` describes this relationship between main object and part object. The association `AssetItemX_AssetItemY` is used to connect objects of the same hierarchical level, such as different parts. 

`AssetPackage` can combine none to several AssetItems into a package. The association describes the connection between object and package. 

`GeometryOfInterest` forms a geometry link in which point, line and surface geometries can be assigned to an object of the AssetBase class at the same time. 

`Contact` includes the information about the type of contact where the AssetObject originates from. The minimum specification for this is the granting authority. The associations `Author`, `Initiator` and `Supplier` separate the contact information into Author, Rights Holder and Supplier of the AssetObject. 



### Model LG_GeolAsset

The topic LGGeolAsset is an extension of the core model GeolAsset. It is extended by the classes `LGContact`, `LGAssetBase`, `LGAssetItem`. `LGAssetPackage` and `Publication`. Most of the classes correspond to their counterpart in the GeolAsset model, but some have additional attributes or class extensions tailored to the work of the regional geology. 

`LGAssetBase` describes restriction properties of the object and storage information both in the internal server and on the web. Furthermore, the date of receipt of the object, legal documents by means of the `LegalDoc` structure and the assessment of national relevance are defined. Links with the swissgeol DB, municipality and other remarks can be added. The use of the object in various projects is described in the structure `UsedBy`. 

`LGAssetItem` contains administrative metadata on the object, including the swisstopo internal ID, information on text recognition and class of GAIA in a separate structure "OCRInfo" and the storage location of the physical original of the document. The association `AssetItem_LGAssetItem` can be used to link assets that occur specifically in projects and archives of the Swiss Geological Survey with the description of general asset objects. Analogous objects must necessarily have a physical storage location. In turn, `LGAssetItemParts` can be linked, but must then also be defined in more detail in the structure `AssetPartInfo`. 

`LGAssetPackage` forms a package of objects. Here, LG project and restriction information are additionally specified. Packages can be connected through the association `AssetPackage_LGAssetPackage`. 

`Publication` describes the time and media channel of the publication of the asset object. Publications can be linked to asset objects through the association `LGAssetBase_Publication`. 
