---
title: "虛擬機器部署在 Windows 上的 sap aaaAzure |Microsoft 文件"
description: "了解如何 toodeploy SAP 軟體的 Windows Azure 中的虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a>透過 Azure 在 Windows VM 上部署 SAP
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
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Azure 虛擬機器是 hello 解決方案需要運算和存放裝置資源，最少的時間，而不冗長的採購循環的組織。 您可以在 Azure 中使用 Azure 虛擬機器 toodeploy 古典應用程式，例如 SAP NetWeaver 架構的應用程式。 擴充應用程式的可靠性與可用性，不需其他內部部署資源。 「Azure 虛擬機器」支援跨單位連線能力，貴公司可將「Azure 虛擬機器」整合到其內部部署網域、私人雲端，以及 SAP 系統環境中。

在本文中，我們將討論 hello 步驟 toodeploy SAP 應用程式在 Azure 中的 Windows 虛擬機器 (Vm) 上。 這篇文章中的 hello 資訊為基礎[Azure 虛擬機器規劃和實作適用於在 Windows 上的 SAP][planning-guide]。 它也可 SAP 安裝文件集和 SAP 附註，也就是安裝和部署 SAP 軟體的 hello 主要資源。

## <a name="prerequisites"></a>必要條件
針對 SAP 軟體部署設定 Azure 虛擬機器，牽涉到多個步驟和資源。 開始之前，請確定您符合 Windows Azure 中的虛擬機器上安裝 SAP 軟體的 hello 必要條件。

### <a name="local-computer"></a>本機電腦
toomanage Windows 或 Linux Vm，您可以使用 PowerShell 指令碼和 hello Azure 入口網站。 對於這兩種工具，您需有執行 Windows 7 或更新 Windows 版本的本機電腦。 如果您想 toomanage 僅 Linux Vm，而且您想 toouse Linux 電腦，這項工作，您可以使用 Azure CLI。

### <a name="internet-connection"></a>網際網路連線
toodownload 執行的 hello 工具及指令碼所需的 SAP 軟體部署，您必須是連接 toohello 網際網路。 hello 執行 hello Azure 強化監視功能延伸模組適用於 SAP 的 Azure VM 也需要存取 toohello 網際網路。 如果 hello Azure VM 的 Azure 虛擬網路或內部部署網域的一部分，請確定，hello 相關的 proxy 設定，如所述[設定 hello proxy][deployment-guide-configure-proxy]。

### <a name="microsoft-azure-subscription"></a>Microsoft Azure 訂用帳戶
您需要使用中的 Azure 帳戶。

### <a name="topology-and-networking"></a>拓撲和網路
您需要 toodefine hello 拓樸和 hello Azure 中 SAP 部署的架構：

* 使用 azure 儲存體帳戶 toobe
* 您想要 toodeploy hello SAP 系統的虛擬網路
* 您希望 toodeploy hello SAP 系統的資源群組 toowhich
* 您想 toodeploy hello SAP 系統的 azure 地區
* SAP 組態 (兩層或三層)
* VM 大小和其他虛擬硬碟 (Vhd) toobe hello 號碼掛接 toohello Vm
* SAP Correction and Transport System (CTS) 組態

建立並設定 Azure 儲存體帳戶或 Azure 虛擬網路，才能開始 hello SAP 軟體部署程序。 如需有關資訊 toocreate 和設定這些資源，請參閱[Azure 虛擬機器規劃和實作適用於在 Windows 上的 SAP][planning-guide]。

### <a name="sap-sizing"></a>SAP 大小調整
了解下列資訊，如 SAP 調整大小的 hello:

* 預計的 SAP 工作負載，比方說，使用 hello SAP 快速 Sizer 工具，與 hello SAP 應用程式的效能標準 (SAP)
* 需要 CPU 資源和記憶體耗用量的 hello SAP 系統
* 每秒所需的輸入/輸出 (I/O) 作業
* Azure 中 VM 之間最終通訊所需的網路頻寬
* 在內部部署資產和 hello Azure 部署 SAP 系統之間的所需的網路頻寬

### <a name="resource-groups"></a>資源群組
Azure 資源管理員 中，您可以使用資源群組 toomanage hello 應用程式的所有資源在您的 Azure 訂用帳戶。 如需詳細資訊，請參閱 [Azure Resource Manager概觀][resource-group-overview]。

## <a name="resources"></a>資源

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP 資源
當您設定 SAP 軟體部署時，您需要遵循 SAP 資源 hello:

* SAP Note [1928533]，其中包含：
  * Hello 部署 SAP 軟體所支援的 Azure VM 大小的清單
  * Azure VM 大小的重要容量資訊
  * 支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合
  * Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本

* SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。
* SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。
* SAP 附註[1409604] hello 需 SAP Host Agent 版本 Windows Azure 中。
* SAP 附註[2191498]具有 hello 必要 SAP Host Agent 版本適用於在 Azure 中的 Linux。
* SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。
* SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。
* SAP Note [2002167] 包含 Red Hat Enterprise Linux 7.x 的一般資訊。
* SAP 附註[1999351] hello Azure 強化監視功能延伸模組適用於 SAP 的其他疑難排解資訊。
* [SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。
* [Azure PowerShell][azure-ps] 所包含的 SAP 特定 PowerShell Cmdlet。
* [Azure CLI][azure-cli] 所包含的 SAP 特定 Azure CLI 命令。

[comment]: <> (MSSedusch TODO 新增 SAP 附註 1409604 中 SAP Host Agent 的 ARM 修補程式層級)

### <a name="microsoft-resources"></a>Microsoft 資源
這些 Microsoft 文章涵蓋 Azure 中的 SAP 部署：

* [適用於 SAP on Windows 的 Azure 虛擬機器規劃和實作][planning-guide]
* [適用於 SAP on Windows 的 Azure 虛擬機器部署 (本文)][deployment-guide]
* [適用於 SAP on Windows 的 Azure 虛擬機器 DBMS 部署][dbms-guide]
* [Azure 入口網站][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure VM 上的 SAP 軟體部署案例
您有多個選項可用於在 Azure 中部署 VM 和相關聯的磁碟。 部署選項之間的重要 toounderstand hello 差異是因為您可能需要不同的步驟 tooprepare 根據您所選擇的 hello 部署類型的部署 Vm。

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>案例 1： 部署從 hello 適用於 SAP 的 Azure Marketplace 中的 VM
您可以使用由 Microsoft 提供的映像，或由協力廠商 hello Azure Marketplace toodeploy 在您的 VM。 hello Marketplace 提供了一些標準的 OS 映像的 Windows Server 和其他 Linux 散發套件。 您也可以部署包含資料庫管理系統 (DBMS) SKU 的映像，例如，Microsoft SQL Server。 如需使用映像搭配 DBMS SKU 的詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]。

hello 下列流程圖顯示 hello SAP 特定的序列，部署將 VM 從 hello Azure Marketplace 的步驟：

![使用 VM 映像從 hello Azure Marketplace 的 SAP 系統部署 VM 的流程圖][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站建立虛擬機器
最簡單方式 toocreate hello hello Azure Marketplace 中的影像與新的虛擬機器是使用 hello Azure 入口網站。

1.  跳過<https://portal.azure.com/#create>。  或者，您也可以在 hello Azure 入口網站功能表，選取**+ 新增**。
2.  選取**計算**，然後選取您想要 toodeploy 作業系統的 hello 類型。 例如，Windows Server 2012 R2、SUSE Linux Enterprise Server 12 (SLES 12) 或 Red Hat Enterprise Linux 7.2 (RHEL 7.2)。 hello 預設清單檢視不會顯示所有支援的作業系統。 選取 [查看全部] 以取得完整清單。 如需 SAP 軟體部署支援的作業系統詳細資訊，請參閱 SAP Note [1928533]。
3.  在 hello 下一個頁面上，檢閱 條款和條件。
4.  在 hello**選取部署模型**方塊中，選取**資源管理員**。
5.  選取 [ **建立**]。

hello 精靈會引導您完成設定所需的 hello 參數 toocreate hello 虛擬機器，此外 tooall 所需的資源，如網路介面和儲存體帳戶。 其中一些參數包括︰

1. **基本**：
  * **名稱**: hello hello 資源 （hello 虛擬機器名稱） 名稱。
 * **使用者名稱和密碼**或**SSH 公開金鑰**: hello 使用者名稱和密碼的 hello 佈建期間建立的 hello 使用者輸入。 針對 Linux 虛擬機器，您可以輸入 hello toohello 機器用於 toosign 公開安全殼層 (SSH) 金鑰。
 * **訂用帳戶**： 選取您想要 toouse tooprovision hello 新虛擬機器的 hello 訂用帳戶。
 * **資源群組**: hello hello 資源群組名稱 hello VM。 您可以輸入新資源群組或 hello 名稱的資源群組已存在的任何一個 hello 名稱。
 * **位置**: toodeploy hello 新的虛擬機器的位置。 如果您想 tooconnect hello 虛擬機器 tooyour 在內部部署網路，請確定您選取 hello hello Azure tooyour 在內部部署網路連線的虛擬網路位置。 如需詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]中的[Microsoft Azure 網路][planning-guide-microsoft-azure-networking]。
2. **大小**：

     如需支援的 VM 類型清單，請參閱 SAP Note [1928533]。 請確定您選取 hello 正確的 VM 類型，如果您想 toouse Azure 高階儲存體。 並非所有 VM 類型都支援進階儲存體。 如需詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]中的[儲存體：Microsoft Azure 儲存體和資料磁碟][planning-guide-storage-microsoft-azure-storage-and-data-disks]和 [Azure 進階儲存體][planning-guide-azure-premium-storage]。

3. **設定**：
   * **儲存體帳戶**：選取現有的儲存體帳戶或建立新的儲存體帳戶。 並非所有的儲存體類型都適用於執行 SAP 應用程式。 如需儲存體類型的詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]。
   * **虛擬網路**和**子網路**: toointegrate hello 虛擬機器與您的內部網路連線的 tooyour 在內部部署網路選取 hello 虛擬網路。
   * **公用 IP 位址**： 選取 hello 公用 IP 位址，您想 toouse，或輸入參數 toocreate 新的公用 IP 位址。 您可以透過 hello 網際網路使用公用 IP 位址 tooaccess 您的虛擬機器。 請確定，您也可以建立網路安全性群組 toohelp 安全存取 tooyour 虛擬機器。
   * **網路安全性群組**：如需詳細資訊，請參閱[使用網路安全性群組控制網路流量流程][virtual-networks-nsg]。
   * **可用性**： 選擇可用性設定組，或輸入 hello 參數 toocreate 新的可用性設定。 如需詳細資訊，請參閱 [Azure 可用性設定組][planning-guide-3.2.3]。
   * **監視**︰您可以選取 [停用]監視診斷。 它會自動啟用當您執行 hello 命令 tooenable hello Azure 強化監視功能延伸模組，如中所述[設定監視][deployment-guide-configure-monitoring-scenario-1]。

4. **摘要**：

  檢閱您的選取項目，然後選取 [確定]。

您的虛擬機器部署在您選取的 hello 資源群組。

#### <a name="create-a-virtual-machine-by-using-a-template"></a>使用範本建立虛擬機器
您可以使用其中一種在 hello 發行 hello SAP 範本建立虛擬機器[azure-快速入門範本 GitHub 儲存機制][azure-quickstart-templates-github]。 您也可以手動建立虛擬機器使用 hello [Azure 入口網站][virtual-machines-windows-tutorial]， [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]，或[Azure CLI][virtual-machines-linux-tutorial].

* [**兩層組態 (僅只一部虛擬機器) 範本** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]

  toocreate 兩層式系統使用只有一部虛擬機器，請使用此範本。
* [**三層組態 (多部虛擬機器) 範本** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]

  toocreate 三層式系統使用多部虛擬機器，請使用此範本。

在 hello Azure 入口網站中，輸入下列 hello 範本參數的 hello:

1. **基本**：
  * **訂用帳戶**: hello 訂用帳戶 toouse toodeploy hello 範本。
  * **資源群組**: hello 資源群組 toouse toodeploy hello 範本。 您可以建立新的資源群組，或者您可以選取現有的資源群組 hello 訂用帳戶中。
  * **位置**: toodeploy hello 範本的位置。 如果您選取現有的資源群組時，會使用該資源群組中的 hello 位置。

2. **設定**：
  * **SAP 系統識別碼**: hello SAP 系統識別碼 (SID)。
  * **OS 類型**: hello 想 toodeploy，例如作業系統、 Windows Server 2012 R2、 SUSE Linux Enterprise Server 12 (SLES 12) 或 Red Hat Enterprise Linux 7.2 (RHEL 7.2)。

    hello 預設清單檢視不會顯示所有支援的作業系統。 選取 [查看全部] 以取得完整清單。 如需 SAP 軟體部署支援的作業系統詳細資訊，請參閱 SAP Note [1928533]。
  * **SAP 系統大小**: hello hello SAP 系統的大小。

    提供的 SAPS hello 新系統的 hello 數目。 如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。
  * **系統可用性**（三層式範本）： hello 系統可用性。

    選取適合高可用性安裝組態的 **HA**。 為 ABAP SAP Central Services (ASCS) 建立兩部資料庫伺服器和兩部伺服器。
  * **儲存體類型**（僅限兩層式範本）： hello 的儲存體 toouse 型別。

    對於大型系統，我們強烈建議使用 Azure 進階儲存體。 如需儲存體類型的詳細資訊，請參閱下列資源：
      * [針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]
      * [適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]
      * [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]
      * [簡介 tooMicrosoft Azure 儲存體][storage-introduction]
  * **管理員使用者名稱**和**管理員密碼**：使用者名稱和密碼。
    建立新的使用者，登入 toohello 虛擬機器。
  * **新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。 如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。
  * **子網路識別碼**: hello 識別碼 hello 子網路 hello 虛擬機器會連接到。 選取您的虛擬私人網路 (VPN) 或 Azure ExpressRoute 虛擬網路 toouse tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。 hello 識別碼通常看起來像這樣： /subscriptions/&lt;訂用帳戶 id > /resourceGroups/&lt;資源群組名稱 > /providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱 > /subnets/&lt;子網路名稱 >

3. **條款及條件**：  
    檢閱並接受 hello 法律條款。

4.  選取 [購買]。

當您使用從 hello Azure Marketplace 映像時，預設會部署 hello Azure VM 代理程式。

#### <a name="configure-proxy-settings"></a>進行 Proxy 設定
根據您在內部部署網路的設定方式，您可能需要在 VM 上的 tooset hello proxy。 如果 VM 是透過 VPN 或 ExpressRoute 連線的 tooyour 在內部部署網路，hello VM 可能不是可以 tooaccess hello 網際網路，和不可以 toodownload hello 所需的擴充功能或收集的監視資料。 如需詳細資訊，請參閱[設定 hello proxy][deployment-guide-configure-proxy]。

#### <a name="join-a-domain-windows-only"></a>加入網域 (僅限 Windows)
如果您的 Azure 部署連接的 tooan 在內部部署 Active Directory 或 DNS 執行個體已透過 Azure 站台對站 VPN 連線或 ExpressRoute (這稱為*跨單位*中[規劃 Azure 虛擬機器與適用於 Linux 上的 SAP 實作][planning-guide])，預期該 hello VM 加入內部網域。 如需考量這項工作的詳細資訊，請參閱[加入 VM tooan 在內部部署網域 (僅限 Windows)][deployment-guide-4.3]。

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>設定監視
確定您的環境支援 SAP、 設定中所述的 hello Azure Monitoring Extension for SAP toobe[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。 檢查 SAP monitoring，和最低要求版本的 SAP 核心與 SAP Host Agent，在 hello 中列出的資源中的 hello 必要條件[SAP 資源][deployment-guide-2.2]。

#### <a name="monitoring-check"></a>監視檢查
如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。

#### <a name="post-deployment-steps"></a>部署後步驟
在建立之後 hello VM 及 hello VM 的部署，您需要在 hello VM tooinstall hello 必要軟體元件。 在這種類型的 VM 部署的 hello 部署/軟體安裝順序，因為安裝 hello 軟體 toobe 必須已經是可供使用，在 Azure 中，另一個在 VM 上，或為可附加的磁碟。 或者，請考慮使用跨單位案例中，哪些連線 toohello 內部部署資產 （安裝共用） 指定。

部署在 Azure VM 之後，後續 hello 相同指導方針和工具 tooinstall hello SAP 軟體在您為您的 VM 會在內部部署環境中。 tooinstall Azure VM 上的 SAP 軟體，同時 SAP 和 Microsoft 建議您上傳並儲存 hello SAP 安裝媒體上 Azure Vhd，或您建立可做為檔案伺服器具有所有 hello Azure VM 所需的 SAP 安裝媒體。

[comment]: <> (為什麼需要 toorecommend 檔案管理 中，例如 MSSedusch TODO、 檔案伺服器或 VHD？這是否與內部部署不同？)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>案例 2：使用自訂映像為 SAP 部署 VM
因為不同版本的作業系統或 DBMS 擁有不同修補程式需求，您在 hello Azure Marketplace 中找到的 hello 映像可能無法滿足您的需求。 Toocreate VM 而可以使用您自己 OS/DBMS VM 映像，您可以稍後再部署。
您使用不同的步驟 toocreate 私人映像適用於 Linux 比 windows toocreate 其中一個。

- - -
> ![Windows][Logo_Windows] Windows
>
> 您可以使用多個虛擬機器、 hello Windows 設定 （例如 Windows SID 和主機名稱） 必須是抽象或一般化的 toodeploy hello 的 Windows 映像 tooprepare 內部部署 VM。 您可以使用[sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo 這。
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare Linux 映像，您可以使用 toodeploy 多部虛擬機器，某些 Linux 設定必須是抽象或一般化上 hello 內部部署 VM。 您可以使用`waagent -deprovision`toodo 這。 如需詳細資訊，請參閱[擷取 Linux 虛擬機器在 Azure 上執行][ virtual-machines-linux-capture-image]和 hello [Azure Linux 代理程式使用者指南][virtual-machines-linux-agent-user-guide-command-line-options]。
>
>

- - -
您可以準備和建立自訂映像，，然後使用它 toocreate 多個新的 Vm。 如需詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]。 設定您的資料庫內容，透過 SAP Software Provisioning Manager tooinstall 新 SAP 系統 （從是附加的 toohello 虛擬機器的 VHD 會還原資料庫備份） 或還原資料庫備份，直接從 Azure 儲存體，如果您的 DBMS支援它。 如需詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]。 如果您已在內部部署 VM （特別是針對兩層式系統） 上安裝 SAP 系統，您可以使用 hello 系統重新命名程序支援的 SAP 軟體佈建 hello 部署的 hello Azure VM 後調整 hello SAP 系統設定管理員 (SAP 附註[1619720])。 否則，您也可以在您部署的 hello Azure VM 之後安裝 hello SAP 軟體。

hello 下列流程圖顯示 hello SAP 特定的序列，部署將 VM 從自訂映像的步驟：

![使用私人 Marketplace 中的 VM 映像部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>建立 hello 的虛擬機器
toocreate 使用私用 hello Azure 入口網站，從作業系統映像的部署使用其中一個 hello 遵循 SAP 範本。 在 hello 中發佈這些範本[azure-快速入門範本 GitHub 儲存機制][azure-quickstart-templates-github]。 您可以也使用 [PowerShell][virtual-machines-upload-image-windows-resource-manager] 手動建立虛擬機器。

* [**兩層組態 (僅限一部虛擬機器) 範本** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]

  toocreate 兩層式系統使用只有一部虛擬機器，請使用此範本。
* [**三層組態 (多部虛擬機器) 範本** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]

  toocreate 三層式系統使用多部虛擬機器或您自己的作業系統映像，請使用此範本。

在 hello Azure 入口網站中，輸入下列 hello 範本參數的 hello:

1. **基本**：
  * **訂用帳戶**: hello 訂用帳戶 toouse toodeploy hello 範本。
  * **資源群組**: hello 資源群組 toouse toodeploy hello 範本。 您可以建立新的資源群組，或選取現有的資源群組 hello 訂用帳戶中。
  * **位置**: toodeploy hello 範本的位置。 如果您選取現有的資源群組時，會使用該資源群組中的 hello 位置。
2. **設定**：
  * **SAP 系統識別碼**: hello SAP 系統識別碼。
  * **OS 類型**: hello 想 toodeploy （Windows 或 Linux） 的作業系統類型。
  * **SAP 系統大小**: hello hello SAP 系統的大小。

    提供的 SAPS hello 新系統的 hello 數目。 如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。
  * **系統可用性**（三層式範本）： hello 系統可用性。

    選取適合高可用性安裝組態的 **HA**。 為 ASCS 建立兩部資料庫伺服器和兩部伺服器。
  * **儲存體類型**（僅限兩層式範本）： hello 的儲存體 toouse 型別。

    對於大型系統，我們強烈建議使用 Azure 進階儲存體。 如需存放裝置類型的詳細資訊，請參閱下列資源的 hello:
      * [針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]
      * [適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]
      * [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]
      * [簡介 tooMicrosoft Azure 儲存體][storage-introduction]
  * **使用者映像 VHD URI**: hello 的 hello 私人 OS 映像 VHD，例如 https:// URI&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd。
  * **使用者映像儲存體帳戶**: hello hello 私人 OS 映像儲存的位置，例如的 hello 儲存體帳戶名稱&lt;accountname > 中 https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd。
  * **系統管理員使用者名稱**和**系統管理員密碼**: hello 使用者名稱和密碼。

    建立新的使用者，登入 toohello 虛擬機器。
  * **新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。 如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。
  * **子網路識別碼**: hello 識別碼 hello 子網路 toowhich hello 虛擬機器會連接到。 選取您的 VPN 或 ExpressRoute 虛擬網路 toouse tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。 hello 識別碼通常看起來像這樣：

    /subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱>

3. **條款及條件**：  
    檢閱並接受 hello 法律條款。

4.  選取 [購買]。

#### <a name="install-hello-vm-agent-linux-only"></a>安裝 VM 代理程式 (只有 Linux) hello
toouse hello 範本 hello 前面一節中所述，hello hello 使用者映像或 hello 部署中必須已安裝 Linux 代理程式將會失敗。 下載並安裝 hello 使用者映像中的 hello VM 代理程式中所述[下載、 安裝及啟用 hello Azure VM 代理程式][deployment-guide-4.4]。 如果您不使用 hello 範本，您也可以安裝 hello VM 代理程式更新版本。

#### <a name="join-a-domain-windows-only"></a>加入網域 (僅限 Windows)
如果您的 Azure 部署連接的 tooan 在內部部署 Active Directory 或 DNS 執行個體已透過 Azure 站台對站 VPN 連線或 Azure ExpressRoute (這稱為*跨單位*中[Azure 虛擬機器規劃和實作適用於 Linux 上的 SAP][planning-guide])，預期該 hello VM 加入內部網域。 如需這個步驟的考量的詳細資訊，請參閱[加入 VM tooan 在內部部署網域 (僅限 Windows)][deployment-guide-4.3]。

#### <a name="configure-proxy-settings"></a>進行 Proxy 設定
根據您在內部部署網路的設定方式，您可能需要在 VM 上的 tooset hello proxy。 如果 VM 是透過 VPN 或 ExpressRoute 連線的 tooyour 在內部部署網路，hello VM 可能不是可以 tooaccess hello 網際網路，和不可以 toodownload hello 所需的擴充功能或收集的監視資料。 如需詳細資訊，請參閱[設定 hello proxy][deployment-guide-configure-proxy]。

#### <a name="configure-monitoring"></a>設定監視
確定您的環境支援 SAP、 設定中所述的 hello Azure Monitoring Extension for SAP toobe[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。 檢查 SAP monitoring，和最低要求版本的 SAP 核心與 SAP Host Agent，在 hello 中列出的資源中的 hello 必要條件[SAP 資源][deployment-guide-2.2]。

#### <a name="monitoring-check"></a>監視檢查
如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>案例 3：使用非一般化 Azure VHD 搭配 SAP 來移動內部部署 VM
在此案例中，您計劃 toomove 特定 SAP 系統從內部部署環境 tooAzure。 您可以執行這項操作 hello hello OS，hello SAP 二進位檔，VHD 上傳及最終 hello DBMS 二進位檔，再加上 hello Vhd hello 資料和記錄檔的 hello tooAzure 的 DBMS。 不同於中所述的 hello 案例[案例 2： 使用部署 VM 的自訂映像為 SAP][deployment-guide-3.3]、 在此情況下，保留 hello 主機名稱、 SAP SID 和 SAP 使用者帳戶在 hello Azure VM 中，所以它們在 hello 在內部部署環境中設定。 您不需要 toogeneralize hello OS。 此案例適用於最常 toocross 內部部署案例，其中 hello SAP 環境的一部分執行的內部部署和在 Azure 上執行的一部分。

在此案例中，hello VM 代理程式不會自動安裝在部署期間。 由於 hello VM 代理程式 」 和 「 hello Azure 強化監視功能延伸模組適用於 SAP 的必要項 toorun SAP，您需要 toodownload、 安裝和啟用這兩個元件建立 hello 虛擬機器之後，以手動方式。

如需 hello Azure VM 代理程式的詳細資訊，請參閱下列資源的 hello。

[comment]: <> (MSSedusch TODO 更新下方的 Windows 連結)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Azure Linux 代理程式使用者指南][virtual-machines-linux-agent-user-guide]
>
>

- - -

下列流程圖顯示 hello 順序的步驟，使用非一般化 Azure VHD 移動內部部署 VM 的 hello:

![使用 VM 磁碟部署適用於 SAP 系統之 VM 的流程圖][deployment-guide-figure-400]

假設 hello 磁碟已上傳，並在 Azure 中定義 (請參閱[Azure 虛擬機器規劃和實作適用於 Linux 上的 SAP][planning-guide])，請勿 hello 工作中所述 hello 接下來的幾個章節。

#### <a name="create-a-virtual-machine"></a>建立虛擬機器
toocreate 使用私用的作業系統磁碟，透過 hello Azure 入口網站的部署使用 hello SAP 範本發行在 hello [azure-快速入門範本 GitHub 儲存機制][azure-quickstart-templates-github]。 您可以也使用 PowerShell 手動建立虛擬機器。

* [**兩層組態 (僅限一部虛擬機器) 範本**  (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]

  toocreate 兩層式系統使用只有一部虛擬機器，請使用此範本。

在 hello Azure 入口網站中，輸入下列 hello 範本參數的 hello:

1. **基本**：
  * **訂用帳戶**: hello 訂用帳戶 toouse toodeploy hello 範本。
  * **資源群組**: hello 資源群組 toouse toodeploy hello 範本。 您可以建立新的資源群組，或選取現有的資源群組 hello 訂用帳戶中。
  * **位置**: toodeploy hello 範本的位置。 如果您選取現有的資源群組時，會使用該資源群組中的 hello 位置。
2. **設定**：
  * **SAP 系統識別碼**: hello SAP 系統識別碼。
  * **OS 類型**: hello 想 toodeploy （Windows 或 Linux） 的作業系統類型。
  * **SAP 系統大小**: hello hello SAP 系統的大小。

    提供的 SAPS hello 新系統的 hello 數目。 如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。
  * **儲存體類型**（僅限兩層式範本）： hello 的儲存體 toouse 型別。

    對於大型系統，我們強烈建議使用 Azure 進階儲存體。 如需存放裝置類型的詳細資訊，請參閱下列資源的 hello:
      * [針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體][2367194]
      * [適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]中的 [Microsoft Azure 儲存體][dbms-guide-2.3]
      * [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體][storage-premium-storage-preview-portal]
      * [簡介 tooMicrosoft Azure 儲存體][storage-introduction]
  * **作業系統磁碟 VHD URI**: hello 的 hello 的私用作業系統磁碟，而例如 https:// URI&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd。
  * **新的或現有的子網路**︰決定要建立新的虛擬網路和子網路，還是使用現有的子網路。 如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。
  * **子網路識別碼**: hello 識別碼 hello 子網路 toowhich hello 虛擬機器會連接到。 選取您的 VPN、 Azure ExpressRoute 虛擬網路 toouse tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。 hello 識別碼通常看起來像這樣：

    /subscriptions/&lt;訂用帳戶識別碼>/resourceGroups/&lt;資源群組名稱>/providers/Microsoft.Network/virtualNetworks/&lt;虛擬網路名稱>/subnets/&lt;子網路名稱>

3. **條款及條件**：  
    檢閱並接受 hello 法律條款。

4.  選取 [購買]。

#### <a name="install-hello-vm-agent"></a>安裝 VM 代理程式 hello
範本中所述的 toouse hello hello 上一節、 hello VM 代理程式必須安裝在 hello 作業系統磁碟或 hello 部署將會失敗。 下載並安裝在 hello VM 中的 hello VM 代理程式中所述[下載、 安裝及啟用 hello Azure VM 代理程式][deployment-guide-4.4]。

如果您不使用 hello 範本 hello 前面一節中所述，您也可以安裝 hello VM 代理程式之後。

#### <a name="join-a-domain-windows-only"></a>加入網域 (僅限 Windows)
如果您的 Azure 部署連接的 tooan 在內部部署 Active Directory 或 DNS 執行個體已透過 Azure 站台對站 VPN 連線或 ExpressRoute (這稱為*跨單位*中[規劃 Azure 虛擬機器與適用於 Linux 上的 SAP 實作][planning-guide])，預期該 hello VM 加入內部網域。 如需考量這項工作的詳細資訊，請參閱[加入 VM tooan 在內部部署網域 (僅限 Windows)][deployment-guide-4.3]。

#### <a name="configure-proxy-settings"></a>進行 Proxy 設定
根據您在內部部署網路的設定方式，您可能需要在 VM 上的 tooset hello proxy。 如果 VM 是透過 VPN 或 ExpressRoute 連線的 tooyour 在內部部署網路，hello VM 可能不是可以 tooaccess hello 網際網路，和不可以 toodownload hello 所需的擴充功能或收集的監視資料。 如需詳細資訊，請參閱[設定 hello proxy][deployment-guide-configure-proxy]。

#### <a name="configure-monitoring"></a>設定監視
確定您的環境支援 SAP、 設定中所述的 hello Azure Monitoring Extension for SAP toobe[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。 檢查 SAP monitoring，和最低要求版本的 SAP 核心與 SAP Host Agent，在 hello 中列出的資源中的 hello 必要條件[SAP 資源][deployment-guide-2.2]。

#### <a name="monitoring-check"></a>監視檢查
如[針對設定端對端監視進行檢查及疑難排解][deployment-guide-troubleshooting-chapter]所述，檢查監視是否正常運作。

## <a name="update-hello-monitoring-configuration-for-sap"></a>更新 hello 適用於 SAP 的監視設定
更新任何下列案例的 hello hello SAP 監視組態：
* hello 聯合 Microsoft/SAP 小組擴充監視功能的 hello，並要求更多或較少的計數器。
* Microsoft 導入了新版本的 hello 基礎的 Azure 基礎結構，提供 hello 監控資料，並針對 SAP 需求 toobe hello Azure 強化監視功能延伸模組調整 toothose 變更。
* 裝載其他 Vhd tooyour Azure VM，或移除 VHD。 在此案例中，更新儲存體相關資料的 hello 集合。 變更組態，藉由加入或刪除端點或指派 IP 位址 tooa VM 不會影響 hello 監視設定。
* 您變更 hello 您 Azure VM 的大小，例如大小 A5 tooany 從其他 VM 大小。
* 您加入新的網路介面 tooyour Azure VM。

中的監視設定，監視基礎結構，可遵循 hello 更新 hello tooupdate 步驟[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>在 Windows VM 上部署 SAP 軟體的詳細工作
本節詳述執行 hello 組態和部署程序中的特定工作的步驟。

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>部署 Azure PowerShell Cmdlet
1.  跳過[Microsoft Azure 下載](https://azure.microsoft.com/downloads/)。
2.  在**命令列工具**的 **PowerShell** 之下，選取 [Windows 安裝]。
3.  在 hello Microsoft 下載管理員對話方塊中，hello 下載檔案 (例如，WindowsAzurePowershellGet.3f.3f.3fnew.exe) 選取**執行**。
4.  選取 Microsoft Web Platform Installer (Microsoft Web PI) toorun**是**。
5.  如下所示的頁面隨即出現︰

  ![Azure PowerShell Cmdlet 的安裝頁面][deployment-guide-figure-500]<a name="figure-5"></a>

6.  選取**安裝**，然後接受 hello Microsoft 軟體授權條款。
7.  已安裝 PowerShell。 選取**完成**tooclose hello 安裝精靈。

經常檢查有無更新 toohello PowerShell cmdlet，這通常每月更新。 hello 最簡單方式 toocheck 更新為先前的安裝步驟，在步驟 5 中所顯示的 toohello 安裝網頁註冊的 toodo hello。 hello 發行日期] 和 [發行 hello cmdlet 包含一些步驟 5 所示的 hello 頁面上。 除非在 SAP 附註中指定，否則[1928533]或 SAP Note [2015553]，我們建議您搭配 hello 最新版 Azure PowerShell cmdlet。

toocheck hello 版的 hello Azure PowerShell cmdlet 安裝在您的電腦上執行這個 PowerShell 命令：
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
hello 結果看起來像這樣：

![Azure PowerShell Cmdlet 版本檢查的結果][deployment-guide-figure-600]
<a name="figure-6"></a>

Hello hello 安裝精靈的第一頁 hello 目前版本在電腦上安裝的 hello Azure cmdlet 版本時，將代表它**（安裝）** toohello 產品標題 （請參閱下列螢幕擷取畫面的 hello）。 您的 PowerShell Azure Cmdlet 都是最新的。 tooclose hello 安裝精靈中，選取**結束**。

![安裝 Azure PowerShell cmdlet，指出該 hello 最新版本的 Azure PowerShell cmdlet 的安裝頁面][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>部署 Azure CLI
1.  跳過[Microsoft Azure 下載](https://azure.microsoft.com/downloads/)。
2.  在下**命令列工具**下**Azure 命令列介面**，選取 hello**安裝**適用於您作業系統的連結。
3.  在 hello Microsoft 下載管理員對話方塊中，hello 下載檔案 (例如，WindowsAzureXPlatCLI.3f.3f.3fnew.exe) 選取**執行**。
4.  選取 Microsoft Web Platform Installer (Microsoft Web PI) toorun**是**。
5.  如下所示的頁面隨即出現︰

  ![Azure PowerShell Cmdlet 的安裝頁面][deployment-guide-figure-500]<a name="figure-5"></a>

6.  選取**安裝**，然後接受 hello Microsoft 軟體授權條款。
7.  已安裝 Azure CLI。 選取**完成**tooclose hello 安裝精靈。

經常檢查有無更新 tooAzure CLI，通常每月更新。 hello 最簡單方式 toocheck 更新為先前的安裝步驟，在步驟 5 中所顯示的 toohello 安裝網頁註冊的 toodo hello。


您的電腦已安裝的 Azure CLI toocheck hello 版本會執行下列命令：
```
azure --version
```

hello 結果看起來像這樣：

![Azure CLI 版本檢查的結果][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>加入 VM tooan 在內部部署網域 (僅限 Windows)
如果您將 SAP Vm 部署在跨內部單位案例中，在內部部署 Active Directory 和 DNS 在 Azure 中，擴充其中預期 hello Vm 加入內部網域。 hello 採取 toojoin VM tooan 在內部部署網域的詳細的步驟和 hello 需要其他軟體 toobe 在內部部署網域的成員會因客戶。 通常，toojoin VM tooan 內部部署網域，您需要 tooinstall 其他軟體，例如反惡意程式碼軟體及備份或監視軟體。

在此案例中，您也需要 toomake 確定 VM 加入您的環境中的網域時，會強制執行網際網路 proxy 設定，如果有本機系統帳戶 (S-1-5-18) hello 客體 VM 中的 hello Windows hello 相同的 proxy 設定。 hello 最簡單的選項是使用網域群組原則，套用在 hello 網域 toosystems tooforce hello proxy。

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>下載、 安裝及啟用 hello Azure VM 代理程式
從無法一般化 （例如映像中的 hello Windows 系統準備或 sysprep 工具不會產生） 的作業系統映像部署的虛擬機器，您需要 toomanually 下載、 安裝和啟用 hello Azure VM 代理程式。

如果您部署的 hello Azure Marketplace 的 VM 時，就不需要此步驟。 Hello Azure Marketplace 映像已擁有 hello Azure VM 代理程式。

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  下載 hello Azure VM 代理程式：
  1.  下載 hello [Azure VM 代理程式安裝程式套件](https://go.microsoft.com/fwlink/?LinkId=394789)。
  2.  在個人電腦或伺服器上的本機儲存 hello VM 代理程式 MSI 封裝。
2.  安裝 hello Azure VM 代理程式：
  1.  連接 toohello 使用遠端桌面通訊協定 (RDP) 來部署 Azure VM。
  2.  開啟 hello VM 上的 Windows 檔案總管 視窗，然後選取 hello hello 的 hello VM 代理程式的 MSI 檔案的目標目錄。
  3.  拖曳 hello hello VM 代理程式在 hello VM 上的本機電腦/伺服器 toohello 目標目錄中的 Azure VM 代理程式安裝程式 MSI 檔案。
  4.  按兩下 hello hello VM 上的 MSI 檔案。
3.  對於聯結的 tooon 內部網域的 Vm，請確定最終網際網路 proxy 設定，也適用於 VM，hello toohello Windows 本機系統帳戶 (S-1-5-18) 中所述[設定 hello proxy] [ deployment-guide-configure-proxy]. hello VM 代理程式在此內容中執行，並需要 toobe 無法 tooconnect tooAzure。

不不需要的 tooupdate hello Azure VM 代理程式的任何使用者互動。 hello VM 代理程式會自動更新，而且不需要在 VM 重新啟動。

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
使用下列命令 tooinstall hello VM 代理程式適用於 Linux 的 hello:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL)**

  ```
  sudo yum install WALinuxAgent
  ```

如果已安裝 hello 代理程式，tooupdate hello Azure Linux 代理程式，請勿 hello 中所述步驟[來自 GitHub 的 VM toohello 最新版本更新 hello Azure Linux 代理程式][virtual-machines-linux-update-agent]。

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>設定 hello proxy
hello 步驟 tooconfigure hello proxy 在 Windows 中是不同於您在 Linux 中設定 hello proxy 的 hello 方式。

#### <a name="windows"></a>Windows
Proxy 設定必須正確設定，如 hello tooaccess hello 網際網路的本機系統帳戶。 如果您的 proxy 設定未由群組原則設定，您可以設定 hello hello 本機系統帳戶。

1. 跳過**啟動**，輸入**gpedit.msc**，然後選取**Enter**。
2. 選取 [電腦設定] > [系統管理範本] > [Windows 元件] > [Internet Explorer]。 請確定該 hello 設定**設定每部電腦 （而非個別使用者） 建立 proxy**已停用或未設定。
3. 在**控制台**，跳過**網路和共用中心** > **網際網路選項**。
4. 在 [hello**連線**索引標籤，選取 hello **LAN 設定**] 按鈕。
5. 清除 hello**自動偵測設定**核取方塊。
6. 選取 hello**您的區域網路使用 proxy 伺服器**核取方塊，，，然後輸入 hello proxy 位址和連接埠。
7. 選取 hello**進階** 按鈕。
8. 在 hello**例外狀況**方塊中，輸入 hello IP 位址**168.63.129.16**。 選取 [確定] 。


#### <a name="linux"></a>Linux
Microsoft Azure 客體代理程式，也就是位於 hello hello 設定檔中設定 hello 正確的 proxy\\等\\waagent.conf。

設定下列參數的 hello:

1.  **HTTP Proxy 主機**。 例如，設定太**proxy.corp.local**。
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **HTTP Proxy 連接埠**。 例如，設定太**80**。
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  重新啟動 hello 代理程式。

  ```
  sudo service waagent restart
  ```

hello 中的 proxy 設定\\等\\waagent.conf 也適用於需要 toohello VM 擴充功能。 如果您想 toouse hello Azure 儲存機制，請確定 hello 流量 toothese 儲存機制不經過您的內部部署內部網路。 如果您建立使用者定義的路由 tooenable 強制通道，請確定您新增的路由，路由傳送流量 toohello 儲存機制直接 toohello 網際網路，而不是透過您的站對站 VPN 連線。

* **SLES**

  您也需要 tooadd 路由 hello IP 位址列於\\等\\regionserverclnt.cfg。 hello 下圖顯示範例：

  ![強制通道][deployment-guide-figure-50]


* **RHEL**

  您也需要 tooadd 路由 hello hello 主機 IP 位址列於\\等\\yum.repos.d\\rhui 負載平衡器。 如需範例，請參閱上述圖 hello。

如需有關使用者定義的路由詳細資訊，請參閱[使用者定義的路由和 IP 轉送][virtual-networks-udr-overview]。

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>設定 Azure 強化監視功能延伸模組適用於 SAP hello
當您已備妥 hello VM 中所述[在 Azure 上 SAP 的 Vm 部署案例][deployment-guide-3]，hello hello 虛擬機器安裝 Azure VM 代理程式。 hello 下一個步驟為 toodeploy hello Azure 增強 Monitoring Extension for SAP，在 hello 全球 Azure 資料中心中的 hello Azure Extension Repository 中可用。 如需詳細資訊，請參閱[適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide-9.1]。

您可以使用 PowerShell 或 Azure CLI tooinstall，並設定 hello Azure 強化監視功能延伸模組適用於 SAP。 tooinstall hello 擴充功能在 Windows 或 Linux VM 上的使用一部 Windows 電腦，請參閱[Azure PowerShell][deployment-guide-4.5.1]。 請參閱 < 使用 Linux 桌面，Linux VM 上的 tooinstall hello 延伸[Azure CLI][deployment-guide-4.5.2]。

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>適用於 Linux 和 Windows VM 的 Azure PowerShell
使用 PowerShell tooinstall hello Azure 強化監視功能延伸模組的 SAP:

1. 請確定您已安裝 hello hello Azure PowerShell cmdlet 的最新版本。 如需詳細資訊，請參閱[部署 Azure PowerShell Cmdlet][deployment-guide-4.1]。  
2. 執行下列 PowerShell cmdlet 的 hello。
  如需可用環境的清單，請執行 `commandlet Get-AzureRmEnvironment`。 如果您想的 toouse 公用 Azure，您的環境是**AzureCloud**。 若為中國的 Azure，請選取 **AzureChinaCloud**。


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

您輸入您的帳戶資料，並找出 hello Azure 虛擬機器之後，hello 指令碼部署所需的 hello 擴充功能，並提供所需的 hello 功能。 這可能需要數分鐘的時間。
如需有關 `Set-AzureRmVMAEMExtension` 的詳細資訊，請參閱 [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension]。

![成功執行 SAP 特定 Azure Cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

hello`Set-AzureRmVMAEMExtension`設定可以進行適用於 SAP 的監視所有的 hello 步驟 tooconfigure 主機。

hello 指令碼輸出包含下列資訊的 hello:

* 確認監視的 hello 基底 VHD （含 hello OS) 和所有其他 Vhd 掛接的 toohello 已設定 VM。
* hello 下面兩個訊息會確認特定儲存體帳戶的儲存體度量 hello 組態。
* 一行輸出提供 hello hello hello 監視組態的實際的更新狀態。
* 另一行輸出會確認該 hello 組態已部署或更新。
* hello 輸出最後一行是參考。 它會顯示測試的 hello 監視設定的選項。

中所述，hello 整備檢查，如 hello Azure 強化監視功能延伸模組 for SAP，繼續 toocheck 成功，已執行的 Azure 強化監視功能的所有步驟，和該 hello Azure 基礎結構提供 hello 必要的資料[Azure 強化監視功能適用於 SAP 的整備檢查][deployment-guide-5.1]。 等候 15-30 分鐘，讓 Azure 診斷 toocollect hello 相關資料。

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>適用於 Linux VM 的 Azure CLI
使用 Azure CLI tooinstall hello Azure 強化監視功能延伸模組的 SAP:

1. 中所述安裝 Azure CLI[安裝 hello Azure CLI][azure-cli]。
2. 使用您的 Azure 帳戶進行登入：

  ```
  azure login
  ```

3. 切換 tooAzure Resource Manager 模式：

  ```
  azure config mode arm
  ```

4. 啟用 Azure Enhanced Monitoring：

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. 請確認該 hello Azure 強化監視功能延伸模組是在 hello Azure Linux VM 上作用。 檢查是否 hello 檔案\\var\\lib\\AzureEnhancedMonitor\\PerfCounters 存在。 如果存在的話，在命令提示字元執行這個命令 toodisplay 所收集資訊的 hello Azure 強化監視：
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

hello 輸出看起來像這樣：
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>針對端對端監視進行檢查及疑難排解
您部署 Azure VM，並設定 hello 相關 Azure 監視基礎結構之後，請檢查所有的 hello 元件的 hello Azure 強化監視功能延伸模組是否如預期般運作。

中所述執行 hello Azure 強化監視功能延伸模組適用於 SAP 的 hello 整備檢查[hello Azure 強化監視功能延伸模組適用於 SAP 的整備檢查][deployment-guide-5.1]。 如果所有整備檢查結果均為正向，而且所有相關效能計數器都呈現 OK 狀態，則已成功設定 Azure 監視。 您可以繼續執行的 SAP Host Agent 中的 hello SAP 附註所述的 hello 安裝[SAP 資源][deployment-guide-2.2]。 如果 hello 整備檢查指出的計數器遺失，則執行中所述的 hello hello Azure 監視基礎結構的健全狀況檢查[的 Azure 監視基礎結構設定健全狀況檢查][ deployment-guide-5.2]. 如需其他疑難排解選項，請參閱[針對適用於 SAP 的 Azure 監視進行疑難排解][deployment-guide-5.3]。

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Hello Azure 強化監視功能延伸模組適用於 SAP 的整備檢查
這項檢查可確保您的 SAP 應用程式中出現的所有效能度量所都提供的 hello Azure 監視基礎結構的基礎。

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>執行 Windows VM 上的 hello 整備檢查

1.  登入 toohello Azure 虛擬機器 （使用系統管理員帳戶不是必要）。
2.  開啟命令提示字元視窗。
3.  Hello 命令提示字元，變更 hello 目錄 toohello 的 hello Azure 強化監視功能延伸模組適用於 SAP 的安裝資料夾： c:\\封裝\\外掛程式\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;版本 >\\卸除

  hello*版本*hello 路徑 toohello 中監視功能延伸模組可能會不同。 如果您看見 hello 監視 hello 安裝資料夾中，核取 hello hello AzureEnhancedMonitoring Windows 服務組態中的擴充功能的多個版本的資料夾，而且交換器 toohello 資料夾再指示為*路徑 tooexecutable*.

  ![服務執行中的屬性 hello Azure 強化監視功能延伸模組的 SAP][deployment-guide-figure-1000]

4.  在 hello 命令提示字元中執行**azperflib.exe**不含任何參數。

  > [!NOTE]
  > Azperflib.exe 會以迴圈執行，並更新 hello 收集計數器每隔 60 秒。 tooend hello 迴圈，關閉 hello 命令提示字元視窗。
  >
  >

如果未安裝 Azure 強化監視功能延伸模組，hello 或 hello AzureEnhancedMonitoring 服務未執行，hello 延伸模組已不正確設定。 如需如何 toodeploy hello 擴充功能的詳細資訊，請參閱[疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構][deployment-guide-5.3]。

##### <a name="check-hello-output-of-azperflibexe"></a>查看 azperflib.exe hello 輸出
Azperflib.exe 輸出會顯示適用於 SAP 的所有已填入 Azure 效能計數器。 在 hello hello 收集的計數器清單底部，摘要和健全狀況指示器會顯示 hello 的 Azure 監視的狀態。

![執行 azperflib.exe 的健康狀態檢查輸出，其表示沒有任何問題][deployment-guide-figure-1100]
<a name="figure-11"></a>

檢查傳回的 hello hello 結果**Counters total**輸出，會針對為空的以及報告**健全狀況狀態**、 hello 前圖所示。

解譯 hello 結果值，如下所示：

| Azperflib.exe 結果值 | Azure 監視健康狀態 |
| --- | --- |
| **API 呼叫 - 無法使用** | 沒有可用的計數器可能不適用 toohello 虛擬機器設定，或錯誤。 請參閱 **Health status**。 |
| **Counters total - empty** |下列兩個 Azure 儲存體計數器 hello 可以是空的： <ul><li>儲存體讀取 Op 延遲伺服器毫秒</li><li>儲存體讀取 Op 延遲 E2E 毫秒</li></ul>所有其他計數器都必須具有值。 |
| **Health status** |只有在傳回狀態顯示 [OK] 時，才算正常。 |
| **診斷** |健康狀態的相關詳細資訊。 |

如果 hello**健全狀況狀態**值不是**確定**，請依照下列中的 hello 指示[的 Azure 監視基礎結構設定健全狀況檢查][ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>執行 Linux VM 上的 hello 整備檢查

1.  使用 SSH 連線 toohello Azure 虛擬機器。

2.  檢查 hello 的 hello Azure 強化監視功能延伸模組的輸出。

  a.  執行 `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **預期的結果**：傳回效能計數器的清單。 hello 檔案不能空白。

 b. 執行 `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **預期的結果**： 傳回 hello 錯誤所在的同一行**無**，例如**3; 組態。錯誤;，則為 0，則為 0;無、 0、 1456416792、 tst servercs;**

  c. 執行 `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **預期的結果**：傳回為空白或不存在。

如果 hello 上述檢查未成功，執行這些額外的檢查：

1.  請確定該 hello waagent 已安裝並啟用。

  a.  執行 `sudo ls -al /var/lib/waagent/`

      **預期的結果**： 列出 hello hello waagent 目錄內容。

  b.  執行 `ps -ax | grep waagent`

   **預期的結果**：顯示類似下列一個項目：`python /usr/sbin/waagent -daemon`

2. 請確定該 hello 安裝並啟用 Linux 診斷延伸模組。

  a.  執行 `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`

   **預期的結果**： 列出 hello hello Linux 診斷延伸模組目錄內容。

 b. 執行 `ps -ax | grep diagnostic`

   **預期的結果**：顯示類似下列一個項目：`python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   請確定該 hello Azure 強化監視功能延伸模組是已安裝且正在執行。

  a.  執行 `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`

    **預期的結果**： 列出 hello hello Azure 強化監視功能延伸模組目錄內容。

  b. 執行 `ps -ax | grep AzureEnhanced`

     **預期的結果**：顯示類似下列一個項目：`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. SAP 附註所述安裝 SAP Host Agent [1031096]，並檢查 hello 輸出`saposcol`。

  a.  執行 `/usr/sap/hostctrl/exe/saposcol -d`

  b.  執行 `dump ccm`

  c.  檢查是否 hello **Virtualization_Configuration\Enhanced 監視存取**度量是**true**。

如果您已安裝 SAP NetWeaver ABAP 應用程式伺服器，請開啟交易 ST06，並檢查是否已啟用增強監視。

如果任何這些檢查失敗，而且如需如何 tooredeploy hello 擴充功能的詳細資訊，請參閱[疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構][deployment-guide-5.3]。

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>健全狀況檢查 hello Azure 監視基礎結構設定
如果部分監視資料的 hello 沒有指示地正確傳遞 hello 測試中所述[Azure 強化監視功能適用於 SAP 的整備檢查][deployment-guide-5.1]中執行的 hello `Test-AzureRmVMAEMExtension` cmdlet toocheck是否 hello Azure 監視基礎結構和 hello SAP 的監視功能延伸模組已正確設定。

1.  確定您已安裝 hello hello Azure PowerShell cmdlet，最新版本中所述[部署 Azure PowerShell cmdlet][deployment-guide-4.1]。
2.  執行下列 PowerShell cmdlet 的 hello。 如需可用環境的清單，執行 hello cmdlet `Get-AzureRmEnvironment`。 toouse 公用 Azure，選取 hello **AzureCloud**環境。 若為中國的 Azure，請選取 **AzureChinaCloud**。
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  輸入您的帳戶資料，並找出 hello Azure 虛擬機器。

  ![SAP 特定 Azure Cmdlet Test-VMConfigForSAP_GUI 的輸入頁面][deployment-guide-figure-1200]

4. 您選取 hello 指令碼測試 hello hello 虛擬機器設定。

  ![順利完成測試的 hello Azure 監視基礎結構，適用於 SAP 的輸出][deployment-guide-figure-1300]

確定每個健康狀態檢查的結果都 [OK]。 如果部分檢查不會顯示**確定**，執行 hello 更新指令程式中所述[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。 請稍候 15 分鐘，並說明重複 hello 檢查[Azure 強化監視功能適用於 SAP 的整備檢查][ deployment-guide-5.1]和[的 Azure 監視基礎結構組態健全狀況檢查][deployment-guide-5.2]. 如果 hello 檢查仍指出某些或全部計數器有問題，請參閱[疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構][deployment-guide-5.3]。

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>疑難排解 hello 適用於 SAP 的 Azure 監視基礎結構

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] 完全未顯示 Azure 效能計數器
hello AzureEnhancedMonitoring Windows 服務會收集在 Azure 中的效能度量。 如果 hello 服務的安裝不正確或不在 VM 中執行，您可以收集效能度量。

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>hello Azure 強化監視功能延伸模組的安裝目錄是 hello 的空的

###### <a name="issue"></a>問題
hello 安裝目錄 c:\\封裝\\外掛程式\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;版本 >\\drop 是空白。

###### <a name="solution"></a>方案
未安裝 hello 延伸模組。 判斷這是否為 Proxy 問題 (如先前所述)。 您可能需要 toorestart hello 機器或重新執行的 hello`Set-AzureRmVMAEMExtension`組態指令碼。

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Azure Enhanced Monitoring 的服務不存在

###### <a name="issue"></a>問題
hello AzureEnhancedMonitoring Windows 服務不存在。

Azperflib.exe 輸出會擲回錯誤︰

![執行 azperflib.exe 指出適用於 SAP 的 Azure 強化監視功能延伸模組的 hello 的 hello 服務未執行][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>方案
如果 hello 服務不存在，hello Azure 強化監視功能延伸模組適用於 SAP 尚未安裝正確。 使用您的部署案例中所述的 hello 步驟來重新部署 hello 延伸[在 Azure 中 SAP 的 Vm 部署案例][deployment-guide-3]。

在一小時後部署 hello 延伸之後，再次檢查 hello Azure VM 中是否提供 hello Azure 效能計數器。

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Azure 強化監視功能的服務存在，但失敗 toostart

###### <a name="issue"></a>問題
hello AzureEnhancedMonitoring Windows 服務存在並已啟用，但失敗 toostart。 如需詳細資訊，請檢查 hello 應用程式事件記錄檔。

###### <a name="solution"></a>方案
hello 設定不正確。 中所述，重新啟動監視 hello VM 延伸模組的 hello[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]。

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] 遺失部分 Azure 效能計數器
hello AzureEnhancedMonitoring Windows 服務會收集在 Azure 中的效能度量。 hello 服務從多個來源取得資料。 有些組態資料是在本機收集，而有些效能計量是從 Azure 診斷讀取而來。 儲存體計數器是從您登入 hello 儲存體訂用帳戶層級來使用。

如果使用 SAP Note 疑難排解[1999351]未解決 hello 問題，請重新執行 hello`Set-AzureRmVMAEMExtension`組態指令碼。 因為儲存體分析或診斷計數器可能不在啟用後，立即建立，您可能需要一小時 toowait。 如果 hello 問題持續發生，請開啟 hello 元件 BC OP-NT AZR 適用於 Windows 或 BC-OP-LNX-AZR Linux 虛擬機器上的 SAP 客戶支援訊息。

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] 完全未顯示 Azure 效能計數器
Daemon 會收集在 Azure 中的效能計量。 如果 hello 服務精靈未執行，您可以收集效能度量。

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>hello Azure 強化監視功能延伸模組的安裝目錄是 hello 的空的

###### <a name="issue"></a>問題
hello 目錄\\var\\lib\\waagent\\沒有 hello Azure 強化監視功能延伸模組的子目錄。

###### <a name="solution"></a>方案
未安裝 hello 延伸模組。 判斷這是否為 Proxy 問題 (如先前所述)。 您可能需要 toorestart hello 電腦及 （或） 重新執行的 hello`Set-AzureRmVMAEMExtension`組態指令碼。

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] 遺失部分 Azure 效能計數器
Azure 中的效能計量是由 Daemon 收集，而 Daemon 會從數個來源取得資料。 有些組態資料是在本機收集，而有些效能計量是從 Azure 診斷讀取而來。 儲存體計數器來自儲存體訂用帳戶中的 hello 記錄檔。

如需完整且最新的已知問題清單，請參閱 SAP Note [1999351]，其中包含適用於 Enhanced Azure Monitoring for SAP 的其他疑難排解資訊。

如果使用 SAP Note 疑難排解[1999351]並未解決 hello 問題，請重新執行 hello`Set-AzureRmVMAEMExtension`組態指令碼中所述[設定 hello Azure 強化監視功能延伸模組適用於 SAP][deployment-guide-4.5]. 因為儲存體分析或診斷計數器可能不在啟用後，立即建立，您可能必須 toowait 一小時。 如果 hello 問題持續發生，請開啟 hello 元件 BC OP-NT AZR 適用於 Windows 或 BC-OP-LNX-AZR Linux 虛擬機器上的 SAP 客戶支援訊息。
