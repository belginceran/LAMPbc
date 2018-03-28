# Deploy and Manage a Scalable Moodle Cluster on Azure

This repo contains guides on how to deploy and manage a scalable
[Moodle](https://moodle.com) cluster on Azure as well as other useful information relevant to running Moodle on Azure such as a listing of Azure-relevant Moodle plugins and information on how to offer Moodle as a Managed Application on the Azure Marketplace or on an IT Service Catalog. 

If you have Azure account you can deploy Moodle via the Azure portal using the button below, or you can [deploy Moodle via the
CLI](docs/Deploy.md). Please note that while you can use an [Azure free account](https://azure.microsoft.com/en-us/free/) to get started depending on which template configuration you choose you will likely be required to upgrade to a paid account.

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy.json)  [![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy.json)

## What this stack will give you

This template set deploys the following infrastructure:
- Autoscaling web frontend layer (Nginx for https termination, Varnish for caching, Apache/php or nginx/php-fpm)
- Private virtual network for frontend instances
- Controller instance running cron and handling syslog for the autoscaled site
- Load balancer to balance across the autoscaled instances
- [Azure Database for MySQL](https://azure.microsoft.com/en-us/services/mysql/) or [Azure Database for PostgreSQL](https://azure.microsoft.com/en-us/services/postgresql/) or [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/) 
- [Azure Redis Cache](https://azure.microsoft.com/en-us/services/cache/) instance for Moodle caching (optional)
- ObjectFS in [Azure Blob Storage](https://azure.microsoft.com/en-us/services/storage/blobs/) (Moodle sitedata)
- Three Elasticsearch VMs for search indexing in Moodle (optional)
- Dual Gluster nodes for high availability access to Moodle files

![network_diagram](images/stack_diagram.png "Diagram of deployed stack")

The template also optionally installs a handful of useful plugins that allow Moodle to be integrated with select Azure services (see below for details). 

## Useful Moodle plugins for running Moodle on Azure
There below is a listing of useful plugins allow Moodle to be integrated with select Azure services: 
- [Azure Search Plugin](https://github.com/catalyst/moodle-search_azure) for [Azure Search](https://azure.microsoft.com/en-us/services/logic-apps/)
- [Trigger Plugin](https://github.com/catalyst/moodle-tool_trigger) for [Azure Logic Apps](https://azure.microsoft.com/en-us/services/logic-apps/)
- [Object File System Plugin*](https://github.com/catalyst/moodle-tool_objectfs) for [Azure Blob Storage](https://azure.microsoft.com/en-us/services/storage/blobs/)
- [Office 365 and Azure Active Directory Plugins for Moodle*](https://github.com/Microsoft/o365-moodle) for [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/)
- [Elasticsearch Plugin*](https://github.com/catalyst/moodle-search_elastic)

At the current time this template allows the optional installation of all of the plugins above with an * next to them. Please note these plugins can be installed at any time post deployment via Moodle's own plugin directory. You can find a list of all Azure relevant plugins in the Moodle plugin directory [here](https://moodle.org/plugins/browse.php?list=set&id=91). You might also choose to follow this list via RSS.

## Moodle as a Managed Application
You can learn more about how to offer Moodle as a Managed Application on the Azure Marketplace or on an IT Service Catalog [here](https://github.com/Azure/Moodle/tree/master/managedApplication). 

## Common Questions about the template
1.  **Is this template Moodle as IaaS or PaaS?**  While the current template leverages PaaS services such as Redis, MySQL, Postgres, MS SQL etc. the current template offers Moodle as IaaS. Given limitations to Moodle our focus is IaaS for the time being however we would love to be informed of your experience running Moodle as PaaS on Azure using Azure Container Service or Azure Web Apps. 

2.  **Will other OSs such as CentOS be supported in the future?** Unfortunately we only have plans to support Ubuntu at this time. It is highly unlikely that this will change.

3.  **Which database should I use?** This is entirely personal preference, however, at this time MySQL and MS SQL have higher performance than PostgreSQL. 

4. **Did Microsoft build this template alone or with the help of the Moodle community?** We did not build this template alone. We relied on the expertise and guidance of many capable Moodle partners around the world. The initial implementation of the template was done by [Catalyst IT](https://github.com/catalyst).

5. **How does this template relate to other Moodle offerings on Azure?** It is generally not a good idea to run Moodle as a single VM in a production setting. This template is highly configurable and allows for high availability and redundancy. 

6. **How does this template relate to this [Azure Quickstart Template for Moodle](https://github.com/Azure/azure-quickstart-templates/tree/master/moodle-scalable-cluster-ubuntu)?** This repo is the working repo for the quickstart template. We will be pushing changes from this template to the quickstart template on a regular cadence.

7. **I am already running Moodle on Azure. How does this benefit me?** We are looking for painpoints from the community that we can help solve. We are also looking to understand where our implementation of Moodle on Azure outperforms or underperforms other implementations out in the wild. If you have load testing scripts, performance benchmarks or just general feedback that you'd like to share we're extremely interested!

8.  **How can I help with this effort?** Please see below. 

## Contributing

This project welcomes contributions and suggestions. Our goal is to
work on Azure specific tooling for deploying and managing the open
source [Moodle](http://moodle.org) learning management system on
Azure. We do not work on Moodle itself here, instead we work upstream
as appropriate.

The short version of how to contribute to this project is "just do
it". Where "it" can be defined as any valuable contribution (and to be
clear, asking questions is a valuable contribution):

  * ask questions
  * provide feedback
  * write or update documentation
  * help new users
  * recommend the project to others
  * test the code and report bugs
  * fix bugs and issue pull requests
  * give us feedback on required features
  * write and update the software
  * create artwork
  * translate to different languages
  * anything you can see that needs doing

For a more detailed discussion of how to contribute see our [Contribution Guide](CONTRIBUTE.md).

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of
Conduct](https://opensource.microsoft.com/codeofconduct/). For more
information see the [Code of Conduct
FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact
[opencode@microsoft.com](mailto:opencode@microsoft.com) with any
additional questions or comments.

## Legal Notices

Microsoft and any contributors grant you a license to the Microsoft
documentation and other content in this repository under the [Creative
Commons Attribution 4.0 International Public
License](https://creativecommons.org/licenses/by/4.0/legalcode), see
the [LICENSE](LICENSE) file, and grant you a license to any code in
the repository under the [MIT
License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure and/or other Microsoft products
and services referenced in the documentation may be either trademarks
or registered trademarks of Microsoft in the United States and/or
other countries. The licenses for this project do not grant you rights
to use any Microsoft names, logos, or trademarks. Microsoft's general
trademark guidelines can be found at
http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all others rights, whether
under their respective copyrights, patents, or trademarks, whether by
implication, estoppel or otherwise.

## Next Steps

  1. [Deploy a Moodle Cluster](docs/Deploy.md)
  1. [Obtain Deployment Details about a Moodle Cluster](docs/Get-Install-Data.md)
  1. [Delete a Moodle Cluster](docs/Delete.md)

