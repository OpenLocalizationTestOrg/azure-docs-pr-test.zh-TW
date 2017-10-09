---
title: "虛擬機器的高可用性的 SAP NetWeaver aaaAzure |Microsoft 文件"
description: "Azure 虛擬機器上的 SAP NetWeaver 高可用性指南"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="a12ef-103">Azure VM 上的 SAP NetWeaver 高可用性</span><span class="sxs-lookup"><span data-stu-id="a12ef-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

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

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
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
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="a12ef-109">Azure 虛擬機器是 hello 解決方案需要計算、 儲存和網路資源的最小時間，而不冗長的採購循環的組織。</span><span class="sxs-lookup"><span data-stu-id="a12ef-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="a12ef-110">您可以使用 Azure 虛擬機器 toodeploy 傳統應用程式為基礎的 SAP NetWeaver 的 ABAP、 Java 和 ABAP + Java 堆疊等。</span><span class="sxs-lookup"><span data-stu-id="a12ef-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="a12ef-111">擴充的可靠性與可用性，無須其他內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="a12ef-112">「Azure 虛擬機器」支援跨單位連線能力，貴公司可將「Azure 虛擬機器」整合到其內部部署網域、私人雲端，以及 SAP 系統環境中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="a12ef-113">在本文中，我們將討論 hello，您可以採取的步驟 toodeploy 高可用性的 SAP 系統在 Azure 中使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="a12ef-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="a12ef-114">我們會引導您完成這些主要工作：</span><span class="sxs-lookup"><span data-stu-id="a12ef-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="a12ef-115">尋找 hello 右 SAP 附註和安裝指南，列在 hello[資源][ sap-ha-guide-2] > 一節。</span><span class="sxs-lookup"><span data-stu-id="a12ef-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="a12ef-116">本文補充 SAP 安裝文件集，SAP 附註，也就是 hello 主要資源，幫助您安裝和部署在特定平台上的 SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="a12ef-117">了解 hello hello Azure Resource Manager 部署模型與 hello Azure 傳統部署模型之間的差異。</span><span class="sxs-lookup"><span data-stu-id="a12ef-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="a12ef-118">瞭解 Windows Server 容錯移轉叢集的仲裁模式，因此您可以選取最適合您的 Azure 部署的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="a12ef-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="a12ef-119">了解 Azure 服務中的「Windows Server 容錯移轉叢集」共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="a12ef-120">了解如何 toohelp 保護單一---失敗點元件類似進階商業應用程式開發 (ABAP) SAP 中央服務 (ASCS) / SAP 中央服務 (SCS) 和資料庫管理系統 (DBMS) 及重複元件，例如 SAP應用程式伺服器，在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="a12ef-121">藉由使用 Azure Resource Manager，遵循在 Windows Server 容錯移轉叢集的叢集中安裝及設定高可用性 SAP 系統的逐步說明範例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="a12ef-122">深入了解額外的步驟需要的 toouse Windows Server 容錯移轉叢集在 Azure 中，但這不需要在內部部署部署中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="a12ef-123">toosimplify 部署和設定，在本文中，我們使用 hello SAP 三層式高可用性資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="a12ef-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="a12ef-124">hello 範本來自動化部署所需的高可用性的 SAP 系統的 hello 整個基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a12ef-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="a12ef-125">hello 基礎結構也支援 SAP 系統的 SAP 應用程式的效能標準 (SAP) 的大小。</span><span class="sxs-lookup"><span data-stu-id="a12ef-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="a12ef-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> 必要條件</span><span class="sxs-lookup"><span data-stu-id="a12ef-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="a12ef-127">開始之前，請確定您符合 hello 必要條件 hello 下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="a12ef-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="a12ef-128">此外，請確定 toocheck hello 中列出的所有資源[資源][ sap-ha-guide-2] > 一節。</span><span class="sxs-lookup"><span data-stu-id="a12ef-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="a12ef-129">在本文中，我們針對[三層式 SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/) 使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="a12ef-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="a12ef-130">如需範本的實用概觀，請參閱 [SAP Azure Resource Manager 範本](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="a12ef-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> 資源</span><span class="sxs-lookup"><span data-stu-id="a12ef-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="a12ef-132">這些文章涵蓋 Azure 中的 SAP 部署：</span><span class="sxs-lookup"><span data-stu-id="a12ef-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="a12ef-133">[SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="a12ef-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="a12ef-134">[SAP NetWeaver 的 Azure 虛擬機器部署][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="a12ef-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="a12ef-135">[SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="a12ef-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="a12ef-136">[SAP NetWeaver 的 Azure 虛擬機器高可用性 (本指南)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="a12ef-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-137">可能的話，我們提供連結 toohello 參考 SAP 安裝指南 (請參閱 hello [SAP 安裝指南][sap-installation-guides])。</span><span class="sxs-lookup"><span data-stu-id="a12ef-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="a12ef-138">必要條件和 hello 安裝程序，它的建議 tooread hello SAP NetWeaver 安裝指南仔細的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a12ef-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="a12ef-139">本文僅涵蓋可與 Azure 虛擬機器搭配使用之 SAP NetWeaver 架構系統的特定工作。</span><span class="sxs-lookup"><span data-stu-id="a12ef-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="a12ef-140">這些 SAP 附註是在 Azure 中 SAP 相關的 toohello 主題：</span><span class="sxs-lookup"><span data-stu-id="a12ef-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="a12ef-141">附註編號</span><span class="sxs-lookup"><span data-stu-id="a12ef-141">Note number</span></span> | <span data-ttu-id="a12ef-142">課程名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="a12ef-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="a12ef-143">[1928533]</span></span> |<span data-ttu-id="a12ef-144">Azure 上的 SAP 應用程式︰支援的產品和大小</span><span class="sxs-lookup"><span data-stu-id="a12ef-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="a12ef-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="a12ef-145">[2015553]</span></span> |<span data-ttu-id="a12ef-146">Microsoft Azure 上的 SAP：支援的必要條件</span><span class="sxs-lookup"><span data-stu-id="a12ef-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="a12ef-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="a12ef-147">[1999351]</span></span> |<span data-ttu-id="a12ef-148">適用於 SAP 的增強型 Azure 監視功能</span><span class="sxs-lookup"><span data-stu-id="a12ef-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="a12ef-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="a12ef-149">[2178632]</span></span> |<span data-ttu-id="a12ef-150">Microsoft Azure 上的 SAP 主要監視度量</span><span class="sxs-lookup"><span data-stu-id="a12ef-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="a12ef-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="a12ef-151">[1999351]</span></span> |<span data-ttu-id="a12ef-152">Windows 上的虛擬化︰增強型監視功能</span><span class="sxs-lookup"><span data-stu-id="a12ef-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="a12ef-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="a12ef-153">[2243692]</span></span> |<span data-ttu-id="a12ef-154">針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體</span><span class="sxs-lookup"><span data-stu-id="a12ef-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="a12ef-155">深入了解 hello[的 Azure 訂用帳戶限制][azure-subscription-service-limits-subscription]，包括一般的預設限制和最大限制。</span><span class="sxs-lookup"><span data-stu-id="a12ef-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="a12ef-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>高可用性的 SAP 的 Azure Resource Manager vs hello Azure 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="a12ef-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="a12ef-157">會在下列區域的 hello 不同 hello Azure 資源管理員和 Azure 傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="a12ef-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="a12ef-158">資源群組</span><span class="sxs-lookup"><span data-stu-id="a12ef-158">Resource groups</span></span>
- <span data-ttu-id="a12ef-159">Azure 內部負載平衡器上 hello Azure 資源群組的相依性</span><span class="sxs-lookup"><span data-stu-id="a12ef-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="a12ef-160">支援 SAP 多 SID 案例</span><span class="sxs-lookup"><span data-stu-id="a12ef-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="a12ef-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> 資源群組</span><span class="sxs-lookup"><span data-stu-id="a12ef-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="a12ef-162">Azure 資源管理員 中，您可以使用資源群組 toomanage hello 應用程式的所有資源在您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a12ef-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="a12ef-163">整合式的方法，在資源群組中，所有資源有都 hello 相同生命週期。</span><span class="sxs-lookup"><span data-stu-id="a12ef-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="a12ef-164">例如，所有的資源在建立 hello 相同時間，而且它們已經刪除了 hello 位於相同的時間。</span><span class="sxs-lookup"><span data-stu-id="a12ef-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="a12ef-165">深入了解[資源群組](../../../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="a12ef-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure 內部負載平衡器上 hello Azure 資源群組的相依性</span><span class="sxs-lookup"><span data-stu-id="a12ef-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="a12ef-167">在 hello Azure 傳統部署模型中，沒有 hello Azure 內部負載平衡器 （Azure 負載平衡器服務） 與 hello 雲端服務群組之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="a12ef-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="a12ef-168">每個內部負載平衡器需要一個雲端服務群組。</span><span class="sxs-lookup"><span data-stu-id="a12ef-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="a12ef-169">Azure 資源管理員 中，您不需要 Azure 資源群組 toouse Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="a12ef-170">hello 環境是比較簡單且更有彈性。</span><span class="sxs-lookup"><span data-stu-id="a12ef-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="a12ef-171">支援 SAP 多 SID 案例</span><span class="sxs-lookup"><span data-stu-id="a12ef-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="a12ef-172">在 Azure Resource Manager 中，您可以在一個叢集中安裝多個 SAP 系統識別碼 (SID) ASCS/SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="a12ef-173">因為每個 Azure 內部負載平衡器的多個 IP 位址支援，可能有多重 SID 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="a12ef-174">toouse hello Azure 傳統部署模型，請遵循 hello 程序中所述[在 Azure 中的 SAP NetWeaver： 使用 Windows Server 容錯移轉叢集與 SIOS DataKeeper Azure 中的叢集 SAP ASCS/SCS 執行個體](http://go.microsoft.com/fwlink/?LinkId=613056)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a12ef-175">我們強烈建議您針對 SAP 安裝使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="a12ef-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="a12ef-176">它提供 hello 傳統部署模型中未提供的許多好處。</span><span class="sxs-lookup"><span data-stu-id="a12ef-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="a12ef-177">進一步了解 Azure [部署模型][virtual-machines-azure-resource-manager-architecture-benefits-arm]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="a12ef-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="a12ef-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="a12ef-179">Windows Server 容錯移轉叢集是高可用性的 SAP ASCS/SCS 安裝和 DBMS Windows 中的 hello 基礎。</span><span class="sxs-lookup"><span data-stu-id="a12ef-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="a12ef-180">容錯移轉叢集是 1 + n 個獨立的伺服器 （節點），會一起運作的應用程式和服務 tooincrease hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="a12ef-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="a12ef-181">如果節點失敗，Windows Server 容錯移轉叢集計算 hello 維護狀況良好時可能發生的失敗數目叢集 tooprovide 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="a12ef-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="a12ef-182">您可以選擇從不同的仲裁模式 tooachieve 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="a12ef-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> 仲裁模式</span><span class="sxs-lookup"><span data-stu-id="a12ef-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="a12ef-184">當您使用 Windows Server 容錯移轉叢集時，可以從四種仲裁模式中選擇：</span><span class="sxs-lookup"><span data-stu-id="a12ef-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="a12ef-185">**節點多數**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-185">**Node Majority**.</span></span> <span data-ttu-id="a12ef-186">Hello 叢集的每個節點可以在此投票。</span><span class="sxs-lookup"><span data-stu-id="a12ef-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="a12ef-187">一半以上的 hello 投票，也就是 hello 只能與大部分的投票，叢集函式。</span><span class="sxs-lookup"><span data-stu-id="a12ef-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="a12ef-188">我們建議針對節點數目為奇數的叢集使用此選項。</span><span class="sxs-lookup"><span data-stu-id="a12ef-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="a12ef-189">例如，七個節點叢集中的三個節點可能會失敗，而 hello 叢集靜像達成大多數並繼續 toorun。</span><span class="sxs-lookup"><span data-stu-id="a12ef-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="a12ef-190">**節點與磁碟多數**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="a12ef-191">每個節點與 hello 叢集存放區中的指定的磁碟 （磁碟見證） 可以在此投票可用且處於通訊狀態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="a12ef-192">hello 叢集函式只能搭配 hello 的多數投票，也就是一半以上的 hello 投票。</span><span class="sxs-lookup"><span data-stu-id="a12ef-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="a12ef-193">此模式適用於節點數目為偶數的叢集環境。</span><span class="sxs-lookup"><span data-stu-id="a12ef-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="a12ef-194">如果一半 hello 節點和 hello 磁碟在線上，hello 叢集會維持狀況良好的狀態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="a12ef-195">**節點與檔案共用多數**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="a12ef-196">Hello 系統管理員指定的檔案共用 （檔案共用見證） 會建立每個節點加號可以在此投票，不論 hello 節點與檔案共用是否可用且處於通訊。</span><span class="sxs-lookup"><span data-stu-id="a12ef-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="a12ef-197">hello 叢集函式只能搭配 hello 的多數投票，也就是一半以上的 hello 投票。</span><span class="sxs-lookup"><span data-stu-id="a12ef-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="a12ef-198">此模式適用於節點數目為偶數的叢集環境。</span><span class="sxs-lookup"><span data-stu-id="a12ef-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="a12ef-199">它類似 toohello 節點與磁碟多數 模式中，但是它使用見證檔案共用，而不是見證磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="a12ef-200">此模式是簡單 tooimplement，但如果 hello 檔案共用本身不是高可用性，它可能會成為單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="a12ef-201">**無多數：僅磁碟**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="a12ef-202">如果有一個節點可用且 hello 叢集存放區中的特定磁碟通訊，hello 叢集有仲裁。</span><span class="sxs-lookup"><span data-stu-id="a12ef-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="a12ef-203">也會在與該磁碟通訊的唯一 hello 節點可以加入 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="a12ef-204">建議您不要使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a12ef-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="a12ef-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server 容錯移轉叢集內部部署</span><span class="sxs-lookup"><span data-stu-id="a12ef-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="a12ef-206">圖 1 顯示兩個節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="a12ef-207">如果 hello hello 節點之間的網路連線失敗與這兩個節點才能保持註冊並執行，仲裁磁碟或檔案共用判斷哪一個節點會繼續 tooprovide hello 叢集的應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="a12ef-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="a12ef-208">hello 具有存取 toohello 仲裁磁碟或檔案共用為 hello 節點，以確保服務繼續執行。</span><span class="sxs-lookup"><span data-stu-id="a12ef-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="a12ef-209">由於這個範例會使用雙節點叢集，我們使用 hello 節點與檔案共用多數仲裁模式。</span><span class="sxs-lookup"><span data-stu-id="a12ef-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="a12ef-210">hello 節點與磁碟多數也是有效的選項。</span><span class="sxs-lookup"><span data-stu-id="a12ef-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="a12ef-211">在生產環境中，建議您使用仲裁磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="a12ef-212">您可以使用網路和儲存體系統技術 toomake 它高度可用。</span><span class="sxs-lookup"><span data-stu-id="a12ef-212">You can use network and storage system technology toomake it highly available.</span></span>

![圖 1：Azure 中 SAP ASCS/SCS 之 Windows Server 容錯移轉叢集組態的範例][sap-ha-guide-figure-1000]

<span data-ttu-id="a12ef-214">_**圖 1：**Azure 中 SAP ASCS/SCS 之 Windows Server 容錯移轉叢集組態的範例_</span><span class="sxs-lookup"><span data-stu-id="a12ef-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="a12ef-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> 共用儲存體</span><span class="sxs-lookup"><span data-stu-id="a12ef-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="a12ef-216">圖 1 也顯示兩個節點的共用儲存體叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="a12ef-217">在內部部署的共用存放裝置叢集中，hello 叢集中所有節點會都偵測共用存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a12ef-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="a12ef-218">鎖定機制會保護 hello 資料損毀。</span><span class="sxs-lookup"><span data-stu-id="a12ef-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="a12ef-219">所有節點也可以偵測到另一個節點是否發生失敗。</span><span class="sxs-lookup"><span data-stu-id="a12ef-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="a12ef-220">如果一個節點失敗，hello 剩餘的節點會取得 hello 存放裝置資源的擁有權，並確保 hello 可用性的服務。</span><span class="sxs-lookup"><span data-stu-id="a12ef-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-221">您不需要與某些 DBMS 應用程式 (例如 SQL Server) 共用提供高可用性的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="a12ef-222">SQL Server Alwayson 複寫 DBMS 資料和記錄檔從一個叢集節點 toohello 本機磁碟上的另一個叢集節點的 hello 本機磁碟上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="a12ef-223">在此情況下，Windows hello 的叢集設定不需要共用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="a12ef-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> 網路與名稱解析</span><span class="sxs-lookup"><span data-stu-id="a12ef-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="a12ef-225">用戶端電腦連線到 hello 叢集透過一個虛擬 IP 位址和虛擬主機名稱的 DNS 伺服器提供該 hello。</span><span class="sxs-lookup"><span data-stu-id="a12ef-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="a12ef-226">hello 內部節點以及 hello DNS 伺服器可以處理多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="a12ef-227">在一般設定中，您會使用兩個或更多個網路連線：</span><span class="sxs-lookup"><span data-stu-id="a12ef-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="a12ef-228">專用的連接 toohello 儲存體</span><span class="sxs-lookup"><span data-stu-id="a12ef-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="a12ef-229">叢集-內部網路連線的 hello 活動訊號</span><span class="sxs-lookup"><span data-stu-id="a12ef-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="a12ef-230">公用網路的用戶端使用 tooconnect toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="a12ef-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="a12ef-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Azure 中的 Windows Server 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="a12ef-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="a12ef-232">比較 toobare 金屬或私人雲端部署，Azure 虛擬機器需要額外的步驟 tooconfigure Windows Server 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="a12ef-233">當您建置共用的叢集磁碟時，您會需要數個 IP 位址和虛擬主機名稱的 tooset hello SAP ASCS/SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="a12ef-234">在本文中，我們會討論重要概念和 hello 額外的步驟需要的 toobuild 在 Azure 中 SAP 中央服務的高可用性叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="a12ef-235">我們會示範如何向上 hello 協力廠商工具 SIOS DataKeeper tooset 和如何 tooconfigure hello Azure 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="a12ef-236">您可以使用這些工具 toocreate Windows 容錯移轉叢集與 Azure 中的檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="a12ef-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![圖 2：Azure 中沒有共用磁碟的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1001]

<span data-ttu-id="a12ef-238">_**圖 2：**Azure 中沒有共用磁碟的 Windows Server 容錯移轉叢集組態_</span><span class="sxs-lookup"><span data-stu-id="a12ef-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="a12ef-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> 使用 SIOS DataKeeper 在 Azure 中共用磁碟</span><span class="sxs-lookup"><span data-stu-id="a12ef-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="a12ef-240">您需要針對高可用性的 SAP ASCS/SCS 執行個體叢集共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="a12ef-241">2016 年 9 月的 Azure 不提供共用存放裝置，您可以使用 toocreate 共用存放裝置叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="a12ef-242">您可以使用協力廠商軟體 SIOS DataKeeper 叢集版本 toocreate 鏡像的儲存體，可以模擬叢集共用存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a12ef-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="a12ef-243">hello SIOS 方案提供即時的同步資料複寫。</span><span class="sxs-lookup"><span data-stu-id="a12ef-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="a12ef-244">可以為叢集建立共用磁碟資源的方式為：</span><span class="sxs-lookup"><span data-stu-id="a12ef-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="a12ef-245">在 Windows 叢集組態中附加 hello 虛擬機器 (Vm) 的其他 Azure 虛擬硬碟 (VHD) tooeach。</span><span class="sxs-lookup"><span data-stu-id="a12ef-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="a12ef-246">在兩個虛擬機器節點上執行 SIOS DataKeeper Cluster Edition。</span><span class="sxs-lookup"><span data-stu-id="a12ef-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="a12ef-247">設定 SIOS DataKeeper 叢集版本，它會反映 hello hello 額外附加 VHD 的磁碟區從 hello 來源虛擬機器 toohello 額外附加 VHD 的磁碟區 hello 目標虛擬機器的內容。</span><span class="sxs-lookup"><span data-stu-id="a12ef-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="a12ef-248">SIOS DataKeeper 抽象化 hello 來源和目標本機磁碟區，並接著呈現 tooWindows Server 容錯移轉叢集與一個共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="a12ef-249">取得 [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a12ef-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![圖 3：Azure 中使用 SIOS DataKeeper 的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1002]

<span data-ttu-id="a12ef-251">_**圖 3：**Azure 中使用 SIOS DataKeeper 的 Windows Server 容錯移轉叢集組態_</span><span class="sxs-lookup"><span data-stu-id="a12ef-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-252">您不需要與某些 DBMS 產品 (例如 SQL Server) 共用提供高可用性的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="a12ef-253">SQL Server Alwayson 複寫 DBMS 資料和記錄檔從一個叢集節點 toohello 本機磁碟上的另一個叢集節點的 hello 本機磁碟上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="a12ef-254">在此情況下，Windows hello 的叢集設定不需要共用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="a12ef-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Azure 中的名稱解析</span><span class="sxs-lookup"><span data-stu-id="a12ef-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="a12ef-256">hello Azure 雲端平台不提供 hello 選項 tooconfigure 虛擬 IP 位址，例如浮點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="a12ef-257">您需要的替代方案 tooset 的虛擬 IP 位址 tooreach hello 叢集資源 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="a12ef-258">Azure hello Azure 負載平衡器服務中有內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="a12ef-259">與 hello 內部負載平衡器，用戶端會透過 hello 叢集虛擬 IP 位址連線 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="a12ef-260">您需要包含 hello 叢集節點的 hello 資源群組中的 toodeploy hello 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="a12ef-261">然後，設定所有必要的通訊埠與 hello 探查 hello 內部負載平衡器的連接埠轉送規則。</span><span class="sxs-lookup"><span data-stu-id="a12ef-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="a12ef-262">hello 用戶端可以透過 hello 虛擬主機名稱連接。</span><span class="sxs-lookup"><span data-stu-id="a12ef-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="a12ef-263">hello DNS 伺服器解析 hello 叢集 IP 位址，與 hello 內部負載平衡器控點連接埠轉送 toohello hello 叢集作用中的節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="a12ef-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Azure 基礎結構即服務 (IaaS) 中的 SAP NetWeaver 高可用性</span><span class="sxs-lookup"><span data-stu-id="a12ef-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="a12ef-265">tooachieve SAP 應用程式的高可用性，例如 SAP 軟體元件，您需要下列元件 tooprotect hello:</span><span class="sxs-lookup"><span data-stu-id="a12ef-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="a12ef-266">SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-266">SAP Application Server instance</span></span>
* <span data-ttu-id="a12ef-267">SAP ASCS/SCS 執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="a12ef-268">DBMS 伺服器</span><span class="sxs-lookup"><span data-stu-id="a12ef-268">DBMS server</span></span>

<span data-ttu-id="a12ef-269">如需在高可用性案例中保護 SAP 元件的詳細資訊，請參閱[適用於 SAP NetWeaver 的 Azure 虛擬機器規劃和實作](planning-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="a12ef-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> 高可用性的 SAP 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="a12ef-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="a12ef-271">您通常不需要特定的高可用性解決方案 hello SAP 應用程式伺服器和對話方塊執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="a12ef-272">您可以透過備援來達成高可用性，而且您會在 Azure 虛擬機器之不同的執行個體中，設定多個對話方塊執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="a12ef-273">您應該至少要有兩個 SAP 應用程式執行個體安裝在 Azure 虛擬機器的兩個執行個體中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![圖 4：高可用性的 SAP 應用程式伺服器][sap-ha-guide-figure-2000]

<span data-ttu-id="a12ef-275">_**圖 4：**高可用性的 SAP 應用程式伺服器_</span><span class="sxs-lookup"><span data-stu-id="a12ef-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="a12ef-276">您必須將所有虛擬機器主機中的 SAP 應用程式伺服器執行個體 hello 相同 Azure 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="a12ef-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="a12ef-277">Azure 可用性設定組可確保：</span><span class="sxs-lookup"><span data-stu-id="a12ef-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="a12ef-278">所有虛擬機器都屬於 hello 相同升級網域。</span><span class="sxs-lookup"><span data-stu-id="a12ef-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="a12ef-279">升級網域，例如，可確保 hello 虛擬機器不在 hello 更新相同計劃性的維護停機期間的時間。</span><span class="sxs-lookup"><span data-stu-id="a12ef-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="a12ef-280">所有虛擬機器都屬於 hello 相同容錯網域。</span><span class="sxs-lookup"><span data-stu-id="a12ef-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="a12ef-281">「 故障 」 網域，例如，確保已部署虛擬機器，以便任何單一失敗點會影響 hello 的所有虛擬機器的可用性。</span><span class="sxs-lookup"><span data-stu-id="a12ef-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="a12ef-282">深入了解如何太[管理虛擬機器可用性 hello][virtual-machines-manage-availability]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="a12ef-283">Hello Azure 儲存體帳戶是潛在的單一失敗點，因為它是重要的 toohave 至少兩個 Azure 儲存體帳戶，分兩個以上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="a12ef-284">在理想的安裝程式中執行 SAP dialog 執行個體的每部虛擬機器的 hello 磁碟將部署於不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a12ef-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="a12ef-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> 高可用性的 SAP ASCS/SCS 執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="a12ef-286">圖 5 是高可用性的 SAP ASCS/SCS 執行個體範例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![圖 5：高可用性的 SAP ASCS/SCS 執行個體][sap-ha-guide-figure-2001]

<span data-ttu-id="a12ef-288">_**圖 5：**高可用性的 SAP ASCS/SCS 執行個體_</span><span class="sxs-lookup"><span data-stu-id="a12ef-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="a12ef-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> 在 Azuer 中使用 Windows Server 容錯移轉叢集的 SAP ASCS/SCS 執行個體高可用性</span><span class="sxs-lookup"><span data-stu-id="a12ef-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="a12ef-290">比較 toobare 金屬或私人雲端部署，Azure 虛擬機器需要額外的步驟 tooconfigure Windows Server 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="a12ef-291">toobuild Windows 容錯移轉叢集，您需要共用的叢集磁碟、 幾個 IP 位址，數個虛擬主機名稱，以及 Azure 內部負載平衡器叢集化 SAP ASCS/SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="a12ef-292">我們將在討論 hello 文章稍後的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a12ef-292">We discuss this in more detail later in hello article.</span></span>

![圖 6：Azure 中使用 SIOS DataKeeper 之 SAP ASCS/SCS 的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1002]

<span data-ttu-id="a12ef-294">_**圖 6：**Azure 中使用 SIOS DataKeeper 之 SAP ASCS/SCS 的 Windows Server 容錯移轉叢集組態_</span><span class="sxs-lookup"><span data-stu-id="a12ef-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="a12ef-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> 高可用性的 DBMS 執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="a12ef-296">hello DBMS 也是 SAP 系統中的單一窗口。</span><span class="sxs-lookup"><span data-stu-id="a12ef-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="a12ef-297">您需要 tooprotect 它使用高可用性解決方案。</span><span class="sxs-lookup"><span data-stu-id="a12ef-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="a12ef-298">圖 7 顯示在 Azure 中的 SQL Server Alwayson 高可用性解決方案，Windows Server 容錯移轉叢集和 hello Azure 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="a12ef-299">SQL Server Always On 會使用自己的 DBMS 複寫來複寫 DBMS 資料和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a12ef-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="a12ef-300">在此情況下，您不需要叢集共用的磁碟，這可簡化 hello 整個安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a12ef-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![圖 7：高可用性的 SAP DBMS，使用 SQL Server Always On 的範例][sap-ha-guide-figure-2003]

<span data-ttu-id="a12ef-302">_**圖 7：**高可用性的 SAP DBMS，使用 SQL Server Always On 的範例_</span><span class="sxs-lookup"><span data-stu-id="a12ef-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="a12ef-303">如需在 Azure 中的 SQL Server 叢集所使用 hello Azure Resource Manager 部署模型的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="a12ef-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="a12ef-304">[使用 Resource Manager 在 Azure 虛擬機器中手動設定 Always On 可用性群組][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="a12ef-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="a12ef-305">[在 Azure 中設定 Always On 可用性群組的 Azure 內部負載平衡器][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="a12ef-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="a12ef-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> 端對端高可用性部署案例</span><span class="sxs-lookup"><span data-stu-id="a12ef-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="a12ef-307">使用架構範本 1 的部署案例</span><span class="sxs-lookup"><span data-stu-id="a12ef-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="a12ef-308">圖 8 顯示**一個** SAP 系統在 Azure 中 SAP NetWeaver 高可用性架構的範例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="a12ef-309">此案例如下所示設定︰</span><span class="sxs-lookup"><span data-stu-id="a12ef-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="a12ef-310">Hello SAP ASCS/SCS 執行個體使用一個專用的叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="a12ef-311">Hello DBMS 執行個體使用一個專用的叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="a12ef-312">SAP 應用程式伺服器執行個體會部署在他們自己專用的 VM。</span><span class="sxs-lookup"><span data-stu-id="a12ef-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![圖 8：SAP 高可用性架構範本 1，包含用於 ASCS/SCS 和用於 DBMS 執行個體的專用叢集][sap-ha-guide-figure-2004]

<span data-ttu-id="a12ef-314">_**圖 8：**SAP 高可用性架構範本 1，包含用於 ASCS/SCS 和用於 DBMS 執行個體的專用叢集_</span><span class="sxs-lookup"><span data-stu-id="a12ef-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="a12ef-315">使用架構範本 2 的部署案例</span><span class="sxs-lookup"><span data-stu-id="a12ef-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="a12ef-316">圖 9 顯示**一個** SAP 系統在 Azure 中 SAP NetWeaver 高可用性架構的範例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="a12ef-317">此案例如下所示設定︰</span><span class="sxs-lookup"><span data-stu-id="a12ef-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="a12ef-318">一個專用的叢集用於**兩者**hello SAP ASCS/SCS 執行個體，並且 hello DBMS。</span><span class="sxs-lookup"><span data-stu-id="a12ef-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="a12ef-319">SAP 應用程式伺服器執行個體會部署在自己專用的 VM。</span><span class="sxs-lookup"><span data-stu-id="a12ef-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![圖 9：SAP 高可用性架構範本 2，包含用於 ASCS/SCS 的專用叢集和用於 DBMS 的專用叢集][sap-ha-guide-figure-2005]

<span data-ttu-id="a12ef-321">_**圖 9：**SAP 高可用性架構範本 2，包含用於 ASCS/SCS 的專用叢集和用於 DBMS 的專用叢集_</span><span class="sxs-lookup"><span data-stu-id="a12ef-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="a12ef-322">使用架構範本 3 的部署案例</span><span class="sxs-lookup"><span data-stu-id="a12ef-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="a12ef-323">圖 10 顯示**兩個** SAP 系統與 &lt;SID1&gt; 和 &lt;SID2&gt;，在 Azure 中 SAP NetWeaver 高可用性架構的範例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="a12ef-324">此案例如下所示設定︰</span><span class="sxs-lookup"><span data-stu-id="a12ef-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="a12ef-325">一個專用的叢集用於**兩者**hello SAP ASCS/SCS SID1 執行個體*和*hello SAP ASCS/SCS SID2 執行個體 （一個叢集）。</span><span class="sxs-lookup"><span data-stu-id="a12ef-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="a12ef-326">一個專用的叢集用於 DBMS SID1，另一個專用的叢集用於 DBMS SID2 (兩個叢集)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="a12ef-327">Hello SID1 的 SAP 系統的 SAP 應用程式伺服器執行個體都有自己專用的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a12ef-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="a12ef-328">Hello SID2 的 SAP 系統的 SAP 應用程式伺服器執行個體都有自己專用的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a12ef-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![圖 10：SAP 高可用性架構範本 3，包含用於不同 ASCS/SCS 執行個體的專用叢集][sap-ha-guide-figure-6003]

<span data-ttu-id="a12ef-330">_**圖 10：**SAP 高可用性架構範本 3，包含用於不同 ASCS/SCS 執行個體的專用叢集_</span><span class="sxs-lookup"><span data-stu-id="a12ef-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="a12ef-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>準備 hello 基礎結構</span><span class="sxs-lookup"><span data-stu-id="a12ef-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="a12ef-332">Hello 基礎結構做好架構範本 1</span><span class="sxs-lookup"><span data-stu-id="a12ef-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="a12ef-333">適用於 SAP 的 Azure Resource Manager 範本有助於簡化部署所需的資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="a12ef-334">hello 三層式範本 Azure 資源管理員中也會支援這類高可用性案例架構的範本 1，有兩個叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="a12ef-335">每個叢集是適用於 SAP ASCS/SCS 和 DBMS 的 SAP 單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="a12ef-336">以下是您可以在其中取得 hello 範例案例，我們在本文中說明的 Azure 資源管理員範本：</span><span class="sxs-lookup"><span data-stu-id="a12ef-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="a12ef-337">Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="a12ef-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="a12ef-338">自訂映像</span><span class="sxs-lookup"><span data-stu-id="a12ef-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="a12ef-339">tooprepare hello 基礎結構架構範本 1:</span><span class="sxs-lookup"><span data-stu-id="a12ef-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="a12ef-340">在 Azure 入口網站上 hello hello**參數**刀鋒視窗中的，在 hello **SYSTEMAVAILABILITY**方塊中，選取**HA**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![圖 11：設定 SAP 高可用性 Azure Resource Manager 參數][sap-ha-guide-figure-3000]

<span data-ttu-id="a12ef-342">_**圖 11：**設定 SAP 高可用性 Azure Resource Manager 參數_</span><span class="sxs-lookup"><span data-stu-id="a12ef-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="a12ef-343">hello 範本會建立：</span><span class="sxs-lookup"><span data-stu-id="a12ef-343">hello templates create:</span></span>

  * <span data-ttu-id="a12ef-344">**虛擬機器**：</span><span class="sxs-lookup"><span data-stu-id="a12ef-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="a12ef-345">SAP 應用程式伺服器虛擬機器︰<*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="a12ef-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="a12ef-346">ASCS/SCS 叢集虛擬機器︰<*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="a12ef-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="a12ef-347">DBMS 叢集：<*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="a12ef-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="a12ef-348">**所有虛擬機器的網路卡，包含關聯的 IP 位址**：</span><span class="sxs-lookup"><span data-stu-id="a12ef-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="a12ef-349"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="a12ef-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="a12ef-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="a12ef-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="a12ef-351"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="a12ef-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="a12ef-352">**Azure 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="a12ef-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="a12ef-353">下列項目的**可用性群組**：</span><span class="sxs-lookup"><span data-stu-id="a12ef-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="a12ef-354">SAP 應用程式伺服器虛擬機器︰<*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="a12ef-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="a12ef-355">SAP ASCS/SCS 叢集虛擬機器︰<*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="a12ef-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="a12ef-356">DBMS 叢集虛擬機器︰<*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="a12ef-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="a12ef-357">**Azure 內部負載平衡器**：</span><span class="sxs-lookup"><span data-stu-id="a12ef-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="a12ef-358">與 hello ASCS/SCS 執行個體和 IP 位址的所有連接埠 <*SAPSystemSID*>-lb 集 ascs</span><span class="sxs-lookup"><span data-stu-id="a12ef-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="a12ef-359">與 hello 的 SQL Server DBMS 和 IP 位址的所有連接埠 <*SAPSystemSID*>-lb 集 db</span><span class="sxs-lookup"><span data-stu-id="a12ef-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="a12ef-360">**網路安全性群組**：<*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="a12ef-361">開啟外部的遠端桌面通訊協定 (RDP) 連接埠 toohello 與 <*SAPSystemSID*>-ascs-0 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a12ef-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-362">Hello 網路卡和 Azure 內部負載平衡器的所有 IP 位址都都**動態**預設。</span><span class="sxs-lookup"><span data-stu-id="a12ef-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="a12ef-363">它們也變更**靜態**IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="a12ef-364">我們將描述如何 toodo 這 hello 文件中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="a12ef-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="a12ef-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>使用公司網路連線能力 （跨內部部署） toouse 在生產環境中部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a12ef-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="a12ef-366">針對生產環境 SAP 系統，使用 Azure 站對站 VPN 或 Azure ExpressRoute，部署具有 [公司網路連線能力 (跨單位)][planning-guide-2.2] 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-367">您可以使用您的 Azure 虛擬網路執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="a12ef-368">hello 虛擬網路和子網路已建立並備妥。</span><span class="sxs-lookup"><span data-stu-id="a12ef-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="a12ef-369">在 Azure 入口網站上 hello hello**參數**刀鋒視窗中的，在 hello **NEWOREXISTINGSUBNET**方塊中，選取**現有**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="a12ef-370">在 hello **SUBNETID**方塊中，加入您備妥的 Azure 網路 SubnetID 您計劃 toodeploy Azure 虛擬機器的 hello 完整字串。</span><span class="sxs-lookup"><span data-stu-id="a12ef-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="a12ef-371">tooget 一份所有 Azure 網路子網路中，執行這個 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="a12ef-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="a12ef-372">hello**識別碼**欄位會顯示 hello **SUBNETID**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="a12ef-373">tooget 所有清單**SUBNETID**值，執行這個 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="a12ef-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="a12ef-374">hello **SUBNETID**看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a12ef-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="a12ef-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> 用於測試和示範的 SAP 執行個體僅限部署雲端</span><span class="sxs-lookup"><span data-stu-id="a12ef-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="a12ef-376">您可以在僅限雲端部署模型中部署您的高可用性 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="a12ef-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="a12ef-377">這種部署主要對於示範和測試的使用案例相當有用。</span><span class="sxs-lookup"><span data-stu-id="a12ef-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="a12ef-378">但不適用於生產環境使用案例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="a12ef-379">在 Azure 入口網站上 hello hello**參數**刀鋒視窗中的，在 hello **NEWOREXISTINGSUBNET**方塊中，選取**新**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="a12ef-380">保留 hello **SUBNETID**欄位空白。</span><span class="sxs-lookup"><span data-stu-id="a12ef-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="a12ef-381">hello SAP Azure Resource Manager 範本會自動建立 hello Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="a12ef-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-382">您也需要 toodeploy 至少一個專用的虛擬機器的 Active Directory 和 DNS 在 hello 相同 Azure 虛擬網路的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="a12ef-383">hello 範本並不會建立這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="a12ef-384">Hello 基礎結構做好架構範本 2</span><span class="sxs-lookup"><span data-stu-id="a12ef-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="a12ef-385">針對 SAP toohelp 簡化架構範本 2 SAP 部署必要的基礎結構資源，您可以使用此 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="a12ef-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="a12ef-386">您可以在這裡取得此部署案例的 Azure Resource Manager 範本：</span><span class="sxs-lookup"><span data-stu-id="a12ef-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="a12ef-387">Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="a12ef-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="a12ef-388">自訂映像</span><span class="sxs-lookup"><span data-stu-id="a12ef-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="a12ef-389">Hello 基礎結構做好架構範本 3</span><span class="sxs-lookup"><span data-stu-id="a12ef-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="a12ef-390">您可以準備 hello 基礎結構，並設定為 SAP**多重 SID**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="a12ef-391">例如，您可以將額外的 SAP ASCS/SCS 執行個體新增至現有的叢集組態以建立 SAP 多 SID 組態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="a12ef-392">如需詳細資訊，請參閱[Azure 資源管理員中設定額外的 SAP ASCS/SCS 執行個體到現有的叢集組態 toocreate SAP 多 SID 組態][sap-ha-multi-sid-guide]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="a12ef-393">如果您想 toocreate 新的多個 SID 叢集，您可以使用 hello 多重 SID [GitHub 上的快速入門範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="a12ef-394">toocreate 新的多個 SID 叢集，您需要下列三個範本 toodeploy hello:</span><span class="sxs-lookup"><span data-stu-id="a12ef-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="a12ef-395">ASCS/SCS 範本</span><span class="sxs-lookup"><span data-stu-id="a12ef-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="a12ef-396">資料庫範本</span><span class="sxs-lookup"><span data-stu-id="a12ef-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="a12ef-397">應用程式伺服器範本</span><span class="sxs-lookup"><span data-stu-id="a12ef-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="a12ef-398">hello 以下幾節有更多詳細 hello 範本和您需要 tooprovide hello 範本中的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="a12ef-399"><a name="ASCS-SCS-template"></a> ASCS/SCS 範本</span><span class="sxs-lookup"><span data-stu-id="a12ef-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="a12ef-400">hello ASCS/SCS 範本部署，您可以使用 toocreate 裝載多個 ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集的兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="a12ef-401">hello ASCS/SCS 多重 SID 範本，在 hello tooset [ASCS/SCS 多重 SID 範本][sap-templates-3-tier-multisid-xscs-marketplace-image]，輸入 hello 下列參數的值：</span><span class="sxs-lookup"><span data-stu-id="a12ef-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="a12ef-402">**資源前置詞**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-402">**Resource Prefix**.</span></span>  <span data-ttu-id="a12ef-403">設定 hello 資源前置詞，也就是使用的 tooprefix hello 部署期間建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="a12ef-404">Hello 資源不屬於 tooonly 一個 SAP 系統，因為 hello 資源 hello 前置詞不是 hello 一個 SAP 系統的 SID。</span><span class="sxs-lookup"><span data-stu-id="a12ef-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="a12ef-405">hello 首碼必須介於**三到六個字元**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="a12ef-406">**堆疊類型**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-406">**Stack Type**.</span></span> <span data-ttu-id="a12ef-407">選取 hello SAP 系統的 hello 堆疊型的別。</span><span class="sxs-lookup"><span data-stu-id="a12ef-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="a12ef-408">根據 hello 堆疊型別，Azure 負載平衡器具有一個 （ABAP 或 Java 只） 或兩個 (ABAP + Java) 私用每個 IP 位址的 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="a12ef-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="a12ef-409">**OS 類型**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-409">**OS Type**.</span></span> <span data-ttu-id="a12ef-410">選取 hello 作業系統 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="a12ef-411">**SAP 系統計數**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-411">**SAP System Count**.</span></span> <span data-ttu-id="a12ef-412">選取 hello 數目要 tooinstall 此叢集中的 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="a12ef-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="a12ef-413">**系統可用性**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-413">**System Availability**.</span></span> <span data-ttu-id="a12ef-414">選取 **HA**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-414">Select **HA**.</span></span>
  -  <span data-ttu-id="a12ef-415">**管理員使用者名稱和管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="a12ef-416">建立新的使用者可以使用的 toosign toohello 機器中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="a12ef-417">**新的或現有的子網路**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="a12ef-418">設定應該建立新的虛擬網路和子網路，還是應該使用現有子網路。</span><span class="sxs-lookup"><span data-stu-id="a12ef-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="a12ef-419">如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="a12ef-420">**子網路識別碼**。設定虛擬機器應該連接 hello 子網路 toowhich hello hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="a12ef-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="a12ef-421">選取您的虛擬私人網路 (VPN) 或 ExpressRoute 虛擬網路 tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="a12ef-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="a12ef-422">hello 識別碼通常看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a12ef-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="a12ef-423">/subscriptions/<*訂用帳戶識別碼*>/resourceGroups/<*資源群組名稱*>/providers/Microsoft.Network/virtualNetworks/<*虛擬網路名稱*>/subnets/<*子網路名稱*></span><span class="sxs-lookup"><span data-stu-id="a12ef-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="a12ef-424">hello 範本部署一個 Azure 負載平衡器執行個體，可支援多個 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="a12ef-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="a12ef-425">hello ASCS 執行個體的執行個體號碼 00，10，20 設定...</span><span class="sxs-lookup"><span data-stu-id="a12ef-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="a12ef-426">hello SCS 執行個體的執行個體號碼 01，11，21 設定...</span><span class="sxs-lookup"><span data-stu-id="a12ef-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="a12ef-427">hello ASCS Enqueue 複寫伺服器 （端） (僅 Linux) 執行個體的執行個體號碼 02，12，22 設定...</span><span class="sxs-lookup"><span data-stu-id="a12ef-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="a12ef-428">hello SCS 端 (只有 Linux) 執行個體設定的執行個體號碼 03，13，23...</span><span class="sxs-lookup"><span data-stu-id="a12ef-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="a12ef-429">hello 負載平衡器包含 1 (適用於 Linux 的 2) VIP(s)、 ASCS/SCS 1 x VIP 和 1 x VIP 端 (只有 Linux)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="a12ef-430">hello 下列清單包含所有的負載平衡的規則 （其中 x 是 hello 數目 hello SAP 系統，例如 1、 2、 3 …）：</span><span class="sxs-lookup"><span data-stu-id="a12ef-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="a12ef-431">每個 SAP 系統的 Windows 特定連接埠︰445、5985</span><span class="sxs-lookup"><span data-stu-id="a12ef-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="a12ef-432">ASCS 連接埠 (執行個體數目 x0)︰32x0、36x0、39x0、81x0、5x013、5x014、5x016</span><span class="sxs-lookup"><span data-stu-id="a12ef-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="a12ef-433">SCS 連接埠 (執行個體數目 x1)︰32x1、33x1、39x1、81x1、5x113、5x114、5x116</span><span class="sxs-lookup"><span data-stu-id="a12ef-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="a12ef-434">Linux 上的 ASCS ERS 連接埠 (執行個體數目 x2)︰33x2、5x213、5x214、5x216</span><span class="sxs-lookup"><span data-stu-id="a12ef-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="a12ef-435">Linux 上的 SCS ERS 連接埠 (執行個體數目 x3)︰33x3、5x313、5x314、5x316</span><span class="sxs-lookup"><span data-stu-id="a12ef-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="a12ef-436">hello 負載平衡器設定的 toouse hello 遵循 （其中 x 是 hello 數目 hello SAP 系統，例如 1、 2、 3 …） 的探查連接埠：</span><span class="sxs-lookup"><span data-stu-id="a12ef-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="a12ef-437">ASCS/SCS 內部負載平衡器探查連接埠︰620x0</span><span class="sxs-lookup"><span data-stu-id="a12ef-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="a12ef-438">ERS 內部負載平衡器探查連接埠 (僅 Linux)︰621x2</span><span class="sxs-lookup"><span data-stu-id="a12ef-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="a12ef-439"><a name="database-template"></a> 資料庫範本</span><span class="sxs-lookup"><span data-stu-id="a12ef-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="a12ef-440">hello 資料庫範本部署一或兩部虛擬機器，您可以使用 tooinstall hello 一個 SAP 系統的關聯式資料庫管理系統 (RDBMS)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="a12ef-441">例如，如果您部署五個 SAP 系統的 ASCS/SCS 範本，您需要 toodeploy 此範本五次。</span><span class="sxs-lookup"><span data-stu-id="a12ef-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="a12ef-442">hello 資料庫多 SID 範本，在 hello tooset[資料庫多 SID 範本][sap-templates-3-tier-multisid-db-marketplace-image]，輸入 hello 下列參數的值：</span><span class="sxs-lookup"><span data-stu-id="a12ef-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="a12ef-443">**SAP 系統識別碼**。輸入您想要 tooinstall 的 SAP 系統 hello hello SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="a12ef-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="a12ef-444">hello 識別碼將用於做為前置詞已部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="a12ef-445">**OS 類型**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-445">**Os Type**.</span></span> <span data-ttu-id="a12ef-446">選取 hello 作業系統 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="a12ef-447">**Dbtype**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-447">**Dbtype**.</span></span> <span data-ttu-id="a12ef-448">選取 hello 類型要 tooinstall hello 叢集上的 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a12ef-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="a12ef-449">選取**SQL**如果您想 tooinstall Microsoft SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a12ef-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="a12ef-450">選取**HANA**如果您打算 tooinstall SAP HANA hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="a12ef-451">請確定 tooselect hello 正確運作的系統類型： 選取**Windows** SQL，和 hana 選取 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="a12ef-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="a12ef-452">hello Azure 負載平衡器的虛擬機器必須連接的 toohello 設定 toosupport hello 選取資料庫類型：</span><span class="sxs-lookup"><span data-stu-id="a12ef-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="a12ef-453">**SQL**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-453">**SQL**.</span></span> <span data-ttu-id="a12ef-454">hello 負載平衡器將負載平衡連接埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="a12ef-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="a12ef-455">請確定 toouse for SQL Server Alwayson 安裝程式的這個連接埠。</span><span class="sxs-lookup"><span data-stu-id="a12ef-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="a12ef-456">**HANA**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-456">**HANA**.</span></span> <span data-ttu-id="a12ef-457">hello 負載平衡器將負載平衡連接埠 35015 和 35017。</span><span class="sxs-lookup"><span data-stu-id="a12ef-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="a12ef-458">請確定 tooinstall SAP HANA 與執行個體號碼**50**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="a12ef-459">hello 負載平衡器會使用探查連接埠 62550。</span><span class="sxs-lookup"><span data-stu-id="a12ef-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="a12ef-460">**SAP 系統大小**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-460">**Sap System Size**.</span></span> <span data-ttu-id="a12ef-461">會提供設定的新系統的 SAPS hello 的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="a12ef-462">如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="a12ef-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="a12ef-463">**系統可用性**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-463">**System Availability**.</span></span> <span data-ttu-id="a12ef-464">選取 **HA**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-464">Select **HA**.</span></span>
  -  <span data-ttu-id="a12ef-465">**管理員使用者名稱和管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="a12ef-466">建立新的使用者可以使用的 toosign toohello 機器中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="a12ef-467">**子網路識別碼**。輸入 hello 識別碼 hello hello hello ASCS/SCS 範本，請在部署您使用的子網路或建立 hello 子網路識別碼 hello hello ASCS/SCS 範本部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="a12ef-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="a12ef-468"><a name="application-servers-template"></a> 應用程式伺服器範本</span><span class="sxs-lookup"><span data-stu-id="a12ef-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="a12ef-469">hello 應用程式伺服器範本部署可以做一個 SAP 系統的 SAP 應用程式伺服器執行個體的兩個或多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="a12ef-470">例如，如果您部署五個 SAP 系統的 ASCS/SCS 範本，您需要 toodeploy 此範本五次。</span><span class="sxs-lookup"><span data-stu-id="a12ef-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="a12ef-471">hello 應用程式伺服器多 SID 範本中，在 hello tooset[應用程式伺服器多 SID 範本][sap-templates-3-tier-multisid-apps-marketplace-image]，輸入 hello 下列參數的值：</span><span class="sxs-lookup"><span data-stu-id="a12ef-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="a12ef-472">**SAP 系統識別碼**。輸入您想要 tooinstall 的 SAP 系統 hello hello SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="a12ef-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="a12ef-473">hello 識別碼將用於做為前置詞已部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="a12ef-474">**OS 類型**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-474">**Os Type**.</span></span> <span data-ttu-id="a12ef-475">選取 hello 作業系統 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="a12ef-476">**SAP 系統大小**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-476">**Sap System Size**.</span></span> <span data-ttu-id="a12ef-477">將提供的 SAPS hello 新系統的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="a12ef-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="a12ef-478">如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="a12ef-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="a12ef-479">**系統可用性**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-479">**System Availability**.</span></span> <span data-ttu-id="a12ef-480">選取 **HA**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-480">Select **HA**.</span></span>
  -  <span data-ttu-id="a12ef-481">**管理員使用者名稱和管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="a12ef-482">建立新的使用者可以使用的 toosign toohello 機器中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="a12ef-483">**子網路識別碼**。輸入 hello 識別碼 hello hello hello ASCS/SCS 範本，請在部署您使用的子網路或建立 hello 子網路識別碼 hello hello ASCS/SCS 範本部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="a12ef-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="a12ef-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a12ef-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="a12ef-485">在本例中，hello hello Azure 虛擬網路位址空間會是 10.0.0.0/16。</span><span class="sxs-lookup"><span data-stu-id="a12ef-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="a12ef-486">有一個名為 **Subnet**、網址範圍為 10.0.0.0/24 的子網路。</span><span class="sxs-lookup"><span data-stu-id="a12ef-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="a12ef-487">所有虛擬機器和內部負載平衡器會部署在此虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a12ef-488">不進行任何變更 toohello hello 客體作業系統內的網路設定。</span><span class="sxs-lookup"><span data-stu-id="a12ef-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="a12ef-489">包括 IP 位址、DNS 伺服器和子網路。</span><span class="sxs-lookup"><span data-stu-id="a12ef-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="a12ef-490">在 Azure 中設定所有網路設定。</span><span class="sxs-lookup"><span data-stu-id="a12ef-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="a12ef-491">hello 動態主機設定通訊協定 (DHCP) 服務會傳播您的設定。</span><span class="sxs-lookup"><span data-stu-id="a12ef-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="a12ef-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="a12ef-493">tooset hello 所需的 DNS IP 位址，執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="a12ef-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="a12ef-494">Hello hello 上的 Azure 入口網站中**DNS 伺服器**刀鋒視窗中，請確定您的虛擬網路**DNS 伺服器**選項設定得**自訂 DNS**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="a12ef-495">選取您根據的網路您擁有 hello 類型的設定。</span><span class="sxs-lookup"><span data-stu-id="a12ef-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="a12ef-496">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="a12ef-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="a12ef-497">[公司網路連線 （跨內部部署）][planning-guide-2.2]： 新增 hello hello 在內部部署 DNS 伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="a12ef-498">您可以擴充在內部部署 DNS 伺服器 toohello 虛擬機器會在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="a12ef-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="a12ef-499">在這種情況下，您可以加入 hello IP 位址的 hello Azure 虛擬機器執行 hello DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="a12ef-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="a12ef-500">[僅限雲端部署][planning-guide-2.1]： 部署額外的虛擬機器在 hello 做為 DNS 伺服器的相同虛擬網路執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="a12ef-501">新增 hello Azure hello IP 位址設定好 toorun DNS 服務的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![圖 12：設定 Azure 虛擬網路的 DNS 伺服器][sap-ha-guide-figure-3001]

    <span data-ttu-id="a12ef-503">_**圖 12：**設定 Azure 虛擬網路的 DNS 伺服器_</span><span class="sxs-lookup"><span data-stu-id="a12ef-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="a12ef-504">如果您變更 hello hello DNS 伺服器 IP 位址，您需要 toorestart hello Azure 虛擬機器 tooapply hello 變更，將傳播 hello 新 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="a12ef-505">在本例中，hello DNS 服務已安裝，並設定這些 Windows 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="a12ef-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="a12ef-506">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="a12ef-506">Virtual machine role</span></span> | <span data-ttu-id="a12ef-507">虛擬機器主機名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-507">Virtual machine host name</span></span> | <span data-ttu-id="a12ef-508">網路卡名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-508">Network card name</span></span> | <span data-ttu-id="a12ef-509">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a12ef-510">第一部 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="a12ef-510">First DNS server</span></span> |<span data-ttu-id="a12ef-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-511">domcontr-0</span></span> |<span data-ttu-id="a12ef-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="a12ef-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="a12ef-513">10.0.0.10</span></span> |
| <span data-ttu-id="a12ef-514">第二部 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="a12ef-514">Second DNS server</span></span> |<span data-ttu-id="a12ef-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-515">domcontr-1</span></span> |<span data-ttu-id="a12ef-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="a12ef-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="a12ef-517">10.0.0.11</span></span> |

### <span data-ttu-id="a12ef-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>主機名稱和 hello SAP ASCS/SCS 叢集執行個體和 DBMS 叢集執行個體的靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="a12ef-519">對於內部部署，您需要下列保留的主機名稱和 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a12ef-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="a12ef-520">虛擬主機名稱角色</span><span class="sxs-lookup"><span data-stu-id="a12ef-520">Virtual host name role</span></span> | <span data-ttu-id="a12ef-521">虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-521">Virtual host name</span></span> | <span data-ttu-id="a12ef-522">虛擬靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a12ef-523">SAP ASCS/SCS 第一個叢集虛擬主機名稱 (用於叢集管理)</span><span class="sxs-lookup"><span data-stu-id="a12ef-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="a12ef-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="a12ef-524">pr1-ascs-vir</span></span> |<span data-ttu-id="a12ef-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="a12ef-525">10.0.0.42</span></span> |
| <span data-ttu-id="a12ef-526">SAP ASCS/SCS 執行個體虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="a12ef-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="a12ef-527">pr1-ascs-sap</span></span> |<span data-ttu-id="a12ef-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="a12ef-528">10.0.0.43</span></span> |
| <span data-ttu-id="a12ef-529">SAP DBMS 第二個叢集虛擬主機名稱 (叢集管理)</span><span class="sxs-lookup"><span data-stu-id="a12ef-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="a12ef-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="a12ef-530">pr1-dbms-vir</span></span> |<span data-ttu-id="a12ef-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="a12ef-531">10.0.0.32</span></span> |

<span data-ttu-id="a12ef-532">當您建立 hello 叢集時，建立 hello 虛擬主機名稱**pr1-ascs-虛擬**和**pr1-dbms 層虛擬**和 hello 相關聯的管理 hello 叢集本身的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="a12ef-533">如需有關資訊 toodo，請參閱[收集在叢集組態中的叢集節點][sap-ha-guide-8.12.1]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="a12ef-534">您可以手動建立 hello 其他兩個的虛擬主機名稱， **pr1 ascs sap**和**pr1 dbms sap**，以及相關聯的 hello hello DNS 伺服器上的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="a12ef-535">hello 叢集的 SAP ASCS/SCS 執行個體和叢集的 hello DBMS 執行個體使用這些資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="a12ef-536">如需有關資訊 toodo，請參閱[建立叢集的 SAP ASCS/SCS 執行個體的虛擬主機名稱][sap-ha-guide-9.1.1]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="a12ef-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>設定靜態 IP 位址的 hello SAP 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a12ef-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="a12ef-538">在叢集中部署 hello 虛擬機器 toouse 之後，您需要 tooset 靜態 IP 位址的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="a12ef-539">Hello Azure 虛擬網路組態中，而不是在 hello 客體作業系統，請執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="a12ef-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="a12ef-540">在 hello Azure 入口網站，選取 **資源群組** > **網路卡** > **設定** > **IP 位址**.</span><span class="sxs-lookup"><span data-stu-id="a12ef-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="a12ef-541">在 hello **IP 位址**刀鋒視窗下**指派**，選取**靜態**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="a12ef-542">在 hello **IP 位址**方塊中，輸入您想 toouse hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a12ef-543">如果您變更 hello hello 網路卡的 IP 位址，您需要 toorestart hello Azure 虛擬機器 tooapply hello 變更。</span><span class="sxs-lookup"><span data-stu-id="a12ef-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![圖 13： 設定每個虛擬機器的 hello 網路卡的靜態 IP 位址][sap-ha-guide-figure-3002]

  <span data-ttu-id="a12ef-545">_**圖 13:**設定 hello 的每個虛擬機器的網路卡的靜態 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="a12ef-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="a12ef-546">也就是說，重複此步驟中的所有網路介面的所有虛擬機器，包括您想 toouse，為您的 Active Directory/DNS 服務的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="a12ef-547">在我們的範例中，有下列虛擬機器和靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a12ef-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="a12ef-548">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="a12ef-548">Virtual machine role</span></span> | <span data-ttu-id="a12ef-549">虛擬機器主機名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-549">Virtual machine host name</span></span> | <span data-ttu-id="a12ef-550">網路卡名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-550">Network card name</span></span> | <span data-ttu-id="a12ef-551">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a12ef-552">第一部 SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-552">First SAP Application Server instance</span></span> |<span data-ttu-id="a12ef-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-553">pr1-di-0</span></span> |<span data-ttu-id="a12ef-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-554">pr1-nic-di-0</span></span> |<span data-ttu-id="a12ef-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="a12ef-555">10.0.0.50</span></span> |
| <span data-ttu-id="a12ef-556">第二部 SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="a12ef-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-557">pr1-di-1</span></span> |<span data-ttu-id="a12ef-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-558">pr1-nic-di-1</span></span> |<span data-ttu-id="a12ef-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="a12ef-559">10.0.0.51</span></span> |
| <span data-ttu-id="a12ef-560">...</span><span class="sxs-lookup"><span data-stu-id="a12ef-560">...</span></span> |<span data-ttu-id="a12ef-561">...</span><span class="sxs-lookup"><span data-stu-id="a12ef-561">...</span></span> |<span data-ttu-id="a12ef-562">...</span><span class="sxs-lookup"><span data-stu-id="a12ef-562">...</span></span> |<span data-ttu-id="a12ef-563">...</span><span class="sxs-lookup"><span data-stu-id="a12ef-563">...</span></span> |
| <span data-ttu-id="a12ef-564">最後一部 SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="a12ef-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="a12ef-565">pr1-di-5</span></span> |<span data-ttu-id="a12ef-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="a12ef-566">pr1-nic-di-5</span></span> |<span data-ttu-id="a12ef-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="a12ef-567">10.0.0.55</span></span> |
| <span data-ttu-id="a12ef-568">ASCS/SCS 執行個體的第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="a12ef-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-569">pr1-ascs-0</span></span> |<span data-ttu-id="a12ef-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="a12ef-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="a12ef-571">10.0.0.40</span></span> |
| <span data-ttu-id="a12ef-572">ASCS/SCS 執行個體的第二個叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="a12ef-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-573">pr1-ascs-1</span></span> |<span data-ttu-id="a12ef-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="a12ef-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="a12ef-575">10.0.0.41</span></span> |
| <span data-ttu-id="a12ef-576">DBMS 執行個體的第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="a12ef-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-577">pr1-db-0</span></span> |<span data-ttu-id="a12ef-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="a12ef-578">pr1-nic-db-0</span></span> |<span data-ttu-id="a12ef-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="a12ef-579">10.0.0.30</span></span> |
| <span data-ttu-id="a12ef-580">DBMS 執行個體的第二個叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="a12ef-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-581">pr1-db-1</span></span> |<span data-ttu-id="a12ef-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="a12ef-582">pr1-nic-db-1</span></span> |<span data-ttu-id="a12ef-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="a12ef-583">10.0.0.31</span></span> |

### <span data-ttu-id="a12ef-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure 內部負載平衡器設定的靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="a12ef-585">hello SAP 的 Azure Resource Manager 範本會建立用於 hello SAP ASCS/SCS 執行個體的叢集和 hello DBMS 叢集 Azure 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a12ef-586">hello hello hello SAP ASCS/SCS 是虛擬的主機名稱的 IP 位址 hello 相同作為 hello hello SAP ASCS/SCS 內部負載平衡器 IP 位址： **pr1-lb 集 ascs**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="a12ef-587">hello hello dbms hello 虛擬名稱的 IP 位址 hello 相同作為 hello hello DBMS 內部負載平衡器 IP 位址： **pr1 lb dbms**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="a12ef-588">tooset hello Azure 內部的靜態 IP 位址的負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="a12ef-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="a12ef-589">hello 初始的部署設定 hello 內部負載平衡器 IP 位址太**動態**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="a12ef-590">Hello hello 上的 Azure 入口網站中**IP 位址**刀鋒視窗底下**指派**，選取**靜態**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="a12ef-591">Hello hello 內部負載平衡器的 IP 位址設定**pr1-lb 集 ascs** hello hello SAP ASCS/SCS 執行個體的虛擬主機名稱 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="a12ef-592">Hello hello 內部負載平衡器的 IP 位址設定**pr1 lb dbms** hello hello DBMS 執行個體的虛擬主機名稱 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![圖 14: Hello hello SAP ASCS/SCS 執行個體的內部負載平衡器設定靜態 IP 位址][sap-ha-guide-figure-3003]

  <span data-ttu-id="a12ef-594">_**圖 14:** hello hello SAP ASCS/SCS 執行個體的內部負載平衡器設定靜態 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="a12ef-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="a12ef-595">在我們的範例中，有兩個 Azure 內部負載平衡器具備這些靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a12ef-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="a12ef-596">Azure 內部負載平衡器角色</span><span class="sxs-lookup"><span data-stu-id="a12ef-596">Azure internal load balancer role</span></span> | <span data-ttu-id="a12ef-597">Azure 內部負載平衡器名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-597">Azure internal load balancer name</span></span> | <span data-ttu-id="a12ef-598">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a12ef-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a12ef-599">SAP ASCS/SCS 執行個體內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a12ef-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="a12ef-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="a12ef-600">pr1-lb-ascs</span></span> |<span data-ttu-id="a12ef-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="a12ef-601">10.0.0.43</span></span> |
| <span data-ttu-id="a12ef-602">SAP DBMS 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a12ef-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="a12ef-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="a12ef-603">pr1-lb-dbms</span></span> |<span data-ttu-id="a12ef-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="a12ef-604">10.0.0.33</span></span> |


### <span data-ttu-id="a12ef-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>預設 ASCS/SCS 負載平衡 hello Azure 內部負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="a12ef-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="a12ef-606">hello SAP 的 Azure Resource Manager 範本會建立您所需要的 hello 連接埠：</span><span class="sxs-lookup"><span data-stu-id="a12ef-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="a12ef-607">具有 hello 預設執行個體號碼的 ABAP ASCS 執行個體， **00**</span><span class="sxs-lookup"><span data-stu-id="a12ef-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="a12ef-608">Java SCS 執行個體，與 hello 預設執行個體號碼**01**</span><span class="sxs-lookup"><span data-stu-id="a12ef-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="a12ef-609">當您安裝 SAP ASCS/SCS 執行個體時，您必須使用 hello 預設執行個體號碼**00**的 ABAP ASCS 執行個體和 hello 預設執行個體號碼**01** Java SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="a12ef-610">接下來，建立必要的內部負載平衡 hello SAP NetWeaver 連接埠的端點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="a12ef-611">toocreate 所需內部負載平衡的端點，首先，建立這些負載平衡 hello SAP NetWeaver ABAP ASCS 連接埠的端點：</span><span class="sxs-lookup"><span data-stu-id="a12ef-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="a12ef-612">服務/負載平衡規則名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-612">Service/load balancing rule name</span></span> | <span data-ttu-id="a12ef-613">預設連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="a12ef-613">Default port numbers</span></span> | <span data-ttu-id="a12ef-614">(執行個體號碼為 00 的 ASCS 執行個體) (ERS 為 10) 的具體連接埠</span><span class="sxs-lookup"><span data-stu-id="a12ef-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a12ef-615">加入佇列伺服器 / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="a12ef-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="a12ef-616">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-617">3200</span><span class="sxs-lookup"><span data-stu-id="a12ef-617">3200</span></span> |
| <span data-ttu-id="a12ef-618">ABAP 訊息伺服器 / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="a12ef-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="a12ef-619">36<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-620">3600</span><span class="sxs-lookup"><span data-stu-id="a12ef-620">3600</span></span> |
| <span data-ttu-id="a12ef-621">內部 ABAP 訊息 / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="a12ef-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="a12ef-622">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-623">3900</span><span class="sxs-lookup"><span data-stu-id="a12ef-623">3900</span></span> |
| <span data-ttu-id="a12ef-624">訊息伺服器 HTTP / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="a12ef-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="a12ef-625">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-626">8100</span><span class="sxs-lookup"><span data-stu-id="a12ef-626">8100</span></span> |
| <span data-ttu-id="a12ef-627">SAP 啟動服務 ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="a12ef-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="a12ef-628">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="a12ef-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="a12ef-629">50013</span><span class="sxs-lookup"><span data-stu-id="a12ef-629">50013</span></span> |
| <span data-ttu-id="a12ef-630">SAP 啟動服務 ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="a12ef-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="a12ef-631">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="a12ef-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="a12ef-632">50014</span><span class="sxs-lookup"><span data-stu-id="a12ef-632">50014</span></span> |
| <span data-ttu-id="a12ef-633">加入佇列複寫 / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="a12ef-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="a12ef-634">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="a12ef-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="a12ef-635">50016</span><span class="sxs-lookup"><span data-stu-id="a12ef-635">50016</span></span> |
| <span data-ttu-id="a12ef-636">SAP 啟動服務 ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="a12ef-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="a12ef-637">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="a12ef-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="a12ef-638">51013</span><span class="sxs-lookup"><span data-stu-id="a12ef-638">51013</span></span> |
| <span data-ttu-id="a12ef-639">SAP 啟動服務 ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="a12ef-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="a12ef-640">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="a12ef-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="a12ef-641">51014</span><span class="sxs-lookup"><span data-stu-id="a12ef-641">51014</span></span> |
| <span data-ttu-id="a12ef-642">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="a12ef-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="a12ef-643">5985</span><span class="sxs-lookup"><span data-stu-id="a12ef-643">5985</span></span> |
| <span data-ttu-id="a12ef-644">檔案共用 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="a12ef-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="a12ef-645">445</span><span class="sxs-lookup"><span data-stu-id="a12ef-645">445</span></span> |

<span data-ttu-id="a12ef-646">_**表 1:**的連接埠號碼的 hello SAP NetWeaver ABAP ASCS 執行個體_</span><span class="sxs-lookup"><span data-stu-id="a12ef-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="a12ef-647">然後，建立這些負載平衡 hello SAP NetWeaver Java SCS 連接埠的端點：</span><span class="sxs-lookup"><span data-stu-id="a12ef-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="a12ef-648">服務/負載平衡規則名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-648">Service/load balancing rule name</span></span> | <span data-ttu-id="a12ef-649">預設連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="a12ef-649">Default port numbers</span></span> | <span data-ttu-id="a12ef-650">(執行個體號碼為 01 的 SCS 執行個體) (ERS 為 11) 的具體連接埠</span><span class="sxs-lookup"><span data-stu-id="a12ef-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a12ef-651">加入佇列伺服器 / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="a12ef-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="a12ef-652">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-653">3201</span><span class="sxs-lookup"><span data-stu-id="a12ef-653">3201</span></span> |
| <span data-ttu-id="a12ef-654">閘道伺服器 / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="a12ef-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="a12ef-655">33<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-656">3301</span><span class="sxs-lookup"><span data-stu-id="a12ef-656">3301</span></span> |
| <span data-ttu-id="a12ef-657">Java 訊息伺服器 / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="a12ef-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="a12ef-658">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-659">3901</span><span class="sxs-lookup"><span data-stu-id="a12ef-659">3901</span></span> |
| <span data-ttu-id="a12ef-660">訊息伺服器 HTTP / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="a12ef-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="a12ef-661">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="a12ef-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="a12ef-662">8101</span><span class="sxs-lookup"><span data-stu-id="a12ef-662">8101</span></span> |
| <span data-ttu-id="a12ef-663">SAP 啟動服務 SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="a12ef-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="a12ef-664">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="a12ef-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="a12ef-665">50113</span><span class="sxs-lookup"><span data-stu-id="a12ef-665">50113</span></span> |
| <span data-ttu-id="a12ef-666">SAP 啟動服務 SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="a12ef-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="a12ef-667">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="a12ef-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="a12ef-668">50114</span><span class="sxs-lookup"><span data-stu-id="a12ef-668">50114</span></span> |
| <span data-ttu-id="a12ef-669">加入佇列複寫 / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="a12ef-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="a12ef-670">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="a12ef-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="a12ef-671">50116</span><span class="sxs-lookup"><span data-stu-id="a12ef-671">50116</span></span> |
| <span data-ttu-id="a12ef-672">SAP 啟動服務 ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="a12ef-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="a12ef-673">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="a12ef-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="a12ef-674">51113</span><span class="sxs-lookup"><span data-stu-id="a12ef-674">51113</span></span> |
| <span data-ttu-id="a12ef-675">SAP 啟動服務 ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="a12ef-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="a12ef-676">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="a12ef-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="a12ef-677">51114</span><span class="sxs-lookup"><span data-stu-id="a12ef-677">51114</span></span> |
| <span data-ttu-id="a12ef-678">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="a12ef-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="a12ef-679">5985</span><span class="sxs-lookup"><span data-stu-id="a12ef-679">5985</span></span> |
| <span data-ttu-id="a12ef-680">檔案共用 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="a12ef-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="a12ef-681">445</span><span class="sxs-lookup"><span data-stu-id="a12ef-681">445</span></span> |

<span data-ttu-id="a12ef-682">_**表 2:**的連接埠號碼的 hello SAP NetWeaver Java SCS 執行個體_</span><span class="sxs-lookup"><span data-stu-id="a12ef-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![圖 15： 預設 ASCS/SCS 負載平衡 hello Azure 內部負載平衡器規則][sap-ha-guide-figure-3004]

<span data-ttu-id="a12ef-684">_**圖 15:**預設 ASCS/SCS 負載平衡 hello Azure 內部負載平衡器規則_</span><span class="sxs-lookup"><span data-stu-id="a12ef-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="a12ef-685">Hello hello 負載平衡器的 IP 位址設定**pr1 lb dbms** hello hello DBMS 執行個體的虛擬主機名稱 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="a12ef-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="a12ef-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="a12ef-687">如果您想 toouse 不同數字 hello SAP ASCS 或 SCS 執行個體時，您必須變更其連接埠的 hello 名稱和值的預設值。</span><span class="sxs-lookup"><span data-stu-id="a12ef-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="a12ef-688">在 hello Azure 入口網站，選取   **<* SID*>-lb 集 ascs 負載平衡器 * * >**負載平衡規則**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="a12ef-689">所有的負載平衡規則屬於 toohello SAP ASCS 或 SCS 執行個體，變更這些值：</span><span class="sxs-lookup"><span data-stu-id="a12ef-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="a12ef-690">名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-690">Name</span></span>
  * <span data-ttu-id="a12ef-691">連接埠</span><span class="sxs-lookup"><span data-stu-id="a12ef-691">Port</span></span>
  * <span data-ttu-id="a12ef-692">後端連接埠</span><span class="sxs-lookup"><span data-stu-id="a12ef-692">Back-end port</span></span>

  <span data-ttu-id="a12ef-693">例如，如果您想 toochange hello 預設 ASCS 執行個體號碼從 00 too31，您需要 toomake hello 變更如表 1 中所列的所有連接埠。</span><span class="sxs-lookup"><span data-stu-id="a12ef-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="a12ef-694">以下是連接埠 *lbrule3200*的更新範例。</span><span class="sxs-lookup"><span data-stu-id="a12ef-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![圖 16： 變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則][sap-ha-guide-figure-3005]

  <span data-ttu-id="a12ef-696">_**圖 16:**變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則_</span><span class="sxs-lookup"><span data-stu-id="a12ef-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="a12ef-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>新增 Windows 虛擬機器 toohello 網域</span><span class="sxs-lookup"><span data-stu-id="a12ef-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="a12ef-698">指派靜態 IP 位址 toohello 虛擬機器之後，新增 hello 虛擬機器 toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="a12ef-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![圖 17： 新增虛擬機器 tooa 網域][sap-ha-guide-figure-3006]

<span data-ttu-id="a12ef-700">_**圖 17:**新增虛擬機器 tooa 網域_</span><span class="sxs-lookup"><span data-stu-id="a12ef-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="a12ef-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Hello SAP ASCS/SCS 執行個體的兩個叢集節點上新增登錄項目</span><span class="sxs-lookup"><span data-stu-id="a12ef-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="a12ef-702">Azure 負載平衡器已關閉連線時 hello 連線閒置一段時間的時間 （閒置逾時） 的內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="a12ef-703">在對話方塊執行個體的開啟連接 toohello SAP 加入佇列中的 SAP 工作流程處理一旦 hello 第一個加入佇列/清除佇列要求需求 toobe 傳送。</span><span class="sxs-lookup"><span data-stu-id="a12ef-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="a12ef-704">這些連線通常會保持已建立 hello 工作處理程序才能或 hello 佇列處理序重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a12ef-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="a12ef-705">不過，如果 hello 連線已經閒置一段時間，hello Azure 內部負載平衡器關閉 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="a12ef-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="a12ef-706">這不是問題，因為 hello SAP 工作處理序重新建立 hello 連線 toohello 加入佇列的程序，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="a12ef-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="a12ef-707">這些活動會記載於 hello 開發人員追蹤 SAP 程序，但是他們建立大量額外的內容中這些追蹤。</span><span class="sxs-lookup"><span data-stu-id="a12ef-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="a12ef-708">它是個不錯的主意 toochange hello TCP/IP`KeepAliveTime`和`KeepAliveInterval`兩個叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="a12ef-709">結合這些變更的 hello TCP/IP 參數搭配 hello 本文稍後所述的 SAP 設定檔參數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="a12ef-710">tooadd hello SAP ASCS/SCS 執行個體的兩個叢集節點上的登錄項目首先，新增這些 Windows 登錄項目在這兩個 Windows 叢集節點上的 SAP ASCS/SCS 中：</span><span class="sxs-lookup"><span data-stu-id="a12ef-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="a12ef-711">Path</span><span class="sxs-lookup"><span data-stu-id="a12ef-711">Path</span></span> | <span data-ttu-id="a12ef-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="a12ef-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="a12ef-713">變數名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="a12ef-714">變數類型</span><span class="sxs-lookup"><span data-stu-id="a12ef-714">Variable type</span></span> |<span data-ttu-id="a12ef-715">REG_DWORD (十進位)</span><span class="sxs-lookup"><span data-stu-id="a12ef-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="a12ef-716">值</span><span class="sxs-lookup"><span data-stu-id="a12ef-716">Value</span></span> |<span data-ttu-id="a12ef-717">120000</span><span class="sxs-lookup"><span data-stu-id="a12ef-717">120000</span></span> |
| <span data-ttu-id="a12ef-718">連結 toodocumentation</span><span class="sxs-lookup"><span data-stu-id="a12ef-718">Link toodocumentation</span></span> |[<span data-ttu-id="a12ef-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="a12ef-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="a12ef-720">_**表 3:**變更 hello 第一個 TCP/IP 參數_</span><span class="sxs-lookup"><span data-stu-id="a12ef-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="a12ef-721">然後，在 SAP ASCS/SCS 的兩個 Windows 叢集節點上都新增下列 Windows 登錄項目：</span><span class="sxs-lookup"><span data-stu-id="a12ef-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="a12ef-722">路徑</span><span class="sxs-lookup"><span data-stu-id="a12ef-722">Path</span></span> | <span data-ttu-id="a12ef-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="a12ef-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="a12ef-724">變數名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="a12ef-725">變數類型</span><span class="sxs-lookup"><span data-stu-id="a12ef-725">Variable type</span></span> |<span data-ttu-id="a12ef-726">REG_DWORD (十進位)</span><span class="sxs-lookup"><span data-stu-id="a12ef-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="a12ef-727">值</span><span class="sxs-lookup"><span data-stu-id="a12ef-727">Value</span></span> |<span data-ttu-id="a12ef-728">120000</span><span class="sxs-lookup"><span data-stu-id="a12ef-728">120000</span></span> |
| <span data-ttu-id="a12ef-729">連結 toodocumentation</span><span class="sxs-lookup"><span data-stu-id="a12ef-729">Link toodocumentation</span></span> |[<span data-ttu-id="a12ef-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="a12ef-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="a12ef-731">_**表 4:**變更 hello 第二個 TCP/IP 參數_</span><span class="sxs-lookup"><span data-stu-id="a12ef-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="a12ef-732">**tooapply hello 變更，重新啟動這兩個叢集節點**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="a12ef-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> 設定 SAP ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="a12ef-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="a12ef-734">設定 SAP ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="a12ef-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="a12ef-735">在叢集組態中的收集 hello 叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="a12ef-736">設定叢集檔案共用見證</span><span class="sxs-lookup"><span data-stu-id="a12ef-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="a12ef-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>收集在叢集組態中的 hello 叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="a12ef-738">在 hello 新增角色及功能精靈，加入容錯移轉叢集 tooboth 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="a12ef-739">使用容錯移轉叢集管理員設定 hello 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="a12ef-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="a12ef-740">在 [容錯移轉叢集管理員] 中，選取**建立叢集**，然後再加入 hello 第一個叢集，節點 a 只 hello 名稱不要在新增 hello 第二個節點。您可以在稍後步驟中加入 hello 第二個節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![圖 18： 新增 hello 伺服器或虛擬機器名稱的第一個叢集節點 hello][sap-ha-guide-figure-3007]

  <span data-ttu-id="a12ef-742">_**圖 18:**新增 hello 伺服器或虛擬機器名稱的第一個叢集節點 hello_</span><span class="sxs-lookup"><span data-stu-id="a12ef-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="a12ef-743">輸入 hello 叢集網路名稱 （虛擬主機名稱） hello。</span><span class="sxs-lookup"><span data-stu-id="a12ef-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![圖 19： 輸入 hello 叢集名稱][sap-ha-guide-figure-3008]

  <span data-ttu-id="a12ef-745">_**圖 19:**輸入 hello 叢集名稱_</span><span class="sxs-lookup"><span data-stu-id="a12ef-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="a12ef-746">在您建立 hello 叢集後，執行叢集驗證測試。</span><span class="sxs-lookup"><span data-stu-id="a12ef-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![圖 20： 執行 hello 叢集驗證檢查][sap-ha-guide-figure-3009]

  <span data-ttu-id="a12ef-748">_**圖 20:**執行 hello 叢集驗證檢查_</span><span class="sxs-lookup"><span data-stu-id="a12ef-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="a12ef-749">您可以忽略這個時候 hello 程序中的磁碟的任何警告。</span><span class="sxs-lookup"><span data-stu-id="a12ef-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="a12ef-750">您要加入的檔案共用見證和 hello SIOS 共用磁碟更新版本。</span><span class="sxs-lookup"><span data-stu-id="a12ef-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="a12ef-751">在這個階段，您不需要 tooworry 具有仲裁。</span><span class="sxs-lookup"><span data-stu-id="a12ef-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![圖 21：找不到仲裁磁碟][sap-ha-guide-figure-3010]

  <span data-ttu-id="a12ef-753">_**圖 21：**_</span><span class="sxs-lookup"><span data-stu-id="a12ef-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![圖 22：核心叢集資源需要新的 IP 位址][sap-ha-guide-figure-3011]

  <span data-ttu-id="a12ef-755">_**圖 22：**核心叢集資源需要新的 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="a12ef-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="a12ef-756">變更 hello hello 核心叢集服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a12ef-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="a12ef-757">hello 叢集之前，無法啟動變更 hello IP 位址的 hello 核心叢集服務，因為 hello hello 伺服器 IP 位址指向 tooone 的 hello 虛擬機器節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="a12ef-758">這麼做在 hello**屬性**hello 核心叢集服務的 IP 資源頁面。</span><span class="sxs-lookup"><span data-stu-id="a12ef-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="a12ef-759">例如，我們需要 tooassign IP 位址 (在本例中， **10.0.0.42**) hello 叢集虛擬主機名稱**pr1-ascs-虛擬**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![圖 23: Hello 內容 對話方塊中變更 hello IP 位址][sap-ha-guide-figure-3012]

  <span data-ttu-id="a12ef-761">_**圖 23:**在 hello**屬性**對話方塊中，變更 hello IP 位址_</span><span class="sxs-lookup"><span data-stu-id="a12ef-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![圖 24： 已保留供 hello 叢集的 hello IP 位址指派給][sap-ha-guide-figure-3013]

  <span data-ttu-id="a12ef-763">_**圖 24:** hello hello 叢集保留的 IP 位址指派給_</span><span class="sxs-lookup"><span data-stu-id="a12ef-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="a12ef-764">將 hello 叢集虛擬主機名稱上線。</span><span class="sxs-lookup"><span data-stu-id="a12ef-764">Bring hello cluster virtual host name online.</span></span>

  ![圖 25： 叢集的核心服務已啟動且正在執行，並以 hello 更正 IP 位址][sap-ha-guide-figure-3014]

  <span data-ttu-id="a12ef-766">_**圖 25:**叢集的核心服務已啟動且正在執行且與 hello 更正 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="a12ef-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="a12ef-767">新增第二個叢集節點 hello。</span><span class="sxs-lookup"><span data-stu-id="a12ef-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="a12ef-768">Hello 核心叢集服務已啟動且正在執行，您可以新增 hello 第二個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![圖 26： 新增 hello 第二個叢集節點][sap-ha-guide-figure-3015]

  <span data-ttu-id="a12ef-770">_**圖 26:**新增 hello 第二個叢集節點_</span><span class="sxs-lookup"><span data-stu-id="a12ef-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="a12ef-771">輸入 hello 第二個叢集節點主機的名稱。</span><span class="sxs-lookup"><span data-stu-id="a12ef-771">Enter a name for hello second cluster node host.</span></span>

  ![圖 27： 輸入 hello 第二個叢集節點主機名稱][sap-ha-guide-figure-3016]

  <span data-ttu-id="a12ef-773">_**圖 27:**輸入 hello 第二個叢集節點主機名稱_</span><span class="sxs-lookup"><span data-stu-id="a12ef-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a12ef-774">務必要是屬於該 hello**新增所有合格的存放裝置 toohello 叢集** 核取方塊**不**選取。</span><span class="sxs-lookup"><span data-stu-id="a12ef-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![圖 28： 未選取 hello 核取方塊][sap-ha-guide-figure-3017]

  <span data-ttu-id="a12ef-776">_**圖 28:**不要**不**選取 hello 核取方塊_</span><span class="sxs-lookup"><span data-stu-id="a12ef-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="a12ef-777">您可以忽略有關仲裁和磁碟的警告。</span><span class="sxs-lookup"><span data-stu-id="a12ef-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="a12ef-778">您將會在 hello 仲裁和共用 hello 磁碟更新版本中中, 所述[SAP ASCS/SCS 叢集共用磁碟的安裝 SIOS DataKeeper 叢集版本][sap-ha-guide-8.12.3]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![圖 29： 忽略 hello 磁碟仲裁的相關警告][sap-ha-guide-figure-3018]

  <span data-ttu-id="a12ef-780">_**圖 29:**忽略 hello 磁碟仲裁的相關警告_</span><span class="sxs-lookup"><span data-stu-id="a12ef-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="a12ef-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> 設定叢集檔案共用見證</span><span class="sxs-lookup"><span data-stu-id="a12ef-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="a12ef-782">設定叢集檔案共用見證包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="a12ef-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="a12ef-783">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="a12ef-783">Creating a file share</span></span>
- <span data-ttu-id="a12ef-784">設定容錯移轉叢集管理員 中的 hello 檔案共用見證仲裁</span><span class="sxs-lookup"><span data-stu-id="a12ef-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="a12ef-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> 建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="a12ef-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="a12ef-786">選取檔案共用見證，而不是仲裁磁碟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="a12ef-787">SIOS DataKeeper 支援此選項。</span><span class="sxs-lookup"><span data-stu-id="a12ef-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="a12ef-788">在本文中的 hello 範例，hello 檔案共用見證是在 Azure 中執行的 hello Active Directory/DNS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="a12ef-789">hello 檔案共用見證稱為**domcontr 0**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="a12ef-790">您會設定 VPN 連線 tooAzure （透過站對站 VPN 或 Azure ExpressRoute），因為您 Active Directory/DNS 在內部部署和服務並不適合 toorun 檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="a12ef-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a12ef-791">如果只在內部部署 Active Directory/DNS 服務會不 hello Active Directory/DNS 的 Windows 作業系統執行內部部署上設定您的檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="a12ef-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="a12ef-792">在 Azure 和 Active Directory DNS 內部部署中執行之叢集節點之間的網路延遲可能太大，而且會造成連線問題。</span><span class="sxs-lookup"><span data-stu-id="a12ef-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="a12ef-793">為確定 tooconfigure hello 檔案共用見證正在關閉 toohello 叢集節點的 Azure 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="a12ef-794">hello 仲裁磁碟機需要至少 1024 MB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="a12ef-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="a12ef-795">我們建議的 hello 仲裁磁碟機的可用空間的 2048 MB。</span><span class="sxs-lookup"><span data-stu-id="a12ef-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="a12ef-796">新增 hello 叢集名稱物件。</span><span class="sxs-lookup"><span data-stu-id="a12ef-796">Add hello cluster name object.</span></span>

  ![圖 30： 指派 hello 共用的權限 hello hello 叢集名稱物件][sap-ha-guide-figure-3019]

  <span data-ttu-id="a12ef-798">_**圖 30:**指派 hello hello hello 叢集名稱物件共用的權限_</span><span class="sxs-lookup"><span data-stu-id="a12ef-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="a12ef-799">請務必 hello 權限，包含 hello hello 叢集名稱物件的共用資料夾中的 hello 授權 toochange 資料 (在本例中， **pr1-ascs-虛擬 $**)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="a12ef-800">tooadd hello 叢集名稱物件 toohello 清單中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="a12ef-801">變更電腦物件、 新增 toothose 圖 31 所示為 hello 篩選 toocheck。</span><span class="sxs-lookup"><span data-stu-id="a12ef-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![圖 31： 變更 hello 物件類型 tooinclude 電腦][sap-ha-guide-figure-3020]

  <span data-ttu-id="a12ef-803">_**圖 31:**變更 hello 物件類型 tooinclude 電腦_</span><span class="sxs-lookup"><span data-stu-id="a12ef-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![選取 [圖 32: Hello 的電腦] 核取方塊][sap-ha-guide-figure-3021]

  <span data-ttu-id="a12ef-805">_**圖 32:**選取 hello**電腦**核取方塊_</span><span class="sxs-lookup"><span data-stu-id="a12ef-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="a12ef-806">輸入 hello 的叢集名稱物件圖 31 中所示。</span><span class="sxs-lookup"><span data-stu-id="a12ef-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="a12ef-807">因為 hello 記錄已經建立，您可以變更 hello 權限，如圖 30 中所示。</span><span class="sxs-lookup"><span data-stu-id="a12ef-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="a12ef-808">選取 hello**安全性**hello 共用，並將其設定 索引標籤是更詳細的 hello 叢集名稱物件的權限。</span><span class="sxs-lookup"><span data-stu-id="a12ef-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![圖 33: Hello 檔案共用的仲裁設定 hello hello 叢集名稱物件的安全性屬性][sap-ha-guide-figure-3022]

  <span data-ttu-id="a12ef-810">_**圖 33:** hello 檔案共用的仲裁設定 hello hello 叢集名稱物件的安全性屬性_</span><span class="sxs-lookup"><span data-stu-id="a12ef-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="a12ef-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>設定容錯移轉叢集管理員 中的 hello 檔案共用見證仲裁</span><span class="sxs-lookup"><span data-stu-id="a12ef-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="a12ef-812">開啟 hello 設定仲裁設定精靈 」。</span><span class="sxs-lookup"><span data-stu-id="a12ef-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![圖 34： 啟動 hello 設定叢集仲裁設定精靈][sap-ha-guide-figure-3023]

  <span data-ttu-id="a12ef-814">_**圖 34:**開始 hello 設定叢集仲裁設定精靈_</span><span class="sxs-lookup"><span data-stu-id="a12ef-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="a12ef-815">在 hello**選取仲裁設定**頁面上，選取**選取 hello 仲裁見證**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![圖 35：您可以選擇的仲裁組態][sap-ha-guide-figure-3024]

  <span data-ttu-id="a12ef-817">_**圖 35：**您可以選擇的仲裁組態_</span><span class="sxs-lookup"><span data-stu-id="a12ef-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="a12ef-818">在 hello**選取仲裁見證**頁面上，選取**設定檔案共用見證**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![圖 36： 選取 hello 檔案共用見證][sap-ha-guide-figure-3025]

  <span data-ttu-id="a12ef-820">_**圖 36:**選取 hello 檔案共用見證_</span><span class="sxs-lookup"><span data-stu-id="a12ef-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="a12ef-821">輸入 hello UNC 路徑 toohello 檔案共用 (在本例中， \\domcontr 0\FSW)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="a12ef-822">toosee hello 進行的變更，選取一份**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![圖 37： 定義 hello hello 見證共用的檔案共用位置][sap-ha-guide-figure-3026]

  <span data-ttu-id="a12ef-824">_**圖 37:**定義 hello hello 見證共用的檔案共用位置_</span><span class="sxs-lookup"><span data-stu-id="a12ef-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="a12ef-825">選取 hello 您要的變更，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="a12ef-826">您需要 toosuccessfully 38 圖所示，重新設定 hello 叢集組態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![圖 38： 確認您已重新設定 hello 叢集][sap-ha-guide-figure-3027]

  <span data-ttu-id="a12ef-828">_**圖 38:**確認您已重新設定 hello 叢集_</span><span class="sxs-lookup"><span data-stu-id="a12ef-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="a12ef-829">已成功安裝 hello Windows 容錯移轉叢集之後, 在 Azure 中進行 toosome 閾值 tooadapt 容錯移轉偵測 tooconditions toobe 需要的變更。</span><span class="sxs-lookup"><span data-stu-id="a12ef-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="a12ef-830">hello 參數 toobe 變更會記載於這篇部落格： https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/。</span><span class="sxs-lookup"><span data-stu-id="a12ef-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="a12ef-831">假設兩個 Vm，建置 hello ASCS/SCS 的 Windows 叢集設定位於 hello 相同子網路、 hello 下列參數需要變更 toobe toothese 值：</span><span class="sxs-lookup"><span data-stu-id="a12ef-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="a12ef-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="a12ef-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="a12ef-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="a12ef-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="a12ef-834">這些設定和已測試的客戶提供良好的折衷方案 toobe 足夠彈性 hello 某一端。</span><span class="sxs-lookup"><span data-stu-id="a12ef-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="a12ef-835">Hello 上另一方面這些設定已提供快速不足，無法容錯移轉中 SAP 軟體或節點/VM 失敗真的錯誤條件。</span><span class="sxs-lookup"><span data-stu-id="a12ef-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="a12ef-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Hello SAP ASCS/SCS 叢集共用磁碟的安裝 SIOS DataKeeper 叢集版本</span><span class="sxs-lookup"><span data-stu-id="a12ef-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="a12ef-837">您現在在 Azure 中有運作中的 Windows Server 容錯移轉叢集組態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="a12ef-838">但是，tooinstall SAP ASCS/SCS 執行個體，您需要共用的磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="a12ef-839">您無法在 Azure 中建立您所需的 hello 共用磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="a12ef-840">SIOS DataKeeper 叢集版本是您可以使用 toocreate 共用磁碟資源的協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="a12ef-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="a12ef-841">叢集共用磁碟的 hello SAP ASCS/SCS 安裝 SIOS DataKeeper 叢集版本包含下列工作：</span><span class="sxs-lookup"><span data-stu-id="a12ef-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="a12ef-842">加入 hello.NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="a12ef-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="a12ef-843">安裝 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="a12ef-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="a12ef-844">設定 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="a12ef-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="a12ef-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>新增 hello.NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="a12ef-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="a12ef-846">hello Microsoft.NET Framework 3.5 不自動啟動，或是安裝在 Windows Server 2012 R2 上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="a12ef-847">因為 SIOS DataKeeper 需要 hello.NET Framework toobe DataKeeper 上所安裝的所有節點上，您必須安裝.NET Framework 3.5 hello hello hello 叢集中的所有虛擬機器的來賓作業系統上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="a12ef-848">有兩種方式 tooadd hello.NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="a12ef-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="a12ef-849">在 Windows 中使用 hello 新增角色及功能精靈 39 圖所示。</span><span class="sxs-lookup"><span data-stu-id="a12ef-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![圖 39： 使用 hello 新增角色及功能精靈來安裝.NET Framework 3.5 hello][sap-ha-guide-figure-3028]

  <span data-ttu-id="a12ef-851">_**圖 39:**使用 hello 新增角色及功能精靈安裝 hello.NET Framework 3.5_</span><span class="sxs-lookup"><span data-stu-id="a12ef-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![圖 40： 安裝進度列，當您安裝.NET Framework 3.5 hello 使用 hello 新增角色及功能精靈][sap-ha-guide-figure-3029]

  <span data-ttu-id="a12ef-853">_**圖 40:**安裝進度列，當您安裝.NET Framework 3.5 hello 使用 hello 新增角色及功能精靈_</span><span class="sxs-lookup"><span data-stu-id="a12ef-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="a12ef-854">使用 hello 命令列工具 dism.exe。</span><span class="sxs-lookup"><span data-stu-id="a12ef-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="a12ef-855">此類型的安裝，您必須在 hello Windows 安裝媒體上的 tooaccess hello SxS 目錄。</span><span class="sxs-lookup"><span data-stu-id="a12ef-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="a12ef-856">在提高權限的命令提示字元上，輸入：</span><span class="sxs-lookup"><span data-stu-id="a12ef-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="a12ef-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> 安裝 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="a12ef-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="a12ef-858">Hello 叢集中的每個節點上安裝 SIOS DataKeeper 叢集版本。</span><span class="sxs-lookup"><span data-stu-id="a12ef-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="a12ef-859">toocreate 虛擬共用存放裝置與 SIOS DataKeeper 建立同步處理的鏡像，然後模擬叢集共用存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a12ef-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="a12ef-860">安裝 hello SIOS 軟體之前，請建立 hello 網域使用者**DataKeeperSvc**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-861">新增 hello **DataKeeperSvc**使用者 toohello**本機系統管理員**群組兩個叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="a12ef-862">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="a12ef-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="a12ef-863">這兩個叢集節點上安裝 hello SIOS 軟體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![SIOS 安裝程式][sap-ha-guide-figure-3030]

  ![圖 41: Hello SIOS DataKeeper 安裝第一頁][sap-ha-guide-figure-3031]

  <span data-ttu-id="a12ef-866">_**圖 41:** hello SIOS DataKeeper 安裝第一頁_</span><span class="sxs-lookup"><span data-stu-id="a12ef-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="a12ef-867">在 hello 42 圖所示的對話方塊中，選取 **是**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![圖 42：DataKeeper 通知將停用某個服務][sap-ha-guide-figure-3032]

  <span data-ttu-id="a12ef-869">_**圖 42：**DataKeeper 通知將停用某個服務_</span><span class="sxs-lookup"><span data-stu-id="a12ef-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="a12ef-870">在 hello 43 圖所示的對話方塊中，我們建議您選取**網域或伺服器的帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![圖 43：SIOS DataKeeper 的使用者選項][sap-ha-guide-figure-3033]

  <span data-ttu-id="a12ef-872">_**圖 43：**SIOS DataKeeper 的使用者選項_</span><span class="sxs-lookup"><span data-stu-id="a12ef-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="a12ef-873">輸入 hello 網域帳戶使用者名稱和密碼 SIOS DataKeeper 所建立。</span><span class="sxs-lookup"><span data-stu-id="a12ef-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![圖 44： 輸入 hello 網域使用者名稱和密碼 hello SIOS DataKeeper 安裝][sap-ha-guide-figure-3034]

  <span data-ttu-id="a12ef-875">_**圖 44:**輸入 hello SIOS DataKeeper 安裝 hello 網域使用者名稱和密碼_</span><span class="sxs-lookup"><span data-stu-id="a12ef-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="a12ef-876">安裝 SIOS DataKeeper 執行個體中 45 圖所示為 hello 授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="a12ef-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![圖 45：輸入您的 SIOS DataKeeper 授權金鑰][sap-ha-guide-figure-3035]

  <span data-ttu-id="a12ef-878">_**圖 45：**輸入您的 SIOS DataKeeper 授權金鑰_</span><span class="sxs-lookup"><span data-stu-id="a12ef-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="a12ef-879">出現提示時，重新啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="a12ef-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> 設定 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="a12ef-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="a12ef-881">兩個節點上安裝 SIOS DataKeeper 之後，您會需要 toostart hello 組態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="a12ef-882">hello 組態 hello 目標是 toohave hello 其他 Vhd 附加 tooeach hello 虛擬機器之間的同步的資料複寫。</span><span class="sxs-lookup"><span data-stu-id="a12ef-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="a12ef-883">啟動 hello DataKeeper 管理和組態工具，然後選取**連線伺服器**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="a12ef-884">(在圖 46 中，此選項是用紅色圈起來的部分。)</span><span class="sxs-lookup"><span data-stu-id="a12ef-884">(In Figure 46, this option is circled in red.)</span></span>

  ![圖 46：SIOS DataKeeper 管理和組態工具][sap-ha-guide-figure-3036]

  <span data-ttu-id="a12ef-886">_**圖 46：**SIOS DataKeeper 管理和組態工具_</span><span class="sxs-lookup"><span data-stu-id="a12ef-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="a12ef-887">輸入 hello 名稱或 TCP/IP 位址的 hello 第一個節點 hello 管理和設定工具應該連接，並在第二個步驟中，hello 第二個節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![圖 47： 插入 hello 名稱或 TCP/IP 位址 hello 第一個節點 hello 管理和設定工具應該連接，然後在第二個步驟，hello 第二個節點][sap-ha-guide-figure-3037]

  <span data-ttu-id="a12ef-889">_**圖 47:**插入 hello 名稱或 TCP/IP 位址 hello 第一個節點 hello 管理和設定工具應該連接，然後在第二個步驟，hello 第二個節點_</span><span class="sxs-lookup"><span data-stu-id="a12ef-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="a12ef-890">建立 hello hello 兩個節點之間的複寫作業。</span><span class="sxs-lookup"><span data-stu-id="a12ef-890">Create hello replication job between hello two nodes.</span></span>

  ![圖 48：建立複寫作業][sap-ha-guide-figure-3038]

  <span data-ttu-id="a12ef-892">_**圖 48：**建立複寫作業_</span><span class="sxs-lookup"><span data-stu-id="a12ef-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="a12ef-893">精靈會引導您完成建立複寫作業的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="a12ef-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="a12ef-894">定義 hello 名稱、 TCP/IP 位址和磁碟區的 hello 來源節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![圖 49： 定義 hello hello 複寫作業名稱][sap-ha-guide-figure-3039]

  <span data-ttu-id="a12ef-896">_**圖 49:** hello 複寫作業定義 hello 名稱_</span><span class="sxs-lookup"><span data-stu-id="a12ef-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![圖 50： 定義 hello hello 節點，它應該 hello 目前的來源節點的基底的資料][sap-ha-guide-figure-3040]

  <span data-ttu-id="a12ef-898">_**圖 50:**定義 hello hello 節點，它應該 hello 目前的來源節點的基底資料_</span><span class="sxs-lookup"><span data-stu-id="a12ef-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="a12ef-899">定義 hello 名稱、 TCP/IP 位址和磁碟區的 hello 目標節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![圖 51： 定義 hello hello 節點，它應該 hello 目前的目標節點的基底的資料][sap-ha-guide-figure-3041]

  <span data-ttu-id="a12ef-901">_**圖 51:**定義 hello hello 節點，它應該 hello 目前的目標節點的基底資料_</span><span class="sxs-lookup"><span data-stu-id="a12ef-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="a12ef-902">定義 hello 壓縮演算法。</span><span class="sxs-lookup"><span data-stu-id="a12ef-902">Define hello compression algorithms.</span></span> <span data-ttu-id="a12ef-903">在本例中，我們建議您壓縮 hello 複寫資料流。</span><span class="sxs-lookup"><span data-stu-id="a12ef-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="a12ef-904">重新同步處理的情況下，尤其是在 hello 複寫資料流的 hello 壓縮會大幅減少重新同步處理時間。</span><span class="sxs-lookup"><span data-stu-id="a12ef-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="a12ef-905">請注意，壓縮會使用 hello 虛擬機器的 CPU 和 RAM 資源。</span><span class="sxs-lookup"><span data-stu-id="a12ef-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="a12ef-906">隨著 hello 壓縮率增加，因此沒有 hello 使用的 CPU 資源數量。</span><span class="sxs-lookup"><span data-stu-id="a12ef-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="a12ef-907">您也可以稍後調整此設定。</span><span class="sxs-lookup"><span data-stu-id="a12ef-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="a12ef-908">另一個設定您需要 toocheck 是 hello 複寫是否進行非同步或同步。</span><span class="sxs-lookup"><span data-stu-id="a12ef-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="a12ef-909">*當您保護 SAP ASCS/SCS 組態時，您必須使用同步複寫*。</span><span class="sxs-lookup"><span data-stu-id="a12ef-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![圖 52︰定義複寫詳細資料][sap-ha-guide-figure-3042]

  <span data-ttu-id="a12ef-911">_**圖 52︰**定義複寫詳細資料_</span><span class="sxs-lookup"><span data-stu-id="a12ef-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="a12ef-912">定義 hello 磁碟區複寫的 hello 複寫作業是否應為表示的 tooa 做為共用磁碟，Windows Server 容錯移轉叢集叢集組態。</span><span class="sxs-lookup"><span data-stu-id="a12ef-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="a12ef-913">Hello SAP ASCS/SCS 設定，請選取**是**使叢集會看見 hello Windows hello 與可作為叢集磁碟區的共用磁碟的複寫磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a12ef-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![圖 53： 選取 [是] tooset hello 複寫磁碟區為叢集磁碟區][sap-ha-guide-figure-3043]

  <span data-ttu-id="a12ef-915">_**圖 53:**選取**是**tooset hello 複寫磁碟區為叢集磁碟區_</span><span class="sxs-lookup"><span data-stu-id="a12ef-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="a12ef-916">建立 hello 磁碟區之後，hello DataKeeper 管理和設定工具會顯示該 hello 複寫作業為作用中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![圖 54: DataKeeper 同步鏡像 hello SAP ASCS/SCS 共用磁碟為作用中][sap-ha-guide-figure-3044]

  <span data-ttu-id="a12ef-918">_**圖 54:**針對 hello SAP ASCS/SCS 共用磁碟 DataKeeper 同步鏡像為作用中_</span><span class="sxs-lookup"><span data-stu-id="a12ef-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="a12ef-919">容錯移轉叢集管理員現在會顯示 hello 磁碟作為 DataKeeper 磁碟，如下圖 55 所示。</span><span class="sxs-lookup"><span data-stu-id="a12ef-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![圖 55： 容錯移轉叢集管理員顯示 hello 磁碟 DataKeeper 複寫][sap-ha-guide-figure-3045]

  <span data-ttu-id="a12ef-921">_**圖 55:**容錯移轉叢集管理員顯示 hello 磁碟複寫該 DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="a12ef-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="a12ef-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>安裝 hello SAP NetWeaver 系統</span><span class="sxs-lookup"><span data-stu-id="a12ef-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="a12ef-923">由於龐大而有所不同 hello 您使用的 DBMS 系統，我們將不會說明 hello DBMS 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a12ef-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="a12ef-924">不過，我們假設 hello 不同 DBMS 廠商都支援適用於 Azure 的 hello 原有處理，以 hello DBMS 的高可用性考量。</span><span class="sxs-lookup"><span data-stu-id="a12ef-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="a12ef-925">例如，適用於 SQL Server 的 Always On 或資料庫鏡像，以及適用於 Oracle 資料庫的 Oracle Data Guard。</span><span class="sxs-lookup"><span data-stu-id="a12ef-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="a12ef-926">在本文章中我們使用 hello 案例中，我們並未新增更多的保護 toohello DBMS。</span><span class="sxs-lookup"><span data-stu-id="a12ef-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="a12ef-927">當不同的 DBMS 服務與 Azure 中這種叢集 SAP ASCS/SCS 組態互動時，沒有任何特殊的考量。</span><span class="sxs-lookup"><span data-stu-id="a12ef-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-928">hello 的 SAP NetWeaver ABAP 系統、 Java 系統和 ABAP + Java 系統的安裝程序是幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="a12ef-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="a12ef-929">hello 最大的差別在於 SAP ABAP 系統有一個 ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="a12ef-930">hello SAP Java 系統有一個 SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="a12ef-931">hello SAP ABAP + Java 系統有一個 ASCS 執行個體和一個 SCS 執行個體中執行 hello 相同 Microsoft 容錯移轉叢集群組。</span><span class="sxs-lookup"><span data-stu-id="a12ef-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="a12ef-932">我們會明確說明每個 SAP NetWeaver 安裝堆疊的所有安裝差異。</span><span class="sxs-lookup"><span data-stu-id="a12ef-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="a12ef-933">您可以假設所有其他部分會 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="a12ef-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="a12ef-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> 使用高可用性 ASCS/SCS 執行個體安裝 SAP</span><span class="sxs-lookup"><span data-stu-id="a12ef-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a12ef-935">請務必的 tooplace DataKeeper 執行您的頁面檔案鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a12ef-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="a12ef-936">DataKeeper 不支援鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a12ef-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="a12ef-937">您可以將分頁檔 hello 暫存磁碟機 D 的 Azure 虛擬機器上 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="a12ef-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="a12ef-938">如果它已經不存在，請移動 hello Windows 分頁檔案 toodrive D 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a12ef-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="a12ef-939">使用高可用性 ASCS/SCS 執行個體安裝 SAP 包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="a12ef-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="a12ef-940">建立 hello 叢集化 SAP ASCS/SCS 執行個體的虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="a12ef-941">安裝 hello SAP 第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="a12ef-942">修改 hello ASCS/SCS 執行個體的 hello SAP 設定檔</span><span class="sxs-lookup"><span data-stu-id="a12ef-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="a12ef-943">新增探查連接埠</span><span class="sxs-lookup"><span data-stu-id="a12ef-943">Adding a probe port</span></span>
- <span data-ttu-id="a12ef-944">開啟 Windows 防火牆探查連接埠 hello</span><span class="sxs-lookup"><span data-stu-id="a12ef-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="a12ef-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>建立 hello 叢集化 SAP ASCS/SCS 執行個體的虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="a12ef-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="a12ef-946">在 hello Windows DNS 管理員中，建立 hello hello ASCS/SCS 執行個體的虛擬主機名稱的 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="a12ef-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a12ef-947">hello 分派 toohello hello ASCS/SCS 執行個體必須是虛擬的主機名稱的 IP 位址 hello 相同 hello IP 位址指派給 tooAzure 負載平衡器 (**<*SID*>-lb 集 ascs**).</span><span class="sxs-lookup"><span data-stu-id="a12ef-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="a12ef-948">hello hello 虛擬 SAP ASCS/SCS 主機名稱 IP 位址 (**pr1 ascs sap**) hello 相同作為 hello Azure 負載平衡器 IP 位址 (**pr1-lb 集 ascs**)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![圖 56： 定義 hello hello SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目][sap-ha-guide-figure-3046]

  <span data-ttu-id="a12ef-950">_**圖 56:**定義 hello hello SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目_</span><span class="sxs-lookup"><span data-stu-id="a12ef-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="a12ef-951">toodefine hello IP 位址指派 toohello 虛擬主機名稱，選取**DNS 管理員** > **網域**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![圖 57：SAP ASCS/SCS 叢集組態的新虛擬名稱和 TCP/IP 位址][sap-ha-guide-figure-3047]

  <span data-ttu-id="a12ef-953">_**圖 57：**SAP ASCS/SCS 叢集組態的新虛擬名稱和 TCP/IP 位址_</span><span class="sxs-lookup"><span data-stu-id="a12ef-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="a12ef-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>安裝 hello SAP 第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="a12ef-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="a12ef-955">執行 hello 第一個叢集節點選項，在叢集節點 a。例如，在 hello **pr1 ascs 0**主機。</span><span class="sxs-lookup"><span data-stu-id="a12ef-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="a12ef-956">tookeep hello 預設連接埠 hello Azure 內部負載平衡器中，選取：</span><span class="sxs-lookup"><span data-stu-id="a12ef-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="a12ef-957">**ABAP 系統**：**ASCS** 執行個體號碼 **00**</span><span class="sxs-lookup"><span data-stu-id="a12ef-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="a12ef-958">**Java 系統**：**SCS** 執行個體號碼 **01**</span><span class="sxs-lookup"><span data-stu-id="a12ef-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="a12ef-959">**ABAP+Java 系統**：**ASCS** 執行個體號碼 **00** 和 **SCS** 執行個體號碼 **01**</span><span class="sxs-lookup"><span data-stu-id="a12ef-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="a12ef-960">toouse 執行個體數字而不是 00 hello ABAP ASCS 執行個體和 hello Java SCS 執行個體的 01、 toochange hello Azure 內部負載平衡器預設負載平衡中所述的規則先[變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則][sap-ha-guide-8.9]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="a12ef-961">hello 下一步幾項工作不 hello 標準 SAP 安裝文件所述。</span><span class="sxs-lookup"><span data-stu-id="a12ef-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-962">hello SAP 安裝文件集說明如何 tooinstall hello 第一個 ASCS/SCS 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="a12ef-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="a12ef-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>修改 hello ASCS/SCS 執行個體的 hello SAP 設定檔</span><span class="sxs-lookup"><span data-stu-id="a12ef-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="a12ef-964">您需要 tooadd 新的設定檔參數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="a12ef-965">hello 設定檔參數可防止 SAP 工作程序與 hello enqueue 伺服器之間的連線關閉時，它們閒置的時間太長。</span><span class="sxs-lookup"><span data-stu-id="a12ef-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="a12ef-966">我們曾提及中的 hello 問題狀況[hello SAP ASCS/SCS 執行個體的兩個叢集節點上新增登錄項目][sap-ha-guide-8.11]。</span><span class="sxs-lookup"><span data-stu-id="a12ef-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="a12ef-967">在該區段中，我們也引進了兩個變更 toosome 基本 TCP/IP 連線參數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="a12ef-968">在第二個步驟中，您需要 tooset hello enqueue 伺服器 toosend`keep_alive`發出訊號，以便 hello 連線未遇到 hello Azure 內部負載平衡器的閒置臨界值。</span><span class="sxs-lookup"><span data-stu-id="a12ef-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="a12ef-969">toomodify hello hello ASCS/SCS 執行個體的 SAP 設定檔：</span><span class="sxs-lookup"><span data-stu-id="a12ef-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="a12ef-970">新增此設定檔參數 toohello SAP ASCS/SCS 執行個體的設定檔：</span><span class="sxs-lookup"><span data-stu-id="a12ef-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="a12ef-971">在本例中，hello 路徑為：</span><span class="sxs-lookup"><span data-stu-id="a12ef-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="a12ef-972">例如，toohello SAP SCS 執行個體設定檔和對應的路徑：</span><span class="sxs-lookup"><span data-stu-id="a12ef-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="a12ef-973">tooapply hello 變更，重新啟動 hello /SCS SAP ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a12ef-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="a12ef-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> 新增探查連接埠</span><span class="sxs-lookup"><span data-stu-id="a12ef-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="a12ef-975">使用 Azure 負載平衡器中的 hello 內部負載平衡器探查功能 toomake hello 整個叢集組態工作。</span><span class="sxs-lookup"><span data-stu-id="a12ef-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="a12ef-976">hello Azure 內部負載平衡器通常會參與虛擬機器之間的平均 hello 連入的工作負載。</span><span class="sxs-lookup"><span data-stu-id="a12ef-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="a12ef-977">不過，這對某些叢集組態不會產生作用，因為只有一個執行個體是主動的。</span><span class="sxs-lookup"><span data-stu-id="a12ef-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="a12ef-978">hello 其他執行個體為被動，無法接受 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="a12ef-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="a12ef-979">Hello Azure 內部負載平衡器指派工作只有 tooan 作用中的執行個體時，可幫助探查功能。</span><span class="sxs-lookup"><span data-stu-id="a12ef-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="a12ef-980">Hello 探查功能，與 hello 內部負載平衡器可以偵測到哪些執行個體作用中，而只與 hello 工作負載的 hello 執行個體然後目標。</span><span class="sxs-lookup"><span data-stu-id="a12ef-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="a12ef-981">tooadd 探查連接埠：</span><span class="sxs-lookup"><span data-stu-id="a12ef-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="a12ef-982">檢查目前的 hello **ProbePort**藉由執行下列 PowerShell 命令的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a12ef-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="a12ef-983">執行從 hello 虛擬機器的其中一個內 hello 叢集組態中。</span><span class="sxs-lookup"><span data-stu-id="a12ef-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="a12ef-984">定義探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="a12ef-984">Define a probe port.</span></span> <span data-ttu-id="a12ef-985">hello 預設探查連接埠號碼是**0**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="a12ef-986">在我們的範例中，我們會使用探查連接埠 **62000**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-986">In our example, we use probe port **62000**.</span></span>

  ![圖 58: hello 叢集設定探查連接埠為預設值 0][sap-ha-guide-figure-3048]

  <span data-ttu-id="a12ef-988">_**圖 58:** hello 預設叢集設定探查連接埠為 0_</span><span class="sxs-lookup"><span data-stu-id="a12ef-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="a12ef-989">hello 連接埠號碼是 SAP 的 Azure Resource Manager 範本中定義。</span><span class="sxs-lookup"><span data-stu-id="a12ef-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="a12ef-990">您可以指定在 PowerShell 中的 hello 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="a12ef-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="a12ef-991">tooset hello 的新 ProbePort 值 **SAP <*SID*> IP * * 叢集資源，執行下列 PowerShell 指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="a12ef-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="a12ef-992">更新您的環境的 hello PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="a12ef-993">Hello 指令碼執行之後，您將會提示的 toorestart hello SAP 叢集群組 tooactivate hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="a12ef-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="a12ef-994">使 hello 之後 **SAP <*SID*> * * 叢集角色上線，請確認**ProbePort**設定 toohello 新值。</span><span class="sxs-lookup"><span data-stu-id="a12ef-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![設定 hello 新值之後，圖 59： 探查 hello 叢集通訊埠][sap-ha-guide-figure-3049]

  <span data-ttu-id="a12ef-996">_**圖 59:**探查 hello 叢集通訊埠設定 hello 新值之後_</span><span class="sxs-lookup"><span data-stu-id="a12ef-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="a12ef-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>開啟 Windows 防火牆探查連接埠 hello</span><span class="sxs-lookup"><span data-stu-id="a12ef-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="a12ef-998">您需要 tooopen 兩個叢集節點上的 Windows 防火牆探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="a12ef-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="a12ef-999">使用下列指令碼 tooopen Windows 防火牆的探查連接埠的 hello。</span><span class="sxs-lookup"><span data-stu-id="a12ef-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="a12ef-1000">更新您的環境的 hello PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="a12ef-1001">hello **ProbePort**設定得**62000**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="a12ef-1002">現在您可以存取 hello 檔案共用 **\\\ascsha-clsap\sapmnt**與其他主控件，例如在**ascsha dba**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="a12ef-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>安裝 hello 資料庫執行個體</span><span class="sxs-lookup"><span data-stu-id="a12ef-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="a12ef-1004">tooinstall hello 資料庫執行個體，請遵循 hello hello SAP 安裝文件中所述的程序。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="a12ef-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>安裝第二個叢集節點 hello</span><span class="sxs-lookup"><span data-stu-id="a12ef-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="a12ef-1006">tooinstall hello 第二個叢集，遵循 hello hello SAP 安裝指南 》 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="a12ef-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>變更 hello hello SAP 端 Windows 服務執行個體的啟動類型</span><span class="sxs-lookup"><span data-stu-id="a12ef-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="a12ef-1008">太變更 hello hello SAP 端 Windows 服務啟動類型**自動 （延遲開始）**兩個叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![圖 60： 變更 hello SAP 端執行個體 toodelayed 自動 hello 服務類型][sap-ha-guide-figure-3050]

<span data-ttu-id="a12ef-1010">_**圖 60:**變更 hello SAP 端執行個體 toodelayed 自動 hello 服務類型_</span><span class="sxs-lookup"><span data-stu-id="a12ef-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="a12ef-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>安裝 hello SAP 主應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="a12ef-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="a12ef-1012">安裝 hello 主應用程式伺服器 (PAS) 執行個體 <*SID*>-di-0 hello 所指定的虛擬機器上 toohost hello PA。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="a12ef-1013">Azure 或 DataKeeper 特定的設定沒有相依性。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="a12ef-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>安裝 hello SAP 其他應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="a12ef-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="a12ef-1015">所有 hello 虛擬機器，您已指定 toohost SAP 應用程式伺服器執行個體上安裝 SAP 其他應用程式伺服器 (AAS)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="a12ef-1016">例如，在 <*SID*>-di-1 太 <*SID*>-di-&lt;n&gt;。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ef-1017">這樣就完成 hello 安裝高可用性的 SAP NetWeaver 系統。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="a12ef-1018">接下來，繼續進行容錯移轉測試。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="a12ef-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>測試 hello SAP ASCS/SCS 執行個體容錯移轉和 SIOS 複寫</span><span class="sxs-lookup"><span data-stu-id="a12ef-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="a12ef-1020">它是簡單 tootest，並使用容錯移轉叢集管理員 」 和 「 hello SIOS DataKeeper 管理和組態工具來監視 SAP ASCS/SCS 執行個體容錯移轉和 SIOS 磁碟複寫。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="a12ef-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS 執行個體在叢集節點 A 上執行</span><span class="sxs-lookup"><span data-stu-id="a12ef-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="a12ef-1022">hello **SAP PR1**叢集節點 a 上執行叢集群組例如，在**pr1 ascs 0**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="a12ef-1023">指派 hello 共用磁碟機 S，屬於的 hello **SAP PR1**叢集群組，以及哪些 hello ASCS/SCS 執行個體使用，toocluster 節點 a。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![圖 61： 容錯移轉叢集管理員： hello SAP < SID > 叢集群組在叢集節點 A 上執行][sap-ha-guide-figure-5000]

<span data-ttu-id="a12ef-1025">_**圖 61:**容錯移轉叢集管理員： hello SAP <*SID*> 叢集節點 A 上執行叢集群組_</span><span class="sxs-lookup"><span data-stu-id="a12ef-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="a12ef-1026">在 hello SIOS DataKeeper 管理和組態工具，您可以看到資料以同步方式從 hello 來源磁碟區磁碟機 S 叢集節點 toohello 目標磁碟區上的磁碟機 S 叢集節點 b 上覆寫該 hello 共用的磁碟例如，從複寫**pr1 ascs 0 [10.0.0.40]**太**pr1 ascs 1 [10.0.0.41]**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![圖 62： 在 SIOS DataKeeper 複製 hello 本機磁碟區從叢集節點的 toocluster 節點 B][sap-ha-guide-figure-5001]

<span data-ttu-id="a12ef-1028">_**圖 62:** SIOS DataKeeper 複寫 hello 本機磁碟區從叢集節點的 toocluster 節點 B_</span><span class="sxs-lookup"><span data-stu-id="a12ef-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="a12ef-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>從節點 A toonode B 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="a12ef-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="a12ef-1030">選擇其中一個這些選項 tooinitiate hello SAP 的容錯移轉 <*SID*> 叢集群組從叢集節點 A toocluster 節點 b:</span><span class="sxs-lookup"><span data-stu-id="a12ef-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="a12ef-1031">使用容錯移轉叢集管理員</span><span class="sxs-lookup"><span data-stu-id="a12ef-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="a12ef-1032">使用容錯移轉叢集 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a12ef-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="a12ef-1033">重新啟動叢集節點的 hello Windows 客體作業系統內 (這會起始自動容錯移轉的 hello SAP <*SID*> 叢集群組從節點 A toonode B)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="a12ef-1034">重新啟動叢集節點 A 從 hello Azure 入口網站 (這會起始自動容錯移轉的 hello SAP <*SID*> 叢集群組從節點 A toonode B)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="a12ef-1035">使用 Azure PowerShell 來重新啟動叢集節點 A (這會起始自動容錯移轉的 hello SAP <*SID*> 叢集群組從節點 A toonode B)。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="a12ef-1036">容錯移轉之後，hello SAP <*SID*> 叢集節點 b 上執行叢集群組例如，在上執行**pr1 ascs 1**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![圖 63： 在容錯移轉叢集管理員中，hello SAP < SID > 叢集群組節點上執行叢集 B][sap-ha-guide-figure-5002]

  <span data-ttu-id="a12ef-1038">_**圖 63**： 在容錯移轉叢集管理員 hello SAP <*SID*> 叢集節點 B 上執行叢集群組_</span><span class="sxs-lookup"><span data-stu-id="a12ef-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="a12ef-1039">hello 共用的磁碟現在裝載在叢集節點 B SIOS DataKeeper 從來源磁碟區磁碟機 S 叢集節點 B tootarget 磁碟區磁碟機 S 上的叢集節點 a 上複寫的資料例如，從複寫**pr1 ascs 1 [10.0.0.41]**太**pr1 ascs 0 [10.0.0.40]**。</span><span class="sxs-lookup"><span data-stu-id="a12ef-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![圖 64: SIOS DataKeeper 複寫 hello 本機磁碟區的叢集節點 B toocluster 節點 A][sap-ha-guide-figure-5003]

  <span data-ttu-id="a12ef-1041">_**圖 64:** SIOS DataKeeper 從叢集節點 B toocluster 節點 A 複寫 hello 本機磁碟區_</span><span class="sxs-lookup"><span data-stu-id="a12ef-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
