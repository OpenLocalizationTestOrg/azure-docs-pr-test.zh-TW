---
title: "適用於 SAP NetWeaver 的 Azure 虛擬機器部署 | Microsoft Docs"
description: "了解如何在 Azure 中的 Linux 虛擬機器上部署 SAP 軟體。"
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
ms.openlocfilehash: 7d0400c834767736f63bc30a7bc2495dc6ee6e36
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a><span data-ttu-id="5d2b5-103">適用於 SAP NetWeaver 的 Azure 虛擬機器部署</span><span class="sxs-lookup"><span data-stu-id="5d2b5-103">Azure Virtual Machines deployment for SAP NetWeaver</span></span>
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
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from the Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics to SQL Server RDBMS)
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
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from the Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM to an on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable the Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure the Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for the Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure the proxy)
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
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on the on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with the on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises to Azure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises to Azure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises to Azure)
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
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI)
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

<span data-ttu-id="5d2b5-117">對於需要在最短的時間內處理計算和儲存資源，而不需要漫長的採購週期的組織而言，Azure 虛擬機器是適用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-117">Azure Virtual Machines is the solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="5d2b5-118">您可以使用 Azure 虛擬機器在 Azure 中部署傳統應用程式，例如 SAP NetWeaver 架構應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-118">You can use Azure Virtual Machines to deploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="5d2b5-119">擴充應用程式的可靠性與可用性，不需其他內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-119">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="5d2b5-120">「Azure 虛擬機器」支援跨單位連線能力，貴公司可將「Azure 虛擬機器」整合到其內部部署網域、私人雲端，以及 SAP 系統環境中。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-120">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="5d2b5-121">在本文中，我們將討論在 Azure 中的虛擬機器 (VM) 上部署 SAP 應用程式的步驟，包括替代部署選項和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-121">In this article, we cover the steps to deploy SAP applications on virtual machines (VMs) in Azure, including alternate deployment options and troubleshooting.</span></span> <span data-ttu-id="5d2b5-122">本文是以 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]為基礎。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-122">This article builds on the information in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span> <span data-ttu-id="5d2b5-123">本文也可補充 SAP 安裝文件和 SAP Note 的不足，而這些是安裝及部署 SAP 軟體的主要資源。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-123">It also complements SAP installation documentation and SAP Notes, which are the primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d2b5-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="5d2b5-124">Prerequisites</span></span>
<span data-ttu-id="5d2b5-125">針對 SAP 軟體部署設定 Azure 虛擬機器，牽涉到多個步驟和資源。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-125">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="5d2b5-126">開始之前，請確定您符合在 Azure 中的虛擬機器上安裝 SAP 軟體的必要條件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-126">Before you start, make sure that you meet the prerequisites for installing SAP software on virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="5d2b5-127">本機電腦</span><span class="sxs-lookup"><span data-stu-id="5d2b5-127">Local computer</span></span>
<span data-ttu-id="5d2b5-128">若要管理 Windows 或 Linux VM，您可以使用 PowerShell 指令碼和 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-128">To manage Windows or Linux VMs, you can use a PowerShell script and the Azure portal.</span></span> <span data-ttu-id="5d2b5-129">對於這兩種工具，您需有執行 Windows 7 或更新 Windows 版本的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-129">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="5d2b5-130">如果您只想管理 Linux VM，而且想要使用 Linux 電腦進行這項工作，您可以使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-130">If you want to manage only Linux VMs and you want to use a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="5d2b5-131">網際網路連線</span><span class="sxs-lookup"><span data-stu-id="5d2b5-131">Internet connection</span></span>
<span data-ttu-id="5d2b5-132">若要下載並執行 SAP 軟體部署所需的工具和指令碼，您必須連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-132">To download and run the tools and scripts that are required for SAP software deployment, you must be connected to the Internet.</span></span> <span data-ttu-id="5d2b5-133">執行 Azure Enhanced Monitoring Extension for SAP 的 Azure VM 也必須能夠存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-133">The Azure VM that is running the Azure Enhanced Monitoring Extension for SAP also needs access to the Internet.</span></span> <span data-ttu-id="5d2b5-134">如果 Azure VM 是 Azure 虛擬網路或內部部署網域的一部分，請務必如[設定 Proxy][deployment-guide-configure-proxy] 所述，設定相關的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-134">If the Azure VM is part of an Azure virtual network or on-premises domain, make sure that the relevant proxy settings are set, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="5d2b5-135">Microsoft Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d2b5-135">Microsoft Azure subscription</span></span>
<span data-ttu-id="5d2b5-136">您需要使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-136">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="5d2b5-137">拓撲和網路</span><span class="sxs-lookup"><span data-stu-id="5d2b5-137">Topology and networking</span></span>
<span data-ttu-id="5d2b5-138">您需要在 Azure 中定義 SAP 部署的拓撲和架構：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-138">You need to define the topology and architecture of the SAP deployment in Azure:</span></span>

* <span data-ttu-id="5d2b5-139">要使用的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5d2b5-139">Azure storage accounts to be used</span></span>
* <span data-ttu-id="5d2b5-140">您想要部署 SAP 系統的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5d2b5-140">Virtual network where you want to deploy the SAP system</span></span>
* <span data-ttu-id="5d2b5-141">您想要部署 SAP 系統的資源群組</span><span class="sxs-lookup"><span data-stu-id="5d2b5-141">Resource group to which you want to deploy the SAP system</span></span>
* <span data-ttu-id="5d2b5-142">您想要部署 SAP 系統的 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="5d2b5-142">Azure region where you want to deploy the SAP system</span></span>
* <span data-ttu-id="5d2b5-143">SAP 組態 (兩層或三層)</span><span class="sxs-lookup"><span data-stu-id="5d2b5-143">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="5d2b5-144">VM 大小以及要掛接到 VM 的額外資料磁碟數目</span><span class="sxs-lookup"><span data-stu-id="5d2b5-144">VM sizes and the number of additional data disks to be mounted to the VMs</span></span>
* <span data-ttu-id="5d2b5-145">SAP Correction and Transport System (CTS) 組態</span><span class="sxs-lookup"><span data-stu-id="5d2b5-145">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="5d2b5-146">開始 SAP 軟體部署程序之前，如有必要請先建立及設定 Azure 儲存體帳戶或 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-146">Create and configure Azure storage accounts (if required) or Azure virtual networks before you begin the SAP software deployment process.</span></span> <span data-ttu-id="5d2b5-147">如需有關如何建立及設定這些資源的詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-147">For information about how to create and configure these resources, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="5d2b5-148">SAP 大小調整</span><span class="sxs-lookup"><span data-stu-id="5d2b5-148">SAP sizing</span></span>
<span data-ttu-id="5d2b5-149">了解下列資訊，以便進行 SAP 大小調整︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-149">Know the following information, for SAP sizing:</span></span>

* <span data-ttu-id="5d2b5-150">預估的 SAP 工作負載 (例如，使用 SAP Quick Sizer 工具) 和 SAP Application Performance Standard (SAPS) 數字</span><span class="sxs-lookup"><span data-stu-id="5d2b5-150">Projected SAP workload, for example, by using the SAP Quick Sizer tool, and the SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="5d2b5-151">SAP 系統所需的 CPU 資源和記憶體耗用量</span><span class="sxs-lookup"><span data-stu-id="5d2b5-151">Required CPU resource and memory consumption of the SAP system</span></span>
* <span data-ttu-id="5d2b5-152">每秒所需的輸入/輸出 (I/O) 作業</span><span class="sxs-lookup"><span data-stu-id="5d2b5-152">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="5d2b5-153">Azure 中 VM 之間最終通訊所需的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="5d2b5-153">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="5d2b5-154">內部部署資產與已部署 Azure 的 SAP 系統之間所需的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="5d2b5-154">Required network bandwidth between on-premises assets and the Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="5d2b5-155">資源群組</span><span class="sxs-lookup"><span data-stu-id="5d2b5-155">Resource groups</span></span>
<span data-ttu-id="5d2b5-156">在 Azure Resource Manager 中，您可以使用資源群組來管理 Azure 訂用帳戶中的所有應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-156">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="5d2b5-157">如需詳細資訊，請參閱 [Azure Resource Manager概觀][resource-group-overview]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-157">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="5d2b5-158">資源</span><span class="sxs-lookup"><span data-stu-id="5d2b5-158">Resources</span></span>

### <span data-ttu-id="5d2b5-159"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP 資源</span><span class="sxs-lookup"><span data-stu-id="5d2b5-159"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP resources</span></span>
<span data-ttu-id="5d2b5-160">當您設定 SAP 軟體部署時，您需要下列 SAP 資源︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-160">When you are setting up your SAP software deployment, you need the following SAP resources:</span></span>

* <span data-ttu-id="5d2b5-161">SAP Note [1928533]，其中包含：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-161">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="5d2b5-162">SAP 軟體部署支援的 Azure VM 大小清單</span><span class="sxs-lookup"><span data-stu-id="5d2b5-162">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="5d2b5-163">Azure VM 大小的重要容量資訊</span><span class="sxs-lookup"><span data-stu-id="5d2b5-163">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="5d2b5-164">支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合</span><span class="sxs-lookup"><span data-stu-id="5d2b5-164">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="5d2b5-165">Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本</span><span class="sxs-lookup"><span data-stu-id="5d2b5-165">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="5d2b5-166">SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-166">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="5d2b5-167">SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-167">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="5d2b5-168">SAP Note [1409604] 包含 Azure 中 Windows 所需的 SAP Host Agent 版本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-168">SAP Note [1409604] has the required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="5d2b5-169">SAP Note [2191498] 包含 Azure 中 Linux 所需的 SAP Host Agent 版本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-169">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="5d2b5-170">SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-170">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="5d2b5-171">SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-171">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="5d2b5-172">SAP Note [2002167] 包含 Red Hat Enterprise Linux 7.x 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-172">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="5d2b5-173">SAP Note [2069760] 包含 Oracle Linux 7.x 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-173">SAP Note [2069760] has general information about Oracle Linux 7.x.</span></span>
* <span data-ttu-id="5d2b5-174">SAP Note [1999351] 包含 Azure Enhanced Monitoring Extension for SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-174">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="5d2b5-175">SAP Note [1597355] 包含 Linux 交換空間的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-175">SAP Note [1597355] has general information about swap-space for Linux.</span></span>
* <span data-ttu-id="5d2b5-176">[Azure SCN 上的 SAP 頁面](https://wiki.scn.sap.com/wiki/x/Pia7Gg)包含新聞和實用資源的集合。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-176">[SAP on Azure SCN page](https://wiki.scn.sap.com/wiki/x/Pia7Gg) has news and a collection of useful resources.</span></span>
* <span data-ttu-id="5d2b5-177">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-177">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="5d2b5-178">[Azure PowerShell][azure-ps] 所包含的 SAP 特定 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-178">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="5d2b5-179">[Azure CLI][azure-cli] 所包含的 SAP 特定 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-179">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

### <span data-ttu-id="5d2b5-180"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Windows 資源</span><span class="sxs-lookup"><span data-stu-id="5d2b5-180"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Windows resources</span></span>
<span data-ttu-id="5d2b5-181">這些 Microsoft 文章涵蓋 Azure 中的 SAP 部署：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-181">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="5d2b5-182">[SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-182">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="5d2b5-183">[適用於 SAP NetWeaver 的 Azure 虛擬機器部署 (本文)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-183">[Azure Virtual Machines deployment for SAP NetWeaver (this article)][deployment-guide]</span></span>
* <span data-ttu-id="5d2b5-184">[SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-184">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>

## <span data-ttu-id="5d2b5-185"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure VM 上的 SAP 軟體部署案例</span><span class="sxs-lookup"><span data-stu-id="5d2b5-185"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="5d2b5-186">您有多個選項可用於在 Azure 中部署 VM 和相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-186">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="5d2b5-187">一定要了解部署選項之間的差異，因為您可能必須根據您選擇的部署類型，採取不同的步驟來準備您的 VM 進行部署。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-187">It's important to understand the differences between deployment options, because you might take different steps to prepare your VMs for deployment based on the deployment type you choose.</span></span>

### <span data-ttu-id="5d2b5-188"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>案例 1：從 Azure Marketplace 為 SAP 部署 VM</span><span class="sxs-lookup"><span data-stu-id="5d2b5-188"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Deploying a VM from the Azure Marketplace for SAP</span></span>
<span data-ttu-id="5d2b5-189">您可以使用 Azure Marketplace 中由 Microsoft 或協力廠商提供的映像來部署 VM。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-189">You can use an image provided by Microsoft or by a third party in the Azure Marketplace to deploy your VM.</span></span> <span data-ttu-id="5d2b5-190">Marketplace 會提供 Windows Server 的一些標準 OS 映像以及不同的 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-190">The Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="5d2b5-191">您也可以部署包含資料庫管理系統 (DBMS) SKU 的映像，例如，Microsoft SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-191">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="5d2b5-192">如需使用映像搭配 DBMS SKU 的詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-192">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span>

<span data-ttu-id="5d2b5-193">下列流程圖顯示從 Azure Marketplace 部署 VM 的 SAP 特定步驟順序：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-193">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from the Azure Marketplace:</span></span>

![使用 Azure Marketplace 中的 VM 映像部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-the-azure-portal"></a><span data-ttu-id="5d2b5-195">使用 Azure 入口網站建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-195">Create a virtual machine by using the Azure portal</span></span>
<span data-ttu-id="5d2b5-196">透過 Azure Marketplace 中的映像建立新虛擬機器的最簡單方式，就是使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-196">The easiest way to create a new virtual machine with an image from the Azure Marketplace is by using the Azure portal.</span></span>

1.  <span data-ttu-id="5d2b5-197">移至 <https://portal.azure.com/#create/hub>。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-197">Go to <https://portal.azure.com/#create/hub>.</span></span>  <span data-ttu-id="5d2b5-198">或者，在 Azure 入口網站功能表中，選取 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-198">Or, in the Azure portal menu, select **+ New**.</span></span>
2.  <span data-ttu-id="5d2b5-199">選取 [計算]，然後選取您想要部署的作業系統類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-199">Select **Compute**, and then select the type of operating system you want to deploy.</span></span> <span data-ttu-id="5d2b5-200">例如，Windows Server 2012 R2、SUSE Linux Enterprise Server 12 (SLES 12)、Red Hat Enterprise Linux 7.2 (RHEL 7.2) 或 Oracle Linux 7.2。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-200">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span></span> <span data-ttu-id="5d2b5-201">預設清單檢視不會顯示所有支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-201">The default list view does not show all supported operating systems.</span></span> <span data-ttu-id="5d2b5-202">選取 [查看全部] 以取得完整清單。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-202">Select **see all** for a full list.</span></span> <span data-ttu-id="5d2b5-203">如需 SAP 軟體部署支援的作業系統詳細資訊，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-203">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
3.  <span data-ttu-id="5d2b5-204">在下一頁上檢閱條款及條件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-204">On the next page, review terms and conditions.</span></span>
4.  <span data-ttu-id="5d2b5-205">在 [選取部署模型] 方塊中，選取 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-205">In the **Select a deployment model** box, select **Resource Manager**.</span></span>
5.  <span data-ttu-id="5d2b5-206">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-206">Select **Create**.</span></span>

<span data-ttu-id="5d2b5-207">除了所有必要的資源 (例如網路介面或儲存體帳戶) 以外，此精靈會引導您完成必要參數設定以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-207">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="5d2b5-208">其中一些參數包括︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-208">Some of these parameters are:</span></span>

1. <span data-ttu-id="5d2b5-209">**基本**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-209">**Basics**:</span></span>
 * <span data-ttu-id="5d2b5-210">**名稱**：資源名稱 (虛擬機器名稱)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-210">**Name**: The name of the resource (the virtual machine name).</span></span>
 * <span data-ttu-id="5d2b5-211">**VM 磁碟類型**：選取作業系統磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-211">**VM disk type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="5d2b5-212">如果您想要使用進階儲存體作為您的資料磁碟，建議您作業系統磁碟也使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-212">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
 * <span data-ttu-id="5d2b5-213">**使用者名稱和密碼**或 **SSH 公用金鑰**︰輸入在佈建期間建立之使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-213">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span></span> <span data-ttu-id="5d2b5-214">對於 Linux 虛擬機器，您可以輸入要用來登入電腦的公開安全殼層 (SSH) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-214">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span></span>
 * <span data-ttu-id="5d2b5-215">**訂用帳戶**：選取您想要用來佈建新虛擬機器的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-215">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span></span>
 * <span data-ttu-id="5d2b5-216">**資源群組**：VM 的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-216">**Resource group**: The name of the resource group for the VM.</span></span> <span data-ttu-id="5d2b5-217">您可以輸入新資源群組的名稱，或現有資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-217">You can enter either the name of a new resource group or the name of a resource group that already exists.</span></span>
 * <span data-ttu-id="5d2b5-218">**位置**︰部署新虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-218">**Location**: Where to deploy the new virtual machine.</span></span> <span data-ttu-id="5d2b5-219">如果您想要將虛擬機器連線到內部部署網路，請務必選取將 Azure 連線到內部部署網路的虛擬網路位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-219">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span></span> <span data-ttu-id="5d2b5-220">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的 [Microsoft Azure 網路][planning-guide-microsoft-azure-networking]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-220">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>
2. <span data-ttu-id="5d2b5-221">：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-221">**Size**:</span></span>

     <span data-ttu-id="5d2b5-222">如需支援的 VM 類型清單，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-222">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="5d2b5-223">如果您想要使用進階儲存體，請務必選取正確的 VM 類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-223">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span></span> <span data-ttu-id="5d2b5-224">並非所有 VM 類型都支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-224">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="5d2b5-225">如需詳細資訊，請參閱[Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的[儲存體：Microsoft Azure 儲存體和資料磁碟][planning-guide-storage-microsoft-azure-storage-and-data-disks]和 [Azure 進階儲存體][planning-guide-azure-premium-storage]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-225">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

3. <span data-ttu-id="5d2b5-226">**設定**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-226">**Settings**:</span></span>
  * <span data-ttu-id="5d2b5-227">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-227">**Storage**</span></span>
    * <span data-ttu-id="5d2b5-228">**磁碟類型**：選取作業系統磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-228">**Disk Type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="5d2b5-229">如果您想要使用進階儲存體作為您的資料磁碟，建議您作業系統磁碟也使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-229">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
    * <span data-ttu-id="5d2b5-230">**使用受管理的磁碟**：如果您想要使用受管理的磁碟，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-230">**Use managed disks**: If you want to use Managed Disks, select Yes.</span></span> <span data-ttu-id="5d2b5-231">如需受控磁碟的詳細資訊，請參閱規劃指南中的[受管理磁碟][planning-guide-managed-disks]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-231">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in the planning guide.</span></span>
    * <span data-ttu-id="5d2b5-232">**儲存體帳戶**：選取現有的儲存體帳戶或建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-232">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="5d2b5-233">並非所有的儲存體類型都適用於執行 SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-233">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="5d2b5-234">如需儲存體類型的詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-234">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span>
  * <span data-ttu-id="5d2b5-235">**網路**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-235">**Network**</span></span>
    * <span data-ttu-id="5d2b5-236">**虛擬網路**和**子網路**：若要整合虛擬機器與內部網路，請選取連線到內部部署網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-236">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span></span>
    * <span data-ttu-id="5d2b5-237">**公用 IP 位址**︰選取您想要使用的公用 IP 位址，或輸入參數來建立新的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-237">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span></span> <span data-ttu-id="5d2b5-238">您可以使用公用 IP 位址，透過網際網路存取您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-238">You can use a public IP address to access your virtual machine over the Internet.</span></span> <span data-ttu-id="5d2b5-239">請務必也建立網路安全性群組，以便對您的虛擬機器進行安全的存取。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-239">Make sure that you also create a network security group to help secure access to your virtual machine.</span></span>
    * <span data-ttu-id="5d2b5-240">**網路安全性群組**：如需詳細資訊，請參閱[使用網路安全性群組控制網路流量流程][virtual-networks-nsg]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-240">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
  * <span data-ttu-id="5d2b5-241">**擴充功能**：您可以將虛擬機器擴充功能新增至部署中，藉此安裝安裝。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-241">**Extensions**: You can install virtual machine extensions by adding them to the deployment.</span></span> <span data-ttu-id="5d2b5-242">您不需要在此步驟新增擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-242">You do not need to add extensions in this step.</span></span> <span data-ttu-id="5d2b5-243">稍後會安裝 SAP 支援所需的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-243">The extensions required for SAP support are installed later.</span></span> <span data-ttu-id="5d2b5-244">請參閱本指南的[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-244">See chapter [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span></span>
  * <span data-ttu-id="5d2b5-245">**高可用性**：選取可用性設定組，或輸入參數來建立新的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-245">**High Availability**: Select an availability set, or enter the parameters to create a new availability set.</span></span> <span data-ttu-id="5d2b5-246">如需詳細資訊，請參閱 [Azure 可用性設定組][planning-guide-3.2.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-246">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
  * <span data-ttu-id="5d2b5-247">**監視**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-247">**Monitoring**</span></span>
    * <span data-ttu-id="5d2b5-248">**開機診斷**︰您可以選取 [停用] 開機診斷。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-248">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span></span>
    * <span data-ttu-id="5d2b5-249">**客體 OS 診斷**︰您可以選取 [停用] 監視診斷。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-249">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span></span>

4. <span data-ttu-id="5d2b5-250">**摘要**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-250">**Summary**:</span></span>

  <span data-ttu-id="5d2b5-251">檢閱您的選取項目，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-251">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="5d2b5-252">您的虛擬機器會部署於您選取的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-252">Your virtual machine is deployed in the resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="5d2b5-253">使用範本建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-253">Create a virtual machine by using a template</span></span>
<span data-ttu-id="5d2b5-254">您可以使用 [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github] 中發佈的其中一個 SAP 範本來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-254">You can create a virtual machine by using one of the SAP templates published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="5d2b5-255">您可以也使用 [Azure 入口網站][virtual-machines-windows-tutorial]、[PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms] 或 [Azure CLI][virtual-machines-linux-tutorial] 來手動建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-255">You also can manually create a virtual machine by using the [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="5d2b5-256">[**兩層組態 (僅只一部虛擬機器) 範本** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-256">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="5d2b5-257">若只要使用一部虛擬機器建立一個兩層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-257">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="5d2b5-258">[**兩層組態 (僅只一部虛擬機器) 範本 - 受管理磁碟** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-258">[**Two-tier configuration (only one virtual machine) template - Managed Disks** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]</span></span>

  <span data-ttu-id="5d2b5-259">若只要使用一部虛擬機器和受管理磁碟建立一個兩層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-259">To create a two-tier system by using only one virtual machine and Managed Disks, use this template.</span></span>
* <span data-ttu-id="5d2b5-260">[**三層組態 (多部虛擬機器) 範本** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-260">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="5d2b5-261">若要使用多部虛擬機器建立一個三層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-261">To create a three-tier system by using multiple virtual machines, use this template.</span></span>
* <span data-ttu-id="5d2b5-262">[**三層組態 (多部虛擬機器) 範本 - 受管理磁碟** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-262">[**Three-tier configuration (multiple virtual machines) template - Managed Disks** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]</span></span>

  <span data-ttu-id="5d2b5-263">若要使用多部虛擬機器和受管理磁碟建立一個三層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-263">To create a three-tier system by using multiple virtual machines and Managed Disks, use this template.</span></span>

<span data-ttu-id="5d2b5-264">在 Azure 入口網站中，輸入範本的下列參數：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-264">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="5d2b5-265">**基本**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-265">**Basics**:</span></span>
  * <span data-ttu-id="5d2b5-266">**訂用帳戶**：用來部署範本的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-266">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="5d2b5-267">**資源群組**：用來部署範本的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-267">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="5d2b5-268">您可以建立新的資源群組，也可以選取訂用帳戶中的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-268">You can create a new resource group, or you can select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="5d2b5-269">**位置**︰部署範本的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-269">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="5d2b5-270">如果您選取了現有的資源群組，則會使用該資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-270">If you selected an existing resource group, the location of that resource group is used.</span></span>

2. <span data-ttu-id="5d2b5-271">**設定**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-271">**Settings**:</span></span>
  * <span data-ttu-id="5d2b5-272">**SAP 系統識別碼**：SAP 系統識別碼 (SID)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-272">**SAP System ID**: The SAP System ID (SID).</span></span>
  * <span data-ttu-id="5d2b5-273">**OS 類型**：您想要部署的作業系統，例如，Windows Server 2012 R2、SUSE Linux Enterprise Server 12 (SLES 12)、Red Hat Enterprise Linux 7.2 (RHEL 7.2) 或 Oracle Linux 7.2。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-273">**OS type**: The operating system you want to deploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span></span>

    <span data-ttu-id="5d2b5-274">清單檢視不會顯示所有支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-274">The list view does not show all supported operating systems.</span></span> <span data-ttu-id="5d2b5-275">如需 SAP 軟體部署支援的作業系統詳細資訊，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-275">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="5d2b5-276">**SAP 系統大小**：SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-276">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="5d2b5-277">新系統所提供的 SAP 數量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-277">The number of SAPS the new system provides.</span></span> <span data-ttu-id="5d2b5-278">如果您不確定系統需要多少 SAP，請詢問您的 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-278">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="5d2b5-279">**系統可用性**：(僅限三層範本) 系統可用性。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-279">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="5d2b5-280">選取適合高可用性安裝組態的 **HA**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-280">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="5d2b5-281">為 ABAP SAP Central Services (ASCS) 建立兩部資料庫伺服器和兩部伺服器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-281">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="5d2b5-282">**儲存體類型**：(僅限兩層範本) 要使用的儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-282">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="5d2b5-283">對於大型系統，我們強烈建議使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-283">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="5d2b5-284">如需儲存體類型的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-284">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="5d2b5-285">[針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-285">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="5d2b5-286">[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-286">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="5d2b5-287">[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-287">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="5d2b5-288">[Microsoft Azure 儲存體簡介][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-288">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="5d2b5-289">**管理員使用者名稱**和**管理員密碼**：使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-289">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="5d2b5-290">建立新的使用者，以便登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-290">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="5d2b5-291">**新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-291">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="5d2b5-292">如果您已經有連線到內部部署網路的虛擬網路，請選取 [現有]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-292">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="5d2b5-293">**子網路識別碼**：虛擬機器將要連線的子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-293">**Subnet ID**: The ID of the subnet the virtual machines will connect to.</span></span> <span data-ttu-id="5d2b5-294">選取將虛擬機器連線到內部部署網路之虛擬私人網路 (VPN) 或 ExpressRoute 虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-294">Select the subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="5d2b5-295">識別碼通常如下所示：/subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱></span><span class="sxs-lookup"><span data-stu-id="5d2b5-295">The ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="5d2b5-296">**條款及條件**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-296">**Terms and conditions**:</span></span>  
    <span data-ttu-id="5d2b5-297">檢閱並接受法律條款。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-297">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="5d2b5-298">選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-298">Select **Purchase**.</span></span>

<span data-ttu-id="5d2b5-299">使用 Azure Marketplace 中的映像時，預設會部署 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-299">The Azure VM Agent is deployed by default when you use an image from the Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="5d2b5-300">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5d2b5-300">Configure proxy settings</span></span>
<span data-ttu-id="5d2b5-301">根據內部部署網路的設定方式，您可能需要在您的 VM 上設定 Proxy。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-301">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="5d2b5-302">如果 VM 已透過 VPN 或 ExpressRoute 連線到內部部署網路，VM 可能無法存取網際網路，而且無法下載所需的擴充功能或收集監視資料。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-302">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="5d2b5-303">如需詳細資訊，請參閱[設定 Proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-303">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="5d2b5-304">加入網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="5d2b5-304">Join a domain (Windows only)</span></span>
<span data-ttu-id="5d2b5-305">如果 Azure 部署連線到內部部署 Active Directory 或 DNS 執行個體，透過 Azure 站對站 VPN 連線或 ExpressRoute (在 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中稱為「跨單位」)，則 VM 應該加入內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-305">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="5d2b5-306">如需這項工作相關考量的詳細資訊，請參閱[將 VM 加入內部部署網域 (僅限 Windows)][deployment-guide-4.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-306">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <span data-ttu-id="5d2b5-307"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>設定監視</span><span class="sxs-lookup"><span data-stu-id="5d2b5-307"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configure monitoring</span></span>
<span data-ttu-id="5d2b5-308">若要確保 SAP 支援您的環境，請如[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 所述，設定 Azure Enhanced Monitoring Extension for SAP。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-308">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="5d2b5-309">請從 [SAP 資源][deployment-guide-2.2]所列的資源中，檢查 SAP 監視的必要條件，以及所需的最低 SAP 核心和 SAP Host Agent 版本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-309">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="5d2b5-310">監視檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-310">Monitoring check</span></span>
<span data-ttu-id="5d2b5-311">如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-311">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="5d2b5-312">部署後步驟</span><span class="sxs-lookup"><span data-stu-id="5d2b5-312">Post-deployment steps</span></span>
<span data-ttu-id="5d2b5-313">建立 VM 及部署 VM 之後，您需要在 VM 中安裝所需的軟體元件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-313">After you create the VM and the VM is deployed, you need to install the required software components in the VM.</span></span> <span data-ttu-id="5d2b5-314">由於這類 VM 部署中的部署/軟體安裝順序，要安裝的軟體必須已可在 Azure 中或另一部 VM 上使用，或成為可以附加的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-314">Because of the deployment/software installation sequence in this type of VM deployment, the software to be installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="5d2b5-315">否則，考慮使用可提供內部部署資產 (安裝共用) 連線的跨單位案例。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-315">Or, consider using a cross-premises scenario, in which connectivity to the on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="5d2b5-316">在 Azure 中部署您的 VM 之後，請遵循相同的指導方針和工具在 VM 上安裝 SAP 軟體，就像在內部部署環境中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-316">After you deploy your VM in Azure, follow the same guidelines and tools to install the SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="5d2b5-317">若要在 Azure VM 上安裝 SAP 軟體，SAP 和 Microsoft 建議將 SAP 安裝媒體上傳並儲存在 Azure VHD 或受管理磁碟上，或建立作為檔案伺服器並包含所有必要 SAP 安裝媒體的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-317">To install SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store the SAP installation media on Azure VHDs or Managed Disks, or that you create an Azure VM that works as a file server that has all the required SAP installation media.</span></span>

### <span data-ttu-id="5d2b5-318"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>案例 2：使用自訂映像為 SAP 部署 VM</span><span class="sxs-lookup"><span data-stu-id="5d2b5-318"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="5d2b5-319">因為不同版本的作業系統或 DBMS 有不同的修補需求，所以您在 Azure Marketplace 中找到的映像可能無法滿足您的需求。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-319">Because different versions of an operating system or DBMS have different patch requirements, the images you find in the Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="5d2b5-320">您可以改為使用自己的 OS/DBMS VM 映像來建立 VM，稍後再加以部署。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-320">You might instead want to create a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="5d2b5-321">您可以使用不同的步驟來建立適用於 Linux 的私人映像，而不是建立適用於 Windows 的映像。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-321">You use different steps to create a private image for Linux than to create one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="5d2b5-323">Windows</span><span class="sxs-lookup"><span data-stu-id="5d2b5-323">Windows</span></span>
>
> <span data-ttu-id="5d2b5-324">若要準備可用來部署多部虛擬機器的 Windows 映像，必須在內部部署 VM 上將 Windows 設定 (如 Windows SID 和主機名稱) 抽象化或一般化。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-324">To prepare a Windows image that you can use to deploy multiple virtual machines, the Windows settings (like Windows SID and hostname) must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="5d2b5-325">您可以使用 [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) 來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-325">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) to do this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="5d2b5-327">Linux</span><span class="sxs-lookup"><span data-stu-id="5d2b5-327">Linux</span></span>
>
> <span data-ttu-id="5d2b5-328">若要準備可用來部署多部虛擬機器的 Linux 映像，必須在內部部署 VM 上抽象化或一般化一些 Linux 設定。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-328">To prepare a Linux image that you can use to deploy multiple virtual machines, some Linux settings must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="5d2b5-329">您可以使用 `waagent -deprovision` 來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-329">You can use `waagent -deprovision`  to do this.</span></span> <span data-ttu-id="5d2b5-330">如需詳細資訊，請參閱[擷取在 Azure 上執行的 Linux 虛擬機器][virtual-machines-linux-capture-image]和 [Azure Linux 代理程式使用者指南][virtual-machines-linux-agent-user-guide-command-line-options]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-330">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and the [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="5d2b5-331">您可以準備和建立自訂映像，然後使用它來建立多個新 VM。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-331">You can prepare and create a custom image, and then use it to create multiple new VMs.</span></span> <span data-ttu-id="5d2b5-332">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-332">This is described in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span> <span data-ttu-id="5d2b5-333">藉由使用 SAP Software Provision Manager 來安裝新的 SAP 系統、從附加至虛擬機器的磁碟還原資料庫備份，或直接從 Azure 儲存體還原資料庫備份 (如果 DBMS 支援的話)，來設定您的資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-333">Set up your database content either by using SAP Software Provisioning Manager to install a new SAP system (restores a database backup from a disk that's attached to the virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="5d2b5-334">如需詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-334">For more information, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span> <span data-ttu-id="5d2b5-335">如果您已在內部部署 VM (特別針對二層系統) 中安裝 SAP 系統，您可以在部署 Azure VM 之後，使用 SAP Software Provisioning Manager 支援的「系統重新命名」程序來調整 SAP 系統設定 (SAP Note [1619720])。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-335">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt the SAP system settings after the deployment of the Azure VM by using the System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="5d2b5-336">否則，您可以在部署 Azure VM 之後安裝 SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-336">Otherwise, you can install the SAP software after you deploy the Azure VM.</span></span>

<span data-ttu-id="5d2b5-337">下列流程圖顯示從自訂映像部署 VM 的 SAP 特定步驟順序：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-337">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![使用私人 Marketplace 中的 VM 映像部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-the-azure-portal"></a><span data-ttu-id="5d2b5-339">使用 Azure 入口網站建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-339">Create a virtual machine by using the Azure portal</span></span>
<span data-ttu-id="5d2b5-340">要從受管理磁碟映像建立新的虛擬機器，最簡單方式就是使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-340">The easiest way to create a new virtual machine from a Managed Disk image is by using the Azure portal.</span></span> <span data-ttu-id="5d2b5-341">如需如何建立受管理磁碟映像的詳細資訊，請參閱[在 Azure 中擷取一般化 VM 的受管理映像](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-341">For more information on how to create a Manage Disk Image, read [Capture a managed image of a generalized VM in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)</span></span>

1.  <span data-ttu-id="5d2b5-342">移至 <https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-342">Go to <https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>.</span></span> <span data-ttu-id="5d2b5-343">或者，在 Azure 入口網站的功能表中選取 [映像]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-343">Or, in the Azure portal menu, select **Images**.</span></span>
2.  <span data-ttu-id="5d2b5-344">選取要部署的受管理磁碟映像，然後按一下 [建立 VM]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-344">Select the Managed Disk image you want to deploy and click on **Create VM**</span></span>

<span data-ttu-id="5d2b5-345">除了所有必要的資源 (例如網路介面或儲存體帳戶) 以外，此精靈會引導您完成必要參數設定以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-345">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="5d2b5-346">其中一些參數包括︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-346">Some of these parameters are:</span></span>

1. <span data-ttu-id="5d2b5-347">**基本**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-347">**Basics**:</span></span>
 * <span data-ttu-id="5d2b5-348">**名稱**：資源名稱 (虛擬機器名稱)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-348">**Name**: The name of the resource (the virtual machine name).</span></span>
 * <span data-ttu-id="5d2b5-349">**VM 磁碟類型**：選取作業系統磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-349">**VM disk type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="5d2b5-350">如果您想要使用進階儲存體作為您的資料磁碟，建議您作業系統磁碟也使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-350">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
 * <span data-ttu-id="5d2b5-351">**使用者名稱和密碼**或 **SSH 公用金鑰**︰輸入在佈建期間建立之使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-351">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span></span> <span data-ttu-id="5d2b5-352">對於 Linux 虛擬機器，您可以輸入要用來登入電腦的公開安全殼層 (SSH) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-352">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span></span>
 * <span data-ttu-id="5d2b5-353">**訂用帳戶**：選取您想要用來佈建新虛擬機器的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-353">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span></span>
 * <span data-ttu-id="5d2b5-354">**資源群組**：VM 的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-354">**Resource group**: The name of the resource group for the VM.</span></span> <span data-ttu-id="5d2b5-355">您可以輸入新資源群組的名稱，或現有資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-355">You can enter either the name of a new resource group or the name of a resource group that already exists.</span></span>
 * <span data-ttu-id="5d2b5-356">**位置**︰部署新虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-356">**Location**: Where to deploy the new virtual machine.</span></span> <span data-ttu-id="5d2b5-357">如果您想要將虛擬機器連線到內部部署網路，請務必選取將 Azure 連線到內部部署網路的虛擬網路位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-357">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span></span> <span data-ttu-id="5d2b5-358">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的 [Microsoft Azure 網路][planning-guide-microsoft-azure-networking]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-358">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>
2. <span data-ttu-id="5d2b5-359">：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-359">**Size**:</span></span>

     <span data-ttu-id="5d2b5-360">如需支援的 VM 類型清單，請參閱 SAP Note [1928533]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-360">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="5d2b5-361">如果您想要使用進階儲存體，請務必選取正確的 VM 類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-361">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span></span> <span data-ttu-id="5d2b5-362">並非所有 VM 類型都支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-362">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="5d2b5-363">如需詳細資訊，請參閱[Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中的[儲存體：Microsoft Azure 儲存體和資料磁碟][planning-guide-storage-microsoft-azure-storage-and-data-disks]和 [Azure 進階儲存體][planning-guide-azure-premium-storage]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-363">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

3. <span data-ttu-id="5d2b5-364">**設定**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-364">**Settings**:</span></span>
  * <span data-ttu-id="5d2b5-365">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-365">**Storage**</span></span>
    * <span data-ttu-id="5d2b5-366">**磁碟類型**：選取作業系統磁碟的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-366">**Disk Type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="5d2b5-367">如果您想要使用進階儲存體作為您的資料磁碟，建議您作業系統磁碟也使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-367">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
    * <span data-ttu-id="5d2b5-368">**使用受管理的磁碟**：如果您想要使用受管理的磁碟，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-368">**Use managed disks**: If you want to use Managed Disks, select Yes.</span></span> <span data-ttu-id="5d2b5-369">如需受控磁碟的詳細資訊，請參閱規劃指南中的[受管理磁碟][planning-guide-managed-disks]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-369">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in the planning guide.</span></span>
  * <span data-ttu-id="5d2b5-370">**網路**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-370">**Network**</span></span>
    * <span data-ttu-id="5d2b5-371">**虛擬網路**和**子網路**：若要整合虛擬機器與內部網路，請選取連線到內部部署網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-371">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span></span>
    * <span data-ttu-id="5d2b5-372">**公用 IP 位址**︰選取您想要使用的公用 IP 位址，或輸入參數來建立新的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-372">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span></span> <span data-ttu-id="5d2b5-373">您可以使用公用 IP 位址，透過網際網路存取您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-373">You can use a public IP address to access your virtual machine over the Internet.</span></span> <span data-ttu-id="5d2b5-374">請務必也建立網路安全性群組，以便對您的虛擬機器進行安全的存取。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-374">Make sure that you also create a network security group to help secure access to your virtual machine.</span></span>
    * <span data-ttu-id="5d2b5-375">**網路安全性群組**：如需詳細資訊，請參閱[使用網路安全性群組控制網路流量流程][virtual-networks-nsg]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-375">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
  * <span data-ttu-id="5d2b5-376">**擴充功能**：您可以將虛擬機器擴充功能新增至部署中，藉此安裝安裝。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-376">**Extensions**: You can install virtual machine extensions by adding them to the deployment.</span></span> <span data-ttu-id="5d2b5-377">您不需要在此步驟新增擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-377">You do not need to add extension in this step.</span></span> <span data-ttu-id="5d2b5-378">稍後會安裝 SAP 支援所需的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-378">The extensions required for SAP support are installed later.</span></span> <span data-ttu-id="5d2b5-379">請參閱本指南的[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-379">See chapter [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span></span>
  * <span data-ttu-id="5d2b5-380">**高可用性**：選取可用性設定組，或輸入參數來建立新的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-380">**High Availability**: Select an availability set, or enter the parameters to create a new availability set.</span></span> <span data-ttu-id="5d2b5-381">如需詳細資訊，請參閱 [Azure 可用性設定組][planning-guide-3.2.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-381">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
  * <span data-ttu-id="5d2b5-382">**監視**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-382">**Monitoring**</span></span>
    * <span data-ttu-id="5d2b5-383">**開機診斷**︰您可以選取 [停用] 開機診斷。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-383">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span></span>
    * <span data-ttu-id="5d2b5-384">**客體 OS 診斷**︰您可以選取 [停用] 監視診斷。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-384">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span></span>

4. <span data-ttu-id="5d2b5-385">**摘要**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-385">**Summary**:</span></span>

  <span data-ttu-id="5d2b5-386">檢閱您的選取項目，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-386">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="5d2b5-387">您的虛擬機器會部署於您選取的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-387">Your virtual machine is deployed in the resource group you selected.</span></span>
#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="5d2b5-388">使用範本建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-388">Create a virtual machine by using a template</span></span>
<span data-ttu-id="5d2b5-389">若要透過 Azure 入口網站使用私人 OS 映像來建立部署，請使用下列其中一個 SAP 範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-389">To create a deployment by using a private OS image from the Azure portal, use one of the following SAP templates.</span></span> <span data-ttu-id="5d2b5-390">這些是 [azure-quickstart-templates GitHub 儲存機制][azure-quickstart-templates-github]中發佈的範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-390">These templates are published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="5d2b5-391">您可以也使用 [PowerShell][virtual-machines-upload-image-windows-resource-manager] 手動建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-391">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="5d2b5-392">[**兩層組態 (僅限一部虛擬機器) 範本** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-392">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="5d2b5-393">若只要使用一部虛擬機器建立一個兩層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-393">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="5d2b5-394">[**兩層組態 (僅只一部虛擬機器) 範本 - 受管理磁碟映像** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-394">[**Two-tier configuration (only one virtual machine) template - Managed Disk Image** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]</span></span>

  <span data-ttu-id="5d2b5-395">若只要使用一部虛擬機器和受管理磁碟映像建立一個兩層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-395">To create a two-tier system by using only one virtual machine and a Managed Disk image, use this template.</span></span>
* <span data-ttu-id="5d2b5-396">[**三層組態 (多部虛擬機器) 範本** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-396">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="5d2b5-397">若要使用多部虛擬機器或自己的 OS 映像建立一個三層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-397">To create a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>
* <span data-ttu-id="5d2b5-398">[**三層組態 (多部虛擬機器) 範本 - 受管理磁碟映像** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-398">[**Three-tier configuration (multiple virtual machines) template - Managed Disk Image** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]</span></span>

  <span data-ttu-id="5d2b5-399">若要使用多部虛擬機器或自己的 OS 映像和受管理磁碟映像建立一個三層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-399">To create a three-tier system by using multiple virtual machines or your own OS image and a Managed Disk image, use this template.</span></span>

<span data-ttu-id="5d2b5-400">在 Azure 入口網站中，輸入範本的下列參數：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-400">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="5d2b5-401">**基本**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-401">**Basics**:</span></span>
  * <span data-ttu-id="5d2b5-402">**訂用帳戶**：用來部署範本的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-402">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="5d2b5-403">**資源群組**：用來部署範本的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-403">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="5d2b5-404">您可以建立新的資源群組，或選取訂用帳戶中的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-404">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="5d2b5-405">**位置**︰部署範本的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-405">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="5d2b5-406">如果您選取了現有的資源群組，則會使用該資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-406">If you selected an existing resource group, the location of that resource group is used.</span></span>
2. <span data-ttu-id="5d2b5-407">**設定**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-407">**Settings**:</span></span>
  * <span data-ttu-id="5d2b5-408">**SAP 系統識別碼**：SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-408">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="5d2b5-409">**OS 類型**：您想要部署的作業系統類型 (Windows 或 Linux)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-409">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="5d2b5-410">**SAP 系統大小**：SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-410">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="5d2b5-411">新系統所提供的 SAP 數量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-411">The number of SAPS the new system provides.</span></span> <span data-ttu-id="5d2b5-412">如果您不確定系統需要多少 SAP，請詢問您的 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-412">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="5d2b5-413">**系統可用性**：(僅限三層範本) 系統可用性。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-413">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="5d2b5-414">選取適合高可用性安裝組態的 **HA**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-414">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="5d2b5-415">為 ASCS 建立兩部資料庫伺服器和兩部伺服器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-415">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="5d2b5-416">**儲存體類型**：(僅限兩層範本) 要使用的儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-416">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="5d2b5-417">對於大型系統，我們強烈建議使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-417">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="5d2b5-418">如需儲存體類型的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-418">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="5d2b5-419">[針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-419">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="5d2b5-420">[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-420">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="5d2b5-421">[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-421">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="5d2b5-422">[Microsoft Azure 儲存體簡介][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-422">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="5d2b5-423">**使用者映像 VHD URI** (僅限非受管理磁碟映像範本)：私人 OS 映像 VHD 的 URI，例如 https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-423">**User image VHD URI** (unmanaged disk image template only): The URI of the private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="5d2b5-424">**使用者映像儲存體帳戶** (僅限非受管理磁碟映像範本)：私人 OS 映像儲存所在的儲存體帳戶名稱，例如 &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-424">**User image storage account** (unmanaged disk image template only): The name of the storage account where the private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="5d2b5-425">**userImageId** (僅限非受管理磁碟映像範本)：您想要使用的受管理磁碟映像的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-425">**userImageId** (managed disk image template only): Id of the Managed Disk image you want to use</span></span>
  * <span data-ttu-id="5d2b5-426">**管理員使用者名稱**和**管理員密碼**：使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-426">**Admin username** and **Admin password**: The username and password.</span></span>

    <span data-ttu-id="5d2b5-427">建立新的使用者，以便登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-427">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="5d2b5-428">**新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-428">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="5d2b5-429">如果您已經有連線到內部部署網路的虛擬網路，請選取 [現有]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-429">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="5d2b5-430">**子網路識別碼**：虛擬機器將要連線的子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-430">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="5d2b5-431">選取用於將虛擬機器連線到內部部署網路之 VPN 或 ExpressRoute 虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-431">Select the subnet of your VPN or ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="5d2b5-432">識別碼通常看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-432">The ID usually looks like this:</span></span>

    <span data-ttu-id="5d2b5-433">/subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱></span><span class="sxs-lookup"><span data-stu-id="5d2b5-433">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="5d2b5-434">**條款及條件**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-434">**Terms and conditions**:</span></span>  
    <span data-ttu-id="5d2b5-435">檢閱並接受法律條款。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-435">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="5d2b5-436">選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-436">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent-linux-only"></a><span data-ttu-id="5d2b5-437">安裝 VM 代理程式 (僅限 Linux)</span><span class="sxs-lookup"><span data-stu-id="5d2b5-437">Install the VM Agent (Linux only)</span></span>
<span data-ttu-id="5d2b5-438">若要使用上一節所述的範本，必須已在使用者映像中安裝 Linux 代理程式，否則部署會失敗。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-438">To use the templates described in the preceding section, the Linux Agent must already be installed in the user image, or the deployment will fail.</span></span> <span data-ttu-id="5d2b5-439">如[下載、安裝和啟用 Azure VM 代理程式][deployment-guide-4.4]所述，下載 VM 代理程式並安裝於使用者映像中。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-439">Download and install the VM Agent in the user image as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="5d2b5-440">如果您未使用範本，稍後也可以安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-440">If you don’t use the templates, you also can install the VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="5d2b5-441">加入網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="5d2b5-441">Join a domain (Windows only)</span></span>
<span data-ttu-id="5d2b5-442">如果 Azure 部署連線到內部部署 Active Directory 或 DNS 執行個體，透過 Azure 站對站 VPN 連線或 Azure ExpressRoute (在[Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中稱為「跨單位」)，則 VM 應該加入內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-442">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="5d2b5-443">如需這個步驟相關考量的詳細資訊，請參閱[將 VM 加入內部部署網域 (僅限 Windows)][deployment-guide-4.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-443">For more information about considerations for this step, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="5d2b5-444">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5d2b5-444">Configure proxy settings</span></span>
<span data-ttu-id="5d2b5-445">根據內部部署網路的設定方式，您可能需要在您的 VM 上設定 Proxy。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-445">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="5d2b5-446">如果 VM 已透過 VPN 或 ExpressRoute 連線到內部部署網路，VM 可能無法存取網際網路，而且無法下載所需的擴充功能或收集監視資料。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-446">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="5d2b5-447">如需詳細資訊，請參閱[設定 Proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-447">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="5d2b5-448">設定監視</span><span class="sxs-lookup"><span data-stu-id="5d2b5-448">Configure monitoring</span></span>
<span data-ttu-id="5d2b5-449">若要確保 SAP 支援您的環境，請如[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 所述，設定 Azure Enhanced Monitoring Extension for SAP。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-449">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="5d2b5-450">請從 [SAP 資源][deployment-guide-2.2]所列的資源中，檢查 SAP 監視的必要條件，以及所需的最低 SAP 核心和 SAP Host Agent 版本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-450">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="5d2b5-451">監視檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-451">Monitoring check</span></span>
<span data-ttu-id="5d2b5-452">如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-452">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>


### <span data-ttu-id="5d2b5-453"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>案例 3：使用非一般化 Azure VHD 搭配 SAP 來移動內部部署 VM</span><span class="sxs-lookup"><span data-stu-id="5d2b5-453"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="5d2b5-454">在此情況下，您會規劃將特定 SAP 系統從內部部署環境移至 Azure。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-454">In this scenario, you plan to move a specific SAP system from an on-premises environment to Azure.</span></span> <span data-ttu-id="5d2b5-455">將包含 OS、SAP 二進位檔和最終 DBMS 二進位檔的 VHD，以及包含 DBMS 資料和記錄檔的 VHD 上傳至 Azure，即可達成。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-455">You can do this by uploading the VHD that has the OS, the SAP binaries, and eventually the DBMS binaries, plus the VHDs with the data and log files of the DBMS, to Azure.</span></span> <span data-ttu-id="5d2b5-456">不同於[案例 2：使用 SAP 適用的自訂映像部署 VM][deployment-guide-3.3] 中所述的案例，在此情況下，您可以在 Azure VM 中保留主機名稱、SAP SID 和 SAP 使用者帳戶，因為這些項目設定於內部部署環境中。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-456">Unlike the scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep the hostname, SAP SID, and SAP user accounts in the Azure VM, because they were configured in the on-premises environment.</span></span> <span data-ttu-id="5d2b5-457">您不需要將 OS 一般化。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-457">You do not need to generalize the OS.</span></span> <span data-ttu-id="5d2b5-458">此案例最適用於跨單位案例，其中部分的 SAP 架構是在內部部署執行，部分則在 Azure 上執行。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-458">This scenario applies most often to cross-premises scenarios where part of the SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="5d2b5-459">在此案例中，**不會**在部署期間自動安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-459">In this scenario, the VM Agent is **not** automatically installed during deployment.</span></span> <span data-ttu-id="5d2b5-460">由於 VM 代理程式和 Azure Enhanced Monitoring Extension for SAP 是在 Azure 上執行 SAP NetWeaver 的必要元件，因此在建立虛擬機器之後，您必須手動下載、安裝和啟用這兩個元件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-460">Because the VM Agent and the Azure Enhanced Monitoring Extension for SAP are required to run SAP NetWeaver on Azure, you need to download, install, and enable both components manually after you create the virtual machine.</span></span>

<span data-ttu-id="5d2b5-461">如需 Azure VM 代理程式的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-461">For more information about the Azure VM Agent, see the following resources.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="5d2b5-463">Windows</span><span class="sxs-lookup"><span data-stu-id="5d2b5-463">Windows</span></span>
>
> <span data-ttu-id="5d2b5-464">[Azure 虛擬機器代理程式概觀][virtual-machines-windows-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-464">[Azure Virtual Machine Agent overview][virtual-machines-windows-agent-user-guide]</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="5d2b5-466">Linux</span><span class="sxs-lookup"><span data-stu-id="5d2b5-466">Linux</span></span>
>
> <span data-ttu-id="5d2b5-467">[Azure Linux 代理程式使用者指南][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-467">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="5d2b5-468">下列流程圖說明使用非一般化 Azure VHD 移動內部部署 VM 的步驟順序︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-468">The following flowchart shows the sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![使用 VM 磁碟部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-400]

<span data-ttu-id="5d2b5-470">如果磁碟已上傳並在 Azure 中定義 (請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide])，請執行後面幾節所述的工作。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-470">If the disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), do the tasks described in the next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="5d2b5-471">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-471">Create a virtual machine</span></span>
<span data-ttu-id="5d2b5-472">若要透過 Azure 入口網站使用私人 OS 磁碟來建立部署，請使用 [azure-quickstart-templates Github 儲存機制][azure-quickstart-templates-github]中所發佈的 SAP 範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-472">To create a deployment by using a private OS disk through the Azure portal, use the SAP template published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="5d2b5-473">您可以也使用 PowerShell 手動建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-473">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="5d2b5-474">[**兩層組態 (僅限一部虛擬機器) 範本**  (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-474">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="5d2b5-475">若只要使用一部虛擬機器建立一個兩層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-475">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="5d2b5-476">[**兩層組態 (僅限一部虛擬機器) 範本 - 受管理磁碟** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-476">[**Two-tier configuration (only one virtual machine) template - Managed Disk** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]</span></span>

  <span data-ttu-id="5d2b5-477">若只要使用一部虛擬機器和受管理磁碟建立一個兩層系統，請使用此範本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-477">To create a two-tier system by using only one virtual machine and a Managed Disk, use this template.</span></span>

<span data-ttu-id="5d2b5-478">在 Azure 入口網站中，輸入範本的下列參數：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-478">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="5d2b5-479">**基本**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-479">**Basics**:</span></span>
  * <span data-ttu-id="5d2b5-480">**訂用帳戶**：用來部署範本的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-480">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="5d2b5-481">**資源群組**：用來部署範本的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-481">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="5d2b5-482">您可以建立新的資源群組，或選取訂用帳戶中的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-482">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="5d2b5-483">**位置**︰部署範本的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-483">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="5d2b5-484">如果您選取了現有的資源群組，則會使用該資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-484">If you selected an existing resource group, the location of that resource group is used.</span></span>
2. <span data-ttu-id="5d2b5-485">**設定**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-485">**Settings**:</span></span>
  * <span data-ttu-id="5d2b5-486">**SAP 系統識別碼**：SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-486">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="5d2b5-487">**OS 類型**：您想要部署的作業系統類型 (Windows 或 Linux)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-487">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="5d2b5-488">**SAP 系統大小**：SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-488">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="5d2b5-489">新系統所提供的 SAP 數量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-489">The number of SAPS the new system provides.</span></span> <span data-ttu-id="5d2b5-490">如果您不確定系統需要多少 SAP，請詢問您的 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-490">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="5d2b5-491">**儲存體類型**：(僅限兩層範本) 要使用的儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-491">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="5d2b5-492">對於大型系統，我們強烈建議使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-492">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="5d2b5-493">如需儲存體類型的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-493">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="5d2b5-494">[針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-494">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="5d2b5-495">[適用於 SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-495">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="5d2b5-496">[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-496">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="5d2b5-497">[Microsoft Azure 儲存體簡介][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="5d2b5-497">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="5d2b5-498">**OS 磁碟 VHD URI** (僅限非受管理磁碟範本)：私人 OS 磁碟的 URI，例如 https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-498">**OS disk VHD URI** (unmanaged disk template only): The URI of the private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="5d2b5-499">**作業系統磁碟受管理磁碟識別碼** (僅限非受管理磁碟範本)：作業系統磁碟 /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN 的受管理磁碟識別碼</span><span class="sxs-lookup"><span data-stu-id="5d2b5-499">**OS disk Managed Disk Id** (managed disk template only): The Id of the Managed Disk OS disk, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN</span></span>
  * <span data-ttu-id="5d2b5-500">**新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-500">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="5d2b5-501">如果您已經有連線到內部部署網路的虛擬網路，請選取 [現有]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-501">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="5d2b5-502">**子網路識別碼**：虛擬機器將要連線的子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-502">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="5d2b5-503">選取用於將虛擬機器連線到內部部署網路之 VPN 或 Azure ExpressRoute 虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-503">Select the subnet of your VPN or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="5d2b5-504">識別碼通常看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-504">The ID usually looks like this:</span></span>

    <span data-ttu-id="5d2b5-505">/subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱></span><span class="sxs-lookup"><span data-stu-id="5d2b5-505">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="5d2b5-506">**條款及條件**：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-506">**Terms and conditions**:</span></span>  
    <span data-ttu-id="5d2b5-507">檢閱並接受法律條款。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-507">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="5d2b5-508">選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-508">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent"></a><span data-ttu-id="5d2b5-509">安裝 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="5d2b5-509">Install the VM Agent</span></span>
<span data-ttu-id="5d2b5-510">若要使用上一節所述的範本，必須在 OS 磁碟上安裝 VM 代理程式，否則部署會失敗。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-510">To use the templates described in the preceding section, the VM Agent must be installed on the OS disk, or the deployment will fail.</span></span> <span data-ttu-id="5d2b5-511">如[下載、安裝和啟用 Azure VM 代理程式][deployment-guide-4.4]所述，下載 VM 代理程式並安裝於 VM 中。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-511">Download and install the VM Agent in the VM, as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="5d2b5-512">如果您未使用上一節所述的範本，則之後也可以安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-512">If you don't use the templates described in the preceding section, you can also install the VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="5d2b5-513">加入網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="5d2b5-513">Join a domain (Windows only)</span></span>
<span data-ttu-id="5d2b5-514">如果 Azure 部署連線到內部部署 Active Directory 或 DNS 執行個體，透過 Azure 站對站 VPN 連線或 ExpressRoute (在 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]中稱為「跨單位」)，則 VM 應該加入內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-514">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="5d2b5-515">如需這項工作相關考量的詳細資訊，請參閱[將 VM 加入內部部署網域 (僅限 Windows)][deployment-guide-4.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-515">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="5d2b5-516">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5d2b5-516">Configure proxy settings</span></span>
<span data-ttu-id="5d2b5-517">根據內部部署網路的設定方式，您可能需要在您的 VM 上設定 Proxy。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-517">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="5d2b5-518">如果 VM 已透過 VPN 或 ExpressRoute 連線到內部部署網路，VM 可能無法存取網際網路，而且無法下載所需的擴充功能或收集監視資料。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-518">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="5d2b5-519">如需詳細資訊，請參閱[設定 Proxy][deployment-guide-configure-proxy]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-519">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="5d2b5-520">設定監視</span><span class="sxs-lookup"><span data-stu-id="5d2b5-520">Configure monitoring</span></span>
<span data-ttu-id="5d2b5-521">若要確保 SAP 支援您的環境，請如[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 所述，設定 Azure Enhanced Monitoring Extension for SAP。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-521">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="5d2b5-522">請從 [SAP 資源][deployment-guide-2.2]所列的資源中，檢查 SAP 監視的必要條件，以及所需的最低 SAP 核心和 SAP Host Agent 版本。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-522">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="5d2b5-523">監視檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-523">Monitoring check</span></span>
<span data-ttu-id="5d2b5-524">如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-524">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-the-monitoring-configuration-for-sap"></a><span data-ttu-id="5d2b5-525">更新 SAP 的監視組態</span><span class="sxs-lookup"><span data-stu-id="5d2b5-525">Update the monitoring configuration for SAP</span></span>
<span data-ttu-id="5d2b5-526">在下列任何一個案例中，更新 SAP 監視組態︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-526">Update the SAP monitoring configuration in any of the following scenarios:</span></span>
* <span data-ttu-id="5d2b5-527">聯合 Microsoft/SAP 小組延伸監視功能，並要求增加或減少計數器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-527">The joint Microsoft/SAP team extends the monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="5d2b5-528">Microsoft 推出新版本的基礎 Azure 基礎結構來提供監視資料，而 Azure Enhanced Monitoring Extension for SAP 必須配合這些變更。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-528">Microsoft introduces a new version of the underlying Azure infrastructure that delivers the monitoring data, and the Azure Enhanced Monitoring Extension for SAP needs to be adapted to those changes.</span></span>
* <span data-ttu-id="5d2b5-529">您將額外的資料磁碟掛接到 Azure VM 或是移除資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-529">You mount additional data disks to your Azure VM or you remove a data disk.</span></span> <span data-ttu-id="5d2b5-530">在此案例中，更新儲存體相關資料的集合。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-530">In this scenario, update the collection of storage-related data.</span></span> <span data-ttu-id="5d2b5-531">藉由新增或刪除端點或將 IP 位址指派給 VM 來變更組態，就不會影響監視組態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-531">Changing your configuration by adding or deleting endpoints or by assigning IP addresses to a VM does not affect the monitoring configuration.</span></span>
* <span data-ttu-id="5d2b5-532">您可變更 Azure VM 的大小 (例如從大小 A5 變更成任何其他 VM 大小)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-532">You change the size of your Azure VM, for example, from size A5 to any other VM size.</span></span>
* <span data-ttu-id="5d2b5-533">您可以在 Azure VM 中新增網路介面。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-533">You add new network interfaces to your Azure VM.</span></span>

<span data-ttu-id="5d2b5-534">若要更新監視設定，請依照[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 中的步驟來更新監視基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-534">To update monitoring settings, update the monitoring infrastructure by following the steps in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment"></a><span data-ttu-id="5d2b5-535">SAP 軟體部署的詳細工作</span><span class="sxs-lookup"><span data-stu-id="5d2b5-535">Detailed tasks for SAP software deployment</span></span>
<span data-ttu-id="5d2b5-536">本節包含在設定和部署程序中執行特定工作的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-536">This section has detailed steps for doing specific tasks in the configuration and deployment process.</span></span>

### <span data-ttu-id="5d2b5-537"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>部署 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5d2b5-537"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="5d2b5-538">前往 [Microsoft Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-538">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="5d2b5-539">在**命令列工具**的 **PowerShell** 之下，選取 [Windows 安裝]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-539">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
3.  <span data-ttu-id="5d2b5-540">在 [Microsoft 下載管理員] 對話方塊中，針對已下載的檔案 (例如，WindowsAzurePowershellGet.3f.3f.3fnew.exe) 選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-540">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="5d2b5-541">若要執行 Microsoft Web Platform Installer (Microsoft Web PI)，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-541">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="5d2b5-542">如下所示的頁面隨即出現︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-542">A page that looks like this appears:</span></span>

  <span data-ttu-id="5d2b5-543">![Azure PowerShell Cmdlet 的安裝頁面][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-543">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="5d2b5-544">選取 [安裝]，然後接受 Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-544">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="5d2b5-545">已安裝 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-545">PowerShell is installed.</span></span> <span data-ttu-id="5d2b5-546">選取 [完成]以關閉安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-546">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="5d2b5-547">經常檢查 PowerShell Cmdlet 的更新 (通常每個月更新一次)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-547">Check frequently for updates to the PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="5d2b5-548">檢查更新的最簡單方式是繼續執行安裝步驟，直到步驟 5 所示的安裝頁面為止。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-548">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span> <span data-ttu-id="5d2b5-549">Cmdlet 的發行日期和版次號碼包含在步驟 5 所示的頁面上。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-549">The release date and release number of the cmdlets are included on the page shown in step 5.</span></span> <span data-ttu-id="5d2b5-550">除非 SAP Note [1928533] 或 SAP Note [2015553] 另外指定，否則建議使用最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-550">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with the latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="5d2b5-551">若要檢查電腦上安裝的 Azure PowerShell Cmdlet 版本，請執行此 PowerShell 命令︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-551">To check the version of the Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
(Get-Module AzureRm.Compute).Version
```
<span data-ttu-id="5d2b5-552">結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-552">The result looks like this:</span></span>

<span data-ttu-id="5d2b5-553">![Azure PowerShell Cmdlet 版本檢查的結果][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-553">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="5d2b5-554">如果電腦上安裝的 Azure Cmdlet 版本是最新版本，則安裝精靈的第一頁會將 **(已安裝)** 新增至產品標題 (請參閱下列螢幕擷取畫面)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-554">If the Azure cmdlet version installed on your computer is the current version, the first page of the installation wizard indicates it by adding **(Installed)** to the product title (see the following screenshot).</span></span> <span data-ttu-id="5d2b5-555">您的 PowerShell Azure Cmdlet 都是最新的。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-555">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="5d2b5-556">若要關閉安裝精靈，請選取 [結束]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-556">To close the installation wizard, select **Exit**.</span></span>

<span data-ttu-id="5d2b5-557">![Azure PowerShell Cmdlet 的安裝頁面，表示已安裝最新版的 Azure PowerShell Cmdlet][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-557">![Installation page for Azure PowerShell cmdlets indicating that the most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <span data-ttu-id="5d2b5-558"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>部署 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5d2b5-558"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Deploy Azure CLI</span></span>
1.  <span data-ttu-id="5d2b5-559">前往 [Microsoft Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-559">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="5d2b5-560">在**命令列工具**的 **Azure 命令列介面**之下，選取您作業系統的 [安裝] 連結。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-560">Under **Command-line tools**, under **Azure command-line interface**, select the **Install** link for your operating system.</span></span>
3.  <span data-ttu-id="5d2b5-561">在 [Microsoft 下載管理員] 對話方塊中，針對已下載的檔案 (例如，WindowsAzureXPlatCLI.3f.3f.3fnew.exe) 選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-561">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="5d2b5-562">若要執行 Microsoft Web Platform Installer (Microsoft Web PI)，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-562">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="5d2b5-563">如下所示的頁面隨即出現︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-563">A page that looks like this appears:</span></span>

  <span data-ttu-id="5d2b5-564">![Azure PowerShell Cmdlet 的安裝頁面][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-564">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="5d2b5-565">選取 [安裝]，然後接受 Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-565">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="5d2b5-566">已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-566">Azure CLI is installed.</span></span> <span data-ttu-id="5d2b5-567">選取 [完成]以關閉安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-567">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="5d2b5-568">經常檢查 Azure CLI 的更新 (通常每個月更新一次)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-568">Check frequently for updates to Azure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="5d2b5-569">檢查更新的最簡單方式是繼續執行安裝步驟，直到步驟 5 所示的安裝頁面為止。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-569">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span>

<span data-ttu-id="5d2b5-570">若要檢查電腦上安裝的 Azure CLI 版本，請執行此命令︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-570">To check the version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="5d2b5-571">結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-571">The result looks like this:</span></span>

<span data-ttu-id="5d2b5-572">![Azure CLI 版本檢查的結果][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-572">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <span data-ttu-id="5d2b5-573"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>將 VM 加入內部部署網域 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="5d2b5-573"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Join a VM to an on-premises domain (Windows only)</span></span>
<span data-ttu-id="5d2b5-574">如果在跨單位案例 (於 Azure 擴充內部部署 Active Directory 和 DNS) 中部署 SAP VM，則必須將 VM 加入內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-574">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that the VMs are joining an on-premises domain.</span></span> <span data-ttu-id="5d2b5-575">將 VM 加入內部部署網域的詳細步驟，以及成為內部部署網域成員所需的其他軟體，因客戶而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-575">The detailed steps you take to join a VM to an on-premises domain, and the additional software required to be a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="5d2b5-576">通常要將 VM 加入內部部署網域，您必須安裝其他軟體 (例如反惡意程式碼軟體以及備份或監視軟體)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-576">Usually, to join a VM to an on-premises domain, you need to install additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="5d2b5-577">在此案例中，您需要確定如果在 VM 加入您環境中的網域時強制使用網際網路 Proxy 設定，則客體 VM 中的 Windows 本機系統帳戶 (S-1-5-18) 會有相同的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-577">In this scenario, you also need to make sure that if Internet proxy settings are forced when a VM joins a domain in your environment, the Windows Local System Account (S-1-5-18) in the Guest VM has the same proxy settings.</span></span> <span data-ttu-id="5d2b5-578">最簡單的選項是使用適用於網域內系統的網域群組原則來強制使用 Proxy。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-578">The easiest option is to force the proxy by using a domain Group Policy, which applies to systems in the domain.</span></span>

### <span data-ttu-id="5d2b5-579"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>下載、安裝和啟用 Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="5d2b5-579"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Download, install, and enable the Azure VM Agent</span></span>
<span data-ttu-id="5d2b5-580">對於從未一般化的 OS 映像 (例如不是源自於 Windows 系統準備 (或 sysprep) 工具的映像) 部署的虛擬機器，您必須手動下載、安裝和啟用 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-580">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in the Windows System Preparation, or sysprep, tool), you need to manually download, install, and enable the Azure VM Agent.</span></span>

<span data-ttu-id="5d2b5-581">如果您從 Azure Marketplace 部署 VM，就不需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-581">If you deploy a VM from the Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="5d2b5-582">Azure Marketplace 中的映像已經有 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-582">Images from the Azure Marketplace already have the Azure VM Agent.</span></span>

#### <span data-ttu-id="5d2b5-583"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span><span class="sxs-lookup"><span data-stu-id="5d2b5-583"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span></span>
1.  <span data-ttu-id="5d2b5-584">下載 Azure VM 代理程式︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-584">Download the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="5d2b5-585">下載 [Azure VM 代理程式安裝程式套件](https://go.microsoft.com/fwlink/?LinkId=394789)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-585">Download the [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  2.  <span data-ttu-id="5d2b5-586">在個人電腦或伺服器本機上儲存 VM 代理程式 MSI 套件。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-586">Store the VM Agent MSI package locally on a personal computer or server.</span></span>
2.  <span data-ttu-id="5d2b5-587">安裝 Azure VM 代理程式︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-587">Install the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="5d2b5-588">使用遠端桌面通訊協定 (RDP) 連線到已部署的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-588">Connect to the deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  2.  <span data-ttu-id="5d2b5-589">在 VM 上開啟「Windows 檔案總管」視窗，然後選取 VM 代理程式之 MSI 檔案的目標目錄。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-589">Open a Windows Explorer window on the VM and select the target directory for the MSI file of the VM Agent.</span></span>
  3.  <span data-ttu-id="5d2b5-590">將 Azure VM 代理程式安裝程式 MSI 檔案從本機電腦/伺服器拖放到 VM 上 VM 代理程式的目標目錄。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-590">Drag the Azure VM Agent Installer MSI file from your local computer/server to the target directory of the VM Agent on the VM.</span></span>
  4.  <span data-ttu-id="5d2b5-591">按兩下 VM 上的 MSI 檔案。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-591">Double-click the MSI file on the VM.</span></span>
3.  <span data-ttu-id="5d2b5-592">對於加入內部部署網域的 VM，請確定最終網際網路 Proxy 設定也適用於 VM 中的 Windows 本機系統帳戶 (S-1-5-18)，如[設定 Proxy][deployment-guide-configure-proxy] 所述。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-592">For VMs that are joined to on-premises domains, make sure that eventual Internet proxy settings also apply to the Windows Local System account (S-1-5-18) in the VM, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="5d2b5-593">VM 代理程式會在此內容中執行，而且必須可以連線到 Azure。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-593">The VM Agent runs in this context and needs to be able to connect to Azure.</span></span>

<span data-ttu-id="5d2b5-594">更新 Azure VM 代理程式時，並不需要使用者介入。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-594">No user interaction is required to update the Azure VM Agent.</span></span> <span data-ttu-id="5d2b5-595">VM 代理程式會自動更新，不需要重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-595">The VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <span data-ttu-id="5d2b5-596"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span><span class="sxs-lookup"><span data-stu-id="5d2b5-596"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span></span>
<span data-ttu-id="5d2b5-597">使用下列命令來安裝適用於 Linux 的 VM 代理程式：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-597">Use the following commands to install the VM Agent for Linux:</span></span>

* <span data-ttu-id="5d2b5-598">**SUSE Linux Enterprise Server (SLES)**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-598">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="5d2b5-599">**Red Hat Enterprise Linux (RHEL) 或 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-599">**Red Hat Enterprise Linux (RHEL) or Oracle Linux**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="5d2b5-600">如果已安裝代理程式，若要更新 Azure Linux 代理程式，請執行[將 VM 上的 Azure Linux 代理程式更新為 GitHub 中的最新版本][virtual-machines-linux-update-agent]所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-600">If the agent is already installed, to update the Azure Linux Agent, do the steps described in [Update the Azure Linux Agent on a VM to the latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <span data-ttu-id="5d2b5-601"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>設定 Proxy</span><span class="sxs-lookup"><span data-stu-id="5d2b5-601"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configure the proxy</span></span>
<span data-ttu-id="5d2b5-602">在 Windows 中設定 Proxy 所採取的步驟，不同於您在 Linux 中設定 Proxy 的方式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-602">The steps you take to configure the proxy in Windows are different from the way you configure the proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="5d2b5-603">Windows</span><span class="sxs-lookup"><span data-stu-id="5d2b5-603">Windows</span></span>
<span data-ttu-id="5d2b5-604">您也必須針對本機系統帳戶進行正確的 Proxy 設定，才能存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-604">Proxy settings must be set up correctly for the Local System account to access the Internet.</span></span> <span data-ttu-id="5d2b5-605">如果您的 Proxy 設定不是透過群組原則設定，您可以為本機系統帳戶進行這些設定。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-605">If your proxy settings are not set by Group Policy, you can configure the settings for the Local System account.</span></span>

1. <span data-ttu-id="5d2b5-606">移至 [開始]，輸入 **gpedit.msc**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-606">Go to **Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
2. <span data-ttu-id="5d2b5-607">選取 [電腦設定] > [系統管理範本] > [Windows 元件] > [Internet Explorer]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-607">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="5d2b5-608">請確定 [為每台電腦建立 Proxy 設定 - 而不是每個使用者] 設定已停用或未設定。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-608">Make sure that the setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
3. <span data-ttu-id="5d2b5-609">在 [控制台] 中，移至 [網路和共用中心] > [網際網路選項]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-609">In **Control Panel**, go to **Network and Sharing Center** > **Internet Options**.</span></span>
4. <span data-ttu-id="5d2b5-610">在 [連線] 索引標籤上，選取 [區域網路設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-610">On the **Connections** tab, select the **LAN settings** button.</span></span>
5. <span data-ttu-id="5d2b5-611">清除 [自動偵測設定] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-611">Clear the **Automatically detect settings** check box.</span></span>
6. <span data-ttu-id="5d2b5-612">選取 [為您的 LAN 使用 Proxy 伺服器] 核取方塊，然後輸入 Proxy 位址和連接埠</span><span class="sxs-lookup"><span data-stu-id="5d2b5-612">Select the **Use a proxy server for your LAN** check box, and then enter the proxy address and port.</span></span>
7. <span data-ttu-id="5d2b5-613">選取 [進階] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-613">Select the **Advanced** button.</span></span>
8. <span data-ttu-id="5d2b5-614">在 [例外狀況] 方塊中，輸入 IP 位址 **168.63.129.16**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-614">In the **Exceptions** box, enter the IP address **168.63.129.16**.</span></span> <span data-ttu-id="5d2b5-615">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-615">Select **OK**.</span></span>

#### <a name="linux"></a><span data-ttu-id="5d2b5-616">Linux</span><span class="sxs-lookup"><span data-stu-id="5d2b5-616">Linux</span></span>
<span data-ttu-id="5d2b5-617">在 Microsoft Azure 客體代理程式的組態檔 (位於 \\etc\\waagent.conf) 中設定正確的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-617">Configure the correct proxy in the configuration file of the Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="5d2b5-618">設定下列參數︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-618">Set the following parameters:</span></span>

1.  <span data-ttu-id="5d2b5-619">**HTTP Proxy 主機**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-619">**HTTP proxy host**.</span></span> <span data-ttu-id="5d2b5-620">例如，將它設為 **proxy.corp.local**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-620">For example, set it to **proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  <span data-ttu-id="5d2b5-621">**HTTP Proxy 連接埠**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-621">**HTTP proxy port**.</span></span> <span data-ttu-id="5d2b5-622">例如，將它設定為 **80**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-622">For example, set it to **80**.</span></span>
  ```
  HttpProxy.Port=<port of the proxy host>

  ```
3.  <span data-ttu-id="5d2b5-623">重新啟動代理程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-623">Restart the agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="5d2b5-624">\\etc\\waagent.conf 中的 Proxy 設定也適用於所需的 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-624">The proxy settings in \\etc\\waagent.conf also apply to the required VM extensions.</span></span> <span data-ttu-id="5d2b5-625">如果您想要使用 Azure 儲存機制，請確定這些儲存機制的流量不會經過內部部署內部網路。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-625">If you want to use the Azure repositories, make sure that the traffic to these repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="5d2b5-626">如果您已建立使用者定義的路由來啟用強制通道，請務必新增路由，以將傳送給儲存機制的流量直接遞送到網際網路，而不透過站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-626">If you created user-defined routes to enable forced tunneling, make sure that you add a route that routes traffic to the repositories directly to the Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="5d2b5-627">**SLES**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-627">**SLES**</span></span>

  <span data-ttu-id="5d2b5-628">您也需要新增 \\etc\\regionserverclnt.cfg 中所列 IP 位址的路由。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-628">You also need to add routes for the IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="5d2b5-629">下圖顯示一個範例：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-629">The following figure shows an example:</span></span>

  ![強制通道][deployment-guide-figure-50]


* <span data-ttu-id="5d2b5-631">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-631">**RHEL**</span></span>

  <span data-ttu-id="5d2b5-632">您還需要一併為 \\etc\\yum.repos.d\\rhui-load-balancers 中所列的主機 IP 位址新增路由。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-632">You also need to add routes for the IP addresses of the hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="5d2b5-633">如需範例，請參閱上圖。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-633">For an example, see the preceding figure.</span></span>

* <span data-ttu-id="5d2b5-634">**Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-634">**Oracle Linux**</span></span>

  <span data-ttu-id="5d2b5-635">Azure 上沒有任何 Oracle Linux 的存放庫。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-635">There are no repositories for Oracle Linux on Azure.</span></span> <span data-ttu-id="5d2b5-636">您要為 Oracle Linux 設定您自己的存放庫，或使用公用存放庫。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-636">You need to configure your own repositories for Oracle Linux or use the public repositories.</span></span>

<span data-ttu-id="5d2b5-637">如需有關使用者定義的路由詳細資訊，請參閱[使用者定義的路由和 IP 轉送][virtual-networks-udr-overview]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-637">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <span data-ttu-id="5d2b5-638"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>設定 Azure Enhanced Monitoring Extension for SAP</span><span class="sxs-lookup"><span data-stu-id="5d2b5-638"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configure the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="5d2b5-639">在您如 [SAP on Azure 的 VM 部署案例][deployment-guide-3]所述準備好 VM 之後，Azure VM 代理程式就會安裝於虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-639">When you've prepared the VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], the Azure VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="5d2b5-640">下一個步驟是部署 Azure Enhanced Monitoring Extension for SAP (位於全球 Azure 資料中心的 Azure 擴充功能儲存機制)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-640">The next step is to deploy the Azure Enhanced Monitoring Extension for SAP, which is available in the Azure Extension Repository in the global Azure datacenters.</span></span> <span data-ttu-id="5d2b5-641">如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide-9.1]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-641">For more information, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-9.1].</span></span>

<span data-ttu-id="5d2b5-642">您可以使用 PowerShell 或 Azure CLI 安裝和設定 Azure Enhanced Monitoring Extension for SAP。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-642">You can use PowerShell or Azure CLI to install and configure the Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="5d2b5-643">若要使用 Windows 電腦在 Windows 或 Linux VM 上安裝該擴充功能，請參閱 [Azure PowerShell][deployment-guide-4.5.1]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-643">To install the extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="5d2b5-644">若要使用 Linux 桌上型電腦在 Linux VM 上安裝該擴充功能，請參閱 [Azure CLI][deployment-guide-4.5.2]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-644">To install the extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <span data-ttu-id="5d2b5-645"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>適用於 Linux 和 Windows VM 的 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d2b5-645"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="5d2b5-646">若要使用 PowerShell 安裝 Azure Enhanced Monitoring Extension for SAP：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-646">To install the Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="5d2b5-647">確定您已安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-647">Make sure that you have installed the latest version of the Azure PowerShell cmdlet.</span></span> <span data-ttu-id="5d2b5-648">如需詳細資訊，請參閱[部署 Azure PowerShell Cmdlet][deployment-guide-4.1]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-648">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
2. <span data-ttu-id="5d2b5-649">執行下列 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-649">Run the following PowerShell cmdlet.</span></span>
    <span data-ttu-id="5d2b5-650">如需可用環境的清單，請執行 `commandlet Get-AzureRmEnvironment`。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-650">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="5d2b5-651">如果您想要使用全域 Azure，則您的環境是 **AzureCloud**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-651">If you want to use global Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="5d2b5-652">若為中國的 Azure，請選取 **AzureChinaCloud**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-652">For Azure in China, select **AzureChinaCloud**.</span></span>

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of the environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

<span data-ttu-id="5d2b5-653">輸入您的帳戶資料並識別 Azure 虛擬機器之後，指令碼會部署所需的擴充功能，並啟用所需的功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-653">After you enter your account data and identify the Azure virtual machine, the script deploys the required extensions and enables the required features.</span></span> <span data-ttu-id="5d2b5-654">這可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-654">This can take several minutes.</span></span>
<span data-ttu-id="5d2b5-655">如需有關 `Set-AzureRmVMAEMExtension` 的詳細資訊，請參閱 [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-655">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![成功執行 SAP 特定 Azure Cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

<span data-ttu-id="5d2b5-657">`Set-AzureRmVMAEMExtension` 設定可以進行設定 SAP 主機監視的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-657">The `Set-AzureRmVMAEMExtension` configuration does all the steps to configure host monitoring for SAP.</span></span>

<span data-ttu-id="5d2b5-658">指令碼輸出包含下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-658">The script output includes the following information:</span></span>

* <span data-ttu-id="5d2b5-659">確認已設定 OS 磁碟和所有額外資料磁碟的監視。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-659">Confirmation that monitoring for the OS disk and all additional data disks has been configured.</span></span>
* <span data-ttu-id="5d2b5-660">接下來的兩則訊息會確認特定儲存體帳戶的儲存體計量組態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-660">The next two messages confirm the configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="5d2b5-661">其中一行輸出會提供監視組態的實際更新狀態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-661">One line of output gives the status of the actual update of the monitoring configuration.</span></span>
* <span data-ttu-id="5d2b5-662">另一行輸出會確認已部署或已更新組態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-662">Another line of output confirms that the configuration has been deployed or updated.</span></span>
* <span data-ttu-id="5d2b5-663">輸出的最後一行是參考資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-663">The last line of output is informational.</span></span> <span data-ttu-id="5d2b5-664">其顯示測試監視組態的選項。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-664">It shows your options for testing the monitoring configuration.</span></span>
* <span data-ttu-id="5d2b5-665">若要確認 Azure Enhanced Monitoring 的所有步驟是否已成功執行，以及「Azure 基礎結構」是否提供必要的資料，請繼續進行 Azure Enhanced Monitoring Extension for SAP 的整備檢查 (如 [Azure Enhanced Monitoring for SAP 整備檢查][deployment-guide-5.1]所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-665">To check that all steps of Azure Enhanced Monitoring have been executed successfully, and that the Azure Infrastructure provides the necessary data, proceed with the readiness check for the Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span>
* <span data-ttu-id="5d2b5-666">等候 15-30 分鐘的時間，讓 Azure 診斷收集相關的資料。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-666">Wait 15-30 minutes for Azure Diagnostics to collect the relevant data.</span></span>

#### <span data-ttu-id="5d2b5-667"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>適用於 Linux VM 的 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5d2b5-667"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI for Linux VMs</span></span>
<span data-ttu-id="5d2b5-668">若要使用 Azure CLI 安裝 Azure Enhanced Monitoring Extension for SAP：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-668">To install the Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="5d2b5-669">如[安裝 Azure CLI 1.0][azure-cli] 所述，安裝 Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-669">Install Azure CLI 1.0, as described in [Install the Azure CLI 1.0][azure-cli].</span></span>
2. <span data-ttu-id="5d2b5-670">使用您的 Azure 帳戶進行登入：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-670">Sign in with your Azure account:</span></span>

  ```
  azure login
  ```

3. <span data-ttu-id="5d2b5-671">切換到 Azure Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-671">Switch to Azure Resource Manager mode:</span></span>

  ```
  azure config mode arm
  ```

4. <span data-ttu-id="5d2b5-672">啟用 Azure Enhanced Monitoring：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-672">Enable Azure Enhanced Monitoring:</span></span>

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. <span data-ttu-id="5d2b5-673">確認 Azure Enhanced Monitoring Extension 在 Azure Linux VM 上為作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-673">Verify that the Azure Enhanced Monitoring Extension is active on the Azure Linux VM.</span></span> <span data-ttu-id="5d2b5-674">檢查 \\var\\lib\\AzureEnhancedMonitor\\PerfCounters 檔案是否存在。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-674">Check whether the file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="5d2b5-675">如果存在，在命令提示字元中執行此命令，以顯示 Azure Enhanced Monitor 所收集的資訊︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-675">If it exists, at a command prompt, run this command to display information collected by the Azure Enhanced Monitor:</span></span>
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

<span data-ttu-id="5d2b5-676">輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-676">The output looks like this:</span></span>
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <span data-ttu-id="5d2b5-677"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>針對端對端監視進行檢查及疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d2b5-677"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="5d2b5-678">部署 Azure VM 並設定相關 Azure 監視基礎結構之後，請檢查 Azure Enhanced Monitoring Extension 的所有元件是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-678">After you have deployed your Azure VM and set up the relevant Azure monitoring infrastructure, check whether all the components of the Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="5d2b5-679">如 [Azure Enhanced Monitoring Extension for SAP 整備檢查][deployment-guide-5.1]所述，執行 Azure Enhanced Monitoring Extension for SAP 整備檢查。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-679">Run the readiness check for the Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for the Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="5d2b5-680">如果所有整備檢查結果均為正向，而且所有相關效能計數器都呈現 OK 狀態，表示已成功設定 Azure 監視。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-680">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring has been set up successfully.</span></span> <span data-ttu-id="5d2b5-681">您可以繼續安裝 SAP Host Agent (如 [SAP 資源][deployment-guide-2.2]中的 SAP Note 所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-681">You can proceed with the installation of SAP Host Agent as described in the SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="5d2b5-682">如果整備檢查指出遺失計數器，請執行 Azure 監視基礎結構的健康狀態檢查 (如 [Azure 監視基礎結構組態的健康狀態檢查][deployment-guide-5.2]所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-682">If the readiness check indicates that counters are missing, run the health check for the Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="5d2b5-683">如需其他疑難排解選項，請參閱[針對適用於 SAP 的 Azure 監視進行疑難排解][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-683">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="5d2b5-684"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Azure Enhanced Monitoring Extension for SAP 整備檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-684"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Readiness check for the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="5d2b5-685">這項檢查可確保基礎 Azure 監視基礎結構提供 SAP 應用程式內所顯示的所有效能計量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-685">This check makes sure that all performance metrics that appear inside your SAP application are provided by the underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-the-readiness-check-on-a-windows-vm"></a><span data-ttu-id="5d2b5-686">在 Windows VM 上執行整備檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-686">Run the readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="5d2b5-687">登入 Azure 虛擬機器 (不一定要使用管理帳戶)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-687">Sign in to the Azure virtual machine (using an admin account is not necessary).</span></span>
2.  <span data-ttu-id="5d2b5-688">開啟命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-688">Open a Command Prompt window.</span></span>
3.  <span data-ttu-id="5d2b5-689">在命令提示字元，將目錄切換到 Azure Enhanced Monitoring Extension for SAP 的安裝資料夾：C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;版本>\\drop</span><span class="sxs-lookup"><span data-stu-id="5d2b5-689">At the command prompt, change the directory to the installation folder of the Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="5d2b5-690">監視擴充功能路徑中的「版本」可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-690">The *version* in the path to the monitoring extension might vary.</span></span> <span data-ttu-id="5d2b5-691">如果您在安裝資料夾中看到多個監視擴充功能版本的資料夾，請檢查 AzureEnhancedMonitoring Windows 服務的組態，然後切換至「可執行檔的路徑」所表示的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-691">If you see folders for multiple versions of the monitoring extension in the installation folder, check the configuration of the AzureEnhancedMonitoring Windows service, and then switch to the folder indicated as *Path to executable*.</span></span>

  ![執行 Azure Enhanced Monitoring Extension for SAP 之服務的屬性][deployment-guide-figure-1000]

4.  <span data-ttu-id="5d2b5-693">在命令視窗中，執行不含任何參數的 **azperflib.exe**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-693">At the command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5d2b5-694">Azperflib.exe 會以迴圈形式執行，並每隔 60 秒更新收集到的計數器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-694">Azperflib.exe runs in a loop and updates the collected counters every 60 seconds.</span></span> <span data-ttu-id="5d2b5-695">若要完成迴圈，請關閉命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-695">To end the loop, close the Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="5d2b5-696">如果未安裝 Azure Enhanced Monitoring Extension 或 AzureEnhancedMonitoring 服務未執行，即表示尚未正確設定擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-696">If the Azure Enhanced Monitoring Extension is not installed, or the AzureEnhancedMonitoring service is not running, the extension has not been configured correctly.</span></span> <span data-ttu-id="5d2b5-697">如需如何部署擴充功能的詳細資訊，請參閱[針對適用於 SAP 的 Azure 監視基礎結構進行疑難排解][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-697">For detailed information about how to deploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-the-output-of-azperflibexe"></a><span data-ttu-id="5d2b5-698">檢查 azperflib.exe 的輸出</span><span class="sxs-lookup"><span data-stu-id="5d2b5-698">Check the output of azperflib.exe</span></span>
<span data-ttu-id="5d2b5-699">Azperflib.exe 輸出會顯示適用於 SAP 的所有已填入 Azure 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-699">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="5d2b5-700">在所收集計數器的清單底部，摘要和健康狀態指標會顯示 Azure 監視的狀態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-700">At the bottom of the list of collected counters, a summary and health indicator show the status of Azure monitoring.</span></span>

<span data-ttu-id="5d2b5-701">![執行 azperflib.exe 的健康狀態檢查輸出，其表示沒有任何問題][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-701">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="5d2b5-702">請檢查針對 **Counters total** 傳回的結果 (其回報是空的)，以及針對 **Health status** 傳回的結果 (如上圖所示)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-702">Check the result returned for the **Counters total** output, which is reported as empty, and for **Health status**, shown in the preceding figure.</span></span>

<span data-ttu-id="5d2b5-703">解譯結果值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-703">Interpret the resulting values as follows:</span></span>

| <span data-ttu-id="5d2b5-704">Azperflib.exe 結果值</span><span class="sxs-lookup"><span data-stu-id="5d2b5-704">Azperflib.exe result values</span></span> | <span data-ttu-id="5d2b5-705">Azure 監視健康狀態</span><span class="sxs-lookup"><span data-stu-id="5d2b5-705">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="5d2b5-706">**API 呼叫 - 無法使用**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-706">**API Calls - not available**</span></span> | <span data-ttu-id="5d2b5-707">無法使用的計數器有可能不適用於虛擬機器組態，或發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-707">Counters that are not available might be either not applicable to the virtual machine configuration, or are errors.</span></span> <span data-ttu-id="5d2b5-708">請參閱 **Health status**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-708">See **Health status**.</span></span> |
| <span data-ttu-id="5d2b5-709">**Counters total - empty**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-709">**Counters total - empty**</span></span> |<span data-ttu-id="5d2b5-710">下列兩個 Azure 儲存體計數器可以空白：</span><span class="sxs-lookup"><span data-stu-id="5d2b5-710">The following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="5d2b5-711">儲存體讀取 Op 延遲伺服器毫秒</span><span class="sxs-lookup"><span data-stu-id="5d2b5-711">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="5d2b5-712">儲存體讀取 Op 延遲 E2E 毫秒</span><span class="sxs-lookup"><span data-stu-id="5d2b5-712">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="5d2b5-713">所有其他計數器都必須具有值。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-713">All other counters must have values.</span></span> |
| <span data-ttu-id="5d2b5-714">**Health status**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-714">**Health status**</span></span> |<span data-ttu-id="5d2b5-715">只有在傳回狀態顯示 [OK] 時，才算正常。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-715">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="5d2b5-716">**診斷**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-716">**Diagnostics**</span></span> |<span data-ttu-id="5d2b5-717">健康狀態的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-717">Detailed information about health status.</span></span> |

<span data-ttu-id="5d2b5-718">如果 [Health status] 值不是 [OK]，請依照 [Azure 監視基礎結構組態的健康狀態檢查][deployment-guide-5.2]中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-718">If the **Health status** value is not **OK**, follow the instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-the-readiness-check-on-a-linux-vm"></a><span data-ttu-id="5d2b5-719">在 Linux VM 上執行整備檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-719">Run the readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="5d2b5-720">使用 SSH 來連線到 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-720">Connect to the Azure Virtual Machine by using SSH.</span></span>

2.  <span data-ttu-id="5d2b5-721">檢查 Azure Enhanced Monitoring Extension 的輸出。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-721">Check the output of the Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="5d2b5-722">a.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-722">a.</span></span>  <span data-ttu-id="5d2b5-723">執行 `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-723">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="5d2b5-724">**預期的結果**：傳回效能計數器的清單。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-724">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="5d2b5-725">此檔案不得是空的。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-725">The file should not be empty.</span></span>

 <span data-ttu-id="5d2b5-726">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-726">b.</span></span> <span data-ttu-id="5d2b5-727">執行 `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-727">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="5d2b5-728">**預期的結果**：傳回**無**錯誤的一行，例如 **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span><span class="sxs-lookup"><span data-stu-id="5d2b5-728">**Expected result**: Returns one line where the error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="5d2b5-729">c.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-729">c.</span></span> <span data-ttu-id="5d2b5-730">執行 `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-730">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="5d2b5-731">**預期的結果**：傳回為空白或不存在。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-731">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="5d2b5-732">如果上述檢查不成功，請執行下列額外的檢查︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-732">If the preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="5d2b5-733">確定已安裝並啟用 waagent。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-733">Make sure that the waagent is installed and enabled.</span></span>

  <span data-ttu-id="5d2b5-734">a.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-734">a.</span></span>  <span data-ttu-id="5d2b5-735">執行 `sudo ls -al /var/lib/waagent/`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-735">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="5d2b5-736">**預期的結果**：列出 waagent 目錄的內容。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-736">**Expected result**: Lists the content of the waagent directory.</span></span>

  <span data-ttu-id="5d2b5-737">b.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-737">b.</span></span>  <span data-ttu-id="5d2b5-738">執行 `ps -ax | grep waagent`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-738">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="5d2b5-739">**預期的結果**：顯示類似下列一個項目：`python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-739">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

3.   <span data-ttu-id="5d2b5-740">確定已安裝並啟用 Azure Enhanced Monitoring Extension。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-740">Make sure that the Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="5d2b5-741">a.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-741">a.</span></span>  <span data-ttu-id="5d2b5-742">執行 `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-742">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`</span></span>

    <span data-ttu-id="5d2b5-743">**預期的結果**：列出 Azure Enhanced Monitoring Extension 目錄的內容。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-743">**Expected result**: Lists the content of the Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="5d2b5-744">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-744">b.</span></span> <span data-ttu-id="5d2b5-745">執行 `ps -ax | grep AzureEnhanced`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-745">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="5d2b5-746">**預期的結果**：顯示類似下列一個項目：`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-746">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

3. <span data-ttu-id="5d2b5-747">安裝 SAP Host Agent (如 SAP Note [1031096] 所述) 並檢查 `saposcol` 的輸出。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-747">Install SAP Host Agent as described in SAP Note [1031096], and check the output of `saposcol`.</span></span>

  <span data-ttu-id="5d2b5-748">a.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-748">a.</span></span>  <span data-ttu-id="5d2b5-749">執行 `/usr/sap/hostctrl/exe/saposcol -d`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-749">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="5d2b5-750">b.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-750">b.</span></span>  <span data-ttu-id="5d2b5-751">執行 `dump ccm`</span><span class="sxs-lookup"><span data-stu-id="5d2b5-751">Run `dump ccm`</span></span>

  <span data-ttu-id="5d2b5-752">c.</span><span class="sxs-lookup"><span data-stu-id="5d2b5-752">c.</span></span>  <span data-ttu-id="5d2b5-753">檢查 **Virtualization_Configuration\Enhanced Monitoring Access** 計量是否為 **true**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-753">Check whether the **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="5d2b5-754">如果您已安裝 SAP NetWeaver ABAP 應用程式伺服器，請開啟交易 ST06，並檢查是否已啟用增強監視。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-754">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="5d2b5-755">如果上述任何檢查失敗，而且如需如何重新部署擴充功能的詳細資訊，請參閱[針對適用於 SAP 的 Azure 監視基礎結構進行疑難排解][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-755">If any of these checks fail, and for detailed information about how to redeploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="5d2b5-756"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Azure 監視基礎結構組態的健康狀態檢查</span><span class="sxs-lookup"><span data-stu-id="5d2b5-756"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Health check for the Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="5d2b5-757">如果未正確提供部分監視資料 (如上面 [Azure Enhanced Monitoring for SAP 整備檢查][deployment-guide-5.1]所述測試所指出)，請執行`Test-AzureRmVMAEMExtension` Cmdlet，以檢查適用於 SAP 的 Azure 監視基礎結構和監視」擴充功能是否設定正確。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-757">If some of the monitoring data is not delivered correctly as indicated by the test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run the `Test-AzureRmVMAEMExtension` cmdlet to check whether the Azure monitoring infrastructure and the monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="5d2b5-758">確定您已安裝最新版的 Azure PowerShell Cmdlet (如[部署 Azure PowerShell Cmdlet][deployment-guide-4.1]所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-758">Make sure that you have installed the latest version of the Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
2.  <span data-ttu-id="5d2b5-759">執行下列 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-759">Run the following PowerShell cmdlet.</span></span> <span data-ttu-id="5d2b5-760">如需可用環境的清單，請執行 `Get-AzureRmEnvironment` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-760">For a list of available environments, run the cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="5d2b5-761">若要使用公用 Azure，請選取 **AzureCloud** 環境。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-761">To use global Azure, select the **AzureCloud** environment.</span></span> <span data-ttu-id="5d2b5-762">若為中國的 Azure，請選取 **AzureChinaCloud**。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-762">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of the environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  <span data-ttu-id="5d2b5-763">輸入您的帳戶資料並識別 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-763">Enter your account data and identify the Azure virtual machine.</span></span>

  ![SAP 特定 Azure Cmdlet Test-VMConfigForSAP_GUI 的輸入頁面][deployment-guide-figure-1200]

4. <span data-ttu-id="5d2b5-765">指令碼會測試您所選虛擬機器的組態。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-765">The script tests the configuration of the virtual machine you select.</span></span>

  ![適用於 SAP 之 Azure 監視基礎結構的成功測試輸出][deployment-guide-figure-1300]

<span data-ttu-id="5d2b5-767">確定每個健康狀態檢查的結果都 [OK]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-767">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="5d2b5-768">如果部分檢查未顯示 [OK]，請執行更新 Cmdlet (如[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-768">If some checks do not display **OK**, run the update cmdlet as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="5d2b5-769">請等待 15 分鐘，然後重複 [Azure Enhanced Monitoring for SAP 整備檢查][deployment-guide-5.1]和 [Azure 監視基礎結構組態的健康狀態檢查][deployment-guide-5.2]所述的檢查。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-769">Wait 15 minutes, and repeat the checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="5d2b5-770">如果檢查仍然指出部分或所有計數器有問題，請參閱[針對適用於 SAP 的 Azure 監視基礎結構進行疑難排解][deployment-guide-5.3]。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-770">If the checks still indicate a problem with some or all counters, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="5d2b5-771"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>針對適用於 SAP 的 Azure 監視基礎結構進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="5d2b5-771"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Troubleshooting the Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="5d2b5-773">完全未顯示 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-773">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="5d2b5-774">AzureEnhancedMonitoring Windows 服務會收集 Azure 中的效能計量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-774">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="5d2b5-775">如果尚未正確安裝服務，或未在 VM 中執行服務，則不會收集任何效能計量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-775">If the service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="5d2b5-776">Azure Enhanced Monitoring Extension 的安裝目錄是空的</span><span class="sxs-lookup"><span data-stu-id="5d2b5-776">The installation directory of the Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="5d2b5-777">問題</span><span class="sxs-lookup"><span data-stu-id="5d2b5-777">Issue</span></span>
<span data-ttu-id="5d2b5-778">安裝目錄 \\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;版本>\\drop 是空的。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-778">The installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="5d2b5-779">方案</span><span class="sxs-lookup"><span data-stu-id="5d2b5-779">Solution</span></span>
<span data-ttu-id="5d2b5-780">未安裝此擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-780">The extension is not installed.</span></span> <span data-ttu-id="5d2b5-781">判斷這是否為 Proxy 問題 (如先前所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-781">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="5d2b5-782">您可能需要重新啟動電腦，或重新執行 `Set-AzureRmVMAEMExtension` 組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-782">You might need to restart the machine or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="5d2b5-783">Azure Enhanced Monitoring 的服務不存在</span><span class="sxs-lookup"><span data-stu-id="5d2b5-783">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="5d2b5-784">問題</span><span class="sxs-lookup"><span data-stu-id="5d2b5-784">Issue</span></span>
<span data-ttu-id="5d2b5-785">AzureEnhancedMonitoring Windows 服務不存在。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-785">The AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="5d2b5-786">Azperflib.exe 輸出會擲回錯誤︰</span><span class="sxs-lookup"><span data-stu-id="5d2b5-786">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="5d2b5-787">![執行 azperflib.exe 即表示 Azure Enhanced Monitoring Extension for SAP 的服務未執行][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="5d2b5-787">![Execution of azperflib.exe indicates that the service of the Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="5d2b5-788">方案</span><span class="sxs-lookup"><span data-stu-id="5d2b5-788">Solution</span></span>
<span data-ttu-id="5d2b5-789">如果服務不存在，即表示尚未正確安裝 Azure Enhanced Monitoring Extension for SAP。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-789">If the service does not exist, the Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="5d2b5-790">請使用 [Azure 中適用於 SAP 的 VM 部署案例][deployment-guide-3]中針對您的部署案例所述的步驟，重新部署此擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-790">Redeploy the extension by using the steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="5d2b5-791">部署此擴充功能之後，請在一小時後再度檢查 Azure VM 中是否提供 Azure 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-791">After you deploy the extension, after one hour, check again whether the Azure performance counters are provided in the Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-to-start"></a><span data-ttu-id="5d2b5-792">Azure Enhanced Monitoring 的服務存在，但無法啟動</span><span class="sxs-lookup"><span data-stu-id="5d2b5-792">Service for Azure Enhanced Monitoring exists, but fails to start</span></span>

###### <a name="issue"></a><span data-ttu-id="5d2b5-793">問題</span><span class="sxs-lookup"><span data-stu-id="5d2b5-793">Issue</span></span>
<span data-ttu-id="5d2b5-794">AzureEnhancedMonitoring Windows 服務存在並已啟用，但無法啟動。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-794">The AzureEnhancedMonitoring Windows service exists and is enabled, but fails to start.</span></span> <span data-ttu-id="5d2b5-795">如需詳細資訊，請檢查應用程式事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-795">For more information, check the application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="5d2b5-796">方案</span><span class="sxs-lookup"><span data-stu-id="5d2b5-796">Solution</span></span>
<span data-ttu-id="5d2b5-797">組態不正確。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-797">The configuration is incorrect.</span></span> <span data-ttu-id="5d2b5-798">如[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 所述，重新啟動 VM 的監視擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-798">Restart the monitoring extension for the VM, as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="5d2b5-800">遺失部分 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-800">Some Azure performance counters are missing</span></span>
<span data-ttu-id="5d2b5-801">AzureEnhancedMonitoring Windows 服務會收集 Azure 中的效能計量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-801">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="5d2b5-802">此服務會從數個來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-802">The service gets data from several sources.</span></span> <span data-ttu-id="5d2b5-803">有些組態資料是在本機收集，而有些效能計量是從 Azure 診斷讀取而來。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-803">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="5d2b5-804">您會從登入儲存體訂用帳戶的層級使用儲存體計數器。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-804">Storage counters are used from your logging on the storage subscription level.</span></span>

<span data-ttu-id="5d2b5-805">如果使用 SAP Note [1999351] 進行疑難排解並未解決問題，請重新執行 `Set-AzureRmVMAEMExtension` 組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-805">If troubleshooting by using SAP Note [1999351] doesn't resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="5d2b5-806">因為儲存體分析或診斷計數器在啟用後可能未立即建立，所以您可能必須等待一個小時的時間。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-806">You might have to wait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="5d2b5-807">如果問題仍然存在，請在元件 BC-OP-NT-AZR (適用於 Windows) 或 BC-OP-LNX-AZR (適用於 Linux 虛擬機器) 上開啟 SAP 客戶支援訊息。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-807">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="5d2b5-809">完全未顯示 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-809">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="5d2b5-810">Daemon 會收集在 Azure 中的效能計量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-810">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="5d2b5-811">如果未執行 Daemon，則不會收集任何效能計量。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-811">If the daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="5d2b5-812">Azure Enhanced Monitoring Extension 的安裝目錄是空白</span><span class="sxs-lookup"><span data-stu-id="5d2b5-812">The installation directory of the Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="5d2b5-813">問題</span><span class="sxs-lookup"><span data-stu-id="5d2b5-813">Issue</span></span>
<span data-ttu-id="5d2b5-814">\\var\\lib\\waagent\\ 目錄未包含 Azure Enhanced Monitoring Extension 的子目錄。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-814">The directory \\var\\lib\\waagent\\ does not have a subdirectory for the Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="5d2b5-815">方案</span><span class="sxs-lookup"><span data-stu-id="5d2b5-815">Solution</span></span>
<span data-ttu-id="5d2b5-816">未安裝此擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-816">The extension is not installed.</span></span> <span data-ttu-id="5d2b5-817">判斷這是否為 Proxy 問題 (如先前所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-817">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="5d2b5-818">您可能需要重新啟動電腦及/或重新執行 `Set-AzureRmVMAEMExtension` 組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-818">You might need to restart the machine and/or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="5d2b5-820">遺失部分 Azure 效能計數器</span><span class="sxs-lookup"><span data-stu-id="5d2b5-820">Some Azure performance counters are missing</span></span>
<span data-ttu-id="5d2b5-821">Azure 中的效能計量是由 Daemon 收集，而 Daemon 會從數個來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-821">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="5d2b5-822">有些組態資料是在本機收集，而有些效能計量是從 Azure 診斷讀取而來。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-822">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="5d2b5-823">儲存體計數器來自您儲存體訂用帳戶中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-823">Storage counters come from the logs in your storage subscription.</span></span>

<span data-ttu-id="5d2b5-824">如需完整且最新的已知問題清單，請參閱 SAP Note [1999351]，其中包含適用於 Enhanced Azure Monitoring for SAP 的其他疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-824">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="5d2b5-825">如果使用 SAP Note [1999351] 進行排解疑難並未解決問題，請重新執行 `Set-AzureRmVMAEMExtension` 組態指令碼 (如[設定 Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] 所述)。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-825">If troubleshooting by using SAP Note [1999351] does not resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="5d2b5-826">因為儲存體分析或診斷計數器在啟用後可能未立即建立，所以您可能必須等待一個小時的時間。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-826">You might have to wait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="5d2b5-827">如果問題仍然存在，請在元件 BC-OP-NT-AZR (適用於 Windows) 或 BC-OP-LNX-AZR (適用於 Linux 虛擬機器) 上開啟 SAP 客戶支援訊息。</span><span class="sxs-lookup"><span data-stu-id="5d2b5-827">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
