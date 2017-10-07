---
title: "aaaSAP NetWeaver on Azure Vm – 的 DBMS 部署指南 |Microsoft 文件"
description: "Azure 虛擬機器 (VM) 上的 SAP NetWeaver - DBMS 部署指南"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>Azure Windows 虛擬機器 (VM) 上的 SAP NetWeaver - DBMS 部署指南
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

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md 
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md 
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
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
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
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

本指南是 hello 文件中實作及部署 Microsoft Azure 上的 hello SAP 軟體的一部分。 之後，再閱讀本指南，請閱讀 hello[計劃與實作指南][planning-guide]。 本文件涵蓋 hello 部署各種關聯式資料庫管理系統 (RDBMS) 和使用 hello Azure 基礎結構即服務 (IaaS) 功能搭配 Microsoft Azure 虛擬機器 (Vm) 上的 SAP 相關的產品。

指定平台 hello 紙張補充 hello SAP 安裝文件集和 SAP 附註 」 包含 hello 安裝和部署上的 SAP 軟體的主要資源

## <a name="general-considerations"></a>一般考量
本章將說明在 Azure VM 中執行 SAP 相關 DBMS 系統的考量。 有幾個參考 toospecific DBMS 系統在本章中。 改為 hello 特定 DBMS 系統是由處理本文件，會在本章之後。

### <a name="definitions-upfront"></a>預先定義
在 hello 文件中，我們將使用下列詞彙的 hello:

* IaaS：基礎結構即服務。
* PaaS：平台即服務。
* SaaS：軟體即服務。
* SAP 元件︰個別的 SAP 應用程式，例如 ECC、BW、Solution Manager 或 EP。  SAP 元件可以傳統 ABAP 或 Java 技術為基礎，或以非 NetWeaver 應用程式 (例如商務物件) 為基礎。
* SAP 環境： 一或多個 SAP 元件以邏輯方式分組 tooperform 商務功能，例如開發、 QAS、 訓練、 DR 或生產環境。
* SAP 版圖： 這是指 toohello 整個 SAP 資產中客戶的 IT 環境。 hello SAP 版圖包括所有生產和非生產環境。
* SAP 系統： hello 組合的 DBMS 層和應用程式層，例如 SAP ERP 開發系統、 SAP BW 測試系統、 SAP CRM 生產系統等。在 Azure 中不支援的部署 toodivide 這些內部部署與 Azure 之間的兩個層級。 這表示 SAP 系統可以在內部部署或在 Azure 部署。 不過，您可以部署在 Azure 或內部部署 SAP 版圖的 hello 不同系統。 例如，您可以部署 hello SAP CRM 開發和測試系統在 Azure 中的，但是 hello SAP CRM 生產系統在內部。
* 僅限雲端部署： 部署其中 hello Azure 訂用帳戶未連線透過網站的站台或 ExpressRoute 連線 toohello 內部部署網路基礎結構。 在一般 Azure 文件中，這類部署也會描述為「僅限雲端」的部署。 採用這種方法部署的虛擬機器透過 hello 網際網路存取，而且公用網際網路端點指派 toohello Vm 在 Azure 中。 hello 內部部署 Active Directory (AD) 和 DNS 未延伸 tooAzure 在這些類型的部署。 因此 hello Vm 不屬於 hello 內部部署 Active Directory。 附註：僅限雲端的部署在本文中定義為在 Azure 中以獨佔方式執行的完整 SAP 架構，不會將 Active Directory 或名稱解析從內部部署擴充到公用雲端。 針對實際執行 SAP 系統或 SAP STMS 或其他內部部署資源需要 toobe 裝載在 Azure 與位於內部部署資源上的 SAP 系統之間使用的組態不支援僅限雲端的組態。
* 跨單位： 說明的案例，當 Vm 是已部署的 tooan Azure 訂用帳戶具有站台間，多站台或 ExpressRoute hello 在內部部署資料中心與 Azure 之間的連線能力。 在一般 Azure 文件中，這類部署也會描述為跨單位案例。 hello hello 連線的原因是 tooextend 在內部部署網域、 在內部部署 Active Directory 和內部部署 DNS 至 Azure。 hello 內部橫向是擴充的 toohello hello 訂用帳戶的 Azure 資產。 透過這樣延伸，hello Vm 可以是 hello 在內部部署網域的一部分。 Hello 在內部部署網域的網域使用者可以存取 hello 伺服器，並且可以執行服務那些 Vm （例如 DBMS 服務）。 您可以在內部部署的 VM 與 Azure 中部署的 VM 之間進行通訊與名稱解析。 我們預期此 toobe hello 最常見的案例部署在 Azure 上的 SAP 資產。 如需詳細資訊，請參閱[這篇文章][vpn-gateway-cross-premises-options]和[這個主題][vpn-gateway-site-to-site-create]。

> [!NOTE]
> SAP 生產系統支援跨單位部署 SAP 系統，其中執行 SAP 系統的 Azure 虛擬機器是內部部署網域的成員。 支援跨單位組態，以便將部分或完整的 SAP 架構部署到 Azure。 即使在 Azure 中執行 hello 完整的 SAP 環境，則需要具有這些 Vm 屬於內部部署網域和廣告。 Hello 文件的先前版本中我們剛才討論過混合式 IT 案例，其中 hello 詞彙 '混合' 已進行 root 破解 hello 事實會在內部部署與 Azure 之間的跨單位連線。 在此情況下 '混合' 也表示，在 Azure 中的 hello Vm 屬於 hello 內部部署 Active Directory。
>
>

有些 Microsoft 文件在描述跨單位案例時稍有不同，特別是針對 DBMS HA 組態。 在 hello 的 hello SAP 案例相關的文件、 hello 跨內部部署案例只分布 toohaving 站對站或私人 (ExpressRoute) 連線和 toohello 事實 hello SAP 版圖分散在內部部署和 Azure。

### <a name="resources"></a>資源
hello 下列指南可供 Azure 上 SAP 部署的 hello 主題：

* [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南][planning-guide]
* [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 部署指南][deployment-guide]
* [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - DBMS 部署指南 (本文件)][dbms-guide]
* [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 高可用性部署指南][ha-guide]

Azure 上的 SAP 相關的 toohello 主題 hello 遵循 SAP 附註︰

| 附註編號 | 課程名稱 |
| --- | --- |
| [1928533] |Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型 |
| [2015553] |Microsoft Azure 上的 SAP：支援的必要條件 |
| [1999351] |疑難排解適用於 SAP 且已強化的 Azure 監視功能 |
| [2178632] |Microsoft Azure 上的 SAP 主要監視度量 |
| [1409604] |Windows 上的虛擬化︰增強型監視功能 |
| [2191498] |Linux 和 Azure 上的 SAP：增強型監視功能 |
| [2039619] |使用 Microsoft Azure 的 SAP 應用程式 hello Oracle 資料庫： 支援的產品和版本 |
| [2233094] |DB6︰Azure 上使用 IBM DB2 for Linux, UNIX, and Windows 的應用程式 - 其他資訊 |
| [2243692] |Microsoft Azure (IaaS) VM 上的 Linux：SAP 授權問題 |
| [1984787] |SUSE LINUX Enterprise Server 12：安裝注意事項 |
| [2002167] |Red Hat Enterprise Linux 7.x：安裝和升級 |

也請閱讀 hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) for Linux 包含所有 SAP 附註。

您應該使用 hello Microsoft Azure 架構與如何部署和操作 Microsoft Azure 虛擬機器的相關知識。 您可以在以下位置找到更多資訊：<https://azure.microsoft.com/documentation/>

> [!NOTE]
> 我們**不**討論 Microsoft Azure 平台為 hello Microsoft Azure 平台的服務 (PaaS)。 這份文件會說明如何執行資料庫管理系統 (DBMS) 在 Microsoft Azure 虛擬機器 (IaaS)，就像您會在內部部署環境中執行 hello DBMS。 這兩個產品之間所提供的資料庫性能與功能差異極大，不應混用彼此。 另請參閱︰<https://azure.microsoft.com/services/sql-database/>
>
>

因為我們討論的 IaaS，一般而言 hello Windows、 Linux 和 DBMS 的安裝和組態會基本上 hello 與任何虛擬機器或裸機機器會與內部部署安裝相同。 不過，有一些架構和系統管理實作決策會與使用 IaaS 時的不同。 本文件的 hello 目的是 tooexplain hello 特定架構和系統管理差異，您必須準備使用 IaaS 時。

一般情況下，hello 的本文將討論的差異層面大致如下：

* 規劃的 SAP 系統 tooensure hello 正確 VM/VHD 配置您擁有 hello 適當的資料檔案配置，並且用於您的工作負載時可以達成足夠的 IOPS。
* 使用 IaaS 時的網路功能考量。
* 特定的資料庫功能 toouse 順序 toooptimize hello 資料庫配置中。
* IaaS 的備份和還原考量。
* 使用不同類型的映像進行部署。
* Azure IaaS 中的高可用性。

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>RDBMS 部署結構
為了遵循這一章，就什麼出示中必要 toounderstand[這][ deployment-guide-3] hello 一章[部署指南 》][deployment-guide]。 相關知識 hello 不同的 VM 系列，其差異和 Azure 標準和高階儲存體的差異應該了解並已知再讀取這一章。

2015 年 3 月中，直到 Azure Vhd 包含作業系統的有限的 too127 GB 的大小。 這項限制在 2015 年 3 月解除 (如需詳細資訊，請參閱 <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/>)。 從該處 Vhd 上包含 hello 作業系統可以有 hello 相同的大小為任何其他 VHD。 不過，我們仍然偏好 hello 作業系統、 DBMS 和最終 SAP 二進位檔所在位置 hello 資料庫檔案不同的部署結構。 因此，我們預期 hello 基底 VM （或 VHD） 與 hello 作業系統一起安裝，資料庫管理系統可執行檔和 SAP 執行檔，都在 Azure 虛擬機器中執行的 SAP 系統。 hello DBMS 資料和記錄檔會儲存在 Azure 儲存體 （Standard 或 Premium 儲存體） 單獨的 VHD 檔案，並在附加為邏輯磁碟 toohello 原始 Azure 作業系統映像 VM。

取決於有 （例如藉由使用 hello DS 系列或 GS 系列 Vm） 利用 Azure 標準或高階儲存體是 Azure 中記載的其他配額[這裡][virtual-machines-sizes]。 當計劃 Azure Vhd，您將需要 toofind hello 取得最佳平衡 hello 配額 hello 下列：

* hello 資料檔案數目。
* hello 包含 hello 檔案的 Vhd 數目。
* hello 單一 vhd 的 IOPS 配額。
* 每個 VHD 的 hello 資料輸送量。
* 每個 VM 大小的額外 Vhd 可能的 hello 數目。
* hello 整體儲存體輸送量 VM 可以提供。

Azure 將針對每個 VHD 磁碟機強制執行 IOPS 配額。 這些配額與 Azure 標準儲存體和進階儲存體上裝載的 VHD 不同。 I/O 延遲也會提供更好的 I/O 延遲因素的進階儲存體 hello 兩個儲存體類型之間非常不同。 每個 hello 不同 VM 類型具有有限的 Vhd，您都可以 tooattach 時。 另一個限制是只有特定的 VM 類型可以利用 Azure 進階儲存體。 這表示使用某種 VM 類型的 hello 決策可能不只重點 hello CPU 和記憶體需求也的 hello IOPS、 延遲和磁碟輸送量需求通常與 hello Vhd 數目縮放或 hello 高階儲存體磁碟類型。 特別是在進階儲存體 hello 之 vhd 的大小也可能會取決於 hello IOPS 及輸送量需要 toobe 達成每個 VHD 數目。

hello 事實的 hello 整體 IOPS 速率、 hello 掛接的 Vhd 數目和 hello 的 hello VM 因素環環相扣，大小可能會導致不同於其內部部署 SAP 系統 toobe 的 Azure 組態。 每個 LUN 的 hello IOPS 限制是內部部署中通常可以設定。 而與 Azure 儲存體這些限制是固定的或如高階儲存體相依 hello 磁碟類型上所示。 因此，與內部部署我們看到客戶組態的資料庫伺服器使用許多不同的磁碟區的特殊的可執行檔，如 SAP 和 DBMS 或特殊磁碟區來存放暫存資料庫或資料表空間 hello。 這類內部部署系統時移動的 tooAzure 時，可能會浪費 tooa IOPS 頻寬所浪費的可執行檔或資料庫不會執行任何或不大量 IOPS 的 VHD。 因此，在 Azure Vm 中建議盡可能該 hello DBMS 和 SAP 執行檔安裝在 hello 作業系統磁碟。

hello hello 資料庫檔案和記錄檔以及 hello 型別使用，Azure 儲存體的位置應該定義 IOPS、 延遲和輸送量需求。 在訂單 toohave 足夠的 IOPS 供 hello 交易記錄檔，您可能會強制的 tooleverage hello 交易記錄檔的多個 Vhd 檔案，或使用較大的進階儲存體磁碟。 在這種情況下其中一項只會建置軟體會 RAID （例如 Windows 儲存體集區的 Windows 或 MDADM 和適用於 Linux LVM （邏輯磁碟區管理員）） 以 hello Vhd hello 交易記錄檔。

- - -
> ![Windows][Logo_Windows] Windows
>
> 在 Azure VM 的 D:\ 磁碟機是由某些本機的磁碟備份 hello Azure 計算節點非持續性磁碟機。 由於非持續性，這表示 hello VM 重新開機時，在 hello D:\ 磁碟機上任何所做的變更 toohello 內容都會遺失。 「任何變更」的意思是已儲存的檔案、已建立的目錄、已安裝的應用程式等。
>
> ![Linux][Logo_Linux] Linux
>
> Linux 的 Azure Vm 中自動掛接磁碟機時 /mnt/resource 這是本機磁碟的 hello Azure 計算節點上支援非持續性磁碟機。 由於非持續性，這表示 hello VM 重新開機時，在 /mnt/resource 任何所做的變更 toocontent 都會遺失。 「任何變更」的意思是已儲存的檔案、已建立的目錄、已安裝的應用程式等。
>
>

- - -
相依於 hello Azure VM 系列，hello hello 上的本機磁碟計算節點顯示不同效能可以像分類：

* A0-A7︰非常有限的效能。 無法使用 Windows 分頁檔以外的項目
* A8-A11︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量
* D 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量
* DS 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量
* G 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量
* GS 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量

上述陳述式會套用 toohello 經過驗證和 SAP 的 VM 類型。 絕佳的 IOPS 及輸送量與 hello VM 系列部分的 DBMS 功能，例如 tempdb 或暫存資料表空間限定的運用。

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>VM 和 VHD 的快取
當我們建立透過 hello 入口網站，或當掛接已上傳的 Vhd tooVMs 那些磁碟 /vhd 時，我們可以選擇是否要快取 hello VM 與 Azure 儲存體中那些 Vhd 間的 hello I/O 流量。 Azure 標準和進階儲存體會針對這種快取類型使用兩種不同技術。 在這兩種情況下 hello 快取本身會在磁碟支援上使用相同的磁碟機的 hello hello 暫存磁碟 (Windows 上的 D:\) 或 /mnt/resource Linux 上的 hello VM。

Azure 標準儲存體 hello 可能快取類型為：

* 無快取
* 讀取快取
* 讀取和寫入快取

順序 tooget 一致且具有決定性效能，您應該設定 hello 快取 Azure 標準儲存體上的所有 Vhd 包含**DBMS 相關資料檔案、 記錄檔和資料表空間 too'NONE'**。 hello 快取的 hello VM 仍可使用 hello 預設值。

Azure 高階儲存體 hello 下列快取的選項有：

* 無快取
* 讀取快取

建議 Azure 高階儲存體是 tooleverage**讀取資料檔的快取**的 hello SAP 資料庫，並選擇**hello VHD(s) 記錄檔的無快取**。

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>軟體 RAID
所述之已上方，您需要 IOPS 的 toobalance hello 數目所需 hello 資料庫檔案，您可以設定的 Vhd 和 hello hello 數目之間的最大 IOPS Azure VM 將會提供每個 VHD 或 Premium 儲存體磁碟類型。 最簡單的方法以載入到 Vhd 的 IOPS 的 hello toodeal 位於 toobuild 軟體 RAID hello 不同 Vhd。 然後置於的 hello LUN 劃分出 hello 軟體 RAID 的 hello SAP DBMS 的資料檔案數目。 相依於 hello 需求，您可能會想 tooconsider hello 使用量的進階儲存體以及自兩個 hello 三個不同的進階儲存體磁碟提供更高版本比標準儲存體為基礎的 Vhd 的 IOPS 配額。 除了 hello 重大 I/O 延遲 Azure 高階儲存體所提供的更好。

這同樣適不同 DBMS 系統 hello toohello 交易記錄的檔。 具有大量它們只要加入更多 Tlog 檔案不會協助因為 hello DBMS 系統一次只能寫入一個 hello 檔案。 如果需要更高 IOPS 速率比單一標準儲存體為基礎 VHD 可以傳遞，您可以等量分割至多個標準儲存體的 Vhd 或您可以使用較大的進階儲存體磁碟類型，高 IOPS 速率超過也提供低延遲因素 hello 寫入我 /Os 到 hello 交易記錄檔。

以下是在 Azure 部署中使用優先軟體 RAID 時所遇到的情況：

* 交易記錄/重做記錄需要的 IOPS 數目比 Azure 針對單一 VHD 所提供的還多。 如前所述，解決此問題的方式是在多個 VHD上使用軟體 RAID 來建置 LUN。
* I/O 工作負載透過 hello 不同資料檔案的分配 hello SAP 資料庫。 在此情況下一個可能會遇到一個資料檔，而是會經常遇到 hello 配額。 而其他資料檔案甚至不會進行關閉 toohello 單一 vhd 的 IOPS 配額。 在這種情況下 hello 最簡單的解決方案是一個 toobuild 使用軟體 RAID 的多個 Vhd 上的 LUN。
* 您不知道哪些 hello 確切的 I/O 工作負載每個資料檔案且只大致了解什麼 hello 整體 IOPS hello DBMS 工作負載會。 最簡單的 toodo 是軟體的的 toobuild hello 與一個 LUN 協助 RAID。 這個 LUN 背後的多個 Vhd 的配額 hello 總和然後應該滿足 hello 已知 IOPS 速率。

- - -
> ![Windows][Logo_Windows] Windows
>
> 最好使用 Windows Server 2012 或更高的儲存空間，因為它比舊版 Windows 的 Windows 等量更有效率。 請注意，您可能需要 toocreate hello Windows 儲存集區和儲存空間的 PowerShell 命令時使用 Windows Server 2012 做為作業系統。 hello PowerShell 命令可以在這裡找到<https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> 只有 MDADM 和 LVM （邏輯磁碟區管理員） 是支援的 toobuild RAID Linux 上的軟體。 如需詳細資訊，請閱讀下列文件的 hello:
>
> * [在 Linux 上設定軟體 RAID][virtual-machines-linux-configure-raid] (適用於 MDADM)
> * [在 Azure 中的 Linux VM 上設定 LVM][virtual-machines-linux-configure-lvm]
>
>

- - -
是運用 VM 系列通常是無法 toowork 與 Azure 高階儲存體的考量：

* 要求 I/O 延遲關閉 toowhat SAN/NAS 裝置傳送。
* 比 Azure 標準儲存體可傳遞的 I/O 延遲更好的因素需求。
* 對於可根據特定 VM 類型使用多個標準儲存體 VHD 來達成的每個 VM 提供更高的 IOPS。

因為 hello 基礎 Azure 儲存體複寫每個 VHD tooat 至少三個儲存體節點簡單的 RAID 0 等量配置可用。 沒有任何需要 tooimplement RAID5 或 RAID1。

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Microsoft Azure 儲存體
Microsoft Azure 儲存體會將 hello （含 OS) 的基底 VM 和 Vhd 或 Blob tooat 至少 3 不同儲存體節點。 建立儲存體帳戶時，有一個保護選項，如下所示：

![針對 Azure 儲存體帳戶啟用異地複寫][dbms-guide-figure-100]

Azure 儲存體本機複寫 （本機備援） 可提供少數客戶可以放心 toodeploy tooinfrastructure 失敗原因會遺失資料的保護層級。 如上所示搭配第五個的其中一個 hello 變化前三個有 4 個不同的選項。 仔細查看我們區分它們的方式︰

* **進階本地備援儲存體 (LRS)**：針對執行需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」提供高效能、低延遲的磁碟支援。 有 3 個複本的 hello hello 資料相同的 Azure 地區的 Azure 資料中心。 hello 複本會以不同的容錯和升級網域中 (如概念，請參閱[這][ planning-guide-3.2]章節 hello[規劃指南 》][planning-guide])。 發生或從到期 tooa 存放裝置節點失敗或磁碟失敗的服務傳送的 hello 資料的複本，會自動產生新的複本。
* **本機備援儲存體 (LRS)**： 在此情況下有 3 個複本的 hello hello 資料相同的 Azure 地區的 Azure 資料中心。 hello 複本會以不同的容錯和升級網域中 (如概念，請參閱[這][ planning-guide-3.2]章節 hello[規劃指南 》][planning-guide])。 發生或從到期 tooa 存放裝置節點失敗或磁碟失敗的服務傳送的 hello 資料的複本，會自動產生新的複本。
* **地理備援儲存體 (GRS)**： 在此情況下沒有將摘要額外的非同步複寫 3 個複本的大部分 hello 中的案例中的另一個 Azure 區域中的 hello 資料 hello 相同的地理區域 （例如北歐和美國西部歐洲）。 這將會產生 3 個額外的複本，因此總共有 6 個複本。 這一種是 「 hello 地理複寫的 Azure 區域中的 hello 資料，用於讀取 （讀取權限的地理備援） 的用途。
* **區域備援儲存體 (ZRS)**： 在此情況下的資料保留在 hello hello 3 複本 hello 相同 Azure 區域。 中所述[這][ planning-guide-3.1] hello 一章[規劃指南 》] [ planning-guide] Azure 地區可以非常接近的數字的資料中心。 LRS hello 案例 hello 複本會分散 hello 不同的資料中心，讓一個 Azure 區域。

如需詳細資訊，請參閱[這裡][storage-redundancy]。

> [!NOTE]
> 不建議的 DBMS 部署 hello 的地理備援儲存體的使用方式
>
> Azure 儲存體異地複寫是非同步的。 單一 VM 未同步處理在鎖定步驟中的個別 Vhd 掛接 tooa 複寫。 因此，它不是適合 tooreplicate DBMS 檔案分散至不同的 Vhd，或是針對根據多個 Vhd 的 RAID 軟體部署。 DBMS 軟體需要 hello 永續性磁碟儲存體精確地同步處理跨不同的 Lun 和基礎磁碟/Vhd/主軸。 DBMS 軟體使用各種機制 toosequence IO 寫入活動，DBMS 將會報告 hello 磁碟儲存體的 hello 複寫目標已損毀，如果這些因甚至幾毫秒。 因此如果您真的想資料庫組態對資料庫延展到多個 Vhd 進行地理複寫，這類複寫需要 toobe 執行使用資料庫方法和功能。 其中一個不應依賴 Azure 儲存體地理複寫 tooperform 這項作業。
>
> hello 問題是使用範例系統最簡單的 tooexplain。 例如，假設您已上傳至 Azure，其具有 8 個含有 hello DBMS 的資料檔案，以及一個 VHD 包含 hello 交易記錄檔將 SAP 系統。 這些 9 Vhd 的每個將有一致的方式根據 toohello DBMS，撰寫 toothem 是否 hello 資料寫入 toohello 資料或交易記錄檔的資料。
>
> 順序 tooproperly 地理複寫 hello 資料及維護一致的資料庫映像、 hello 內容 9 個 vhd 會有 toobe hello 順序 hello I/O 作業中進行地理複寫針對執行 hello 九個不同的 Vhd。 不過，Azure 儲存體地理複寫不允許 toodeclare Vhd 之間的相依性。 這表示這些 9 個不同 Vhd 中的 hello 內容的其他相關的 tooeach 而且 hello 資料變更時，都是一致只複寫 hello 順序 hello I/O 作業中發生的 hello 事實不知道 Microsoft Azure 儲存體地理複寫跨所有 hello 9 Vhd。
>
> 除了過高，在 hello 案例中的 hello 進行地理複寫映像不會提供一致的資料庫映像，也沒有可造成嚴重的地理備援儲存體和一同顯示對效能帶來負面影響的機會會影響效能。 總之，請勿針對 DBMS 類型的工作負載使用這個類型的儲存體備援。
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>將 VHD 對應至 Azure 虛擬機器服務儲存體帳戶
Azure 儲存體帳戶不只是一個系統管理的建構，而且還是限制的緣由。 而 hello 限制會隨著談論 Azure 標準儲存體帳戶或 Azure 高階儲存體帳戶。 列出 hello 確切功能和限制[這裡][storage-scalability-targets]

因此您很重要的 toonote Azure 標準儲存體上每個儲存體帳戶的 IOPS hello 沒有限制 (中的資料列包含 '總要求率' [hello 文章][storage-scalability-targets])。 此外，每個 Azure 訂用帳戶的「儲存體帳戶」初始限制為 100 個 (自 2015 年 7 月起)。 因此，建議您使用多個儲存體帳戶時使用 Azure 標準儲存體之間 toobalance IOPS 的 Vm。 另一方面，單一 VM 最好盡可能使用一個儲存體帳戶。 因此，如果我們談到 DBMS 部署，其中每個裝載於 Azure 標準儲存體的 VHD 會到達其配額限制時，您應該只針對每個使用 Azure 標準儲存體的 Azure 儲存體帳戶部署 30-40 個 VHD。 上 hello 另一方面，如果您利用 Azure 高階儲存體，並想 toostore 大型資料庫的磁碟區，您可能會根據 IOPS 來沒問題。 但是，Azure 進階儲存體帳戶在資料磁碟區方面會比 Azure 標準儲存體帳戶更嚴格。 如此一來，您只可以部署有限的數目的 Azure 高階儲存體帳戶內的 Vhd 才按下 hello 資料磁碟區限制。 在 hello 結束考慮為 「 虛擬 SAN 」 的 Azure 儲存體帳戶，具有有限的功能在 IOPS 及/或容量。 如此一來，hello 工作仍會留，如同內部部署，透過 hello 不同 「 虛構 SAN 裝置' hello 不同 SAP 系統的 Vhd 或 Azure 儲存體帳戶的 hello toodefine hello 版面配置。

Azure 不建議從不同的儲存體帳戶 tooa toopresent 儲存體的標準儲存體盡可能單一 VM。

而使用 hello DS 或 GS 系列的 Azure Vm，則很可能 toomount Vhd 從 Azure 標準儲存體帳戶和 Premium 儲存體帳戶。 使用案例，例如寫入到標準儲存體的備份會備份 Vhd 而 DBMS 的資料，並在高階儲存體上的記錄檔有 toomind 無法運用這類異質儲存區的位置。

根據客戶的部署及測試大約 30 too40 包含資料庫資料檔案和記錄檔的 Vhd 可以佈建單一 Azure 標準儲存體帳戶與可接受的效能。 如先前所述，Azure 高階儲存體帳戶的 hello 限制是它能容納可能 toobe hello 資料容量和不 IOPS。

為透過 SAN 裝置在內部，共用所需的某些監視順序 tooeventually 中偵測到 Azure 儲存體帳戶上的瓶頸。 hello Azure Monitoring Extension for SAP 和 hello Azure 入口網站是可使用的 toodetect 的工具忙碌未能提供最佳 IO 效能的 Azure 儲存體帳戶。  如果已偵測到這種情況下，建議 toomove 忙碌 Vm tooanother Azure 儲存體帳戶。 請參閱 toohello[部署指南 》] [ deployment-guide]如如何 tooactivate hello SAP 主機監視功能的詳細資訊。

您可以在下列網址中，找到另一篇摘要說明「Azure 標準儲存體」和「Azure 標準儲存體帳戶」最佳做法的文章：<https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>移動 Azure 標準儲存體 tooAzure 高階儲存體從部署 DBMS Vm
我們會遇到一段的案例中，您為客戶 toomove 從 Azure 標準儲存體 VM 已部署到 Azure 進階儲存體。 這是不可能沒有實際移動 hello 資料。 有數種方式 tooachieve hello 目標：

* 您只需將所有的 VHD、基底 VHD 以及資料 VHD 複製到新的 Azure 進階儲存體帳戶。 通常您已選擇 hello Vhd 數目在 Azure 標準儲存體不是因為您所需的 hello 資料磁碟區的 hello 事實。 但您需要許多 Vhd，因為 hello IOPS。 既然您移動 tooAzure 高階儲存體，您無法搭配的方式較少的 Vhd tooachieve hello 一些 IOPS 輸送量。 指定您需支付 hello Azure 標準儲存體中使用的資料和非 hello 名義上的磁碟大小的 hello 事實，hello Vhd 數目未不真的很重要方面成本。 不過，Azure 高階儲存體，您將支付 hello 名義上的磁碟大小。 因此，大部分的 hello 客戶嘗試 tookeep hello Azure Vhd 數目高階儲存體中 hello 數字所需的 tooachieve hello IOPS 輸送量必要。 因此，大部分的客戶決定針對簡單 1:1 的 hello 方式複製。
* 如果尚未掛接，您要掛接單一 VHD，其中可包含 SAP 資料庫的資料庫備份。 Hello 備份後卸載所有 Vhd 包括 hello VHD 包含 hello 備份和複製 hello 基底 VHD 和 hello 與 hello 備份的 VHD 到 Azure 進階儲存體帳戶。 然後，您會部署的 hello hello 基底 VHD 和掛接 hello VHD hello 備份為基礎的 VM。 現在您可以建立其他空高階儲存體磁碟 hello VM 所使用的 toorestore hello 資料庫。 這是假設該 hello DBMS 可讓您 toochange 路徑 toohello 資料和記錄檔 hello 還原程序的一部分。
* 另一個可能性是一種 hello 先前程序，其中只需要將 hello 備份 VHD 複製到 Azure 進階儲存體，並將它附加對新部署和安裝的 VM。
* hello 第四個可能性您可以選擇當您需要資料庫的資料檔案的 toochange hello 數目。 在這種情況下，您會使用匯出/匯入來執行 SAP 同質性系統複製。 放入與匯出到複製到 Azure 進階儲存體帳戶的 VHD 檔案，並將它附加 tooa VM，您會使用 toorun hello 匯入處理程序。 客戶在主要是要 toodecrease hello 數目的資料檔案時，才使用這種可能性。

### <a name="deployment-of-vms-for-sap-in-azure"></a>在 Azure 中部署適用於 SAP 的 VM
Microsoft Azure 提供的多種 toodeploy Vm 和相關聯的磁碟。 因此就非常重要的 toounderstand hello 差異因為 hello Vm 的準備工作可能會與不同部署的 hello 方式而定。 一般情況下，我們探討 hello hello 後面章節所述的案例。

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>部署的 hello Azure Marketplace 中的 VM
您喜歡 tootake Microsoft 或第 3 個合作對象提供的映像 hello Azure Marketplace toodeploy 從您的 VM。 部署在 Azure VM 之後，請依照 hello 相同的指導方針和工具 tooinstall hello SAP 軟體，在 VM 內像您一樣在內部部署環境中。 安裝 Azure VM hello hello SAP 軟體，SAP 和 Microsoft 建議 tooupload hello SAP 安裝媒體或中與儲存 Azure Vhd toocreate Azure VM 以 「 檔案伺服器 」 包含所有 hello 所需的 SAP 安裝媒體。

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>使用客戶特定的一般化映像部署 VM
Toospecific 修補程式需求方面 tooyour OS 或 DBMS 版本中，因為提供的 hello hello Azure Marketplace 中的映像可能不適合您的需求。 因此，您可能需要 toocreate 使用您自己 'private' 的 OS/DBMS VM 映像之後數次可部署的 VM。 tooprepare 這類的 'private' 映像進行複製，在 hello 一般化作業系統的 hello 內部部署 VM。 請參閱 toohello[部署指南 》] [ deployment-guide]的詳細資料 toogeneralize VM。

如果您已在內部部署 VM （特別是 2 層系統） 中安裝 SAP 內容，hello 部署的 hello Azure VM 透過 hello 執行個體重新命名程序支援 hello SAP 軟體佈建之後，您可以調整 hello SAP 系統設定管理員 (SAP 附註[1619720])。 否則，您可以 hello 部署的 hello Azure VM 之後再安裝 hello SAP 軟體。

為準，hello hello SAP 應用程式所使用的資料庫內容，您可以產生 hello 內容全新由 SAP 安裝或使用包含 DBMS 資料庫備份的 VHD，或運用 hello DBMS toodirectly 的功能，您可以會匯入您的內容至 Azure備份至 Microsoft Azure 儲存體。 在此情況下，可以也準備 Vhd，以 hello DBMS 資料和記錄檔案內部，然後將磁碟以匯入至 Azure。 但 hello 載入從內部部署 tooAzure DBMS 資料傳輸會透過需要 toobe 準備內部部署的 VHD 磁碟運作。

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>將 VM 從內部部署 tooAzure 使用非一般化磁碟
您計劃 toomove 特定 SAP 系統從內部部署 tooAzure （「 增益 」 和 「 shift 」）。 這可藉由來上傳 VHD，含 hello OS hello、 hello SAP 二進位檔和最終 DBMS 二進位檔加上 Vhd hello 與 hello hello DBMS tooAzure 的資料和記錄檔。 相反的 tooscenario #2 以上版本，則讓 hello 主機名稱、 SAP SID 和 SAP 使用者帳戶 hello Azure VM 中為 hello 在內部部署環境中設定。 因此，將一般化 hello 映像不需要。 此情況下最適合用於 hello SAP 環境的一部分執行的內部部署和組件在 Azure 上的跨內部部署案例。

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Azure VM 的相關高可用性和災害復原
Azure 提供下列高可用性 (HA) 和災害復原 (DR) 功能套用 toodifferent 元件，我們會使用適用於 SAP 和 DBMS 部署的 hello

### <a name="vms-deployed-on-azure-nodes"></a>部署於 Azure 節點上的 VM
hello Azure 平台不提供功能，例如即時移轉的已部署的 Vm。 這表示如果在部署 VM 的伺服器叢集上沒有維護所需，hello VM 需要 tooget 停止並重新啟動。 Azure 中的維護作業是在伺服器叢集內使用升級網域來執行。 一次只會維護一個升級網域。 在重新啟動期間將會中斷服務，而關閉 VM 的 hello、 進行維護然後重新啟動 VM。 大部分 DBMS 廠商都不過提供高可用性和災害復原功能，就會迅速重新啟動另一個節點上的 hello DBMS 服務如果 hello 主要節點無法使用。 hello Azure 平台提供了功能 toodistribute Vm、 儲存體和其他 Azure 服務規劃維護或基礎結構失敗的升級網域 tooensure 跨只會影響 Vm 或服務的小型子集。  計劃很可能 tooachieve 可用性層級比較 tooon 內部部署基礎結構。

Microsoft Azure 可用性設定組是 Vm 的邏輯群組或服務，可確保 Vm 和其他服務是分散式的 toodifferent 容錯和升級網域，並在叢集內，只能有一個節點關閉任何一處 （讀取的時間[這][ virtual-machines-manage-availability]文件以取得更多詳細資料)。

它需要 toobe 推出如下所示的 Vm 時設定的用途：

![適用於 DBMS HA 組態的可用性設定組定義][dbms-guide-figure-200]

如果我們想 toocreate 的 DBMS 部署 （的 hello 個別 DBMS HA 功能使用獨立） 的高可用性組態，hello DBMS Vm 需要：

* 新增 hello Vm toohello 相同 Azure 虛擬網路 (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* hello hello HA 組態的 Vm 也應該在 hello 相同子網路。 Hello 不同子網路之間的名稱解析無法在僅限雲端部署中，只有 IP 解析正常運作。 針對跨單位部署使用站對站或 ExpressRoute 連線能力，就已經建立了至少含有一個子網路的網路。 名稱解析都是根據 toohello 內部部署 AD 原則和網路基礎結構。

[comment]: <> (MSSedusch TODO 測試在 ARM 中是否仍為 true)

#### <a name="ip-addresses"></a>IP 位址
強烈建議 toosetup hello Vm HA 組態的彈性的方式。 依賴 IP 位址 tooaddress hello HA 夥伴 hello HA 組態內不可靠，在 Azure 中使用靜態 IP 位址。 Azure 中有兩種「關閉」概念︰

* 關閉透過 Azure 入口網站或 Azure PowerShell cmdlet 停止 AzureRmVM: hello 虛擬機器在此情況下會關閉和取消配置。 因此 hello 唯一要收費會致使其 hello 存放裝置使用，您的 Azure 帳戶不再計費此 vm。 不過，如果 hello 網路介面的 hello 私人 IP 位址不是靜態的 hello IP address 已釋放，而且不保證該 hello 網路介面取得 hello 分派 hello VM 重新啟動之後，再次舊 IP 位址。 執行 hello hello Azure 入口網站透過關閉，或藉由呼叫停止 AzureRmVM 會自動導致取消配置。 如果您不想停止 AzureRmVM StayProvisioned toodeallocat hello 機器使用
* 如果您關閉 hello 作業系統層級中的 VM，hello VM 取得關閉，無法取消配置。 不過，在此情況下，您的 Azure 帳戶將仍然支付 hello VM，儘管它已經關閉的 hello 事實。 在這種情況下，hello 分派的 hello IP 位址 tooa 已停止的 VM 將會維持不變。 正在關閉 hello 從 VM 內不會自動強制取消配置。

即使對於跨內部部署案例中，依預設關閉和取消配置都表示取消指派的 hello hello VM，IP 位址即使 DHCP 設定中的內部部署原則不同。

* hello 例外狀況如果其中一個會指派靜態 IP 位址 tooa 網路介面做為說明[這裡][virtual-networks-reserved-private-ip]。
* 在這種情況下 hello IP 位址會保持固定，只要 hello 網路介面不會刪除。

> [!IMPORTANT]
> 順序 tookeep hello 整個部署簡單且容易管理，在清除建議 toosetup hello hello Vm 合作 DBMS HA 或 DR 組態中在 Azure 中的 hello 牽涉到不同的 Vm 之間沒有正常運作的名稱解析的方式。
>
>

## <a name="deployment-of-host-monitoring"></a>部署主機監視功能
具生產力的 SAP 應用程式在 Azure 虛擬機器使用量和 SAP 需要 hello 能力 tooget 主機監視 hello 執行 hello Azure 虛擬機器的實體主機的資料。 需要有特定的 SAP HostAgent 修補程式等級，才能在 SAPOSCOL 和 SAP HostAgent 中啟用此功能。 hello 確切的修補程式層級記載於 SAP Note [1409604]。

關於部署元件，以便將主機資料 tooSAPOSCOL 和 SAPHostAgent 和 hello 該等元件的生命週期管理的 hello 詳細資訊，請參閱 toohello[部署指南][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>細節 tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>SQL Server IaaS
開始使用 Microsoft Azure，您可以輕鬆地移轉現有 SQL Server 建立的應用程式在 Windows Server 平台 tooAzure 虛擬機器上。 虛擬機器中 SQL Server 可讓您 tooreduce hello 擁有權總成本的部署、 管理和維護的企業廣度應用程式，輕鬆地將移轉這些應用程式 tooMicrosoft Azure。 透過 SQL Server 在 Azure 虛擬機器，系統管理員和開發人員仍然可以使用的 hello 可用的相同開發和管理工具內部。

> [!IMPORTANT]
> 請注意，我們不會討論 Microsoft Azure SQL Database 即平台為 hello Microsoft Azure 平台的服務供應項目。 本白皮書中的 hello 討論是 azure 的有關所知的內部部署在 Azure 虛擬機器，運用 hello 基礎結構即服務功能執行 hello SQL Server 產品。 這兩個產品之間所提供的資料庫性能與功能並不相同，不應混用彼此。 另請參閱︰<https://azure.microsoft.com/services/sql-database/>
>
>

強烈建議 tooreview[這][ virtual-machines-sql-server-infrastructure-services]文件，然後再繼續。

Hello 中將彙總而提及部分上方連結 hello hello 文件的下列各節片段。 也會提到 SAP 專屬的詳細資料，並更深入說明一些概念。 不過，強烈建議 toowork 透過上述第一個再讀取 hello SQL Server 特定文件的 hello 文件。

繼續之前，您應該先了解一些 IaaS 中 SQL Server 專屬的資訊：

* **虛擬機器 SLA**：如需適用於在 Azure 中執行之「虛擬機器」的 SLA，請參閱：<https://azure.microsoft.com/support/legal/sla/>  
* **SQL 版本支援**︰針對 SAP 客戶，我們在「Microsoft Azure 虛擬機器」上支援 SQL Server 2008 R2 和更新版本。 不支援舊版。 如需更多詳細資料，請檢閱這份通用的 [支援聲明](https://support.microsoft.com/kb/956893) 。 請注意，Microsoft 通常也支援 SQL Server 2008。 不過，與 SQL Server 2008 R2 引進 SAP toosignificant 功能，因為 SQL Server 2008 R2 為 hello 適用於 SAP 的最低版本。 請記住，SQL Server 2012 和 2014年收到 hello IaaS 案例 （例如，直接對 Azure 儲存體備份） 的更深入整合與擴充。 因此，我們會限制此紙張 tooSQL Server 2012 和 2014 其最新修補程式等級，適用於 Azure。
* **SQL 功能支援**︰「Microsoft Azure 虛擬機器」上支援大部分的 SQL Server 功能，但有一些例外。 **不支援使用共用磁碟的 SQL Server 容錯移轉叢集**。  單一 Azure 區域內支援分散式技術 (例如，資料庫鏡像、AlwaysOn 可用性群組、複寫、記錄傳送，以及 Service Broker)。 SQL Server AlwaysOn 也在不同 Azure 區域之間受到支援，如以下文件所述︰<https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>。  檢閱 hello[支援聲明](https://support.microsoft.com/kb/956893)如需詳細資訊。 有關如何 toodeploy AlwaysOn 組態所示的範例[這][ virtual-machines-workload-template-sql-alwayson]發行項。 此外，請參閱 hello 記載的最佳作法[這裡][virtual-machines-sql-server-infrastructure-services]
* **SQL 效能**： 我們確信 Microsoft Azure 代管的虛擬機器將會執行地很好比較 tooother 公用雲端虛擬化方案，但是個別結果中，可能會不同。 請參閱[這篇][virtual-machines-sql-server-performance-best-practices]文章。
* **使用 Azure marketplace 的映像**: hello 最快方式 toodeploy 新的 Microsoft Azure VM 是 toouse hello Azure Marketplace 中的影像。 有含有 SQL Server hello Azure Marketplace 映像。 SQL Server 已安裝的 hello 映像不能立即用於 SAP NetWeaver 應用程式。 hello 原因是 hello 預設 SQL Server 定序會安裝這些映像或不 SAP NetWeaver 系統所需的 hello 定序中。 在排序 toouse 這類映像，請檢查 hello 章節所述的步驟[超出 hello Microsoft Azure Marketplace 使用 SQL Server 映像][dbms-guide-5.6]。
* 如需詳細資訊，請參閱 [定價詳細資料](https://azure.microsoft.com/pricing/) 。 hello [SQL Server 2012 授權指南](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf)和[SQL Server 2014 授權指南](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf)也是相當重要的資源。

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 相關之 SQL Server 的 SQL Server 組態指導方針
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>適用於 SAP 相關之 SQL Server 部署的 VM/VHD 結構建議
Hello 一般描述，根據 SQL Server 可執行檔應該位於或安裝到 hello hello VM 基本 vhd 的系統磁碟機 (磁碟機 c:\)。  一般而言，大部分的 hello SQL Server 系統資料庫不會使用高層次的 SAP NetWeaver 工作量。 因此 hello 系統資料庫 （master、 msdb 和 model） 的 SQL server 可留在 hello C:\ 磁碟機上。 例外狀況可能是 tempdb，這在 hello 案例中的某些 SAP ERP 和所有 BW 工作量可能需要較高的資料量或 I/O 作業量，無法放入 hello 原始 VM。 這類系統，應該執行下列步驟的 hello:

* 移動 hello 主要 tempdb 資料檔案 toohello hello 主要資料檔案中的 hello SAP 資料庫的相同邏輯磁碟機。
* 新增 hello 的任何其他的 tempdb 資料檔案 tooeach 其他包含 hello SAP 使用者資料庫的資料檔案的邏輯磁碟機。
* 新增 hello tempdb 記錄檔 toohello 邏輯磁碟機包含 hello 使用者資料庫的記錄檔。
* **專用的 VM 類型可使用本機 Ssd** hello 計算節點 tempdb 資料和記錄檔可能會放在 hello D:\ 磁碟機上。 不過，它可能會建議 toouse 多個 tempdb 資料檔案。 請注意 D:\ 磁碟機的磁碟區都不同 hello VM 類型為基礎。

這些設定可讓 tempdb tooconsume 空間 hello 系統磁碟機無法 tooprovide 還要多。 順序 toodetermine hello 正確的 tempdb 大小，使用者可以檢查現有的系統執行內部部署的 hello tempdb 大小。 此外，這種組態會啟用對 tempdb 無法隨附 hello 系統磁碟機的 IOPS 數目。 同樣地，在內部部署執行的系統可以針對 tempdb 使用的 toomonitor I/O 工作負載，讓您可以衍生預期在 tempdb 上 toosee hello IOPS 數目。

執行 SQL Server 與 SAP 資料庫和 tempdb 資料和 tempdb 記錄檔放置在 hello D:\ 磁碟機上的 VM 組態應該像這樣：

![適用於 SAP 之 Azure IaaS VM 的參考組態][dbms-guide-figure-300]

請注意該 hello D:\ 磁碟機具有不同大小 hello VM 類型而定。 相依於 tempdb hello 大小需求可能會強制的 toopair tempdb 資料和記錄檔以 hello SAP 資料庫資料和記錄檔中的情況下，D:\ 磁碟機太小。

#### <a name="formatting-hello-vhds"></a>格式化 hello Vhd
SQL Server hello NTFS 區塊大小的 Vhd，含 SQL Server 資料和記錄檔案應該是 64k。 沒有任何需要 tooformat hello D:\ 磁碟機。 此磁碟機已預先格式化。

在確定 hello 還原或建立的資料庫不會初始化 hello 資料檔案所清空 hello hello 檔案內容，您應該確定的順序 toomake hello 使用者內容 hello SQL Server 服務正在執行具有特定權限。 Hello Windows 系統管理員群組中的使用者通常會有這些權限。 Hello SQL Server 服務執行於非 Windows 系統管理員使用者 hello 使用者內容，如果您需要 tooassign 該使用者 hello '執行磁碟區維護工作' 的使用者權限。  請參閱 Microsoft 知識庫文件中的 hello 詳細資料： <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>資料庫壓縮的影響
在組態中的 I/O 頻寬可能會變成限制因素，每個量值可減少 IOPS 可能有助於 toostretch hello 工作負載一次可以執行像是 Azure IaaS 案例中。 因此，如果尚未這樣做，套用 SQL Server PAGE 壓縮強烈建議 SAP 和 Microsoft 之前上傳現有 SAP 資料庫 tooAzure。

再上傳 tooAzure hello 建議 tooperform 資料庫壓縮是出於兩個原因：

* 上傳資料 toobe hello 量較低。
* 假設有更多的 Cpu 或更高 I/O 頻寬或更少的 I/O 延遲內部部署可以使用更強的硬體較短的 hello 壓縮執行 hello 持續時間。
* 較小的資料庫大小可能會導致 tooless 成本進行磁碟配置

資料庫壓縮也可以在 Azure 虛擬機器中運作，如同它在內部部署中的運作方式。 如需有關如何 toocompress 現有 SAP SQL Server 資料庫，請參閱以下： <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>SQL Server 2014 – 將資料庫檔案直接儲存於 Azure Blog 儲存體上
SQL Server 2014 開啟 hello 可能性 toostore 直接在 Azure Blob 存放區沒有 hello '的包裝函式' 周圍的 VHD 上的資料庫檔案。 特別是在使用標準的 Azure 儲存體或較小的 VM 類型這可讓您可以在其中克服 hello 有限數目的可掛接的 toosome 較小的 VM 類型的 Vhd 的 IOPS 會強制執行限制的案例。 不過，這適用於 SQL Server 的使用者資料庫，而不適用於系統資料庫。 這也適用於 SQL server 的資料和記錄檔。 如果您想要 toodeploy SAP 的 SQL Server 資料庫中而不是這種方式 '前後' 到 Vhd，請記住下列 hello:

* 中的 hello 使用儲存體帳戶的需求 toobe hello 相同 Azure 區域為 hello 為使用的 toodeploy hello VM 的 SQL Server 正在執行中的其中一個。
* 先前所述有關 toodistribute Vhd 透過不同的 Azure 儲存體帳戶的考量適用於這個部署同樣的方法。 表示 hello hello 限制 hello Azure 儲存體帳戶的 I/O 作業數目。

[comment]: <> (MSSedusch TODO 但這將會使用網路頻寬而非儲存體頻寬，不是嗎？)

這種部署類型的詳細資料如下︰<https://msdn.microsoft.com/library/dn385720.aspx>

在訂單 toostore SQL Server 資料檔案直接在 Azure 高階儲存體上，您需要 toohave 最小的 SQL Server 2014 修補程式版本，請參閱： <https://support.microsoft.com/kb/3063054>。 儲存在 Azure 標準儲存體的 SQL Server 資料檔案會與 hello 發行版本的 SQL Server 2014 運作。 不過，hello 完全相同的修補程式包含修正程式，這會導致 hello 直接使用 Azure Blob 儲存體的 SQL Server 資料檔案和備份更可靠的另一個的數列。 因此我們建議 toouse 這些修補程式一般。

### <a name="sql-server-2014-buffer-pool-extension"></a>SQL Server 2014 緩衝集區延伸
SQL Server 2014 引進的新功能，稱為「緩衝集區延伸模組」。 這個功能擴展了 hello 緩衝集區的保留記憶體中的第二個層級快取伺服器的本機 Ssd 或 VM 所支援的 SQL Server。 這可讓 tookeep 大的工作集的 'in '的記憶體資料。 比較的 tooaccessing 成 hello 擴充功能，並儲存在 Azure VM 的本機 Ssd 上 hello 緩衝集區的標準儲存體 Azure hello 存取將會更快許多因素而定。  因此，利用 hello 本機 D:\ 磁碟機有絕佳的 IOPS 及輸送量的 hello VM 類型可能是非常合理方式 tooreduce hello IOPS 載入對 Azure 儲存體，並大幅改善查詢回應時間。 這特別適用於未使用進階儲存體時。 高階儲存體和 hello 使用方式的 hello Premium Azure 讀取快取 hello 計算節點上，如果資料檔案的建議，預期不大的差異。 原因是這兩個快取 （SQL Server 緩衝集區延伸模組和 Premium 儲存體讀取快取） 會使用 hello 的 hello 運算節點的本機磁碟。
如需有關此功能的更多詳細資料，請參閱這份文件︰<https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>SQL Server 的備份/復原考量
將 SQL Server 部署至 Azure 時，必須檢閱您的備份方法。 即使 hello 系統不是生產系統，由 SQL Server 託管的 hello SAP 資料庫必須定期備份。 因為 Azure 儲存體會保留三個影像，備份現在是較不重要，尤其是尊重 toocompensating 儲存體損毀。 維護適當的備份和復原計劃 hello 優先順序原因是，您可以藉由提供時間復原功能的中點補償邏輯/手動錯誤有更多。 因此 hello 的目標是 tooeither 使用備份 toorestore hello 資料庫備份 tooa 特定點 Azure tooseed 中的時間或 toouse hello 備份中另一個系統複製 hello 現有的資料庫。 例如，您無法從傳輸的 2 層 SAP 組態 tooa 3 層系統設定 hello 相同系統還原的備份。

有三個不同的方式 toobackup SQL Server tooAzure 儲存體：

1. SQL Server 2012 CU4 和更高版本可以原生備份資料庫 tooa URL。 Hello 部落格有詳細說明[中 SQL Server 2014 – 第 5 部分 – 備份/還原增強功能的新功能](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx)。 請參閱 [SQL Server 2012 SP1 CU4 和更新版本][dbms-guide-5.5.1]一章。
2. SQL Server 版本先前 tooSQL 2012 CU4 可以使用重新導向功能 toobackup tooa VHD，基本上再 hello 寫入串流移往已設定的 Azure 儲存體位置。 請參閱 [SQL Server 2012 SP1 CU3 和舊版][dbms-guide-5.5.2]一章。
3. hello 最後一種方法是 tooperform 傳統的 SQL Server 備份 toodisk 命令至 VHD 磁碟裝置。  這是相同的 toohello 在內部部署的部署模式，而且不會在這份文件中詳細討論。

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 和更新版本
這項功能可讓您 toodirectly 備份 tooAzure BLOB 儲存體。 如果沒有這個方法中，您必須備份 tooother Azure Vhd，因而耗用 VHD 和 IOPS 容量。 hello 基本上想法如下：

 ![使用 SQL Server 2012 備份 tooMicrosoft Azure 儲存體 BLOB][dbms-guide-figure-400]

hello 優點在此情況下會是不需要 toospend Vhd toostore SQL Server 備份上。 因此，有較少的 Vhd 配置，hello 的 VHD IOPS 的整個頻寬可用於資料和記錄檔。 請注意 hello 備份的大小上限是有限的 tooa 上限為 1 TB，如本文中的 hello 一節 < 限制 > 中所述： <https://msdn.microsoft.com/library/dn435916.aspx#limitations>。 如果 hello 備份的大小，即使使用 SQL Server 備份壓縮的大小超過 1 TB，hello 章節所述的功能[SQL Server 2012 SP1 CU3 和更舊版本][ dbms-guide-5.5.2]在這份文件，也需要使用 toobe。

[相關文件](https://msdn.microsoft.com/library/dn449492.aspx)描述 hello 還原的資料庫從 Azure Blob 存放區中的備份，建議您無法直接從 Azure BLOB 存放區 toorestore hello 備份是否 > 25 GB。 本文章中的 hello 建議只根據效能考量，並不因為 toofunctional 限制。 因此，隨著案例的不同，可能會發生不同的狀況。

如需有關如何設定和利用此備份類型的說明，請參閱 [這個](https://msdn.microsoft.com/library/dn466438.aspx) 教學課程

可以讀取的一連串步驟 hello 範例[這裡](https://msdn.microsoft.com/library/dn435916.aspx)。

自動備份，為最高的重要性 toomake 確定每個備份的 hello Blob 的名稱不同。 否則將會覆寫，而且 hello restore 鏈已中斷。

為了不 toomix hello 3 之備份的不同類型的項目上時，它是建議 toocreate 不同的容器下方 hello 做為備份用途的儲存體帳戶。 hello 容器可以是只有 VM 或 VM 和備份類型。 hello 結構描述如下：

 ![使用 SQL Server 2012 備份 tooMicrosoft Azure 儲存體 BLOB-個別儲存體帳戶不同的容器][dbms-guide-figure-500]

Hello 備份不會執行到相同的儲存體帳戶在 hello hello hello 上述範例中所部署 Vm。 有新的儲存體帳戶，特別針對 hello 備份。 內 hello 儲存體帳戶，會建立不同的備份與 hello VM 名稱 hello 型矩陣的容器。 這類分割可讓您更輕鬆 tooadministrate hello 備份 hello 不同的 Vm。

其中一個直接寫入 hello 備份 hello Blob 不會加入 toohello hello VM 的 Vhd 數目。 因此可以最大化 hello hello 資料的 hello 特定 VM SKU 的掛接 Vhd 上限和交易記錄檔，並仍然執行備份，以對儲存體容器。

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 和舊版
您必須執行順序 tooachieve 中備份，直接對 Azure 儲存體的 hello 第一個步驟就是連結太 toodownload hello msi[這](https://www.microsoft.com/download/details.aspx?id=40740)KBA 文章。

下載 hello x64 安裝檔案和 hello 文件。 hello 檔案會安裝程式: 'Microsoft SQL Server Backup tooMicrosoft Azure 工具'。 徹底閱讀 hello hello 產品文件。  hello 工具基本上可以下列方式 hello:

* Hello SQL Server 端，從定義 hello SQL Server 備份的磁碟位置 （請勿這個使用 hello D:\ 磁碟機）。
* hello 工具可讓您可使用的 toodirect 不同類型的備份 toodifferent Azure 儲存體容器 toodefine 規則。
* 一旦 hello 規則準備就緒，hello 工具將會重新導向 hello 備份 tooone hello Vhd/磁碟 toohello 先前所定義 Azure 儲存體位置的 hello 寫入資料的流。
* hello 工具會導致 hello VHD/磁碟所定義的 hello SQL Server 上的一個數 KB 大小的小型的虛設常式檔案備份。 **此檔案應該留在 hello 儲存位置，因為它是必要的 toorestore 再次從 Azure 儲存體。**
  * 如果您遺失 hello stub 檔案 （例如，透過遺失 hello 包含 hello stub 檔案的儲存媒體），而且您已選擇備份 tooa Microsoft Azure 儲存體帳戶的 hello 選項，您可能會復原 hello stub 檔案透過 Microsoft Azure 儲存體從放置的 hello 儲存體容器下載。 您應該然後將 hello stub 檔案放在其中 hello 工具是設定的 toodetect 和上傳 toohello hello 本機電腦上資料夾相同的容器以 hello 如果加密搭配 hello 原始規則使用相同的加密密碼。

這表示 hello 結構描述可以也可供 SQL Server 版本不允許直接定址 Azure 儲存體位置放置與上述針對較新版的 SQL Server。

此方法不應與較新版的 SQL Server 搭配使用，這些版本支援以原生方式備份 Azure 儲存體。 例外狀況是其中的 hello 原生備份至 Azure 的限制會封鎖 Azure 原生備份執行。

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>其他可能性 toobackup SQL Server 資料庫
其他可能性 toobackup 資料庫是其他 Vhd tooa tooattach VM 上使用 toostore 備份。 在這類情況下，您必須 toomake 確定該 hello Vhd 正在不完整。 在 hello 情形下，您需要 toounmount hello VHD，因此 toospeak '' 將它封存，並取代為新的空白 VHD。 如果您向該路徑下，您要 tookeep hello 的 hello 與 hello 資料庫檔案的 Vhd 從不同的 Azure 儲存體帳戶中的這些 Vhd。

第二種可能性是 toouse 可以有許多 Vhd 附加的大型 VM。 例如 有 32 個 VHD 的 D14。 使用儲存空間 toobuild 彈性的環境，您無法建立共用，會再做為備份目標 hello 不同 DBMS 伺服器使用。

[這裡](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) 也記載了一些最佳做法。

#### <a name="performance-considerations-for-backupsrestores"></a>備份/還原的效能考量
裸機部署，如同備份/還原效能是取決於磁碟區數目可以讀取以平行方式，而且這些磁碟區的哪些 hello 輸送量可能。 此外，hello 備份壓縮所使用的 CPU 耗用量可能相當重要的角色上播放的 Vm 只向上 too8 CPU 執行緒。 因此，您可以假設︰

* hello 較少的 Vhd hello 數目使用 toostore hello 資料檔案，hello 較小 hello 中讀取的整體輸送量。
* hello 數目較少 hello hello VM 中的 CPU 執行緒，hello 更嚴重 hello 備份壓縮的影響。
* hello 較少的目標 （Blob 或 Vhd） toowrite hello 來備份、 hello 較小者 hello 輸送量。
* hello 小 hello VM 大小，hello 小 hello 儲存體輸送量配額寫入和讀取從 Azure 儲存體。 Hello 備份是否直接儲存在 Azure Blob 上或儲存在一次在 Azure Blob 中儲存的 Vhd 是否與無關。

時使用 Microsoft Azure 儲存體 BLOB 做為較新版本中的 hello 備份目標，您必須針對每個特定的備份限制的 toodesignating 只有一個 URL 目標。

但當使用 hello 'Microsoft SQL Server Backup tooMicrosoft Azure 工具' 中的較舊版本中，您可以定義多個檔案目標。 具有多個目標，hello 備份規模和 hello hello 備份的輸送量較高。 這會導致再也在 hello Azure 儲存體帳戶中的多個檔案。 在我們的測試，使用其中一個絕對可以達到 hello 輸送量達到使用 hello 備份延伸模組的多個檔案目的地實作從 SQL Server 2012 SP1 CU4 上。 您也不會封鎖 hello 1 TB 限制與 hello 原生備份至 Azure。

不過，請記住，hello 輸送量也取決於 hello hello hello 備份所使用的 Azure 儲存體帳戶位置。 了解可能 toolocate hello 儲存體帳戶以外的不同區域 hello Vm 正在執行中。 例如 您會在西歐，執行 hello VM 組態，但將 hello 對付 tooback 用於北歐的儲存體帳戶。 一定會有影響 hello 備份輸送量和似乎 toobe hello 目標儲存體，而且 hello Vm 可能在 hello 中執行的每秒 150MB 的輸送量是不可能 toogenerate 相同地區資料中心。

#### <a name="managing-backup-blobs"></a>管理備份 BLOB
沒有自己的需求 toomanage hello 備份。 由於 hello 預期的情況下，將透過執行頻繁的交易記錄備份中建立許多 blob，管理 blob 輕鬆可以運作 hello Azure 入口網站。 因此，它是時 tooleverage Azure 儲存體總管。 有數個類好工具可用，可協助 toomanage Azure 儲存體帳戶

* 安裝 Azure SDK 的 Microsoft Visual Studio (<https://azure.microsoft.com/downloads/>)
* Microsoft Azure 儲存體總管 (<https://azure.microsoft.com/downloads/>)
* 協力廠商工具

[comment]: <> (在 ARM 上尚不支援)
[comment]: <> (#### Azure VM 備份)
[comment]: <> (Hello SAP 系統內的 Vm 可以備份使用 Azure 虛擬機器備份功能。Azure 虛擬機器備份及早在 hello 2015 年引進，並同時是標準方法 toobackup 完成 VM 在 Azure 中。Azure 備份儲存在 Azure 中的 hello 備份，並允許虛擬機器還原一次。)
[comment]: <> (執行的資料庫可以備份以一致的方式以及如果 hello DBMS 系統支援 hello Windows VSS 磁碟區陰影複製服務的 Vm < 沒有 https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> 與 SQL Server。因此使用 Azure VM 的備份可以是可還原的已方式 tooget tooa SAP 資料庫的備份。不過請注意，您無法以資料庫的 Azure VM 備份還原時間點為基礎。因此，hello 建議 tooperform DBMS 功能，而不是依賴 Azure VM 備份的資料庫備份。)
[comment]: <> (熟悉 Azure 虛擬機器備份 tooget 請從這裡開始 < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>使用 Microsoft Azure Marketplace hello 超出 SQL Server 映像
Microsoft 提供 hello 已經包含 SQL Server 版本的 Azure Marketplace 中的 Vm。 對於需要 SQL Server 和 Windows 的授權的 SAP 客戶，這可能是由已安裝的 SQL server Vm，大致授權機會 toobasically 封面 hello 需求。 在訂單 toouse for SAP，這類映像 hello 下列考量需要 toobe 進行：

* hello SQL Server 非評估版取得的成本會高於只 ' 僅限 Windows' 部署的 VM 從 Azure Marketplace。 這些文章 toocompare 價格，請參閱： <https://azure.microsoft.com/pricing/details/virtual-machines/>和<https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>。
* 您只能使用 SAP 支援的 SQL Server 版本，例如 SQL Server 2012。
* hello SQL Server 執行個體安裝在 hello hello Azure Marketplace 中提供的 Vm 中的 hello 定序不是 hello 定序的 SAP NetWeaver 需要 hello SQL Server 執行個體 toorun。 您可以變更 hello 定序，但仍有 hello hello 之後 > 一節中的指示進行。

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>變更 hello 的 Microsoft Windows/SQL Server VM 的 SQL Server 定序
Hello hello Azure Marketplace 中的 SQL Server 映像未設定 toouse hello 定序所需的 SAP NetWeaver 應用程式，因為它需要 toobe hello 部署之後立即變更。 SQL Server 2012，作法是以 hello 下列步驟儘速 hello 已部署 VM，並且系統管理員可以到 hello toolog 部署 VM:

* 以「系統管理員身分」開啟 Windows 命令視窗。
* 變更 hello 目錄 tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012。
* 執行 hello 命令： Setup.exe /QUIET /ACTION = REBUILDDATABASE /INSTANCENAME = MSSQLSERVER /SQLSYSADMINACCOUNTS =`<local_admin_account_name`> /SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> 是 hello 帳戶透過 hello 圖庫的第一次部署的 hello hello VM 時定義為 hello 系統管理員帳戶。

hello 程序應該只需要幾分鐘的時間。 確定的順序 toomake 中 hello 步驟結果 hello 正確的結果，是否，請執行下列步驟的 hello:

* 開啟 SQL Server Management Studio。
* 開啟查詢視窗。
* Hello SQL Server master 資料庫中，執行 sp_helpsort hello 命令。

hello 預期的結果應該如下：

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

如果這不是 hello 結果，停止 」 部署 SAP，並調查為什麼 hello setup 命令未正常運作。 部署到具有不同的 SQL Server 字碼頁之 SQL Server 執行個體上的 SAP NetWeaver 應用程式比 hello 上面所述的其中一個是**不**支援。

### <a name="sql-server-high-availability-for-sap-in-azure"></a>SQL Server 在 Azure 中適用於 SAP 的高可用性
如本文稍早所述，沒有任何所需 hello hello 最舊的 SQL Server 高可用性功能使用方式的可能性 toocreate 共用存放裝置。 這項功能會安裝在 Windows Server 容錯移轉叢集 (WSFC) hello 使用者資料庫 （以及最終 tempdb） 使用的共用的磁碟的兩個或多個 SQL Server 執行個體。 這是 SAP 也支援 hello 很長的時間標準的高可用性方法。 由於 Azure 不支援共用儲存體，所以無法實現具有共用磁碟叢集組態的 SQL Server 高可用性組態。 不過，許多其他高可用性方法仍可能發生而且 hello 下列各節所述。

[comment]: <> (仍在參考 tooASM 發行項。)
[comment]: <> (閱讀 hello 不同特定高可用性技術可使用 Azure 中的 SQL Server 之前, 有是很好的文件提供更多詳細資料和指標 [這裡] [virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions])

#### <a name="sql-server-log-shipping"></a>SQL Server 記錄傳送
其中一個高可用性 (HA) hello 方法是 SQL Server 記錄傳送。 如果 hello 參與 hello HA 組態的 Vm 具有運作中的名稱解析，沒有任何問題，並在 Azure 中的 hello 安裝程式沒有差別是在內部部署的任何設定。 不建議 toorely 上只有 IP 解析。 設定記錄傳送和 hello 記錄傳送原則的相關事宜 toosetting，請參閱這份文件：

<https://technet.microsoft.com/library/ms187103.aspx>

順序 tooreally 達成任何高可用性，您需要 toodeploy hello 是中的這類記錄傳送組態 toobe 內 hello 相同 Azure 可用性設定組的 Vm。

#### <a name="database-mirroring"></a>資料庫鏡像
SAP 支援的資料庫鏡像 (請參閱 SAP 附註[965908]) 依賴定義 hello SAP 連接字串中的容錯移轉夥伴。 Hello 跨單位的情況下，我們假設兩個 Vm 位於 hello 該 hello 相同的網域下執行 hello 使用者內容 hello 兩個 SQL Server 執行個體，網域使用者，以及和是相關的 hello 兩個 SQL Server 執行個體中有足夠的權限。 因此，資料庫鏡像在 Azure 中的 hello 安裝程式會相同典型的內部部署安裝程式組態。

為僅限雲端部署的 hello 簡單的方法是 toohave 另一個網域安裝程式在 Azure toohave 那些 DBMS Vm （和最好是專用的 SAP Vm） 單一網域內。

如果網域不可行，其中也可以使用憑證 hello 資料庫鏡像端點，如下所述： <https://technet.microsoft.com/library/ms191477.aspx>

教學課程 tooset 向上資料庫鏡像在 Azure 中可以在這裡找到： <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>AlwaysOn
因為 SAP 內部部署環境支援 AlwaysOn (請參閱 SAP 附註[1772688])，它是用於結合，以在 Azure 中 SAP 支援的 toobe。 您不能共用的 toocreate 磁碟在 Azure 中的 hello 事實並不表示其中一個無法建立 AlwaysOn Windows Server 容錯移轉叢集 (WSFC) 之間的設定不同的 Vm。 這只表示，您不需要 hello 可能性 toouse 共用的磁碟做為仲裁 hello 叢集組態中。 因此您可以建置在 Azure 中的 AlwaysOn WSFC 組態和只要不選取利用共用的磁碟的 hello 仲裁類型。 hello Azure 環境來部署那些 Vm 中依名稱 hello Vm 再 hello Vm 應該在 hello 應該可以解決相同的網域。 這適用於僅限 Azure 和跨單位部署。 有一些特殊考量部署 hello SQL Server 可用性群組接聽程式 (不 toobe 與 hello Azure 可用性設定組混淆) 因為 toosimply 因為 Azure 在此時間點不允許建立 AD/DNS 物件內部部署。 因此，執行一些不同的安裝步驟是必要 tooovercome Azure 的 hello 特定行為。

以下是使用可用性群組接聽程式的一些考量︰

* 使用可用性群組接聽程式只適用於 Windows Server 2012 或 Windows Server 2012 R2 做為客體作業系統的 hello VM。 適用於 Windows Server 2012 中，您必須確保已套用這個修補程式 toomake: <https://support.microsoft.com/kb/2854082>
* 針對 Windows Server 2008 R2 本修補檔不存在，且必須 AlwaysOn toobe 用於 hello 相同做為資料庫鏡像的方式指定 hello 連接字串中的容錯移轉夥伴 （完成透過 hello SAP default.pfl 參數 dbs/mss/server – 請參閱 SAP 附註[965908])。
* 當使用可用性群組接聽程式、 hello 資料庫 Vm 需要連接 toobe tooa 專用負載平衡器。 名稱解析，僅限雲端部署中的可能會需要 SAP 系統的所有 Vm （應用程式伺服器、 DBMS 伺服器和 (A) SCS 伺服器） 是在 hello 相同虛擬網路，或都需要從 hello etc\host 檔案中的 SAP 應用程式層 hello 維護順序 tooget hello VM 的名稱解析的 hello SQL Server Vm。 順序 tooavoid Azure 指派新的 IP 位址，在其中兩個 Vm 都關機的情況下，在其中一個應該指派靜態 IP 位址 （定義靜態 IP 位址所述的 hello AlwaysOn 組態中的那些 Vm toohello 網路介面[這][ virtual-networks-reserved-private-ip]文章)

[comment]: <> (舊部落格)
[comment]: <> (<https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, <https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx>)
* 不需要建置 hello WSFC 叢集組態中的 hello 叢集需要特殊的 IP 位址指派時，因為 Azure 及其目前功能會指派 hello 叢集名稱的特殊步驟 hello hello 節點 hello 叢集相同的 IP 位址上建立。 這表示手動步驟必須是執行的 tooassign 不同的 IP 位址 toohello 叢集。
* hello 可用性群組接聽程式正在 toobe 在 Azure 中建立具有 TCP/IP 端點指派 toohello Vm 執行 hello hello 可用性群組的主要和次要複本。
* 可能有需要 toosecure 這些端點，其中包含 Acl。

[comment]: <> (TODO 舊部落格)
[comment]: <> (hello 詳細的步驟和逐步解說 hello 教學課程可以使用 [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups] 時，最佳遇到必要條件安裝在 Azure 上的 AlwaysOn 組態)
[comment]: <> (預先設定透過 hello Azure 組件庫的 AlwaysOn 安裝程式 < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> ([這個][virtual-machines-windows-classic-ps-sql-int-listener] 教學課程提供建立「可用性群組接聽程式」的最佳說明)
[comment]: <> (以下提供使用 ACL 來保護網路端點的最佳說明：)
[comment]: <> (*    <https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx> )
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>)

透過不同的 Azure 區域也是可能 toodeploy SQL Server AlwaysOn 可用性群組。 這項功能將會利用 hello Azure 是 「 VNet 對 Vnet 連線能力 ([詳細][virtual-networks-configure-vnet-to-vnet-connection])。

[comment]: <> (TODO 舊部落格)
[comment]: <> (此處所述的 SQL Server AlwaysOn 可用性群組在此案例中的 hello 安裝程式： < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>。)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Azure 中 SQL Server 高可用性的摘要
指定 Azure 儲存體會保護 hello 內容 hello 事實，沒有一個較少因此 tooinsist 熱待命映像。 這表示您的高可用性案例需要 tooonly 防範 hello 下列案例：

* 因為在 Azure 中的 hello 伺服器叢集上 toomaintenance 或其他原因整個 hello VM 無法使用
* Hello SQL Server 執行個體中的軟體問題
* 防止發生資料遭到刪除而需要進行時間點復原的手動錯誤

尋找符合綜觀 hello 前兩個案例可以依照資料庫鏡像或 AlwaysOn，而第三個案例的 hello 只可以涵蓋記錄傳送的技術。

您將需要 toobalance hello 更複雜的設定 AlwaysOn，比較 tooDatabase 的鏡像，與 hello AlwaysOn 的優點。 以下列出這些優點︰

* 可讀取的次要複本。
* 來自次要複本的備份。
* 延展性較佳。
* 一個以上的次要複本。

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>適用於 Azure 上 SAP 的一般 SQL Server 摘要
本指南中提供許多建議，而我們建議您在規劃 Azure 部署之前，多次閱讀本指南。 一般情況下，不過，是確定 toofollow hello Azure 的特定點上的前十個一般 DBMS:

[comment]: <> (2.3 輸送量比什麼更高？比一個 VHD 高？)
1. 使用 hello 最新 DBMS 版本中的，像是 SQL Server 2014 中，在 Azure 中具有 hello 大部分優點。 SQL Server，這是備份的 SQL Server 2012 SP1 CU4 會包括 hello 與 Azure 儲存體功能。 不過，與 SAP 一起建議至少 SQL Server 2014 SP1 CU1 或 SQL Server 2012 SP2 和 hello 的最新 CU。
2. 請仔細規劃 SAP 系統版圖中 Azure toobalance hello 資料檔案配置和 Azure 限制：
   * 不需要太多 Vhd，但有足夠 tooensure 可以連線到您所需的 IOPS。
   * 請記住，每個「Azure 儲存體帳戶」也都有 IOPS 限制，而且「儲存體帳戶」在每個 Azure 訂用帳戶內是有限的 ([更多詳細資料][azure-subscription-service-limits])。
   * 只有等量磁碟區跨 Vhd，如果您需要 tooachieve 較高的輸送量。
3. 永不安裝軟體，或將需要 hello D:\ 磁碟機上的持續性，因為它是不是永久性，而且此磁碟機上的任何項目將會遺失在重新啟動 Windows 之後的任何檔案。
4. 不要針對 Azure 標準儲存體使用 Azure VHD 快取。
5. 不要使用 Azure 異地備援的儲存體帳戶。  針對 DBMS 工作負載使用本機備援。
6. 使用 DBMS 廠商的 HA/DR 解決方案 tooreplicate 資料庫資料。
7. 一律使用名稱解析，不要依賴 IP 位址。
8. 使用 hello 高的資料庫壓縮可能。 針對 SQL Server 而言，此為頁面壓縮。
9. 請小心使用 SQL Server 映像從 hello Azure Marketplace。 如果您使用 hello 其中一個 SQL Server，您必須變更 hello 執行個體定序，才能在其上安裝任何 SAP NetWeaver 系統。
10. 安裝及設定中所述的 SAP Host Monitoring for Azure 的 hello[部署指南 》][deployment-guide]。

## <a name="specifics-toosap-ase-on-windows"></a>細節 tooSAP Windows 上 ASE
開始使用 Microsoft Azure，您可以輕鬆地移轉您現有的 SAP ASE 應用程式 tooAzure 虛擬機器。 虛擬機器中的 SAP ASE 可輕鬆地將移轉這些應用程式 tooMicrosoft Azure 讓您 tooreduce hello 擁有權總成本的部署、 管理和維護的企業廣度應用程式。 透過 SAP ASE Azure 虛擬機器中，系統管理員和開發人員仍然可以使用的 hello 可用的相同開發和管理工具內部。

Hello 可以在這裡找到 Azure 虛擬機器的 sla: <https://azure.microsoft.com/support/legal/sla>

我們確信 Microsoft Azure 代管的虛擬機器將會執行地很好比較 tooother 公用雲端虛擬化方案，但是個別結果中，可能會不同。 SAP 調整大小的 SAPS 數字的不同 SAP 認證中個別的 SAP 附註將會提供 VM Sku 的 hello [1928533]。

陳述式和 Azure 儲存體、 SAP 部署 Vm 或 SAP Monitoring 的建議考慮 toohello 使用量套用 toodeployments 的 SAP ASE 搭配述整個 hello 的這份文件的前四個章節的 SAP 應用程式。

### <a name="sap-ase-version-support"></a>SAP ASE 版本支援
SAP 目前支援 SAP ASE 版本 16.0，可與 SAP 商務套件產品搭配使用。 SAP ASE 伺服器、 或 JDBC 和 ODBC 驅動程式 toobe SAP Business Suite 等作業只透過所提供的產品搭配使用的所有更新都 hello 在 SAP 服務 Marketplace: <https://support.sap.com/swdc>。

安裝與內部部署，不要直接從 Sybase 網站下載更新 hello SAP ASE 伺服器或 hello JDBC 和 ODBC 驅動程式。 支援使用 SAP Business Suite 產品在內部部署與 Azure 虛擬機器中的修補程式的詳細資訊，請參閱下列 「 SAP 附註的 hello:

* [1590719]
* [1973241]

SAP ASE 上執行 SAP Business Suite 的一般資訊位於 hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 相關之 SAP ASE 的 SAP ASE 組態指導方針
#### <a name="structure-of-hello-sap-ase-deployment"></a>Hello SAP ASE 部署的結構
Hello 一般描述，根據 SAP ASE 可執行檔應該位於或安裝到 hello hello VM 基本 vhd 的系統磁碟機 (磁碟機 c:\)。 一般而言，大部分的 hello SAP ASE 系統和工具資料庫可不真的利用硬 SAP NetWeaver 工作量。 因此 hello 系統和工具的資料庫 （master、 model、 saptools、 sybmgmtdb、 sybsystemdb） 可留在 hello C:\drive 上。

例外狀況可能是包含所有的工作資料表和暫存資料表建立的 SAP ASE 其中發生某些 SAP ERP 和所有 BW 工作量可能需要較高的資料量或 I/O 作業量，無法放入 hello 原始 hello 暫存資料庫VM 的基底 VHD (磁碟機 c:\)。

根據 hello SAPInst/SWPM 使用新版 tooinstall hello 系統、 hello 資料庫可能包含：

* 安裝 SAP ASE 時建立單一的 SAP ASE tempdb
* 建立藉由安裝 SAP ASE 和建立 hello SAP 安裝常式的其他 saptempdb SAP ASE tempdb
* 建立藉由安裝 SAP ASE 和手動建立額外的 tempdb SAP ASE tempdb (例如下列 「 SAP 附註[1752266]) toomeet ERP/BW 特定 tempdb 需求

如果發生特定 ERP 或所有 BW 工作量合理，不管 tooperformance tookeep hello tempdb 裝置 hello 另外建立 tempdb （SWPM 或手動） 以外 C:\ 磁碟機上。 如果沒有其他的 tempdb 已存在，則建議一個 toocreate (SAP 附註[1752266])。

這類系統 hello 應該 hello 另外建立 tempdb 上執行下列步驟：

* 移動 hello 第一個 tempdb toohello 第一個裝置的 hello SAP 資料庫
* 新增 tempdb 裝置 tooeach 的 hello Vhd，含 hello SAP 資料庫的裝置

此設定可讓 tempdb tooeither 耗用較多的空間，比可以 tooprovide hello 系統磁碟機。 做為參考其中一個可以檢查現有的系統執行內部部署的 hello tempdb 裝置大小。 或者，這種組態會啟用對 tempdb 無法隨附 hello 系統磁碟機的 IOPS 數目。 再次執行內部部署的系統可以針對 tempdb 使用的 toomonitor I/O 工作負載。

永遠不會將任何 SAP ASE 裝置放置到 hello hello VM 的 D:\ 磁碟機。 即使保留在 hello tempdb 中的 hello 物件只是暫時性的這也適用於 toohello tempdb。

#### <a name="impact-of-database-compression"></a>資料庫壓縮的影響
在組態中的 I/O 頻寬可能會變成限制因素，每個量值可減少 IOPS 可能有助於 toostretch hello 工作負載一次可以執行像是 Azure IaaS 案例中。 因此，強烈建議 toomake 確定 SAP ASE 壓縮會使用上傳現有的 SAP 資料庫 tooAzure 之前。

如果未實作上傳 tooAzure 之前 hello 建議 tooperform 壓縮是出於多種原因所造成：

* 資料上傳 toobe tooAzure hello 量較低
* hello hello 壓縮執行持續時間較短，假設有更多的 Cpu 或更高 I/O 頻寬或更少的 I/O 延遲內部部署可以使用更強的硬體
* 較小的資料庫大小可能會導致 tooless 成本進行磁碟配置

資料壓縮和 LOB 壓縮可以在 Azure 虛擬機器上裝載的 VM 中運作，如同它在內部部署中的運作方式。 如需有關如何 toocheck 如果壓縮已在使用中現有的 SAP ASE 資料庫請檢查 SAP Note [1750510]。

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>使用 DBACockpit toomonitor 資料庫執行個體
適用於 SAP 系統做為資料庫平台使用 SAP ASE hello DBACockpit 存取。 為交易 DBACockpit 中內嵌的瀏覽器視窗或 Webdynpro 不過 hello 完整功能，以監視並管理 hello 資料庫可用於只 hello DBACockpit hello Webdynpro 實作。

在內部部署與執行數個步驟的系統必須 tooenable hello DBACockpit hello Webdynpro 實作所使用的所有 SAP NetWeaver 功能。 請依照 SAP Note [1245200] tooenable hello webdynpros 的使用方式，並產生 hello 必要的。 當上述資訊，您也會設定 hello 網際網路通訊管理員 (icm) 以及 hello 連接埠 toobe hello 中的下列 hello 指示用於 http 和 https 連線。 hello http 的預設設定看起來像這樣：

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

和產生交易 DBACockpit 中的 hello 連結看起來類似 toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

取決於如何 hello Azure 虛擬機器裝載 hello SAP 系統連接的網站，透過多站台或 ExpressRoute （跨單位部署），您需要確定 toomake 該 ICM 可解析的完整主機名稱上使用 hello電腦嘗試 tooopen hello DBACockpit 從。 請參閱 SAP 附註[773830] toounderstand ICM 如何決定 hello 取決於設定檔參數和 icm host_name_full 方式設定參數的完整的主機名稱明確必要。

如果您部署的 hello VM 在僅限雲端的情況下，不在內部部署與 Azure 之間的跨單位連線，您需要 toodefine，公用 IP 位址和 domainlabel 也一樣。 hello hello 公用 DNS 名稱格式 hello VM 然後看起來像這樣：

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
>
>

可以找到 toohello DNS 名稱相關的更多詳細資料[這裡][virtual-machines-azurerm-versus-azuresm]。

設定 hello SAP 設定檔參數 icm/host_name_full toohello hello Azure VM hello 連結的 DNS 名稱可能類似於：

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

在此情況下您需要 toomake 務必：

* 新增輸入的規則 toohello 網路安全性群組中的 hello TCP/IP 通訊埠的 hello Azure 入口網站使用 icm toocommunicate
* 新增輸入的規則以 hello ICM hello TCP/IP 連接埠使用 toocommunicate 的 toohello Windows 防火牆設定

建議您使用自動匯入的所有可用的更正，tooperiodically 套用 hello 更正集合 SAP 附註適用於 tooyour SAP 版本：

* [1558958]
* [1619967]
* [1882376]

針對 SAP ASE DBA Cockpit 的進一步資訊位於下列 SAP 附註的 hello:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>SAP ASE 的備份/復原考量
將 SAP ASE 部署至 Azure 時，必須檢閱您的備份方法。 即使 hello 系統不是生產系統，SAP ASE 所裝載的 hello SAP 資料庫必須定期備份。 因為 Azure 儲存體會保留三個影像，備份現在是較不重要，尤其是尊重 toocompensating 儲存體損毀。 hello 維護適當的備份與還原計劃的主要原因是，您可以藉由提供時間復原功能的中點補償邏輯/手動錯誤有更多。 因此 hello 的目標是 tooeither 使用備份 toorestore hello 資料庫備份 tooa 特定點 Azure tooseed 中的時間或 toouse hello 備份中另一個系統複製 hello 現有的資料庫。 例如，您無法從傳輸的 2 層 SAP 組態 tooa 3 層系統設定 hello 相同系統還原的備份。

備份和還原 Azure 運作中的資料庫 hello 相同方式就如同內部部署。 請參閱 SAP 附註︰

* [1588316]
* [1585981]

以取得建立傾印組態和排程備份的詳細資料。 根據您的策略和需求，您可以設定資料庫和記錄檔傾印到其中一個現有的 Vhd 的 hello toodisk 或加入的額外 VHD hello 備份。  tooreduce hello 危險資料遺失，就會發生錯誤的建議 toouse 沒有資料庫裝置所在位置的 VHD。

除了資料壓縮與 LOB 壓縮之外，SAP ASE 也會提供備份壓縮。 與 hello 資料庫和記錄空間小於 toooccupy 傾印它建議 toouse 備份壓縮。 如需詳細資訊，請參閱 SAP 附註 [1588316] 。 壓縮 hello 備份也是重要的 tooreduce hello 數量資料 toobe 傳輸，如果您計劃 toodownload 備份或包含備份的傾印從 hello tooon 內部部署 Azure 虛擬機器的 Vhd。

請勿使用磁碟機 D:\ 做為資料庫或記錄傾印目的地。

#### <a name="performance-considerations-for-backupsrestores"></a>備份/還原的效能考量
裸機部署，如同備份/還原效能是取決於磁碟區數目可以讀取以平行方式，而且這些磁碟區的哪些 hello 輸送量可能。 此外，hello 備份壓縮所使用的 CPU 耗用量可能相當重要的角色上播放的 Vm 只向上 too8 CPU 執行緒。 因此，您可以假設︰

* hello 較少的 Vhd hello 數目使用 toostore hello 資料庫裝置 hello 較小 hello 整體讀取輸送量
* hello 數目較少 hello hello VM 中的 CPU 執行緒、 hello 更嚴重 hello 備份壓縮的影響
* hello 較少 （等量磁碟區的目錄、 Vhd） 的目標 toowrite hello 備份、 hello 較小者 hello 輸送量

目標 toowrite toothere tooincrease hello 數目是它可以是根據您的需求使用/結合兩個選項：

* 透過順序 tooimprove hello IOPS 輸送量該等量磁碟區上的多個已掛接 Vhd 的條狀配置 hello 備份目標磁碟區
* 使用多個目標目錄 toowrite hello 傾印至 SAP ASE 層級建立的傾印組態

本指南的先前內容中已討論過在多個掛接的 VHD 上等量劃分磁碟區的方式。 如需有關使用 hello SAP ASE 傾印組態中的多個目錄，請參閱 toohello 文件，也就是使用的 toocreate hello 傾印組態上 hello 預存程序 sp_config_dump 上[Sybase 資訊中心](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>使用 Azure VM 的災害復原
#### <a name="data-replication-with-sap-sybase-replication-server"></a>利用 SAP Sybase 複寫伺服器的資料複寫
以 hello SAP Sybase 複寫伺服器 (SRS) SAP ASE 提供暖待命方案 tootransfer 資料庫交易 tooa 遠方位置，以非同步方式。

hello 安裝及操作 SRS 的運作方式也會在內部部署，在 Azure 虛擬機器服務中裝載的 VM 中的功能。

預計未來會發行透過 SAP 複寫伺服器的 ASE HADR 版本。 一旦該版本可供使用之後，就會立即進行測試並針對 Microsoft Azure 平台加以發行。

## <a name="specifics-toosap-ase-on-linux"></a>在 Linux 上的細節 tooSAP ASE
開始使用 Microsoft Azure，您可以輕鬆地移轉您現有的 SAP ASE 應用程式 tooAzure 虛擬機器。 虛擬機器中的 SAP ASE 可輕鬆地將移轉這些應用程式 tooMicrosoft Azure 讓您 tooreduce hello 擁有權總成本的部署、 管理和維護的企業廣度應用程式。 透過 SAP ASE Azure 虛擬機器中，系統管理員和開發人員仍然可以使用的 hello 可用的相同開發和管理工具內部。

部署 Azure Vm 的重要 tooknow hello 正式的 Sla，可以在這裡找到： <https://azure.microsoft.com/support/legal/sla>

SAP 附註 [1928533]將會提供 SAP 大小調整資訊和 SAP 認證的 VM SKU 清單。 Azure 虛擬機器的額外 SAP 調整大小文件可以在下列網址中找到：<http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> 和 <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

陳述式和 Azure 儲存體、 SAP 部署 Vm 或 SAP Monitoring 的建議考慮 toohello 使用量套用 toodeployments 的 SAP ASE 搭配述整個 hello 的這份文件的前四個章節的 SAP 應用程式。

hello 下列兩個 SAP 附註上 Linux 和 ASE ASE 的一般資訊中包含 hello 雲端：

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>SAP ASE 版本支援
SAP 目前支援 SAP ASE 版本 16.0，可與 SAP 商務套件產品搭配使用。 SAP ASE 伺服器、 或 JDBC 和 ODBC 驅動程式 toobe SAP Business Suite 等作業只透過所提供的產品搭配使用的所有更新都 hello 在 SAP 服務 Marketplace: <https://support.sap.com/swdc>。

安裝與內部部署，不要直接從 Sybase 網站下載更新 hello SAP ASE 伺服器或 hello JDBC 和 ODBC 驅動程式。 支援使用 SAP Business Suite 產品在內部部署與 Azure 虛擬機器中的修補程式的詳細資訊，請參閱下列 「 SAP 附註的 hello:

* [1590719]
* [1973241]

SAP ASE 上執行 SAP Business Suite 的一般資訊位於 hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 相關之 SAP ASE 的 SAP ASE 組態指導方針
#### <a name="structure-of-hello-sap-ase-deployment"></a>Hello SAP ASE 部署的結構
Hello 一般描述，根據 SAP ASE 可執行檔應該位於或安裝到 VM (/sybase) hello hello 根檔案系統。 一般而言，大部分的 hello SAP ASE 系統和工具資料庫可不真的利用硬 SAP NetWeaver 工作量。 因此 hello 系統和工具的資料庫 （master、 model、 saptools、 sybmgmtdb、 sybsystemdb） 可留在 hello 根檔案系統上。

例外狀況可能是包含所有的工作資料表和暫存資料表建立的 SAP ASE 其中發生某些 SAP ERP 和所有 BW 工作量可能需要較高的資料量或 I/O 作業量，無法放入 hello 原始 hello 暫存資料庫VM 之 OS 磁碟。

根據 hello SAPInst/SWPM 使用新版 tooinstall hello 系統、 hello 資料庫可能包含：

* 安裝 SAP ASE 時建立單一的 SAP ASE tempdb
* 建立藉由安裝 SAP ASE 和建立 hello SAP 安裝常式的其他 saptempdb SAP ASE tempdb
* 建立藉由安裝 SAP ASE 和手動建立額外的 tempdb SAP ASE tempdb (例如下列 「 SAP 附註[1752266]) toomeet ERP/BW 特定 tempdb 需求

如果發生特定 ERP 或所有 BW 工作量合理，不管 tooperformance tookeep hello tempdb 裝置 hello 另外建立 tempdb （SWPM 或手動） 可以由單一 Azure 資料磁碟或 Linux RAID 的個別的檔案系統上的跨越多個 Azure 資料磁碟。 如果沒有其他的 tempdb 已存在，則建議一個 toocreate (SAP 附註[1752266])。

這類系統 hello 應該 hello 另外建立 tempdb 上執行下列步驟：

* 移動 hello 第一次 tempdb 目錄 toohello 第一個檔案系統的 hello SAP 資料庫
* 新增 hello Vhd，含 hello SAP 資料庫的檔案系統的 tempdb 目錄的 tooeach

此設定可讓 tempdb tooeither 耗用較多的空間，比可以 tooprovide hello 系統磁碟機。 做為參考其中一個可以檢查現有的系統執行內部部署的 hello tempdb 目錄大小。 或者，這種組態會啟用對 tempdb 無法隨附 hello 系統磁碟機的 IOPS 數目。 再次執行內部部署的系統可以針對 tempdb 使用的 toomonitor I/O 工作負載。

永遠不會放入 /mnt 或 /mnt/resource 的 hello VM 的任何 SAP ASE 目錄。 即使 hello 物件保留在 hello tempdb 中只有暫時因為 /mnt 或 /mnt/resource 預設 Azure VM 暫存空間這不是永久性的這也適用於 toohello tempdb。 位於 hello Azure VM 的暫存空間更多詳細[這篇文章][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>資料庫壓縮的影響
在組態中的 I/O 頻寬可能會變成限制因素，每個量值可減少 IOPS 可能有助於 toostretch hello 工作負載一次可以執行像是 Azure IaaS 案例中。 因此，強烈建議 toomake 確定 SAP ASE 壓縮會使用上傳現有的 SAP 資料庫 tooAzure 之前。

如果未實作上傳 tooAzure 之前 hello 建議 tooperform 壓縮是出於多種原因所造成：

* 資料上傳 toobe tooAzure hello 量較低
* hello hello 壓縮執行持續時間較短，假設有更多的 Cpu 或更高 I/O 頻寬或更少的 I/O 延遲內部部署可以使用更強的硬體
* 較小的資料庫大小可能會導致 tooless 成本進行磁碟配置

資料壓縮和 LOB 壓縮可以在 Azure 虛擬機器上裝載的 VM 中運作，如同它在內部部署中的運作方式。 如需有關如何 toocheck 如果壓縮已在使用中現有的 SAP ASE 資料庫請檢查 SAP Note [1750510]。 另請參閱 SAP 附註 [2121797] ，以取得有關資料庫壓縮的其他資訊。

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>使用 DBACockpit toomonitor 資料庫執行個體
適用於 SAP 系統做為資料庫平台使用 SAP ASE hello DBACockpit 存取。 為交易 DBACockpit 中內嵌的瀏覽器視窗或 Webdynpro 不過 hello 完整功能，以監視並管理 hello 資料庫可用於只 hello DBACockpit hello Webdynpro 實作。

在內部部署與執行數個步驟的系統必須 tooenable hello DBACockpit hello Webdynpro 實作所使用的所有 SAP NetWeaver 功能。 請依照 SAP Note [1245200] tooenable hello webdynpros 的使用方式，並產生 hello 必要的。 當上述資訊，您也會設定 hello 網際網路通訊管理員 (icm) 以及 hello 連接埠 toobe hello 中的下列 hello 指示用於 http 和 https 連線。 hello http 的預設設定看起來像這樣：

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

和產生交易 DBACockpit 中的 hello 連結看起來類似 toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

取決於如何 hello Azure 虛擬機器裝載 hello SAP 系統連接的網站，透過多站台或 ExpressRoute （跨單位部署），您需要確定 toomake 該 ICM 可解析的完整主機名稱上使用 hello電腦嘗試 tooopen hello DBACockpit 從。 請參閱 SAP 附註[773830] toounderstand ICM 如何決定 hello 取決於設定檔參數和 icm host_name_full 方式設定參數的完整的主機名稱明確必要。

如果您部署的 hello VM 在僅限雲端的情況下，不在內部部署與 Azure 之間的跨單位連線，您需要 toodefine，公用 IP 位址和 domainlabel 也一樣。 hello hello 公用 DNS 名稱格式 hello VM 然後看起來像這樣：

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
>
>

可以找到 toohello DNS 名稱相關的更多詳細資料[這裡][virtual-machines-azurerm-versus-azuresm]。

設定 hello SAP 設定檔參數 icm/host_name_full toohello hello Azure VM hello 連結的 DNS 名稱可能類似於：

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

在此情況下您需要 toomake 務必：

* 新增輸入的規則 toohello 網路安全性群組中的 hello TCP/IP 通訊埠的 hello Azure 入口網站使用 icm toocommunicate
* 新增輸入的規則以 hello ICM hello TCP/IP 連接埠使用 toocommunicate 的 toohello Windows 防火牆設定

建議您使用自動匯入的所有可用的更正，tooperiodically 套用 hello 更正集合 SAP 附註適用於 tooyour SAP 版本：

* [1558958]
* [1619967]
* [1882376]

針對 SAP ASE DBA Cockpit 的進一步資訊位於下列 SAP 附註的 hello:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>SAP ASE 的備份/復原考量
將 SAP ASE 部署至 Azure 時，必須檢閱您的備份方法。 即使 hello 系統不是生產系統，SAP ASE 所裝載的 hello SAP 資料庫必須定期備份。 因為 Azure 儲存體會保留三個影像，備份現在是較不重要，尤其是尊重 toocompensating 儲存體損毀。 hello 維護適當的備份與還原計劃的主要原因是，您可以藉由提供時間復原功能的中點補償邏輯/手動錯誤有更多。 因此 hello 的目標是 tooeither 使用備份 toorestore hello 資料庫備份 tooa 特定點 Azure tooseed 中的時間或 toouse hello 備份中另一個系統複製 hello 現有的資料庫。 例如，您無法從傳輸的 2 層 SAP 組態 tooa 3 層系統設定 hello 相同系統還原的備份。

備份和還原 Azure 運作中的資料庫 hello 相同方式就如同內部部署。 請參閱 SAP 附註︰

* [1588316]
* [1585981]

以取得建立傾印組態和排程備份的詳細資料。 根據您的策略和需求，您可以設定資料庫和記錄檔傾印到其中一個現有的 Vhd 的 hello toodisk 或加入的額外 VHD hello 備份。  tooreduce hello 危險資料遺失，就會發生錯誤的建議 toouse 沒有資料庫目錄/檔案所在位置的 VHD。

除了資料壓縮與 LOB 壓縮之外，SAP ASE 也會提供備份壓縮。 與 hello 資料庫和記錄空間小於 toooccupy 傾印它建議 toouse 備份壓縮。 如需詳細資訊，請參閱 SAP 附註 [1588316] 。 壓縮 hello 備份也是重要的 tooreduce hello 數量資料 toobe 傳輸，如果您計劃 toodownload 備份或包含備份的傾印從 hello tooon 內部部署 Azure 虛擬機器的 Vhd。

請勿使用 hello Azure VM 的暫存空間 /mnt 或 /mnt/resource 做為資料庫或記錄檔傾印目的地。

#### <a name="performance-considerations-for-backupsrestores"></a>備份/還原的效能考量
裸機部署，如同備份/還原效能是取決於磁碟區數目可以讀取以平行方式，而且這些磁碟區的哪些 hello 輸送量可能。 此外，hello 備份壓縮所使用的 CPU 耗用量可能相當重要的角色上播放的 Vm 只向上 too8 CPU 執行緒。 因此，您可以假設︰

* hello 較少的 Vhd hello 數目使用 toostore hello 資料庫裝置 hello 較小 hello 整體讀取輸送量
* hello 數目較少 hello hello VM 中的 CPU 執行緒、 hello 更嚴重 hello 備份壓縮的影響
* hello 較少的目標 （Linux 軟體 RAID Vhd） toowrite hello 來備份、 hello 較小者 hello 輸送量

目標 toowrite toothere tooincrease hello 數目是它可以是根據您的需求使用/結合兩個選項：

* 透過順序 tooimprove hello IOPS 輸送量該等量磁碟區上的多個已掛接 Vhd 的條狀配置 hello 備份目標磁碟區
* 使用多個目標目錄 toowrite hello 傾印至 SAP ASE 層級建立的傾印組態

本指南的先前內容中已討論過在多個掛接的 VHD 上等量劃分磁碟區的方式。 如需有關使用 hello SAP ASE 傾印組態中的多個目錄，請參閱 toohello 文件，也就是使用的 toocreate hello 傾印組態上 hello 預存程序 sp_config_dump 上[Sybase 資訊中心](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>使用 Azure VM 的災害復原
#### <a name="data-replication-with-sap-sybase-replication-server"></a>利用 SAP Sybase 複寫伺服器的資料複寫
以 hello SAP Sybase 複寫伺服器 (SRS) SAP ASE 提供暖待命方案 tootransfer 資料庫交易 tooa 遠方位置，以非同步方式。

hello 安裝及操作 SRS 的運作方式也會在內部部署，在 Azure 虛擬機器服務中裝載的 VM 中的功能。

目前不支援透過 SAP 複寫伺服器的 ASE HADR。 它可能會進行測試並發行中 hello 未來的 Microsoft Azure 平台。

## <a name="specifics-toooracle-database-on-windows"></a>細節 tooOracle Windows 上的資料庫
因為 midyear 2013，Microsoft Windows HYPER-V 和 Azure 的 Oracle toorun 支援 Oracle 軟體。 請閱讀此文章 tooget hello 一般支援 Windows HYPER-V 和 Azure 的 Oracle 上更多詳細資料： <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

下列 hello 一般支援，是也支援 hello 的 SAP 應用程式利用 Oracle 資料庫的特定案例。 這一部分 hello 文件中命名詳細資料。

### <a name="oracle-version-support"></a>Oracle 版本支援
Oracle 版本和對應可以找到下列 SAP 附註的 hello 中的 Oracle 在 Azure 虛擬機器上執行 SAP 支援的作業系統版本的所有詳細[2039619]

如需有關在 Oracle 上執行「SAP 商務套件」的一般資訊，請參閱 SCN：<https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 的 Oracle 組態指導方針
#### <a name="storage-configuration"></a>儲存體組態
只支援 Oracle 使用 NTFS 格式化磁碟的單一執行個體。 所有資料庫檔案必須都儲存 VHD 磁碟為基礎的 hello NTFS 檔案系統上。 這些 Vhd 掛接的 toohello Azure VM 作業，而且根據 Azure 分頁 BLOB 儲存體 (<https://msdn.microsoft.com/library/azure/ee691964.aspx>)。
任何類型的網路磁碟機或遠端共用 (例如 Azure 檔案服務)：

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

就 Oracle 資料庫檔案而言，都「不」  支援使用！

使用根據 Azure 分頁 BLOB 儲存體的 Azure Vhd，hello 的文件章節中所做的陳述式[Vm 和 Vhd 的快取][ dbms-guide-2.1]和[Microsoft Azure 儲存體][dbms-guide-2.3]套用 toodeployments 以 hello 以及 Oracle 資料庫。

如同稍早在 hello hello 文件的一般組件中所說明，存在 Azure Vhd 的 IOPS 輸送量的配額。 hello 確切配額會根據 hello VM 類型使用。 如需 VM 類型及其配額的清單，請參閱[這裡][virtual-machines-sizes]

tooidentify hello 支援的 Azure VM 類型，請參閱 tooSAP 注意[1928533]

每個磁碟 hello 目前 IOPS 配額滿足 hello 需求，因為它是可能 toostore 上的所有 hello DB 檔案一個單一掛接 Azure VHD。

如果需要更多的 IOPS，強烈建議 toouse 視窗儲存集區 （只可用在 Windows Server 2012 和更新版本） 或 Windows 等量的 Windows 2008 R2 toocreate 一個大的邏輯裝置透過多個已掛接的 VHD 磁碟。 另請參閱本文件的[軟體 RAID][dbms-guide-2.2] 一章。 這種方法可以簡化 hello 管理負擔 toomanage hello 磁碟空間，並避免 hello 投入時間 toomanually 散佈到多個已掛接的 Vhd 檔案。

#### <a name="backup--restore"></a>備份 / 還原
備份 / 還原功能、 hello SAP BR * 工具支援 Oracle 為 hello 相同方式與在標準的 Windows 伺服器作業系統和 HYPER-V。 Toodisk 備份與還原自磁碟也支援 oracle 復原管理員 (RMAN)。

#### <a name="high-availability"></a>高可用性
[comment]: <> (連結會參考 tooASM)
基於高可用性和災害復原目的支援 Oracle Data Guard。 如需詳細資料，請參閱[這份][virtual-machines-windows-classic-configure-oracle-data-guard]文件。

#### <a name="other"></a>其他
此文件以 hello 以及 Oracle 資料庫的 Vm 部署的前三個章節述 hello 適用於所有其他的一般主題如同 Azure 可用性設定組或 SAP 的監視。

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>環境的 hello Windows 上的 SAP MaxDB 資料庫
### <a name="sap-maxdb-version-support"></a>SAP MaxDB 版本支援
SAP 目前支援 SAP MaxDB 版本 7.9，以便與 Azure 中 SAP NetWeaver 架構的產品搭配使用。 在 SAP 服務商場提供 SAP MaxDB 伺服器、 或 JDBC 和 ODBC 驅動程式 toobe SAP NetWeaver 架構的產品搭配使用的所有更新等作業只透過 hello <https://support.sap.com/swdc>。
如需有關在 SAP MaxDB 上執行 SAP NetWeaver 的一般資訊，請參閱 <https://scn.sap.com/community/maxdb>。

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>針對 SAP MaxDB DBMS 支援的 Microsoft Windows 版本和 Azure VM 類型
在 Azure 上 SAP MaxDB DBMS toofind hello 支援 Microsoft Windows 版本，請參閱：

* [SAP 產品可用性對照表 (PAM)][sap-pam]
* SAP 附註 [1928533]

強烈建議 toouse hello 最新版本的 hello 作業系統 Microsoft Windows 中，這是 Microsoft Windows 2012 R2。

### <a name="available-sap-maxdb-documentation"></a>可用的 SAP MaxDB 文件
您可以找到下列 SAP 附註的 hello hello 更新 SAP MaxDB 文件清單[767598]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 的 SAP MaxDB 組態指導方針
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>儲存體組態
SAP MaxDB 的 azure 儲存體最佳作法，請依照下列章節中所述的 hello 一般建議[RDBMS 部署結構][dbms-guide-2]。

> [!IMPORTANT]
> 如同其他資料庫，SAP MaxDB 也有資料和記錄檔。 不過，在 SAP MaxDB 用語 hello 正確詞彙是 「 磁碟區 」 （非 「 檔案 」）。 例如，有 SAP MaxDB 資料磁碟區和記錄磁碟區。 請勿與作業系統磁碟區混淆。
>
>

簡單地說，您必須︰

* 設定太保存 hello SAP MaxDB 資料和記錄磁碟區 （也就是檔案） 的 hello Azure 儲存體帳戶**本機備援儲存體 (LRS)**章節中所指定[Microsoft Azure 儲存體][ dbms-guide-2.3].
* 從記錄檔磁碟區 （也就是檔案） 的 hello IO 路徑 SAP MaxDB 資料磁碟區 （也就是檔案） 的個別 hello IO 路徑。 這表示 SAP MaxDB 資料磁碟區 （也就是檔案） 有一個邏輯磁碟機上安裝的 toobe，而且 SAP MaxDB 記錄磁碟區 （也就是檔案） 有 toobe 安裝在另一個邏輯磁碟機。
* 設定 hello 適當的檔案快取每一個 Azure blob，是否使用它的 SAP MaxDB 資料或記錄檔磁碟區 （也就是 「 檔案 」），以及您是否使用標準 Azure 或 Azure 高階儲存體，根據的章節中所述[Vm 的快取][dbms-guide-2.1].
* 只要每個磁碟 hello 目前 IOPS 配額滿足 hello 需求，可能 toostore 所有 hello 資料磁碟區，在單一的掛接 Azure VHD，並也儲存在另一個單一掛接 Azure VHD 上的所有資料庫記錄檔磁碟區。
* 如果需要更多的 IOPS 及/或空格，強烈建議 toouse Microsoft 視窗儲存集區 （只用於 Microsoft Windows Server 2012 和更新版本） 或 Microsoft Windows 的 Microsoft Windows 2008 R2 toocreate 的條狀配置一個大型的邏輯裝置透過多個已掛接的 VHD 磁碟。 另請參閱本文件的[軟體 RAID][dbms-guide-2.2] 一章。 這種方法可以簡化 hello 管理負擔 toomanage hello 磁碟空間，並避免 hello 投入時間的手動將檔案分散到多個已掛接的 Vhd。
* 如需最高 IOPS 需求 hello，您可以使用 Azure 高階儲存體，DS 系列和 GS 系列 Vm 上。

![適用於 SAP MaxDB DBMS 之 Azure IaaS VM 的參考組態][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>備份與還原
將 SAP MaxDB 部署至 Azure 時，您必須檢閱備份方法。 即使 hello 系統不是生產系統，SAP MaxDB 所裝載的 hello SAP 資料庫必須定期備份。 由於 Azure 儲存體會保留三個映像，因此在保護系統以免發生儲存體失敗以及更重要的操作或系統管理失敗方面，備份現在已變得較不重要。 hello 維護適當的備份與還原計劃的主要原因是，讓您可以藉由提供時間點復原功能的邏輯或手動錯誤補償。 Hello 的目標是讓 tooeither 使用備份 toorestore hello 資料庫 tooa 特定點 Azure tooseed 中的時間或 toouse hello 備份中的另一個系統複製 hello 現有的資料庫。 例如，您無法從傳輸的 2 層 SAP 組態 tooa 3 層系統設定 hello 相同系統還原的備份。

備份和還原 Azure works hello 相同方式如同對內部部署系統，因此您可以使用標準的 SAP MaxDB 備份/還原工具，如下所述其中 hello SAP MaxDB 文件集文件中的資料庫所列於 SAP Note [767598].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>備份與還原的效能考量
與裸機部署備份和還原效能是取決於磁碟區數目可以讀取這些磁碟區的平行和 hello 輸送量。 此外，備份壓縮所使用的 CPU 耗用量 hello 可以播放相當重要的角色與 Vm 上 too8 CPU 執行緒。 因此，您可以假設︰

* hello 使用 Vhd toostore hello 資料庫裝置的較少 hello 數目、 hello 較低的 hello 整體讀取輸送量
* hello 數目較少 hello hello VM 中的 CPU 執行緒、 hello 更嚴重 hello 備份壓縮的影響
* hello 較少 （等量磁碟區的目錄、 Vhd） 的目標 toowrite hello 備份至 hello hello 輸送量更低

tooincrease hello 數目為目標來 toowrite，有兩個選項，您可以使用，可能是在組合中，根據您的需求：

* 專門用來備份的個別磁碟區
* 透過順序 tooimprove hello IOPS 輸送量等量的磁碟區上的多個已掛接 Vhd 的條狀配置 hello 備份目標磁碟區
* 有適用於下列各項的個別專用邏輯磁碟裝置︰
  * SAP MaxDB 備份磁碟區 (也就是檔案)
  * SAP MaxDB 資料磁碟區 (也就是檔案)
  * SAP MaxDB 記錄磁碟區 (也就是檔案)

關於在多個掛接的 VHD 上等量劃分磁碟區，先前在本文件的[軟體 RAID][dbms-guide-2.2] 一章中已討論過。

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>其他
中所述 hello 與 hello SAP MaxDB 資料庫的 Vm 部署此文件的前三個章節，也適用於所有其他的一般主題例如 Azure 可用性設定組或 SAP 的監視。
其他 SAP MaxDB 特定設定透明 tooAzure vm，而且不同於 SAP Note 列出的文件中描述[767598]和在這些 SAP 附註：

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Windows 上 SAP liveCache 專屬的詳細資料
### <a name="sap-livecache-version-support"></a>SAP liveCache 版本支援
「Azure 虛擬機器」中支援的 SAP liveCache 最低版本是針對 **EhP 2 for SAP SCM 7.0** 和更新版本發行的 **SAP LC/LCAPPS 10.0 SP 25** (包括 **liveCache 7.9.08.31** 和 **LCA-Build 25**)。

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>針對 SAP liveCache DBMS 支援的 Microsoft Windows 版本和 Azure VM 類型
在 Azure 上 SAP liveCache toofind hello 支援 Microsoft Windows 版本，請參閱：

* [SAP 產品可用性對照表 (PAM)][sap-pam]
* SAP 附註 [1928533]

強烈建議 toouse hello 最新版本的 hello 作業系統 Microsoft Windows 中，這是 Microsoft Windows 2012 R2。

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 的 SAP liveCache 組態指導方針
#### <a name="recommended-azure-vm-types"></a>建議的 Azure VM 類型
因為 SAP liveCache 是執行大量計算的應用程式，hello 容量和速度的 RAM 與 CPU 會有對 SAP liveCache 效能的主要影響。

針對 SAP 所支援的 hello Azure VM 類型 (SAP 附註[1928533])，所有的虛擬 CPU 資源配置的 toohello VM 都由專用的 hello hypervisor 實體的 CPU 資源。 不會產生過度佈建 (因此不會產生 CPU 資源競爭)。

同樣地，SAP 支援的所有 Azure VM 執行個體類型，hello VM 記憶體都是對應的 100 %toohello 實體記憶體 – 過度佈建 （超額認可），例如，未使用。

從這個觀點來看強烈建議 toouse hello 新 D 系列或 DS 系列 （以與 Azure 高階儲存體一起使用） 的 Azure VM 類型，因為它們有 60%更快的處理器比 hello A 系列。 Hello 最高的 RAM 和 CPU 負載，您可以使用 G 系列和最新 Intel® Xeon® 處理器 hello E5 v3 系列兩次 hello 記憶體，而且四次 hello 固態磁碟機 (Ssd) 的儲存 hello D （在搭配 Azure 高階儲存體） 的 GS 系列 Vm /DS 系列。

#### <a name="storage-configuration"></a>儲存體組態
因為 SAP liveCache 根據 SAP MaxDB 技術，所有 hello Azure 儲存體的最佳作法建議章節中所述的 SAP MaxDB[儲存體設定][ dbms-guide-8.4.1]也都適用於 SAP liveCache。

#### <a name="dedicated-azure-vm-for-livecache"></a>liveCache 專用的 Azure VM
因為 SAP liveCache 密集使用計算能力，正式上線使用強烈建議 toodeploy 專用 Azure 虛擬機器上。

![適用於具生產力使用案例的 liveCache 專用的 Azure VM][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>備份與還原
備份和還原，包括效能考量，已詳述於 hello 相關的 SAP MaxDB 章節[備份和還原][ dbms-guide-8.4.2]和[備份的效能考量還原和][dbms-guide-8.4.3]。

#### <a name="other"></a>其他
其他一般的主題已詳述於 hello 相關 SAP MaxDB[這][ dbms-guide-8.4.4]章節。

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>環境的 hello Windows 上的 SAP 內容伺服器
hello SAP 內容伺服器是個別伺服器元件 toostore 內容，例如以不同格式的電子文件。 hello SAP 內容伺服器提供所開發的技術，而且只使用 toobe 跨應用程式的任何 SAP 應用程式。 它會安裝於不同的系統上。 一般內容定型資料和從知識倉儲或技術的繪圖源自 hello mySAP PLM 文件管理系統的文件。

### <a name="sap-content-server-version-support"></a>SAP 內容伺服器版本支援
SAP 目前支援：

* **SAP 內容伺服器**版本 **6.50 (和更新版本)**
* **SAP MaxDB 版本 7.9**
* **Microsoft IIS (網際網路資訊伺服器) 版本 8.0 (和更新版本)**

強烈建議 toouse hello 最新版本的 SAP 內容伺服器，這在撰寫本文件的 hello 階段是**6.50 SP4**，與 hello 最新版本的**Microsoft IIS 8.5**。

檢查 SAP 內容伺服器與 Microsoft IIS 的最新支援的 hello 版本 hello [SAP 產品可用性矩陣 」 (PAM)][sap-pam]。

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>針對 SAP 內容伺服器支援的 Microsoft Windows 和 Azure VM 類型
toofind 支援的 Windows 版本，在 Azure 上 SAP 內容伺服器時，請參閱：

* [SAP 產品可用性對照表 (PAM)][sap-pam]
* SAP 附註 [1928533]

強烈建議 toouse hello 最新版本的 Microsoft Windows，這在撰寫本文件的 hello 階段是**Windows Server 2012 R2**。

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 的 SAP 內容伺服器組態指導方針
#### <a name="storage-configuration"></a>儲存體組態
如果您設定 SAP 內容伺服器 toostore 檔案 hello SAP MaxDB 資料庫中，所有 Azure 儲存體最佳作法建議章節中所述的 SAP MaxDB[儲存體設定][ dbms-guide-8.4.1]也適用於 hello SAP 內容伺服器案例。

如果您設定 SAP 內容伺服器 toostore 檔案 hello 檔案系統中，則建議 toouse 專屬的邏輯磁碟機。 使用儲存空間可讓您 tooalso 增加邏輯磁碟的大小和 IOPS 輸送量中所述章節中[軟體 RAID][dbms-guide-2.2]。

#### <a name="sap-content-server-location"></a>SAP 內容伺服器位置
SAP 內容伺服器已部署在 hello toobe 相同的 Azure 地區和 hello SAP 系統部署所在的 Azure VNET。 您是否想 toodeploy SAP 內容伺服器元件專用的 Azure VM 上或在 hello hello SAP 系統執行所在的相同 VM，就可用 toodecide。

![SAP 內容伺服器專用的 Azure VM][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>SAP 快取伺服器位置
hello SAP 快取伺服器是額外的伺服器端元件 tooprovide 存取 too(cached) 文件在本機。 hello SAP 快取伺服器快取 SAP 內容伺服器 hello 文的件。 如果文件 toobe 擷取一次以上，從不同位置，這會是 toooptimize 網路流量。 hello 一般規則是該 hello SAP 快取伺服器必須存取 SAP 快取伺服器 hello toobe 實際關閉 toohello 用戶端。

您有兩個選擇：

1. **用戶端是後端 SAP 系統**如果設定的 tooaccess SAP 內容伺服器後端 SAP 系統，SAP 系統是一個用戶端。 SAP 系統和 SAP 內容伺服器部署在 hello 相同 Azure 地區 – hello 中的相同的 Azure 資料中心 – 它們是實際關閉 tooeach 其他。 因此，沒有任何需要 toohave 專用的 SAP 快取伺服器。 SAP UI （SAP GUI 或 web 瀏覽器） 的用戶端存取 hello SAP 系統直接與 hello SAP 系統從 hello SAP 內容伺服器的擷取文件。
2. **用戶端是在內部部署 web 瀏覽器**hello SAP 內容伺服器可以設定的 toobe 由 hello 網頁瀏覽器直接存取。 在此情況下，執行內部的網頁瀏覽器的用戶端 hello SAP 內容伺服器。 在內部部署資料中心與 Azure 資料中心會放置在不同實體位置 (其他理想的情況下關閉 tooeach) 中。 您的內部部署資料中心是透過 Azure 站台對站台 VPN 或 ExpressRoute 連線的 tooAzure。 雖然這兩個選項可提供安全的 VPN 網路連線 tooAzure，站台對站台網路連線不提供 hello 在內部部署資料中心與 hello Azure 資料中心之間的網路頻寬和延遲 SLA。 總存取 toodocuments toospeed，您可以執行 hello 下列其中一種：
   1. 安裝 SAP 快取伺服器在內部，請關閉 toohello 內部 web 瀏覽器 (選項[這][ dbms-guide-900-sap-cache-server-on-premises]圖)
   2. 設定 Azure ExpressRoute，提供內部部署的資料中心與 Azure 資料中心之間高速且低延遲的專用網路連接。

![選項 tooinstall SAP 快取伺服器在內部部署][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>備份 / 還原
如果您設定 hello SAP 內容伺服器 toostore 檔案 hello SAP MaxDB 資料庫中，hello 備份/還原程序和效能考量已詳述於 SAP MaxDB 章[備份和還原][dbms-guide-8.4.2]和章節[的備份和還原效能考量][dbms-guide-8.4.3]。

如果您設定 hello 檔案系統中的 hello SAP 內容伺服器 toostore 檔案，其中一個選項是 tooexecute 手動備份/還原 hello 整個檔案結構的 hello 文件的所在位置。 它是類似 tooSAP MaxDB 備份/還原，建議使用 toohave 專用的磁碟區備份的目的。

#### <a name="other"></a>其他
其他 SAP 內容伺服器的特定設定透明 tooAzure vm 和各種文件和 SAP 附註所述：

* <https://service.sap.com/contentserver>
* SAP 附註 [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>細節 tooIBM DB2 for luw 會在 Windows 上
使用 Microsoft Azure，您可以輕鬆地移轉現有 SAP 執行的應用程式在 IBM DB2 for Linux、 UNIX 和 Windows (LUW) tooAzure 虛擬機器。 透過在 IBM DB2 for luw 會 SAP、 管理員和開發人員仍然可以使用的 hello 可用的相同開發和管理工具內部。
一般資訊執行 SAP Business Suite IBM DB2 for luw 會位在 hello SAP 社群網路 (SCN) 在<https://scn.sap.com/community/db2-for-linux-unix-windows>。

如需有關 Azure 中 DB2 for LUW 上 SAP 的其他資訊和更新，請參閱 SAP 附註 [2233094]。

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>IBM DB2 for Linux, UNIX, and Windows 支援版本
當 DB2 版本為 10.5 時，支援 Microsoft Azure 虛擬機器中 IBM DB2 for LUW 上的 SAP。

如需支援的 SAP 產品和 Azure VM 類型資訊，請參閱 tooSAP 注意[1928533]。

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>在 Azure VM 中安裝 SAP 的 IBM DB2 for Linux, UNIX, and Windows 組態指導方針
#### <a name="storage-configuration"></a>儲存體組態
所有資料庫檔案必須都儲存 VHD 磁碟為基礎的 hello NTFS 檔案系統上。 這些 Vhd 會掛接的 toohello Azure VM，並以 Azure 分頁 BLOB 儲存體 (<https://msdn.microsoft.com/library/azure/ee691964.aspx>)。
任何種類的網路磁碟機或遠端共用像下列 Azure 檔案服務的 hello 就**不**支援資料庫檔案：

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

如果您使用根據 Azure 分頁 BLOB 儲存體的 Azure Vhd，hello 的文件章節中所做的陳述式[RDBMS 部署結構][ dbms-guide-2]也套用 toodeployments 以 hello IBM DB2 for luw 會資料庫。

如同稍早在 hello hello 文件的一般組件中所說明，存在 Azure Vhd 的 IOPS 輸送量的配額。 hello 確切的配額取決於 hello VM 類型使用。 如需 VM 類型及其配額的清單，請參閱[這裡][virtual-machines-sizes]

只要每個磁碟 hello 目前 IOPS 配額已足夠，它是所有 hello 資料庫檔案可能 toostore 一個單一掛接 Azure VHD。

效能考量也會參照 toochapter 資料安全性和效能考量的資料庫目錄 SAP 安裝指南中。

或者，您可以使用 Windows 儲存集區 （只可用在 Windows Server 2012 和更新版本） 或 Windows 2008 R2 的 Windows 條狀配置章節所述[軟體 RAID] [ dbms-guide-2.2]的這份文件toocreate 一個大邏輯裝置透過多個已掛接的 VHD 磁碟。
包含針對 sapdata 和 saptmp 目錄 hello DB2 儲存體路徑 hello 磁碟，您必須指定實體磁碟磁區大小為 512 KB。 使用 Windows 儲存集區，您必須建立 hello 存放集區以手動方式透過命令列介面使用 hello 參數"-LogicalSectorSizeDefault"。 如需詳細資訊，請參閱 <https://technet.microsoft.com/library/hh848689.aspx>。

#### <a name="backuprestore"></a>備份/還原
hello 備份/還原功能，對於 IBM DB2 for luw 會支援 hello 相同方式與在標準的 Windows 伺服器作業系統和 HYPER-V。

您必須確定您擁有恰當且有效的資料庫備份策略。

裸機部署，如同備份/還原效能取決於磁碟區數目可以讀取以平行方式，而且這些磁碟區的哪些 hello 輸送量可能。 此外，hello 備份壓縮所使用的 CPU 耗用量可能相當重要的角色上播放的 Vm 只向上 too8 CPU 執行緒。 因此，您可以假設︰

* hello 較少的 Vhd hello 數目使用 toostore hello 資料庫裝置 hello 較小 hello 整體讀取輸送量
* hello 數目較少 hello hello VM 中的 CPU 執行緒、 hello 更嚴重 hello 備份壓縮的影響
* hello 較少 （等量磁碟區的目錄、 Vhd） 的目標 toowrite hello 備份至 hello hello 輸送量更低

tooincrease hello 數到目標 toowrite，兩個選項可以根據需求使用/合併：

* 透過順序 tooimprove hello IOPS 輸送量該等量磁碟區上的多個已掛接 Vhd 的條狀配置 hello 備份目標磁碟區
* 使用多個目標目錄 toowrite hello 備份至

#### <a name="high-availability-and-disaster-recovery"></a>高可用性和災害復原
不支援 Microsoft Cluster Server (MSCS)。

支援 DB2 高可用性災害復原 (HADR)。 如有 hello 的 hello HA 組態的虛擬機器使用名稱解析，Azure 中的 hello 設定沒有差別是在內部部署的任何設定。 不建議 toorely 上只有 IP 解析。

請勿使用 Azure 市集異地複寫。 如需詳細資訊，請參閱 toochapter [Microsoft Azure 儲存體][ dbms-guide-2.3]和章節[高可用性和災害復原與 Azure Vm 搭配][ dbms-guide-3].

#### <a name="other"></a>其他
前三個章節的這份文件，以及部署的 Vm 與 IBM DB2 for luw 會述 hello 適用於所有其他的一般主題如同 Azure 可用性設定組或 SAP 的監視。

也請參閱 toochapter [SAP on Azure 摘要的 SQL Server 一般][dbms-guide-5.8]。
