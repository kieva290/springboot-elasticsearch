# springboot-elasticsearch
Springboot elasticsearch project

lets add some notes:

Elasticsearch is an open search, free, distributed and analytics engine for all types of data, including textual, numerical, geospatial,
structured, and unstructured.
It is built on Apache Lucene

Tools and Concepts used in this tutorial:
- Spring Boot 3.0.5
- Spring Boot Starter Data Easticsearch 2.7.1
- Elasticsearch 8.3.2
- Maven
- Java 13

steps to install Elasticsearch on MACOS:
-----
step 1: "curl -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.7.0-darwin-x86_64.tar.gz"
step 2: "curl https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.7.0-darwin-x86_64.tar.gz.sha512 | shasum -a 512 -c -" 
step 3: "tar -xzf elasticsearch-8.7.0-darwin-x86_64.tar.gz"
step 4: "cd elasticsearch-8.7.0/"

run the following command to start Elasticsearch from the command line:
go to the root folder where elasticsearch has been instaled on the machine, and run the below command,
"./bin/elasticsearch"
to stop elasticsearch, press "Ctrl + C"

url to view elastisearch locally:
"http://localhost:9200/"
-----
explanation for class "ElasticSearchConfiguration":
- @Configuration: indicates that the class can be used by the Spring IoC container as a source of bean definitions i.e. it contains methods
  tag with @Bean, which return the object
- @Bean: tell Spring that a method annotated with @Bean will return an object that should be registered as a bean in the Spring application context
- getRestClient(...){}: this method used to configure the URL and port on which Elasticsearch is running
- getElasticsearchTransport(...){}: it returns the Transport Object, whose purpose is to automatically ma p the Model class to JSON and integrates them with API client
- getElasticsearchClient(...){}: it returns a bean of elasticsearchclient, which we further use to perform all query operations with Elasticsearch

explanation model class "Product":
model class Product will represent the document structure in Elasticsearch which contains the mentioned fields,
so whenever ny document is created in index named "products", then it will have the 4-felds information
- @Document - to specify the index, in this case "products"
- @Id - use to represent the field _id of document and it is unique for each message
- @Field - it represents a different typ of field that might be in our data 

explanation for class "ElasticSearchQuery":
- createOrUpdateDocument(): if indexdoes not exist in Elasticsearch, then it will create automatically and insert the document into it.
and if the document already present in that index then it will update the fields value under it.
- getDocumentById(): used to fetch the document based on id.
- deleteDocumentById(): to delete the document based on id.
- searchAllDocuments(): return all the documents present in that index. 

explanation for class "ElasticSearchController":
- @PostMapping("/createOrUpdateDocument"): create or update the document
- @GetMapping("/getDocument"): to fetch the document from index
- @DeleteMapping("/deleteDocument"): use to delete the document
- @GetMapping("/searchDocument"): return list of the documents present in the index

Note: you can easily "create/read/update/delete" the document present in Elasticsearch using POSTMAN.

explanation UI Controller Class "UIController":
- @GetMapping("/"): it will return the homepage of the application
- @PotMapping("/saveProduct"): use to create the product Document in the index
- @GetMapping("/showFormForUpdate/{id}"): it will show the page to update the existing document
- @GetMapping("/showNewProductForm"): to create a new document which contains prodict details
- @GetMApping("/deleteProduct/{id}"): to delete the existing document of product based on ID

Note: we used "@Controller annotation", never use "@RestController" in this class,
since @RestController annotation internally also have @ResponseBody annotation which automatically convert/serialize the response into JSON,
which we don't want since in this class we are trying to achieve MVC and need to return html page 

Please make sure your Elasticsearch is UP and running on your system, 
once you run, the home page will be hosted locally and you can reference it via the local browser.