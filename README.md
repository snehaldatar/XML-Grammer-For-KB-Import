# XML-Grammer-For-KB-Import

Knowledge management system should be a single source of truth for your customers, customer services agents, partners, and most of the enterprise. Unfortunately, most of the business use wide variety of knowledge sources and during implementing or onboarding new line of businesses in eGain wants to migrate the content into eGain. Contents are stored in text, html, word, PDF or XML formats in these systems. eGain has built tools to import the content from various sources to ease the burden for its customers. However it is not realistic to import the content for every available source, customers can export the content from their existing content sources in the schema published at eGain Github library. Once content is exported in the XML format, you can create requests to import the content via eGain Technical Support X times in a quarter. 

# Prerequisites

1. Target department in which object needs to be imported should already exists.
2. All the languages. macros, customattributes must be present in the Target System else the Import may not be successful.
3. Import only supports languages that are present in eGain system, check Article.XSD for the list of supported languages in eGain.
4. KB author used for import should have 'Edit Folder' permission on all the existing eGain folders in target environment in which article needs to be created.
5. In article XML if any version has expiry date then it should be of some future date.
6. In article XML if any version has availability date then it should be of some future date.
7. The target eGain version supported are V17 and above.
8. Create date and last modified date for all entities will not be imported in Target system. Dates would be generated by target system based on current date.
9. Topic and folder XMLs are not mandatory and may not be present if the topic and folder paths (folder path of egainArticlePath element) mentioned in article XML already exists in target environment.


NOTE : Import will only create topics, folders and articles, Import tool doesn't support modification of topics, folders or articles.


## Sample Files

This Sample in sample folder includes XSDs and a zip file which has the xmls in required hierarchy.

 XSDs -  Topic.xsd, Folder.xsd,  Article.xsd
 Sample zip with xmls - eGain_Import_Sample.zip
 

# XML Grammar

## Topic XSD
|Name | Description | Type | Mandatory
|-----|-------------|------|-------|
|id |Topic |Id |String |Yes 
|egainTopicPath |eGain Topic Path will be path to eGain Topic with all parent topics. This will slways start with "\Topics".
egainTopicPath :      " \Topics\Policy\Leaves:Paid leave"	|String |Yes 
|exportedTopicLangDataList |Language specific Topic Data. |ExportedTopicLangData |Yes
|translate |Field to convey whether this topic is translatable |Allowed values are :    0 - No translation, 1 - Do translate |int |No

### ExportedTopicLangData
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |Name of the topic |String |Yes 
|description |Description of the topic |String |No
|language	|Language code. Please refer appendix for details. |String |Yes
|imageUrl |Image Url of the requested topic | String | No


## Folder XSD
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|id |Folder |ID |String |Yes
|egainFolderPath |eGain Folder Path will be path to eGain Folder with all parent folders. egainFolderPath: "\Content\Shared\Texting#bSlash#SMS-MMS\Agent Calling" | String | Yes
|exportedFolderLangDataList	|Language specific Folder Data |ExportedFolderLangData| Yes
|translate |Specifies, whether, the articles in this folder to be considered for translation when the content is exported for translation. Allowed values are :  0 - No translation, 1 - Do translate| int| No

### ExportedFolderLangData
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |Name of the folder |String | Yes
|description |Description of the folder| String| No
|language |Language code. Please refer appendix for details |String| Yes

## Article XSD
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|id |This is unique ID of article. If content is exported from eGain environment then this ID can be of the source eGain object and in case exported XML files are created from HTML, PDF etc. then this ID should be programmatically generated and mentioned in ID element of object XML files. |String |	Yes
|egainArticlePath |eGain Article Path will be path to eGain Folder that contains article and article name. egainFolderPath:     "\Content\Shared\Texting#fSlash#SMS-MMS\Agent Calling" egainArticlePath:  "\Content\Shared\Texting#fSlash#SMS-MMS\Agent Calling\Leaves:Paid leave" | String	Yes
| macro | This field denotes if this article can be used as a macro. If this element is present, it must have its 'name' element. Other elements of macro are optional.| Macro|	No
|langDataList |List of all languages and language specific versions. |LangData |Yes
| notes | List of notes attached to the article. If this element is present then it must contain atleast one 'Note' element and this 'Note' element must have the 'content' attribute. |Note | No
|relatedQuestions |Related Questins of the Article. |String |No
|egainTopicPathList | List of topics where the article is added. egainTopicPath: "\Topics\Policy\Leaves#col#Paid leave". |String |No
|createdDate |Creation date and time. |String |No
|lastModifiedDate |Last modification date and time.	|String |No
|createdBy |Name of user who created Article. (this would be eGain user name) |String |No
|lastModifiedBy| Name of user who modified the Article last. (this would be eGain user name) | String | No
|customAttributeList |List of custom attributes of Article.	|CustomAttribute |No
|relatedArticles |List of articles related to this article. e.g. "\Content\Shared\Texting#fSlash#SMS-MMS\Agent Calling\Leaves:Paid leave"| String| No
|linkAlias |UUID of article	|String |No

### Macro

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |Name of the macro |String | Yes
|description |Description of the macro |String |No
|defaultArticle |Default article with the macro |String |No
|defaultValue |Default value of macro |String |No

### Lang Data

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|language | Language code. Please refer appendix for details. |String |Yes
|versionDataList |Details of all the  versions of Article for this language. |VersionData |Yes

#### Version Data

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |name of the the version |String |Yes
|versionNumber |Version number of the version |String |Yes
|createdDate |created date of the version |String |No
|lastModifiedDate| Last modification date of the version| String |No
|label |Label of the article version. (This is message entered by author while publishing a version) |String |No
|description |Description of the version| String| No
|keywords |article keywords |String |No
|summary |article summary |String |No
|additionInfo |Addition info of the version |String |No
|content |Content of the version |String |No
|availabilityDate|	Availability date of version |String |No
|expirationDate |Expiration date of the version |String |No
|imageUrl |ImageUrl of the version |String |No
|attachmentList |Attachments with the version |Attachment |No
|articleType |Article type , by default 'General' |String |No
|createdBy |Name of user who created Article. (this would be eGain user name) |String |No
|lastModifiedBy |Name of user who modified the Article last. (this would be eGain user name) |String |No
|linkedAliases |List of linkAliases of articles to which the present article has links within its content |String |No
|containsLinks |Boolean indicating whether content of version contains links to other eGain articles |boolean |Yes


### Note

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|content |Text of the note, should be of CDATA type |String |Yes
|createdBy |Name of user who created Note. (this would be eGain user name) |String |No
|createdDate | Creation date and time. |String |No


### Custom Attributes

|Attribute | Description | Type|Mandatory
|---------------|-------------|------|-------|
|name |Name of custom Attribute |String |Yes
|type |Type of custom attribute |String |Yes
|value| Value of Custom Attribute. |String |Yes
