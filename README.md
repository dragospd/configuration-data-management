configuration-data-management
=============================

Running multiple software projects in a company usually leads to configuration data management troubles. How many times you missed an expensive deployment cycle due to an error in (one of) the configuration file(s)? A software company tipically maintains different deployment environments for different purposes like:

- Development
- Test
- Acceptance
- Stres test
- Production

Based on its purpose, each environment is configured different in terms of available resources so you will expect that each application maintains a list of configuration properties that are to be set with different values based on the target environment before the application is deployed. For example, your application will use a specific mail server in development to send emails and another one in production. Or, you might want to experiment different cache sizes in different environments. Or thread numbers. Or database connection pool settings. You name it. Some of the properties are read-only, others can be changed at runtime. Usually the places where applications are keeping the configuration data are subject of debate between developers. Some of them prefer the .properties files, others .xml's, others database tables and so on. There are some (usually complex) projects where you can encounter a mixture of all of this. Clear enought, there is no solution that fits all necessities, that's why some configuration frameworks popped out (like Apache common configuration) trying to unify the way developers access the configuration data. And that's good. What is missing out in the picture is a consistent way to manage the configuration data itself in a common continuous integration environment.

In large software organisations there are multiple roles supposed to do configuration data management, most of the time only partially. The range starts from the developers and goes to the infrastructure managers but covers also software architects and project managers. This ads a lot of complexity since there is no single person responsible for this task and moreover the persons are even in different organizational units within the same organisation. Take one example: due to a migration of one of the database production servers, the connection data related to one of the database server changed. The infrastructure manager will communicate the new data to each project team. In each team a person should be assigned to change the data wherever is necessary and create a new build than the build artefacts are moved into the target environment. The usual workflow based on manual interventions is slow and prone to errors. There are hundreds of configuration variables spreaded in multiple configuration files or even in databases. Combine this with multiple deployment environments and you will figure out why more that 90% of the initial deplyments fail during sanity tests due to a configuration issue. I've spend hours and days to figure out why a deployment failed and finally noticed that the destination queue parameter pointed to the test environment instead of the acceptance... And that happened due to a copy paste error. Not to mention that it was almost impossible to trace back the person responsible of doing the mistake. If people know that any configuration data change is traceable they will be far more carefull when they actually do it. It should be a way to compare old configurations with new configurations, to track the changes, to comment on them, to rollback the configuration to a previous version.

The idea of this project is to propose a consistent way to organize the configuration data and tools that can be used to automate the configuration data manipulation in a continuous integration environment. The following assertions are used to better describe the configuration data:
- is a resource produced and consumed by different entities within an organisation;
- it requires traceability - knowing what has been changed, when, who and why;
- it requires version management - with versions a configuration can be easily associated or integrated in a normal release management process;
- it requires security - configuration data can be shared or private;
- it requires easy automation - data should be stored in a standard format easy to be write and read by standard io libraries.
- it should be easily read and write manually - configuration data is something that you might want to change 

First question is how this resource can be organized to fulfill the requirements? I propose a federated composition of xml files. Basically any consumer can aggregate a "current" version of resource by building an XML 



Depending on the environment the
