Artifact ID
========

This a content package project generated using the multimodule-content-package-archetype.

This project via three sub-modules defines
* Tenant Groups
* Tenant Users (Mainly Service but Non-Service can be defined too)
* ACLs

This project contains three sub-modules, namely
* all: contains users, groups and ACLs required on BOTH Author and Publish instances. It will produce ‘permissions-all’ package. 
* author: contains users, groups and ACLs required ONLY on AUTHOR instance. It will produce ‘permissions-author’ package.
* publish: contains users, groups and ACLs required ONLY on PUBLISH instance. It will produce ‘permissions-author’ package.


R&F Groups & Privileges
--------
Based on current business requirements we will have following AEM - Author groups, see below role & privileges table,

> Note: CUDR = **C**reate **U**pdate **D**elete **R**eplicate

| Privilege        	| rf-author | rf-dam  | rf-tagger | rf-workflow-approver | rf-contributor | 
| ------------- 	|:---------:|:-------:|:---------:|:--------------------:|:--------------:|
|Read Assets        |   x       | x       | x         | x                    | x              |  
|CUDR Assets        |   x       | x       |           |                      |                |
|Read Pages         |   x       | x       | x         | x                    | x              |    
|CUDR Pages         |   x       |         |           |                      |                |
|Read Tags          |   x       | x       | x         | x                    | x              |
|CRUDR Tags         |   x       |         | x         |                      |                |
|Read Designs       |   x       | x       | x         | x                    | x              |
|CUDR Design        |   x       |         |           |                      |                |
|Read Workflows     |   x       | x       | x         | x                    | x              |
|Approve Workflows  |           |         |           | x                    |                |

They are defined in /raymourflanigan-permissions/author/src/main/content/jcr_root/home/groups/raymourflanigan-internal.

There is 'rf-developer' group defined in /raymourflanigan-permissions/all/src/main/content/jcr_root/home/groups/raymourflanigan-system. This group will be part of OOTB 'administrator' group (manual assignment) in lower Dev, QA and maybe Stage environments. On prod environment this group can get readonly access to entire repository with the help of AMS team.

> Note: The 'rf-contributor' group will be member of OOTB 'contributor' group and rest of the 'rf-*' groups will be members of 'rf-contributor' group. This way custom groups will inherit necessary OOTB permissions and we don't have to reinvent the wheel.

Building
--------
This project uses Maven for building. Common commands:

From the root directory, run ``mvn -PautoInstallPackage clean install`` to build the content package and install to a CQ instance.

Generate artifacts can be found within <PROJECT-DIR>/<all | author | publish>/target folder.


Using with VLT
--------------

To use vlt with this project, first build and install the package to your local CQ instance as described above. Then cd to `content/src/main/content/jcr_root` and run

    vlt --credentials admin:admin checkout -f ../META-INF/vault/filter.xml --force http://localhost:4502/crx

Once the working copy is created, you can use the normal ``vlt up`` and ``vlt ci`` commands.

Specifying CRX Host/Port
------------------------

The CRX host and port can be specified on the command line with:
mvn -Dcrx.host=otherhost -Dcrx.port=5502 <goals>




