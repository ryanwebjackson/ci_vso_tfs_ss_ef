# Continuous Integration - Managing schema changes when using SQL Server and Entity Framework
## General Plan for Continuous Integration with Microsoft Team Foundation Server (TFS), Visual Studio Online (VSO), SQL Server (SS), and Entity Framework (EF).

*rough outline*
1. Script (existing) database schema - Can be done manually with SSMS, but the goal of this project is to do it consistently and reliably (via the command line).  
2. Check-in script(s) with related code (back-end, etc.) changes.  
3. Utilize Visual Studio Online (VSO), or another CI server, to spin up a an empty, temporary database, based on checked in scripts (in a specific directory).  
4. Call the Entity Data Model Generator [EdmGen.exe](https://msdn.microsoft.com/en-us/library/bb896270(v=vs.110).aspx) on that database, to generate (or update?) the EF data model (edmx) for the subject code project.  
5. As part of the subject code project's build process (in VSO or other CI server), run all T4 templates - [Code Generation in a Build Process](https://msdn.microsoft.com/en-us/library/ee847423.aspx).  
6. Compile and build the project as usual.  
7. Run any tests, etc.  
8. Tear down the temporary database.  
9. The database schema scripts will remain in source control (this will version the database, regardless of the database update paradigm (migrations, etc.) used).  
