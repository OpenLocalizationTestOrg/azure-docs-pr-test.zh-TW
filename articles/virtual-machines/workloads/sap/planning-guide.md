---
title: "aaaAzure 虛擬機器規劃和實作的 SAP NetWeaver |Microsoft 文件"
description: "SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
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

[deployment-guide]:deployment-guide.md
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
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
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

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

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

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
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
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
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
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
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
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
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Microsoft Azure 會讓公司 tooacquire 運算和存放裝置資源的最小時間沒有冗長的採購循環。 Azure 虛擬機器可讓公司 toodeploy 古典應用程式，例如 SAP NetWeaver 架構應用程式至 Azure，並擴充其可靠性和可用性，而不需要進一步的資源可以使用內部部署。 Azure 虛擬機器服務也支援跨單位連線，哪些啟用公司 tooactively 將 Azure 虛擬機器整合到他們的內部部署網域、 私人雲端和與其 SAP 系統版圖。
這份技術白皮書說明 hello 基本概念的 Microsoft Azure 虛擬機器提供規劃和實作考量在 Azure 中的 SAP NetWeaver 安裝的逐步解說，而在這種情況應該是 hello 文件 tooread 開始之前實際部署在 Azure 上 SAP NetWeaver。
平台提供 hello 紙張補充 hello SAP 安裝文件集和 SAP 附註，表示 hello 安裝和部署上的 SAP 軟體的主要資源。

## <a name="summary"></a>摘要
雲端運算廣泛使用的術語，取得從小型公司向上 toolarge 和一家跨國企業內 hello IT 產業日漸重要。

Microsoft Azure 為 hello 雲端服務平台，從 Microsoft 取得，它提供了各式各樣的新的可能性。 現在的客戶可以 toorapidly 佈建和取消佈建應用程式以 hello 雲端服務讓它們不受限制的 tootechnical 或預算限制。 而不是投入時間和預算硬體基礎結構中，公司可以專注於 hello 應用程式、 商務程序和它的優點的客戶與使用者。

透過 Microsoft Azure 虛擬機器服務，Microsoft 提供完整的基礎結構即服務 (IaaS) 平台。 Azure 虛擬機器 (IaaS) 支援以 SAP NetWeaver 為基礎的應用程式。 本白皮書說明如何 tooplan 和實作 SAP NetWeaver 架構的應用程式在 Microsoft Azure 中的做選擇的 hello 平台。

hello 紙張本身著重於兩個主要層面：

* hello 第一個部分會說明在 Azure 上 SAP NetWeaver 架構應用程式的兩個支援的部署模式。 也會說明考慮到 SAP 部署之一般處理 Azure 的方式。
* hello 第二個部分的詳細資料實作 hello 兩個不同的案例 hello 第一個部分中所述。

如需其他資源，請參閱本文的[資源][planning-guide-1.2]一章。

### <a name="definitions-upfront"></a>預先定義
在 hello 文件中，我們會使用下列詞彙的 hello:

* IaaS：基礎結構即服務
* PaaS：平台即服務
* SaaS：軟體即服務
* ARM：Azure Resource Manager
* SAP 元件︰個別 SAP 應用程式，例如 ECC、BW、Solution Manager 或 EP。  SAP 元件可以傳統 ABAP 或 Java 技術為基礎，或以非 NetWeaver 應用程式 (例如商務物件) 為基礎。
* SAP 環境： 一或多個 SAP 元件以邏輯方式分組 tooperform 商務功能，例如開發、 QAS、 訓練、 DR 或生產環境。
* SAP 版圖： 這是指 toohello 整個 SAP 資產中客戶的 IT 環境。 hello SAP 版圖包括所有生產和非生產環境。
* DBMS 層和應用程式層，例如 SAP ERP 開發系統、 SAP BW 測試系統、 SAP CRM 生產系統等的 SAP 系統： hello 組合.. 在 Azure 部署中，不支援的 toodivide 這些內部部署與 Azure 之間的兩個層級。 這表示 SAP 系統可以在內部部署或在 Azure 部署。 不過，您可以部署至 Azure 或內部部署 SAP 版圖的 hello 不同系統。 例如，您可以部署 hello SAP CRM 開發和測試系統在 Azure 中的，但是 hello SAP CRM 生產系統在內部。
* 僅限雲端部署： 部署其中 hello Azure 訂用帳戶未連線透過網站的站台或 ExpressRoute 連線 toohello 內部部署網路基礎結構。 在一般 Azure 文件中，這類部署也會描述為「僅限雲端」的部署。 採用這種方法部署的虛擬機器可透過存取 hello 網際網路和公用 IP 位址和/或公用 DNS 命名指派的 toohello Vm 在 Azure 中。 Microsoft windows hello 在內部部署 Active Directory (AD) 和 DNS 未延伸 tooAzure 在這些類型的部署。 因此 hello Vm 不屬於 hello 內部部署 Active Directory。 此規則也適用於使用像是 OpenLDAP + Kerberos 的 Linux 實作。

> [!NOTE]
> 本文中的僅限雲端部署定義成在 Azure 中以獨佔方式執行的完整 SAP 環境，而不會將 Active Directory/OpenLDAP 或名稱解析從內部部署擴充到公用雲端。 針對實際執行 SAP 系統或 SAP STMS 或其他內部部署資源需要 toobe 裝載在 Azure 與位於內部部署資源上的 SAP 系統之間使用的組態不支援僅限雲端的組態。
>
>

* 跨單位： 說明的案例，其中 Vm 是已部署的 tooan Azure 訂用帳戶具有站台對站台、 多站台或 ExpressRoute hello 在內部部署資料中心與 Azure 之間的連線能力。 在一般 Azure 文件中，這類部署也會描述為跨單位案例。 hello hello 連線的原因是 tooextend 在內部部署網域、 在內部部署 Active Directory/OpenLDAP 和內部部署 DNS 至 Azure。 hello 內部橫向是擴充的 toohello hello 訂用帳戶的 Azure 資產。 透過這樣延伸，hello Vm 可以是 hello 在內部部署網域的一部分。 Hello 在內部部署網域的網域使用者可以存取 hello 伺服器，並且可以執行服務那些 Vm （例如 DBMS 服務）。 但無法在內部部署的 VM 和 Azure 部署的 VM 之間進行通訊和名稱解析。 這是我們預期大部分 SAP 資產 toobe 部署中的 hello 案例。 如需詳細資訊，請參閱[這篇文章][vpn-gateway-cross-premises-options]和[這個主題][vpn-gateway-site-to-site-create]。

> [!NOTE]
> SAP 生產系統支援跨單位部署 SAP 系統，其中執行 SAP 系統的 Azure 虛擬機器是內部部署網域的成員。 跨單位組態可將部分或完整 SAP 環境部署到 Azure。 即使在 Azure 中執行 hello 完整的 SAP 環境，則需要具有這些 Vm 屬於內部部署網域和廣告/OpenLDAP。 在先前版本中的 hello 文件，我們剛才討論過混合式 IT 案例，其中 hello 詞彙 '混合' 已進行 root 破解 hello 事實會在內部部署與 Azure 之間的跨單位連線。 此外，該 hello Azure 中的 Vm 屬於 hello hello 事實內部部署 Active Directory / OpenLDAP。
>
>

有些 Microsoft 文件在描述跨單位案例時稍有不同，特別是針對 DBMS HA 組態。 在 hello 案例中的 hello SAP 相關文件，hello 跨內部單位案例只分布 toohaving 站對站或私人 (ExpressRoute) 連線和 hello 事實 hello SAP 版圖分散在內部部署和 Azure。  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>資源
hello 下列其他指南可供 Azure 上 SAP 部署的 hello 主題：

* [SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南 (本文件)][planning-guide]
* [SAP NetWeaver 的 Azure 虛擬機器部署][deployment-guide]
* [SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]

> [!IMPORTANT]
> 只要使用使用可能連結 toohello 參考 SAP 安裝指南 》 (Reference instguide-01，請參閱<http://service.sap.com/instguides>)。 當上線 toohello 必要條件和安裝程序，hello SAP NetWeaver 安裝指南 》，應該一律是本文件只包含安裝 Microsoft Azure 虛擬機器中的 SAP NetWeaver 系統的特定工作時，仔細閱讀。
>
>

Azure 上的 SAP 相關的 toohello 主題 hello 遵循 SAP 附註︰

| 附註編號 | 課程名稱 |
| --- | --- |
| [1928533] |Azure 上的 SAP 應用程式︰支援的產品和大小 |
| [2015553] |Microsoft Azure 上的 SAP：支援的必要條件 |
| [1999351] |疑難排解適用於 SAP 且已強化的 Azure 監視功能 |
| [2178632] |Microsoft Azure 上的 SAP 主要監視度量 |
| [1409604] |Windows 上的虛擬化︰增強型監視功能 |
| [2191498] |Linux 搭配 Azure 上的 SAP：增強型監視 |
| [2243692] |Microsoft Azure (IaaS) VM 上的 Linux：SAP 授權問題 |
| [1984787] |SUSE LINUX Enterprise Server 12：安裝注意事項 |
| [2002167] |Red Hat Enterprise Linux 7.x：安裝和升級 |
| [2069760] |Oracle Linux 7.x SAP 安裝和升級 |
| [1597355] |適用於 Linux 的交換空間建議 |

也會讀取 hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) for Linux 包含所有 SAP 附註。

有關 Azure 訂用帳戶的一般預設限制和最大限制，請參閱[這篇文章][azure-subscription-service-limits-subscription]。

## <a name="possible-scenarios"></a>可能的案例
SAP 通常會視為一個 hello 企業中最重要的應用程式。 hello 架構和作業，這些應用程式的大部分是非常複雜，並確定您符合可用性和效能的需求是相當重要。

因此，企業必須仔細了解哪種應用程式可以執行在公用雲端環境中，選擇 hello 雲端提供者的獨立 toothink。

以下列出可能在公用雲端環境中部署 SAP NetWeaver 應用程式的系統類型︰

1. 中型生產系統
2. 開發系統
3. 測試系統
4. 原型系統
5. 學習/示範系統

順序 toosuccessfully 中部署 SAP 系統到 Azure IaaS 或 IaaS 一般情況下，很重要的 toounderstand hello 明顯差異的傳統外包或主機服務提供者的供應項目 hello 和 IaaS 供應項目。 Hello 傳統主機服務提供者或外包適應基礎結構 （網路、 儲存體和伺服器類型） toohello 工作負載而客戶希望 toohost，改為 hello 客戶責任 toochoose hello 適當工作負載在 IaaS 部署。

第一個步驟中，客戶需要下列項目 tooverify hello:

* hello SAP 支援 Azure VM 的類型
* 在 Azure 上 hello SAP 支援的產品/版本
* hello hello Azure 中特定 SAP 版本支援 OS 和 DBMS 版本
* 不同 Azure SKU 所提供的 SAPS 輸送量

hello 答案 toothese 問題可以讀取於 SAP Note [1928533]。

在第二個步驟中，Azure 資源和頻寬限制必須 toobe 比較 tooactual 資源耗用量的內部部署系統。 因此，客戶需要 toobe 熟悉 hello 不同功能的 hello Azure hello 區域中的 SAP 支援的型別：

* 不同 VM 類型的 CPU 和記憶體資源，以及
* 不同 VM 類型的 IOPS 頻寬，以及
* 不同 VM 類型的網路功能。

您可以在[這裡 (Linux)][virtual-machines-sizes-linux] 和[這裡 (Windows)][virtual-machines-sizes-windows] 找到大部分的資料。

請記住，hello hello 上方的連結中所列的限制是上限。 它並不表示，任何 hello 資源 hello 限制，例如 IOPS 可以提供在所有情況下。 雖然 hello 例外狀況會是 hello 選擇 VM 類型的 CPU 和記憶體資源。 針對 SAP 所支援的 hello VM 類型，hello CPU 和記憶體資源都已保留，因此可用在任何時間點 hello VM 內耗用的時間。

hello 像其他 IaaS 平台的 Microsoft Azure 平台是多租用戶的平台。 這表示儲存體、網路和其他資源會在租用戶之間共用。 智慧型節點和配額邏輯是使用的 tooprevent 一個租用戶大幅影響 hello 效能的另一個租用戶 （雜訊像素）。 雖然 Azure 中的邏輯會試著頻寬 tookeep 差異小型的高度分享的平台通常 toointroduce 較大的變化資源/頻寬可用性中有許多客戶使用的 tooin 其內部部署。 如此一來，您可能會遇到分鐘 toominute 從不同層級有關網路或儲存體 I/O （hello 磁碟區，以及延遲） 的頻寬。 在 Azure 上的 SAP 系統，可能經歷較大的變化，比在內部部署系統中的 hello 機率需要 toobe 列入考量。

最後一個步驟是 tooevaluate 可用性需求。 這可能是，該 hello 基礎 Azure 基礎結構必須 tooget 更新，且必須執行重新啟動 Vm toobe hello 主機。 在這些情況下，也會關閉並重新啟動正在這些主機上執行的 VM。 hello 計時的這類的維護期間特定區域的非基本營業時間內完成，但較寬 hello 潛在窗口的幾個小時的期間將會重新啟動電腦。 有各種技術 hello 可能是 Azure 平台內設定 toomitigate 部分或所有 hello 這類更新的影響。 未來的增強功能的 hello Azure 平台的 DBMS 和 SAP 應用程式而設計的這類的重新啟動 toominimize hello 影響。

為了 toosuccessfully 部署到 Azure 的 SAP 系統、 hello 內部部署 SAP 系統的作業系統，資料庫和 SAP 應用程式必須出現在 hello SAP Azure 可以提供的支援矩陣，納入 hello 資源 hello Azure 基礎結構，以及哪些可與可用性 Sla Microsoft Azure 提供的 hello。 當識別出這些系統，您會需要 toodecide hello 下列兩個部署案例的其中一個上。

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>僅限雲端-無 hello 相依性的虛擬機器部署到 Azure 內部部署客戶網路
![在 Azure 中部署 SAP 示範或訓練案例的單一 VM][planning-guide-figure-100]

這個案例是典型的訓練或示範系統，SAP 和非 SAP 軟體的所有 hello 元件之單一 VM 內的都安裝位置。 此部署案例不支援 SAP 生產系統。 一般情況下，此案例符合下列需求的 hello:

* 您可存取透過 hello 公用網路內使用 hello Vm 本身。 Hello hello Vm toohello 內執行的應用程式的網路直接連線在內部網路的任一個的 hello 公司擁有 hello 示範或訓練內容或 hello 客戶不需要。
* 代表 hello 訓練或示範案例的多個 Vm，發生網路通訊和名稱解析必須 toowork hello Vm 之間。 但 hello 組的 Vm 之間的通訊需要 toobe 隔離，以便可以並存部署多組的 Vm，不受干擾。  
* Hello 終端使用者 tooremote 登入到 Azure 中裝載的 Vm toohello 需要網際網路連線。 Hello 客體作業系統，根據終端機服務/RDS 或 VNC/ssh 用 tooaccess hello VM tooeither 滿足 hello 訓練工作或執行 hello 示範。 如果 SAP 連接埠 3200、 3300 & 3600 可以例如也公開 hello SAP 應用程式執行個體可以存取從任何網際網路連線的桌面。
* hello SAP 系統 （和 VM(s)) 代表在 Azure 中只需要公用網際網路連線的使用者存取，而且不需要連接 tooother Vm 在 Azure 中的獨立案例。
* SAPGUI 和瀏覽器安裝並直接在 hello VM 上執行。
* 快速 VM toohello 原始狀態重設和新的部署該原始狀態再需要。
* 在示範和訓練案例的 hello 情況下，其中中實現多個 Vm，Active Directory /，就需要為每一組 Vm OpenLDAP 和 （或） DNS 服務。

![代表 Azure 雲端服務中一個示範或訓練案例的 VM 群組][planning-guide-figure-200]

請務必注意，在每個 hello hello VM tookeep 設定需要 toobe 部署以平行方式，其中每個 hello 組中的 hello VM 名稱是 hello 相同。

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>跨單位-部署的單一或多個 SAP Vm 至 Azure 且 hello 需求完全整合至 hello 與內部網路
![具有站對站連線能力的 VPN (跨單位)][planning-guide-figure-300]

此案例是具有許多可能之部署模式的跨單位案例。 它可以描述為做為 Azure 上執行 hello SAP 版圖在內部的某些部分和 hello SAP 環境的其他部分。 Hello 事實 hello SAP 元件的一部分會在 Azure 上執行的所有層面都應該都是透明的使用者。 因此 hello SAP 傳輸更正系統 (STMS)、 RFC 通訊、 列印、 安全性 （例如 SSO) 等一起順暢運作的 hello SAP 系統在 Azure 上執行。 但 hello 跨內部單位案例也說明其中 hello 完整的 SAP 環境在 Azure 中執行與 hello 客戶的網域和 DNS 延伸至 Azure 的案例。

> [!NOTE]
> 這是 hello 部署案例，這支援執行生產性 SAP 系統。
>
>

讀取[本文][ vpn-gateway-create-site-to-site-rm-powershell]如需有關如何 tooconnect 您內部網路 tooMicrosoft Azure

> [!IMPORTANT]
> 當我們說 Azure 與內部部署客戶部署之間的跨內部部署案例中時，我們會查看整體 SAP 系統的 hello 資料粒度。 跨單位案例「不支援」的情況包括︰
>
> * 以不同的部署方法執行不同的 SAP 應用程式層。 例如，請執行 hello DBMS 層在內部，但 hello SAP 應用程式層中 Vm 部署為 Azure Vm，反之亦然。
> * SAP 層的部分元件在 Azure 中，部分元件在內部部署。 例如分割 hello SAP 應用程式層之間的內部部署和 Azure Vm 的執行個體。
> * 不支援將執行一個系統之 SAP 執行個體的 VM 分散到多個 Azure 區域。
>
> 這些限制的 hello 原因是非常低的延遲高效能的網路，一個 SAP 系統，特別是 hello 應用程式執行個體和 hello DBMS 層之間的 SAP 系統內的 hello 需求。
>
>

### <a name="supported-os-and-database-releases"></a>支援的 OS 和資料庫版本
* 下列文章列出「Azure 虛擬機器服務」支援的 Microsoft 伺服器軟體：<http://support.microsoft.com/kb/2721672>。
* 「Azure 虛擬機器服務」搭配 SAP 軟體支援的作業系統版本和資料庫版本記載於 SAP 附註 [1928533]。
* 「Azure 虛擬機器服務」支援的 SAP 應用程式和版本記載於 SAP 附註 [1928533]。
* 只有 64 位元映像對於支援的 toorun 當做來賓 Vm 在 Azure 中 SAP 案例。 這也表示只支援 64 位元 SAP 應用程式和資料庫。

## <a name="microsoft-azure-virtual-machine-services"></a>Microsoft Azure 虛擬機器服務
hello Microsoft Azure 平台是網際網路規模之雲端服務平台裝載和操作於 Microsoft 資料中心。 hello 平台包括 hello Microsoft Azure 虛擬機器服務 （基礎結構即服務，簡稱 IaaS） 和一組豐富的平台即服務 (PaaS) 功能。

hello Azure 平台可減少 hello 需要預先採購技術和基礎結構。 它可簡化維護和操作應用程式藉由提供隨運算和儲存體 toohost 調整及管理 web 應用程式和連接的應用程式。 自動化設計高可用性的平台而動態調整 toomatch 使用需求與 hello 選項隨用隨付計價模型的基礎結構的管理。

![Microsoft Azure 虛擬機器服務的定位][planning-guide-figure-400]

使用 Azure 虛擬機器服務，Microsoft 可讓您 toodeploy 自訂伺服器映像 tooAzure 與 IaaS 執行個體 （請參閱圖 4）。 hello Azure 虛擬機器中 HYPER-V 虛擬硬碟 (VHD) 為基礎，而無法 toorun 不同作業系統做為客體 OS。

就操作觀點而言，Azure 虛擬機器服務提供類似的 hello 體驗做為內部部署的虛擬機器。 不過，它有 hello 更大的優點，您不需要 tooprocure，管理和管理 hello 基礎結構。 開發人員和管理員具有完全控制權的 hello 這些虛擬機器內的作業系統映像。 系統管理員可以遠端登入在 toothose 虛擬機器 tooperform 維護和疑難排解工作，以及軟體部署工作。 在考慮 toodeployment hello 唯一限制是 hello 大小和 Azure Vm 的功能。 您可能無法如內部部署般，對這些項目進行細微的設定。 您可以選擇包含下列項目組合的 VM 類型︰

* vCPU 數目、
* 記憶體、
* 可連接的 VHD 數目、
* 網路和儲存體頻寬。

hello 大小和各種不同的虛擬機器大小的限制所提供的資料表中可以看到[(Linux) 的這篇文章][ virtual-machines-sizes-linux]和[(Windows) 的這篇文章][virtual-machines-sizes-windows].

如您所見，虛擬機器有不同的系列。 您可以區別下列系列 Vm 的 hello:

* A0-A7 VM 類型︰並未全部通過 SAP 認證。 這是 Azure IaaS 引進的第一個 VM 系列。
* A8-A11 VM 類型：高效能運算執行個體。 在計算主機上的執行效能高於其他 A 系列 VM。
* D/Dv2 系列 VM 類型︰執行效能高於 A0-A7。 不是所有的 hello VM 類型經過與 SAP 驗證。
* DS/DSv2 系列 VM 類型： 類似 tooD/Dv2 系列，但這是無法 tooconnect tooAzure 高階儲存體 (請參閱第章[Azure 高階儲存體][ planning-guide-3.3.2]的這份文件)。 同樣地，此 VM 類型並未全部通過 SAP 認證。
* G 系列 VM 類型︰高記憶體 VM 類型。
* GS 系列 VM 類型： 像是 G 系列，但包括 hello 選項 toouse Azure 高階儲存體 (請參閱第章[Azure 高階儲存體][ planning-guide-3.3.2]的這份文件)。 使用時 GS 系列 Vm 做為資料庫伺服器，它是強制 toouse 高階儲存體的資料庫資料和交易記錄檔

您可能會發現 hello 相同的 CPU 和記憶體組態中不同的 VM 系列。 不過，當您查詢 hello 它們可能會顯著的不同序列出這些 Vm hello 輸送量效能。 儘管有 hello 相同 CPU 和記憶體組態。 原因是 hello 基礎主機伺服器硬體在 hello 導入 hello 不同 VM 類型具有不同的輸送量特性。  通常輸送量效能所示的 hello 差異也會反映在 hello hello 價格不同的 Vm。

並非所有的其他 VM 系列，可能會提供每一種 hello Azure 區域 （適用於 Azure 區域，請參閱下一章）。 另請注意，並非所有 VM 或 VM 系列都通過 SAP 認證。

> [!IMPORTANT]
> Hello SAP NetWeaver 型應用程式使用，只有 hello 子集 VM 類型和組態列於 SAP Note [1928533]支援。
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Azure 區域
Microsoft 可讓稱為 'Azure 區域' toodeploy 虛擬機器。 Azure 區域可以是位置很近的一或多個資料中心。 大部分的 hello 地緣政治區域 hello world Microsoft 中的有至少兩個 Azure 區域。 例如，在歐洲，有一個「北歐」和一個「西歐」Azure 區域。 這類地理政治區域內的兩個 Azure 區域大的距離相隔的自然或技術的嚴重損壞時不會影響這兩個 Azure 中的區域 hello 相同地理政治區域。 因為 Microsoft 穩定全域建置出新的 Azure 區域中不同的地理政治區域，這些區域的 hello 數目穩定成長時，並自 2015 年 12 月達到 20 已宣布的其他區域的 Azure 區域的 hello 數目。 您的客戶可以將 SAP 系統部署到所有這些區域，包含在中國的 hello 兩個 Azure 區域。 如需有關 Azure 區域的目前最新資訊，請參閱下列網站：<https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>hello Microsoft Azure 虛擬機器概念
Microsoft Azure 提供一種基礎結構服務 (IaaS) 方案 toohost 為虛擬機器功能類似做為內部部署虛擬化解決方案。 您所能 toocreate 從虛擬機器內 hello Azure 入口網站、 PowerShell 或 CLI，後者也提供部署和管理功能。

Azure 資源管理員可讓您 tooprovision 使用宣告式範本的應用程式。 在單一的範本中，您可以部署多個服務及其相依性。 使用 hello 相同範本 toorepeatedly 部署應用程式在每個階段中的 hello 應用程式生命週期。

如需使用 Resource Manager 範本的詳細資訊，請參閱：

* [部署和管理虛擬機器使用的 Azure 資源管理員範本和 hello Azure CLI][../../ linux/create-ssh-secured-vm-from-template.md]
* [使用 Azure Resource Manager 和 PowerShell 管理虛擬機器][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

另一個有趣的功能是 hello 能力 toocreate 映像，從虛擬機器，可讓您 tooprepare 特定儲存機制的 tooquickly 能部署虛擬機器執行個體，您的需求。

如需有關從「虛擬機器」建立映像的詳細資訊，請參閱[這篇文章 (Linux)][virtual-machines-linux-capture-image-resource-manager] 或[這篇文章 (Windows)][virtual-machines-windows-capture-image-resource-manager]。

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>容錯網域
故障網域代表實體單位失敗時，非常密切相關的 toohello 實體基礎結構所包含的資料中心，雖然實體刀鋒伺服器或機架可視為 「 故障 」 網域，hello 兩者之間沒有直接的一對一對應。

當您部署多部虛擬機器做為 Microsoft Azure 虛擬機器服務中的一個 SAP 系統的一部分時，您可能會影響 hello Azure 網狀架構控制器 toodeploy 應用程式分成不同容錯網域，以符合 hello hello 需求Microsoft Azure SLA。 不過，透過 Azure 縮放單位 （數以百計的運算節點或儲存體節點和網路功能的集合） hello 的容錯網域的發佈或 Vm tooa hello 指派特定的容錯網域是透過它您不需要直接控制。 順序 toodirect hello Azure 網狀架構控制器 toodeploy 一組不同的故障網域上的 Vm，您需要 tooassign Azure 可用性設定組 toohello Vm 在部署階段。 如需有關「Azure 可用性設定組」的詳細資訊，請參閱本文件的 [Azure 可用性設定組][planning-guide-3.2.3]一章。

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>升級網域
升級網域代表協助的 toodetermine 如何更新 SAP 系統，可包含多個 Vm 中執行的 SAP 執行個體，在 VM 的邏輯單元。 進行升級時，Microsoft Azure 會開始逐一更新這些 「 升級 」 網域一個 hello 程序中。 藉由在部署時將 VM 散佈到不同的升級網域，即可防止您的 SAP 系統可能有一部分停機。 中排序 tooforce Azure toodeploy hello Vm 的 SAP 系統分散到不同的 「 升級 」 網域，您需要 tooset 特定的屬性在部署期間的每個 VM。 類似 tooFault 定義域、 Azure 縮放單位會分成多個升級網域。 順序 toodirect hello Azure 網狀架構控制器 toodeploy 一組的 Vm，透過不同的 「 升級 」 網域，您需要 tooassign Azure 可用性設定組 toohello Vm 在部署階段。 如需有關「Azure 可用性設定組」的詳細資訊，請參閱下一章 [Azure 可用性設定][planning-guide-3.2.3]。

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Azure 可用性設定組
一個 Azure 可用性設定組內的 azure 虛擬機器由 Azure 網狀架構控制器 hello 分散在不同的容錯和升級網域上。 hello 目的 hello 分散至不同的容錯和升級網域是的 tooprevent 從 SAP 系統的所有 Vm 都關機 hello 案例的基礎結構維護或一個 「 故障 」 網域內的失敗。 根據預設，VM 不是可用性設定組的一部分。 hello 參與 VM 的可用性設定組被定義在部署期間或在稍後重新設定和重新部署 VM。

可用性設定組與 tooFault 」 和 「 升級 」 網域，Azure 可用性設定組和 hello 方式 toounderstand hello 概念讀取[這篇文章][virtual-machines-manage-availability]

請參閱 toodefine 的可用性設定組 ARM 透過 json 範本[hello rest api 規格](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json)，並搜尋 「 可用性 」。

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>儲存體：Microsoft Azure 儲存體和資料磁碟
Microsoft Azure 虛擬機器使用不同的儲存體類型。 在 Azure 虛擬機器服務上實作 SAP 時，它會是重要 toounderstand hello 差異存放區這兩種主要類型：

* 非永續性、可變更的儲存體。
* 永續性儲存體。

hello 非持續性儲存體是執行中虛擬機器的直接連結的 toohello，和位於 hello 計算節點本身-hello 本機執行個體儲存體 （暫存儲存體）。 hello 大小取決於 hello hello hello 部署啟動時選擇的虛擬機器大小。 此儲存體類型是暫時性的因此 hello 磁碟初始化重新啟動虛擬機器執行個體時。 一般而言，hello hello 作業系統分頁檔位於此暫存磁碟上。

- - -
> ![Windows][Logo_Windows] Windows
>
> 在 Windows Vm 上 hello 暫存磁碟機裝載為磁碟機中已部署 VM 的 D:\。
>
> ![Linux][Logo_Linux] Linux
>
> 在 Linux VM 上，則會掛接為 /mnt/resource 或 /mnt。 如需詳細資訊，請參閱：
>
> * [如何 tooAttach 資料磁碟 tooa Linux 虛擬機器][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux#temporary-disk>
>
>

- - -
hello 實際磁碟機是暫時性的因為它儲存在 hello 主機伺服器本身。 如果在重新部署中的 hello VM 移動 (例如在 hello 主機或關機，然後重新啟動到期 toomaintenance) hello hello 磁碟機的內容都會遺失。 因此，它不是選項 toostore 此磁碟機上的任何重要資料。 hello 用於這種類型的存放裝置的媒體類型不同的自 2015 年 6 月看起來非常不同的效能特性與不同的 VM 系列：

* A5-A7︰非常有限的效能。 除了分頁檔之外，不建議使用
* A8-A11︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量。
* D 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量。
* DS 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量。
* G 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量。
* GS 系列︰效能特性非常良好，有數萬個 IOPS 和 > 1 GB/秒的輸送量。

上述陳述式會套用 toohello 經過驗證和 SAP 的 VM 類型。 絕佳的 IOPS 及輸送量與 hello VM 系列限定運用的一些 DBMS 功能。 如需詳細資訊，請參閱 hello[的 DBMS 部署指南][dbms-guide]。

Microsoft Azure 儲存體提供持續性儲存體和 hello 一般層級的保護和備援在 SAN 存放裝置上看到。 Azure 儲存體為基礎的磁碟是虛擬硬碟 (Vhd) 位於 hello Azure 儲存體服務。 hello 本機作業系統磁碟 (Windows c:\, Linux/開發/sda1) 儲存在 hello Azure 儲存體，和其他磁碟區/磁碟掛接的 toohello VM 儲存在這裡太。

可能的 tooupload 現有的 VHD 從內部部署或建立從在 Azure 中的空的並附加這些 toodeployed Vm。

建立或上傳 VHD 到 Azure 儲存體之後, 可能 toomount，並附加現有的虛擬機器和現有的 （卸載） VHD toocopy 這些 tooan。

由於這些 VHD 為永續性，因此當重新啟動及重新建立虛擬機器執行個體時，這些 VHD 中的資料和變更是安全的。 即使刪除執行個體時，這些 Vhd 保持安全和可重新部署或如果不是作業系統磁碟可在掛接的 tooother Vm。

Hello 內可以設定網路的 Azure 儲存體不同的備援層級：

* 可供選取的最低層級為 '本機備援'，這是一個 hello hello 資料的對等 toothree 複本相同的資料中心的 Azure 區域 (請參閱第章[Azure 區域][planning-guide-3.1])。
* 區域備援儲存體，透過不同的資料中心內的模式 hello 三個影像 hello 相同 Azure 區域。
* 預設的備援層級是地理備援，以非同步方式將 hello 內容複寫到另一個 Azure 區域，裝載於 hello hello 資料的其他三個映像至相同的地理政治區域。

另請參閱 hello 資料表頂端 hello 不同備援選項有關的這篇文章： <https://azure.microsoft.com/pricing/details/storage/>

如需 Azure 儲存體的詳細資訊，請參閱：

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Azure 標準儲存體
Azure 的標準儲存體時發行 Azure IaaS hello 類型可用的儲存體。 每個單一磁碟會強制執行 IOPS 配額。 發生延遲不是在相同類別，如 SAN/NAS 裝置通常會部署為高階的 SAP 系統裝載在內部部署的 hello。 不過，標準儲存體 Azure 證實足以應付數以百計的 hello 同時部署在 Azure 中 SAP 系統。

負責根據 hello 實際儲存的資料，hello 磁碟區的儲存體交易、 傳出資料傳輸，與選擇的備援選項會儲存在 Azure 標準儲存體帳戶的磁碟。 可以在 hello 大 1 TB 的大小，建立多個磁碟但只要維持空白會產生任何費用。 接著，您就會填入一個 100 gb VHD，如果您需要付費來儲存 100 GB，不能用於建立 vhd 與 hello 名義大小 hello。

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Azure 進階儲存體
在 2015 年 4 月，Microsoft 引進 Azure 進階儲存體。 高階儲存體引進與 hello 目標 tooprovide:

* 更佳的 I/O 延遲。
* 更佳的輸送量。
* 更小的 I/O 延遲變化性。

基於這個目的，許多導入了變更哪些 hello 兩個最重要的：

* Hello Azure 儲存體節點中的 SSD 磁碟的使用方式
* 新的讀取快取，並受到 hello Azure 計算節點的本機 SSD

功能未變更的相反 tooStandard 儲存體中相依於 hello 大小 hello 磁碟 （或 VHD），進階儲存體目前有三個不同的磁碟類別，這篇文章中會顯示這些： <https://azure.microsoft.com/價格/詳細資料/儲存體/不受管理磁碟 />

您會看到 IOPS/磁碟和磁碟輸送量/磁碟會相依於 hello 的 hello 磁碟的大小類別目錄

這類 disks，但這類的磁碟，獨立於 hello 資料 hello 磁碟中所儲存的 hello 量 hello 大小類別目錄中儲存的 hello 實際的資料磁碟區的無法在 hello 案例中的進階儲存體的成本為基礎。

您也可以建立不會直接對應到顯示 hello 大小類別目錄的高階儲存體的磁碟。 這可能是 hello 的情況下，尤其是將磁碟從標準儲存體複製到高階儲存體。 在此情況下對應 toohello 下一個最大高階儲存體磁碟選項會執行。

請注意，只有特定 VM 系列可受益於 hello Azure 高階儲存體。 自 2015 年 12 月中，這些是 hello DS-與 GS 系列。 hello DS 系列是基本上 hello 相同作為 DS 系列有 hello 能力 toomount 高階儲存體的 hello 例外狀況的 D 系列 Vm 此外 toodisks 裝載在 Azure 標準儲存體上。 G 系列比較 tooGS 數列相同的動作無效。

如果您正在簽出 hello DS 系列 Vm 中的 hello 一部分[(Linux) 的這篇文章][ virtual-machines-sizes-linux]和[(Windows) 的這篇文章][virtual-machines-sizes-windows]，您了解有資料磁碟區限制 tooPremium 存放磁碟上的 hello VM 層級的 hello 資料粒度。 不同的 DS 系列或 GS 系列 Vm 也可掛接的資料磁碟的相關事宜 toohello 數種具有不同的限制。 這些限制記載於 hello 發行項，以及先前所述。 但是，基本上這表示，如果您，比方說，裝載 32 x P30 磁碟 tooa 單一 DS14 VM 您無法取得 32 x hello P30 磁碟的最大的輸送量。 改為 hello 在 VM 層級述 hello 文章限制資料輸送量最大輸送量。

如需有關進階儲存體的詳細資訊，請參閱：<http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>受控磁碟
受控磁碟是 Azure Resource Manager 的新資源類型，可用來取代儲存在 Azure 儲存體帳戶的 VHD。 受管理的磁碟自動對齊的 hello 可用性設定組的 hello 虛擬機器，它們是附加 tooand 因此增加 hello 可用性，您的虛擬機器與 hello 服務 hello 虛擬機器上執行。 如需詳細資訊，請閱讀 hello[概觀文章](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview)。

我們建議 tooyou 使用受管理磁碟，因為它們簡化 hello 部署和管理的虛擬機器。
SAP 目前僅支援進階受控磁碟。 如需詳細資訊，請參閱 SAP 附註 [1928533]。

#### <a name="azure-storage-accounts"></a>Azure 儲存體帳戶
在 Azure 中部署服務或 VM 時，VHD 和 VM 映像的部署可以組織成不同單位，稱為 Azure 儲存體帳戶。 當規劃 Azure 部署時，您需要 toocarefully 考慮 hello Azure 的限制。 在 hello 一邊沒有有限的儲存體帳戶的每個 Azure 訂用帳戶。 Hello 雖然每個 Azure 儲存體帳戶可以保存大量的 VHD 檔案，但沒有固定的限制的總每個儲存體帳戶的 IOPS。 在部署數以百計的 SAP Vm 且 DBMS 系統會建立大量 IO 呼叫時，它會建議 toodistribute 高 IOPS 的 DBMS Vm 之間的多個 Azure 儲存體帳戶。 必須小心不要 tooexceed hello 目前限制 Azure 儲存體帳戶的每個訂閱。 這個概念，因為存放裝置 hello 資料庫部署 SAP 系統不可或缺的一部分，hello 已經被參考的更詳細地討論[的 DBMS 部署指南][dbms-guide]。

如需有關「Azure 儲存體帳戶」的詳細資訊，請參閱[這篇文章][storage-scalability-targets]。 您閱讀這篇文章，了解有 hello 限制 Azure 標準儲存體帳戶和 Premium 儲存體帳戶之間的差異。 主要差異是 hello 可以儲存在儲存體帳戶內的資料量。 在標準儲存體 hello 磁碟區是大於高階儲存體的範圍。 在 hello 另一端，hello 標準儲存體帳戶是嚴重限制了的 IOPS （請參閱資料行 ' 總要求率 '），而 hello Azure 高階儲存體帳戶有沒有這類限制。 討論的 SAP 系統，特別是 hello DBMS 伺服器的 hello 部署時，我們將討論詳細資料，以及這些差異的結果。

儲存體帳戶，在您目前 hello 目的，是組織和分類不同 Vhd 的 hello 可能性 toocreate 不同容器。 這些容器通常用於不同 VM 的個別 VHD。 在單一 Azure 儲存體帳戶下只使用一個容器或使用多個容器對效能不會有太大影響。

在 Azure 中的 VHD 名稱會遵循 hello 遵循命名需要 tooprovide hello VHD 在 Azure 中的唯一名稱的連接：

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

為上面所述的 hello 字串需要 toouniquely 識別 hello 儲存在 Azure 儲存體的 VHD。

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Microsoft Azure 網路
Microsoft Azure 提供網路基礎結構，可讓所有案例中，我們想要的 hello 對應 toorealize SAP 軟體。 hello 功能包括：

* 存取外部，直接 toohello Vm 透過 Windows 終端機服務或 ssh/VNC hello
* 存取 tooservices 與 hello Vm 內的應用程式所使用的特定連接埠
* 在部署為 Azure VM 的一組 VM 之間進行內部通訊和名稱解析
* 客戶的內部部署網路與 hello Azure 網路之間的跨單位連線
* Azure 網站之間的跨 Azure 區域或資料中心連線能力

如需詳細資訊，請參閱這裡：<https://azure.microsoft.com/documentation/services/virtual-network/>

有許多不同的方式 tooconfigure 名稱和 IP 解析，Azure 中。 本文件僅限雲端案例依賴 hello 預設值是使用 Azure DNS （在對比 toodefining 自己的 DNS 服務)。 此外，還可使用新的 Azure DNS 服務，而不是使用您自己的 DNS 伺服器。 如需詳細資訊，請參閱[這篇文章][virtual-networks-manage-dns-in-vnet]和[這個頁面](https://azure.microsoft.com/services/dns/)。

跨內部部署案例中，我們會依賴 hello 事實該 hello 內部部署 AD/OpenLDAP/DNS 透過 VPN 或私人連線 tooAzure 已擴充。 某些這裡所述的案例中，可能需要 toohave 安裝在 Azure AD/OpenLDAP 複本。

因為網路和名稱解析是不可或缺的一部分的 SAP 系統的 hello 資料庫部署、 hello 的更詳細地討論這個概念[的 DBMS 部署指南][dbms-guide]。

##### <a name="azure-virtual-networks"></a>Azure 虛擬網路
建置 Azure 虛擬網路，您可以定義 hello 的 hello Azure DHCP 功能所配置的私人 IP 位址的位址範圍。 在跨單位案例中，定義 hello IP 位址範圍是仍然使用 DHCP 配置由 Azure。 不過，網域名稱解析是在內部部署 （假設 hello Vm 會在內部部署網域的一部分），因此可以解決超出不同 Azure 雲端服務的位址。

Azure 需要 toobe 中每個虛擬機器連線 tooa 虛擬網路。

如需更多詳細資料，請參閱[這篇文章][resource-groups-networking]和[這個頁面](https://azure.microsoft.com/documentation/services/virtual-network/)。

[comment]: <> (MShermannd TODO 無法尋找發行項，其中包括 hello OpenLDAP 主題 + ARM;)
[comment]: <> (MSSedusch <https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> 根據預設，在部署 VM 之後無法變更 hello 虛擬網路組態。 hello TCP/IP 設定必須留給 toohello Azure DHCP 伺服器。 預設行為是動態 IP 指派。
>
>

hello hello 虛擬網路卡的 MAC 位址之後可能會變更，例如調整大小與 hello Windows 或 Linux 客體作業系統會拾取 hello 新的網路卡，並會自動在此情況下使用 DHCP tooassign hello IP 和 DNS 位址。

##### <a name="static-ip-assignment"></a>靜態 IP 指派
它是固定的可能 tooassign 或 tooVMs Azure 虛擬網路內的保留的 IP 位址。 在 Azure 虛擬網路中執行 hello Vm 開啟很棒的可能性 tooleverage 這項功能有必要，在某些情況下。 hello IP 指派持續有效整個 hello hello hello VM 是否正在執行或關機的獨立 VM 存在。 如此一來，您需要 tootake hello Vm 總數 (執行中和已停止的 VM) 納入考量，當定義 hello 虛擬網路的 hello 範圍的 IP 位址。 直到刪除為止 hello VM 和其網路介面或直到再次取消指派 hello IP 位址取得 hello IP 位址仍然維持指派。 如需詳細資訊，請參閱[這篇文章][virtual-networks-static-private-ip-arm-pportal]。

##### <a name="multiple-nics-per-vm"></a>每個 VM 可以有多個 NIC
您可以為一個 Azure 虛擬機器定義多個虛擬網路介面卡 (vNIC)。 與 hello 能力 toohave vNICs 多個您可以啟動 tooset 向上，比方說，用戶端流量路由傳送透過一個 vNIC 後, 端流量都會透過第二個 vNIC 路由傳送網路流量隔離。 依存於 VM 有一些不同的限制的 hello 類型目前 toohello vNICs 數目。 如需確切詳細資料、功能和限制，請參閱下列文章︰

* [建立具有多個 NIC 的 Windows VM][virtual-networks-multiple-nics-windows]
* [建立連接多個 NIC 的 Linux VM][virtual-networks-multiple-nics-linux]
* [使用範本部署多個 NIC VM][virtual-network-deploy-multinic-arm-template]
* [使用 PowerShell 部署多個 NIC VM][virtual-network-deploy-multinic-arm-ps]
* [部署使用 Azure CLI hello 多重 NIC Vm][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>站對站連線能力
跨單位是指使用透明且永久的 VPN 連線連結 Azure VM 和內部部署 VM。 這是預期的 toobecome hello 最常見 SAP 部署模式在 Azure 中。 hello 假設是操作程序和處理程序與在 Azure 中的 SAP 執行個體應以透明的方式運作。 這表示您應該要能夠 tooprint 出這些系統，以及使用 SAP 傳輸管理系統 (TMS) tootransport 開發系統變更 Azure tooa 測試系統，也就是在內部部署中的 hello。 如需有關站對站的詳細記載，請參閱[這篇文章][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>VPN 通道裝置
在排序 toocreate 站對站連線 （在內部部署資料中心 tooAzure 資料中心），您需要 tooeither 取得和設定 VPN 裝置，或使用路由及遠端存取服務 (RRAS) 導入的 Windows server 的軟體元件2012。

* [使用 PowerShell 建立具有站對站 VPN 連線的虛擬網路][vpn-gateway-create-site-to-site-rm-powershell]
* [關於站對站 VPN 閘道連線的 VPN 裝置][vpn-gateway-about-vpn-devices]
* [VPN 閘道常見問題集][vpn-gateway-vpn-faq]

![內部部署與 Azure 之間的站對站連線][planning-guide-figure-600]

hello 上圖顯示兩個 Azure 訂用帳戶在 Azure 中虛擬網路中有使用保留的 IP 位址子範圍。 從 hello hello 連線在內部網路 tooAzure 透過 VPN 建立。

#### <a name="point-to-site-vpn"></a>點對站 VPN
點對站 VPN 需要有它自己的 VPN 每個用戶端機器 tooconnect 至 Azure。 我們會查看 hello SAP 案例，並不實用點對站連線能力。 因此，沒有進一步的參考會提供 toopoint 對站 VPN 連線能力。

如需詳細資訊，請參閱這裡
* [設定點對站連線 tooa VNet 使用 hello Azure 入口網站](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [設定點對站連線 tooa VNet 使用 PowerShell](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>多站台 VPN
Azure screen 鍵也會提供一個 Azure 訂用帳戶 hello 可能性 toocreate 多網站 VPN 連線。 單一訂用帳戶之前有限的 tooone 站對站 VPN 連線。 此限制在單一訂用帳戶可以有「多站台 VPN」連線之後已不存在。 這使得可能 tooleverage 多個特定的訂用帳戶，透過跨單位組態的一個 Azure 區域。

如需詳細的記載，請參閱[這篇文章][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO 找不到 ARM 文件連結)

#### <a name="vnet-toovnet-connection"></a>VNet tooVNet 連線
使用多網站 VPN，您需要 tooconfigure 個別 Azure 虛擬網路中每個 hello 區域。 不過經常需要 hello hello hello 不同區域中的軟體元件應該與彼此通訊。 在理想情況下此通訊應該不會路由傳送沒有 toohello 從一個 Azure 區域 tooon 內部部署與其他 Azure 區域。 tooshortcut，Azure 提供 hello 可能性 tooconfigure 從一個 Azure 虛擬網路中裝載在另一個地區的 Azure 虛擬網路的一個區域 tooanother 的連接。 此功能稱為 VNet 對 VNet 連線。 如需有關此功能的詳細資訊，請參閱這裡：<https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>。

#### <a name="private-connection-tooazure--expressroute"></a>私用連接 tooAzure – ExpressRoute
Microsoft Azure ExpressRoute 可讓 hello 建立私人連線 Azure 資料中心與任一 hello 客戶的內部部署基礎結構之間部署或共置環境中。 ExpressRoute 是由各種 MPLS (封包交換式) VPN 提供者或其他網路服務提供者所提供。 ExpressRoute 連線不會經過 hello 公用網際網路。 ExpressRoute 連線 hello 網際網路提供較高的安全性、 透過多個並聯電路、 更快的速度和低延遲比一般的連線。

如需 Azure ExpressRoute 和供應項目的詳細資訊，請參閱︰

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

如下方所記載，Express Route 可透過一個 ExpressRoute 循環來啟用多個 Azure 訂用帳戶

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>跨單位時的強制通道
對於 Vm 加入內部部署網域透過站對站、 點對站或 ExpressRoute，您需要 toomake 確定也對這些 Vm 中的所有 hello 使用者會取得都部署 hello 網際網路 proxy 設定。 根據預設，這些 Vm 或使用者使用瀏覽器 tooaccess hello 網際網路不會透過 hello 公司 proxy，但會直接透過 Azure toohello 連接中執行的軟體網際網路。 但即使 hello proxy 設定不是 100%的解決方案 toodirect hello 流量透過 hello 公司 proxy 因為負責軟體與服務 toocheck hello proxy。 如果 hello VM 中執行的軟體沒有這樣做，或有系統管理員操作 hello 設定，可以再次繞道流量 toohello 網際網路直接透過 Azure toohello 網際網路。

在這排序 tooavoid 中，您可以設定強制通道與內部部署與 Azure 之間的站對站連線。 hello hello 強制通道功能的詳細的說明發行這裡<https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

透過 ExpressRoute 強制的通道會啟用客戶透過 ExpressRoute BGP hello 將預設路由通告對等互連工作階段。

#### <a name="summary-of-azure-networking"></a>Azure 網路摘要
本章包含有關 Azure 網路的許多重點。 Hello 重點摘要如下：

* Azure 虛擬網路可讓 tooset hello 網路根據 tooyour 自己的需求
* Azure 虛擬網路可以是運用 tooassign IP 位址範圍 tooVMs 或指派固定的 IP 位址 tooVMs
* tooset 站對站或點對站連線，您需要先 toocreate Azure 虛擬網路
* 部署虛擬機器之後, 就無法再虛擬網路指派 toohello VM 的可能 toochange hello

### <a name="quotas-in-azure-virtual-machine-services"></a>Azure 虛擬機器服務中的配額
我們需要 toobe 清除有關 hello 事實，hello 儲存，並在 hello Azure 基礎結構中執行各種服務的 Vm 之間會共用網路基礎結構。 如同 hello 客戶自己的資料中心，過度佈建一些 hello 基礎結構資源採用位置 tooa 程度。 hello Microsoft Azure 平台會使用磁碟、 CPU、 網路和其他配額 toolimit hello 資源耗用量和 toopreserve 一致和確定的效能。  hello 不同 VM 類型 （A5、 A6 等） 有不同的配額 hello 編號磁碟、 CPU、 RAM 和網路。

> [!NOTE]
> SAP 所支援的 hello VM 類型的 CPU 和記憶體資源上會預先配置 hello 主機節點。 這表示，hello VM 部署之後，hello hello 主機上可用的資源 hello VM 類型所定義。
>
>

您必須考量時，規劃和調整 SAP Azure 解決方案上 hello 每種虛擬機器大小的配額。 說明 hello VM 配額[這裡 (Linux)] [ virtual-machines-sizes-linux]和[這裡 (Windows)][virtual-machines-sizes-windows]。

所述的 hello 配額代表 hello 理論上的最大值。  每個磁碟的 IOPS hello 限制可能達到較小 Io (8kb)，但可能可能無法達到較大 Io (1mb)。  hello IOPS 限制是單一磁碟 hello 細部上實施。

為初步決策樹狀結構 toodecide 是否 SAP 系統整合到 Azure 虛擬機器服務和其功能或現有的系統必須 toobe 中訂單 toodeploy hello 系統在 Azure 上，以不同的方式設定是否可以使用下列 hello 決策樹：

![決策樹 toodecide 能力 toodeploy SAP on Azure][planning-guide-figure-700]

**步驟 1**: hello 最重要資訊 toostart 與是 hello 特定 SAP 系統的 SAPS 需求。 hello SAPS 需求需要 toobe 分割成 hello DBMS 部分和 hello SAP 應用程式部分，即使已 hello SAP 系統部署在內部 2 層組態中。 對於現有的系統，SAP 相關 toohello 使用硬體通常可以決定或預估的 hello 根據現有的 SAP 基準。 hello 結果可以在這裡找到： <http://global.sap.com/campaigns/benchmark/index.epx>。
針對新部署的 SAP 系統，您應該已經完成調整工作，而應該決定 hello hello 系統的 SAPS 需求。
關於 Azure 上的 SAP 大小調整，另請參閱這個部落格和附加的文件：<http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**步驟 2**： 對於現有的系統，hello I/O 量和應該以 hello DBMS 伺服器上的每秒 I/O 作業。 對於新規劃的系統，hello 縮放 hello 新系統的練習也應該提供 hello DBMS 方面上的初步了解 hello I/O 需求。 如果不確定，您最終需要 tooconduct 概念證明。

**步驟 3**: hello 與 hello SAPS hello 不同 VM 類型的 Azure 的 DBMS 伺服器可以提供比較 hello SAPS 需求。 hello 不同 Azure VM 類型的 saps 相關 hello 資訊記載於 SAP Note [1928533]。 hello 焦點應該 hello DBMS VM 上第一次因為 hello 資料庫層級是在 SAP NetWeaver 系統中，不會向外延展 hello 的大部分部署中的 hello 層。 相反地，hello SAP 應用程式層可以向外延展。如果支援任何 hello SAP Azure VM 類型可以傳送 hello 所需的 SAPS，無法在 Azure 上執行計劃的 hello SAP 系統的 hello 工作負載。 您必須 toodeploy hello 系統在內部部署或 hello 系統所需 toochange hello 工作負載磁碟區。

**步驟 4**︰如[這裡 (Linux)][virtual-machines-sizes-linux] 和[這裡 (Windows)][virtual-machines-sizes-windows] 所述，不論您使用的是「標準儲存體」還是「進階儲存體」，Azure 都會針對每個磁碟強制執行 IOPS 配額。 視 VM 類型 hello hello 可掛接的資料磁碟數目而異。 如此一來，您可以計算與每個 hello 不同 VM 類型可達到 IOPS 數目上限。 相依於 hello 資料庫檔案配置，您可以等量分割磁碟 toobecome 一個磁碟區 hello 客體作業系統中。 不過，如果 hello 目前 IOPS 磁碟區已部署的 SAP 系統超過 hello 最大 VM 類型的 Azure，而且如果沒有更多的記憶體使用沒有機會 toocompensate hello 計算限制，hello 的 hello SAP 系統的工作負載可能會影響嚴重。 在這種情況下，您可以按其中則不應部署在 Azure 上的 hello 系統的點。

**步驟 5**： 特別是在 SAP 系統，是部署在內部 2 層組態中、 hello 有可能是因為 hello 系統，可能需要 toobe 3 層組態中設定。 在此步驟中，您會需要 toocheck 中是否有元件 hello SAP 應用程式層，其無法擴充，以及這不會放入 hello CPU 和記憶體資源 hello 不同 Azure VM 類型提供項目。 如果確實有這類元件，hello SAP 系統和其工作負載無法部署到 Azure。 但是，如果您可以向外延展 hello SAP 應用程式元件到多個 Azure Vm，hello 系統可以部署到 Azure。

**步驟 6**: hello DBMS 和 SAP 應用程式層元件可以在 Azure Vm 中執行，如果需要 toobe 定義與 hello 組態：

* Azure VM 數目
* Hello 個別元件的 VM 類型
* DBMS VM tooprovide 中的 Vhd 數目足夠的 IOPS

## <a name="managing-azure-assets"></a>管理 Azure 資產
### <a name="azure-portal"></a>Azure 入口網站
hello Azure 入口網站是一個三個介面 toomanage Azure VM 部署。 hello 基本管理工作，例如從映像，來部署 Vm 可以透過 hello Azure 入口網站。 此外，hello 建立儲存體帳戶、 虛擬網路和其他 Azure 元件也是工作 hello Azure 入口網站可妥善處理。 不過，像是將 Vhd 從內部部署 tooAzure 上傳或複製 VHD 在 Azure 中的功能都需要協力廠商工具或透過 PowerShell 或 CLI 管理的工作。

![Microsoft Azure 入口網站 - 虛擬機器概觀][planning-guide-figure-800]

[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

從 hello Azure 入口網站內可能會有 hello 虛擬機器執行個體的管理和組態工作。

除了重新啟動和關閉虛擬機器，您也附加、 卸離，並建立 hello 虛擬機器執行個體，來準備映像 toocapture hello 執行個體的資料磁碟並設定 hello hello 虛擬機器執行個體的大小。

hello Azure 入口網站提供基本功能 toodeploy 和設定 Vm 及其他許多 Azure 服務。 不過不所有可用的功能會涵蓋的 hello Azure 入口網站。 在 hello Azure 入口網站，就不可能 tooperform 工作，例如：

* 上傳 Vhd tooAzure
* 複製 VM

[comment]: <> (MShermannd TODO SAP VM 的自動化服務如何？)
[comment]: <> (MSSedusch 目前可以部署多個 VM OS)
[comment]: <> (也 MSSedusch 自動化部署有關的任何型別不可能以 hello Azure 入口網站。工作，例如指令碼的多個 Vm 的部署不能透過 hello Azure 入口網站。)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>透過 Microsoft Azure PowerShell Cmdlet 管理
Windows PowerShell 是強大且可擴充的架構，客戶已廣泛採用此架構在 Azure 中部署大量系統。 Hello 安裝後 PowerShell 指令程式在桌上型電腦、 膝上型電腦或專用的管理工作站，可以從遠端執行 hello PowerShell cmdlet。

hello 程序 tooenable 本機桌上型電腦/膝上型電腦 hello Azure PowerShell cmdlet 的使用方式，以及如何與 hello 與使用方式的 tooconfigure hello Azure 訂閱所述[本文][powershell-install-configure]。

也可以在中找到 tooinstall，如何更新，以及設定 hello Azure PowerShell cmdlet 的詳細的步驟[hello 部署指南的這一章][deployment-guide-4.1]。

客戶經驗到目前為止已 PowerShell (PS) 的確是 hello 功能更強大的工具 toodeploy Vm 和自訂 toocreate hello 部署的 Vm 中的步驟。 Hello 客戶在 Azure 中執行 SAP 執行個體的所有使用 PS cmdlet toosupplement 管理工作它們在 hello Azure 入口網站中，或甚至使用 PS 指令程式以獨佔方式 toomanage Azure 中的部署。 因為 hello Azure 專用指令程式共用 hello 相同命名慣例為 hello 超過 2000年與 Windows 相關的 cmdlet，將會以簡單的工作 Windows 系統管理員 tooleverage 這些指令程式。

請參閱以下的範例︰<http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO 描述測試時的新 CLI 命令)
部署的 hello Azure Monitoring Extension for SAP (請參閱第章[適用於 SAP 的 Azure 監視解決方案][ planning-guide-9.1]本文件中) 僅能透過 PowerShell 或 CLI。 因此它會強制 tooset 已啟動並設定 PowerShell 或 CLI 時部署或管理在 Azure 中的 SAP NetWeaver 系統。  

隨著 Azure 提供更多的功能，toobe 加入需要 hello 指令程式更新將新增 PS 指令程式。 因此它使意義 toocheck hello 下載 Azure 站台至少 hello 月一次<https://azure.microsoft.com/downloads/> hello cmdlet 的新版本。 hello 新版本會安裝在 hello 舊版之上。

如需 Azure 相關 PowerShell 命令的一般清單，請按一下這裡︰<https://docs.microsoft.com/powershell/azure/overview>。

### <a name="management-via-microsoft-azure-cli-commands"></a>透過 Microsoft Azure CLI 命令管理
對於客戶使用 Linux 並想 toomanage Azure Powershell 資源可能不是選項。 Microsoft 提供 Azure CLI 作為替代方案。
hello Azure CLI 提供一組的開放原始碼跨平台命令來處理 hello Azure 平台。 hello Azure CLI 提供許多 hello hello Azure 入口網站中找到相同的功能。

如需有關安裝、 設定及 toouse CLI 命令 tooaccomplish 的如何資訊 Azure 的工作，請參閱

* [安裝 hello Azure CLI][xplat-cli]
* [部署和管理虛擬機器使用的 Azure 資源管理員範本和 hello Azure CLI][../../ linux/create-ssh-secured-vm-from-template.md]
* [使用 Mac、 Linux 及 Windows Azure 資源管理員與 hello Azure CLI][xplat-cli-azure-resource-manager]

也會讀取章[適用於 Linux Vm 的 Azure CLI] [ deployment-guide-4.5.2]在 hello[部署指南 》] [ planning-guide]上 toouse Azure CLI toodeploy hello Azure 監視功能適用於 SAP 的擴充功能。

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>不同的方式 toodeploy Azure 中 sap 的 Vm
在本章中，您會學習 hello 不同的方式 toodeploy Azure 中的 VM。 本章涵蓋其他準備程序，以及在 Azure 中處理 VHD 和 VM 的方式。

### <a name="deployment-of-vms-for-sap"></a>為 SAP 部署 VM
Microsoft Azure 提供的多種 toodeploy Vm 和相關聯的磁碟。 因此是非常重要的 toounderstand hello 差異因為 hello Vm 的準備工作可能會根據部署的 hello 方法不同。 一般情況下，我們看看下列案例的 hello:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>將 VM 從內部部署 tooAzure 使用非一般化磁碟
您計劃 toomove 特定 SAP 系統從內部部署 tooAzure。 這可藉由來上傳 VHD 包含 hello OS hello、 hello SAP 二進位檔和 DBMS 二進位檔加上 Vhd hello 與 hello hello DBMS tooAzure 的資料和記錄檔。 相較之下太[案例 #2 下方][planning-guide-5.1.2]、 保留 hello 主機名稱、 SAP SID 和 SAP 使用者帳戶在 hello Azure VM 中，為 hello 在內部部署環境中設定。 因此，將一般化 hello 映像不需要。 請參閱章節[將 VM 從內部部署 tooAzure 使用非一般化磁碟準備][ planning-guide-5.2.1]在內部部署準備步驟及將非一般化 Vm 或 Vhd tooAzure 上的傳此文件。 讀取章[案例 3： 將 VM 從內部部署使用非一般化 Azure VHD 和 SAP] [ deployment-guide-3.4]在 hello[部署指南 》] [ deployment-guide]如需部署在 Azure 中的這類映像的詳細步驟。

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>使用客戶特定的映像部署 VM
因為 OS 或 DBMS 版本 toospecific 修補程式需求，提供 hello hello Azure Marketplace 中的映像可能不適合您的需求。 因此，您可能需要 toocreate 使用您自己 'private' OS/DBMS VM 映像，之後數次可部署的 VM。 tooprepare 這類的 'private' 映像進行複製，hello 下列項目有 toobe 考量：

- - -
> ![Windows][Logo_Windows] Windows
>
> 請參閱以下更多詳細資料： <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> hello Windows 設定 （例如 Windows SID 和主機名稱） 必須是 hello 內部部署上摘錄/一般化VM 經由 hello sysprep 命令。
>
>
> ![Linux][Logo_Linux] Linux
>
> 請依照下列文章中所述的 hello 步驟[SUSE][virtual-machines-linux-create-upload-vhd-suse]， [Red Hat][virtual-machines-linux-redhat-create-upload-vhd]，或[Oracle Linux][ virtual-machines-linux-create-upload-vhd-oracle]，tooprepare VHD toobe 上傳 tooAzure。
>
>

- - -
如果您已在內部部署 VM （特別是 2 層系統） 中安裝 SAP 內容，hello 部署的 hello Azure VM 透過 hello 執行個體重新命名程序支援 hello SAP 軟體佈建之後，您可以調整 hello SAP 系統設定管理員 (SAP 附註[1619720])。 請參閱章節[準備使用部署 VM 的客戶特定映像為 SAP] [ planning-guide-5.2.2]和[上傳 VHD 從內部部署 tooAzure] [ planning-guide-5.3.2]在內部部署準備步驟及將一般化 VM tooAzure 上的傳此文件。 讀取章[案例 2： 使用部署 VM 的自訂映像為 SAP] [ deployment-guide-3.3]在 hello[部署指南 》] [ deployment-guide]如需詳細的部署步驟此映像在 Azure 中。

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>部署 hello Azure Marketplace 中的 VM
您想要 toouse Microsoft 或協力廠商提供的 VM 映像從 hello Azure Marketplace toodeploy VM。 部署在 Azure VM 之後，請依照 hello 相同的指導方針和工具 tooinstall hello SAP 軟體和 （或) 在 VM 內的 DBMS 像您一樣在內部部署環境中。 如需詳細的部署說明，請參閱章節[案例 1： 部署 hello 適用於 SAP 的 Azure Marketplace 中的 VM] [ deployment-guide-3.2]在 hello[部署指南 》] [deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>使用適用於 Azure 的 SAP 準備 VM
將 Vm 上傳至 Azure 之前，您需要 toomake 確定 hello Vm 和 Vhd 符合某些需求。 有根據 hello 部署方法所使用的小差異。

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>將 VM 從內部部署 tooAzure 使用非一般化磁碟準備
常見的部署方法是 toomove 現有 VM 從內部部署 tooAzure 執行 SAP 系統。 VM 和 hello hello VM 只應該在執行 Azure 中，使用中的 SAP 系統 hello 相同的主機名稱，以及很可能 hello 相同 SAP SID。 在此情況下 hello 客體 OS 的 VM 不應該有多個部署的一般化。 如果 hello 與內部網路已延伸至 Azure (請參閱第章[跨單位-部署的單一或多個 SAP Vm 至 hello 需求完全整合至 hello 與內部網路與 Azure] [planning-guide-2.2]本文件中)，然後甚至可以 hello VM 內使用相同的網域帳戶，使用之前在內部部署的 hello。

準備您自己的 Azure VM 磁碟時的需求如下︰

* 原本 hello VHD 包含 hello 作業系統可能會有大小上限為 127 GB 只。 這項限制也會在 2015 年 3 月的 hello 結尾處取得刪除。 現在 hello 包含 hello 作業系統的 VHD 最長可能會在大小 too1TB 任何 Azure 儲存體以及裝載 VHD。
* 它需要 toobe hello 固定 VHD 格式中。 Azure 尚未支援動態 VHD 或 VHDx 格式的 VHD。 當您上傳與 PowerShell 指令程式或 CLI hello VHD 動態 Vhd 將會轉換的 toostatic Vhd
* 掛接的 toohello VM 且應該固定 VHD 格式以及 Azure toohello VM 需要 toobe 中再次掛接的 Vhd。 如需資料磁碟的大小限制，請參閱[這篇文章 (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) 和[這篇文章 (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows)。 當您上傳與 PowerShell 指令程式或 CLI hello VHD 動態 Vhd 將會轉換的 toostatic Vhd
* 新增可使用具有系統管理員權限可供 Microsoft 支援服務或指派做為服務和應用程式中的 toorun 環境直到 VM 部署的 hello 與更適當的使用者的本機帳戶。
* 使用僅限雲端的部署案例的 hello 案例 (請參閱第章[-僅限雲端的虛擬機器部署到 Azure 無相依性 hello 內部部署客戶網路][ planning-guide-2.1]這個文件） 搭配使用此部署方法，在 Azure 中部署 hello Azure 磁碟之後，帳戶可能無法運作的網域。 這特別適用於使用的 toorun 如同 hello DBMS 或 SAP 應用程式的服務帳戶。 因此您需要 tooreplace 這類 VM 本機帳戶的網域帳戶，並刪除 hello VM 中的 hello 在內部部署網域帳戶。 保留在內部部署網域使用者 hello VM 映像中不是問題時 hello VM 部署在 hello 跨內部單位案例中章節所述[跨單位-部署的單一或多個 SAP Vm 至 Azure 的 hello 需求完全整合到 hello 與內部網路][ planning-guide-2.2]本文件中。
* 如果網域帳戶做為 DBMS 登入或使用者執行 hello 系統內部以及這些 Vm 時應該 toobe 部署在僅限雲端的情況下，，需要 toobe 刪除 hello 網域使用者。 您需要 toomake 已 hello 本機系統管理員，再加上另一個 VM 本機使用者加入為登入/使用者到 hello DBMS 中成為系統管理員。
* 視需要新增其他本機帳戶這些可能是 hello 特定部署案例。

- - -
> ![Windows][Logo_Windows] Windows
>
> 在此案例中的 hello VM 沒有一般化 (sysprep) 是必要的 tooupload，及部署 hello Azure 上的 VM。
> 請確定並未使用磁碟機 D:\，
> 並如本文件中的[為連接的磁碟設定自動掛接][planning-guide-5.5.3]一章所述，為連接的磁碟設定磁碟自動掛接。
>
> ![Linux][Logo_Linux] Linux
>
> 在此案例中沒有一般化 (waagent-取消佈建) 的 hello VM 是必要的 tooupload 和部署 hello Azure 上的 VM。
> 確定不會使用 /mnt/resource，並透過 uuid 掛接所有磁碟。 Hello OS 磁碟，請確定 hello 開機載入器項目也會反映 hello uuid 型掛接。
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>準備使用客戶特定的映像為 SAP 部署 VM
含有一般化 OS 的 VHD 檔案會儲存在 Azure 儲存體帳戶的容器中或作為受控磁碟映像。 您可以部署新的 VM，從這類映像參考做為來源，在您的部署範本檔案中的 hello VHD 或管理的磁碟映像，如本章所述[案例 2： 使用部署 VM 的自訂映像為 SAP] [ deployment-guide-3.3]的 hello[部署指南 》][deployment-guide]。

準備您自己的 Azure VM 映像時的需求包括︰

* 原本 hello VHD 包含 hello 作業系統可能會有大小上限為 127 GB 只。 這項限制也會在 2015 年 3 月的 hello 結尾處取得刪除。 現在 hello 包含 hello 作業系統的 VHD 最長可能會在大小 too1TB 任何 Azure 儲存體以及裝載 VHD。
* 它需要 toobe hello 固定 VHD 格式中。 Azure 尚未支援動態 VHD 或 VHDx 格式的 VHD。 當您上傳與 PowerShell 指令程式或 CLI hello VHD 動態 Vhd 將會轉換的 toostatic Vhd
* 掛接的 toohello VM 且應該固定 VHD 格式以及 Azure toohello VM 需要 toobe 中再次掛接的 Vhd。 如需資料磁碟的大小限制，請參閱[這篇文章 (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) 和[這篇文章 (Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows)。 當您上傳與 PowerShell 指令程式或 CLI hello VHD 動態 Vhd 將會轉換的 toostatic Vhd
* 因為所有 hello 註冊為 hello VM 中的使用者不會在僅限雲端的案例中存在的網域使用者 (請參閱第章[-僅限雲端的虛擬機器部署到 Azure 無相依性 hello 內部部署客戶網路][planning-guide-2.1]的這份文件)，使用這類帳戶可能無法運作，一旦 hello 映像部署在 Azure 中的網域服務。 這特別適用於使用的 toorun 像 DBMS 或 SAP 應用程式的服務帳戶。 因此您需要 tooreplace 這類 VM 本機帳戶的網域帳戶，並刪除 hello VM 中的 hello 在內部部署網域帳戶。 保留在內部部署網域使用者 hello VM 映像中不可能發生問題時 hello VM 部署在 hello 跨內部單位案例中章節所述[跨單位-部署的單一或多個 SAP Vm 至 Azure 的 hello 需求完全整合至 hello 與內部網路][ planning-guide-2.2]本文件中。
* 新增可使用具有系統管理員權限可供 Microsoft 支援部門用於問題調查，或指派做為服務和應用程式中的 toorun 環境直到 VM 部署的 hello 和更適當的使用者的本機帳戶。
* 在僅限雲端部署和網域帳戶做為 DBMS 登入或使用者執行時 hello 系統在內部部署位置，應該刪除 hello 網域使用者。 您必須確定 hello 本機系統管理員，再加上另一個 VM 本機使用者新增為 hello DBMS 系統管理員的身分登入/使用者 toomake。
* 視需要新增其他本機帳戶這些可能是 hello 特定部署案例。
* 如果 hello 映像包含的 SAP NetWeaver 安裝和重新命名的 hello hello hello Azure 部署的 hello 點的原始名稱的主機名稱可能是，則建議的 toocopy hello 最新版的 hello SAP 軟體佈建 Manager dvd 放入hello 範本。 這可讓您 tooeasily 使用 hello SAP 提供重新命名功能 tooadapt hello 變更主機名稱和/或變更 hello SID hello hello 內的 SAP 系統部署 VM 映像，一旦啟動新的複本。

- - -
> ![Windows][Logo_Windows] Windows
>
> 請確定並未使用磁碟機 D:\，並如本文件中的[為連接的磁碟設定自動掛接][planning-guide-5.5.3]一章所述，為連接的磁碟設定磁碟自動掛接。
>
> ![Linux][Logo_Linux] Linux
>
> 確定不會使用 /mnt/resource，並透過 uuid 掛接所有磁碟。 Hello OS 磁碟，請確定 hello 開機載入器項目也會反映 hello uuid 型掛接。
>
>

- - -
* SAP GUI (用於管理和安裝) 可預先安裝在這類範本中。
* 其他軟體可以安裝已成功在跨單位案例中的 Vm，只要此軟體可與 hello 必要 toorun hello 重新命名的 hello VM。

如果 hello VM 夠備妥 toobe 泛型和最終獨立的帳戶/使用者 hello 中無法使用目標 Azure 部署案例，會將此映像一般化的 hello 最後準備步驟進行。

##### <a name="generalizing-a-vm"></a>一般化 VM
- - -
> ![Windows][Logo_Windows] Windows
>
> hello 最後一個步驟是 toolog tooa VM 以系統管理員帳戶中。 以「系統管理員」身分開啟 Windows 命令視窗。 移 too%windir%\windows\system32\sysprep and execute sysprep.exe。
> 隨即會出現一個小視窗。 這是重要的 toocheck hello [一般化] 選項 （hello 預設為不勾選），並從其預設值是 '重新啟動' too'Shutdown 變更 hello 關機選項 '。 此程序假設 hello sysprep 程序會執行的內部 hello 的 VM 客體作業系統中。
> 如果您想 tooperform hello 程序已在 Azure 中執行 vm 時，請依照下列中所述的 hello 步驟[本文](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource)。
>
> ![Linux][Logo_Linux] Linux
>
> [如何為資源管理員範本 Linux 虛擬機器 toouse toocapture][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>在內部部署 tooAzure 之間傳輸 Vm 和 Vhd
由於上傳 VM 映像和磁碟 tooAzure 不是可透過 hello Azure 入口網站，您必須 toouse Azure PowerShell cmdlet 或 CLI。 另一個可能性是 hello 工具 'AzCopy' hello 用法。 hello 工具可以在內部部署與 Azure 之間複製 Vhd （在兩個方向）。 它也可以在 Azure 區域之間複製 VHD。 如需了解如何下載及使用 AzCopy，請參閱[這份文件][storage-use-azcopy]。

第三個替代會 toouse 各種協力廠商 GUI 導向工具。 不過，請確定這些工具支援 Azure 分頁 Blob。 針對我們的目的我們需要 toouse Azure 分頁 Blob 儲存 (hello 差異如下所示： <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>)。 也提供 Azure 的 hello 工具可以非常有效率地壓縮 hello Vm 和 Vhd 所需要 toobe 上傳。 這是很重要，因為此壓縮效率可縮短 hello 上傳時間 （hello 上傳連結 toohello 網際網路 hello 在內部部署設備和 hello Azure 部署區域從目標還是而有所不同）。 它是一項公平假設，上載 VM 或 VHD 從歐洲地區 toohello 美國 Azure 資料中心將會花費超過上傳 hello 相同的 Vm/Vhd toohello 歐洲 Azure 資料中心。

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>上傳 VHD 從內部部署 tooAzure
現有的 VM 或 VHD hello 從內部網路這類 VM 或 VHD 需要 toomeet hello 需求，如下所示章 tooupload[將 VM 從內部部署 tooAzure 使用非一般化磁碟準備][planning-guide-5.2.1]的這份文件。

這類 VM 不需要 toobe 一般化，可以在 hello 狀態和後關機 hello 內部端，它有的圖形中上傳。 hello 也適用於其他 Vhd 也不包含任何作業系統。

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>上傳 VHD 並將其設為 Azure 磁碟
在此情況下我們想 tooupload VHD，不論有無作業系統中，並將其裝載 tooa 當做資料磁碟的 VM 或使用做為作業系統磁碟。 這是一個多步驟程序

**Powershell**

* 記錄 tooyour 訂用帳戶中*登入 AzureRmAccount*
* 設定的內容，您的訂用帳戶 hello*組 AzureRmContext*及參數訂用帳戶 Id 或訂用帳戶名稱-請參閱<https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* 上傳 hello 與 VHD*新增 AzureRmVhd* tooan Azure 儲存體帳戶-請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* （選擇性）從 hello VHD 建立受管理的磁碟與*新增 AzureRmDisk* -請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* 設定新的 VM 組態 toohello VHD hello OS 磁碟] 或 [管理磁碟*組 AzureRmVMOSDisk* -請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* 從 hello VM 組態，以建立新的 VM*新增 AzureRmVM* -請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* 新增資料磁碟 tooa 與新的 VM*新增 AzureRmVMDataDisk* -請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Azure CLI 2.0**

* 記錄 tooyour 訂用帳戶中*az 登入*
* 使用 *az account set --subscription `<subscription name or id`>* 來選取您的訂用帳戶
* 上傳 hello 與 VHD *az 儲存體 blob 上傳*-請參閱[使用 hello 與 Azure 儲存體的 Azure CLI][storage-azure-cli]
* （選擇性）從 hello VHD 建立受管理的磁碟與*az 磁碟建立*-請參閱 https://docs.microsoft.com/cli/azure/disk#create
* 建立新的 VM 指定 hello 當做上傳 VHD 或管理的磁碟與作業系統磁碟*az vm 建立*和參數*-附加 os 磁碟*
* 新增資料磁碟 tooa 與新的 VM *az vm 磁碟附加*和參數*-新增*

**範本**

* 上傳 VHD 使用 Powershell 或 Azure CLI hello
* （選擇性）從 hello 與 Powershell、 Azure CLI 或 hello Azure 入口網站的 VHD 建立受管理磁碟
* Hello VM 部署使用 JSON 範本中所示，參考 hello VHD[此範例 JSON 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json)或使用受管理的磁碟中所示[此範例 JSON 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json)。

#### <a name="deployment-of-a-vm-image"></a>VM 映像的部署
現有的 VM 或 VHD hello 從內部網路中的順序 toouse 它做為 Azure VM 映像這類 VM 或 VHD 是否需要 toomeet hello 需求章節中所列的 tooupload[準備使用部署 VM 的客戶特定映像為 SAP] [ planning-guide-5.2.2]的這份文件。

* 使用*sysprep* Windows 上或*waagent-取消佈建*Linux toogeneralize 上您的 VM-請參閱[Sysprep 技術參照](https://technet.microsoft.com/library/cc766049.aspx)適用於 Windows 或[如何 toocapture為資源管理員範本的 Linux 虛擬機器 toouse] [ capture-image-linux-step-2-create-vm-image] for Linux
* 記錄 tooyour 訂用帳戶中*登入 AzureRmAccount*
* 設定的內容，您的訂用帳戶 hello*組 AzureRmContext*及參數訂用帳戶 Id 或訂用帳戶名稱-請參閱<https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* 上傳 hello 與 VHD*新增 AzureRmVhd* tooan Azure 儲存體帳戶-請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* （選擇性）建立受管理的磁碟映像從 hello VHD 與*新增 AzureRmImage* -請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* 設定新的 VM 組態 toothe hello OS 磁碟
  * VHD (使用 *Set-AzureRmVMOSDisk -SourceImageUri -CreateOption fromImage*) - 請參閱 <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
  * 受控磁碟映像 *Set-AzureRmVMSourceImage* - 請參閱 <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage>
* 從 hello VM 組態，以建立新的 VM*新增 AzureRmVM* -請參閱<https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Azure CLI 2.0**

* 使用*sysprep* Windows 上或*waagent-取消佈建*Linux toogeneralize 上您的 VM-請參閱[Sysprep 技術參照](https://technet.microsoft.com/library/cc766049.aspx)適用於 Windows 或[如何 toocapture為資源管理員範本的 Linux 虛擬機器 toouse] [ capture-image-linux-step-2-create-vm-image] for Linux
* 記錄 tooyour 訂用帳戶中*az 登入*
* 使用 *az account set --subscription `<subscription name or id`>* 來選取您的訂用帳戶
* 上傳 hello 與 VHD *az 儲存體 blob 上傳*-請參閱[使用 hello 與 Azure 儲存體的 Azure CLI][storage-azure-cli]
* （選擇性）建立受管理的磁碟映像從 hello VHD 與*az 映像建立*-請參閱 https://docs.microsoft.com/cli/azure/image#create
* 建立新的 VM 指定 hello 當做上傳 VHD 或受管理的磁碟映像的 OS 磁碟*az vm 建立*和參數*-映像*

**範本**

* 使用*sysprep* Windows 上或*waagent-取消佈建*Linux toogeneralize 上您的 VM-請參閱[Sysprep 技術參照](https://technet.microsoft.com/library/cc766049.aspx)適用於 Windows 或[如何 toocapture為資源管理員範本的 Linux 虛擬機器 toouse] [ capture-image-linux-step-2-create-vm-image] for Linux
* 上傳 VHD 使用 Powershell 或 Azure CLI hello
* （選擇性）從 hello 與 Powershell、 Azure CLI 或 hello Azure 入口網站的 VHD 建立受管理的磁碟映像
* Hello VM 部署使用 JSON 範本中所示，參考 hello 映像 VHD[此範例 JSON 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json)或使用 hello 管理磁碟映像中所示[此範例 JSON 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json)。

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>下載 Vhd 或管理磁碟 tooon 內部部署
Azure 基礎結構即服務不是單向的僅能 tooupload Vhd 和 SAP 系統。 您可以移動 SAP 系統從 Azure 送回 hello 內部世界。

Hello hello 階段期間下載 hello Vhd 或受管理的磁碟無法啟動。 即使是下載掛接的 tooVMs 的磁碟，hello VM 需要 toobe 關閉並取消配置。 如果您只想 toodownload hello 資料庫內容的則應該使用新的系統 tooset 內部，而且如果可接受的 hello hello 階段期間下載及 hello hello hello 系統在 Azure 中的新系統的安裝程式可以依然可運作您無法執行壓縮的資料庫備份到磁碟來避免長的停機時間，並且只下載該磁碟，而不必同時下載 OS 基本 VM hello。

#### <a name="powershell"></a>Powershell

  * 下載受控磁碟  
  您必須先 tooget 存取 toohello 基礎 hello 受管理磁碟的 blob。 然後您可以複製 hello 基礎 blob tooa 新儲存體帳戶，並從這個儲存體帳戶下載 hello blob。

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * 下載 VHD  
  一旦 hello SAP 系統已停止，而且 hello 關閉 VM，您可以使用在 hello hello PowerShell 指令程式儲存 AzureRmVhd 內部目標 toodownload hello VHD 磁碟回到 toohello 內部世界。 中，您需要的 hello VHD，您可以在 hello ' 儲存體區段 中找到的 hello URL 的 hello 順序 toodo Azure 入口網站 （需要 toonavigate toohello 儲存體帳戶和 hello 儲存體 hello VHD 已建立的容器），且需要的 tooknow hello VHD 應該儲存複製到。

  然後您可以利用 hello 命令，只定義 hello 參數 SourceUri hello VHD toodownload 和 hello LocalFilePath hello URL 做為 hello 的 hello VHD （包括其名稱） 的實體位置。 hello 命令如下：

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  如需詳細的 hello 儲存 AzureRmVhd cmdlet 的詳細資訊，請參閱以下<https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>。

#### <a name="cli-20"></a>CLI 2.0
  * 下載受控磁碟  
  您必須先 tooget 存取 toohello 基礎 hello 受管理磁碟的 blob。 然後您可以複製 hello 基礎 blob tooa 新儲存體帳戶，並從這個儲存體帳戶下載 hello blob。
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * 下載 VHD   
  一旦 hello SAP 系統已停止，而且 hello 關閉 VM，您可以使用 hello Azure CLI 命令_azure 儲存體 blob 下載_hello 在內部部署目標上 toodownload hello VHD 磁碟回復 toohello 內部世界。 中，您需要 hello 名稱及 hello 容器的 hello VHD，您可以在 hello ' 儲存體區段 中找到的 hello 順序 toodo Azure 入口網站 （需要 toonavigate toohello 儲存體帳戶和 hello 儲存體 hello VHD 已建立的容器），且需要 tooknow 位置hello VHD 應該複製到。

  然後您可以利用 hello 命令，只定義 hello 參數 blob 和容器的 hello VHD toodownload 和 hello 目的地，做為 hello 實體的目標位置的 hello VHD （包括其名稱）。 hello 命令如下：

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>在 Azure 內傳輸 VM 和磁碟
#### <a name="copying-sap-systems-within-azure"></a>在 Azure 內複製 SAP 系統
SAP 系統或甚至專用的 DBMS 伺服器支援的 SAP 應用程式層會可能包含數個磁碟，其中包含可能是 OS hello 與 hello 二進位檔或 hello 資料和記錄檔案中的 hello SAP 資料庫。 Hello 複製磁碟的 Azure 功能都 hello Azure 功能，將儲存磁碟 tooa 本機磁碟的已同步處理機制，以同步方式將快照集多個磁碟。 因此，hello hello 複製或狀態儲存磁碟，即使它們都已掛接 hello 針對相同的 VM 會有不同。 這表示，在具有不同的資料和記錄 hello 不同的磁碟中包含的 hello 具體案例，hello 結尾中的 hello 資料庫會是不一致。

**結論： 順序 toocopy] 或 [儲存磁碟的一部分的 SAP 系統設定您需要 toostop hello SAP 系統，而且也需要向 hello tooshut 部署 VM。然後您可以複製或下載磁碟 tooeither hello 組，只建立一份 hello SAP 系統在 Azure 或內部部署。**

資料可以儲存為 VHD 檔案位於 Azure 儲存體帳戶、 磁碟可以是直接連接的 tooa 虛擬機器或作為映像。 在此情況下，hello VHD 會是複製的 tooanother 位置，才能附加的 toohello 虛擬機器。 hello Azure 中的 hello VHD 檔案的完整名稱必須是在 Azure 中獨一無二的。 已經稍早所述，hello 名稱是種類型的三部分名稱所示：

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

資料磁碟也可以是受控磁碟。 在此情況下，hello 受管理磁碟會使用新的受管理磁碟之前附加的 toohello 虛擬機器的 toocreate。 hello hello 受管理磁碟名稱必須是唯一的資源群組中。

##### <a name="powershell"></a>Powershell
中所示，您可以使用 Azure PowerShell cmdlet toocopy VHD[本文][storage-powershell-guide-full-copy-vhd]。 toocreate 一個新的受管理磁碟，請使用新增 AzureRmDiskConfig 和新增 AzureRmDisk hello 下列範例所示。

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>CLI 2.0
中所示，您可以使用 Azure CLI toocopy VHD[本文][storage-azure-cli-copy-blobs]。 使用新的受管理磁碟，toocreate *az 磁碟建立*hello 下列範例所示。

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Azure 儲存體工具
* <http://storageexplorer.com/>

您可以在下面找到 Azure 儲存體總管的專業版︰

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

VHD 本身的儲存體帳戶中的 hello 副本就是需要幾秒鐘 （類似 tooSAN 硬體以延遲複製，並複製建立快照集，在寫入） 的處理序。 您已擁有 hello VHD 檔案的副本之後您可以將它附加 tooa 虛擬機器或使用它做為映像 tooattach hello VHD toovirtual 機器的複本。

##### <a name="powershell"></a>Powershell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>CLI 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>在 Azure 儲存體帳戶之間複製磁碟
無法在 hello Azure 入口網站上執行這項工作。 您可以使用 Azure PowerShell Cmdlet、Azure CLI 或協力廠商儲存體瀏覽器。 hello PowerShell cmdlet 或 CLI 命令可以建立和管理跨儲存體帳戶和 hello Azure 訂用帳戶內的各區域包括 hello 能力 tooasynchronously 複製 blob 的 blob。

##### <a name="powershell"></a>Powershell
您也可以訂用帳戶之間複製 VHD。 如需詳細資訊，請參閱[這篇文章][storage-powershell-guide-full-copy-vhd]。

hello 的 hello PS 指令程式邏輯的基本流程看起來像這樣：

* 建立儲存體帳戶內容的 hello**來源**儲存體帳戶*新增 AzureStorageContext* -請參閱<https://msdn.microsoft.com/library/dn806380.aspx>
* 建立儲存體帳戶內容的 hello**目標**儲存體帳戶*新增 AzureStorageContext* -請參閱<https://msdn.microsoft.com/library/dn806380.aspx>
* 開始使用 hello 複製

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* 檢查 hello 的迴圈中的 hello 複本狀態

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* 附加 hello 新 VHD tooa 虛擬機器，如上面所述。

如需範例，請參閱[這篇文章][storage-powershell-guide-full-copy-vhd]。

##### <a name="cli-20"></a>CLI 2.0
* 開始使用 hello 複製

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* 如果 hello 檢查 hello 狀態中的迴圈複本

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* 附加 hello 新 VHD tooa 虛擬機器，如上面所述。

如需範例，請參閱[這篇文章][storage-azure-cli-copy-blobs]。

### <a name="disk-handling"></a>磁碟處理
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>SAP 部署的 VM/磁碟結構
在理想情況下 hello 處理 VM 的 hello 結構和相關聯的 hello 磁碟應該非常簡單。 在內部部署安裝中，客戶開發了許多方法來結構化伺服器安裝。

* 其中包含 hello OS 一個基底磁碟上，所有的 hello 二進位碼檔案的 hello DBMS 和/或 SAP。 自 2015 年 3 月，此磁碟可以是總大小，而不是受限制的舊版限制 too1TB too127GB。
* 一或多個磁碟，其中包含 hello DBMS hello SAP 資料庫的檔案和記錄 hello hello DBMS 暫存儲存區記錄檔 （如果 hello DBMS 支援此）。 如果 hello 資料庫記錄 IOPS 需求很高，您需要 toostripe 順序 tooreach hello IOPS 磁碟區所需的多個磁碟。
* 包含一或兩個 hello SAP 資料庫的資料庫檔案和 hello DBMS 暫存資料檔以及 （如果 hello DBMS 支援） 的磁碟數目。

![適用於 SAP 之 Azure IaaS VM 的參考組態][planning-guide-figure-1300]

[comment]: <> (MShermannd TODO 描述 Linux 結構)

- - -
> ![Windows][Logo_Windows] Windows
>
> 對許多客戶我們可了解組態，例如，SAP 和 DBMS 二進位檔上未安裝 hello 作業系統安裝所在的 hello c:\ 磁碟機。 有各種原因，這麼做，但回溯源頭時 toohello 根，通常就是，hello 磁碟機太小，OS 升級需要的額外空間 10-15 年前。 最近則不太常發生這兩種情況。 現今 hello c:\ 磁碟機可以對應大型磁碟區磁碟或 Vm 上。 在順序 tookeep 部署簡單的結構中，是建議 toofollow SAP NetWeaver 系統在 Azure 中的下列部署模式
>
> hello Windows 作業系統分頁檔應該放在 hello d： 磁碟機 （非持續性磁碟）
>
> ![Linux][Logo_Linux] Linux
>
> 中所述，在 Linux 上放置 /mnt /mnt/retention/ 資源下的 hello Linux 交換檔[本文][virtual-machines-linux-agent-user-guide]。 hello 交換檔可以設定 hello hello /etc/waagent.conf Linux 代理程式組態檔中。 新增或變更下列設定的 hello:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

tooactivate hello 變更，您需要 toorestart hello 與 Linux 代理程式

```
sudo service waagent restart
```

請參閱 SAP 附註[1597355]如需有關 hello 建議交換檔的大小

- - -
hello hello DBMS 資料檔案和 hello 類型的這些磁碟裝載的 Azure 儲存體使用的磁碟數目應該取決 hello IOPS 需求和所需的 hello 延遲。 如需確切配額的說明，請參閱[這篇文章 (Linux)][virtual-machines-sizes-linux] 和[這篇文章 (Windows)][virtual-machines-sizes-windows]。

SAP 部署透過 hello 過去 2 年內的經驗過關部分課程其中可以摘要如下：

* IOPS 流量 toodifferent 資料檔案不一定相同因為現有的客戶系統可能會以不同的方式調整資料檔案代表其 SAP 資料庫的 hello。 因此事實上 toobe 更多個磁碟 tooplace hello 資料檔案超出所規劃 Lun 使用 RAID 組態。 有個情況下，特別是在 Azure 標準儲存體 IOPS 速率要叫用 hello 與 hello DBMS 交易記錄檔的單一磁碟配額。 在這類案例建議 hello 使用進階儲存體或或者彙總多個標準儲存體磁碟使用軟體 RAID。

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Azure 虛擬機器中的 SQL Server 效能最佳做法][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [在 Linux 上設定軟體 RAID][virtual-machines-linux-configure-raid]
> * [在 Azure 中的 Linux VM 上設定 LVM][virtual-machines-linux-configure-lvm]
> * [Azure 儲存體密碼和 Linux I/O 最佳化](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* 進階儲存體顯示效能大幅提升，特別是針對重要的交易記錄寫入。 對於是效能類似的預期的 toodeliver 實際執行的 SAP 案例，強烈建議 toouse VM 系列，可以運用 Azure 高階儲存體。

Hello 磁碟包含 hello 作業系統，請記住，且為建議，hello SAP 和 hello 資料庫 (基本 VM) 的二進位檔，不再限制的 too127GB。 它現在最多可以有 too1TB 的大小。 這應該是所有 hello 包括所需的檔案，例如足夠空間 tookeep、 SAP 批次工作記錄。

如需其他建議和詳細資訊，特別是關於 DBMS Vm，請參閱 hello[的 DBMS 部署指南][dbms-guide]

#### <a name="disk-handling"></a>磁碟處理
在大部分情況下您需要 hello VM toocreate 順序 toodeploy hello SAP 資料庫中的其他磁碟。 我們討論的章節中的磁碟數目上 hello 考量[SAP 部署的 VM/磁碟內存結構][ planning-guide-5.5.1]的這份文件。 hello Azure 入口網站可讓 tooattach 和部署基本 VM 之後，中斷連接磁碟。 hello 磁碟可以附加/卸離 hello VM 已啟動，以及停止時執行。 附加磁碟時, hello Azure 入口網站提供 tooattach 空的磁碟或現有的磁碟不在此時間點是附加 tooanother VM。

**請注意**： 磁碟在任何給定時間只能附加的 tooone VM。

![連接/中斷連接 Azure 標準儲存體的磁碟][planning-guide-figure-1400]

Hello 在部署期間的新的虛擬機器，您可以決定是否 toouse 管理磁碟，或將您的磁碟放在 Azure 儲存體帳戶。 如果您想 toouse 高階儲存體，我們建議使用受管理的磁碟。

接下來，您需要 toodecide，是否要 toocreate 新的和空的磁碟，或您是否要 tooselect，先前上傳也應該將現有磁碟附加 toohello VM。

**重要**： 您**不**想 toouse 主機快取與 Azure 標準儲存體。 您應該將 hello 預設是無保留 hello 主機快取喜好設定。 Azure 高階儲存體具有您應該啟用讀取快取如果 hello I/O 特性大部分是讀取對資料庫資料檔的一般 I/O 流量。 在資料庫交易記錄檔中，不建議使用快取。

- - -
> ![Windows][Logo_Windows] Windows
>
> [Tooattach 資料 hello Azure 入口網站中的磁碟][virtual-machines-linux-attach-disk-portal]
>
> 如果已連接磁碟，您會需要 toolog toohello VM tooopen hello Windows 磁碟管理員中。 如果依照章節中的建議未啟用自動掛接[設定自動掛接，如附加磁碟][planning-guide-5.5.3]，hello 新附加的磁碟區需要 toobe 採取上線和初始化。
>
> ![Linux][Logo_Linux] Linux
>
> 如果已連接磁碟，您需要 toolog toohello VM 中的，並初始化 hello 磁碟中所述[這篇文章][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
如果 hello 新磁碟是空的磁碟，您會需要 tooformat hello 磁碟。 格式化時，特別是針對 DBMS 資料和記錄檔 hello 套用 DBMS 裸機部署的 hello 與相同的建議。

如先前章節中所述[hello Microsoft Azure 虛擬機器概念][planning-guide-3.2]，Azure 儲存體帳戶不提供無限資源 I/O 容量、 IOPS 及資料量。 這點對 DBMS VM 的影響通常最大。 如果您有幾個高 I/O 磁碟區的 Vm toodeploy 中的 hello Azure 儲存體帳戶的磁碟區的 hello 限制內的順序 toostay，可能最佳 toouse 個別的儲存體帳戶，每個 VM。 否則，您需要 toosee 如何您就可以平衡這些 Vm 之間不同的儲存體帳戶，而不叫用的每個單一儲存體帳戶的 hello 限制。 更多詳細資料會討論 hello[的 DBMS 部署指南][dbms-guide]。 針對完全使用 SAP 應用程式伺服器 VM，或最後可能需要更多 VHD 的其他 VM，您也應該記住這些限制。 如果您使用受控磁碟，並不適用這些限制。 如果您計劃 toouse 高階儲存體，我們建議使用受管理的磁碟。

另一個主題是關於儲存體帳戶是 hello 儲存體帳戶中的 Vhd 是否要取得地理複寫。 啟用或停用 hello 儲存體帳戶層級上，而不是在 VM 層級 hello 地理複寫。 如果已啟用地理複寫，hello Vhd 中儲存體帳戶會複寫到另一個 Azure 資料中心內的 hello hello 相同的區域。 做此決定之前，您應該考慮下列限制的 hello:

Azure 地理複寫在 VM 中的每個 VHD 本機運作，並不會複寫到在 VM 中的多個 Vhd hello IOs 依時間先後順序。 因此，hello 代表 hello 基本 VM，以及任何其他的 Vhd 附加 toohello VM 的 VHD 會複寫彼此獨立。 這表示沒有在 hello hello 變更之間的同步處理不同的 Vhd。 hello hello IOs 的事實會複寫與 hello 順序無關的寫法是表示具有資料庫分散至多個 Vhd 的資料庫伺服器的值不是，地理複寫。 在加法 toohello DBMS，也可能會有其他應用程式處理程序在寫入或操作不同 Vhd 中以及其所處變更重要 tookeep hello 順序的資料。 如果這是必要條件，則不應該在 Azure 中啟用 [異地複寫]。 根據您是否需要或想要對一組 VM 進行異地複寫，但不對另一組進行異地複寫，您可能已將 VM 及其相關的 VHD 分類到已啟用或停用 [異地複寫] 的不同儲存體帳戶。

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>為連接的磁碟設定自動掛接
- - -
> ![Windows][Logo_Windows] Windows
>
> 對於從自有映像或磁碟建立的 Vm，它是必要的 toocheck 然後可能將 hello 自動掛接參數設定。 設定此參數可讓 hello VM 之後重新啟動或重新部署在 Azure toomount hello 已連接/掛接磁碟機再次自動。
> hello 參數會設定由 Microsoft 提供 hello Azure Marketplace 中的 hello 映像。
>
> 順序 tooset hello 自動掛接，請參閱 hello 的 hello 命令列可執行檔 diskpart.exe 的說明文件：
>
> * [DiskPart 命令列選項](https://technet.microsoft.com/library/bb490893.aspx)
> * [Automount (自動掛接)](http://technet.microsoft.com/library/cc753703.aspx)
>
> hello 應該以系統管理員身分開啟命令列視窗的視窗。
>
> 如果已連接磁碟，您會需要 toolog toohello VM tooopen hello Windows 磁碟管理員中。 如果依照章節中的建議未啟用自動掛接[設定自動掛接，如附加磁碟][planning-guide-5.5.3]，hello 新連接的磁碟區 > 需要 toobe 採取上線和初始化。
>
> ![Linux][Logo_Linux] Linux
>
> 中所述，您會需要 tooinitialize 新附加空磁碟[本文][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]。
> 您也需要新磁碟 toohello /etc/fstab tooadd。
>
>

- - -
### <a name="final-deployment"></a>最終部署
如需 hello 最後的部署和確切步驟，尤其是與相關事宜 toohello 部署 SAP Extended Monitoring，請參閱 toohello[部署指南 》][deployment-guide]。

## <a name="accessing-sap-systems-running-within-azure-vms"></a>存取在 Azure VM 中執行的 SAP 系統
僅限雲端的情況下，您可能需要 tooconnect toothose SAP 系統之間 hello 使用 SAP GUI 公用網際網路。 這些情況下，hello 下列程序需要 toobe 套用。

我們將討論的 hello 文件中稍後 hello 其他的主要狀況，在跨單位部署中具有站對站連線 （VPN 通道） 或 Azure ExpressRoute 連線 hello 在內部部署系統和 Azure 系統之間的連線 tooSAP 系統。

### <a name="remote-access-toosap-systems"></a>遠端存取 tooSAP 系統
與 Azure 資源管理員會有任何預設端點不再像 hello 先前傳統模型中。 只要符合下列情況，就可以開啟 Azure ARM VM 的所有連接埠︰

1. 沒有網路安全性群組定義 hello 子網路或 hello 網路介面。 網路流量 tooAzure Vm 可以透過所謂 「 網路安全性群組 」 保護。 如需詳細資訊，請參閱[什麼是網路安全性群組 (NSG)？][virtual-networks-nsg]
2. 沒有 Azure 負載平衡器定義 hello 網路介面   

中所述，請參閱 hello 架構差異傳統的模型和 ARM[本文][virtual-machines-azure-resource-manager-architecture]。

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Hello 僅限雲端案例的 SAP 系統和 SAP GUI 連線能力的組態
本文描述的詳細資料 toothis 主題，請參閱： <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>變更 VM 中的防火牆設定
它可能是必要的 tooconfigure hello 防火牆上的虛擬機器 tooallow 輸入流量 tooyour SAP 系統。

- - -
> ![Windows][Logo_Windows] Windows
>
> 根據預設，會開啟 hello Azure 部署的 VM 內的 Windows 防火牆。 接著，您必須開啟 tooallow hello SAP 連接埠 toobe，否則 hello SAP GUI 不將能 tooconnect。
> toodo 這樣：
>
> * 開啟 控制台 \ 系統及安全性 \windows 防火牆 too'Advanced 設定。
> * 現在以滑鼠右鍵按一下 [輸入規則]，然後選擇 [新增規則]。
> * 在 hello 下列精靈選擇 toocreate 新 'Port' 的規則。
> * 在 hello 精靈的下一個步驟中 hello，hello 將設定保留在 TCP，並輸入 hello 您想要的連接埠號碼 tooopen。 因為我們的 SAP 執行個體 ID 為 00，所以我們採用 3200。 如果您的執行個體有不同的執行個體數目，則應該開啟 hello 定義連接埠您稍早根據 hello 執行個體數目。
> * 在 hello hello 精靈部分下一步，您需要 tooleave hello 項目 [允許連線] 核取。
> * Hello 的 hello 精靈的下一個步驟中您會需要 toodefine 是否 hello 規則適用於網域、 私人和公用網路。 請調整其如果必要 tooyour 需要。 不過，您需要從外部透過公用網路的 hello 的 hello 連接 SAP gui，toohave hello 套用規則 toohello 公用網路。
> * 在 hello 的 hello 精靈的最後一個步驟，hello 規則然後按 [完成] 儲存
>
> hello 規則會立即生效。
>
> ![連接埠規則定義][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> 依預設在 hello Azure Marketplace 中的 hello Linux 映像並啟用 hello iptables 防火牆和 hello 連接 tooyour SAP 系統應該會運作。 如果您啟用 iptables 或其他防火牆，iptables toohello 文件，請參閱，或使用 hello 防火牆 tooallow 太輸入 tcp 流量 （其中 xx 是 hello 的 SAP 系統的系統編號） 的連接埠 32xx。
>
>

- - -
#### <a name="security-recommendations"></a>安全性建議
hello SAP GUI 不會立即連線 tooany 的 hello SAP 執行個體 (連接埠 32xx) 正在執行，但是第一次連接透過 hello 開啟連接埠 toohello SAP 訊息伺服器程序 (連接埠 36xx)。 在 hello 過去 hello 相同的連接埠已用於 hello 訊息伺服器 hello 內部通訊 toohello 應用程式執行個體。 tooprevent 內部應用程式伺服器不慎與訊息中的伺服器內部 Azure hello 通訊的通訊連接埠可以變更。 強烈建議 toochange hello 之間的內部通訊 hello SAP 訊息伺服器和其應用程式執行個體 tooa 不同的通訊埠編號已經從內部部署系統，例如適用於專案測試的開發的複製品已複製的系統上等等。這可以使用 hello 預設設定檔參數來完成：

> rdisp/msserv_internal
>
>

如中所述[hello SAP 訊息伺服器的安全性設定](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>SAP 執行個體的僅限雲端部署概念
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>搭配 SAP NetWeaver 示範/訓練案例的單一 VM
![Azure 雲端服務中執行單一 VM SAP 示範系統以 hello 相同 VM 名稱，隔離][planning-guide-figure-1700]

在此案例中 (請參閱第章[僅限雲端][ planning-guide-2.1]的這份文件)，我們實作典型的訓練/示範系統案例，其中包含 hello 整個訓練/示範案例的單一 VM 中。 我們假設 hello 部署透過 VM 映像範本完成。 我們也假設其中多個以 hello 擁有 hello 的 Vm 部署這些示範/訓練 Vm 需要 toobe 相同名稱。

hello 假設是章的某些小節所述，建立 VM 映像[準備 Vm 與 Azure 的 SAP] [ planning-guide-5.2]本文件中。

事件 tooimplement hello 案例的 hello 順序看起來像這樣：

##### <a name="powershell"></a>Powershell
* 為每個訓練/示範環境建立新的資源群組

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* 如果您不想 toouse 管理磁碟，建立新的儲存體帳戶

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* 建立新的虛擬網路 hello 每個訓練/示範橫向 tooenable hello 使用相同的主機名稱和 IP 位址。 網路安全性群組，只允許流量 tooport 3389 tooenable 遠端桌面存取和連接埠 22 SSH 受 hello 虛擬網路。

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* 建立新的公用 IP 位址可能是使用的 tooaccess hello 虛擬機器從 hello 網際網路

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* 建立新的網路介面 hello 虛擬機器

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* 建立虛擬機器。 Hello 僅限雲端案例中每個 VM 都有 hello 相同的名稱。 hello hello 這些 Vm 中的執行個體將會是 SAP NetWeaver 的 SAP SID hello 相同也一樣。 內 hello Azure 資源群組，hello hello VM 名稱需要 toobe 唯一的但您可以在不同的 Azure 資源群組中執行 Vm 以 hello 相同的名稱。 hello 預設 'Administrator' 帳戶的 Windows 或 linux 的 ' root' 不是有效。 因此，新的系統管理員使用者名稱需要 toobe 定義連同密碼。 hello hello VM 大小也需要定義 toobe。

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* 選擇性地新增其他磁碟，並還原所需的內容。 請注意，所有 blob 名稱 (Url toohello blob) 必須都是在 Azure 中獨一無二。

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
下列範例程式碼的 hello 可用在 Linux 上。 對於 Windows，請使用 PowerShell，如上面所述或調整 hello 範例 toouse %rgname%而不是 $rgName 再設定 hello 環境變數使用 hello Windows 命令*設定*。

* 為每個訓練/示範環境建立新的資源群組

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* 建立新的儲存體帳戶

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* 建立新的虛擬網路 hello 每個訓練/示範橫向 tooenable hello 使用相同的主機名稱和 IP 位址。 網路安全性群組，只允許流量 tooport 3389 tooenable 遠端桌面存取和連接埠 22 SSH 受 hello 虛擬網路。

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* 建立新的公用 IP 位址可能是使用的 tooaccess hello 虛擬機器從 hello 網際網路

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* 建立新的網路介面 hello 虛擬機器

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* 建立虛擬機器。 Hello 僅限雲端案例中每個 VM 都有 hello 相同的名稱。 hello hello 這些 Vm 中的執行個體將會是 SAP NetWeaver 的 SAP SID hello 相同也一樣。 內 hello Azure 資源群組，hello hello VM 名稱需要 toobe 唯一的但您可以在不同的 Azure 資源群組中執行 Vm 以 hello 相同的名稱。 hello 預設 'Administrator' 帳戶的 Windows 或 linux 的 ' root' 不是有效。 因此，新的系統管理員使用者名稱需要 toobe 定義連同密碼。 hello hello VM 大小也需要定義 toobe。

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* 選擇性地新增其他磁碟，並還原所需的內容。 請注意，所有 blob 名稱 (Url toohello blob) 必須都是在 Azure 中獨一無二。

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>範本
您可以在 github 上的 hello azure-快速入門範本儲存機制使用 hello 範例範本。

* [簡單的 Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [簡單的 Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [來自映像的 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>實作一組 Vm 需要 toocommunicate 在 Azure 中的
此項僅限雲端的案例是訓練和示範用途的典型案例其中 hello 代表 hello 示範/訓練案例的軟體分佈於多個 Vm。 hello hello 不同 Vm 需要 toocommunicate 彼此中安裝了不同的元件。 同樣地，在此案例中，不需要內部部署網路通訊或跨單位案例。

此案例中是章節所述的 hello 安裝的擴充[單一 VM 與 SAP NetWeaver 示範/訓練案例][ planning-guide-7.1]的這份文件。 在此情況下更多虛擬機器將加入 tooan 現有的資源群組。 Hello 在下列範例 hello 訓練橫向包含 SAP ASCS/SCS VM 執行 DBMS 和 SAP 應用程式伺服器執行個體 VM 的 VM。

建立這種情況下您必須先 toothink 有關 hello 案例之前已執行的基本設定。

#### <a name="resource-group-and-virtual-machine-naming"></a>資源群組和虛擬機器命名
所有資源群組名稱必須是唯一的。 請開發您自己的資源命名配置，例如 `<rg-name`>-尾碼。

hello 虛擬機器名稱中有 toobe 唯一 hello 的資源群組中。

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>設定網路之間的通訊 hello 不同的 Vm
![Azure 虛擬網路內的 VM 集合][planning-guide-figure-1900]

tooprevent 命名衝突的 hello 複製程式碼相同的訓練/示範環境，您需要每個橫向 toocreate Azure 虛擬網路。 將由 Azure 提供的 DNS 名稱解析，或者您可以設定 Azure (不 toobe 進一步這裡所討論) 外部 DNS 伺服器。 在本例中，我們不會設定自己的 DNS。 針對一個 Azure 虛擬網路內的所有虛擬機器，會啟用透過主機名稱進行通訊。

hello 理由 tooseparate 訓練或示範環境的虛擬網路，而不只是資源群組可能會：

* hello SAP 橫向的需要設定自己的 AD/OpenLDAP 和 hello 環境的每個網域的伺服器需求 toobe 部分。  
* 因為設定有元件具有固定 IP 位址，需要 toowork hello SAP 環境。

Azure 虛擬網路和如何 toodefine 它們可以在中找到更多詳細[本文][virtual-networks-create-vnet-arm-pportal]。

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>部署具有公司網路連線能力的 SAP VM (跨單位)
您執行 SAP 環境，而且想 toodivide hello 部署之間高階 DBMS 伺服器的裸機、 應用程式層級和較小的 2 層在內部部署虛擬化環境設定 SAP 系統和 Azure IaaS。 hello 基本假設是一個 SAP 環境內的 SAP 系統需要 toocommunicate 與彼此、 與許多其他 hello 家公司的何種部署形式獨立部署的軟體元件。 也應該有任何差異 hello 部署形式 hello 終端使用者使用 SAP GUI 或其他介面連接。 我們有時，可以只符合這些條件 hello 內部部署 Active Directory/OpenLDAP 和 DNS 服務延伸 toohello 透過站台-到-站台/多站台連線能力或私人連線，例如 Azure ExpressRoute 的 Azure 系統。

在多個背景的 SAP on Azure 的 hello 實作詳細資料的順序 tooget，我們建議您 tooread 章[概念的純雲端部署的 SAP 執行個體][ planning-guide-7]本文件的說明hello 基本概念的某些建構 Azure 與這些使用方式與在 Azure 中的 SAP 應用程式。

### <a name="scenario-of-an-sap-landscape"></a>SAP 環境的案例
hello 跨內部單位案例可以大致上描述類似下方的 hello 圖形中：

![內部部署與 Azure 資產之間的站對站連線能力][planning-guide-figure-2100]

如上所示的 hello 案例說明 hello 內部部署 AD/OpenLDAP，DNS 會擴充 tooAzure 的案例。 在 hello 內部端，每個 Azure 訂用帳戶保留特定 IP 位址範圍。 hello IP 位址範圍會指派 hello Azure 端上的 tooan Azure 虛擬網路。

#### <a name="security-considerations"></a>安全性考量
hello 最小需求是安全的通訊協定 hello 使用例如 SSL/TLS 的瀏覽器存取或 VPN 式連線讓系統存取 toohello Azure 服務。 hello 假設是公司處理非常不同的 hello 其公司網路與 Azure 之間的 VPN 連線。 有些公司可能會開放所有 hello 連接埠。 有些公司可能會想 toobe 非常精確的連接埠需要 tooopen 等等。

在典型的 SAP 的 hello 表會列出通訊連接埠。 基本上它是足夠 tooopen hello SAP 閘道連接埠。

| 服務 | 連接埠名稱 | 範例 `<nn`> = 01 | 預設範圍 (最小值-最大值) | 註解 |
| --- | --- | --- | --- | --- |
| 發送器 |sapdp`<nn>` 請參閱 * |3201 |3200 - 3299 |SAP 發送器，供 Windows 和 Java 的 SAP GUI 使用 |
| 訊息伺服器 |sapms`<sid`> 請參閱 ** |3600 |任意 sapms`<anySID`> |sid = SAP 系統 ID |
| 閘道器 |sapgw`<nn`> 請參閱 * |3301 |任意 |SAP 閘道，用於 CPIC 和 RFC 通訊 |
| SAP 路由器 |sapdp99 |3299 |任意 |僅 CI （中央執行個體） 的服務名稱可以指派在 /etc/services tooan 任意值，安裝之後。 |

*) nn = SAP 執行個體號碼

**) sid = SAP 系統 ID

如需不同 SAP 產品或 SAP 產品所提供的服務所需之連接埠的詳細資訊，請參閱 <http://scn.sap.com/docs/DOC-17124>。
與這個文件，您應該能夠 tooopen 專用 hello VPN 裝置所需的特定 SAP 產品和案例中的連接埠。

其他安全性量值在此案例中部署 Vm，則可能是 toocreate 時[網路安全性群組][ virtual-networks-nsg] toodefine 存取規則。

### <a name="dealing-with-different-virtual-machine-series"></a>面對不同的虛擬機器系列
在 hello 課程中前 12 個月的 Microsoft 加入更多 VM 類型不同 Vcpu 數目、 記憶體中或更重要的是硬體上執行。 SAP 並未針對所有這些 VM 都提供支援 (請參閱 SAP 附註 [1928533]中支援的 VM 類型)。 其中一些 VM 會在不同世代的主機硬體上執行。 取得部署這些主機硬體層代在 hello 資料粒度的 Azure 延展單位。 方法的情況下可能會發生其中 hello 無法在執行您選擇不同 VM 大小 hello 相同的延展單位。 可用性設定組中 hello 能力 toospan 延展單位根據不同的硬體的限制。  例如，如果您想要 toorun hello A5 A11 Vm 上的 DBMS hello G 系列 Vm 上的 SAP 應用程式層，會強制 toodeploy 單一的 SAP 系統或在不同的可用性設定組內的不同 SAP 系統。

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>在 Azure 中從 SAP 執行個體的區域網路印表機進行列印
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>在跨單位案例中透過 TCP/IP 進行列印
您在內部部署 TCP/IP 網路印表機的 Azure VM 中設定為與您的公司網路，前提您在相同沒有 VPN 站台-站通道或 ExpressRoute 連線建立的整體 hello。

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo 這樣：
>
> * 有些網路印表機隨附的組態精靈，可讓 Azure VM 中輕鬆 tooset 註冊您的印表機。 如果沒有精靈軟體已隨附的印表機 hello"manual"方式 hello 印表機 tooset toocreate 新 TCP/IP 印表機連接埠。
> * 開啟 [控制台] -> [裝置和印表機] -> [新增印表機]
> * 選擇 [使用 TCP/IP 位址或主機名稱新增印表機]
> * 輸入 hello hello 印表機的 IP 位址
> * 印表機連接埠標準 9100
> * 如有必要請手動安裝 hello 適當的印表機驅動程式。
>
> ![Linux][Logo_Linux] Linux
>
> * 像是 Windows 只要按照 hello 標準程序 tooinstall 網路印表機
> * 只要遵循的 hello 公用 Linux 指南[SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html)或[Red Hat 和 Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html)如何 tooadd 印表機。
>
>

- - -
![網路列印][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>在跨單位案例中透過 SMB 的主機型印表機 (共用印表機)
根據設計，主機型印表機與網路不相容。 但只要 hello 印表機連線的 tooa 開機的電腦，可以在網路上電腦之間共用主機型印表機。 請以站對站或 ExpressRoute 方式連線到您的公司網路，並共用您的本機印表機。 hello SMB 通訊協定而不是 DNS 使用 NetBIOS，做為名稱服務。 hello NetBIOS 主機名稱可以不同於 hello DNS 主機名稱。 hello 標準情況是 hello NetBIOS 主機名稱和 hello DNS 主機名稱完全相同。 hello DNS 網域不具意義 hello NetBIOS 命名空間中。 因此，hello hello DNS 主機名稱所組成的完整的 DNS 主機名稱和 DNS 網域必須不能用於 hello NetBIOS 命名空間。

hello 印表機共用是 hello 網路中的唯一名稱來識別：

* （永遠需要） 的 hello SMB 主機的主機名稱。
* Hello 共用 （永遠需要） 的名稱。
* 如果印表機共用不在 hello hello 網域名稱與 SAP 系統的相同網域。
* 此外，使用者名稱和密碼可能會需要的 tooaccess hello 印表機共用。

作法：

- - -
> ![Windows][Logo_Windows] Windows
>
> 共用您的本機印表機。
> 在 hello Azure VM 中，開啟 hello Windows 檔案總管和 hello 共用名稱中的 hello 印表機的類型。
> 印表機安裝精靈將引導您完成 hello 安裝程序。
>
> ![Linux][Logo_Linux] Linux
>
> 以下是有關在 Linux 中設定網路印表機，或包含在 Linux 中列印之相關章節的一些文件範例。 它就能 hello Azure Linux VM 只要 hello VM 中的相同方式是 VPN 的一部分：
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL 或 Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>USB 印表機 (印表機轉送)
中的 hello 遠端桌面服務 tooprovide 使用者 hello 存取 Azure 的 hello 能力 tootheir 本機印表機裝置遠端工作階段中的無法使用。

- - -
> ![Windows][Logo_Windows] Windows
>
> 使用 Windows 列印的更多詳細資料，請參閱：<http://technet.microsoft.com/library/jj590748.aspx>。
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>在跨單位中將 SAP Azure 系統整合到 Correction and Transport System (TMS)
hello SAP 變更和傳輸系統 (TMS) 需要設定 toobe tooexport 和 hello 橫向中的系統之間匯入傳輸要求。 我們假設 SAP 系統 (DEV) hello 開發執行個體位於 Azure 中而 hello 品質保證 (QA) 和生產性系統 (PRD) 是在內部部署。 此外，假設有一個中央傳輸目錄。

##### <a name="configuring-hello-transport-domain"></a>設定傳輸網域 hello
您指定為 hello 傳輸網域控制站中所述的 hello 系統上設定傳輸網域[設定 hello 傳輸網域控制站](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm)。 系統使用者 TMSADM 將會建立需要有和 hello 將產生的 RFC 目的地。 您可以查看使用 hello 交易 SM59 這些 RFC 連線。 您必須在傳輸網域內啟用主機名稱解析。

作法：

* 在我們的案例中，我們決定 hello 內部部署 QAS 系統將會 hello CTS 網域控制站。 呼叫交易 STMS。 hello TMS 對話方塊隨即出現。 [Configure Transport Domain]\(設定傳輸網域) 對話方塊隨即顯示 (只有在您尚未設定傳輸網域時，才會顯示此對話方塊)。
* 請確定自動建立 hello 使用者 TMSADM 已獲授權 (SM59-> ABAP 連線-> TMSADM@E61.DOMAIN_E61 ]-> [詳細資料]-> [Utilities(M)-> 授權測試)。 hello 初始畫面上的交易 STMS 應該會顯示此 SAP 系統現在就做 hello 控制站的 hello 傳輸網域如下所示：

![Hello 網域控制站上的交易 STMS 初始畫面][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>SAP 系統加入傳輸網域 hello
SAP 系統加入傳輸網域中的 hello 順序如下所示：

* 在 hello DEV 系統在 Azure 中，移 toohello 傳輸系統 (Client 000) 並呼叫交易 STMS。 從 hello 對話方塊中，選擇 其他組態，並繼續進行將系統加入網域。 指定為目標主機的 hello 網域控制站 ([將 SAP 系統加入傳輸網域 hello 中](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm))。 等候 toobe hello 傳輸網域中包含的現在 hello 系統。
* 基於安全性理由，您必須 toogo 後 toohello 網域控制站 tooconfirm 您的要求。 選擇 系統概觀 和 核准的 hello 等待中系統。 然後確認 hello 提示和 hello 設定將散佈。

此 SAP 系統現在包含 hello 必要資訊所有 hello hello 傳輸網域中的其他 SAP 系統。 在 hello 相同的時間，hello 位址 tooall hello 其他 SAP 系統，而且 hello 的 hello 傳輸控制程式的傳輸設定檔中輸入 hello SAP 系統，會傳送 hello 新 SAP 系統的資料。 請檢查 Rfc 和 hello 網域存取 toohello 傳輸目錄是否運作。

如往常般 hello 文件中所述繼續 hello 您系統的設定傳輸[變更和傳輸系統](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)。

作法：

* 確定您在內部部署的 STMS 已正確設定。
* 請確定您在 Azure 反之亦然上的虛擬機器可以解析 hello hello 傳輸網域控制站主機名稱。
* 呼叫交易 STMS -> [Other Configuration]\(其他組態) -> [Include System in Domain]\(將系統加入網域)。
* 確認內部部署 TMS 系統上的 hello 中的 hello 連接。
* 像往常一樣，設定傳輸路由、群組和層級。

在 站對站連線的跨單位案例中，在內部部署與 Azure 之間的 hello 延遲仍然很嚴重。 如果我們依照傳輸物件經由開發和測試系統 tooproduction hello 順序，或考慮套用傳輸或支援封裝 toohello 不同系統，您會發現，取決於 hello 中央傳輸 hello 位置hello 系統目錄中，會發生高延遲讀取或寫入 hello 中央傳輸目錄中的資料。 hello 的情況是類似 tooSAP 橫向設定其中 hello 不同系統分布於相距遙遠 hello 資料中心使用不同資料中心。

在排序這類延遲周圍 toowork 與擁有更快讀取或寫入 tooor 從 hello 傳輸目錄，您可以設定兩個 STMS 傳輸網域 （一個用於內部部署。 而另一個為 hello 系統 Azure 和連結 hello 傳輸網域中的 hello 系統 請參閱此文件，其中說明 hello SAP TMS 中此概念背後的 hello 原則： <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/38dd924eb711d182bf0000e829fbfe/frameset.htm>。

作法：

* 使用交易 STMS 在每個位置 (內部部署和 Azure) 設定傳輸網域 <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* 連結的定義域連結的 hello 定義域，並確認 hello hello 兩個網域之間的連結。
  <http://help.sap.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/content.htm>
* 將發佈 hello 組態 toohello 連結系統。

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>在 Azure 中及內部部署的 SAP 執行個體之間的 RFC 流量 (跨單位)
系統之間的內部部署和 Azure 中的 RFC 流量必須 toowork。 連線 tooset 呼叫交易 SM59 來源系統中，您需要 toodefine hello 目標系統 RFC 連線。 hello 組態是類似的 toohello 標準設定 RFC 連線。

我們假設在 hello 跨內部部署案例中，可以在需要彼此 toocommunicate 哪些執行的 SAP 系統的 hello Vm hello 相同的網域。 因此 hello RFC 連線 SAP 系統之間的安裝程式不會與差異 hello 設定步驟和內部部署案例中的輸入。

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>從 Azure 中的 SAP 執行個體存取「本機」檔案共用，反之亦然
位於 Azure 中的 SAP 執行個體需要 hello 公司內部的 tooaccess 檔案共用。 此外，在內部部署 SAP 執行個體必須位於 Azure tooaccess 檔案共用。 您必須設定 hello 權限和 hello 本機系統上的共用選項 tooenable hello 檔案共用。 請確定上 hello VPN 或 ExpressRoute 連線在 Azure 與您的資料中心之間的 tooopen hello 連接埠。

## <a name="supportability"></a>支援能力
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>適用於 SAP 的 Azure 監視解決方案
在訂單 tooenable hello 監視關鍵任務 SAP 系統上 Azure hello SAP 監控工具 SAPOSCOL 或 SAP Host Agent 會取得 hello 透過 Azure Monitoring Extension for SAP 的 Azure 虛擬機器服務主機關閉的資料。 因為 sap hello 要求 tooSAP 的非常特定的應用程式，所以 Microsoft 決定 toogenerically 實作所需的 hello 功能至 Azure，但將它保留為客戶 toodeploy hello 必要監視元件和組態 tootheir在 Azure 中執行的虛擬機器。 不過，您將大部分由 Azure 自動部署和生命週期管理的監視元件的 hello。

#### <a name="solution-design"></a>解決方案設計
hello 方案開發的 tooenable SAP Monitoring 以 Azure VM 代理程式和擴充功能架構的 hello 架構為基礎。 hello hello Azure VM Agent and Extension 架構概念是 tooallow 安裝的軟體應用程式可在 VM 內的 hello Azure VM 延伸模組組件庫中。 hello 此概念背後的概念是 tooallow （在像 hello Azure Monitoring Extension for SAP 的情況下） 的原則，hello 的特殊功能的 VM 與 hello 設定此類軟體在部署階段的部署。

hello ' Azure VM 代理程式 」，可讓 VM 插入 Windows Vm 預設會在建立 VM hello Azure 入口網站中的 hello 內的特定 Azure VM 延伸模組的處理。 如果發生 SUSE、 Red Hat 或 Oracle Linux，hello VM 代理程式已經是 Azure Marketplace 映像的一部分。 萬一其中一個會將從 Linux VM 上傳內部 tooAzure hello VM 代理程式有 toobe 手動安裝。

hello Azure hello 監控解決方案的基本建置組塊，如 SAP 看起來像這樣：

![Microsoft Azure 擴充功能元件][planning-guide-figure-2400]

Hello 區塊上圖所示，hello 的 SAP 監控解決方案的一個部分會裝載於 hello Azure VM 映像和 Azure 延伸模組庫即由 Azure Operations 管理的全球複寫儲存機制。 它負責 hello hello hello Azure 實作 SAP toowork hello Azure Monitoring Extension for SAP 的 Azure 作業 toopublish 新版本上使用聯合 SAP/MS 小組。

當您部署新的 Windows VM 時，hello ' Azure VM 代理程式 」 會自動加入到 hello VM。 此代理程式的 hello 函式是載入 toocoordinate hello 和 hello Azure 延伸模組設定 SAP NetWeaver 系統的監視。 適用於 Linux Vm hello Azure VM 代理程式已經是 hello Azure Marketplace 作業系統映像的一部分。

不過，沒有仍然需要 toobe hello 客戶所執行的步驟。 這是 hello 啟用及設定 hello 效能集合。 hello 程序的相關 toohello 「 設定 」 會自動化的 PowerShell 指令碼或 CLI 命令。 hello 中所述，hello PowerShell 指令碼可以在 hello Microsoft Azure 指令碼中心下載[部署指南 》][deployment-guide]。

hello 整體架構的 hello Azure 的 SAP 監控解決方案如下：

![適用於 SAP NetWeaver 的 Azure 監視解決方案][planning-guide-figure-2500]

**Hello 確切方式-tooand 如需在部署期間使用這些 PowerShell cmdlet 或 CLI 命令的詳細步驟，請遵循 hello 所提供的 hello 指示[部署指南 》][deployment-guide]。**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>將位於 Azure 的 SAP 執行個體整合到 SAProuter
在 Azure 中執行的 SAP 執行個體需要 toobe 可從 SAProuter 存取以及。

![SAP 路由器網路連線][planning-guide-figure-2600]

SAProuter 可啟用參與系統，如果沒有直接的 IP 連線之間的 hello TCP/IP 通訊。 這會提供網路層級上沒有 hello 通訊夥伴之間的端對端連線是必要的 hello 優點。 hello SAProuter 會接聽連接埠 3299 預設值。
tooconnect SAP 執行個體透過 SAProuter 您需要 toogive hello SAProuter 字串和主機名稱與任何嘗試 tooconnect。

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
到目前為止 hello 焦點 hello 文件的一般情況下被 SAP NetWeaver 或 hello SAP NetWeaver ABAP 堆疊。 在這一小節列出 hello SAP Java 堆疊的特定考量。 其中一個最重要的 SAP NetWeaver Java 專門架構的應用程式的 hello 為 hello SAP 企業入口網站。 其他 SAP NetWeaver 架構的應用程式，例如 SAP PI 和 SAP Solution Manager 使用 hello SAP NetWeaver ABAP 和 Java 堆疊。 因此，有當然是需要 tooconsider 特定層面相關的 toohello SAP NetWeaver Java 堆疊以及。

### <a name="sap-enterprise-portal"></a>SAP 企業版入口網站
SAP 入口網站在 Azure 虛擬機器中的 hello 安裝與在內部部署安裝沒有差異，如果您要在跨單位案例中部署。 因為 DNS 由內部部署的 hello，hello hello 個別執行個體的連接埠設定可設定在內部部署。 hello 建議和目前為止，本文件中描述的限制適用於 SAP 企業入口網站或 hello SAP NetWeaver Java 堆疊等應用程式一般。

![公開的 SAP 入口網站][planning-guide-figure-2700]

有些客戶的特殊的部署案例時，hello hello SAP 企業入口網站 toohello 網際網路直接暴露 hello 虛擬機器主機是透過站對站 VPN 通道或 ExpressRoute 連線的 toohello 公司網路。 此案例中，您必須確定特定連接埠已開啟且未被防火牆或網路安全性群組封鎖 toomake。 hello 相同機制需要 toobe 您要從內部部署在僅限雲端案例的 tooconnect tooan SAP Java 執行個體時套用。

hello 初始入口網站 URI 是 http （s）：`<Portalserver`>: 5XX00/irj 50000 加上 （Systemnumber × 100） 格式 hello 連接埠的位置。 hello 預設入口網站 URI 的 SAP 系統 00 是`<dns name`>。`<azure region`>.Cloudapp.azure.com:PublicPort/irj。 如需詳細資訊，請參閱 <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>。

![端點組態][planning-guide-figure-2800]

如果您想 toocustomize hello URL 和/或 SAP 企業入口網站的連接埠，請參閱這份文件：

* [Change Portal URL (變更入口網站 URL)](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Change Default port numbers, Portal port numbers (變更預設連接埠號碼、入口網站連接埠號碼)](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Azure 虛擬機器上執行之 SAP NetWeaver 的高可用性 (HA) 和災害復原 (DR)
### <a name="definition-of-terminologies"></a>術語定義
hello 詞彙**高可用性 (HA)**通常相關的 tooa 設定的技術，藉由提供業務續航力透過 IT 服務，IT 中斷情況降到最低備援、 容錯或容錯移轉受保護的元件在 hello**相同**資料中心。 在本例中，會是在一個 Azure 區域內。

**災害復原 (DR)** 的目標也是將 IT 服務中斷的情況降到最低，但其復原通常會橫跨距離數百公里遠的**不同**資料中心。 在我們的案例通常 hello 不同 Azure 區域間相同地理政治地區或客戶為您所建立。

### <a name="overview-of-high-availability"></a>高可用性概觀
我們可以分隔 hello 討論 SAP 中的高可用性 Azure 分成兩個部分：

* **Azure 基礎結構高可用性** (例如計算 (VM)、網路、儲存體等的 HA)，以及它在增加 SAP 應用程式可用性方面的優點。
* **SAP 應用程式高可用性** (例如 SAP 軟體元件的 HA)︰
  * SAP 應用程式伺服器
  * SAP ASCS/SCS 執行個體
  * DB 伺服器

以及如何與 Azure 基礎結構 HA 結合。

在 Azure 中 SAP 高可用性有一些差異比較 tooSAP 高可用性的內部部署實體或虛擬環境中。 hello 從 SAP 的下列文件描述在 Windows 上的虛擬化環境中的標準 SAP 高可用性組態： <http://scn.sap.com/docs/DOC-44415>。 不同於 Windows，Linux 沒有整合 sapinst 的 SAP-HA 組態。 如需有關 Linux 之內部部署 SAP HA 的詳細資訊，請參閱︰<http://scn.sap.com/docs/DOC-8541>。

### <a name="azure-infrastructure-high-availability"></a>Azure 基礎結構高可用性
目前 99.9% 都是單一 VM SLA。 tooget 了解如何在單一 VM 的 hello 可用性看起來就像是只可以建立 hello 產品的 hello 不同可用的 Azure Sla: <https://azure.microsoft.com/support/legal/sla/>。

hello 計算 hello 基礎都是 30 天內每月或 43200 分鐘。 因此，0.05%停機對應 too21.6 分鐘的時間。 像往常一樣，hello hello 不同服務可用性會乘以 hello 遵循方法中：

(可用性服務 #1/100) * (可用性服務 #2/100) * (可用性服務 #3/100) *...

例如：

(99.95/100) * (99.9/100) * (99.9/100) = 0.9975 或整體可用性 99.75%。

#### <a name="virtual-machine-vm-high-availability"></a>虛擬機器 (VM) 高可用性
Azure 平台事件可能會影響 hello 可用性的虛擬機器的兩種類型： 維護與非計劃性的維護計畫。

* 規劃的維護事件會定期更新由 Microsoft toohello 基礎 Azure 平台 tooimprove 整體的可靠性、 效能和安全性的虛擬機器執行的 hello 平台基礎結構。
* 當 hello 硬體或基礎虛擬機器的實體基礎結構發生某種錯誤時，就會發生非計劃性的維護事件。 這可能包含本機網路錯誤、本機磁碟錯誤，或其他機架層級的錯誤。 偵測到這類失敗時，hello Azure 平台會自動移轉虛擬機器從 hello 狀況不良的實體伺服器主控虛擬機器 tooa 狀況良好實體伺服器。 這類事件很少見，但也可能會造成虛擬機器 tooreboot。

如需更多詳細資訊，請參閱這份文件︰<http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Azure 儲存體備援
Microsoft Azure 儲存體帳戶中的 hello 資料會一直在複寫的 tooensure 耐久性與高可用性，會議 hello Azure 儲存體 SLA，即使在暫時性硬體故障的 hello 字體。

由於 Azure 儲存體而導致 hello 資料的三個映像，根據預設，就不需要 RAID5 或 RAID1 跨多個 Azure 磁碟。

如需更多詳細資訊，請參閱這篇文章︰<http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>利用 Azure 基礎結構 VM 重新啟動 tooAchieve 的 SAP 應用程式的 「 高可用性 」
如果您決定不像 Windows Server 容錯移轉叢集 (WSFC) 或 on Linux Pacemaker toouse 功能 （目前只支援針對 SLES 12 和更新版本），Azure VM 重新啟動是利用的 tooprotect hello 的規劃與未規劃的停機時間對 SAP 系統Azure 的實體伺服器基礎結構及整體基礎的 Azure 平台。

> [!NOTE]
> 重要 toomention Vm 並不是應用程式，將 Azure VM 重新啟動主要保護它。 VM 重新啟動並未提供 SAP 應用程式的高可用性，而是提供特定基礎結構層級的可用性，因而間接達到 SAP 系統的「更高可用性」。 另外還有任何 SLA 的 hello 花費的時間 toorestart VM 主機計劃性或非計劃性中斷後。 因此，此「高可用性」方法不適用於 SAP 系統的重要元件，例如 (A)SCS 或 DBMS。
>
>

高可用性的另一個重要基礎結構項目是儲存體。 例如，Azure 儲存體 SLA 可用性為 99.9%。 如果使用者將所有 VM 及其磁碟部署到單一 Azure 儲存體帳戶，當 Azure 儲存體可能無法使用時，將會導致 Azure 儲存體帳戶中的所有 VM，以及這些 VM 內執行的所有 SAP 元件都無法使用。  

您也可以針對每個 VM 使用專用儲存體帳戶，而不是將所有 VM 放入單一 Azure 儲存體帳戶；如此一來，您就可以藉由使用多個獨立的 Azure 儲存體帳戶，來增加整體 VM 和 SAP 應用程式可用性。

Azure 受管理的磁碟會自動放入 hello 它們附加到 hello 虛擬機器的容錯網域中。 如果您將兩部虛擬機器的可用性中設定和使用受管理的磁碟，hello 平台將負責散發到不同容錯網域也 hello 管理磁碟。 如果您計劃 toouse 高階儲存體，我們強烈建議也使用管理磁碟。

使用 Azure 基礎結構 HA 和儲存體帳戶之 SAP NetWeaver 系統的範例架構如下所示︰

![利用 Azure 基礎結構 HA tooachieve SAP 應用程式 「 較高 」 的可用性][planning-guide-figure-2900]

使用 Azure 基礎結構 HA 和受控磁碟之 SAP NetWeaver 系統的範例架構如下所示︰

![利用 Azure 基礎結構 HA tooachieve SAP 應用程式 「 較高 」 的可用性][planning-guide-figure-2901]

重要的 SAP 元件我們所達成 hello 遵循為止：

* SAP 應用程式伺服器 (AS) 的高可用性

  SAP 應用程式伺服器執行個體是備援元件。 每個 SAP AS 執行個體都是部署在自己的 VM 上，而此 VM 是在不同的 Azure「容錯網域」及「升級網域」中執行 (請參閱[容錯網域][planning-guide-3.2.1]和[升級網域][planning-guide-3.2.2]章節)。 這是藉由使用「Azure 可用性設定組」來加以確保 (請參閱 [Azure 可用性設定組][planning-guide-3.2.3]一章)。 當 Azure 容錯或升級網域可能因規劃或未規劃而無法使用時，將會導致有限數目的 VM 及其 SAP AS 執行個體無法使用。

  每個 SAP 執行個體都會在自己的 Azure 儲存體帳戶中 - 當一個 Azure 儲存體可能無法使用時，只會導致一個 VM 及其 SAP AS 執行個體無法使用。 不過請注意，一個 Azure 訂用帳戶中的「Azure 儲存體帳戶」數目有限。 tooensure 自動啟動 (A) SCS 執行個體之後 hello VM 重新開機，請確定 tooset hello Autostart 參數 (A) SCS 執行個體中的啟動章節所述的設定檔[使用自動啟動 SAP 執行個體][ planning-guide-11.5].
  如需更多詳細資料，另請參閱 [SAP 應用程式伺服器的高可用性][planning-guide-11.4.1]一章。

  即使您使用受控磁碟，這些磁碟也會儲存在 Azure 儲存體帳戶，而且在儲存體發生中斷時會無法使用。

*  SAP (A)SCS 執行個體可用性

  這裡我們利用 Azure VM 重新啟動 VM 的 tooprotect hello 與已安裝的 SAP (A) SCS 執行個體。 在 hello 案例的規劃或未規劃的停機時間的 Azure 伺服器，將重新啟動 Vm，另一個可用的伺服器上。 如先前所述，Azure VM 重新啟動主要保護 Vm 並不是應用程式時，在此情況下 hello (A) SCS 執行個體。 透過重新啟動 VM 的 hello 我們將達到間接 SAP (A) SCS 執行個體的 「 高可用性 」。 tooinsure 自動啟動 (A) SCS 執行個體之後 hello VM 重新開機，請確定 tooset Autostart 參數 (A) SCS 執行個體中的啟動章節所述的設定檔[使用自動啟動 SAP 執行個體][planning-guide-11.5]。 這表示 hello (A) SCS 執行個體當做單一失敗點 (SPOF) 執行單一 VM 中的 hello 整個 SAP 環境的 hello 可用性 hello 就因素。

*  DBMS 伺服器可用性

  在這裡，類似 toohello SAP (A) SCS 執行個體使用的大小寫、 我們利用 Azure VM 重新啟動 tooprotect hello VM 與已安裝的 DBMS 軟體和我們在達到 「 高可用性 」 的 DBMS 軟體透過 VM 重新啟動。
  單一 VM 中執行 DBMS 也 SPOF，而且它是整個 SAP 環境 hello hello 可用性 hello 就因素。

### <a name="sap-application-high-availability-on-azure-iaas"></a>Azure IaaS 上的 SAP 應用程式高可用性
我們需要 tooprotect tooachieve 完整 SAP 系統高可用性，所有重要的 SAP 系統元件，為範例備援 SAP 應用程式伺服器，以及 SAP (A) SCS 執行個體和 DBMS 等唯一的元件 （例如單一失敗點）。

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>SAP 應用程式伺服器的高可用性
Hello SAP 應用程式伺服器/對話執行個體的不必要 toothink 需特定的高可用性解決方案。 高可用性可直接透過備援來達成，因此必須在不同的虛擬機器中有足夠的備援。 它們應該全部放在相同 Azure 可用性設定組的 hello Vm tooavoid 可能同時更新 hello hello 計劃性的維護停機期間有相同的時間。 hello 基本功能所建置不同的升級和故障 」 網域在 Azure 的擴充單元已經首見於章[升級 」 網域][planning-guide-3.2.2]。 本文件的 [Azure 可用性設定組][planning-guide-3.2.3]一章則提供「Azure 可用性設定組」的說明。

Azure 縮放單位內的 Azure 可用性設定組可使用不限數目的容錯和升級網域。 這表示，將 Vm 數目放入一個可用性設定組，很快多個 VM 最後會送入中 hello 相同錯誤或升級網域。

在其專用的 Vm 中部署一些 SAP 應用程式伺服器執行個體，假設我們有五個升級網域，hello 下列圖片會形成 hello 結束。 hello 未來可能會變更 hello 實際的最大數容錯網域和更新網域內的可用性設定組：

![Azure 中 SAP 應用程式伺服器的 HA][planning-guide-figure-3000]

如需更多詳細資訊，請參閱這份文件︰<http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>在 Windows 上的 hello SAP (A) SCS 執行個體的高可用性
Windows Server 容錯移轉叢集 (WSFC) 是常用的解決方案 tooprotect hello SAP (A) SCS 執行個體。 它也會以「HA 安裝」的形式整合到 sapinst。 在此時間點 hello Azure 基礎結構不能 tooprovide hello 功能 tooset hello 需要 Windows Server 容錯移轉叢集 hello 相同方式完成內部部署設定。

從 2016 年 1 月開始執行 Windows 作業系統 hello hello Azure 雲端平台不提供 hello 可能會使用兩個 Azure Vm 之間共用的磁碟上的叢集共用磁碟區。

有效的方案雖然是 hello 3rd 方軟體來提供同步和透明磁碟複寫，可以整合到 WSFC 共用磁碟區使用量。 這個方式意味著該只有 hello 作用中的叢集節點是無法 tooaccess 一個 hello 磁碟複製一點時間。 年 1 月 2016 此 HA 組態為 Windows 客體作業系統在 Azure Vm 上搭配第 3 合作對象軟體 SIOS DataKeeper 上的支援的 tooprotect hello SAP (A) SCS 執行個體。

hello SIOS DataKeeper 方案提供所需的共用的磁碟叢集資源 tooWindows 容錯移轉叢集：

* 其他的 Azure VHD 附加 tooeach 的 Windows 叢集組態中的 hello 虛擬機器 (Vm)
* 會在兩個 VM 節點上執行 SIOS DataKeeper Cluster Edition
* VHD 具有 SIOS DataKeeper 叢集版本設定以同步方式會反映其他 hello hello 內容的方式從來源 Vm tooadditional VHD 附加磁碟區的目標 VM 附加磁碟區。
* SIOS DataKeeper 是抽象化 hello 來源和目標本機磁碟區，以及顯示這些 tooWindows 當做單一的共用磁碟容錯移轉叢集。

您可以如何找到所有詳細資料中 hello tooinstall Windows 容錯移轉叢集與 SIOS DataKeeper 和 SAP[叢集 SAP ASCS 執行個體使用 Windows Server 容錯移轉叢集與 SIOS DataKeeper Azure 上][ ha-guide-classic]技術白皮書。

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>在 Linux 上的 hello SAP (A) SCS 執行個體的高可用性
自 2015 年 12 月沒有也相當 tooshared 磁碟 WSFC 適用於 Linux Vm 在 Azure 上。 使用協力廠商軟體的替代解決方案 (例如適用於Windows 的 SIOS) 尚未經過驗證，無法在 Azure 上的 Linux 執行 SAP。

#### <a name="high-availability-for-hello-sap-database-instance"></a>Hello SAP 資料庫執行個體的高可用性
hello 一般 SAP DBMS HA 安裝根據 DBMS 高可用性功能，使用其中兩個 DBMS Vm tooreplicate 資料從使用中 DBMS 執行個體 toohello hello 秒到被動的 DBMS 執行個體的 VM。

高可用性和災害復原功能一般與特定 DBMS 中的所述 hello[的 DBMS 部署指南][dbms-guide]。

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>端對端的高可用性 hello 完整的 SAP 系統
以下是 Azure 中完整 SAP NetWeaver HA 架構的兩個範例 - 一個用於 Windows，一個用於 Linux。

Unmanaged 磁碟才： hello 概念如下所述，可能需要 toobe 部署許多 SAP 系統與 hello 部署的 Vm 數目已超過 hello 最大限制儲存體帳戶的每個訂閱時有點入侵。 在這種情況下，Vm 的 Vhd 會需要 toobe 結合一個儲存體帳戶內。 您通常會結合不同 SAP 系統之 SAP 應用程式層 VM 的 VHD 來達成目的。  我們也會將不同 SAP 系統之不同 DBMS VM 的不同 VHD 結合到一個 Azure 儲存體帳戶。 因此記住保留 hello 的 Azure 儲存體帳戶的 IOPS 限制 (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] Windows 上的 HA
![Azure IaaS SQL Server 的 SAP NetWeaver 應用程式 HA 架構][planning-guide-figure-3200]

下列 Azure 結構 hello 適用於 hello SAP NetWeaver 系統基礎結構問題和主機修補所 toominimize 影響：

* hello 完整的系統被部署在 Azure （必要-DBMS 層、 (A) SCS 執行個體和完成的應用程式層需要 toorun 在 hello 相同的位置）。
* hello 完整的系統在一個 Azure 訂閱 （必要） 內執行。
* hello 完整的系統在一個 Azure 虛擬網路 （必要） 內執行。
* 即使是使用所有的 hello Vm 屬於 toohello hello 的 hello 一個 SAP 系統的 Vm 中的分隔成三個可用性設定組有可能相同的虛擬網路。
* 執行一個 SAP 系統之 DBMS 執行個體的所有 VM 都會在一個可用性設定組中。 假設有多個 VM 針對每個系統執行 DBMS 執行個體，因為使用了原生 DBMS 高可用性功能，例如 SQL Server AlwaysOn 或 Oracle Data Guard。
* 所有執行 DBMS 執行個體的 VM 都會使用自己的儲存體帳戶。 DBMS 資料和記錄檔會從一個儲存體帳戶 tooanother 儲存體帳戶使用 DBMS 高可用性功能 hello 資料同步處理複寫。 無法使用的一個儲存體帳戶會導致無法使用的一個 SQL Windows 叢集節點，但不是 hello 整個 SQL Server 服務。
* 執行一個 SAP 系統之 (A)SCS 執行個體的所有 VM 都會在一個可用性設定組中。 設定 Windows Server 容錯移轉叢集 (WSFC) 內的 Vm tooprotect hello (A) SCS 執行個體。
* 所有執行 (A)SCS 執行個體的 VM 都會使用自己的儲存體帳戶。 (A)SCS 執行個體的檔案與 SAP 通用資料夾會從一個儲存體帳戶 tooanother 儲存體帳戶使用 SIOS DataKeeper 複寫複寫。 無法使用的一個儲存體帳戶會導致無法使用其中一個 (A) SCS Windows 叢集節點，但不是 hello 整個 (A) SCS 服務。
* 所有代表 hello SAP 應用程式伺服器層的 hello Vm 位於第三個可用性設定組中。
* 所有的 hello Vm 執行 SAP 應用程式伺服器使用他們自己的儲存體帳戶。 無法使用的一個儲存體帳戶將會造成一個 SAP 應用程式伺服器，讓其他 SAP AS 繼續 toorun 無法使用。

hello 以下圖所示的 hello 相同會橫向使用受管理的磁碟。

![Azure IaaS SQL Server 的 SAP NetWeaver 應用程式 HA 架構][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] Linux 上的 HA
SAP HA 在 Linux on Azure 的 hello 架構基本上是的 hello 與 Windows，做為相同上面所述。 截至 2016 年 6 月為止，Azure 上的 Linux 尚未支援 SAP (A)SCS HA 解決方案

因此 SAP Linux Azure 系統無法達成的 2016 年 1 月 hello 為 SAP Azure 系統相同的可用性，因為遺漏 HA hello (A) SCS 執行個體和 hello 單一執行個體 SAP ASE 資料庫。

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>對 SAP 執行個體使用自動啟動
SAP 提供 hello OS hello VM 中的 hello 開頭之後立即 hello 功能 toostart SAP 執行個體。 hello 確切步驟已記載於 SAP 知識庫文章[1909114]。 不過，SAP 不建議您使用 toouse hello 設定，再因為 hello 順序的執行個體重新啟動時，沒有控制項假設影響多個 VM 收到或每個 VM 執行的多個執行個體。 假設 Azure 典型案例一個 SAP 應用程式伺服器執行個體的單一 VM，最後會開始重新啟動 VM，hello 案例中，hello Autostart 不是真的很重要，而且可以藉由加入這個參數啟用：

    Autostart = 1

Hello 到啟動 hello SAP ABAP 和/或 Java 執行個體的設定檔。

> [!NOTE]
> hello Autostart 參數可以有以及一些困難。 詳細資料，hello 參數觸發程序 hello 相關 hello 執行個體的 Windows/Linux 服務啟動時 hello SAP ABAP 或 Java 執行個體的開頭。 這當然是 hello 案例時 hello 作業系統開機。 不過，SAP 軟體生命週期管理功能 (例如加總或其他更新或升級) 也經常需要重新啟動 SAP 服務。 這些功能不預期會自動重新啟動所有執行個體 toobe。 因此，hello Autostart 參數應該停用然後再執行這類工作。 hello Autostart 參數也不應該對叢集化，例如 ASCS/SCS/CI SAP 執行個體使用。
>
>

如需自動啟動 SAP 執行個體的其他資訊，請參閱︰

* [Start/Stop SAP along with your Unix Server Start/Stop (隨著 Unix 伺服器啟動/停止一起啟動/停止 SAP)](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Starting and Stopping SAP NetWeaver Management Agents (啟動及停止 SAP NetWeaver 管理代理程式)](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Tooenable 如何自動啟動的 HANA 資料庫](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>更大型的 3 層 SAP 系統
稍早的章節中已談到 3 層 SAP 組態的高可用性觀點。 但是，要如何系統 hello DBMS 伺服器要求太大而 toohave 該檔案位於 Azure 中，但無法部署到 Azure 的 hello SAP 應用程式層嗎？

#### <a name="location-of-3-tier-sap-configurations"></a>3 層 SAP 組態的位置
不支援的 toosplit hello 應用程式層本身或 hello 應用程式和 DBMS 層在內部部署與 Azure 之間。 SAP 系統可以完全在內部部署或在 Azure 中部署。 它也不是支援的 toohave 部分 hello 應用程式伺服器在 Azure 中執行內部部署和某些其他人。 這是起始點的 hello 討論 hello。 我們也不支援 toohave hello DBMS SAP 系統的元件，hello 部署在兩個不同的 Azure 區域中的 SAP 應用程式伺服器層。 例如，DBMS 在美國西部，而 SAP 應用程式層在美國中部。 不支援這類設定的原因是 hello SAP NetWeaver 架構的 hello 延遲敏感度。

不過，透過 hello 課程的最後一年的資料中心的協力廠商開發共同位置 tooAzure 區域。 這些共同位置通常是非常接近 toohello 實體 Azure 資料中心內的 Azure 區域。 hello 短距離和資產的 hello 共透過 ExpressRoute 至 Azure 的連線可能會導致是小於 2 毫秒的延遲。 在這種情況下，toolocate hello DBMS 層 （包括儲存體 SAN/NAS） 這類的代管和在 Azure 中的 hello SAP 應用程式層中有可能的。 截至 2015 年 12 月為止，我們沒有這類部署。 但是，具有非 SAP 應用程式部署的其他客戶已採用此方法。

### <a name="offline-backup-of-sap-systems"></a>SAP 系統的離線備份
相依於 hello SAP 組態選擇 （2 層或 3 層） 有可能是需要 tooback 組成。 hello 內容 hello VM 本身加上 toohave hello 資料庫的備份。 hello DBMS 相關的備份是以資料庫方法預期的 toobe。 Hello 不同資料庫的詳細的說明位於[DBMS 指南][dbms-guide]。 在 hello 另一方面，hello SAP 資料可以備份採用離線方式 （包括 hello 資料庫內容） 這一節中所述或線上 hello 下一節中所述。

hello 離線備份基本上需要關機的 hello 透過 hello Azure 入口網站的 VM，以及基本 VM 磁碟 hello 加上所有已連接的磁碟 toohello VM 的複本。 這會保留 hello VM 時間映像中的點和其相關聯的磁碟。 建議 toocopy hello 「 備份 」 到不同的 Azure 儲存體帳戶。 因此 hello 章節所述的程序[Azure 儲存體帳戶之間複製磁碟][ planning-guide-5.4.2]本文件將會套用。
除了使用 hello Azure hello 關閉其中一個入口網站也可以執行它透過 Powershell 或 CLI 如下所述： <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

還原該狀態會包含刪除 hello 的基底 VM 也為 hello 原始磁碟的 hello 基本 VM 與掛接的磁碟，複製回 hello 已儲存的磁碟 toohello 原始儲存體帳戶或資源群組的受管理的磁碟，然後重新部署 hello 系統。
本文示範如何 tooscript 此程序會在 Powershell: <http://www.westerndevs.com/azure-snapshots/>

請先確定 tooinstall 新的 SAP 授權還原上面所述的 VM 備份會建立新的硬體金鑰。

### <a name="online-backup-of-an-sap-system"></a>SAP 系統的線上備份
備份的 DBMS 執行 DBMS 專屬方法與 hello 中所述的 hello [DBMS 指南][dbms-guide]。

Hello SAP 系統內的其他 Vm 可以備份使用 Azure 虛擬機器備份功能。 Azure 虛擬機器備份引進早期 2015年中，並同時是標準方法 tooback 將完整的 vm 在 Azure 中。 Azure 備份儲存在 Azure 中的 hello 備份，並允許虛擬機器還原一次。

> [!NOTE]
> 自 2015 年 12 月使用 VM 備份不會保留 hello 唯一 VM 識別碼是用於 SAP 授權。 這表示從 VM 備份進行還原，需要安裝新的 SAP 授權金鑰示為 hello 已還原的 VM 會被視為 toobe 新的 VM 和已儲存的先前一個取代。
>
> ![Windows][Logo_Windows] Windows
>
> 理論上，執行會備份資料庫以一致的方式以及如果 hello DBMS 系統支援 hello Windows VSS 的 Vm (磁碟區陰影複製服務<https://msdn.microsoft.com/library/windows/desktop/bb968832 (vs.85>)，例如，SQL Server 一樣。
> 不過請注意，您無法根據 Azure VM 備份還原時間點來還原資料庫。 因此，建議使用 DBMS 功能，而不是依賴 Azure VM 備份的資料庫的 tooperform 備份。
>
> 熟悉 Azure 虛擬機器備份 tooget 請從這裡開始： <https://docs.microsoft.com/azure/backup/backup-azure-vms>。
>
> 其他可能性是 toouse 組合 Microsoft Data Protection Manager 安裝在 Azure VM，Azure Backup 備份/還原資料庫。 如需詳細資訊，請參閱：<https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>。  
>
> ![Linux][Logo_Linux] Linux
>
> 沒有任何對等的 tooWindows VSS 在 Linux 中。 因此，您只能進行檔案一致備份，而無法進行應用程式一致備份。 hello SAP DBMS 備份應該使用 DBMS 功能。 hello 包含 hello SAP 相關資料的檔案系統可以儲存，例如，使用 tar 檔案解壓縮述此處： <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure 作為 SAP 生產環境的 DR 網站
Mid 2014，因為 HYPER-V、 系統中心和 Azure 延伸模組 toovarious 元件可讓 Azure 的 hello 使用量執行內部部署 HYPER-V 為基礎的 vm 與 DR 網站。

詳述如何 toodeploy 此解決方案的部落格記載於此： <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>。

## <a name="summary"></a>摘要
hello 關鍵點的高可用性 Azure 中 SAP 系統如下：

* 在此時間點，hello SAP 單一失敗點無法保護完全 hello 相同方式與可在內部部署。 hello 原因是沒有 hello 使用第 3 個合作對象軟體，共用磁碟叢集，無法尚未建置在 Azure 中。
* 對於 hello DBMS 層，您會需要 toouse 不依賴共用的磁碟叢集技術的 DBMS 功能。 詳細資料會記載於 hello [DBMS 指南][dbms-guide]。
* toominimize hello hello Azure 基礎結構或主機維護故障 」 網域內有問題的影響，您應該使用 Azure 可用性設定組：
  * 建議一個 toohave hello SAP 應用程式層可用性設定組。
  * 建議的 toohave hello SAP DBMS 層個別的可用性設定組。
  * 不建議 tooapply hello 相同可用性設定組不同 SAP 系統的 Vm。
  * 建議 toouse 高階管理磁碟。
* 為了備份 hello SAP DBMS 層，請檢查 hello [DBMS 指南][dbms-guide]。
* 備份 SAP Dialog 執行個體就很少的有意義，因為它是通常更快的 tooredeploy 簡單的對話執行個體。
* 備份 hello VM 所在的 hello SAP 系統，並與其 hello 全域目錄 hello 不同執行個體的所有 hello 設定檔就很重要，應該使用 Windows 備份執行或者，，例如 tar 檔案解壓縮在 Linux 上。 由於 Windows Server 2008 (R2) 和 Windows Server 2012 (R2)，使其更容易使用 hello tooback 之間有差異較新的 Windows Server 版本，我們建議 toorun 做為 Windows 客體作業系統的 Windows Server 2012 (R2)。
