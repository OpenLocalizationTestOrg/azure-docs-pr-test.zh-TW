---
title: "aaaGetting 開始使用 Azure Vm 上的 SAP |Microsoft 文件"
description: "了解在 Microsoft Azure 中的虛擬機器 (VM) 上執行的 SAP 解決方案"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a>使用 Azure 來裝載和執行 SAP 工作負載案例
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

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
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
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
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
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
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
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

選擇您的 SAP 準備雲端夥伴身分登入 Microsoft Azure，您便可以 tooreliably 可擴充相容，且企業證實的平台上執行您的關鍵任務 SAP 工作負載和案例。  取得 hello 延展性、 彈性，並節省 Azure 的成本。 使用 Microsoft SAP 之間 hello 展開合作關係，您可以跨 Azure-開發/測試和實際執行案例中執行 SAP 應用程式，並受到完整支援。 從 SAP NetWeaver tooSAP S4/HANA、 SAP BI Linux tooWindows、 SAP HANA tooSQL 我們有涵蓋您。 

除了主機使用的 SAP NetWeaver 案例 hello Azure 上的不同 DBMS，您可以以不同的方式裝載在 Azure 上 SAP BI 等其他 SAP 工作負載案例。 關於 Azure 原生的虛擬機器上的 SAP NetWeaver 部署文件，請參閱 hello 一節 「 SAP NetWeaver on Azure 虛擬機器 」。 

Azure 有原生大小的 CPU 和記憶體資源 toocover SAP 工作負載會運用 SAP HANA 增長的 Azure 虛擬機器提供。 如需有關本主題的詳細資訊，查閱 hello hello 之下 SAP HANA Azure 虛擬機器上的文件。 」

Azure for SAP HANA hello 唯一性是除了競爭設定 Azure 的唯一優惠。 順序 tooenable 裝載更多的記憶體和 CPU 資源中有關 SAP HANA 的案例，Azure 提供的客戶 hello 使用量嚴苛的 SAP 專用 hello 目的是要執行需要向上 too20 TB （60 TB 向外） 的 SAP HANA 部署裸機的硬體S/4HANA 或其他 SAP HANA 工作負載的記憶體。 在 Azure （大型執行個體） 上的 SAP HANA 此唯一 Azure 方案可讓您 toorun SAP HANA 專用的 hello 裸機硬體與 hello SAP 應用程式層或工作負載中介軟體層裝載在原生 Azure 虛擬機器上。 此解決方案會記載在許多份文件在 hello 區段 」"（大型執行個體） 在 Azure 上 SAP HANA。   

裝載在 Azure 中的 SAP 工作負載案例也可以建立的身分識別整合和單一登入使用 Azure Active Directory toodifferent SAP 元件和 SAP SaaS 需求或 PaaS 提供。 這類的整合和單一登入案例使用 Azure Active Directory (AAD) 與 SAP 實體的清單會描述和 hello > 一節所述"AAD SAP 身分識別整合和單一登入。 」


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a>SAP HANA on Azure (大型執行個體) 上的 SAP HANA

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a>SAP HANA on Azure (大型執行個體) 的概觀與架構
標題： aaaOverview 與 SAP HANA 的架構上 Azure （大型執行個體）

摘要： 這個架構和技術的部署指南 》 提供資訊 toohelp 部署 SAP hello Azure 中的新 Azure （大型執行個體） 上的 SAP HANA。 它不是預期的 toobe SAP 解決方案，但您初始的部署和進行中作業相當實用資訊的完整指南涵蓋特定設定。 它不應該取代 SAP 文件集相關的 SAP HANA toohello 安裝 （或 hello 許多 SAP 支援附註，其中涵蓋 hello 主題）。 它提供的概觀，並提供 hello Azure （大型執行個體） 上安裝 SAP HANA 的其他詳細資料。

更新日期：2017 年 7 月

[這裡可以找到本指南](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a>基礎結構和連線能力 tooSAP HANA Azure （大型執行個體） 上
標題： aaaInfrastructure 和連線 tooSAP HANA Azure （大型執行個體） 上

摘要： hello Azure （大型執行個體） 上的 SAP HANA 購買您與 Microsoft 企業帳戶小組 hello 間完成之後，各種網路設定中需要順序 tooensure 適當連線。  需要有 toobe 下列資訊的 hello 與共用此文件大綱 hello 資訊。 本文將概述哪些資訊具有 toobe 收集而哪些設定指令碼具有 toobe 執行。 

更新日期：2017 年 7 月

[這裡可以找到本指南](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a>在 SAP HANA on Azure (大型執行個體) 中安裝 SAP HANA
標題： aaaInstall Azure （大型執行個體） 上的 SAP HANA 上的 SAP HANA

摘要： 本文件概述 hello Azure 大型執行個體上安裝 SAP HANA 的安裝程序。 

更新日期：2017 年 7 月

[這裡可以找到本指南](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a>SAP HANA on Azure (大型執行個體) 的高可用性和災害復原
標題： aaaHigh 可用性和災害復原的 SAP HANA Azure （大型執行個體） 上

摘要︰高可用性 (HA) 和災害復原 (DR) 對於執行關鍵任務 SAP HANA on Azure (大型執行個體) 伺服器是非常重要的層面。 它的匯入 toowork 與 SAP、 您系統整合者，及/或 Microsoft tooproperly 架構設計人員和為您實作 hello 右邊 HA/DR 策略。 您必須考量復原點目標 (RPO) 和復原時間目標 (RTO)，特定 tooyour 環境等重要考量。  本文件說明啟用您慣用層級 HA 和 DR 的選項。

更新日期：2016 年 12 月

[可以在這裡找到這份文件](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a>針對 SAP HANA on Azure (大型執行個體) 進行疑難排解和監視
標題： aaaTroubleshooting 與監視的 SAP HANA Azure （大型執行個體） 上

摘要︰本指南提供建立監視 SAP HANA on Azure 環境的有用資訊，以及其他疑難排解資訊。 

更新日期：2016 年 12 月

[可以在這裡找到這份文件](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a>Azure 虛擬機器上的 SAP HANA

### <a name="getting-started-with-sap-hana-on-azure"></a>在 Azure 上開始使用 SAP HANA
標題： Azure Vm 上手動安裝的 SAP HANA aaaQuickstart 指南

摘要： 本快速入門指南可協助單一執行個體 SAP HANA 系統在 Azure Vm 上手動安裝的 SAP NetWeaver 7.5 和 SAP HANA SP12 tooset。 hello 指南會假設 hello 讀者已熟悉 Azure IaaS 像 toodeploy 虛擬機器或虛擬網路透過 hello Azure 入口網站或 Powershell/CLI 包括 hello 選項 toouse json 範本的基本概念。 此外應該 hello 讀者已熟悉 SAP HANA、 SAP NetWeaver 和如何 tooinstall 它在內部。

更新日期：2017 年 6 月

[這裡可以找到本指南](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a>Azure 上的 S/4HANA SAP CAL 部署
標題： aaaDeploy SAP S/4HANA 或 BW/4HANA 在 Azure 上

摘要： 本指南可協助 toodemonstrate hello SAP S/4HANA 使用 SAP 雲端應用裝置程式庫在 Azure 上部署。 SAP 雲端應用裝置程式庫是可讓 toodeploy SAP 應用程式在 Azure 上的 sap 的服務。 hello 指南說明逐步解說 hello 部署。

更新日期：2017 年 6 月

[這裡可以找到本指南](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a>Azure 虛擬機器中 SAP HANA 的高可用性
標題： aaaHigh 可用性的 SAP HANA Azure 虛擬機器上

摘要： 本指南會引導您透過 hello 高可用性組態的 hello SUSE 12 OS 和 SAP HANA tooaccommodate HANA 系統複寫具有自動容錯移轉。 hello 指南是針對 SUSE 和 Azure 虛擬機器。 hello 指南不適用尚未 Red Hat 或裸機或私人雲端或其他非 Azure 公用雲端部署。

更新日期：2017 年 6 月

[這裡可以找到本指南](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a>Azure VM 上的 SAP HANA 備份概觀
標題： aaaBackup 指南的 SAP HANA Azure 虛擬機器上

摘要：此指南提供關於在 Azure 虛擬機器上執行 SAP HANA 之備份可能性的基本資訊。

更新日期：2017 年 3 月

[這裡可以找到本指南](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a>Azure VM 上的 SAP HANA 檔案層級備份
標題： aaaSAP HANA 備份為基礎儲存快照集

摘要：此指南提供在 Azure 虛擬機器上執行 SAP HANA 時，於 Azure VM 上使用以快照集為基礎的備份相關資訊。

更新日期：2017 年 3 月

[這裡可以找到本指南](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a>在 Azure VM 上以 SAP HANA 快照集為基礎的備份
標題： aaaSAP HANA 檔案層級上的 Azure 備份

摘要：此指南提供在 Azure 虛擬機器上執行 SAP HANA 時，使用 SAP HANA 檔案層級備份的相關資訊

更新日期：2017 年 3 月

[這裡可以找到本指南](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a>在 Azure 虛擬機器上開發的 SAP NetWeaver

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a>透過 SAP CAL on Azure，在 Windows 和 SQL Server 上部署 SAP IDES 系統
標題： aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux Vm 

摘要： 本文件說明 SAP IDE 系統根據 Windows 和 SQL Server on Azure 中使用 SAP 雲端應用裝置程式庫的 hello 部署。 SAP 雲端應用裝置程式庫是可讓在 Azure 的 SAP 產品的 hello 部署 SAP 服務。 此文件會經歷 IDE SAP 系統的 hello 部署逐步解說。 hello IDE 系統只是範例數個其他數十個應用程式，可部署到 Microsoft Azure 上 SAP 雲端應用裝置。

更新日期：2017 年 6 月

[這裡可以找到本指南](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a>Azure 之 SUSE Linux 上的 NetWeaver 快速入門指南
標題： aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux Vm 

摘要： 本文說明各種項目 tooconsider 如果您在 Microsoft Azure SUSE Linux 虛擬機器 (Vm) 上執行的 SAP NetWeaver。 在 Azure 的 SUSE Linux VM 上已正式支援 SAP NetWeaver。 如需有關 Linux 版本、SAP 核心版本的所有詳細資料及其他詳細資料，請參閱 SAP 附註 1928533＜Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型＞。

更新時間：2016 年 9 月

[這裡可以找到本指南](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>規劃和實作
標題： aaaAzure 虛擬機器規劃和實作的 SAP NetWeaver

摘要： 本文件是與 hello 指南 toostart 如果您對於 Azure 虛擬機器中執行 SAP NetWeaver 的想法。 此規劃和實作指南可協助您評估現有或計劃 SAP NetWeaver 架構系統可以為已部署的 tooan Azure 虛擬機器環境。 它涵蓋了多個 SAP NetWeaver 部署案例中，並包含屬於特定 tooAzure SAP 組態。 hello 紙張列出並描述上的所有 hello 必要的設定資訊必須 hello SAP/Azure 端 toorun 混合式 SAP landscape。 您可以採取 tooensure 高可用性的 SAP NetWeaver 架構系統上 IaaS 也涵蓋。

更新日期：2017 年 6 月

[這裡可以找到本指南][planning-guide]

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a>在 Azure VM 中 SAP NetWeaver 的高可用性組態
標題： aaaAzure 虛擬機器的 SAP NetWeaver 的高可用性

摘要： 在本文件中，我們將討論 hello，您可以採取的步驟 toodeploy 高可用性的 SAP 系統在 Azure 中使用 hello Azure Resource Manager 部署模型。 我們會引導您完成這些主要工作。 我們可以在 hello 文件，描述如何單一---失敗點元件像進階商業應用程式開發 (ABAP) SAP 中央服務 (ASCS) / SAP 中央服務 (SCS) 和資料庫管理系統 (DBMS) 及重複元件，例如 SAP應用程式伺服器將 toobe Azure Vm 中執行時受到保護。 此文件中會示範及顯示在 Azure 的 Windows Server 容錯移轉叢集的叢集中安裝及設定高可用性 SAP 系統的逐步說明範例。

更新日期：2017 年 6 月

[這裡可以找到本指南](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a>在 Azure VM 中實現 SAP NetWeaver 的多 SID 部署
標題： aaaCreate SAP NetWeaver 多重 SID 組態 

摘要： 本文件是加法 toohello 文件的 Azure Vm 上的 SAP NetWeaver 的高可用性。 Toonew 引進在 2016 年 9 月的 Azure 中的功能，因為它是可能 toodeploy 成對的 Azure Vm 中的多個 SAP NetWeaver ASCS/SCS 執行個體。 使用這類設定時，您可以減少 hello Vm 需要 toodeploy toorealize 高可用性的 SAP NetWeaver 組態數目。 hello 指南將說明這類多重 SID 設定的 hello 安裝程式。

更新日期：2016 年 12 月

[這裡可以找到本指南](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>在 Azure VM 中部署 SAP NetWeaver
標題： aaaAzure SAP NetWeaver 的虛擬機器部署

摘要： 本文件提供部署在 Azure 中的 SAP NetWeaver 軟體 toovirtual 機器程序指引。 這份文件將重點放在三個特定部署案例，強調啟用 hello Azure Monitoring Extensions for SAP，包括疑難排解 hello Azure Monitoring Extensions for SAP 的建議。 本文件假設您已閱讀 hello 規劃和實作指南 》。

更新日期：2017 年 6 月

[這裡可以找到本指南][deployment-guide]

### <a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS 部署指南
標題： aaaAzure SAP NetWeaver 的虛擬機器的 DBMS 部署

摘要： 本文件涵蓋應該與 SAP 一起執行的 hello DBMS 系統的規劃和實作考量。 在 hello 第一個部分中，一般考量列出，並顯示上。 hello hello 紙張的下列部分與在 Azure 中 SAP 所支援的不同 dbms toodeployments。 所提出的不同 DBMS 分別是 SQL Server、SAP ASE 和 Oracle。 在這些特定的組件、 討論有 tooaccount 時，您是 Azure 上執行 SAP 系統中與這些 DBMS 一起考量。 主旨，例如的 hello hello 與 SAP 應用程式的使用量會在 Azure 上的不同 DBMS 所支援的備份和高可用性方法。

更新日期：2017 年 6 月

[這裡可以找到本指南][dbms-guide]

### <a name="using-azure-site-recovery-for-sap-workload"></a>針對 SAP 工作負載使用 Azure Site Recovery
標題： aaaSAP NetWeaver： 建置與 Azure Site Recovery 的災害復原方案 

摘要： 本文件說明如何使用 Azure Site Recovery 服務的 hello 目的是要處理的災害復原案例的 hello 方式。 案例中使用 Azure 作為災害復原位置，用於 Azure Site Recovery 服務之內部部屬 SAP 環境中。 另一個 hello 文件中所述的案例是 hello Aure Azure (A2A) 嚴重損壞修復案例及如何管理與 Azure Site Recovery。  

更新日期：2017 年 8 月

[這裡可以找到本指南](http://aka.ms/asr-sap)
