
Please note: 

- glue2.xsd is the XSD schema
- glue2_SampleDoc1.xml is a sample doc that is valid against 'glue2.xsd' 
- glue2_SampleManyEndpoints.xml is a sample doc that is valid against 'glue2.xsd' 

- 'sampleGlue2_Extension.xsd' imports the GLUE2 XSD (glue2.xsd) 
  in order to derive custom sub-types that are NOT part of the GLUE2 spec. 
- 'sampleGlue2_ExtensionDoc.xml' needs to be validated against both 
  'glue2.xsd' and 'sampleGlue2_Extension.xsd' and it is NOT GLUE2 compliant! 
  (it merely demonstrates how custom sub-types can be derived and nested within 
  Glue without having to modify the base glue2.xsd schema - see Doc for details).

- To validate the xml docs, the XSDs need to be in the same folder (unless you 
 modify the xsd:schemaLocation attribute). You can use xmllint command line tool 
 to validate as follows (available for linux and via cygwin for win):   

  $xmllint --noout --schema glue2.xsd glue2_SampleDoc1.xml 
  glue2_SampleDoc1.xml validates
 
  $xmllint --noout --schema glue2.xsd glue2_SampleManyEndpoints.xml
  glue2_SampleManyEndpoints.xml validates

  $xmllint --noout --schema sampleGlue2_Extension.xsd sampleGlue2_ExtensionDoc.xml
  sampleGlue2_ExtensionDoc.xml validates



Some minor TODOs to look at 
===========================
- DataStore_t: TODO Should it also inherit ActivityID from Resource? p52 in conceptual spec
- StorageShare_t: TODO Should it also inherit ActivityID from Share? p 49 in conceptual spec
- StorageEndpoint_t: TODO Should it also inherit ActivityID from Endpoint? p 48 in conc spec
Clarification from S.Burke: 
These could all be redefined relations to a StorageActivity class, except that we (GLUE WG)
didn't define such a class. Perhaps it should have been defined with no attributes as we 
did for StorageManager, but at the moment we have no use for such an object so it was left out. 

- StorageService_t: TODO - Should this entity have a ToComputingService.ID association? 
  or is this intended to be a uni-directional association (since ToComputingService, 
  p52/53 has an association back to StorageService). 
Clarification from S.Burke: 
Intrinsically relations are always bi-directional, you can follow them either way, 
but in this case the relation is going to be published by the computing service 
and the storage service doesn't "know" which things are pointing to it



- ComputingService_t : TODO should this reference a ToStorageServiceID ? 
- ComputingActivity_t: TODO A ComputingActivity is managed by a UserDomain, but we specify DomainID to be generic - check this is ok. 
- ComputingService_t: TODO Should it contain a reference to a ToStorageServiceID (is labeled as StorageServiceID in conceptual spec, p24) 
- MappingPolicy_t : TODO should it specify UserDomainID instead of DomainID
- AccessPolicy_t :  TODO should it specify UserDomainID instead of DomainID
- Activity_t :  TODO should it specify UserDomainID instead of DomainID
- ManagerBase_t : TODO ProductName attribute type has been changed from string to ComputingManagerType_t (is this wrongly? labeled as string in conc spec). 
- Endpoint_t : TODO  Should it define AccessPolicyID instead of the more generic PolicyID in its associations. 
- AccessMode_t : TODO FIXME this isn't defined in GLUE2.0


