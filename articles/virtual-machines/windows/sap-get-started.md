---
title: "開始在 Azure 中的 Windows Vm 上的 SAP aaaGetting |Microsoft 文件"
description: "了解在 Microsoft Azure 中的虛擬機器 (VM) 上執行的 SAP 解決方案"
services: virtual-machines-windows
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e714c47-add3-44c5-a6c8-9d26472ddcc4
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 678770955ecc78bf1d39c193c833ae4e11912fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-azure-windows-virtual-machines-vms"></a><span data-ttu-id="42678-103">在 Azure Windows 虛擬機器 (VM) 上使用 SAP</span><span class="sxs-lookup"><span data-stu-id="42678-103">Using SAP on Azure Windows Virtual Machines (VMs)</span></span>
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
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription

[dbms-guide]:../virtual-machines-windows-sap-dbms-guide.md 
[dbms-guide-2.1]:../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

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

[getting-started]:virtual-machines-windows-../linux/classic/sap-get-started.md
[getting-started-dbms]:virtual-machines-windows-../linux/classic/sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:virtual-machines-windows-../linux/classic/sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:virtual-machines-windows-../linux/classic/sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md
[getting-started-windows-classic-dbms]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
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
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md 
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

<span data-ttu-id="42678-104">藉由選擇您的 SAP 準備雲端夥伴身分登入 Microsoft Azure，您就會無法 tooreliably 執行您的任務關鍵性工作 scaaleable 規定上的 SAP 負載和企業證明平台。</span><span class="sxs-lookup"><span data-stu-id="42678-104">By choosing Microsoft Azure as your SAP ready cloud partner, you will be able tooreliably run your mission critical SAP workloads on a scaaleable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="42678-105">取得彈性，、 hello 延展性，並節省 Azure 的成本。</span><span class="sxs-lookup"><span data-stu-id="42678-105">Get hello scaleability, flexability, and cost savings of Azure.</span></span> <span data-ttu-id="42678-106">使用 Microsoft SAP 之間 hello 展開合作關係，您可以跨 azure-開發/測試和實際執行案例中執行 SAP 應用程式，並受到完整支援。</span><span class="sxs-lookup"><span data-stu-id="42678-106">With hello expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in azure - and be fully supported.</span></span> <span data-ttu-id="42678-107">從 SAP NetWeaver tooSAP S4/HANA、 Linux tooWindows、 SAP HANA tooSQL，我們已涵蓋您。</span><span class="sxs-lookup"><span data-stu-id="42678-107">From SAP NetWeaver tooSAP S4/HANA, Linux tooWindows, SAP HANA tooSQL, we have you covered.</span></span> 

<span data-ttu-id="42678-108">透過 Microsoft Azure 虛擬機器服務，以及 Azure 大型執行個體上的 SAP HANA，Microsoft 提供了完整的「基礎結構即服務」(IaaS) 平台。</span><span class="sxs-lookup"><span data-stu-id="42678-108">With Microsoft Azure virtual machine services, and SAP HANA on Azure large instances, Microsoft offers a comprehensive Infrastructure As A Service (IaaS) platform.</span></span> <span data-ttu-id="42678-109">由於 Azure 上支援廣泛的 SAP 解決方案，因此這份「入門文件」將作為我們目前 SAP 文件集的「目錄」。</span><span class="sxs-lookup"><span data-stu-id="42678-109">Because a wide range of SAP solutions are supported on Azure, this "getting started document will serve as a Table of Contents for our current set of SAP documents.</span></span> <span data-ttu-id="42678-110">多個項目加入 tooour 文件庫-您將會看到它們在此處加入。</span><span class="sxs-lookup"><span data-stu-id="42678-110">As more titles get added tooour document library - you will see them added here.</span></span> 

## <a name="sap-hana-certifications-on-microsoft-azure"></a><span data-ttu-id="42678-111">Microsoft Azure 上的 SAP HANA 認證</span><span class="sxs-lookup"><span data-stu-id="42678-111">SAP HANA Certifications on Microsoft Azure</span></span>
| <span data-ttu-id="42678-112">SAP 產品</span><span class="sxs-lookup"><span data-stu-id="42678-112">SAP Product</span></span> | <span data-ttu-id="42678-113">支援的 OS</span><span class="sxs-lookup"><span data-stu-id="42678-113">Supported OS</span></span> | <span data-ttu-id="42678-114">Azure 供應項目</span><span class="sxs-lookup"><span data-stu-id="42678-114">Azure Offerings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42678-115">SAP HANA Developer Edition (包括 hello HANA 用戶端軟體組成 SQLODBC、 僅限 ODBO-Windows ODBC，JDBC 驅動程式，HANA studio 和 HANA 資料庫)</span><span class="sxs-lookup"><span data-stu-id="42678-115">SAP HANA Developer Edition (including hello HANA client software comprised of SQLODBC, ODBO-Windows only, ODBC, JDBC drivers, HANA studio, and HANA database)</span></span> |<span data-ttu-id="42678-116">Red Hat Enterprise Linux、SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="42678-116">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="42678-117">A7、A8</span><span class="sxs-lookup"><span data-stu-id="42678-117">A7, A8</span></span> |
| <span data-ttu-id="42678-118">MHANA One</span><span class="sxs-lookup"><span data-stu-id="42678-118">MHANA One</span></span> |<span data-ttu-id="42678-119">Red Hat Enterprise Linux、SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="42678-119">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="42678-120">DS14_v2 (正式運作後)</span><span class="sxs-lookup"><span data-stu-id="42678-120">DS14_v2 (upon general availability)</span></span> |
| <span data-ttu-id="42678-121">SAP S/4HANA</span><span class="sxs-lookup"><span data-stu-id="42678-121">SAP S/4HANA</span></span> |<span data-ttu-id="42678-122">Red Hat Enterprise Linux、SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="42678-122">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="42678-123">GS5 管制性運作、SAP HANA on Azure (大型執行個體)</span><span class="sxs-lookup"><span data-stu-id="42678-123">Controlled Availability for GS5, SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="42678-124">Suite on HANA (OLTP)</span><span class="sxs-lookup"><span data-stu-id="42678-124">Suite on HANA, OLTP</span></span> |<span data-ttu-id="42678-125">Red Hat Enterprise Linux、SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="42678-125">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="42678-126">SAP HANA on Azure (大型執行個體)</span><span class="sxs-lookup"><span data-stu-id="42678-126">SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="42678-127">HANA Enterprise for BW (OLAP)</span><span class="sxs-lookup"><span data-stu-id="42678-127">HANA Enterprise for BW, OLAP</span></span> |<span data-ttu-id="42678-128">Red Hat Enterprise Linux、SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="42678-128">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="42678-129">適用於單一節點部署的 GS5、SAP HANA on Azure (大型執行個體)</span><span class="sxs-lookup"><span data-stu-id="42678-129">GS5 for single node deployments, SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="42678-130">SAP BW/4HANA</span><span class="sxs-lookup"><span data-stu-id="42678-130">SAP BW/4HANA</span></span> |<span data-ttu-id="42678-131">Red Hat Enterprise Linux、SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="42678-131">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="42678-132">適用於單一節點部署的 GS5、SAP HANA on Azure (大型執行個體)</span><span class="sxs-lookup"><span data-stu-id="42678-132">GS5 for single node deployments, SAP HANA on Azure (Large instances)</span></span> |

## <a name="sap-netweaver-certifications"></a><span data-ttu-id="42678-133">SAP NetWeaver 認證</span><span class="sxs-lookup"><span data-stu-id="42678-133">SAP NetWeaver Certifications</span></span>
<span data-ttu-id="42678-134">Microsoft Azure 認證 hello 遵循 SAP 產品，從 Microsoft 和 SAP 的完整支援。</span><span class="sxs-lookup"><span data-stu-id="42678-134">Microsoft Azure is certified for hello following SAP products, with full support from Microsoft and SAP.</span></span>

| <span data-ttu-id="42678-135">SAP 產品</span><span class="sxs-lookup"><span data-stu-id="42678-135">SAP Product</span></span> | <span data-ttu-id="42678-136">客體作業系統</span><span class="sxs-lookup"><span data-stu-id="42678-136">Guest OS</span></span> | <span data-ttu-id="42678-137">RDBMS</span><span class="sxs-lookup"><span data-stu-id="42678-137">RDBMS</span></span> | <span data-ttu-id="42678-138">虛擬機器類型</span><span class="sxs-lookup"><span data-stu-id="42678-138">Virtual Machine Types</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="42678-139">SAP Business Suite 軟體</span><span class="sxs-lookup"><span data-stu-id="42678-139">SAP Business Suite Software</span></span> |<span data-ttu-id="42678-140">Windows、SUSE Linux Enterprise、Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="42678-140">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="42678-141">SQL Server、Oracle (僅限 Windows)、DB2、SAP ASE</span><span class="sxs-lookup"><span data-stu-id="42678-141">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="42678-142">A5 tooA11、 D11 tooD14、 DS11 tooDS14、 GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="42678-142">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |
| <span data-ttu-id="42678-143">SAP Business All-in-One</span><span class="sxs-lookup"><span data-stu-id="42678-143">SAP Business All-in-One</span></span> |<span data-ttu-id="42678-144">Windows、SUSE Linux Enterprise、Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="42678-144">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="42678-145">SQL Server、Oracle (僅限 Windows)、DB2、SAP ASE</span><span class="sxs-lookup"><span data-stu-id="42678-145">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="42678-146">A5 tooA11、 D11 tooD14、 DS11 tooDS14、 GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="42678-146">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |
| <span data-ttu-id="42678-147">SAP BusinessObjects BI</span><span class="sxs-lookup"><span data-stu-id="42678-147">SAP BusinessObjects BI</span></span> |<span data-ttu-id="42678-148">Windows</span><span class="sxs-lookup"><span data-stu-id="42678-148">Windows</span></span> |<span data-ttu-id="42678-149">N/A</span><span class="sxs-lookup"><span data-stu-id="42678-149">N/A</span></span> |<span data-ttu-id="42678-150">A5 tooA11、 D11 tooD14、 DS11 tooDS14、 GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="42678-150">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |
| <span data-ttu-id="42678-151">SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="42678-151">SAP NetWeaver</span></span> |<span data-ttu-id="42678-152">Windows、SUSE Linux Enterprise、Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="42678-152">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="42678-153">SQL Server、Oracle (僅限 Windows)、DB2、SAP ASE</span><span class="sxs-lookup"><span data-stu-id="42678-153">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="42678-154">A5 tooA11、 D11 tooD14、 DS11 tooDS14、 GS1 tooGS5</span><span class="sxs-lookup"><span data-stu-id="42678-154">A5 tooA11, D11 tooD14, DS11 tooDS14, GS1 tooGS5</span></span> |

## <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="42678-155">在 Azure 上開始使用 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="42678-155">Getting Started with SAP HANA on Azure</span></span>
<span data-ttu-id="42678-156">標題： Azure Vm 上手動安裝的 SAP HANA aaaQuickstart 指南</span><span class="sxs-lookup"><span data-stu-id="42678-156">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="42678-157">摘要： 本快速入門指南將協助單一執行個體 SAP HANA 原型/示範系統在 Azure Vm 上手動安裝的 SAP NetWeaver 7.5 和 SAP HANA SP12 tooset。</span><span class="sxs-lookup"><span data-stu-id="42678-157">Summary: This quickstart guide will help tooset up a single-instance SAP HANA prototype/demo system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="42678-158">hello 指南會假設 hello 讀者已熟悉 Azure IaaS 像 toodeploy 虛擬機器或虛擬網路透過 hello Azure 入口網站或 Powershell/CLI 包括 hello 選項 toouse json 範本的基本概念。</span><span class="sxs-lookup"><span data-stu-id="42678-158">hello guide presumes that hello reader is familiar with Azure IaaS basics like how toodeploy virtual machines or virtual networks either via hello Azure portal or Powershell/CLI including hello option toouse json templates.</span></span> <span data-ttu-id="42678-159">此外應該 hello 讀者已熟悉 SAP HANA、 SAP NetWeaver 和如何 tooinstall 它在內部。</span><span class="sxs-lookup"><span data-stu-id="42678-159">Furthermore it's expected that hello reader is familiar with SAP HANA, SAP NetWeaver and how tooinstall it on-premises.</span></span>

<span data-ttu-id="42678-160">更新時間：2016 年 9 月</span><span class="sxs-lookup"><span data-stu-id="42678-160">Updated: September 2016</span></span>

[<span data-ttu-id="42678-161">這裡可以找到本指南</span><span class="sxs-lookup"><span data-stu-id="42678-161">This guide can be found here</span></span>](../virtual-machines-linux-sap-hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="42678-162">Azure 之 SUSE Linux 上的 NetWeaver 快速入門指南</span><span class="sxs-lookup"><span data-stu-id="42678-162">Quickstart Guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="42678-163">標題： aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux Vm</span><span class="sxs-lookup"><span data-stu-id="42678-163">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="42678-164">摘要： 本文說明各種項目 tooconsider 如果您在 Microsoft Azure SUSE Linux 虛擬機器 (Vm) 上執行的 SAP NetWeaver。</span><span class="sxs-lookup"><span data-stu-id="42678-164">Summary: This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="42678-165">自 2016 年 5 月 19 日起，在 Azure 的 SUSE Linux VM 上已正式支援 SAP NetWeaver。</span><span class="sxs-lookup"><span data-stu-id="42678-165">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="42678-166">如需有關 Linux 版本、SAP 核心版本等等的所有詳細資料，請參閱 SAP 附註 1928533＜Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型＞。</span><span class="sxs-lookup"><span data-stu-id="42678-166">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="42678-167">更新時間：2016 年 9 月</span><span class="sxs-lookup"><span data-stu-id="42678-167">Updated: September 2016</span></span>

[<span data-ttu-id="42678-168">這裡可以找到本指南</span><span class="sxs-lookup"><span data-stu-id="42678-168">This guide can be found here</span></span>](../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deploying-sap-ides-ehp7-sp3-for-sap-erp-60-on-microsoft-azure"></a><span data-ttu-id="42678-169">在 Microsoft Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3</span><span class="sxs-lookup"><span data-stu-id="42678-169">Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure</span></span>
<span data-ttu-id="42678-170">標題： Azure Vm 上手動安裝的 SAP HANA aaaQuickstart 指南</span><span class="sxs-lookup"><span data-stu-id="42678-170">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="42678-171">摘要： 本文說明如何 toodeploy SAP 與 SQL Server 和 Windows 作業系統執行 Microsoft Azure 上 SAP 雲端應用裝置程式庫 3.0 透過 IDE。</span><span class="sxs-lookup"><span data-stu-id="42678-171">Summary: This article describes how toodeploy SAP IDES running with SQL Server and Windows OS on Microsoft Azure via SAP Cloud Appliance Library 3.0.</span></span> 

<span data-ttu-id="42678-172">更新時間：2016 年 9 月</span><span class="sxs-lookup"><span data-stu-id="42678-172">Updated: September 2016</span></span>

[<span data-ttu-id="42678-173">這裡可以找到本指南</span><span class="sxs-lookup"><span data-stu-id="42678-173">This guide can be found here</span></span>](sap-cal-ides-erp6-ehp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <span data-ttu-id="42678-174"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>規劃和實作</span><span class="sxs-lookup"><span data-stu-id="42678-174"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and Implementation</span></span>
<span data-ttu-id="42678-175">標題： aaaSAP NetWeaver Azure 虛擬機器 (Vm) 上 – 計劃與實作指南</span><span class="sxs-lookup"><span data-stu-id="42678-175">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – Planning and Implementation Guide</span></span>

<span data-ttu-id="42678-176">摘要： 這是與 hello 紙張 toostart，如果您對於 Azure 虛擬機器中執行 SAP NetWeaver 的想法。</span><span class="sxs-lookup"><span data-stu-id="42678-176">Summary: This is hello paper toostart with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="42678-177">本規劃和實作指南將協助您評估現有或已規劃的 SAP NetWeaver 架構系統可以是已部署的 tooan Azure 虛擬機器環境。</span><span class="sxs-lookup"><span data-stu-id="42678-177">This planning and implementation guide will help you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed tooan Azure Virtual Machines environment.</span></span> <span data-ttu-id="42678-178">它涵蓋了多個 SAP NetWeaver 部署案例中，並包含屬於特定 tooAzure SAP 組態。</span><span class="sxs-lookup"><span data-stu-id="42678-178">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific tooAzure.</span></span> <span data-ttu-id="42678-179">hello 紙張列出並描述上的所有 hello 必要的設定資訊必須 hello SAP/Azure 端 toorun 混合式 SAP landscape。</span><span class="sxs-lookup"><span data-stu-id="42678-179">hello paper lists and describes all hello necessary configuration information you’ll need on hello SAP/Azure side toorun a hybrid SAP landscape.</span></span> <span data-ttu-id="42678-180">您可以採取 tooensure 高可用性的 SAP NetWeaver 架構系統上 IaaS 也涵蓋。</span><span class="sxs-lookup"><span data-stu-id="42678-180">Measures you can take tooensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="42678-181">更新日期︰2016 年 8 月</span><span class="sxs-lookup"><span data-stu-id="42678-181">Updated: August 2016</span></span>

<span data-ttu-id="42678-182">[這裡可以找到本指南][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="42678-182">[This guide can be found here][planning-guide]</span></span>

## <span data-ttu-id="42678-183"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>部署</span><span class="sxs-lookup"><span data-stu-id="42678-183"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment</span></span>
<span data-ttu-id="42678-184">標題： aaaSAP NetWeaver Azure 虛擬機器 (Vm) 上 – 部署指南</span><span class="sxs-lookup"><span data-stu-id="42678-184">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – Deployment Guide</span></span>

<span data-ttu-id="42678-185">摘要： 本文件提供部署在 Azure 中的 SAP NetWeaver 軟體 toovirtual 機器程序指引。</span><span class="sxs-lookup"><span data-stu-id="42678-185">Summary: This document provides procedural guidance for deploying SAP NetWeaver software toovirtual machines in Azure.</span></span> <span data-ttu-id="42678-186">這份文件將重點放在三個特定部署案例，強調啟用 hello Azure Monitoring Extensions for SAP，包括疑難排解 hello Azure Monitoring Extensions for SAP 的建議。</span><span class="sxs-lookup"><span data-stu-id="42678-186">This paper focuses on three specific deployment scenarios, with an emphasis on enabling hello Azure Monitoring Extensions for SAP, including troubleshooting recommendations for hello Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="42678-187">本文件假設您已閱讀 hello 規劃和實作指南 》。</span><span class="sxs-lookup"><span data-stu-id="42678-187">This paper assumes that you’ve read hello planning and implementation guide.</span></span>

<span data-ttu-id="42678-188">更新日期：2016 年 12 月</span><span class="sxs-lookup"><span data-stu-id="42678-188">Updated: December 2016</span></span>

<span data-ttu-id="42678-189">[這裡可以找到本指南][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="42678-189">[This guide can be found here][deployment-guide]</span></span>

## <span data-ttu-id="42678-190"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS 部署指南</span><span class="sxs-lookup"><span data-stu-id="42678-190"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS Deployment Guide</span></span>
<span data-ttu-id="42678-191">標題： aaaSAP NetWeaver Azure 虛擬機器 (Vm) 上 – 的 DBMS 部署指南</span><span class="sxs-lookup"><span data-stu-id="42678-191">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – DBMS Deployment Guide</span></span>

<span data-ttu-id="42678-192">摘要： 本文件涵蓋應該與 SAP 一起執行的 hello DBMS 系統的規劃和實作考量。</span><span class="sxs-lookup"><span data-stu-id="42678-192">Summary: This paper covers planning and implementation considerations for hello DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="42678-193">在 hello 第一個部分中，一般考量列出，並顯示上。</span><span class="sxs-lookup"><span data-stu-id="42678-193">In hello first part, general considerations are listed and presented.</span></span> <span data-ttu-id="42678-194">hello hello 紙張的下列部分與在 Azure 中 SAP 所支援的不同 dbms toodeployments。</span><span class="sxs-lookup"><span data-stu-id="42678-194">hello following parts of hello paper relate toodeployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="42678-195">所提出的不同 DBMS 分別是 SQL Server、SAP ASE 和 Oracle。</span><span class="sxs-lookup"><span data-stu-id="42678-195">Different DBMS presented are SQL Server, SAP ASE and Oracle.</span></span> <span data-ttu-id="42678-196">這些特定的組件中討論有 tooaccount 時，您是 Azure 上執行 SAP 系統中與這些 DBMS 一起考量。</span><span class="sxs-lookup"><span data-stu-id="42678-196">In those specific parts considerations you have tooaccount for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="42678-197">主旨，例如的 hello hello 與 SAP 應用程式的使用量會在 Azure 上的不同 DBMS 所支援的備份和高可用性方法。</span><span class="sxs-lookup"><span data-stu-id="42678-197">Subjects like backup and high availability methods that are supported by hello different DBMS on Azure are presented for hello usage with SAP applications.</span></span>

<span data-ttu-id="42678-198">更新日期︰2016 年 8 月</span><span class="sxs-lookup"><span data-stu-id="42678-198">Updated: August 2016</span></span>

<span data-ttu-id="42678-199">[這裡可以找到本指南][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="42678-199">[This guide can be found here][dbms-guide]</span></span>

## <span data-ttu-id="42678-200"><a name="63dab028-2c4f-4636-8f99-90bbb264eaba"></a>高可用性部署指南</span><span class="sxs-lookup"><span data-stu-id="42678-200"><a name="63dab028-2c4f-4636-8f99-90bbb264eaba"></a>High Availability Deployment Guide</span></span>
<span data-ttu-id="42678-201">標題： aaaSAP NetWeaver Azure 虛擬機器 (Vm) 上-高可用性部署指南</span><span class="sxs-lookup"><span data-stu-id="42678-201">title: aaaSAP NetWeaver on Azure Virtual Machines (VMs) – High Availability Deployment Guide</span></span>

<span data-ttu-id="42678-202">摘要： 本文件說明如何保護 SAP 單點失敗的元件，例如 SAP ASCS/SCS hello 和 DBMS，在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="42678-202">Summary: This document describes how SAP single point of failure components like hello SAP ASCS/SCS and DBMS can be protected in Azure.</span></span> <span data-ttu-id="42678-203">元件的 hello SAP ASCS/SCS、 DBMS 和應用程式伺服器是不可或缺的 SAP NetWeaver 系統，例如 SAP NetWeaver ABAP、 SAP NetWeaver ABAP + Java 系統，SAP NetWeaver Java hello 功能。</span><span class="sxs-lookup"><span data-stu-id="42678-203">Components of hello SAP ASCS/SCS, DBMS and application servers are essential for hello functionality of SAP NetWeaver systems, e.g. SAP NetWeaver ABAP, SAP NetWeaver Java, SAP NetWeaver ABAP+Java systems.</span></span> <span data-ttu-id="42678-204">因此，高可用性功能需求 toobe 置於放置 toomake 確定這些元件可以承受伺服器或 VM 的失敗，因為透過裸機和 HYPER-V 環境的 Windows 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="42678-204">Therefore, high-availability functionality needs toobe put in place toomake sure that those components can sustain a failure of a server or a VM as done with Windows Cluster configurations for bare-metal and Hyper-V environments.</span></span>

<span data-ttu-id="42678-205">更新日期：2016 年 12 月</span><span class="sxs-lookup"><span data-stu-id="42678-205">Updated: December 2016</span></span>

<span data-ttu-id="42678-206">[這裡可以找到本指南][ha-guide]</span><span class="sxs-lookup"><span data-stu-id="42678-206">[This guide can be found here][ha-guide]</span></span>

