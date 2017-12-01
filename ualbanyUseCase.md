# Draft PCDM Model Use Case for UAlbany

UAlbany wants to pull WARCs and metadata from Archive-It APIs for ingest into both ArchivesSpace and a Fedora Commons Repository.


## Use case 1
* User searches archival description
* User finds relevant web archives record
	* URL captured in some crawl, may or may not be seed
* User clicks find more details about web archives record
* User learns about crawl context and provenance
	* When crawl was made
	* What seed was used
	* Result of crawl
	* Any rules that limit crawl scope
	* Schedule or recurrence if applicable
	* Size of crawl in data and documents
* User clicks link to wayback instance of capture

## Use case 2
* User searches web archives
* User finds relevant web archives record
* User learns context from related archival description displayed around record
* User learns about crawl context and provenance
* User clicks link to wayback instance of capture



## A Proposed Workflow

### WARC Level

* Get date of last run from log or config
* Get new crawls from Archive-It Partner Data API
* Download WARC from WASAPI Data Transfer API
* Post WARC record to Repository
	* technical data from Partner Data API
	* WARC file itself
	* maybe derivatives 


### Archival Description Level

* Get existing web archives records from ArchivesSpace API
	* URL that might be seed, or any URL captured in any crawl
* Get hashes of existing records
	* Currently in ASpace but preferably from Repository API
* Get new capture instances from CDX
	* Compare hashes with CDX
* Get metadata from CDX
	* timestamp
	* WARC filename
	* hash
	* Archive-It collection ID number
* Get archived web page from Wayback with URL and timestamp
	* Parse with Beautiful soup to get title and any data in meta tags
* Put new archival description record into ArchivesSpace
	* Title
	* Date of capture
* Get ArchivesSpace ref_id for new record
* Get Warc file record from Repository API
* Post ArchivesSpace ref_id to Warc Record


## Examples

This what the [current script](https://github.com/UAlbanyArchives/describingWebArchives) does:

* [http://meg.library.albany.edu:8080/archive/view?docId=apap043.xml#d287c6d710066258fd65e31283b1df74](http://meg.library.albany.edu:8080/archive/view?docId=apap043.xml#d287c6d710066258fd65e31283b1df74)
* [http://meg.library.albany.edu:8080/archive/view?docId=apap331.xml#8ec7709c37dbca6e0053cb48282ed471](http://meg.library.albany.edu:8080/archive/view?docId=apap331.xml#8ec7709c37dbca6e0053cb48282ed471)
* [http://meg.library.albany.edu:8080/archive/view?docId=ua450.xml#4263b8cbb12b599b5adfdaa424b597ec](http://meg.library.albany.edu:8080/archive/view?docId=ua450.xml#4263b8cbb12b599b5adfdaa424b597ec)
* [http://meg.library.albany.edu:8080/archive/view?docId=ua500.xml;query=;brand=default#a1dd2018d29a6782fc89f5a94bd261f5](http://meg.library.albany.edu:8080/archive/view?docId=ua500.xml;query=;brand=default#a1dd2018d29a6782fc89f5a94bd261f5)
* [http://http://meg.library.albany.edu:8080/archive/view?docId=ua500.xml;query=;brand=default#56b1e5c161ad0d9dc3531277b857b58d](http://http://meg.library.albany.edu:8080/archive/view?docId=ua500.xml;query=;brand=default#56b1e5c161ad0d9dc3531277b857b58d)



