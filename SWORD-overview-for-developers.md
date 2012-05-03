DataStage and SWORD
-------------------

This section describes the protocol operations which DataStage employs to speak to a SWORDv2 server.

Outline
-------

DataStage uses a very limited set of operations to speak to the SWORD server:

1. It queries for Service Documents (GET on SD-IRI, spec section 6.1)
2. It creates items in the repository with only an Atom Entry (POST Entry
to Col-IRI, spec section 6.3.3)
3. It queries for Atom Entry Documents (GET on Edit-IRI)
4. It Updates items in the repository by sending the zipped content as a
package (PUT Package to EM-IRI, spec section 6.5.1)
5. It regularly checks the status of items it has deposited in the repository, monitoring for errors, by retrieving the Statement (GET on State-IRI, spec section 11)


Service Documents
-----------------

GET on SD-IRI

DataStage obtains a list of collections into which the user can deposit by requesting the Service Document from the SWORDv2 server.  Once a collection is selected, then DataStage can go on and carry out its deposit.

The Service Document is requested from the server with the user credentials supplied by the DataStage user, and no On-Behalf-Of header is added.

If the retrieval is unsuccessful, DataStage presents the user with an error message, and the deposit cannot proceed.


Creating an item in the repository
----------------------------------

POST Atom Entry to Col-IRI
Content-Type: application/atom+xml;type=entry
Slug: [dataset identifier]

Once a collection has been selected from the Service Document, DataStage carries out a synchronous deposit operation by POSTing to the Col-IRI selected an Atom Entry Document which contains the basic dataset metadata: title and description, as provided by the user interface.

When the deposit takes place, the Slug header is set with the dataset's unique identifier, which DataStage expects (although does not require) the repository to respect.

The deposit is carried out with the user credentials supplied by the DataStage user, and no On-Behalf-Of header is added.

If the deposit is unsuccessful, the user is presented immediately with an error message.

If the deposit is successful, DataStage will disregard the deposit receipt and store the Edit-IRI from the Location header against the dataset for future use.  The dataset is then added to the content deposit queue, to be processed asynchronously (see below)


Obtaining the Entry Document
----------------------------

GET on Edit-IRI

Before DataStage can go ahead and deposit the package to the repository, it needs to obtain the EM-IRI, which can be obtained from the Atom Entry Document, which can be obtained by performing a GET on the Edit-IRI it stored after creating the item initially.

The retrieval is carried out with the user credentials supplied by the DataStage user, and no On-Behalf-Of header is added.

If the retrieval is unsuccessful, several re-try attempts are made before the deposit is marked as having failed (see the section below on the full deposit for more details).

If the retrieval is successful then the EM-IRI is extracted from the Entry Document and the package deposit can proceed.


Depositing the content package
------------------------------

PUT Package to EM-IRI
Packaging: http://dataflow.ox.ac.uk/package/DataBankBagIt
Content-Type: application/zip

When the deposit request reaches the front of the deposit queue, the content will be packaged up and delivered to the repository.  At first the Entry Document is retrieved with a GET on the Edit-IRI (see above), and the EM-IRI is obtained.

The content of the dataset is then packaged in the DataBankBagIt format and PUT to the EM-IRI with the appropriate Packaging the Content-Type headers.

The deposit is carried out with the user credentials supplied by the DataStage user, and no On-Behalf-Of header is added.

If the deposit is unsuccessful, it is re-tried a number of times and if still unsuccessful the deposit is marked with an error, and skipped over.  It may then be re-tried again some time in the future.

If the deposit is successful, the status of the item is updated to indicate success.


Checking items in the repository
--------------------------------

GET on State-IRI
Accept: application/rdf+xml

DataStage assumes that because it is delivering large files to the server that there may be asynchronous processes running there which could result in errors arising at some point further down the line.  It therefore regularly checks up on the items it has deposited to monitor their state.

In order to check the state it first does a GET on the Edit-IRI (see above), to obtain the State-IRI from the retrieved Entry Document.  Then DataStage issues a GET on the State-IRI for an ORE formatted Statement document.

DataStage will examine the sword:state element of the Statement document and look for pre-determined error URIs.

If an error URI is found the dataset is put back onto the queue for further attempts at deposit.



DataBank and SWORD
------------------

This section describes the protocol operations which DataBank supports for use by a SWORDv2 client.

Outline
-------

DataBank provides a very limited set of operations from the SWORDv2 specification:

1. It supplies Service Documents (GET on SD-IRI, spec section 6.1)
2. It receives Atom Entry Documents in create requests and creates new datasets from them (POST Entry to Col-IRI, spec section 6.3.3)
3. It supplies Atom Entry Documents for items in the archive (GET on Edit-IRI)
4. It receives zip files and adds them to the item in the archive (PUT Package to EM-IRI, spec section 6.5.1)
5. It supplies ORE formatted Statements (GET on State-IRI, spec section 11)

Service Document
----------------

GET on SD-IRI

DataBank provides a Service Document with one Workspace which contains a single Collection per Silo.  Each Collection will accept any Content-Type, and will accept one of two package formats:

    http://purl.org/net/sword/package/Binary
    http://dataflow.ox.ac.uk/package/DataBankBagIt

DataBank does not support mediated deposit, so the mediation element for each Collection will be false.

The list of Silos provided on request will be those which the authenticating user has permission to create Datasets in.


Creating an item in the repository
----------------------------------

POST Atom Entry to Col-IRI
Content-Type: application/atom+xml;type=entry
Slug: [dataset identifier]

DataBank will only accept create requests with Atom Entry Documents, and not packaged content.  Upon receipt of such a request, a new Dataset will be created in the Silo, and the metadata embedded in the Atom Entry (title and description) will be placed into the manifest.

The depositing user must have the appropriate authorisations to create items in the Silo for this operation to be successful.


Obtaining the Entry Document
----------------------------

GET on Edit-IRI

DataBank can provide Entry Documents on request to the Edit-IRI of a Dataset.

The retrieving user must have the appropriate authorisations to retrieve the item from DataBank.


Depositing the content package
------------------------------

PUT Package to EM-IRI
Packaging: http://dataflow.ox.ac.uk/package/DataBankBagIt
Content-Type: application/zip

DataStage will receive packaged content in the DataBankBagIt format.  Upon receipt of a package a new version of the Dataset will be created, preserving all the metadata but none of the previous files contained therein.  The new package will then be added to the Dataset.

The package is not unpacked at deposit time; instead the Dataset is added to a queue, and the package will be unpacked at a later time.

If the unpacking process fails, the item will have a sword:status set to an appropriate Error URI; the client is responsible for checking the status of the item regularly to monitor for errors.


Checking items in the repository
--------------------------------

GET on State-IRI
Accept: application/rdf+xml

DataBank makes Statement documents available in ORE format only.  The sword:state element contains information about the state of the item.  When a Dataset is first created, the state will be:

    http://databank.ox.ac.uk/state/EmptyContainer
    
Once a package has been added, the state will become:

    http://databank.ox.ac.uk/state/ZipFileAdded

If there is an error unpacking the Zip, the state will be set to an appropriate Error URI.




Some useful SWORDv2 resources
-----------------------------

Code libraries providing client and server environments: http://github.com/swordapp

The SWORDv2 Specification: http://swordapp.github.com/SWORDv2-Profile/SWORDProfile.html

A DSpace fork with a stabilised SWORDv2 webapp (use this branch, not the master): https://github.com/nye-duo/DSpace/tree/duo