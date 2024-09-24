Original Email from Asieh for context: 

Friends:
 
Thanks so much again for agreeing to participate in this work and run the test script. With it, we want to establish the readiness of each data partner to run cancer studies as per our use case list. For that, we want to find out what cancer-related concepts are recorded in the data, and whether they follow the rules and conventions:
 
•	Whether source concepts are correctly mapped to standard concepts, and if at all.
•	Whether non-standard concepts reside in the source_concept_id fields, while the concept_id fields only contain standard concepts
•	Concepts from which vocabularies are used, and whether they follow the conventions (e.g. genomic data in OMOP Genomic).
•	Whether concepts are used according to their domain, e.g. if information about topology and histology represented in the Condition and those about metastases in the Measurement domain/table.
•	Counts of concepts to give a general idea to the size and depth of the database.
 
We are NOT testing any patient-specific information: their demographic and how the above concepts relate to individual patients. We also don’t query non-cancer concepts of any kind.
 
You can find 3 scripts testing data records for in Oncology Data Readiness Assessment folder in Teams. 
 
1.	general.sql: Script for general cancer concepts. These are any concepts, standard or non-standard, which have to do with the diagnosis, treatment, or other management of cancer patients. The script will test for 280k such concepts.
2.	genomic.sql: Genomic concepts. These cover any variant: small (usually SNPs), large (e.g. fusion proteins), on the DNA, RNA and protein level. The script tests for 590k such concepts.
3.	episode.sql: Episode concepts. These queries check the usage of Episode concepts (disease and treatment episodes = regimens). The script will test for 8,000 concepts.
 
Each query will create a list of source-standard concept pairs, the table they were found in (out of CONDITION_OCCURRENCE, DRUG_EXPOSURE, DEVICE_EXPOSURE, OBSERVATION, MEASUREMENT including value_as_concept_id, PROCEDURE and, only in the Episode query, EPISODE) and their total counts (again, without any relation to patients). The output format is a table with the columns domain, source_concept_id, standard_concept_id and cnt. 
 
Execution
 
Each of you should run the “generic.sql” query, checking the tables for general cancer-related concepts. If you have genomic data, you should run the “genomic.sql” query. If you have built an EPISODE table, you should run the “episode.sql” query. You can run them through either one of the following:
 
•	The SQL client you are using to access your data: DBeaver, Toad, SQL Workbench, SQL Developer or any other. Load the script, set the default schema to where the data resides and execute the script. 
•	R wrapper. Place it in the same directory as the *.sql files and edit the parameters at the top: set sqlFile (“general.sql”, “genomic.sql” or "episode.sql"), the schema name and the connection string:

connectionDetails <- DatabaseConnector::createConnectionDetails(dbms = " yourDBMS",
                                                                server="yourServer",
                                                                user="yourUsername",
                                                                port = " yourPort",
                                                                password="yourPassword",
                                                                pathToDriver = "JDBC/")

and execute the script. The script uses DatabaseConnector to connect to your database. If you need help with installing this package or want help running it using DBI or other databased interfaces, please let us know. Run the script for episode.sql ONLY IF you have an EPISODE table built in. The R wrapper is also available at the Oncology Data Readiness Assessment folder in Teams. 
•	Python wrapper. We are still testing the python wrapper. We will upload it to the same folder in Team and send an email with instructions on Monday. 

This is the timeline. 

	Timeline
Develop cancer specific concept prevalence query	Sunday, Sep 21
Execute the query and share the results	Friday, Oct 4
Aggregate results 	Monday, October 14
Develop high level summary 	Friday, October 18
Review the results together at the workshop 	Thursday, October 24
Develop and publish the list of impediments and solutions 	Friday, November 8

Please let us know if you have any questions or need help. 

We will start putting together a template for results overview to review in one of our upcoming meetings. 

Looking forward to working together on this! 
Asieh and the team

