---
title: "虛擬機器部署的 SAP NetWeaver aaaAzure |Microsoft 文件"
description: "了解如何 toodeploy SAP Azure 中 Linux 虛擬機器上的軟體。"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 1c4f1951-3613-4a5a-a0af-36b85750c84e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.openlocfilehash: 42f1d8a3eff51e113729dbfe2848b67deaf06936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a><span data-ttu-id="1e716-103">適用於 SAP NetWeaver 的 Azure 虛擬機器部署</span><span class="sxs-lookup"><span data-stu-id="1e716-103">Azure Virtual Machines deployment for SAP NetWeaver</span></span>
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP)
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md (Azure Virtual Machines deployment for SAP)
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md (Azure Virtual Machines planning and implementation for SAP)
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-managed-disks]:planning-guide.md#c55b2c6e-3ca1-4476-be16-16c81927550f (Managed Disks)
[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-os-disk-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk-md%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-2-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image-md%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image-md%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-windows-agent-user-guide]:../../windows/agent-user-guide.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="1e716-117">Azure 虛擬機器是 hello 解決方案需要運算和存放裝置資源，最少的時間，而不冗長的採購循環的組織。</span><span class="sxs-lookup"><span data-stu-id="1e716-117">Azure Virtual Machines is hello solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="1e716-118">您可以在 Azure 中使用 Azure 虛擬機器 toodeploy 古典應用程式，例如 SAP NetWeaver 架構的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-118">You can use Azure Virtual Machines toodeploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="1e716-119">擴充應用程式的可靠性與可用性，不需其他內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="1e716-119">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="1e716-120">「Azure 虛擬機器」支援跨單位連線能力，貴公司可將「Azure 虛擬機器」整合到其內部部署網域、私人雲端，以及 SAP 系統環境中。</span><span class="sxs-lookup"><span data-stu-id="1e716-120">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="1e716-121">在本文中，我們將討論 hello 步驟 toodeploy SAP 應用程式在 Azure 中，包括替代的部署選項與疑難排解虛擬機器 (Vm) 上。</span><span class="sxs-lookup"><span data-stu-id="1e716-121">In this article, we cover hello steps toodeploy SAP applications on virtual machines (VMs) in Azure, including alternate deployment options and troubleshooting.</span></span> <span data-ttu-id="1e716-122">這篇文章中的 hello 資訊為基礎[Azure 虛擬機器規劃和實作的 SAP NetWeaver][planning-guide]。</span><span class="sxs-lookup"><span data-stu-id="1e716-122">This article builds on hello information in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span> <span data-ttu-id="1e716-123">它也可 SAP 安裝文件集和 SAP 附註，也就是安裝和部署 SAP 軟體的 hello 主要資源。</span><span class="sxs-lookup"><span data-stu-id="1e716-123">It also complements SAP installation documentation and SAP Notes, which are hello primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e716-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="1e716-124">Prerequisites</span></span>
<span data-ttu-id="1e716-125">針對 SAP 軟體部署設定 Azure 虛擬機器，牽涉到多個步驟和資源。</span><span class="sxs-lookup"><span data-stu-id="1e716-125">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="1e716-126">開始之前，請確定您符合 hello Azure 中的虛擬機器上安裝 SAP 軟體的必要條件。</span><span class="sxs-lookup"><span data-stu-id="1e716-126">Before you start, make sure that you meet hello prerequisites for installing SAP software on virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="1e716-127">本機電腦</span><span class="sxs-lookup"><span data-stu-id="1e716-127">Local computer</span></span>
<span data-ttu-id="1e716-128">toomanage Windows 或 Linux Vm，您可以使用 PowerShell 指令碼和 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e716-128">toomanage Windows or Linux VMs, you can use a PowerShell script and hello Azure portal.</span></span> <span data-ttu-id="1e716-129">對於這兩種工具，您需有執行 Windows 7 或更新 Windows 版本的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="1e716-129">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="1e716-130">如果您想 toomanage 僅 Linux Vm，而且您想 toouse Linux 電腦，這項工作，您可以使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="1e716-130">If you want toomanage only Linux VMs and you want toouse a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="1e716-131">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="1e716-131">Internet connection</span></span>
<span data-ttu-id="1e716-132">toodownload 執行的 hello 工具及指令碼所需的 SAP 軟體部署，您必須是連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-132">toodownload and run hello tools and scripts that are required for SAP software deployment, you must be connected toohello Internet.</span></span> <span data-ttu-id="1e716-133">hello 執行 hello Azure 強化監視功能延伸模組適用於 SAP 的 Azure VM 也需要存取 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-133">hello Azure VM that is running hello Azure Enhanced Monitoring Extension for SAP also needs access toohello Internet.</span></span> <span data-ttu-id="1e716-134">如果 hello Azure VM 的 Azure 虛擬網路或內部部署網域的一部分，請確定，hello 相關的 proxy 設定，如所述[設定 hello proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="1e716-134">If hello Azure VM is part of an Azure virtual network or on-premises domain, make sure that hello relevant proxy settings are set, as described in [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="1e716-135">Microsoft Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1e716-135">Microsoft Azure subscription</span></span>
<span data-ttu-id="1e716-136">您需要使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-136">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="1e716-137">拓撲和網路</span><span class="sxs-lookup"><span data-stu-id="1e716-137">Topology and networking</span></span>
<span data-ttu-id="1e716-138">您需要 toodefine hello 拓樸和 hello Azure 中 SAP 部署的架構：</span><span class="sxs-lookup"><span data-stu-id="1e716-138">You need toodefine hello topology and architecture of hello SAP deployment in Azure:</span></span>

* <span data-ttu-id="1e716-139">使用 azure 儲存體帳戶 toobe</span><span class="sxs-lookup"><span data-stu-id="1e716-139">Azure storage accounts toobe used</span></span>
* <span data-ttu-id="1e716-140">您想要 toodeploy hello SAP 系統的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="1e716-140">Virtual network where you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="1e716-141">您希望 toodeploy hello SAP 系統的資源群組 toowhich</span><span class="sxs-lookup"><span data-stu-id="1e716-141">Resource group toowhich you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="1e716-142">您想 toodeploy hello SAP 系統的 azure 地區</span><span class="sxs-lookup"><span data-stu-id="1e716-142">Azure region where you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="1e716-143">SAP 組態 (兩層或三層)</span><span class="sxs-lookup"><span data-stu-id="1e716-143">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="1e716-144">VM 大小和其他資料磁碟 toobe hello 號碼掛接 toohello Vm</span><span class="sxs-lookup"><span data-stu-id="1e716-144">VM sizes and hello number of additional data disks toobe mounted toohello VMs</span></span>
* <span data-ttu-id="1e716-145">SAP Correction and Transport System (CTS) 組態</span><span class="sxs-lookup"><span data-stu-id="1e716-145">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="1e716-146">建立並設定 Azure 儲存體帳戶 （如有必要） 或 Azure 虛擬網路，才能開始 hello SAP 軟體部署程序。</span><span class="sxs-lookup"><span data-stu-id="1e716-146">Create and configure Azure storage accounts (if required) or Azure virtual networks before you begin hello SAP software deployment process.</span></span> <span data-ttu-id="1e716-147">如需有關資訊 toocreate 和設定這些資源，請參閱[Azure 虛擬機器規劃和實作的 SAP NetWeaver][planning-guide]。</span><span class="sxs-lookup"><span data-stu-id="1e716-147">For information about how toocreate and configure these resources, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="1e716-148">SAP 大小調整</span><span class="sxs-lookup"><span data-stu-id="1e716-148">SAP sizing</span></span>
<span data-ttu-id="1e716-149">了解下列資訊，如 SAP 調整大小的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-149">Know hello following information, for SAP sizing:</span></span>

* <span data-ttu-id="1e716-150">預計的 SAP 工作負載，比方說，使用 hello SAP 快速 Sizer 工具，與 hello SAP 應用程式的效能標準 (SAP)</span><span class="sxs-lookup"><span data-stu-id="1e716-150">Projected SAP workload, for example, by using hello SAP Quick Sizer tool, and hello SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="1e716-151">需要 CPU 資源和記憶體耗用量的 hello SAP 系統</span><span class="sxs-lookup"><span data-stu-id="1e716-151">Required CPU resource and memory consumption of hello SAP system</span></span>
* <span data-ttu-id="1e716-152">每秒所需的輸入/輸出 (I/O) 作業</span><span class="sxs-lookup"><span data-stu-id="1e716-152">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="1e716-153">Azure 中 VM 之間最終通訊所需的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="1e716-153">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="1e716-154">在內部部署資產和 hello Azure 部署 SAP 系統之間的所需的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="1e716-154">Required network bandwidth between on-premises assets and hello Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="1e716-155">資源群組</span><span class="sxs-lookup"><span data-stu-id="1e716-155">Resource groups</span></span>
<span data-ttu-id="1e716-156">Azure 資源管理員 中，您可以使用資源群組 toomanage hello 應用程式的所有資源在您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-156">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="1e716-157">如需詳細資訊，請參閱 [Azure Resource Manager概觀][resource-group-overview]。</span><span class="sxs-lookup"><span data-stu-id="1e716-157">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="1e716-158">資源</span><span class="sxs-lookup"><span data-stu-id="1e716-158">Resources</span></span>

### <span data-ttu-id="1e716-159"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP 資源</span><span class="sxs-lookup"><span data-stu-id="1e716-159"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP resources</span></span>
<span data-ttu-id="1e716-160">當您設定 SAP 軟體部署時，您需要遵循 SAP 資源 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-160">When you are setting up your SAP software deployment, you need hello following SAP resources:</span></span>

* <span data-ttu-id="1e716-161">SAP Note [1928533]，其中包含：</span><span class="sxs-lookup"><span data-stu-id="1e716-161">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="1e716-162">Hello 部署 SAP 軟體所支援的 Azure VM 大小的清單</span><span class="sxs-lookup"><span data-stu-id="1e716-162">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="1e716-163">Azure VM 大小的重要容量資訊</span><span class="sxs-lookup"><span data-stu-id="1e716-163">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="1e716-164">支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合</span><span class="sxs-lookup"><span data-stu-id="1e716-164">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="1e716-165">Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本</span><span class="sxs-lookup"><span data-stu-id="1e716-165">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="1e716-166">SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。</span><span class="sxs-lookup"><span data-stu-id="1e716-166">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="1e716-167">SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-167">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="1e716-168">SAP 附註[1409604] hello 需 SAP Host Agent 版本 Windows Azure 中。</span><span class="sxs-lookup"><span data-stu-id="1e716-168">SAP Note [1409604] has hello required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="1e716-169">SAP 附註[2191498]具有 hello 必要 SAP Host Agent 版本適用於在 Azure 中的 Linux。</span><span class="sxs-lookup"><span data-stu-id="1e716-169">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="1e716-170">SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-170">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="1e716-171">SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-171">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="1e716-172">SAP Note [2002167] 包含 Red Hat Enterprise Linux 7.x 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-172">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="1e716-173">SAP Note [2069760] 包含 Oracle Linux 7.x 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-173">SAP Note [2069760] has general information about Oracle Linux 7.x.</span></span>
* <span data-ttu-id="1e716-174">SAP 附註[1999351] hello Azure 強化監視功能延伸模組適用於 SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-174">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="1e716-175">SAP Note [1597355] 包含 Linux 交換空間的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-175">SAP Note [1597355] has general information about swap-space for Linux.</span></span>
* <span data-ttu-id="1e716-176">[Azure SCN 上的 SAP 頁面](https://wiki.scn.sap.com/wiki/x/Pia7Gg)包含新聞和實用資源的集合。</span><span class="sxs-lookup"><span data-stu-id="1e716-176">[SAP on Azure SCN page](https://wiki.scn.sap.com/wiki/x/Pia7Gg) has news and a collection of useful resources.</span></span>
* <span data-ttu-id="1e716-177">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。</span><span class="sxs-lookup"><span data-stu-id="1e716-177">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="1e716-178">[Azure PowerShell][azure-ps] 所包含的 SAP 特定 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1e716-178">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="1e716-179">[Azure CLI][azure-cli] 所包含的 SAP 特定 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="1e716-179">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

### <span data-ttu-id="1e716-180"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Windows 資源</span><span class="sxs-lookup"><span data-stu-id="1e716-180"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Windows resources</span></span>
<span data-ttu-id="1e716-181">這些 Microsoft 文章涵蓋 Azure 中的 SAP 部署：</span><span class="sxs-lookup"><span data-stu-id="1e716-181">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="1e716-182">[SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="1e716-182">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="1e716-183">[適用於 SAP NetWeaver 的 Azure 虛擬機器部署 (本文)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="1e716-183">[Azure Virtual Machines deployment for SAP NetWeaver (this article)][deployment-guide]</span></span>
* <span data-ttu-id="1e716-184">[SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="1e716-184">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>

## <span data-ttu-id="1e716-185"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure VM 上的 SAP 軟體部署案例</span><span class="sxs-lookup"><span data-stu-id="1e716-185"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="1e716-186">您有多個選項可用於在 Azure 中部署 VM 和相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-186">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="1e716-187">部署選項之間的重要 toounderstand hello 差異是因為您可能需要不同的步驟 tooprepare 根據您所選擇的 hello 部署類型的部署 Vm。</span><span class="sxs-lookup"><span data-stu-id="1e716-187">It's important toounderstand hello differences between deployment options, because you might take different steps tooprepare your VMs for deployment based on hello deployment type you choose.</span></span>

### <span data-ttu-id="1e716-188"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>案例 1： 部署從 hello 適用於 SAP 的 Azure Marketplace 中的 VM</span><span class="sxs-lookup"><span data-stu-id="1e716-188"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Deploying a VM from hello Azure Marketplace for SAP</span></span>
<span data-ttu-id="1e716-189">您可以使用由 Microsoft 提供的映像，或由協力廠商 hello Azure Marketplace toodeploy 在您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-189">You can use an image provided by Microsoft or by a third party in hello Azure Marketplace toodeploy your VM.</span></span> <span data-ttu-id="1e716-190">hello Marketplace 提供了一些標準的 OS 映像的 Windows Server 和其他 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="1e716-190">hello Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="1e716-191">您也可以部署包含資料庫管理系統 (DBMS) SKU 的映像，例如，Microsoft SQL Server。</span><span class="sxs-lookup"><span data-stu-id="1e716-191">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="1e716-192">如需使用映像搭配 DBMS SKU 的詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]。</span><span class="sxs-lookup"><span data-stu-id="1e716-192">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span>

<span data-ttu-id="1e716-193">hello 下列流程圖顯示 hello SAP 特定的序列，部署將 VM 從 hello Azure Marketplace 的步驟：</span><span class="sxs-lookup"><span data-stu-id="1e716-193">hello following flowchart shows hello SAP-specific sequence of steps for deploying a VM from hello Azure Marketplace:</span></span>

![使用 VM 映像從 hello Azure Marketplace 的 SAP 系統部署 VM 的流程圖][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a><span data-ttu-id="1e716-195">使用 hello Azure 入口網站建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e716-195">Create a virtual machine by using hello Azure portal</span></span>
<span data-ttu-id="1e716-196">最簡單方式 toocreate hello hello Azure Marketplace 中的影像與新的虛擬機器是使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e716-196">hello easiest way toocreate a new virtual machine with an image from hello Azure Marketplace is by using hello Azure portal.</span></span>

1.  <span data-ttu-id="1e716-197">跳過<https://portal.azure.com/#create/hub>。</span><span class="sxs-lookup"><span data-stu-id="1e716-197">Go too<https://portal.azure.com/#create/hub>.</span></span>  <span data-ttu-id="1e716-198">或者，您也可以在 hello Azure 入口網站功能表，選取**+ 新增**。</span><span class="sxs-lookup"><span data-stu-id="1e716-198">Or, in hello Azure portal menu, select **+ New**.</span></span>
2.  <span data-ttu-id="1e716-199">選取**計算**，然後選取您想要 toodeploy 作業系統的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-199">Select **Compute**, and then select hello type of operating system you want toodeploy.</span></span> <span data-ttu-id="1e716-200">例如，Windows Server 2012 R2、SUSE Linux Enterprise Server 12 (SLES 12)、Red Hat Enterprise Linux 7.2 (RHEL 7.2) 或 Oracle Linux 7.2。</span><span class="sxs-lookup"><span data-stu-id="1e716-200">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span></span> <span data-ttu-id="1e716-201">hello 預設清單檢視不會顯示所有支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="1e716-201">hello default list view does not show all supported operating systems.</span></span> <span data-ttu-id="1e716-202">選取 [查看全部] 以取得完整清單。</span><span class="sxs-lookup"><span data-stu-id="1e716-202">Select **see all** for a full list.</span></span> <span data-ttu-id="1e716-203">如需 SAP 軟體部署支援的作業系統詳細資訊，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="1e716-203">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
3.  <span data-ttu-id="1e716-204">在 hello 下一個頁面上，檢閱 條款和條件。</span><span class="sxs-lookup"><span data-stu-id="1e716-204">On hello next page, review terms and conditions.</span></span>
4.  <span data-ttu-id="1e716-205">在 hello**選取部署模型**方塊中，選取**資源管理員**。</span><span class="sxs-lookup"><span data-stu-id="1e716-205">In hello **Select a deployment model** box, select **Resource Manager**.</span></span>
5.  <span data-ttu-id="1e716-206">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="1e716-206">Select **Create**.</span></span>

<span data-ttu-id="1e716-207">hello 精靈會引導您完成設定所需的 hello 參數 toocreate hello 虛擬機器，此外 tooall 所需的資源，如網路介面和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-207">hello wizard guides you through setting hello required parameters toocreate hello virtual machine, in addition tooall required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="1e716-208">其中一些參數包括︰</span><span class="sxs-lookup"><span data-stu-id="1e716-208">Some of these parameters are:</span></span>

1. <span data-ttu-id="1e716-209">**基本**：</span><span class="sxs-lookup"><span data-stu-id="1e716-209">**Basics**:</span></span>
 * <span data-ttu-id="1e716-210">**名稱**: hello hello 資源 （hello 虛擬機器名稱） 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e716-210">**Name**: hello name of hello resource (hello virtual machine name).</span></span>
 * <span data-ttu-id="1e716-211">**VM 磁碟類型**： 選取 hello 的 hello OS 磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-211">**VM disk type**: Select hello disk type of hello OS disk.</span></span> <span data-ttu-id="1e716-212">如果您想 toouse 高階儲存體的資料磁碟時，建議使用進階儲存體的 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-212">If you want toouse Premium Storage for your data disks, we recommend using Premium Storage for hello OS disk as well.</span></span>
 * <span data-ttu-id="1e716-213">**使用者名稱和密碼**或**SSH 公開金鑰**: hello 使用者名稱和密碼的 hello 佈建期間建立的 hello 使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="1e716-213">**Username and password** or **SSH public key**: Enter hello username and password of hello user that is created during hello provisioning.</span></span> <span data-ttu-id="1e716-214">針對 Linux 虛擬機器，您可以輸入 hello toohello 機器用於 toosign 公開安全殼層 (SSH) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e716-214">For a Linux virtual machine, you can enter hello public Secure Shell (SSH) key that you use toosign in toohello machine.</span></span>
 * <span data-ttu-id="1e716-215">**訂用帳戶**： 選取您想要 toouse tooprovision hello 新虛擬機器的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-215">**Subscription**: Select hello subscription that you want toouse tooprovision hello new virtual machine.</span></span>
 * <span data-ttu-id="1e716-216">**資源群組**: hello hello 資源群組名稱 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-216">**Resource group**: hello name of hello resource group for hello VM.</span></span> <span data-ttu-id="1e716-217">您可以輸入新資源群組或 hello 名稱的資源群組已存在的任何一個 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e716-217">You can enter either hello name of a new resource group or hello name of a resource group that already exists.</span></span>
 * <span data-ttu-id="1e716-218">**位置**: toodeploy hello 新的虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-218">**Location**: Where toodeploy hello new virtual machine.</span></span> <span data-ttu-id="1e716-219">如果您想 tooconnect hello 虛擬機器 tooyour 在內部部署網路，請確定您選取 hello hello Azure tooyour 在內部部署網路連線的虛擬網路位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-219">If you want tooconnect hello virtual machine tooyour on-premises network, make sure you select hello location of hello virtual network that connects Azure tooyour on-premises network.</span></span> <span data-ttu-id="1e716-220">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的 [Microsoft Azure 網路][planning-guide-microsoft-azure-networking]。</span><span class="sxs-lookup"><span data-stu-id="1e716-220">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>
2. <span data-ttu-id="1e716-221">：</span><span class="sxs-lookup"><span data-stu-id="1e716-221">**Size**:</span></span>

     <span data-ttu-id="1e716-222">如需支援的 VM 類型清單，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="1e716-222">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="1e716-223">請確定您選取 hello 正確的 VM 類型，如果您想 toouse Azure 高階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-223">Be sure you select hello correct VM type if you want toouse Azure Premium Storage.</span></span> <span data-ttu-id="1e716-224">並非所有 VM 類型都支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-224">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="1e716-225">如需詳細資訊，請參閱[Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的[儲存體：Microsoft Azure 儲存體和資料磁碟][planning-guide-storage-microsoft-azure-storage-and-data-disks]和 [Azure 進階儲存體][planning-guide-azure-premium-storage]。</span><span class="sxs-lookup"><span data-stu-id="1e716-225">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

3. <span data-ttu-id="1e716-226">**設定**：</span><span class="sxs-lookup"><span data-stu-id="1e716-226">**Settings**:</span></span>
  * <span data-ttu-id="1e716-227">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="1e716-227">**Storage**</span></span>
    * <span data-ttu-id="1e716-228">**磁碟類型**： 選取 hello 的 hello OS 磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-228">**Disk Type**: Select hello disk type of hello OS disk.</span></span> <span data-ttu-id="1e716-229">如果您想 toouse 高階儲存體的資料磁碟時，建議使用進階儲存體的 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-229">If you want toouse Premium Storage for your data disks, we recommend using Premium Storage for hello OS disk as well.</span></span>
    * <span data-ttu-id="1e716-230">**使用受管理的磁碟**： 如果您想 toouse 管理磁碟，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="1e716-230">**Use managed disks**: If you want toouse Managed Disks, select Yes.</span></span> <span data-ttu-id="1e716-231">如需有關管理磁碟的詳細資訊，請參閱第章[管理磁碟][ planning-guide-managed-disks] hello 規劃指南中。</span><span class="sxs-lookup"><span data-stu-id="1e716-231">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in hello planning guide.</span></span>
    * <span data-ttu-id="1e716-232">**儲存體帳戶**：選取現有的儲存體帳戶或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-232">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="1e716-233">並非所有的儲存體類型都適用於執行 SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-233">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="1e716-234">如需儲存體類型的詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-234">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span>
  * <span data-ttu-id="1e716-235">**網路**</span><span class="sxs-lookup"><span data-stu-id="1e716-235">**Network**</span></span>
    * <span data-ttu-id="1e716-236">**虛擬網路**和**子網路**: toointegrate hello 虛擬機器與您的內部網路連線的 tooyour 在內部部署網路選取 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-236">**Virtual network** and **Subnet**: toointegrate hello virtual machine with your intranet, select hello virtual network that is connected tooyour on-premises network.</span></span>
    * <span data-ttu-id="1e716-237">**公用 IP 位址**： 選取 hello 公用 IP 位址，您想 toouse，或輸入參數 toocreate 新的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1e716-237">**Public IP address**: Select hello public IP address that you want toouse, or enter parameters toocreate a new public IP address.</span></span> <span data-ttu-id="1e716-238">您可以透過 hello 網際網路使用公用 IP 位址 tooaccess 您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-238">You can use a public IP address tooaccess your virtual machine over hello Internet.</span></span> <span data-ttu-id="1e716-239">請確定，您也可以建立網路安全性群組 toohelp 安全存取 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-239">Make sure that you also create a network security group toohelp secure access tooyour virtual machine.</span></span>
    * <span data-ttu-id="1e716-240">**網路安全性群組**：如需詳細資訊，請參閱[使用網路安全性群組控制網路流量流程][virtual-networks-nsg]。</span><span class="sxs-lookup"><span data-stu-id="1e716-240">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
  * <span data-ttu-id="1e716-241">**擴充功能**： 您可以藉由加入 toohello 部署中安裝虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1e716-241">**Extensions**: You can install virtual machine extensions by adding them toohello deployment.</span></span> <span data-ttu-id="1e716-242">您不需要在此步驟中 tooadd 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1e716-242">You do not need tooadd extensions in this step.</span></span> <span data-ttu-id="1e716-243">所需的 SAP 支援的 hello 延伸模組會安裝更新版本。</span><span class="sxs-lookup"><span data-stu-id="1e716-243">hello extensions required for SAP support are installed later.</span></span> <span data-ttu-id="1e716-244">請參閱第章[設定 hello Azure 強化監視功能延伸模組適用於 SAP] [ deployment-guide-4.5]本指南中。</span><span class="sxs-lookup"><span data-stu-id="1e716-244">See chapter [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span></span>
  * <span data-ttu-id="1e716-245">**高可用性**： 選擇可用性設定組，或輸入 hello 參數 toocreate 新的可用性設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-245">**High Availability**: Select an availability set, or enter hello parameters toocreate a new availability set.</span></span> <span data-ttu-id="1e716-246">如需詳細資訊，請參閱 [Azure 可用性設定組][planning-guide-3.2.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-246">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
  * <span data-ttu-id="1e716-247">**監視**</span><span class="sxs-lookup"><span data-stu-id="1e716-247">**Monitoring**</span></span>
    * <span data-ttu-id="1e716-248">**開機診斷**︰您可以選取 [停用] 開機診斷。</span><span class="sxs-lookup"><span data-stu-id="1e716-248">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span></span>
    * <span data-ttu-id="1e716-249">**客體 OS 診斷**︰您可以選取 [停用] 監視診斷。</span><span class="sxs-lookup"><span data-stu-id="1e716-249">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span></span>

4. <span data-ttu-id="1e716-250">**摘要**：</span><span class="sxs-lookup"><span data-stu-id="1e716-250">**Summary**:</span></span>

  <span data-ttu-id="1e716-251">檢閱您的選取項目，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1e716-251">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="1e716-252">您的虛擬機器部署在您選取的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e716-252">Your virtual machine is deployed in hello resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="1e716-253">使用範本建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e716-253">Create a virtual machine by using a template</span></span>
<span data-ttu-id="1e716-254">您可以使用其中一種在 hello 發行 hello SAP 範本建立虛擬機器[azure-快速入門範本 GitHub 儲存機制][azure-quickstart-templates-github]。</span><span class="sxs-lookup"><span data-stu-id="1e716-254">You can create a virtual machine by using one of hello SAP templates published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="1e716-255">您也可以手動建立虛擬機器使用 hello [Azure 入口網站][virtual-machines-windows-tutorial]， [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]，或[Azure CLI][virtual-machines-linux-tutorial].</span><span class="sxs-lookup"><span data-stu-id="1e716-255">You also can manually create a virtual machine by using hello [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="1e716-256">[**兩層組態 (僅只一部虛擬機器) 範本** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="1e716-256">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="1e716-257">toocreate 兩層式系統使用只有一部虛擬機器，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-257">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="1e716-258">[**兩層組態 (僅只一部虛擬機器) 範本 - 受管理磁碟** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]</span><span class="sxs-lookup"><span data-stu-id="1e716-258">[**Two-tier configuration (only one virtual machine) template - Managed Disks** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]</span></span>

  <span data-ttu-id="1e716-259">toocreate 兩層式系統使用只有一個虛擬機器和受管理的磁碟，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-259">toocreate a two-tier system by using only one virtual machine and Managed Disks, use this template.</span></span>
* <span data-ttu-id="1e716-260">[**三層組態 (多部虛擬機器) 範本** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="1e716-260">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="1e716-261">toocreate 三層式系統使用多部虛擬機器，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-261">toocreate a three-tier system by using multiple virtual machines, use this template.</span></span>
* <span data-ttu-id="1e716-262">[**三層組態 (多部虛擬機器) 範本 - 受管理磁碟** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]</span><span class="sxs-lookup"><span data-stu-id="1e716-262">[**Three-tier configuration (multiple virtual machines) template - Managed Disks** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]</span></span>

  <span data-ttu-id="1e716-263">toocreate 三層式系統使用多個虛擬機器和受管理的磁碟，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-263">toocreate a three-tier system by using multiple virtual machines and Managed Disks, use this template.</span></span>

<span data-ttu-id="1e716-264">在 hello Azure 入口網站中，輸入下列 hello 範本參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-264">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="1e716-265">**基本**：</span><span class="sxs-lookup"><span data-stu-id="1e716-265">**Basics**:</span></span>
  * <span data-ttu-id="1e716-266">**訂用帳戶**: hello 訂用帳戶 toouse toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-266">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="1e716-267">**資源群組**: hello 資源群組 toouse toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-267">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="1e716-268">您可以建立新的資源群組，或者您可以選取現有的資源群組 hello 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1e716-268">You can create a new resource group, or you can select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="1e716-269">**位置**: toodeploy hello 範本的位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-269">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="1e716-270">如果您選取現有的資源群組時，會使用該資源群組中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-270">If you selected an existing resource group, hello location of that resource group is used.</span></span>

2. <span data-ttu-id="1e716-271">**設定**：</span><span class="sxs-lookup"><span data-stu-id="1e716-271">**Settings**:</span></span>
  * <span data-ttu-id="1e716-272">**SAP 系統識別碼**: hello SAP 系統識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="1e716-272">**SAP System ID**: hello SAP System ID (SID).</span></span>
  * <span data-ttu-id="1e716-273">**OS 類型**: hello 作業系統 toodeploy，例如、 Windows Server 2012 R2、 SUSE Linux Enterprise Server 12 (SLES 12)、 Red Hat Enterprise Linux 7.2 (RHEL 7.2) 或 Oracle Linux 7.2。</span><span class="sxs-lookup"><span data-stu-id="1e716-273">**OS type**: hello operating system you want toodeploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span></span>

    <span data-ttu-id="1e716-274">hello 清單檢視不會顯示所有支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="1e716-274">hello list view does not show all supported operating systems.</span></span> <span data-ttu-id="1e716-275">如需 SAP 軟體部署支援的作業系統詳細資訊，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="1e716-275">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="1e716-276">**SAP 系統大小**: hello hello SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="1e716-276">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="1e716-277">提供的 SAPS hello 新系統的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1e716-277">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="1e716-278">如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="1e716-278">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="1e716-279">**系統可用性**（三層式範本）： hello 系統可用性。</span><span class="sxs-lookup"><span data-stu-id="1e716-279">**System availability** (three-tier template only): hello system availability.</span></span>

    <span data-ttu-id="1e716-280">選取適合高可用性安裝組態的 **HA**。</span><span class="sxs-lookup"><span data-stu-id="1e716-280">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="1e716-281">為 ABAP SAP Central Services (ASCS) 建立兩部資料庫伺服器和兩部伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e716-281">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="1e716-282">**儲存體類型**（僅限兩層式範本）： hello 的儲存體 toouse 型別。</span><span class="sxs-lookup"><span data-stu-id="1e716-282">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="1e716-283">對於大型系統，我們強烈建議使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-283">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="1e716-284">如需儲存體類型的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="1e716-284">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="1e716-285">[針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]</span><span class="sxs-lookup"><span data-stu-id="1e716-285">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="1e716-286">[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="1e716-286">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="1e716-287">[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="1e716-287">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="1e716-288">[簡介 tooMicrosoft Azure 儲存體][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="1e716-288">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="1e716-289">**管理員使用者名稱**和**管理員密碼**：使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-289">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="1e716-290">建立新的使用者，登入 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-290">A new user is created, for signing in toohello virtual machine.</span></span>
  * <span data-ttu-id="1e716-291">**新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-291">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="1e716-292">如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。</span><span class="sxs-lookup"><span data-stu-id="1e716-292">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="1e716-293">**子網路識別碼**: hello 識別碼 hello 子網路 hello 虛擬機器會連接到。</span><span class="sxs-lookup"><span data-stu-id="1e716-293">**Subnet ID**: hello ID of hello subnet hello virtual machines will connect to.</span></span> <span data-ttu-id="1e716-294">選取您的虛擬私人網路 (VPN) 或 Azure ExpressRoute 虛擬網路 toouse tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-294">Select hello subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="1e716-295">hello 識別碼通常看起來像這樣： /subscriptions/&lt;訂用帳戶 id > /resourceGroups/&lt;資源群組名稱 > /providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱 > /subnets/&lt;子網路名稱 ></span><span class="sxs-lookup"><span data-stu-id="1e716-295">hello ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="1e716-296">**條款及條件**：</span><span class="sxs-lookup"><span data-stu-id="1e716-296">**Terms and conditions**:</span></span>  
    <span data-ttu-id="1e716-297">檢閱並接受 hello 法律條款。</span><span class="sxs-lookup"><span data-stu-id="1e716-297">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="1e716-298">選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="1e716-298">Select **Purchase**.</span></span>

<span data-ttu-id="1e716-299">當您使用從 hello Azure Marketplace 映像時，預設會部署 hello Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-299">hello Azure VM Agent is deployed by default when you use an image from hello Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="1e716-300">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="1e716-300">Configure proxy settings</span></span>
<span data-ttu-id="1e716-301">根據您在內部部署網路的設定方式，您可能需要在 VM 上的 tooset hello proxy。</span><span class="sxs-lookup"><span data-stu-id="1e716-301">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="1e716-302">如果 VM 是透過 VPN 或 ExpressRoute 連線的 tooyour 在內部部署網路，hello VM 可能不是可以 tooaccess hello 網際網路，和不可以 toodownload hello 所需的擴充功能或收集的監視資料。</span><span class="sxs-lookup"><span data-stu-id="1e716-302">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="1e716-303">如需詳細資訊，請參閱[設定 hello proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="1e716-303">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="1e716-304">加入網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="1e716-304">Join a domain (Windows only)</span></span>
<span data-ttu-id="1e716-305">如果您的 Azure 部署連接的 tooan 在內部部署 Active Directory 或 DNS 執行個體已透過 Azure 站台對站 VPN 連線或 ExpressRoute (這稱為*跨單位*中[規劃 Azure 虛擬機器與實作的 SAP NetWeaver][planning-guide])，預期該 hello VM 加入內部網域。</span><span class="sxs-lookup"><span data-stu-id="1e716-305">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="1e716-306">如需考量這項工作的詳細資訊，請參閱[加入 VM tooan 在內部部署網域 (僅限 Windows)][deployment-guide-4.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-306">For more information about considerations for this task, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <span data-ttu-id="1e716-307"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>設定監視</span><span class="sxs-lookup"><span data-stu-id="1e716-307"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configure monitoring</span></span>
<span data-ttu-id="1e716-308">確定 SAP 支援您的環境中所述設定 hello Azure Monitoring Extension for SAP toobe[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="1e716-308">toobe sure SAP supports your environment, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1e716-309">檢查 SAP monitoring，和最低要求版本的 SAP 核心與 SAP Host Agent，在 hello 中列出的資源中的 hello 必要條件[SAP 資源][deployment-guide-2.2]。</span><span class="sxs-lookup"><span data-stu-id="1e716-309">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="1e716-310">監視檢查</span><span class="sxs-lookup"><span data-stu-id="1e716-310">Monitoring check</span></span>
<span data-ttu-id="1e716-311">如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="1e716-311">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="1e716-312">部署後步驟</span><span class="sxs-lookup"><span data-stu-id="1e716-312">Post-deployment steps</span></span>
<span data-ttu-id="1e716-313">在建立之後 hello VM 及 hello VM 的部署，您需要在 hello VM tooinstall hello 必要軟體元件。</span><span class="sxs-lookup"><span data-stu-id="1e716-313">After you create hello VM and hello VM is deployed, you need tooinstall hello required software components in hello VM.</span></span> <span data-ttu-id="1e716-314">在這種類型的 VM 部署的 hello 部署/軟體安裝順序，因為安裝 hello 軟體 toobe 必須已經是可供使用，在 Azure 中，另一個在 VM 上，或為可附加的磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-314">Because of hello deployment/software installation sequence in this type of VM deployment, hello software toobe installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="1e716-315">或者，請考慮使用跨單位案例中，哪些連線 toohello 內部部署資產 （安裝共用） 指定。</span><span class="sxs-lookup"><span data-stu-id="1e716-315">Or, consider using a cross-premises scenario, in which connectivity toohello on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="1e716-316">部署在 Azure VM 之後，後續 hello 相同指導方針和工具 tooinstall hello SAP 軟體在您為您的 VM 會在內部部署環境中。</span><span class="sxs-lookup"><span data-stu-id="1e716-316">After you deploy your VM in Azure, follow hello same guidelines and tools tooinstall hello SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="1e716-317">tooinstall Azure VM 上的 SAP 軟體，同時 SAP 和 Microsoft 建議您上傳，並將 hello SAP 安裝媒體儲存在 Azure Vhd 或受管理的磁碟，或您建立 Azure VM，為檔案伺服器具有所有 hello 運作所需的 SAP 安裝媒體。</span><span class="sxs-lookup"><span data-stu-id="1e716-317">tooinstall SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store hello SAP installation media on Azure VHDs or Managed Disks, or that you create an Azure VM that works as a file server that has all hello required SAP installation media.</span></span>

### <span data-ttu-id="1e716-318"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>案例 2：使用自訂映像為 SAP 部署 VM</span><span class="sxs-lookup"><span data-stu-id="1e716-318"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="1e716-319">因為不同版本的作業系統或 DBMS 擁有不同修補程式需求，您在 hello Azure Marketplace 中找到的 hello 映像可能無法滿足您的需求。</span><span class="sxs-lookup"><span data-stu-id="1e716-319">Because different versions of an operating system or DBMS have different patch requirements, hello images you find in hello Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="1e716-320">Toocreate VM 而可以使用您自己 OS/DBMS VM 映像，您可以稍後再部署。</span><span class="sxs-lookup"><span data-stu-id="1e716-320">You might instead want toocreate a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="1e716-321">您使用不同的步驟 toocreate 私人映像適用於 Linux 比 windows toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="1e716-321">You use different steps toocreate a private image for Linux than toocreate one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="1e716-323">Windows</span><span class="sxs-lookup"><span data-stu-id="1e716-323">Windows</span></span>
>
> <span data-ttu-id="1e716-324">您可以使用多個虛擬機器、 hello Windows 設定 （例如 Windows SID 和主機名稱） 必須是抽象或一般化的 toodeploy hello 的 Windows 映像 tooprepare 內部部署 VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-324">tooprepare a Windows image that you can use toodeploy multiple virtual machines, hello Windows settings (like Windows SID and hostname) must be abstracted or generalized on hello on-premises VM.</span></span> <span data-ttu-id="1e716-325">您可以使用[sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo 這。</span><span class="sxs-lookup"><span data-stu-id="1e716-325">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="1e716-327">Linux</span><span class="sxs-lookup"><span data-stu-id="1e716-327">Linux</span></span>
>
> <span data-ttu-id="1e716-328">tooprepare Linux 映像，您可以使用 toodeploy 多部虛擬機器，某些 Linux 設定必須是抽象或一般化上 hello 內部部署 VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-328">tooprepare a Linux image that you can use toodeploy multiple virtual machines, some Linux settings must be abstracted or generalized on hello on-premises VM.</span></span> <span data-ttu-id="1e716-329">您可以使用`waagent -deprovision`toodo 這。</span><span class="sxs-lookup"><span data-stu-id="1e716-329">You can use `waagent -deprovision`  toodo this.</span></span> <span data-ttu-id="1e716-330">如需詳細資訊，請參閱[擷取 Linux 虛擬機器在 Azure 上執行][ virtual-machines-linux-capture-image]和 hello [Azure Linux 代理程式使用者指南][virtual-machines-linux-agent-user-guide-command-line-options]。</span><span class="sxs-lookup"><span data-stu-id="1e716-330">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and hello [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="1e716-331">您可以準備和建立自訂映像，，然後使用它 toocreate 多個新的 Vm。</span><span class="sxs-lookup"><span data-stu-id="1e716-331">You can prepare and create a custom image, and then use it toocreate multiple new VMs.</span></span> <span data-ttu-id="1e716-332">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]。</span><span class="sxs-lookup"><span data-stu-id="1e716-332">This is described in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span> <span data-ttu-id="1e716-333">設定您的資料庫內容，透過 SAP Software Provisioning Manager tooinstall 新 SAP 系統 （會從附加的 toohello 虛擬機器的磁碟還原資料庫備份） 或還原資料庫備份，直接從 Azure 儲存體，如果您的 DBMS支援它。</span><span class="sxs-lookup"><span data-stu-id="1e716-333">Set up your database content either by using SAP Software Provisioning Manager tooinstall a new SAP system (restores a database backup from a disk that's attached toohello virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="1e716-334">如需詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]。</span><span class="sxs-lookup"><span data-stu-id="1e716-334">For more information, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span> <span data-ttu-id="1e716-335">如果您已在內部部署 VM （特別是針對兩層式系統） 上安裝 SAP 系統，您可以使用 hello 系統重新命名程序支援的 SAP 軟體佈建 hello 部署的 hello Azure VM 後調整 hello SAP 系統設定管理員 (SAP 附註[1619720])。</span><span class="sxs-lookup"><span data-stu-id="1e716-335">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt hello SAP system settings after hello deployment of hello Azure VM by using hello System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="1e716-336">否則，您也可以在您部署的 hello Azure VM 之後安裝 hello SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="1e716-336">Otherwise, you can install hello SAP software after you deploy hello Azure VM.</span></span>

<span data-ttu-id="1e716-337">hello 下列流程圖顯示 hello SAP 特定的序列，部署將 VM 從自訂映像的步驟：</span><span class="sxs-lookup"><span data-stu-id="1e716-337">hello following flowchart shows hello SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![使用私人 Marketplace 中的 VM 映像部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a><span data-ttu-id="1e716-339">使用 hello Azure 入口網站建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e716-339">Create a virtual machine by using hello Azure portal</span></span>
<span data-ttu-id="1e716-340">最簡單方式 toocreate hello 中受管理的磁碟映像的新虛擬機器是使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e716-340">hello easiest way toocreate a new virtual machine from a Managed Disk image is by using hello Azure portal.</span></span> <span data-ttu-id="1e716-341">如需有關如何 toocreate 管理磁碟映像，讀取[擷取受管理的 Azure 中的一般化 VM 映像](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)</span><span class="sxs-lookup"><span data-stu-id="1e716-341">For more information on how toocreate a Manage Disk Image, read [Capture a managed image of a generalized VM in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)</span></span>

1.  <span data-ttu-id="1e716-342">跳過<https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>。</span><span class="sxs-lookup"><span data-stu-id="1e716-342">Go too<https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>.</span></span> <span data-ttu-id="1e716-343">或者，您也可以在 hello Azure 入口網站功能表，選取**映像**。</span><span class="sxs-lookup"><span data-stu-id="1e716-343">Or, in hello Azure portal menu, select **Images**.</span></span>
2.  <span data-ttu-id="1e716-344">選取 hello 管理磁碟映像 toodeploy 然後按一下**建立 VM**</span><span class="sxs-lookup"><span data-stu-id="1e716-344">Select hello Managed Disk image you want toodeploy and click on **Create VM**</span></span>

<span data-ttu-id="1e716-345">hello 精靈會引導您完成設定所需的 hello 參數 toocreate hello 虛擬機器，此外 tooall 所需的資源，如網路介面和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-345">hello wizard guides you through setting hello required parameters toocreate hello virtual machine, in addition tooall required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="1e716-346">其中一些參數包括︰</span><span class="sxs-lookup"><span data-stu-id="1e716-346">Some of these parameters are:</span></span>

1. <span data-ttu-id="1e716-347">**基本**：</span><span class="sxs-lookup"><span data-stu-id="1e716-347">**Basics**:</span></span>
 * <span data-ttu-id="1e716-348">**名稱**: hello hello 資源 （hello 虛擬機器名稱） 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e716-348">**Name**: hello name of hello resource (hello virtual machine name).</span></span>
 * <span data-ttu-id="1e716-349">**VM 磁碟類型**： 選取 hello 的 hello OS 磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-349">**VM disk type**: Select hello disk type of hello OS disk.</span></span> <span data-ttu-id="1e716-350">如果您想 toouse 高階儲存體的資料磁碟時，建議使用進階儲存體的 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-350">If you want toouse Premium Storage for your data disks, we recommend using Premium Storage for hello OS disk as well.</span></span>
 * <span data-ttu-id="1e716-351">**使用者名稱和密碼**或**SSH 公開金鑰**: hello 使用者名稱和密碼的 hello 佈建期間建立的 hello 使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="1e716-351">**Username and password** or **SSH public key**: Enter hello username and password of hello user that is created during hello provisioning.</span></span> <span data-ttu-id="1e716-352">針對 Linux 虛擬機器，您可以輸入 hello toohello 機器用於 toosign 公開安全殼層 (SSH) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e716-352">For a Linux virtual machine, you can enter hello public Secure Shell (SSH) key that you use toosign in toohello machine.</span></span>
 * <span data-ttu-id="1e716-353">**訂用帳戶**： 選取您想要 toouse tooprovision hello 新虛擬機器的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-353">**Subscription**: Select hello subscription that you want toouse tooprovision hello new virtual machine.</span></span>
 * <span data-ttu-id="1e716-354">**資源群組**: hello hello 資源群組名稱 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-354">**Resource group**: hello name of hello resource group for hello VM.</span></span> <span data-ttu-id="1e716-355">您可以輸入新資源群組或 hello 名稱的資源群組已存在的任何一個 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e716-355">You can enter either hello name of a new resource group or hello name of a resource group that already exists.</span></span>
 * <span data-ttu-id="1e716-356">**位置**: toodeploy hello 新的虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-356">**Location**: Where toodeploy hello new virtual machine.</span></span> <span data-ttu-id="1e716-357">如果您想 tooconnect hello 虛擬機器 tooyour 在內部部署網路，請確定您選取 hello hello Azure tooyour 在內部部署網路連線的虛擬網路位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-357">If you want tooconnect hello virtual machine tooyour on-premises network, make sure you select hello location of hello virtual network that connects Azure tooyour on-premises network.</span></span> <span data-ttu-id="1e716-358">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的 [Microsoft Azure 網路][planning-guide-microsoft-azure-networking]。</span><span class="sxs-lookup"><span data-stu-id="1e716-358">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>
2. <span data-ttu-id="1e716-359">：</span><span class="sxs-lookup"><span data-stu-id="1e716-359">**Size**:</span></span>

     <span data-ttu-id="1e716-360">如需支援的 VM 類型清單，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="1e716-360">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="1e716-361">請確定您選取 hello 正確的 VM 類型，如果您想 toouse Azure 高階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-361">Be sure you select hello correct VM type if you want toouse Azure Premium Storage.</span></span> <span data-ttu-id="1e716-362">並非所有 VM 類型都支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-362">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="1e716-363">如需詳細資訊，請參閱[Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的[儲存體：Microsoft Azure 儲存體和資料磁碟][planning-guide-storage-microsoft-azure-storage-and-data-disks]和 [Azure 進階儲存體][planning-guide-azure-premium-storage]。</span><span class="sxs-lookup"><span data-stu-id="1e716-363">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

3. <span data-ttu-id="1e716-364">**設定**：</span><span class="sxs-lookup"><span data-stu-id="1e716-364">**Settings**:</span></span>
  * <span data-ttu-id="1e716-365">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="1e716-365">**Storage**</span></span>
    * <span data-ttu-id="1e716-366">**磁碟類型**： 選取 hello 的 hello OS 磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-366">**Disk Type**: Select hello disk type of hello OS disk.</span></span> <span data-ttu-id="1e716-367">如果您想 toouse 高階儲存體的資料磁碟時，建議使用進階儲存體的 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-367">If you want toouse Premium Storage for your data disks, we recommend using Premium Storage for hello OS disk as well.</span></span>
    * <span data-ttu-id="1e716-368">**使用受管理的磁碟**： 如果您想 toouse 管理磁碟，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="1e716-368">**Use managed disks**: If you want toouse Managed Disks, select Yes.</span></span> <span data-ttu-id="1e716-369">如需有關管理磁碟的詳細資訊，請參閱第章[管理磁碟][ planning-guide-managed-disks] hello 規劃指南中。</span><span class="sxs-lookup"><span data-stu-id="1e716-369">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in hello planning guide.</span></span>
  * <span data-ttu-id="1e716-370">**網路**</span><span class="sxs-lookup"><span data-stu-id="1e716-370">**Network**</span></span>
    * <span data-ttu-id="1e716-371">**虛擬網路**和**子網路**: toointegrate hello 虛擬機器與您的內部網路連線的 tooyour 在內部部署網路選取 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-371">**Virtual network** and **Subnet**: toointegrate hello virtual machine with your intranet, select hello virtual network that is connected tooyour on-premises network.</span></span>
    * <span data-ttu-id="1e716-372">**公用 IP 位址**： 選取 hello 公用 IP 位址，您想 toouse，或輸入參數 toocreate 新的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1e716-372">**Public IP address**: Select hello public IP address that you want toouse, or enter parameters toocreate a new public IP address.</span></span> <span data-ttu-id="1e716-373">您可以透過 hello 網際網路使用公用 IP 位址 tooaccess 您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-373">You can use a public IP address tooaccess your virtual machine over hello Internet.</span></span> <span data-ttu-id="1e716-374">請確定，您也可以建立網路安全性群組 toohelp 安全存取 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-374">Make sure that you also create a network security group toohelp secure access tooyour virtual machine.</span></span>
    * <span data-ttu-id="1e716-375">**網路安全性群組**：如需詳細資訊，請參閱[使用網路安全性群組控制網路流量流程][virtual-networks-nsg]。</span><span class="sxs-lookup"><span data-stu-id="1e716-375">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
  * <span data-ttu-id="1e716-376">**擴充功能**： 您可以藉由加入 toohello 部署中安裝虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1e716-376">**Extensions**: You can install virtual machine extensions by adding them toohello deployment.</span></span> <span data-ttu-id="1e716-377">您不需要在此步驟中 tooadd 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1e716-377">You do not need tooadd extension in this step.</span></span> <span data-ttu-id="1e716-378">所需的 SAP 支援的 hello 延伸模組會安裝更新版本。</span><span class="sxs-lookup"><span data-stu-id="1e716-378">hello extensions required for SAP support are installed later.</span></span> <span data-ttu-id="1e716-379">請參閱第章[設定 hello Azure 強化監視功能延伸模組適用於 SAP] [ deployment-guide-4.5]本指南中。</span><span class="sxs-lookup"><span data-stu-id="1e716-379">See chapter [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span></span>
  * <span data-ttu-id="1e716-380">**高可用性**： 選擇可用性設定組，或輸入 hello 參數 toocreate 新的可用性設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-380">**High Availability**: Select an availability set, or enter hello parameters toocreate a new availability set.</span></span> <span data-ttu-id="1e716-381">如需詳細資訊，請參閱 [Azure 可用性設定組][planning-guide-3.2.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-381">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
  * <span data-ttu-id="1e716-382">**監視**</span><span class="sxs-lookup"><span data-stu-id="1e716-382">**Monitoring**</span></span>
    * <span data-ttu-id="1e716-383">**開機診斷**︰您可以選取 [停用] 開機診斷。</span><span class="sxs-lookup"><span data-stu-id="1e716-383">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span></span>
    * <span data-ttu-id="1e716-384">**客體 OS 診斷**︰您可以選取 [停用] 監視診斷。</span><span class="sxs-lookup"><span data-stu-id="1e716-384">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span></span>

4. <span data-ttu-id="1e716-385">**摘要**：</span><span class="sxs-lookup"><span data-stu-id="1e716-385">**Summary**:</span></span>

  <span data-ttu-id="1e716-386">檢閱您的選取項目，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1e716-386">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="1e716-387">您的虛擬機器部署在您選取的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e716-387">Your virtual machine is deployed in hello resource group you selected.</span></span>
#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="1e716-388">使用範本建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e716-388">Create a virtual machine by using a template</span></span>
<span data-ttu-id="1e716-389">toocreate 使用私用 hello Azure 入口網站，從作業系統映像的部署使用其中一個 hello 遵循 SAP 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-389">toocreate a deployment by using a private OS image from hello Azure portal, use one of hello following SAP templates.</span></span> <span data-ttu-id="1e716-390">在 hello 中發佈這些範本[azure-快速入門範本 GitHub 儲存機制][azure-quickstart-templates-github]。</span><span class="sxs-lookup"><span data-stu-id="1e716-390">These templates are published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="1e716-391">您可以也使用 [PowerShell][virtual-machines-upload-image-windows-resource-manager] 手動建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-391">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="1e716-392">[**兩層組態 (僅限一部虛擬機器) 範本** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="1e716-392">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="1e716-393">toocreate 兩層式系統使用只有一部虛擬機器，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-393">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="1e716-394">[**兩層組態 (僅只一部虛擬機器) 範本 - 受管理磁碟映像** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]</span><span class="sxs-lookup"><span data-stu-id="1e716-394">[**Two-tier configuration (only one virtual machine) template - Managed Disk Image** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]</span></span>

  <span data-ttu-id="1e716-395">toocreate 兩層式系統使用只有一部虛擬機器和受管理的磁碟映像，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-395">toocreate a two-tier system by using only one virtual machine and a Managed Disk image, use this template.</span></span>
* <span data-ttu-id="1e716-396">[**三層組態 (多部虛擬機器) 範本** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="1e716-396">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="1e716-397">toocreate 三層式系統使用多部虛擬機器或您自己的作業系統映像，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-397">toocreate a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>
* <span data-ttu-id="1e716-398">[**三層組態 (多部虛擬機器) 範本 - 受管理磁碟映像** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]</span><span class="sxs-lookup"><span data-stu-id="1e716-398">[**Three-tier configuration (multiple virtual machines) template - Managed Disk Image** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]</span></span>

  <span data-ttu-id="1e716-399">toocreate 三層式系統使用多部虛擬機器或您自己的作業系統映像和受管理的磁碟映像，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-399">toocreate a three-tier system by using multiple virtual machines or your own OS image and a Managed Disk image, use this template.</span></span>

<span data-ttu-id="1e716-400">在 hello Azure 入口網站中，輸入下列 hello 範本參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-400">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="1e716-401">**基本**：</span><span class="sxs-lookup"><span data-stu-id="1e716-401">**Basics**:</span></span>
  * <span data-ttu-id="1e716-402">**訂用帳戶**: hello 訂用帳戶 toouse toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-402">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="1e716-403">**資源群組**: hello 資源群組 toouse toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-403">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="1e716-404">您可以建立新的資源群組，或選取現有的資源群組 hello 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1e716-404">You can create a new resource group or select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="1e716-405">**位置**: toodeploy hello 範本的位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-405">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="1e716-406">如果您選取現有的資源群組時，會使用該資源群組中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-406">If you selected an existing resource group, hello location of that resource group is used.</span></span>
2. <span data-ttu-id="1e716-407">**設定**：</span><span class="sxs-lookup"><span data-stu-id="1e716-407">**Settings**:</span></span>
  * <span data-ttu-id="1e716-408">**SAP 系統識別碼**: hello SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-408">**SAP System ID**: hello SAP System ID.</span></span>
  * <span data-ttu-id="1e716-409">**OS 類型**: hello 想 toodeploy （Windows 或 Linux） 的作業系統類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-409">**OS type**: hello operating system type you want toodeploy (Windows or Linux).</span></span>
  * <span data-ttu-id="1e716-410">**SAP 系統大小**: hello hello SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="1e716-410">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="1e716-411">提供的 SAPS hello 新系統的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1e716-411">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="1e716-412">如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="1e716-412">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="1e716-413">**系統可用性**（三層式範本）： hello 系統可用性。</span><span class="sxs-lookup"><span data-stu-id="1e716-413">**System availability** (three-tier template only): hello system availability.</span></span>

    <span data-ttu-id="1e716-414">選取適合高可用性安裝組態的 **HA**。</span><span class="sxs-lookup"><span data-stu-id="1e716-414">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="1e716-415">為 ASCS 建立兩部資料庫伺服器和兩部伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e716-415">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="1e716-416">**儲存體類型**（僅限兩層式範本）： hello 的儲存體 toouse 型別。</span><span class="sxs-lookup"><span data-stu-id="1e716-416">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="1e716-417">對於大型系統，我們強烈建議使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-417">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="1e716-418">如需存放裝置類型的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-418">For more information about storage types, see hello following resources:</span></span>
      * <span data-ttu-id="1e716-419">[針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]</span><span class="sxs-lookup"><span data-stu-id="1e716-419">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="1e716-420">[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="1e716-420">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="1e716-421">[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="1e716-421">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="1e716-422">[簡介 tooMicrosoft Azure 儲存體][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="1e716-422">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="1e716-423">**使用者映像 VHD URI** （僅限不受管理的磁碟映像範本）： hello 的 hello 私人 OS 映像 VHD，例如 https:// URI&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd。</span><span class="sxs-lookup"><span data-stu-id="1e716-423">**User image VHD URI** (unmanaged disk image template only): hello URI of hello private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="1e716-424">**使用者映像儲存體帳戶**（僅限不受管理的磁碟映像範本）： hello hello 私人 OS 映像儲存的位置，例如的 hello 儲存體帳戶名稱&lt;accountname > 中 https://&lt;accountname >。blob.core.windows.net/vhds/userimage.vhd。</span><span class="sxs-lookup"><span data-stu-id="1e716-424">**User image storage account** (unmanaged disk image template only): hello name of hello storage account where hello private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="1e716-425">**userImageId** （僅限受管理的磁碟映像範本）： hello 想 toouse 的受管理的磁碟映像的識別碼</span><span class="sxs-lookup"><span data-stu-id="1e716-425">**userImageId** (managed disk image template only): Id of hello Managed Disk image you want toouse</span></span>
  * <span data-ttu-id="1e716-426">**系統管理員使用者名稱**和**系統管理員密碼**: hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-426">**Admin username** and **Admin password**: hello username and password.</span></span>

    <span data-ttu-id="1e716-427">建立新的使用者，登入 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-427">A new user is created, for signing in toohello virtual machine.</span></span>
  * <span data-ttu-id="1e716-428">**新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-428">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="1e716-429">如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。</span><span class="sxs-lookup"><span data-stu-id="1e716-429">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="1e716-430">**子網路識別碼**: hello 識別碼 hello 子網路 toowhich hello 虛擬機器會連接到。</span><span class="sxs-lookup"><span data-stu-id="1e716-430">**Subnet ID**: hello ID of hello subnet toowhich hello virtual machines will connect to.</span></span> <span data-ttu-id="1e716-431">選取您的 VPN 或 ExpressRoute 虛擬網路 toouse tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-431">Select hello subnet of your VPN or ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="1e716-432">hello 識別碼通常看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1e716-432">hello ID usually looks like this:</span></span>

    <span data-ttu-id="1e716-433">/subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱></span><span class="sxs-lookup"><span data-stu-id="1e716-433">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="1e716-434">**條款及條件**：</span><span class="sxs-lookup"><span data-stu-id="1e716-434">**Terms and conditions**:</span></span>  
    <span data-ttu-id="1e716-435">檢閱並接受 hello 法律條款。</span><span class="sxs-lookup"><span data-stu-id="1e716-435">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="1e716-436">選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="1e716-436">Select **Purchase**.</span></span>

#### <a name="install-hello-vm-agent-linux-only"></a><span data-ttu-id="1e716-437">安裝 VM 代理程式 (只有 Linux) hello</span><span class="sxs-lookup"><span data-stu-id="1e716-437">Install hello VM Agent (Linux only)</span></span>
<span data-ttu-id="1e716-438">toouse hello 範本 hello 前面一節中所述，hello hello 使用者映像或 hello 部署中必須已安裝 Linux 代理程式將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1e716-438">toouse hello templates described in hello preceding section, hello Linux Agent must already be installed in hello user image, or hello deployment will fail.</span></span> <span data-ttu-id="1e716-439">下載並安裝 hello 使用者映像中的 hello VM 代理程式中所述[下載、 安裝及啟用 hello Azure VM 代理程式][deployment-guide-4.4]。</span><span class="sxs-lookup"><span data-stu-id="1e716-439">Download and install hello VM Agent in hello user image as described in [Download, install, and enable hello Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="1e716-440">如果您不使用 hello 範本，您也可以安裝 hello VM 代理程式更新版本。</span><span class="sxs-lookup"><span data-stu-id="1e716-440">If you don’t use hello templates, you also can install hello VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="1e716-441">加入網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="1e716-441">Join a domain (Windows only)</span></span>
<span data-ttu-id="1e716-442">如果您的 Azure 部署連接的 tooan 在內部部署 Active Directory 或 DNS 執行個體已透過 Azure 站台對站 VPN 連線或 Azure ExpressRoute (這稱為*跨單位*中[Azure 虛擬機器規劃和實作的 SAP NetWeaver][planning-guide])，預期該 hello VM 加入內部網域。</span><span class="sxs-lookup"><span data-stu-id="1e716-442">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="1e716-443">如需這個步驟的考量的詳細資訊，請參閱[加入 VM tooan 在內部部署網域 (僅限 Windows)][deployment-guide-4.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-443">For more information about considerations for this step, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="1e716-444">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="1e716-444">Configure proxy settings</span></span>
<span data-ttu-id="1e716-445">根據您在內部部署網路的設定方式，您可能需要在 VM 上的 tooset hello proxy。</span><span class="sxs-lookup"><span data-stu-id="1e716-445">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="1e716-446">如果 VM 是透過 VPN 或 ExpressRoute 連線的 tooyour 在內部部署網路，hello VM 可能不是可以 tooaccess hello 網際網路，和不可以 toodownload hello 所需的擴充功能或收集的監視資料。</span><span class="sxs-lookup"><span data-stu-id="1e716-446">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="1e716-447">如需詳細資訊，請參閱[設定 hello proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="1e716-447">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="1e716-448">設定監視</span><span class="sxs-lookup"><span data-stu-id="1e716-448">Configure monitoring</span></span>
<span data-ttu-id="1e716-449">確定 SAP 支援您的環境中所述設定 hello Azure Monitoring Extension for SAP toobe[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="1e716-449">toobe sure SAP supports your environment, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1e716-450">檢查 SAP monitoring，和最低要求版本的 SAP 核心與 SAP Host Agent，在 hello 中列出的資源中的 hello 必要條件[SAP 資源][deployment-guide-2.2]。</span><span class="sxs-lookup"><span data-stu-id="1e716-450">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="1e716-451">監視檢查</span><span class="sxs-lookup"><span data-stu-id="1e716-451">Monitoring check</span></span>
<span data-ttu-id="1e716-452">如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="1e716-452">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>


### <span data-ttu-id="1e716-453"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>案例 3：使用非一般化 Azure VHD 搭配 SAP 來移動內部部署 VM</span><span class="sxs-lookup"><span data-stu-id="1e716-453"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="1e716-454">在此案例中，您計劃 toomove 特定 SAP 系統從內部部署環境 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1e716-454">In this scenario, you plan toomove a specific SAP system from an on-premises environment tooAzure.</span></span> <span data-ttu-id="1e716-455">您可以執行這項操作 hello hello OS，hello SAP 二進位檔，VHD 上傳及最終 hello DBMS 二進位檔，再加上 hello Vhd hello 資料和記錄檔的 hello tooAzure 的 DBMS。</span><span class="sxs-lookup"><span data-stu-id="1e716-455">You can do this by uploading hello VHD that has hello OS, hello SAP binaries, and eventually hello DBMS binaries, plus hello VHDs with hello data and log files of hello DBMS, tooAzure.</span></span> <span data-ttu-id="1e716-456">不同於中所述的 hello 案例[案例 2： 使用部署 VM 的自訂映像為 SAP][deployment-guide-3.3]、 在此情況下，保留 hello 主機名稱、 SAP SID 和 SAP 使用者帳戶在 hello Azure VM 中，所以它們在 hello 在內部部署環境中設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-456">Unlike hello scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep hello hostname, SAP SID, and SAP user accounts in hello Azure VM, because they were configured in hello on-premises environment.</span></span> <span data-ttu-id="1e716-457">您不需要 toogeneralize hello OS。</span><span class="sxs-lookup"><span data-stu-id="1e716-457">You do not need toogeneralize hello OS.</span></span> <span data-ttu-id="1e716-458">此案例適用於最常 toocross 內部部署案例，其中 hello SAP 環境的一部分執行的內部部署和在 Azure 上執行的一部分。</span><span class="sxs-lookup"><span data-stu-id="1e716-458">This scenario applies most often toocross-premises scenarios where part of hello SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="1e716-459">在此案例中，hello VM 代理程式是**不**在部署期間自動安裝。</span><span class="sxs-lookup"><span data-stu-id="1e716-459">In this scenario, hello VM Agent is **not** automatically installed during deployment.</span></span> <span data-ttu-id="1e716-460">因為 hello VM 代理程式 」 和 「 hello Azure 強化監視功能延伸模組適用於 SAP 必要的 toorun SAP NetWeaver on Azure，您需要 toodownload、 安裝和啟用這兩個元件建立 hello 虛擬機器之後，以手動方式。</span><span class="sxs-lookup"><span data-stu-id="1e716-460">Because hello VM Agent and hello Azure Enhanced Monitoring Extension for SAP are required toorun SAP NetWeaver on Azure, you need toodownload, install, and enable both components manually after you create hello virtual machine.</span></span>

<span data-ttu-id="1e716-461">如需 hello Azure VM 代理程式的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e716-461">For more information about hello Azure VM Agent, see hello following resources.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="1e716-463">Windows</span><span class="sxs-lookup"><span data-stu-id="1e716-463">Windows</span></span>
>
> <span data-ttu-id="1e716-464">[Azure 虛擬機器代理程式概觀][virtual-machines-windows-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="1e716-464">[Azure Virtual Machine Agent overview][virtual-machines-windows-agent-user-guide]</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="1e716-466">Linux</span><span class="sxs-lookup"><span data-stu-id="1e716-466">Linux</span></span>
>
> <span data-ttu-id="1e716-467">[Azure Linux 代理程式使用者指南][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="1e716-467">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="1e716-468">下列流程圖顯示 hello 順序的步驟，使用非一般化 Azure VHD 移動內部部署 VM 的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-468">hello following flowchart shows hello sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![使用 VM 磁碟部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-400]

<span data-ttu-id="1e716-470">如果已上傳並在 Azure 中定義 hello 磁碟 (請參閱[Azure 虛擬機器規劃和實作的 SAP NetWeaver][planning-guide])，請勿 hello 工作中所述 hello 接下來的幾個章節。</span><span class="sxs-lookup"><span data-stu-id="1e716-470">If hello disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), do hello tasks described in hello next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="1e716-471">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e716-471">Create a virtual machine</span></span>
<span data-ttu-id="1e716-472">toocreate 使用私用的作業系統磁碟，透過 hello Azure 入口網站的部署使用 hello SAP 範本發行在 hello [azure-快速入門範本 GitHub 儲存機制][azure-quickstart-templates-github]。</span><span class="sxs-lookup"><span data-stu-id="1e716-472">toocreate a deployment by using a private OS disk through hello Azure portal, use hello SAP template published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="1e716-473">您可以也使用 PowerShell 手動建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-473">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="1e716-474">[**兩層組態 (僅限一部虛擬機器) 範本**  (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="1e716-474">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="1e716-475">toocreate 兩層式系統使用只有一部虛擬機器，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-475">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="1e716-476">[**兩層組態 (僅限一部虛擬機器) 範本 - 受管理磁碟** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]</span><span class="sxs-lookup"><span data-stu-id="1e716-476">[**Two-tier configuration (only one virtual machine) template - Managed Disk** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]</span></span>

  <span data-ttu-id="1e716-477">toocreate 兩層式系統使用只有一部虛擬機器和受管理的磁碟，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-477">toocreate a two-tier system by using only one virtual machine and a Managed Disk, use this template.</span></span>

<span data-ttu-id="1e716-478">在 hello Azure 入口網站中，輸入下列 hello 範本參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-478">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="1e716-479">**基本**：</span><span class="sxs-lookup"><span data-stu-id="1e716-479">**Basics**:</span></span>
  * <span data-ttu-id="1e716-480">**訂用帳戶**: hello 訂用帳戶 toouse toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-480">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="1e716-481">**資源群組**: hello 資源群組 toouse toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1e716-481">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="1e716-482">您可以建立新的資源群組，或選取現有的資源群組 hello 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1e716-482">You can create a new resource group or select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="1e716-483">**位置**: toodeploy hello 範本的位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-483">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="1e716-484">如果您選取現有的資源群組時，會使用該資源群組中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="1e716-484">If you selected an existing resource group, hello location of that resource group is used.</span></span>
2. <span data-ttu-id="1e716-485">**設定**：</span><span class="sxs-lookup"><span data-stu-id="1e716-485">**Settings**:</span></span>
  * <span data-ttu-id="1e716-486">**SAP 系統識別碼**: hello SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-486">**SAP System ID**: hello SAP System ID.</span></span>
  * <span data-ttu-id="1e716-487">**OS 類型**: hello 想 toodeploy （Windows 或 Linux） 的作業系統類型。</span><span class="sxs-lookup"><span data-stu-id="1e716-487">**OS type**: hello operating system type you want toodeploy (Windows or Linux).</span></span>
  * <span data-ttu-id="1e716-488">**SAP 系統大小**: hello hello SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="1e716-488">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="1e716-489">提供的 SAPS hello 新系統的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1e716-489">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="1e716-490">如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="1e716-490">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="1e716-491">**儲存體類型**（僅限兩層式範本）： hello 的儲存體 toouse 型別。</span><span class="sxs-lookup"><span data-stu-id="1e716-491">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="1e716-492">對於大型系統，我們強烈建議使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e716-492">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="1e716-493">如需存放裝置類型的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-493">For more information about storage types, see hello following resources:</span></span>
      * <span data-ttu-id="1e716-494">[針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]</span><span class="sxs-lookup"><span data-stu-id="1e716-494">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="1e716-495">[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="1e716-495">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="1e716-496">[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="1e716-496">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="1e716-497">[簡介 tooMicrosoft Azure 儲存體][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="1e716-497">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="1e716-498">**作業系統磁碟 VHD URI** （僅限 unmanaged 的磁碟範本）： hello 的 hello 的私用作業系統磁碟，而例如 https:// URI&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd。</span><span class="sxs-lookup"><span data-stu-id="1e716-498">**OS disk VHD URI** (unmanaged disk template only): hello URI of hello private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="1e716-499">**作業系統磁碟管理磁碟識別碼**（僅限受管理的磁碟範本）： hello hello 管理磁碟作業系統磁碟的識別碼，/subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN</span><span class="sxs-lookup"><span data-stu-id="1e716-499">**OS disk Managed Disk Id** (managed disk template only): hello Id of hello Managed Disk OS disk, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN</span></span>
  * <span data-ttu-id="1e716-500">**新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-500">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="1e716-501">如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。</span><span class="sxs-lookup"><span data-stu-id="1e716-501">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="1e716-502">**子網路識別碼**: hello 識別碼 hello 子網路 toowhich hello 虛擬機器會連接到。</span><span class="sxs-lookup"><span data-stu-id="1e716-502">**Subnet ID**: hello ID of hello subnet toowhich hello virtual machines will connect to.</span></span> <span data-ttu-id="1e716-503">選取您的 VPN、 Azure ExpressRoute 虛擬網路 toouse tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-503">Select hello subnet of your VPN or Azure ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="1e716-504">hello 識別碼通常看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1e716-504">hello ID usually looks like this:</span></span>

    <span data-ttu-id="1e716-505">/subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱></span><span class="sxs-lookup"><span data-stu-id="1e716-505">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="1e716-506">**條款及條件**：</span><span class="sxs-lookup"><span data-stu-id="1e716-506">**Terms and conditions**:</span></span>  
    <span data-ttu-id="1e716-507">檢閱並接受 hello 法律條款。</span><span class="sxs-lookup"><span data-stu-id="1e716-507">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="1e716-508">選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="1e716-508">Select **Purchase**.</span></span>

#### <a name="install-hello-vm-agent"></a><span data-ttu-id="1e716-509">安裝 VM 代理程式 hello</span><span class="sxs-lookup"><span data-stu-id="1e716-509">Install hello VM Agent</span></span>
<span data-ttu-id="1e716-510">範本中所述的 toouse hello hello 上一節、 hello VM 代理程式必須安裝在 hello 作業系統磁碟或 hello 部署將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1e716-510">toouse hello templates described in hello preceding section, hello VM Agent must be installed on hello OS disk, or hello deployment will fail.</span></span> <span data-ttu-id="1e716-511">下載並安裝在 hello VM 中的 hello VM 代理程式中所述[下載、 安裝及啟用 hello Azure VM 代理程式][deployment-guide-4.4]。</span><span class="sxs-lookup"><span data-stu-id="1e716-511">Download and install hello VM Agent in hello VM, as described in [Download, install, and enable hello Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="1e716-512">如果您不使用 hello 範本 hello 前面一節中所述，您也可以安裝 hello VM 代理程式之後。</span><span class="sxs-lookup"><span data-stu-id="1e716-512">If you don't use hello templates described in hello preceding section, you can also install hello VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="1e716-513">加入網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="1e716-513">Join a domain (Windows only)</span></span>
<span data-ttu-id="1e716-514">如果您的 Azure 部署連接的 tooan 在內部部署 Active Directory 或 DNS 執行個體已透過 Azure 站台對站 VPN 連線或 ExpressRoute (這稱為*跨單位*中[規劃 Azure 虛擬機器與實作的 SAP NetWeaver][planning-guide])，預期該 hello VM 加入內部網域。</span><span class="sxs-lookup"><span data-stu-id="1e716-514">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="1e716-515">如需考量這項工作的詳細資訊，請參閱[加入 VM tooan 在內部部署網域 (僅限 Windows)][deployment-guide-4.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-515">For more information about considerations for this task, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="1e716-516">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="1e716-516">Configure proxy settings</span></span>
<span data-ttu-id="1e716-517">根據您在內部部署網路的設定方式，您可能需要在 VM 上的 tooset hello proxy。</span><span class="sxs-lookup"><span data-stu-id="1e716-517">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="1e716-518">如果 VM 是透過 VPN 或 ExpressRoute 連線的 tooyour 在內部部署網路，hello VM 可能不是可以 tooaccess hello 網際網路，和不可以 toodownload hello 所需的擴充功能或收集的監視資料。</span><span class="sxs-lookup"><span data-stu-id="1e716-518">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="1e716-519">如需詳細資訊，請參閱[設定 hello proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="1e716-519">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="1e716-520">設定監視</span><span class="sxs-lookup"><span data-stu-id="1e716-520">Configure monitoring</span></span>
<span data-ttu-id="1e716-521">確定 SAP 支援您的環境中所述設定 hello Azure Monitoring Extension for SAP toobe[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="1e716-521">toobe sure SAP supports your environment, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1e716-522">檢查 SAP monitoring，和最低要求版本的 SAP 核心與 SAP Host Agent，在 hello 中列出的資源中的 hello 必要條件[SAP 資源][deployment-guide-2.2]。</span><span class="sxs-lookup"><span data-stu-id="1e716-522">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="1e716-523">監視檢查</span><span class="sxs-lookup"><span data-stu-id="1e716-523">Monitoring check</span></span>
<span data-ttu-id="1e716-524">如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="1e716-524">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-hello-monitoring-configuration-for-sap"></a><span data-ttu-id="1e716-525">更新 hello 適用於 SAP 的監視設定</span><span class="sxs-lookup"><span data-stu-id="1e716-525">Update hello monitoring configuration for SAP</span></span>
<span data-ttu-id="1e716-526">更新任何下列案例的 hello hello SAP 監視組態：</span><span class="sxs-lookup"><span data-stu-id="1e716-526">Update hello SAP monitoring configuration in any of hello following scenarios:</span></span>
* <span data-ttu-id="1e716-527">hello 聯合 Microsoft/SAP 小組擴充監視功能的 hello，並要求更多或較少的計數器。</span><span class="sxs-lookup"><span data-stu-id="1e716-527">hello joint Microsoft/SAP team extends hello monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="1e716-528">Microsoft 導入了新版本的 hello 基礎的 Azure 基礎結構，提供 hello 監控資料，並針對 SAP 需求 toobe hello Azure 強化監視功能延伸模組調整 toothose 變更。</span><span class="sxs-lookup"><span data-stu-id="1e716-528">Microsoft introduces a new version of hello underlying Azure infrastructure that delivers hello monitoring data, and hello Azure Enhanced Monitoring Extension for SAP needs toobe adapted toothose changes.</span></span>
* <span data-ttu-id="1e716-529">裝載其他資料磁碟 tooyour Azure VM，或移除資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="1e716-529">You mount additional data disks tooyour Azure VM or you remove a data disk.</span></span> <span data-ttu-id="1e716-530">在此案例中，更新儲存體相關資料的 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="1e716-530">In this scenario, update hello collection of storage-related data.</span></span> <span data-ttu-id="1e716-531">變更組態，藉由加入或刪除端點或指派 IP 位址 tooa VM 不會影響 hello 監視設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-531">Changing your configuration by adding or deleting endpoints or by assigning IP addresses tooa VM does not affect hello monitoring configuration.</span></span>
* <span data-ttu-id="1e716-532">您變更 hello 您 Azure VM 的大小，例如大小 A5 tooany 從其他 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="1e716-532">You change hello size of your Azure VM, for example, from size A5 tooany other VM size.</span></span>
* <span data-ttu-id="1e716-533">您加入新的網路介面 tooyour Azure VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-533">You add new network interfaces tooyour Azure VM.</span></span>

<span data-ttu-id="1e716-534">中的監視設定，監視基礎結構，可遵循 hello 更新 hello tooupdate 步驟[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="1e716-534">tooupdate monitoring settings, update hello monitoring infrastructure by following hello steps in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment"></a><span data-ttu-id="1e716-535">SAP 軟體部署的詳細工作</span><span class="sxs-lookup"><span data-stu-id="1e716-535">Detailed tasks for SAP software deployment</span></span>
<span data-ttu-id="1e716-536">本節詳述執行 hello 組態和部署程序中的特定工作的步驟。</span><span class="sxs-lookup"><span data-stu-id="1e716-536">This section has detailed steps for doing specific tasks in hello configuration and deployment process.</span></span>

### <span data-ttu-id="1e716-537"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>部署 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="1e716-537"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="1e716-538">跳過[Microsoft Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="1e716-538">Go too[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="1e716-539">在**命令列工具**的 **PowerShell** 之下，選取 [Windows 安裝]。</span><span class="sxs-lookup"><span data-stu-id="1e716-539">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
3.  <span data-ttu-id="1e716-540">在 hello Microsoft 下載管理員對話方塊中，hello 下載檔案 (例如，WindowsAzurePowershellGet.3f.3f.3fnew.exe) 選取**執行**。</span><span class="sxs-lookup"><span data-stu-id="1e716-540">In hello Microsoft Download Manager dialog box, for hello downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="1e716-541">選取 Microsoft Web Platform Installer (Microsoft Web PI) toorun**是**。</span><span class="sxs-lookup"><span data-stu-id="1e716-541">toorun Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="1e716-542">如下所示的頁面隨即出現︰</span><span class="sxs-lookup"><span data-stu-id="1e716-542">A page that looks like this appears:</span></span>

  <span data-ttu-id="1e716-543">![Azure PowerShell Cmdlet 的安裝頁面][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-543">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="1e716-544">選取**安裝**，然後接受 hello Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="1e716-544">Select **Install**, and then accept hello Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="1e716-545">已安裝 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1e716-545">PowerShell is installed.</span></span> <span data-ttu-id="1e716-546">選取**完成**tooclose hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="1e716-546">Select **Finish** tooclose hello installation wizard.</span></span>

<span data-ttu-id="1e716-547">經常檢查有無更新 toohello PowerShell cmdlet，這通常每月更新。</span><span class="sxs-lookup"><span data-stu-id="1e716-547">Check frequently for updates toohello PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="1e716-548">hello 最簡單方式 toocheck 更新為先前的安裝步驟，在步驟 5 中所顯示的 toohello 安裝網頁註冊的 toodo hello。</span><span class="sxs-lookup"><span data-stu-id="1e716-548">hello easiest way toocheck for updates is toodo hello preceding installation steps, up toohello installation page shown in step 5.</span></span> <span data-ttu-id="1e716-549">hello 發行日期] 和 [發行 hello cmdlet 包含一些步驟 5 所示的 hello 頁面上。</span><span class="sxs-lookup"><span data-stu-id="1e716-549">hello release date and release number of hello cmdlets are included on hello page shown in step 5.</span></span> <span data-ttu-id="1e716-550">除非在 SAP 附註中指定，否則[1928533]或 SAP Note [2015553]，我們建議您搭配 hello 最新版 Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1e716-550">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with hello latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="1e716-551">toocheck hello 版的 hello Azure PowerShell cmdlet 安裝在您的電腦上執行這個 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="1e716-551">toocheck hello version of hello Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
(Get-Module AzureRm.Compute).Version
```
<span data-ttu-id="1e716-552">hello 結果看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1e716-552">hello result looks like this:</span></span>

<span data-ttu-id="1e716-553">![Azure PowerShell Cmdlet 版本檢查的結果][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-553">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="1e716-554">Hello hello 安裝精靈的第一頁 hello 目前版本在電腦上安裝的 hello Azure cmdlet 版本時，將代表它**（安裝）** toohello 產品標題 （請參閱下列螢幕擷取畫面的 hello）。</span><span class="sxs-lookup"><span data-stu-id="1e716-554">If hello Azure cmdlet version installed on your computer is hello current version, hello first page of hello installation wizard indicates it by adding **(Installed)** toohello product title (see hello following screenshot).</span></span> <span data-ttu-id="1e716-555">您的 PowerShell Azure Cmdlet 都是最新的。</span><span class="sxs-lookup"><span data-stu-id="1e716-555">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="1e716-556">tooclose hello 安裝精靈中，選取**結束**。</span><span class="sxs-lookup"><span data-stu-id="1e716-556">tooclose hello installation wizard, select **Exit**.</span></span>

<span data-ttu-id="1e716-557">![安裝 Azure PowerShell cmdlet，指出該 hello 最新版本的 Azure PowerShell cmdlet 的安裝頁面][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-557">![Installation page for Azure PowerShell cmdlets indicating that hello most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <span data-ttu-id="1e716-558"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>部署 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1e716-558"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Deploy Azure CLI</span></span>
1.  <span data-ttu-id="1e716-559">跳過[Microsoft Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="1e716-559">Go too[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="1e716-560">在下**命令列工具**下**Azure 命令列介面**，選取 hello**安裝**適用於您作業系統的連結。</span><span class="sxs-lookup"><span data-stu-id="1e716-560">Under **Command-line tools**, under **Azure command-line interface**, select hello **Install** link for your operating system.</span></span>
3.  <span data-ttu-id="1e716-561">在 hello Microsoft 下載管理員對話方塊中，hello 下載檔案 (例如，WindowsAzureXPlatCLI.3f.3f.3fnew.exe) 選取**執行**。</span><span class="sxs-lookup"><span data-stu-id="1e716-561">In hello Microsoft Download Manager dialog box, for hello downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="1e716-562">選取 Microsoft Web Platform Installer (Microsoft Web PI) toorun**是**。</span><span class="sxs-lookup"><span data-stu-id="1e716-562">toorun Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="1e716-563">如下所示的頁面隨即出現︰</span><span class="sxs-lookup"><span data-stu-id="1e716-563">A page that looks like this appears:</span></span>

  <span data-ttu-id="1e716-564">![Azure PowerShell Cmdlet 的安裝頁面][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-564">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="1e716-565">選取**安裝**，然後接受 hello Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="1e716-565">Select **Install**, and then accept hello Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="1e716-566">已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="1e716-566">Azure CLI is installed.</span></span> <span data-ttu-id="1e716-567">選取**完成**tooclose hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="1e716-567">Select **Finish** tooclose hello installation wizard.</span></span>

<span data-ttu-id="1e716-568">經常檢查有無更新 tooAzure CLI，通常每月更新。</span><span class="sxs-lookup"><span data-stu-id="1e716-568">Check frequently for updates tooAzure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="1e716-569">hello 最簡單方式 toocheck 更新為先前的安裝步驟，在步驟 5 中所顯示的 toohello 安裝網頁註冊的 toodo hello。</span><span class="sxs-lookup"><span data-stu-id="1e716-569">hello easiest way toocheck for updates is toodo hello preceding installation steps, up toohello installation page shown in step 5.</span></span>

<span data-ttu-id="1e716-570">您的電腦已安裝的 Azure CLI toocheck hello 版本會執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="1e716-570">toocheck hello version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="1e716-571">hello 結果看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1e716-571">hello result looks like this:</span></span>

<span data-ttu-id="1e716-572">![Azure CLI 版本檢查的結果][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-572">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <span data-ttu-id="1e716-573"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>加入 VM tooan 在內部部署網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="1e716-573"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Join a VM tooan on-premises domain (Windows only)</span></span>
<span data-ttu-id="1e716-574">如果您將 SAP Vm 部署在跨內部單位案例中，在內部部署 Active Directory 和 DNS 在 Azure 中，擴充其中預期 hello Vm 加入內部網域。</span><span class="sxs-lookup"><span data-stu-id="1e716-574">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that hello VMs are joining an on-premises domain.</span></span> <span data-ttu-id="1e716-575">hello 採取 toojoin VM tooan 在內部部署網域的詳細的步驟和 hello 需要其他軟體 toobe 在內部部署網域的成員會因客戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-575">hello detailed steps you take toojoin a VM tooan on-premises domain, and hello additional software required toobe a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="1e716-576">通常，toojoin VM tooan 內部部署網域，您需要 tooinstall 其他軟體，例如反惡意程式碼軟體及備份或監視軟體。</span><span class="sxs-lookup"><span data-stu-id="1e716-576">Usually, toojoin a VM tooan on-premises domain, you need tooinstall additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="1e716-577">在此案例中，您也需要 toomake 確定 VM 加入您的環境中的網域時，會強制執行網際網路 proxy 設定，如果有本機系統帳戶 (S-1-5-18) hello 客體 VM 中的 hello Windows hello 相同的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-577">In this scenario, you also need toomake sure that if Internet proxy settings are forced when a VM joins a domain in your environment, hello Windows Local System Account (S-1-5-18) in hello Guest VM has hello same proxy settings.</span></span> <span data-ttu-id="1e716-578">hello 最簡單的選項是使用網域群組原則，套用在 hello 網域 toosystems tooforce hello proxy。</span><span class="sxs-lookup"><span data-stu-id="1e716-578">hello easiest option is tooforce hello proxy by using a domain Group Policy, which applies toosystems in hello domain.</span></span>

### <span data-ttu-id="1e716-579"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>下載、 安裝及啟用 hello Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="1e716-579"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Download, install, and enable hello Azure VM Agent</span></span>
<span data-ttu-id="1e716-580">從無法一般化 （例如映像中的 hello Windows 系統準備或 sysprep 工具不會產生） 的作業系統映像部署的虛擬機器，您需要 toomanually 下載、 安裝和啟用 hello Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-580">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in hello Windows System Preparation, or sysprep, tool), you need toomanually download, install, and enable hello Azure VM Agent.</span></span>

<span data-ttu-id="1e716-581">如果您部署的 hello Azure Marketplace 的 VM 時，就不需要此步驟。</span><span class="sxs-lookup"><span data-stu-id="1e716-581">If you deploy a VM from hello Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="1e716-582">Hello Azure Marketplace 映像已擁有 hello Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-582">Images from hello Azure Marketplace already have hello Azure VM Agent.</span></span>

#### <span data-ttu-id="1e716-583"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span><span class="sxs-lookup"><span data-stu-id="1e716-583"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span></span>
1.  <span data-ttu-id="1e716-584">下載 hello Azure VM 代理程式：</span><span class="sxs-lookup"><span data-stu-id="1e716-584">Download hello Azure VM Agent:</span></span>
  1.  <span data-ttu-id="1e716-585">下載 hello [Azure VM 代理程式安裝程式套件](https://go.microsoft.com/fwlink/?LinkId=394789)。</span><span class="sxs-lookup"><span data-stu-id="1e716-585">Download hello [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  2.  <span data-ttu-id="1e716-586">在個人電腦或伺服器上的本機儲存 hello VM 代理程式 MSI 封裝。</span><span class="sxs-lookup"><span data-stu-id="1e716-586">Store hello VM Agent MSI package locally on a personal computer or server.</span></span>
2.  <span data-ttu-id="1e716-587">安裝 hello Azure VM 代理程式：</span><span class="sxs-lookup"><span data-stu-id="1e716-587">Install hello Azure VM Agent:</span></span>
  1.  <span data-ttu-id="1e716-588">連接 toohello 使用遠端桌面通訊協定 (RDP) 來部署 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="1e716-588">Connect toohello deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  2.  <span data-ttu-id="1e716-589">開啟 hello VM 上的 Windows 檔案總管 視窗，然後選取 hello hello 的 hello VM 代理程式的 MSI 檔案的目標目錄。</span><span class="sxs-lookup"><span data-stu-id="1e716-589">Open a Windows Explorer window on hello VM and select hello target directory for hello MSI file of hello VM Agent.</span></span>
  3.  <span data-ttu-id="1e716-590">拖曳 hello hello VM 代理程式在 hello VM 上的本機電腦/伺服器 toohello 目標目錄中的 Azure VM 代理程式安裝程式 MSI 檔案。</span><span class="sxs-lookup"><span data-stu-id="1e716-590">Drag hello Azure VM Agent Installer MSI file from your local computer/server toohello target directory of hello VM Agent on hello VM.</span></span>
  4.  <span data-ttu-id="1e716-591">按兩下 hello hello VM 上的 MSI 檔案。</span><span class="sxs-lookup"><span data-stu-id="1e716-591">Double-click hello MSI file on hello VM.</span></span>
3.  <span data-ttu-id="1e716-592">對於聯結的 tooon 內部網域的 Vm，請確定最終網際網路 proxy 設定，也適用於 VM，hello toohello Windows 本機系統帳戶 (S-1-5-18) 中所述[設定 hello proxy] [ deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="1e716-592">For VMs that are joined tooon-premises domains, make sure that eventual Internet proxy settings also apply toohello Windows Local System account (S-1-5-18) in hello VM, as described in [Configure hello proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="1e716-593">hello VM 代理程式在此內容中執行，並需要 toobe 無法 tooconnect tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1e716-593">hello VM Agent runs in this context and needs toobe able tooconnect tooAzure.</span></span>

<span data-ttu-id="1e716-594">不不需要的 tooupdate hello Azure VM 代理程式的任何使用者互動。</span><span class="sxs-lookup"><span data-stu-id="1e716-594">No user interaction is required tooupdate hello Azure VM Agent.</span></span> <span data-ttu-id="1e716-595">hello VM 代理程式會自動更新，而且不需要在 VM 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="1e716-595">hello VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <span data-ttu-id="1e716-596"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span><span class="sxs-lookup"><span data-stu-id="1e716-596"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span></span>
<span data-ttu-id="1e716-597">使用下列命令 tooinstall hello VM 代理程式適用於 Linux 的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-597">Use hello following commands tooinstall hello VM Agent for Linux:</span></span>

* <span data-ttu-id="1e716-598">**SUSE Linux Enterprise Server (SLES)**</span><span class="sxs-lookup"><span data-stu-id="1e716-598">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="1e716-599">**Red Hat Enterprise Linux (RHEL) 或 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="1e716-599">**Red Hat Enterprise Linux (RHEL) or Oracle Linux**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="1e716-600">如果已安裝 hello 代理程式，tooupdate hello Azure Linux 代理程式，請勿 hello 中所述步驟[來自 GitHub 的 VM toohello 最新版本更新 hello Azure Linux 代理程式][virtual-machines-linux-update-agent]。</span><span class="sxs-lookup"><span data-stu-id="1e716-600">If hello agent is already installed, tooupdate hello Azure Linux Agent, do hello steps described in [Update hello Azure Linux Agent on a VM toohello latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <span data-ttu-id="1e716-601"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>設定 hello proxy</span><span class="sxs-lookup"><span data-stu-id="1e716-601"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configure hello proxy</span></span>
<span data-ttu-id="1e716-602">hello 步驟 tooconfigure hello proxy 在 Windows 中是不同於您在 Linux 中設定 hello proxy 的 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="1e716-602">hello steps you take tooconfigure hello proxy in Windows are different from hello way you configure hello proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="1e716-603">Windows</span><span class="sxs-lookup"><span data-stu-id="1e716-603">Windows</span></span>
<span data-ttu-id="1e716-604">Proxy 設定必須正確設定，如 hello tooaccess hello 網際網路的本機系統帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-604">Proxy settings must be set up correctly for hello Local System account tooaccess hello Internet.</span></span> <span data-ttu-id="1e716-605">如果您的 proxy 設定未由群組原則設定，您可以設定 hello hello 本機系統帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e716-605">If your proxy settings are not set by Group Policy, you can configure hello settings for hello Local System account.</span></span>

1. <span data-ttu-id="1e716-606">跳過**啟動**，輸入**gpedit.msc**，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="1e716-606">Go too**Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
2. <span data-ttu-id="1e716-607">選取 [電腦設定] > [系統管理範本] > [Windows 元件] > [Internet Explorer]。</span><span class="sxs-lookup"><span data-stu-id="1e716-607">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="1e716-608">請確定該 hello 設定**設定每部電腦 （而非個別使用者） 建立 proxy**已停用或未設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-608">Make sure that hello setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
3. <span data-ttu-id="1e716-609">在**控制台**，跳過**網路和共用中心** > **網際網路選項**。</span><span class="sxs-lookup"><span data-stu-id="1e716-609">In **Control Panel**, go too**Network and Sharing Center** > **Internet Options**.</span></span>
4. <span data-ttu-id="1e716-610">在 [hello**連線**索引標籤，選取 hello **LAN 設定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e716-610">On hello **Connections** tab, select hello **LAN settings** button.</span></span>
5. <span data-ttu-id="1e716-611">清除 hello**自動偵測設定**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1e716-611">Clear hello **Automatically detect settings** check box.</span></span>
6. <span data-ttu-id="1e716-612">選取 hello**您的區域網路使用 proxy 伺服器**核取方塊，，，然後輸入 hello proxy 位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e716-612">Select hello **Use a proxy server for your LAN** check box, and then enter hello proxy address and port.</span></span>
7. <span data-ttu-id="1e716-613">選取 hello**進階** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e716-613">Select hello **Advanced** button.</span></span>
8. <span data-ttu-id="1e716-614">在 hello**例外狀況**方塊中，輸入 hello IP 位址**168.63.129.16**。</span><span class="sxs-lookup"><span data-stu-id="1e716-614">In hello **Exceptions** box, enter hello IP address **168.63.129.16**.</span></span> <span data-ttu-id="1e716-615">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1e716-615">Select **OK**.</span></span>

#### <a name="linux"></a><span data-ttu-id="1e716-616">Linux</span><span class="sxs-lookup"><span data-stu-id="1e716-616">Linux</span></span>
<span data-ttu-id="1e716-617">Microsoft Azure 客體代理程式，也就是位於 hello hello 設定檔中設定 hello 正確的 proxy\\等\\waagent.conf。</span><span class="sxs-lookup"><span data-stu-id="1e716-617">Configure hello correct proxy in hello configuration file of hello Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="1e716-618">設定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-618">Set hello following parameters:</span></span>

1.  <span data-ttu-id="1e716-619">**HTTP Proxy 主機**。</span><span class="sxs-lookup"><span data-stu-id="1e716-619">**HTTP proxy host**.</span></span> <span data-ttu-id="1e716-620">例如，設定太**proxy.corp.local**。</span><span class="sxs-lookup"><span data-stu-id="1e716-620">For example, set it too**proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  <span data-ttu-id="1e716-621">**HTTP Proxy 連接埠**。</span><span class="sxs-lookup"><span data-stu-id="1e716-621">**HTTP proxy port**.</span></span> <span data-ttu-id="1e716-622">例如，設定太**80**。</span><span class="sxs-lookup"><span data-stu-id="1e716-622">For example, set it too**80**.</span></span>
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  <span data-ttu-id="1e716-623">重新啟動 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-623">Restart hello agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="1e716-624">hello 中的 proxy 設定\\等\\waagent.conf 也適用於需要 toohello VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="1e716-624">hello proxy settings in \\etc\\waagent.conf also apply toohello required VM extensions.</span></span> <span data-ttu-id="1e716-625">如果您想 toouse hello Azure 儲存機制，請確定 hello 流量 toothese 儲存機制不經過您的內部部署內部網路。</span><span class="sxs-lookup"><span data-stu-id="1e716-625">If you want toouse hello Azure repositories, make sure that hello traffic toothese repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="1e716-626">如果您建立使用者定義的路由 tooenable 強制通道，請確定您新增的路由，路由傳送流量 toohello 儲存機制直接 toohello 網際網路，而不是透過您的站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="1e716-626">If you created user-defined routes tooenable forced tunneling, make sure that you add a route that routes traffic toohello repositories directly toohello Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="1e716-627">**SLES**</span><span class="sxs-lookup"><span data-stu-id="1e716-627">**SLES**</span></span>

  <span data-ttu-id="1e716-628">您也需要 tooadd 路由 hello IP 位址列於\\等\\regionserverclnt.cfg。</span><span class="sxs-lookup"><span data-stu-id="1e716-628">You also need tooadd routes for hello IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="1e716-629">hello 下圖顯示範例：</span><span class="sxs-lookup"><span data-stu-id="1e716-629">hello following figure shows an example:</span></span>

  ![強制通道][deployment-guide-figure-50]


* <span data-ttu-id="1e716-631">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="1e716-631">**RHEL**</span></span>

  <span data-ttu-id="1e716-632">您也需要 tooadd 路由 hello hello 主機 IP 位址列於\\等\\yum.repos.d\\rhui 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1e716-632">You also need tooadd routes for hello IP addresses of hello hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="1e716-633">如需範例，請參閱上述圖 hello。</span><span class="sxs-lookup"><span data-stu-id="1e716-633">For an example, see hello preceding figure.</span></span>

* <span data-ttu-id="1e716-634">**Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="1e716-634">**Oracle Linux**</span></span>

  <span data-ttu-id="1e716-635">Azure 上沒有任何 Oracle Linux 的存放庫。</span><span class="sxs-lookup"><span data-stu-id="1e716-635">There are no repositories for Oracle Linux on Azure.</span></span> <span data-ttu-id="1e716-636">您需要適用於 Oracle Linux tooconfigure 您自己的儲存機制，或使用 hello 公用儲存機制。</span><span class="sxs-lookup"><span data-stu-id="1e716-636">You need tooconfigure your own repositories for Oracle Linux or use hello public repositories.</span></span>

<span data-ttu-id="1e716-637">如需有關使用者定義的路由詳細資訊，請參閱[使用者定義的路由和 IP 轉送][virtual-networks-udr-overview]。</span><span class="sxs-lookup"><span data-stu-id="1e716-637">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <span data-ttu-id="1e716-638"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>設定 Azure 強化監視功能延伸模組適用於 SAP hello</span><span class="sxs-lookup"><span data-stu-id="1e716-638"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configure hello Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="1e716-639">當您已備妥 hello VM 中所述[在 Azure 上 SAP 的 Vm 部署案例][deployment-guide-3]，hello hello 虛擬機器安裝 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e716-639">When you've prepared hello VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], hello Azure VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="1e716-640">hello 下一個步驟為 toodeploy hello Azure 增強 Monitoring Extension for SAP，在 hello 全球 Azure 資料中心中的 hello Azure Extension Repository 中可用。</span><span class="sxs-lookup"><span data-stu-id="1e716-640">hello next step is toodeploy hello Azure Enhanced Monitoring Extension for SAP, which is available in hello Azure Extension Repository in hello global Azure datacenters.</span></span> <span data-ttu-id="1e716-641">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide-9.1]。</span><span class="sxs-lookup"><span data-stu-id="1e716-641">For more information, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-9.1].</span></span>

<span data-ttu-id="1e716-642">您可以使用 PowerShell 或 Azure CLI tooinstall，並設定 hello Azure 強化監視功能延伸模組適用於 SAP。</span><span class="sxs-lookup"><span data-stu-id="1e716-642">You can use PowerShell or Azure CLI tooinstall and configure hello Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="1e716-643">tooinstall hello 擴充功能在 Windows 或 Linux VM 上的使用一部 Windows 電腦，請參閱[Azure PowerShell][deployment-guide-4.5.1]。</span><span class="sxs-lookup"><span data-stu-id="1e716-643">tooinstall hello extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="1e716-644">請參閱 < 使用 Linux 桌面，Linux VM 上的 tooinstall hello 延伸[Azure CLI][deployment-guide-4.5.2]。</span><span class="sxs-lookup"><span data-stu-id="1e716-644">tooinstall hello extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <span data-ttu-id="1e716-645"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>適用於 Linux 和 Windows VM 的 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e716-645"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="1e716-646">使用 PowerShell tooinstall hello Azure 強化監視功能延伸模組的 SAP:</span><span class="sxs-lookup"><span data-stu-id="1e716-646">tooinstall hello Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="1e716-647">請確定您已安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="1e716-647">Make sure that you have installed hello latest version of hello Azure PowerShell cmdlet.</span></span> <span data-ttu-id="1e716-648">如需詳細資訊，請參閱[部署 Azure PowerShell Cmdlet][deployment-guide-4.1]。</span><span class="sxs-lookup"><span data-stu-id="1e716-648">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
2. <span data-ttu-id="1e716-649">執行下列 PowerShell cmdlet 的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e716-649">Run hello following PowerShell cmdlet.</span></span>
    <span data-ttu-id="1e716-650">如需可用環境的清單，請執行 `commandlet Get-AzureRmEnvironment`。</span><span class="sxs-lookup"><span data-stu-id="1e716-650">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="1e716-651">如果您想要 toouse 全域 Azure 中，您的環境是**AzureCloud**。</span><span class="sxs-lookup"><span data-stu-id="1e716-651">If you want toouse global Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="1e716-652">若為中國的 Azure，請選取 **AzureChinaCloud**。</span><span class="sxs-lookup"><span data-stu-id="1e716-652">For Azure in China, select **AzureChinaCloud**.</span></span>

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of hello environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

<span data-ttu-id="1e716-653">您輸入您的帳戶資料，並找出 hello Azure 虛擬機器之後，hello 指令碼部署所需的 hello 擴充功能，並提供所需的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="1e716-653">After you enter your account data and identify hello Azure virtual machine, hello script deploys hello required extensions and enables hello required features.</span></span> <span data-ttu-id="1e716-654">這可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="1e716-654">This can take several minutes.</span></span>
<span data-ttu-id="1e716-655">如需有關 `Set-AzureRmVMAEMExtension` 的詳細資訊，請參閱 [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension]。</span><span class="sxs-lookup"><span data-stu-id="1e716-655">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![成功執行 SAP 特定 Azure Cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

<span data-ttu-id="1e716-657">hello`Set-AzureRmVMAEMExtension`設定可以進行適用於 SAP 的監視所有的 hello 步驟 tooconfigure 主機。</span><span class="sxs-lookup"><span data-stu-id="1e716-657">hello `Set-AzureRmVMAEMExtension` configuration does all hello steps tooconfigure host monitoring for SAP.</span></span>

<span data-ttu-id="1e716-658">hello 指令碼輸出包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e716-658">hello script output includes hello following information:</span></span>

* <span data-ttu-id="1e716-659">確認 hello OS 磁碟和所有其他資料磁碟的監視已設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-659">Confirmation that monitoring for hello OS disk and all additional data disks has been configured.</span></span>
* <span data-ttu-id="1e716-660">hello 下面兩個訊息會確認特定儲存體帳戶的儲存體度量 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="1e716-660">hello next two messages confirm hello configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="1e716-661">一行輸出提供 hello hello hello 監視組態的實際的更新狀態。</span><span class="sxs-lookup"><span data-stu-id="1e716-661">One line of output gives hello status of hello actual update of hello monitoring configuration.</span></span>
* <span data-ttu-id="1e716-662">另一行輸出會確認該 hello 組態已部署或更新。</span><span class="sxs-lookup"><span data-stu-id="1e716-662">Another line of output confirms that hello configuration has been deployed or updated.</span></span>
* <span data-ttu-id="1e716-663">hello 輸出最後一行是參考。</span><span class="sxs-lookup"><span data-stu-id="1e716-663">hello last line of output is informational.</span></span> <span data-ttu-id="1e716-664">它會顯示測試的 hello 監視設定的選項。</span><span class="sxs-lookup"><span data-stu-id="1e716-664">It shows your options for testing hello monitoring configuration.</span></span>
* <span data-ttu-id="1e716-665">中所述，hello 整備檢查，如 hello Azure 強化監視功能延伸模組 for SAP，繼續 toocheck 成功，已執行的 Azure 強化監視功能的所有步驟，和該 hello Azure 基礎結構提供 hello 必要的資料[Azure 強化監視功能適用於 SAP 的整備檢查][deployment-guide-5.1]。</span><span class="sxs-lookup"><span data-stu-id="1e716-665">toocheck that all steps of Azure Enhanced Monitoring have been executed successfully, and that hello Azure Infrastructure provides hello necessary data, proceed with hello readiness check for hello Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span>
* <span data-ttu-id="1e716-666">等候 15-30 分鐘，讓 Azure 診斷 toocollect hello 相關資料。</span><span class="sxs-lookup"><span data-stu-id="1e716-666">Wait 15-30 minutes for Azure Diagnostics toocollect hello relevant data.</span></span>

#### <span data-ttu-id="1e716-667"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>適用於 Linux VM 的 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1e716-667"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI for Linux VMs</span></span>
<span data-ttu-id="1e716-668">使用 Azure CLI tooinstall hello Azure 強化監視功能延伸模組的 SAP:</span><span class="sxs-lookup"><span data-stu-id="1e716-668">tooinstall hello Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="1e716-669">中所述，安裝 Azure CLI 1.0，[安裝 hello Azure CLI 1.0][azure-cli]。</span><span class="sxs-lookup"><span data-stu-id="1e716-669">Install Azure CLI 1.0, as described in [Install hello Azure CLI 1.0][azure-cli].</span></span>
2. <span data-ttu-id="1e716-670">使用您的 Azure 帳戶進行登入：</span><span class="sxs-lookup"><span data-stu-id="1e716-670">Sign in with your Azure account:</span></span>

  ```
  azure login
  ```

3. <span data-ttu-id="1e716-671">切換 tooAzure Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="1e716-671">Switch tooAzure Resource Manager mode:</span></span>

  ```
  azure config mode arm
  ```

4. <span data-ttu-id="1e716-672">啟用 Azure Enhanced Monitoring：</span><span class="sxs-lookup"><span data-stu-id="1e716-672">Enable Azure Enhanced Monitoring:</span></span>

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. <span data-ttu-id="1e716-673">請確認該 hello Azure 強化監視功能延伸模組是在 hello Azure Linux VM 上作用。</span><span class="sxs-lookup"><span data-stu-id="1e716-673">Verify that hello Azure Enhanced Monitoring Extension is active on hello Azure Linux VM.</span></span> <span data-ttu-id="1e716-674">檢查是否 hello 檔案\\var\\lib\\AzureEnhancedMonitor\\PerfCounters 存在。</span><span class="sxs-lookup"><span data-stu-id="1e716-674">Check whether hello file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="1e716-675">如果存在的話，在命令提示字元執行這個命令 toodisplay 所收集資訊的 hello Azure 強化監視：</span><span class="sxs-lookup"><span data-stu-id="1e716-675">If it exists, at a command prompt, run this command toodisplay information collected by hello Azure Enhanced Monitor:</span></span>
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

<span data-ttu-id="1e716-676">hello 輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1e716-676">hello output looks like this:</span></span>
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <span data-ttu-id="1e716-677"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>針對端對端監視進行檢查及疑難排解</span><span class="sxs-lookup"><span data-stu-id="1e716-677"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="1e716-678">您部署 Azure VM，並設定 hello 相關 Azure 監視基礎結構之後，請檢查所有的 hello 元件的 hello Azure 強化監視功能延伸模組是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="1e716-678">After you have deployed your Azure VM and set up hello relevant Azure monitoring infrastructure, check whether all hello components of hello Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="1e716-679">中所述執行 hello Azure 強化監視功能延伸模組適用於 SAP 的 hello 整備檢查[hello Azure 強化監視功能延伸模組適用於 SAP 的整備檢查][deployment-guide-5.1]。</span><span class="sxs-lookup"><span data-stu-id="1e716-679">Run hello readiness check for hello Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="1e716-680">如果所有整備檢查結果均為正向，而且所有相關效能計數器都呈現 OK 狀態，表示已成功設定 Azure 監視。</span><span class="sxs-lookup"><span data-stu-id="1e716-680">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring has been set up successfully.</span></span> <span data-ttu-id="1e716-681">您可以繼續執行的 SAP Host Agent 的 hello 安裝中的 hello SAP 附註所述[SAP 資源][deployment-guide-2.2]。</span><span class="sxs-lookup"><span data-stu-id="1e716-681">You can proceed with hello installation of SAP Host Agent as described in hello SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="1e716-682">如果 hello 整備檢查指出的計數器遺失，則執行中所述的 hello hello Azure 監視基礎結構的健全狀況檢查[的 Azure 監視基礎結構設定健全狀況檢查][ deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="1e716-682">If hello readiness check indicates that counters are missing, run hello health check for hello Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="1e716-683">如需其他疑難排解選項，請參閱[針對適用於 SAP 的 Azure 監視進行疑難排解][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-683">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="1e716-684"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Hello Azure 強化監視功能延伸模組適用於 SAP 的整備檢查</span><span class="sxs-lookup"><span data-stu-id="1e716-684"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Readiness check for hello Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="1e716-685">這項檢查可確保您的 SAP 應用程式中出現的所有效能度量所都提供的 hello Azure 監視基礎結構的基礎。</span><span class="sxs-lookup"><span data-stu-id="1e716-685">This check makes sure that all performance metrics that appear inside your SAP application are provided by hello underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a><span data-ttu-id="1e716-686">執行 Windows VM 上的 hello 整備檢查</span><span class="sxs-lookup"><span data-stu-id="1e716-686">Run hello readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="1e716-687">登入 toohello Azure 虛擬機器 （使用系統管理員帳戶不是必要）。</span><span class="sxs-lookup"><span data-stu-id="1e716-687">Sign in toohello Azure virtual machine (using an admin account is not necessary).</span></span>
2.  <span data-ttu-id="1e716-688">開啟命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="1e716-688">Open a Command Prompt window.</span></span>
3.  <span data-ttu-id="1e716-689">Hello 命令提示字元，變更 hello 目錄 toohello 的 hello Azure 強化監視功能延伸模組適用於 SAP 的安裝資料夾： c:\\封裝\\外掛程式\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;版本 >\\卸除</span><span class="sxs-lookup"><span data-stu-id="1e716-689">At hello command prompt, change hello directory toohello installation folder of hello Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="1e716-690">hello*版本*hello 路徑 toohello 中監視功能延伸模組可能會不同。</span><span class="sxs-lookup"><span data-stu-id="1e716-690">hello *version* in hello path toohello monitoring extension might vary.</span></span> <span data-ttu-id="1e716-691">如果您看見 hello 監視 hello 安裝資料夾中，核取 hello hello AzureEnhancedMonitoring Windows 服務組態中的擴充功能的多個版本的資料夾，而且交換器 toohello 資料夾再指示為*路徑 tooexecutable*.</span><span class="sxs-lookup"><span data-stu-id="1e716-691">If you see folders for multiple versions of hello monitoring extension in hello installation folder, check hello configuration of hello AzureEnhancedMonitoring Windows service, and then switch toohello folder indicated as *Path tooexecutable*.</span></span>

  ![服務執行中的屬性 hello Azure 強化監視功能延伸模組的 SAP][deployment-guide-figure-1000]

4.  <span data-ttu-id="1e716-693">在 hello 命令提示字元中執行**azperflib.exe**不含任何參數。</span><span class="sxs-lookup"><span data-stu-id="1e716-693">At hello command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1e716-694">Azperflib.exe 會以迴圈執行，並更新 hello 收集計數器每隔 60 秒。</span><span class="sxs-lookup"><span data-stu-id="1e716-694">Azperflib.exe runs in a loop and updates hello collected counters every 60 seconds.</span></span> <span data-ttu-id="1e716-695">tooend hello 迴圈，關閉 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="1e716-695">tooend hello loop, close hello Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="1e716-696">如果未安裝 Azure 強化監視功能延伸模組，hello 或 hello AzureEnhancedMonitoring 服務未執行，hello 延伸模組已不正確設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-696">If hello Azure Enhanced Monitoring Extension is not installed, or hello AzureEnhancedMonitoring service is not running, hello extension has not been configured correctly.</span></span> <span data-ttu-id="1e716-697">如需如何 toodeploy hello 擴充功能的詳細資訊，請參閱[疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-697">For detailed information about how toodeploy hello extension, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-hello-output-of-azperflibexe"></a><span data-ttu-id="1e716-698">查看 azperflib.exe hello 輸出</span><span class="sxs-lookup"><span data-stu-id="1e716-698">Check hello output of azperflib.exe</span></span>
<span data-ttu-id="1e716-699">Azperflib.exe 輸出會顯示適用於 SAP 的所有已填入 Azure 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1e716-699">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="1e716-700">在 hello hello 收集的計數器清單底部，摘要和健全狀況指示器會顯示 hello 的 Azure 監視的狀態。</span><span class="sxs-lookup"><span data-stu-id="1e716-700">At hello bottom of hello list of collected counters, a summary and health indicator show hello status of Azure monitoring.</span></span>

<span data-ttu-id="1e716-701">![執行 azperflib.exe 的健康狀態檢查輸出，其表示沒有任何問題][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-701">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="1e716-702">檢查傳回的 hello hello 結果**Counters total**輸出，會針對為空的以及報告**健全狀況狀態**、 hello 前圖所示。</span><span class="sxs-lookup"><span data-stu-id="1e716-702">Check hello result returned for hello **Counters total** output, which is reported as empty, and for **Health status**, shown in hello preceding figure.</span></span>

<span data-ttu-id="1e716-703">解譯 hello 結果值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e716-703">Interpret hello resulting values as follows:</span></span>

| <span data-ttu-id="1e716-704">Azperflib.exe 結果值</span><span class="sxs-lookup"><span data-stu-id="1e716-704">Azperflib.exe result values</span></span> | <span data-ttu-id="1e716-705">Azure 監視健康狀態</span><span class="sxs-lookup"><span data-stu-id="1e716-705">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="1e716-706">**API 呼叫 - 無法使用**</span><span class="sxs-lookup"><span data-stu-id="1e716-706">**API Calls - not available**</span></span> | <span data-ttu-id="1e716-707">沒有可用的計數器可能不適用 toohello 虛擬機器設定，或錯誤。</span><span class="sxs-lookup"><span data-stu-id="1e716-707">Counters that are not available might be either not applicable toohello virtual machine configuration, or are errors.</span></span> <span data-ttu-id="1e716-708">請參閱 **Health status**。</span><span class="sxs-lookup"><span data-stu-id="1e716-708">See **Health status**.</span></span> |
| <span data-ttu-id="1e716-709">**Counters total - empty**</span><span class="sxs-lookup"><span data-stu-id="1e716-709">**Counters total - empty**</span></span> |<span data-ttu-id="1e716-710">下列兩個 Azure 儲存體計數器 hello 可以是空的：</span><span class="sxs-lookup"><span data-stu-id="1e716-710">hello following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="1e716-711">儲存體讀取 Op 延遲伺服器毫秒</span><span class="sxs-lookup"><span data-stu-id="1e716-711">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="1e716-712">儲存體讀取 Op 延遲 E2E 毫秒</span><span class="sxs-lookup"><span data-stu-id="1e716-712">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="1e716-713">所有其他計數器都必須具有值。</span><span class="sxs-lookup"><span data-stu-id="1e716-713">All other counters must have values.</span></span> |
| <span data-ttu-id="1e716-714">**Health status**</span><span class="sxs-lookup"><span data-stu-id="1e716-714">**Health status**</span></span> |<span data-ttu-id="1e716-715">只有在傳回狀態顯示 [OK] 時，才算正常。</span><span class="sxs-lookup"><span data-stu-id="1e716-715">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="1e716-716">**診斷**</span><span class="sxs-lookup"><span data-stu-id="1e716-716">**Diagnostics**</span></span> |<span data-ttu-id="1e716-717">健康狀態的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-717">Detailed information about health status.</span></span> |

<span data-ttu-id="1e716-718">如果 hello**健全狀況狀態**值不是**確定**，請依照下列中的 hello 指示[的 Azure 監視基礎結構設定健全狀況檢查][ deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="1e716-718">If hello **Health status** value is not **OK**, follow hello instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a><span data-ttu-id="1e716-719">執行 Linux VM 上的 hello 整備檢查</span><span class="sxs-lookup"><span data-stu-id="1e716-719">Run hello readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="1e716-720">使用 SSH 連線 toohello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-720">Connect toohello Azure Virtual Machine by using SSH.</span></span>

2.  <span data-ttu-id="1e716-721">檢查 hello 的 hello Azure 強化監視功能延伸模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="1e716-721">Check hello output of hello Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="1e716-722">a.</span><span class="sxs-lookup"><span data-stu-id="1e716-722">a.</span></span>  <span data-ttu-id="1e716-723">執行 `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span><span class="sxs-lookup"><span data-stu-id="1e716-723">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="1e716-724">**預期的結果**：傳回效能計數器的清單。</span><span class="sxs-lookup"><span data-stu-id="1e716-724">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="1e716-725">hello 檔案不能空白。</span><span class="sxs-lookup"><span data-stu-id="1e716-725">hello file should not be empty.</span></span>

 <span data-ttu-id="1e716-726">b.</span><span class="sxs-lookup"><span data-stu-id="1e716-726">b.</span></span> <span data-ttu-id="1e716-727">執行 `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span><span class="sxs-lookup"><span data-stu-id="1e716-727">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="1e716-728">**預期的結果**： 傳回 hello 錯誤所在的同一行**無**，例如**3; 組態。錯誤;，則為 0，則為 0;無、 0、 1456416792、 tst servercs;**</span><span class="sxs-lookup"><span data-stu-id="1e716-728">**Expected result**: Returns one line where hello error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="1e716-729">c.</span><span class="sxs-lookup"><span data-stu-id="1e716-729">c.</span></span> <span data-ttu-id="1e716-730">執行 `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span><span class="sxs-lookup"><span data-stu-id="1e716-730">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="1e716-731">**預期的結果**：傳回為空白或不存在。</span><span class="sxs-lookup"><span data-stu-id="1e716-731">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="1e716-732">如果 hello 上述檢查未成功，執行這些額外的檢查：</span><span class="sxs-lookup"><span data-stu-id="1e716-732">If hello preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="1e716-733">請確定該 hello waagent 已安裝並啟用。</span><span class="sxs-lookup"><span data-stu-id="1e716-733">Make sure that hello waagent is installed and enabled.</span></span>

  <span data-ttu-id="1e716-734">a.</span><span class="sxs-lookup"><span data-stu-id="1e716-734">a.</span></span>  <span data-ttu-id="1e716-735">執行 `sudo ls -al /var/lib/waagent/`</span><span class="sxs-lookup"><span data-stu-id="1e716-735">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="1e716-736">**預期的結果**： 列出 hello hello waagent 目錄內容。</span><span class="sxs-lookup"><span data-stu-id="1e716-736">**Expected result**: Lists hello content of hello waagent directory.</span></span>

  <span data-ttu-id="1e716-737">b.</span><span class="sxs-lookup"><span data-stu-id="1e716-737">b.</span></span>  <span data-ttu-id="1e716-738">執行 `ps -ax | grep waagent`</span><span class="sxs-lookup"><span data-stu-id="1e716-738">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="1e716-739">**預期的結果**：顯示類似下列一個項目：`python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="1e716-739">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

3.   <span data-ttu-id="1e716-740">請確定該 hello Azure 強化監視功能延伸模組是已安裝且正在執行。</span><span class="sxs-lookup"><span data-stu-id="1e716-740">Make sure that hello Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="1e716-741">a.</span><span class="sxs-lookup"><span data-stu-id="1e716-741">a.</span></span>  <span data-ttu-id="1e716-742">執行 `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`</span><span class="sxs-lookup"><span data-stu-id="1e716-742">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`</span></span>

    <span data-ttu-id="1e716-743">**預期的結果**： 列出 hello hello Azure 強化監視功能延伸模組目錄內容。</span><span class="sxs-lookup"><span data-stu-id="1e716-743">**Expected result**: Lists hello content of hello Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="1e716-744">b.</span><span class="sxs-lookup"><span data-stu-id="1e716-744">b.</span></span> <span data-ttu-id="1e716-745">執行 `ps -ax | grep AzureEnhanced`</span><span class="sxs-lookup"><span data-stu-id="1e716-745">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="1e716-746">**預期的結果**：顯示類似下列一個項目：`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="1e716-746">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

3. <span data-ttu-id="1e716-747">SAP 附註所述安裝 SAP Host Agent [1031096]，並檢查 hello 輸出`saposcol`。</span><span class="sxs-lookup"><span data-stu-id="1e716-747">Install SAP Host Agent as described in SAP Note [1031096], and check hello output of `saposcol`.</span></span>

  <span data-ttu-id="1e716-748">a.</span><span class="sxs-lookup"><span data-stu-id="1e716-748">a.</span></span>  <span data-ttu-id="1e716-749">執行 `/usr/sap/hostctrl/exe/saposcol -d`</span><span class="sxs-lookup"><span data-stu-id="1e716-749">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="1e716-750">b.</span><span class="sxs-lookup"><span data-stu-id="1e716-750">b.</span></span>  <span data-ttu-id="1e716-751">執行 `dump ccm`</span><span class="sxs-lookup"><span data-stu-id="1e716-751">Run `dump ccm`</span></span>

  <span data-ttu-id="1e716-752">c.</span><span class="sxs-lookup"><span data-stu-id="1e716-752">c.</span></span>  <span data-ttu-id="1e716-753">檢查是否 hello **Virtualization_Configuration\Enhanced 監視存取**度量是**true**。</span><span class="sxs-lookup"><span data-stu-id="1e716-753">Check whether hello **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="1e716-754">如果您已安裝 SAP NetWeaver ABAP 應用程式伺服器，請開啟交易 ST06，並檢查是否已啟用增強監視。</span><span class="sxs-lookup"><span data-stu-id="1e716-754">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="1e716-755">如果任何這些檢查失敗，而且如需如何 tooredeploy hello 擴充功能的詳細資訊，請參閱[疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-755">If any of these checks fail, and for detailed information about how tooredeploy hello extension, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="1e716-756"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>健全狀況檢查 hello Azure 監視基礎結構設定</span><span class="sxs-lookup"><span data-stu-id="1e716-756"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Health check for hello Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="1e716-757">如果部分監視資料的 hello 沒有指示地正確傳遞 hello 測試中所述[Azure 強化監視功能適用於 SAP 的整備檢查][deployment-guide-5.1]中執行的 hello `Test-AzureRmVMAEMExtension` cmdlet toocheck是否 hello Azure 監視基礎結構和 hello SAP 的監視功能延伸模組已正確設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-757">If some of hello monitoring data is not delivered correctly as indicated by hello test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run hello `Test-AzureRmVMAEMExtension` cmdlet toocheck whether hello Azure monitoring infrastructure and hello monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="1e716-758">確定您已安裝 hello hello Azure PowerShell cmdlet，最新版本中所述[部署 Azure PowerShell cmdlet][deployment-guide-4.1]。</span><span class="sxs-lookup"><span data-stu-id="1e716-758">Make sure that you have installed hello latest version of hello Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
2.  <span data-ttu-id="1e716-759">執行下列 PowerShell cmdlet 的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e716-759">Run hello following PowerShell cmdlet.</span></span> <span data-ttu-id="1e716-760">如需可用環境的清單，執行 hello cmdlet `Get-AzureRmEnvironment`。</span><span class="sxs-lookup"><span data-stu-id="1e716-760">For a list of available environments, run hello cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="1e716-761">toouse 全域 Azure，選取 hello **AzureCloud**環境。</span><span class="sxs-lookup"><span data-stu-id="1e716-761">toouse global Azure, select hello **AzureCloud** environment.</span></span> <span data-ttu-id="1e716-762">若為中國的 Azure，請選取 **AzureChinaCloud**。</span><span class="sxs-lookup"><span data-stu-id="1e716-762">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  <span data-ttu-id="1e716-763">輸入您的帳戶資料，並找出 hello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e716-763">Enter your account data and identify hello Azure virtual machine.</span></span>

  ![SAP 特定 Azure Cmdlet Test-VMConfigForSAP_GUI 的輸入頁面][deployment-guide-figure-1200]

4. <span data-ttu-id="1e716-765">您選取 hello 指令碼測試 hello hello 虛擬機器設定。</span><span class="sxs-lookup"><span data-stu-id="1e716-765">hello script tests hello configuration of hello virtual machine you select.</span></span>

  ![順利完成測試的 hello Azure 監視基礎結構，適用於 SAP 的輸出][deployment-guide-figure-1300]

<span data-ttu-id="1e716-767">確定每個健康狀態檢查的結果都 [OK]。</span><span class="sxs-lookup"><span data-stu-id="1e716-767">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="1e716-768">如果部分檢查不會顯示**確定**，執行 hello 更新指令程式中所述[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="1e716-768">If some checks do not display **OK**, run hello update cmdlet as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1e716-769">請稍候 15 分鐘，並說明重複 hello 檢查[Azure 強化監視功能適用於 SAP 的整備檢查][ deployment-guide-5.1]和[的 Azure 監視基礎結構組態健全狀況檢查][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="1e716-769">Wait 15 minutes, and repeat hello checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="1e716-770">如果 hello 檢查仍指出某些或全部計數器有問題，請參閱[疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-770">If hello checks still indicate a problem with some or all counters, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="1e716-771"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構</span><span class="sxs-lookup"><span data-stu-id="1e716-771"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Troubleshooting hello Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="1e716-773">完全未顯示 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="1e716-773">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="1e716-774">hello AzureEnhancedMonitoring Windows 服務會收集在 Azure 中的效能度量。</span><span class="sxs-lookup"><span data-stu-id="1e716-774">hello AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="1e716-775">如果 hello 服務的安裝不正確或不在 VM 中執行，您可以收集效能度量。</span><span class="sxs-lookup"><span data-stu-id="1e716-775">If hello service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="1e716-776">hello Azure 強化監視功能延伸模組的安裝目錄是 hello 的空的</span><span class="sxs-lookup"><span data-stu-id="1e716-776">hello installation directory of hello Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="1e716-777">問題</span><span class="sxs-lookup"><span data-stu-id="1e716-777">Issue</span></span>
<span data-ttu-id="1e716-778">hello 安裝目錄 c:\\封裝\\外掛程式\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;版本 >\\drop 是空白。</span><span class="sxs-lookup"><span data-stu-id="1e716-778">hello installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="1e716-779">方案</span><span class="sxs-lookup"><span data-stu-id="1e716-779">Solution</span></span>
<span data-ttu-id="1e716-780">未安裝 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1e716-780">hello extension is not installed.</span></span> <span data-ttu-id="1e716-781">判斷這是否為 Proxy 問題 (如先前所述)。</span><span class="sxs-lookup"><span data-stu-id="1e716-781">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="1e716-782">您可能需要 toorestart hello 機器或重新執行的 hello`Set-AzureRmVMAEMExtension`組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-782">You might need toorestart hello machine or rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="1e716-783">Azure Enhanced Monitoring 的服務不存在</span><span class="sxs-lookup"><span data-stu-id="1e716-783">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="1e716-784">問題</span><span class="sxs-lookup"><span data-stu-id="1e716-784">Issue</span></span>
<span data-ttu-id="1e716-785">hello AzureEnhancedMonitoring Windows 服務不存在。</span><span class="sxs-lookup"><span data-stu-id="1e716-785">hello AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="1e716-786">Azperflib.exe 輸出會擲回錯誤︰</span><span class="sxs-lookup"><span data-stu-id="1e716-786">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="1e716-787">![執行 azperflib.exe 指出適用於 SAP 的 Azure 強化監視功能延伸模組的 hello 的 hello 服務未執行][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="1e716-787">![Execution of azperflib.exe indicates that hello service of hello Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="1e716-788">方案</span><span class="sxs-lookup"><span data-stu-id="1e716-788">Solution</span></span>
<span data-ttu-id="1e716-789">如果 hello 服務不存在，hello Azure 強化監視功能延伸模組適用於 SAP 尚未安裝正確。</span><span class="sxs-lookup"><span data-stu-id="1e716-789">If hello service does not exist, hello Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="1e716-790">使用您的部署案例中所述的 hello 步驟來重新部署 hello 延伸[在 Azure 中 SAP 的 Vm 部署案例][deployment-guide-3]。</span><span class="sxs-lookup"><span data-stu-id="1e716-790">Redeploy hello extension by using hello steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="1e716-791">在一小時後部署 hello 延伸之後，再次檢查 hello Azure VM 中是否提供 hello Azure 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1e716-791">After you deploy hello extension, after one hour, check again whether hello Azure performance counters are provided in hello Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a><span data-ttu-id="1e716-792">Azure 強化監視功能的服務存在，但失敗 toostart</span><span class="sxs-lookup"><span data-stu-id="1e716-792">Service for Azure Enhanced Monitoring exists, but fails toostart</span></span>

###### <a name="issue"></a><span data-ttu-id="1e716-793">問題</span><span class="sxs-lookup"><span data-stu-id="1e716-793">Issue</span></span>
<span data-ttu-id="1e716-794">hello AzureEnhancedMonitoring Windows 服務存在並已啟用，但失敗 toostart。</span><span class="sxs-lookup"><span data-stu-id="1e716-794">hello AzureEnhancedMonitoring Windows service exists and is enabled, but fails toostart.</span></span> <span data-ttu-id="1e716-795">如需詳細資訊，請檢查 hello 應用程式事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1e716-795">For more information, check hello application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="1e716-796">方案</span><span class="sxs-lookup"><span data-stu-id="1e716-796">Solution</span></span>
<span data-ttu-id="1e716-797">hello 設定不正確。</span><span class="sxs-lookup"><span data-stu-id="1e716-797">hello configuration is incorrect.</span></span> <span data-ttu-id="1e716-798">中所述，重新啟動監視 hello VM 延伸模組的 hello[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="1e716-798">Restart hello monitoring extension for hello VM, as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="1e716-800">遺失部分 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="1e716-800">Some Azure performance counters are missing</span></span>
<span data-ttu-id="1e716-801">hello AzureEnhancedMonitoring Windows 服務會收集在 Azure 中的效能度量。</span><span class="sxs-lookup"><span data-stu-id="1e716-801">hello AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="1e716-802">hello 服務從多個來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="1e716-802">hello service gets data from several sources.</span></span> <span data-ttu-id="1e716-803">有些組態資料是在本機收集，而有些效能計量是從 Azure 診斷讀取而來。</span><span class="sxs-lookup"><span data-stu-id="1e716-803">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="1e716-804">儲存體計數器是從您登入 hello 儲存體訂用帳戶層級來使用。</span><span class="sxs-lookup"><span data-stu-id="1e716-804">Storage counters are used from your logging on hello storage subscription level.</span></span>

<span data-ttu-id="1e716-805">如果使用 SAP Note 疑難排解[1999351]未解決 hello 問題，請重新執行 hello`Set-AzureRmVMAEMExtension`組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-805">If troubleshooting by using SAP Note [1999351] doesn't resolve hello issue, rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="1e716-806">因為儲存體分析或診斷計數器可能不在啟用後，立即建立，您可能需要一小時 toowait。</span><span class="sxs-lookup"><span data-stu-id="1e716-806">You might have toowait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="1e716-807">如果 hello 問題持續發生，請開啟 hello 元件 BC OP-NT AZR 適用於 Windows 或 BC-OP-LNX-AZR Linux 虛擬機器上的 SAP 客戶支援訊息。</span><span class="sxs-lookup"><span data-stu-id="1e716-807">If hello problem persists, open an SAP customer support message on hello component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="1e716-809">完全未顯示 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="1e716-809">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="1e716-810">Daemon 會收集在 Azure 中的效能計量。</span><span class="sxs-lookup"><span data-stu-id="1e716-810">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="1e716-811">如果 hello 服務精靈未執行，您可以收集效能度量。</span><span class="sxs-lookup"><span data-stu-id="1e716-811">If hello daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="1e716-812">hello Azure 強化監視功能延伸模組的安裝目錄是 hello 的空的</span><span class="sxs-lookup"><span data-stu-id="1e716-812">hello installation directory of hello Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="1e716-813">問題</span><span class="sxs-lookup"><span data-stu-id="1e716-813">Issue</span></span>
<span data-ttu-id="1e716-814">hello 目錄\\var\\lib\\waagent\\沒有 hello Azure 強化監視功能延伸模組的子目錄。</span><span class="sxs-lookup"><span data-stu-id="1e716-814">hello directory \\var\\lib\\waagent\\ does not have a subdirectory for hello Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="1e716-815">方案</span><span class="sxs-lookup"><span data-stu-id="1e716-815">Solution</span></span>
<span data-ttu-id="1e716-816">未安裝 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1e716-816">hello extension is not installed.</span></span> <span data-ttu-id="1e716-817">判斷這是否為 Proxy 問題 (如先前所述)。</span><span class="sxs-lookup"><span data-stu-id="1e716-817">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="1e716-818">您可能需要 toorestart hello 電腦及 （或） 重新執行的 hello`Set-AzureRmVMAEMExtension`組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e716-818">You might need toorestart hello machine and/or rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="1e716-820">遺失部分 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="1e716-820">Some Azure performance counters are missing</span></span>
<span data-ttu-id="1e716-821">Azure 中的效能計量是由 Daemon 收集，而 Daemon 會從數個來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="1e716-821">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="1e716-822">有些組態資料是在本機收集，而有些效能計量是從 Azure 診斷讀取而來。</span><span class="sxs-lookup"><span data-stu-id="1e716-822">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="1e716-823">儲存體計數器來自儲存體訂用帳戶中的 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1e716-823">Storage counters come from hello logs in your storage subscription.</span></span>

<span data-ttu-id="1e716-824">如需完整且最新的已知問題清單，請參閱 SAP Note [1999351]，其中包含適用於 Enhanced Azure Monitoring for SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="1e716-824">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="1e716-825">如果使用 SAP Note 疑難排解[1999351]並未解決 hello 問題，請重新執行 hello`Set-AzureRmVMAEMExtension`組態指令碼中所述[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1e716-825">If troubleshooting by using SAP Note [1999351] does not resolve hello issue, rerun hello `Set-AzureRmVMAEMExtension` configuration script as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1e716-826">因為儲存體分析或診斷計數器可能不在啟用後，立即建立，您可能必須 toowait 一小時。</span><span class="sxs-lookup"><span data-stu-id="1e716-826">You might have toowait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="1e716-827">如果 hello 問題持續發生，請開啟 hello 元件 BC OP-NT AZR 適用於 Windows 或 BC-OP-LNX-AZR Linux 虛擬機器上的 SAP 客戶支援訊息。</span><span class="sxs-lookup"><span data-stu-id="1e716-827">If hello problem persists, open an SAP customer support message on hello component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
