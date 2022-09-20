# AnnotationCompiler
Compiles book annotations from various sources into one location

Infrastructure

Overview: The infrastructure that supports this project is based on Azure Services. Two viruatl networks were created. One to hold the Virtual Machine used to develop the project code and the other was created to house the postgres azure database. They were not hosted on the same network as the postgres database instance does not support IpV6 connection which is what I needed to use to connect to the virtual machine. As this is a learning project with a focus on getting familiar with the Azure environment and improving my coding skills I chose to implement a environment that would support my aims without getting to bogged down in areas that were not the focus. In later iterations as I progress in the project and continue to improve my skill base I hope to containerize everything to increase efficiency.

Setup: Resource Group 1 (RG-PostAnnotation)
        - Network security group
        - Azure Database for PostgreSQL flexible server
        - Private DNS zone
        - Public IP Address (IPv4)
        - Storage account
        - Virtual Network
       Resource Group 2 (RG-VMProAnnotation)
        - Network security group
        - Public IP Address (IPv4 & IPv6)
        - Storage account
        - Virtual machine
        - Network Interface
        - Disk
        - Virtual Network
        
Data: The annotation data will be stored in three tables housed in the postgres instance: Annotations, Books, Publishers

Postgres schema:
      Annotations (Columns): UniqueID, Book Uniqe ID, Page No., Annotations, Date
      Books (Columns): Book Unique ID, Title, Author, Publisher ID
      Publishers (Columns): Publisher Unique ID, Publishing house location
      
Data aggregation: Annotations will either be uploaded individually by the application user with the option to upload a google sheet, kindle file, or csv file. Or, the user will select a folder (in google drive?) or a book in the kindle app(?) that will be checked when a event is triggered (new save date, file is closed, etc?) for updates. If new updates are found the annotation file will then be converted to a csv file and run against a data quality control to ensure the data clean before storying it in the database.

Application: 
    - Language: C#
    - Framework: .NET Core 3.1
    - IDE: Visual studios

Current goal: automating copying data from a csv file into the postgres instance as only super users are allowed to use the SQL copy command and only Microsoft company users can be superusers.
    
