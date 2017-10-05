---
title: "SAP NetWeaver 的 Azure 虛擬機器高可用性 | Microsoft Docs"
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
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d00db895ffcf9ba9a51e3df2dae5d33c0277dd6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="5ff84-103">SAP NetWeaver 的 Azure 虛擬機器高可用性</span><span class="sxs-lookup"><span data-stu-id="5ff84-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="5ff84-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="5ff84-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="5ff84-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="5ff84-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="5ff84-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="5ff84-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="5ff84-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="5ff84-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="5ff84-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="5ff84-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="5ff84-109">對於需要在最短的時間內處理計算、儲存和網路資源，而不需要漫長的採購週期的組織而言，「Azure 虛擬機器」是適用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5ff84-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="5ff84-110">您可以使用「Azure 虛擬機器」以部署傳統的應用程式，例如 SAP NetWeaver 架構 ABAP、Java，以及 ABAP+Java 堆疊。</span><span class="sxs-lookup"><span data-stu-id="5ff84-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="5ff84-111">擴充的可靠性與可用性，無須其他內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="5ff84-112">「Azure 虛擬機器」支援跨單位連線能力，貴公司可將「Azure 虛擬機器」整合到其內部部署網域、私人雲端，以及 SAP 系統環境中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="5ff84-113">在本文中，我們將探討使用 Azure Resource Manager 部署模型，在 Azure 中部署高可用性 SAP 系統時可採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="5ff84-114">我們會引導您完成這些主要工作：</span><span class="sxs-lookup"><span data-stu-id="5ff84-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="5ff84-115">尋找正確的 SAP 附註和安裝指南 (在[資源][sap-ha-guide-2]一節中列出)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="5ff84-116">本文補充 SAP 安裝文件及 SAP 附註，其為有助於在特定平台上安裝及部署 SAP 軟體的主要資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="5ff84-117">了解 Azure Resource Manager 部署模型與 Azure 傳統部署模型之間的差異。</span><span class="sxs-lookup"><span data-stu-id="5ff84-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="5ff84-118">了解「Windows Server 容錯移轉叢集」仲裁模式，以便選取適合您 Azure 部署的模型。</span><span class="sxs-lookup"><span data-stu-id="5ff84-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="5ff84-119">了解 Azure 服務中的「Windows Server 容錯移轉叢集」共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="5ff84-120">了解如何在 Azure 中協助保護單一失敗點元件，例如進階商業應用程式程式設計 (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) 和資料庫管理系統 (DBMS)，以及備援元件，例如 SAP 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="5ff84-121">藉由使用 Azure Resource Manager，遵循在 Windows Server 容錯移轉叢集的叢集中安裝及設定高可用性 SAP 系統的逐步說明範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="5ff84-122">深入了解在 Azure 中使用 Windows Server 容錯移轉叢集所需的步驟，但內部部署不需要這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="5ff84-123">為了簡化部署和設定，在本文中，我們使用新的 SAP 三層式高可用性 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="5ff84-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="5ff84-124">此範本自動部署高可用性 SAP 系統所需的整個基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5ff84-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="5ff84-125">基礎結構也支援 SAP 應用程式效能標準 (SAPS) 調整您 SAP 系統的大小。</span><span class="sxs-lookup"><span data-stu-id="5ff84-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="5ff84-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> 必要條件</span><span class="sxs-lookup"><span data-stu-id="5ff84-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="5ff84-127">開始之前，請確定符合下列各節所述的必要條件。</span><span class="sxs-lookup"><span data-stu-id="5ff84-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="5ff84-128">此外，請務必檢查[資源][sap-ha-guide-2]一節中列出的所有資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="5ff84-129">在本文中，我們針對[使用受控磁碟的三層式 SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/) 使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="5ff84-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="5ff84-130">如需範本的實用概觀，請參閱 [SAP Azure Resource Manager 範本](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="5ff84-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> 資源</span><span class="sxs-lookup"><span data-stu-id="5ff84-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="5ff84-132">這些文章涵蓋 Azure 中的 SAP 部署：</span><span class="sxs-lookup"><span data-stu-id="5ff84-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="5ff84-133">[SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="5ff84-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="5ff84-134">[SAP NetWeaver 的 Azure 虛擬機器部署][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="5ff84-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="5ff84-135">[SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="5ff84-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="5ff84-136">[SAP NetWeaver 的 Azure 虛擬機器高可用性 (本指南)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="5ff84-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-137">文件中會儘可能提供所參考 SAP 安裝指南的連結 (請參閱 [SAP 安裝指南][sap-installation-guides])。</span><span class="sxs-lookup"><span data-stu-id="5ff84-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="5ff84-138">如需安裝程序的必要條件和相關資訊，建議您詳細閱讀 SAP NetWeaver 安裝指南。</span><span class="sxs-lookup"><span data-stu-id="5ff84-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="5ff84-139">本文僅涵蓋可與 Azure 虛擬機器搭配使用之 SAP NetWeaver 架構系統的特定工作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="5ff84-140">下列 SAP 附註與 Azure 上的 SAP 主題相關：</span><span class="sxs-lookup"><span data-stu-id="5ff84-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="5ff84-141">附註編號</span><span class="sxs-lookup"><span data-stu-id="5ff84-141">Note number</span></span> | <span data-ttu-id="5ff84-142">課程名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="5ff84-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="5ff84-143">[1928533]</span></span> |<span data-ttu-id="5ff84-144">Azure 上的 SAP 應用程式︰支援的產品和大小</span><span class="sxs-lookup"><span data-stu-id="5ff84-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="5ff84-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="5ff84-145">[2015553]</span></span> |<span data-ttu-id="5ff84-146">Microsoft Azure 上的 SAP：支援的必要條件</span><span class="sxs-lookup"><span data-stu-id="5ff84-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="5ff84-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="5ff84-147">[1999351]</span></span> |<span data-ttu-id="5ff84-148">適用於 SAP 的增強型 Azure 監視功能</span><span class="sxs-lookup"><span data-stu-id="5ff84-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="5ff84-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="5ff84-149">[2178632]</span></span> |<span data-ttu-id="5ff84-150">Microsoft Azure 上的 SAP 主要監視度量</span><span class="sxs-lookup"><span data-stu-id="5ff84-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="5ff84-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="5ff84-151">[1999351]</span></span> |<span data-ttu-id="5ff84-152">Windows 上的虛擬化︰增強型監視功能</span><span class="sxs-lookup"><span data-stu-id="5ff84-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="5ff84-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="5ff84-153">[2243692]</span></span> |<span data-ttu-id="5ff84-154">針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體</span><span class="sxs-lookup"><span data-stu-id="5ff84-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="5ff84-155">深入了解 [Azure 訂用帳戶限制][azure-subscription-service-limits-subscription]，包含一般預設限制與最大限制。</span><span class="sxs-lookup"><span data-stu-id="5ff84-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="5ff84-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>使用 Azure Resource Manager 的高可用性 SAP 與 Azure 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="5ff84-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="5ff84-157">Azure Resource Manager 與 Azure 傳統部署模型在下列方面有所不同：</span><span class="sxs-lookup"><span data-stu-id="5ff84-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="5ff84-158">資源群組</span><span class="sxs-lookup"><span data-stu-id="5ff84-158">Resource groups</span></span>
- <span data-ttu-id="5ff84-159">Azure 資源群組上的 Azure 內部負載平衡器相依性</span><span class="sxs-lookup"><span data-stu-id="5ff84-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="5ff84-160">支援 SAP 多 SID 案例</span><span class="sxs-lookup"><span data-stu-id="5ff84-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="5ff84-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> 資源群組</span><span class="sxs-lookup"><span data-stu-id="5ff84-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="5ff84-162">在 Azure Resource Manager 中，您可以使用資源群組來管理 Azure 訂用帳戶中的所有應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="5ff84-163">利用整合式的方法，在資源群組中，所有資源都有相同的生命週期。</span><span class="sxs-lookup"><span data-stu-id="5ff84-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="5ff84-164">例如，所有資源會同時建立，並且同時刪除。</span><span class="sxs-lookup"><span data-stu-id="5ff84-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="5ff84-165">深入了解[資源群組](../../../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="5ff84-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure 資源群組上的 Azure 內部負載平衡器相依性</span><span class="sxs-lookup"><span data-stu-id="5ff84-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="5ff84-167">在 Azure 傳統部署模型中，Azure 內部負載平衡器 (Azure Load Balancer 服務) 和雲端服務之間具有相依性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service.</span></span> <span data-ttu-id="5ff84-168">每個內部負載平衡器需要一個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5ff84-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="5ff84-169">在 Azure Resource Manager 中，每個 Azure 資源都需要放進 Azure 資源群組中，而這對 Azure Load Balancer 也有效。</span><span class="sxs-lookup"><span data-stu-id="5ff84-169">In Azure Resource Manager, every Azure resource needs to be placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="5ff84-170">不過，不需要讓每個 Azure Load Balancer 都有一個 Azure 資源群組，例如，一個 Azure 資源群組可以包含多個 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="5ff84-170">However, there is no need to have one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="5ff84-171">環境更簡單且更有彈性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-171">The environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="5ff84-172">支援 SAP 多 SID 案例</span><span class="sxs-lookup"><span data-stu-id="5ff84-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="5ff84-173">在 Azure Resource Manager 中，您可以在一個叢集中安裝多個 SAP 系統識別碼 (SID) ASCS/SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="5ff84-174">因為每個 Azure 內部負載平衡器的多個 IP 位址支援，可能有多重 SID 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="5ff84-175">若要使用 Azure 傳統部署模型，請依照 [Azure 上的 SAP NetWeaver：在 Azure 上使用 Windows Server 容錯移轉叢集搭配 SIOS DataKeeper 將 SAP ASCS/SCS 執行個體組成叢集](http://go.microsoft.com/fwlink/?LinkId=613056)中所述的步驟操作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-175">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ff84-176">強烈建議您針對 SAP 安裝使用 Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="5ff84-176">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="5ff84-177">它提供傳統部署模型所沒有的許多好處。</span><span class="sxs-lookup"><span data-stu-id="5ff84-177">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="5ff84-178">進一步了解 Azure [部署模型][virtual-machines-azure-resource-manager-architecture-benefits-arm]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="5ff84-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="5ff84-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="5ff84-180">Windows Server 容錯移轉叢集是 Windows 中高可用性 SAP ASCS/SCS 安裝和 DBMS 的基礎。</span><span class="sxs-lookup"><span data-stu-id="5ff84-180">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="5ff84-181">容錯移轉叢集是由 1+n 個獨立伺服器 (節點) 所組成的群組，這些伺服器會共同運作以提升應用程式和服務的可用性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-181">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="5ff84-182">如果發生節點失敗，Windows Server 容錯移轉叢集會計算發生的失敗次數，同時維護狀況良好的叢集，以提供應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="5ff84-182">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="5ff84-183">您可以從不同的仲裁模式選擇以達成容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-183">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="5ff84-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> 仲裁模式</span><span class="sxs-lookup"><span data-stu-id="5ff84-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="5ff84-185">當您使用 Windows Server 容錯移轉叢集時，可以從四種仲裁模式中選擇：</span><span class="sxs-lookup"><span data-stu-id="5ff84-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="5ff84-186">**節點多數**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-186">**Node Majority**.</span></span> <span data-ttu-id="5ff84-187">叢集的每個節點皆可投票。</span><span class="sxs-lookup"><span data-stu-id="5ff84-187">Each node of the cluster can vote.</span></span> <span data-ttu-id="5ff84-188">只有取得多數票 (也就是票數過半) 時，叢集才能運作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-188">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5ff84-189">我們建議針對節點數目為奇數的叢集使用此選項。</span><span class="sxs-lookup"><span data-stu-id="5ff84-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="5ff84-190">例如，具有七個節點的叢集中有三個節點可能會失敗，而叢集仍會達成多數並繼續執行。</span><span class="sxs-lookup"><span data-stu-id="5ff84-190">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="5ff84-191">**節點與磁碟多數**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="5ff84-192">每個節點和叢集儲存體中的指定磁碟 (磁碟見證) 處於可用且通訊中狀態時，都可投票。</span><span class="sxs-lookup"><span data-stu-id="5ff84-192">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="5ff84-193">只有取得多數票 (也就是票數過半) 時，叢集才能運作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-193">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5ff84-194">此模式適用於節點數目為偶數的叢集環境。</span><span class="sxs-lookup"><span data-stu-id="5ff84-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="5ff84-195">如果半數的節點和該磁碟在線上，叢集就會維持狀況良好的狀態。</span><span class="sxs-lookup"><span data-stu-id="5ff84-195">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="5ff84-196">**節點與檔案共用多數**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="5ff84-197">每個節點再加上一個由系統管理員所建立的指定檔案共用 (檔案共用見證) 無論節點和檔案共用是否處於可用且通訊中狀態，皆可投票。</span><span class="sxs-lookup"><span data-stu-id="5ff84-197">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="5ff84-198">只有取得多數票 (也就是票數過半) 時，叢集才能運作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-198">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5ff84-199">此模式適用於節點數目為偶數的叢集環境。</span><span class="sxs-lookup"><span data-stu-id="5ff84-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="5ff84-200">類似於「節點與磁碟多數」模式，但它使用見證檔案共享，而不是見證磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-200">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="5ff84-201">此模式很容易實作，但如果檔案共用本身不具有高可用性，它可能會變成單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-201">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="5ff84-202">**無多數：僅磁碟**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="5ff84-203">只要有一個節點可用且正與叢集儲存體中的特定磁碟進行通訊，叢集就會擁有仲裁。</span><span class="sxs-lookup"><span data-stu-id="5ff84-203">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="5ff84-204">只有也在與該磁碟進行通訊的節點能夠加入叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-204">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="5ff84-205">建議您不要使用此模式。</span><span class="sxs-lookup"><span data-stu-id="5ff84-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="5ff84-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server 容錯移轉叢集內部部署</span><span class="sxs-lookup"><span data-stu-id="5ff84-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="5ff84-207">圖 1 顯示兩個節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="5ff84-208">如果節點之間的網路連線失敗，而且兩個節點仍保持運作，仲裁磁碟或檔案共用會決定哪一個節點將繼續提供叢集的應用程式與服務。</span><span class="sxs-lookup"><span data-stu-id="5ff84-208">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="5ff84-209">能夠存取仲裁磁碟或檔案共用的節點就是可以確保服務可繼續的節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-209">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="5ff84-210">因為此範例使用雙節點叢集，所以我們使用「節點與檔案共用多數」仲裁模式。</span><span class="sxs-lookup"><span data-stu-id="5ff84-210">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="5ff84-211">「節點與磁碟多數」也是有效的選項。</span><span class="sxs-lookup"><span data-stu-id="5ff84-211">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="5ff84-212">在生產環境中，建議您使用仲裁磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="5ff84-213">您可以使用網路和儲存體系統技術，使其成為高可用性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-213">You can use network and storage system technology to make it highly available.</span></span>

![圖 1：Azure 中 SAP ASCS/SCS 之 Windows Server 容錯移轉叢集組態的範例][sap-ha-guide-figure-1000]

<span data-ttu-id="5ff84-215">_**圖 1：**Azure 中 SAP ASCS/SCS 之 Windows Server 容錯移轉叢集組態的範例_</span><span class="sxs-lookup"><span data-stu-id="5ff84-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="5ff84-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> 共用儲存體</span><span class="sxs-lookup"><span data-stu-id="5ff84-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="5ff84-217">圖 1 也顯示兩個節點的共用儲存體叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="5ff84-218">在內部部署共用儲存體叢集中，叢集中的所有節點會偵測共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-218">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="5ff84-219">鎖定機制可防止資料損毀。</span><span class="sxs-lookup"><span data-stu-id="5ff84-219">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="5ff84-220">所有節點也可以偵測到另一個節點是否發生失敗。</span><span class="sxs-lookup"><span data-stu-id="5ff84-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="5ff84-221">如果一個節點發生失敗，剩餘的節點就會取得儲存體資源的擁有權並確保服務的可用性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-221">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-222">您不需要與某些 DBMS 應用程式 (例如 SQL Server) 共用提供高可用性的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="5ff84-223">SQL Server Always On 會將 DBMS 資料及記錄檔，從一個叢集節點的本機磁碟複寫到另一個叢集節點的本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-223">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="5ff84-224">在此情況下，Windows 叢集組態不需要共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-224">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="5ff84-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> 網路與名稱解析</span><span class="sxs-lookup"><span data-stu-id="5ff84-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="5ff84-226">用戶端電腦可透過 DNS 伺服器提供的虛擬 IP 位址和虛擬主機名稱連線叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-226">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="5ff84-227">內部部署節點與 DNS 伺服器可以處理多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-227">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="5ff84-228">在一般設定中，您會使用兩個或更多個網路連線：</span><span class="sxs-lookup"><span data-stu-id="5ff84-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="5ff84-229">一個連接到儲存體的專用連線</span><span class="sxs-lookup"><span data-stu-id="5ff84-229">A dedicated connection to the storage</span></span>
* <span data-ttu-id="5ff84-230">一個用於活動訊號的叢集內部網路連線</span><span class="sxs-lookup"><span data-stu-id="5ff84-230">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="5ff84-231">一個供用戶端用來連線到叢集的公用網路</span><span class="sxs-lookup"><span data-stu-id="5ff84-231">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="5ff84-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Azure 中的 Windows Server 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="5ff84-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="5ff84-233">相較於裸機或私人雲端部署，「Azure 虛擬機器」需要額外的步驟來設定 Windows Server 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-233">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="5ff84-234">當您建置共用叢集磁碟時，需要為 SAP ASCS/SCS 執行個體設定數個 IP 位址和虛擬的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5ff84-234">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="5ff84-235">在本文中，我們會討論在 Azure 中建置 SAP 高可用性中心服務叢集時所需要的重要概念與其他步驟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-235">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="5ff84-236">我們會為您示範如何設定協力廠商工具 SIOS DataKeeper，以及如何設定 Azure 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-236">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="5ff84-237">您可以使用這些工具，在 Azure 中透過檔案共用見證建立 Windows 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-237">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![圖 2：Azure 中沒有共用磁碟的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1001]

<span data-ttu-id="5ff84-239">_**圖 2：**Azure 中沒有共用磁碟的 Windows Server 容錯移轉叢集組態_</span><span class="sxs-lookup"><span data-stu-id="5ff84-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="5ff84-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> 使用 SIOS DataKeeper 在 Azure 中共用磁碟</span><span class="sxs-lookup"><span data-stu-id="5ff84-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="5ff84-241">您需要針對高可用性的 SAP ASCS/SCS 執行個體叢集共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5ff84-242">自 2016 年 9 月起，Azure 即不再提供可用於建立共用儲存體叢集的共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-242">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="5ff84-243">您可以使用協力廠商軟體 SIOS DataKeeper Cluster Edition 以建立鏡像儲存體，以模擬叢集共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-243">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="5ff84-244">SIOS 解決方案提供即時同步的資料複寫。</span><span class="sxs-lookup"><span data-stu-id="5ff84-244">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="5ff84-245">可以為叢集建立共用磁碟資源的方式為：</span><span class="sxs-lookup"><span data-stu-id="5ff84-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="5ff84-246">將額外的磁碟連接到 Windows 叢集組態中的每個虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-246">Attach an additional disk to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="5ff84-247">在兩個虛擬機器節點上執行 SIOS DataKeeper Cluster Edition。</span><span class="sxs-lookup"><span data-stu-id="5ff84-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="5ff84-248">設定 SIOS DataKeeper Cluster Edition，使它將來源虛擬機器的額外磁碟連接磁碟區內容鏡像至目標虛擬機器的額外磁碟連接磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ff84-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional disk attached volume from the source virtual machine to the additional disk attached volume of the target virtual machine.</span></span> <span data-ttu-id="5ff84-249">SIOS DataKeeper 會提取來源和目標本機磁碟區，並將它們當作一個共用磁碟來呈現給「Windows Server 容錯移轉叢集」。</span><span class="sxs-lookup"><span data-stu-id="5ff84-249">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="5ff84-250">取得 [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5ff84-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![圖 3：Azure 中使用 SIOS DataKeeper 的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1002]

<span data-ttu-id="5ff84-252">_**圖 3：**Azure 中使用 SIOS DataKeeper 的 Windows Server 容錯移轉叢集組態_</span><span class="sxs-lookup"><span data-stu-id="5ff84-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-253">您不需要與某些 DBMS 產品 (例如 SQL Server) 共用提供高可用性的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="5ff84-254">SQL Server Always On 會將 DBMS 資料及記錄檔，從一個叢集節點的本機磁碟複寫到另一個叢集節點的本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-254">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="5ff84-255">在此情況下，Windows 叢集組態不需要共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-255">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="5ff84-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Azure 中的名稱解析</span><span class="sxs-lookup"><span data-stu-id="5ff84-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="5ff84-257">Azure 雲端平台不提供設定虛擬 IP 位址的選項，例如浮動 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-257">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="5ff84-258">您需要一個替代解決方案來設定虛擬 IP，以便連線到雲端的叢集資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-258">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="5ff84-259">Azure 具有 Azure Load Balancer 服務中的內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-259">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="5ff84-260">使用內部負載平衡器，用戶端可透過叢集虛擬 IP 位址連線叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-260">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="5ff84-261">您需要將內部負載平衡器部署在包含叢集節點的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-261">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="5ff84-262">接著，使用內部負載平衡器的探查連接埠來設定所有必要的連接埠轉送規則。</span><span class="sxs-lookup"><span data-stu-id="5ff84-262">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="5ff84-263">用戶端可以透過虛擬主機名稱來進行連線。</span><span class="sxs-lookup"><span data-stu-id="5ff84-263">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="5ff84-264">DNS 伺服器會解析叢集 IP 位址，而內部負載平衡器則會處理對作用中叢集節點的轉送。</span><span class="sxs-lookup"><span data-stu-id="5ff84-264">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="5ff84-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Azure 基礎結構即服務 (IaaS) 中的 SAP NetWeaver 高可用性</span><span class="sxs-lookup"><span data-stu-id="5ff84-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="5ff84-266">若要達成 SAP 應用程式高可用性，例如 SAP 軟體元件，您需要保護下列元件：</span><span class="sxs-lookup"><span data-stu-id="5ff84-266">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="5ff84-267">SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-267">SAP Application Server instance</span></span>
* <span data-ttu-id="5ff84-268">SAP ASCS/SCS 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="5ff84-269">DBMS 伺服器</span><span class="sxs-lookup"><span data-stu-id="5ff84-269">DBMS server</span></span>

<span data-ttu-id="5ff84-270">如需在高可用性案例中保護 SAP 元件的詳細資訊，請參閱 [SAP NetWeaverAzure 的虛擬機器規劃和實作][planning-guide-11]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="5ff84-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> 高可用性的 SAP 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="5ff84-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="5ff84-272">對於 SAP 應用程式伺服器和對話方塊執行個體，您通常不需要特定的高可用性解決方案。</span><span class="sxs-lookup"><span data-stu-id="5ff84-272">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="5ff84-273">您可以透過備援來達成高可用性，而且您會在 Azure 虛擬機器之不同的執行個體中，設定多個對話方塊執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="5ff84-274">您應該至少要有兩個 SAP 應用程式執行個體安裝在 Azure 虛擬機器的兩個執行個體中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![圖 4：高可用性的 SAP 應用程式伺服器][sap-ha-guide-figure-2000]

<span data-ttu-id="5ff84-276">_**圖 4：**高可用性的 SAP 應用程式伺服器_</span><span class="sxs-lookup"><span data-stu-id="5ff84-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="5ff84-277">所有裝載 SAP 應用程式伺服器執行個體的虛擬機器都必須放置在同一個 Azure 可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-277">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="5ff84-278">Azure 可用性設定組可確保：</span><span class="sxs-lookup"><span data-stu-id="5ff84-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="5ff84-279">所有虛擬機器都是相同升級網域的一部分。</span><span class="sxs-lookup"><span data-stu-id="5ff84-279">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="5ff84-280">例如，升級網域可確保虛擬機器不會在計劃性維護停機期間同時更新。</span><span class="sxs-lookup"><span data-stu-id="5ff84-280">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="5ff84-281">所有虛擬機器都是相同容錯網域的一部分。</span><span class="sxs-lookup"><span data-stu-id="5ff84-281">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="5ff84-282">例如，容錯網域可確保部署虛擬機器，以便不會有任何單一失敗點影響所有虛擬機器的可用性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="5ff84-283">深入了解如何[管理虛擬機器的可用性][virtual-machines-manage-availability]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-283">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="5ff84-284">僅限非受控的磁碟：由於 Azure 儲存體帳戶是潛在的單一失敗點，因此您務必擁有至少兩個 Azure 儲存體帳戶，且至少要將兩個虛擬機器分散到其中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-284">Unmanaged disk only: Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="5ff84-285">在理想的設定中，執行 SAP 對話方塊執行個體的每一個虛擬機器磁碟會部署在不同的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-285">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="5ff84-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> 高可用性的 SAP ASCS/SCS 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="5ff84-287">圖 5 是高可用性的 SAP ASCS/SCS 執行個體範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![圖 5：高可用性的 SAP ASCS/SCS 執行個體][sap-ha-guide-figure-2001]

<span data-ttu-id="5ff84-289">_**圖 5：**高可用性的 SAP ASCS/SCS 執行個體_</span><span class="sxs-lookup"><span data-stu-id="5ff84-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="5ff84-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> 在 Azuer 中使用 Windows Server 容錯移轉叢集的 SAP ASCS/SCS 執行個體高可用性</span><span class="sxs-lookup"><span data-stu-id="5ff84-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="5ff84-291">相較於裸機或私人雲端部署，「Azure 虛擬機器」需要額外的步驟來設定 Windows Server 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-291">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="5ff84-292">為了建置 Windows 容錯移轉叢集，您需要一個共用叢集磁碟、數個 IP 位址、數個虛擬主機名稱，以及 Azure 內部負載平衡器，來將 SAP ASCS/SCS 執行個體組成叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-292">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5ff84-293">本文稍後會有詳細討論。</span><span class="sxs-lookup"><span data-stu-id="5ff84-293">We discuss this in more detail later in the article.</span></span>

![圖 6：Azure 中使用 SIOS DataKeeper 之 SAP ASCS/SCS 的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1002]

<span data-ttu-id="5ff84-295">_**圖 6：**Azure 中使用 SIOS DataKeeper 之 SAP ASCS/SCS 的 Windows Server 容錯移轉叢集組態_</span><span class="sxs-lookup"><span data-stu-id="5ff84-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="5ff84-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> 高可用性的 DBMS 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="5ff84-297">DBMS 也是 SAP 系統的單一連絡點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-297">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="5ff84-298">您需要使用高可用性的解決方案來保護它。</span><span class="sxs-lookup"><span data-stu-id="5ff84-298">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="5ff84-299">圖 7 顯示在 Azure 中使用 Windows Server 容錯移轉叢集和 Azure 內部負載平衡器的 SQL Server Always On 高可用性解決方案的範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="5ff84-300">SQL Server Always On 會使用自己的 DBMS 複寫來複寫 DBMS 資料和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5ff84-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="5ff84-301">在此情況下，您不需要叢集共用磁碟，以簡化整個設定。</span><span class="sxs-lookup"><span data-stu-id="5ff84-301">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![圖 7：高可用性的 SAP DBMS，使用 SQL Server Always On 的範例][sap-ha-guide-figure-2003]

<span data-ttu-id="5ff84-303">_**圖 7：**高可用性的 SAP DBMS，使用 SQL Server Always On 的範例_</span><span class="sxs-lookup"><span data-stu-id="5ff84-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="5ff84-304">如需有關使用 Azure Resource Manager 部署模型在 Azure 中將 SQL Server 組成叢集的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="5ff84-304">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="5ff84-305">[用 Resource Manager 在 Azure 虛擬機器中設定 Always On 可用性群組][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="5ff84-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="5ff84-306">[在 Azure 中為 Always On 可用性群組設訂內部負載平衡器][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="5ff84-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="5ff84-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> 端對端高可用性部署案例</span><span class="sxs-lookup"><span data-stu-id="5ff84-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="5ff84-308">使用架構範本 1 的部署案例</span><span class="sxs-lookup"><span data-stu-id="5ff84-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="5ff84-309">圖 8 顯示**一個** SAP 系統在 Azure 中 SAP NetWeaver 高可用性架構的範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="5ff84-310">此案例如下所示設定︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5ff84-311">一個專用的叢集用於 SAP ASCS/SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-311">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="5ff84-312">一個專用的叢集用於 DBMS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-312">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="5ff84-313">SAP 應用程式伺服器執行個體會部署在他們自己專用的 VM。</span><span class="sxs-lookup"><span data-stu-id="5ff84-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![圖 8：SAP 高可用性架構範本 1，包含用於 ASCS/SCS 和用於 DBMS 執行個體的專用叢集][sap-ha-guide-figure-2004]

<span data-ttu-id="5ff84-315">_**圖 8：**SAP 高可用性架構範本 1，包含用於 ASCS/SCS 和用於 DBMS 執行個體的專用叢集_</span><span class="sxs-lookup"><span data-stu-id="5ff84-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="5ff84-316">使用架構範本 2 的部署案例</span><span class="sxs-lookup"><span data-stu-id="5ff84-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="5ff84-317">圖 9 顯示**一個** SAP 系統在 Azure 中 SAP NetWeaver 高可用性架構的範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="5ff84-318">此案例如下所示設定︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5ff84-319">一個專用的叢集用於 SAP ASCS/SCS 和 DBMS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-319">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="5ff84-320">SAP 應用程式伺服器執行個體會部署在自己專用的 VM。</span><span class="sxs-lookup"><span data-stu-id="5ff84-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![圖 9：SAP 高可用性架構範本 2，包含用於 ASCS/SCS 的專用叢集和用於 DBMS 的專用叢集][sap-ha-guide-figure-2005]

<span data-ttu-id="5ff84-322">_**圖 9：**SAP 高可用性架構範本 2，包含用於 ASCS/SCS 的專用叢集和用於 DBMS 的專用叢集_</span><span class="sxs-lookup"><span data-stu-id="5ff84-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="5ff84-323">使用架構範本 3 的部署案例</span><span class="sxs-lookup"><span data-stu-id="5ff84-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="5ff84-324">圖 10 顯示**兩個** SAP 系統與 &lt;SID1&gt; 和 &lt;SID2&gt;，在 Azure 中 SAP NetWeaver 高可用性架構的範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="5ff84-325">此案例如下所示設定︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5ff84-326">一個專用的叢集用於 SAP ASCS/SCS SID1 執行個體和 SAP ASCS/SCS SID2 執行個體 (一個叢集)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-326">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="5ff84-327">一個專用的叢集用於 DBMS SID1，另一個專用的叢集用於 DBMS SID2 (兩個叢集)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="5ff84-328">SAP 系統 SID1 的 SAP 應用程式伺服器執行個體有自己專用的 VM。</span><span class="sxs-lookup"><span data-stu-id="5ff84-328">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="5ff84-329">SAP 系統 SID2 的 SAP 應用程式伺服器執行個體有自己專用的 VM。</span><span class="sxs-lookup"><span data-stu-id="5ff84-329">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![圖 10：SAP 高可用性架構範本 3，包含用於不同 ASCS/SCS 執行個體的專用叢集][sap-ha-guide-figure-6003]

<span data-ttu-id="5ff84-331">_**圖 10：**SAP 高可用性架構範本 3，包含用於不同 ASCS/SCS 執行個體的專用叢集_</span><span class="sxs-lookup"><span data-stu-id="5ff84-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="5ff84-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> 準備基礎架構</span><span class="sxs-lookup"><span data-stu-id="5ff84-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="5ff84-333">準備架構範本 1 的基礎結構</span><span class="sxs-lookup"><span data-stu-id="5ff84-333">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="5ff84-334">適用於 SAP 的 Azure Resource Manager 範本有助於簡化部署所需的資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="5ff84-335">Azure Resource Manager 中的三層式範本也支援高可用性案例，例如架構範本 1，有兩個叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-335">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="5ff84-336">每個叢集是適用於 SAP ASCS/SCS 和 DBMS 的 SAP 單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="5ff84-337">以下是可取得我們在本文中說明之範例案例的 Azure Resource Manager 範本︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-337">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="5ff84-338">Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="5ff84-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* <span data-ttu-id="5ff84-339">[使用受控磁碟的 Azure Marketplace 映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="5ff84-339">[Azure Marketplace image using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)</span></span>  
* [<span data-ttu-id="5ff84-340">自訂映像</span><span class="sxs-lookup"><span data-stu-id="5ff84-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* <span data-ttu-id="5ff84-341">[使用受控磁碟的自訂映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="5ff84-341">[Custom image using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)</span></span>

<span data-ttu-id="5ff84-342">若要準備架構範本 1 的基礎結構：</span><span class="sxs-lookup"><span data-stu-id="5ff84-342">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="5ff84-343">在 Azure 入口網站中，在 [參數] 刀鋒視窗的 [SYSTEMAVAILABILITY] 方塊中，選取 [HA]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-343">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![圖 11：設定 SAP 高可用性 Azure Resource Manager 參數][sap-ha-guide-figure-3000]

<span data-ttu-id="5ff84-345">_**圖 11：**設定 SAP 高可用性 Azure Resource Manager 參數_</span><span class="sxs-lookup"><span data-stu-id="5ff84-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="5ff84-346">範本會建立：</span><span class="sxs-lookup"><span data-stu-id="5ff84-346">The templates create:</span></span>

  * <span data-ttu-id="5ff84-347">**虛擬機器**：</span><span class="sxs-lookup"><span data-stu-id="5ff84-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="5ff84-348">SAP 應用程式伺服器虛擬機器︰<*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5ff84-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="5ff84-349">ASCS/SCS 叢集虛擬機器︰<*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5ff84-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="5ff84-350">DBMS 叢集：<*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5ff84-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="5ff84-351">**所有虛擬機器的網路卡，包含關聯的 IP 位址**：</span><span class="sxs-lookup"><span data-stu-id="5ff84-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="5ff84-352"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5ff84-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="5ff84-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5ff84-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="5ff84-354"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5ff84-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="5ff84-355">**Azure 儲存體帳戶 (僅限非受控磁碟)**</span><span class="sxs-lookup"><span data-stu-id="5ff84-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="5ff84-356">下列項目的**可用性群組**：</span><span class="sxs-lookup"><span data-stu-id="5ff84-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="5ff84-357">SAP 應用程式伺服器虛擬機器︰<*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="5ff84-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="5ff84-358">SAP ASCS/SCS 叢集虛擬機器︰<*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="5ff84-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="5ff84-359">DBMS 叢集虛擬機器︰<*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="5ff84-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="5ff84-360">**Azure 內部負載平衡器**：</span><span class="sxs-lookup"><span data-stu-id="5ff84-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="5ff84-361">包含 ASCS/SCS 執行個體的所有連接埠與 IP 位址 <*SAPSystemSID*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5ff84-361">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="5ff84-362">包含 SQL Server DBMS 的所有連接埠與 IP 位址 <*SAPSystemSID*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5ff84-362">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="5ff84-363">**網路安全性群組**：<*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="5ff84-364">包含向 <*SAPSystemSID*>-ascs-0 虛擬機器開放的外部遠端桌面通訊協定 (RDP) 連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-364">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-365">網路卡的所有 IP 位址和 Azure 內部負載平衡器依預設為**動態**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-365">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="5ff84-366">將其變更為**靜態** IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-366">Change them to **static** IP addresses.</span></span> <span data-ttu-id="5ff84-367">本文稍後會描述做法。</span><span class="sxs-lookup"><span data-stu-id="5ff84-367">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="5ff84-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> 使用公司網路連線能力 (跨單位) 部署虛擬機器以用於生產環境中</span><span class="sxs-lookup"><span data-stu-id="5ff84-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="5ff84-369">針對生產環境 SAP 系統，使用 Azure 站對站 VPN 或 Azure ExpressRoute，部署具有 [公司網路連線能力 (跨單位)][][planning-guide-2.2] 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-370">您可以使用您的 Azure 虛擬網路執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="5ff84-371">虛擬網路和子網路已建立並備妥。</span><span class="sxs-lookup"><span data-stu-id="5ff84-371">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="5ff84-372">在 Azure 入口網站中，在 [參數] 刀鋒視窗的 [NEWOREXISTINGSUBNET] 方塊中，選取 [存在]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-372">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="5ff84-373">在 [SUBNETID] 方塊中，新增已備妥的「Azure 網路 SubnetID」的完整字串，這是您打算用來部署 Azure 虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="5ff84-373">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="5ff84-374">若要取得所有 Azure 網路子網路的清單，請執行此 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="5ff84-374">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="5ff84-375">[ID] 欄位顯示 **SUBNETID**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-375">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="5ff84-376">若要取得所有 **SUBNETID** 值的清單，請執行此 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="5ff84-376">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="5ff84-377">**SUBNETID** 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="5ff84-377">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="5ff84-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> 用於測試和示範的 SAP 執行個體僅限部署雲端</span><span class="sxs-lookup"><span data-stu-id="5ff84-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="5ff84-379">您可以在僅限雲端部署模型中部署您的高可用性 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="5ff84-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="5ff84-380">這種部署主要對於示範和測試的使用案例相當有用。</span><span class="sxs-lookup"><span data-stu-id="5ff84-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="5ff84-381">但不適用於生產環境使用案例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="5ff84-382">在 Azure 入口網站中，在 [參數] 刀鋒視窗的 [NEWOREXISTINGSUBNET] 方塊中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-382">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="5ff84-383">將 [SUBNETID] 欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="5ff84-383">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="5ff84-384">SAP Azure Resource Manager 範本將會自動建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="5ff84-384">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-385">您也需要在相同的 Azure 虛擬網路執行個體中，針對 Active Directory 和 DNS 部署至少一個專用的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-385">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="5ff84-386">此範本不會建立這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-386">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="5ff84-387">準備架構範本 2 的基礎結構</span><span class="sxs-lookup"><span data-stu-id="5ff84-387">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="5ff84-388">您可以使用這個適用於 SAP 的 Azure Resource Manager 範本，以協助簡化部署必要的 SAP 架構範本 2 基礎結構資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-388">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="5ff84-389">您可以在這裡取得此部署案例的 Azure Resource Manager 範本：</span><span class="sxs-lookup"><span data-stu-id="5ff84-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="5ff84-390">Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="5ff84-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* <span data-ttu-id="5ff84-391">[使用受控磁碟的 Azure Marketplace 映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="5ff84-391">[Azure Marketplace image using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)</span></span>  
* [<span data-ttu-id="5ff84-392">自訂映像</span><span class="sxs-lookup"><span data-stu-id="5ff84-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* <span data-ttu-id="5ff84-393">[使用受控磁碟的自訂映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="5ff84-393">[Custom image using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)</span></span>


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="5ff84-394">準備架構範本 3 的基礎結構</span><span class="sxs-lookup"><span data-stu-id="5ff84-394">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="5ff84-395">您可以準備基礎結構，並將 SAP 設定為**多 SID**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-395">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="5ff84-396">例如，您可以將額外的 SAP ASCS/SCS 執行個體新增至現有的叢集組態以建立 SAP 多 SID 組態。</span><span class="sxs-lookup"><span data-stu-id="5ff84-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="5ff84-397">如需詳細資訊，請參閱[將額外的 SAP ASCS/SCS 執行個體設定為現有的叢集組態以在 Azure Resource Manager 中建立 SAP 多 SID 組態][sap-ha-multi-sid-guide]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="5ff84-398">如果您想要建立新的多 SID 叢集，可以使用多 SID [GitHub 上的快速入門範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-398">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="5ff84-399">若要建立新的多 SID 叢集，您需要部署下列三個範本︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-399">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="5ff84-400">ASCS/SCS 範本</span><span class="sxs-lookup"><span data-stu-id="5ff84-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="5ff84-401">資料庫範本</span><span class="sxs-lookup"><span data-stu-id="5ff84-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="5ff84-402">應用程式伺服器範本</span><span class="sxs-lookup"><span data-stu-id="5ff84-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="5ff84-403">下列各節有更多關於您需要在範本中提供之範本和參數的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5ff84-403">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="5ff84-404"><a name="ASCS-SCS-template">ASCS/SCS 範本</a></span><span class="sxs-lookup"><span data-stu-id="5ff84-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="5ff84-405">ASCS/SCS 範本會部署兩部虛擬機器，可讓您用來建立裝載多個 ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-405">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="5ff84-406">若要設定 ASCS/SCS 多 SID 範本，請在 [ASCS/SCS 多 SID 範本][sap-templates-3-tier-multisid-xscs-marketplace-image]或[使用受控磁碟的 ASCS/SCS 多 SID 範本][sap-templates-3-tier-multisid-xscs-marketplace-image-md]中輸入下列參數的值︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-406">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for the following parameters:</span></span>

  - <span data-ttu-id="5ff84-407">**資源前置詞**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-407">**Resource Prefix**.</span></span>  <span data-ttu-id="5ff84-408">設定資源前置詞，其用來前置部署期間建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-408">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="5ff84-409">因為資源不只屬於一個 SAP 系統，資源的前置詞不是一個 SAP 系統的 SID。</span><span class="sxs-lookup"><span data-stu-id="5ff84-409">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="5ff84-410">前置詞必須介於**三到六個字元**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-410">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="5ff84-411">**堆疊類型**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-411">**Stack Type**.</span></span> <span data-ttu-id="5ff84-412">選取 SAP 系統的堆疊類型。</span><span class="sxs-lookup"><span data-stu-id="5ff84-412">Select the stack type of the SAP system.</span></span> <span data-ttu-id="5ff84-413">根據堆疊類型而定，Azure Load Balancer 每個 SAP 系統會有一個 (ABAP 或僅 Java) 或兩個 (ABAP + Java) 私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-413">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="5ff84-414">**OS 類型**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-414">**OS Type**.</span></span> <span data-ttu-id="5ff84-415">選取虛擬機器的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5ff84-415">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5ff84-416">**SAP 系統計數**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-416">**SAP System Count**.</span></span> <span data-ttu-id="5ff84-417">選取您想要安裝在此叢集中的 SAP 系統數目。</span><span class="sxs-lookup"><span data-stu-id="5ff84-417">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="5ff84-418">**系統可用性**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-418">**System Availability**.</span></span> <span data-ttu-id="5ff84-419">選取 **HA**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-419">Select **HA**.</span></span>
  -  <span data-ttu-id="5ff84-420">**管理員使用者名稱和管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5ff84-421">建立可用來登入電腦的新使用者。</span><span class="sxs-lookup"><span data-stu-id="5ff84-421">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5ff84-422">**新的或現有的子網路**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="5ff84-423">設定應該建立新的虛擬網路和子網路，還是應該使用現有子網路。</span><span class="sxs-lookup"><span data-stu-id="5ff84-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="5ff84-424">如果您已經有連接到內部部署網路的虛擬網路，請選取**現有**虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5ff84-424">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="5ff84-425">**子網路識別碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-425">**Subnet Id**.</span></span> <span data-ttu-id="5ff84-426">設定虛擬機器應該連接的子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-426">Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="5ff84-427">選取將虛擬機器連接到內部部署網路之虛擬私人網路 (VPN) 或 ExpressRoute 虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="5ff84-427">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="5ff84-428">識別碼通常看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-428">The ID usually looks like this:</span></span>

   <span data-ttu-id="5ff84-429">/subscriptions/<*訂用帳戶識別碼*>/resourceGroups/<*資源群組名稱*>/providers/Microsoft.Network/virtualNetworks/<*虛擬網路名稱*>/subnets/<*子網路名稱*></span><span class="sxs-lookup"><span data-stu-id="5ff84-429">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="5ff84-430">範本會部署一個 Azure Load Balancer 執行個體，可支援多個 SAP 系統。</span><span class="sxs-lookup"><span data-stu-id="5ff84-430">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="5ff84-431">針對執行個體號碼 00、10、20... 設定的 ASCS 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-431">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="5ff84-432">針對執行個體號碼 01、11、21... 設定的 ASCS 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-432">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="5ff84-433">針對執行個體號碼 02、12、22... 設定的 ASCS 加入佇列複寫伺服器 (ERS) (僅限 Linux) 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-433">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="5ff84-434">針對執行個體號碼 03、13、23... 設定的 SCS ERS (僅限 Linux) 執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-434">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="5ff84-435">負載平衡器包含 1 個 (2 個適用於 Linux) VIP、1 個 VIP 適用於 ASCS/SCS 和1 個 VIP 適用於 ERS (僅 Linux)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-435">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="5ff84-436">下列清單包含所有的負載平衡規則 (其中 x 是 SAP 系統的數目，例如 1、2、3...)︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-436">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="5ff84-437">每個 SAP 系統的 Windows 特定連接埠︰445、5985</span><span class="sxs-lookup"><span data-stu-id="5ff84-437">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="5ff84-438">ASCS 連接埠 (執行個體數目 x0)︰32x0、36x0、39x0、81x0、5x013、5x014、5x016</span><span class="sxs-lookup"><span data-stu-id="5ff84-438">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="5ff84-439">SCS 連接埠 (執行個體數目 x1)︰32x1、33x1、39x1、81x1、5x113、5x114、5x116</span><span class="sxs-lookup"><span data-stu-id="5ff84-439">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="5ff84-440">Linux 上的 ASCS ERS 連接埠 (執行個體數目 x2)︰33x2、5x213、5x214、5x216</span><span class="sxs-lookup"><span data-stu-id="5ff84-440">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="5ff84-441">Linux 上的 SCS ERS 連接埠 (執行個體數目 x3)︰33x3、5x313、5x314、5x316</span><span class="sxs-lookup"><span data-stu-id="5ff84-441">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="5ff84-442">負載平衡器設定為使用下列的探查連接埠 (其中 x 是 SAP 系統的數目，例如 1、2、3...)︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-442">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="5ff84-443">ASCS/SCS 內部負載平衡器探查連接埠︰620x0</span><span class="sxs-lookup"><span data-stu-id="5ff84-443">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="5ff84-444">ERS 內部負載平衡器探查連接埠 (僅 Linux)︰621x2</span><span class="sxs-lookup"><span data-stu-id="5ff84-444">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="5ff84-445"><a name="database-template"></a> 資料庫範本</span><span class="sxs-lookup"><span data-stu-id="5ff84-445"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="5ff84-446">資料庫範本會部署一個或兩個虛擬機器，可讓您用來安裝一個 SAP 系統的關聯式資料庫管理系統 (RDBMS)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-446">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="5ff84-447">例如，如果您部署五個 SAP 系統的 ASCS/SCS 範本，您需要部署此範本五次。</span><span class="sxs-lookup"><span data-stu-id="5ff84-447">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="5ff84-448">若要設定資料庫多 SID 範本，請在[資料庫多 SID 範本][sap-templates-3-tier-multisid-db-marketplace-image]或[使用受控磁碟的資料庫多 SID 範本][sap-templates-3-tier-multisid-db-marketplace-image-md]中輸入下列參數的值︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-448">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="5ff84-449">**SAP 系統識別碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-449">**Sap System Id**.</span></span> <span data-ttu-id="5ff84-450">輸入您想要安裝的 SAP 系統之 SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-450">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="5ff84-451">識別碼將用於已部署資源的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5ff84-451">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="5ff84-452">**OS 類型**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-452">**Os Type**.</span></span> <span data-ttu-id="5ff84-453">選取虛擬機器的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5ff84-453">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5ff84-454">**Dbtype**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-454">**Dbtype**.</span></span> <span data-ttu-id="5ff84-455">選取您想要在叢集上安裝的資料庫類型。</span><span class="sxs-lookup"><span data-stu-id="5ff84-455">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="5ff84-456">如果您想要安裝 Microsoft SQL Server，選取 **SQL**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-456">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="5ff84-457">如果您打算在虛擬機器上安裝 SAP HANA，選取 **HANA**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-457">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="5ff84-458">請務必選取正確的作業系統類型︰針對 SQL 選取 **Windows**，針對 HANA 選取 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="5ff84-458">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="5ff84-459">連線到虛擬機器的 Azure Load Balancer 會設定為支援所選取的資料庫類型︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-459">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="5ff84-460">**SQL**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-460">**SQL**.</span></span> <span data-ttu-id="5ff84-461">負載平衡器會負載平衡連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="5ff84-461">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="5ff84-462">請務必針對您的 SQL Server Always On 設定使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="5ff84-462">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="5ff84-463">**HANA**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-463">**HANA**.</span></span> <span data-ttu-id="5ff84-464">負載平衡器會負載平衡連接埠 35015 和 35017。</span><span class="sxs-lookup"><span data-stu-id="5ff84-464">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="5ff84-465">請務必以執行個體數目 **50** 安裝 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="5ff84-465">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="5ff84-466">負載平衡器會使用探查連接埠 62550。</span><span class="sxs-lookup"><span data-stu-id="5ff84-466">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="5ff84-467">**SAP 系統大小**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-467">**Sap System Size**.</span></span> <span data-ttu-id="5ff84-468">設定新系統將提供的 SAP 數量。</span><span class="sxs-lookup"><span data-stu-id="5ff84-468">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="5ff84-469">如果您不確定系統將需要多少 SAP，請詢問您的 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="5ff84-469">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="5ff84-470">**系統可用性**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-470">**System Availability**.</span></span> <span data-ttu-id="5ff84-471">選取 **HA**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-471">Select **HA**.</span></span>
  -  <span data-ttu-id="5ff84-472">**管理員使用者名稱和管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-472">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5ff84-473">建立可用來登入電腦的新使用者。</span><span class="sxs-lookup"><span data-stu-id="5ff84-473">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5ff84-474">**子網路識別碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-474">**Subnet Id**.</span></span> <span data-ttu-id="5ff84-475">輸入您在部署 ASCS/SCS 範本期間使用的子網路識別碼，或做為 ASCS/SCS 範本部署的一部分建立之子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-475">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="5ff84-476"><a name="application-servers-template"></a> 應用程式伺服器範本</span><span class="sxs-lookup"><span data-stu-id="5ff84-476"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="5ff84-477">應用程式伺服器範本會部署兩個或多個虛擬機器，可用來做為一個 SAP 系統的 SAP 應用程式伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-477">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="5ff84-478">例如，如果您部署五個 SAP 系統的 ASCS/SCS 範本，您需要部署此範本五次。</span><span class="sxs-lookup"><span data-stu-id="5ff84-478">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="5ff84-479">若要設定應用程式伺服器多 SID 範本，請在[應用程式伺服器多 SID 範本][sap-templates-3-tier-multisid-apps-marketplace-image]或[使用受控磁碟的應用程式伺服器多 SID 範本][sap-templates-3-tier-multisid-apps-marketplace-image-md]中輸入下列參數的值︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-479">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="5ff84-480">**SAP 系統識別碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-480">**Sap System Id**.</span></span> <span data-ttu-id="5ff84-481">輸入您想要安裝的 SAP 系統之 SAP 系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-481">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="5ff84-482">識別碼將用於已部署資源的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5ff84-482">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="5ff84-483">**OS 類型**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-483">**Os Type**.</span></span> <span data-ttu-id="5ff84-484">選取虛擬機器的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5ff84-484">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5ff84-485">**SAP 系統大小**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-485">**Sap System Size**.</span></span> <span data-ttu-id="5ff84-486">新系統將提供的 SAP 數量。</span><span class="sxs-lookup"><span data-stu-id="5ff84-486">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="5ff84-487">如果您不確定系統將需要多少 SAP，請詢問您的 SAP 技術合作夥伴或系統整合者。</span><span class="sxs-lookup"><span data-stu-id="5ff84-487">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="5ff84-488">**系統可用性**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-488">**System Availability**.</span></span> <span data-ttu-id="5ff84-489">選取 **HA**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-489">Select **HA**.</span></span>
  -  <span data-ttu-id="5ff84-490">**管理員使用者名稱和管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-490">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5ff84-491">建立可用來登入電腦的新使用者。</span><span class="sxs-lookup"><span data-stu-id="5ff84-491">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5ff84-492">**子網路識別碼**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-492">**Subnet Id**.</span></span> <span data-ttu-id="5ff84-493">輸入您在部署 ASCS/SCS 範本期間使用的子網路識別碼，或做為 ASCS/SCS 範本部署的一部分建立之子網路識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-493">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="5ff84-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5ff84-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="5ff84-495">在我們的範例中，Azure 虛擬網路的位址空間是 10.0.0.0/16。</span><span class="sxs-lookup"><span data-stu-id="5ff84-495">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="5ff84-496">有一個名為 **Subnet**、網址範圍為 10.0.0.0/24 的子網路。</span><span class="sxs-lookup"><span data-stu-id="5ff84-496">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="5ff84-497">所有虛擬機器和內部負載平衡器會部署在此虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-497">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ff84-498">請勿對客體作業系統內的網路設定進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="5ff84-498">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="5ff84-499">包括 IP 位址、DNS 伺服器和子網路。</span><span class="sxs-lookup"><span data-stu-id="5ff84-499">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="5ff84-500">在 Azure 中設定所有網路設定。</span><span class="sxs-lookup"><span data-stu-id="5ff84-500">Configure all your network settings in Azure.</span></span> <span data-ttu-id="5ff84-501">動態主機設定通訊協定 (DHCP) 服務會散佈您的設定。</span><span class="sxs-lookup"><span data-stu-id="5ff84-501">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="5ff84-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="5ff84-503">若要設定所需的 DNS IP 位址，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-503">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="5ff84-504">在 Azure 入口網站的 [DNS 伺服器] 刀鋒視窗上，確定您的虛擬網路 [DNS 伺服器] 選項是設定為 [自訂 DNS]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-504">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="5ff84-505">根據您擁有的網路類型選取設定。</span><span class="sxs-lookup"><span data-stu-id="5ff84-505">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="5ff84-506">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5ff84-506">For more information, see the following resources:</span></span>
    * <span data-ttu-id="5ff84-507">[公司網路連線能力 (跨單位)][planning-guide-2.2]︰請新增內部部署 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-507">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="5ff84-508">您可以將內部部署 DNS 伺服器擴充至 Azure 中執行的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-508">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="5ff84-509">在這種情況下，您可以加入執行 DNS 服務之 Azure 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-509">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="5ff84-510">[僅限雲端部署][planning-guide-2.1]：在做為 DNS 伺服器的相同虛擬網路執行個體中，部署其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-510">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="5ff84-511">新增您已設定執行 DNS 服務之 Azure 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-511">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![圖 12：設定 Azure 虛擬網路的 DNS 伺服器][sap-ha-guide-figure-3001]

    <span data-ttu-id="5ff84-513">_**圖 12：**設定 Azure 虛擬網路的 DNS 伺服器_</span><span class="sxs-lookup"><span data-stu-id="5ff84-513">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="5ff84-514">如果您變更 DNS 伺服器的 IP 位址，您就必須重新啟動 Azure 虛擬機器，才能套用變更並傳播新的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-514">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="5ff84-515">在我們的範例中，是在下列 Windows 虛擬機器上安裝並設定 DNS 服務：</span><span class="sxs-lookup"><span data-stu-id="5ff84-515">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="5ff84-516">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="5ff84-516">Virtual machine role</span></span> | <span data-ttu-id="5ff84-517">虛擬機器主機名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-517">Virtual machine host name</span></span> | <span data-ttu-id="5ff84-518">網路卡名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-518">Network card name</span></span> | <span data-ttu-id="5ff84-519">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-519">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5ff84-520">第一部 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="5ff84-520">First DNS server</span></span> |<span data-ttu-id="5ff84-521">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-521">domcontr-0</span></span> |<span data-ttu-id="5ff84-522">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-522">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="5ff84-523">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="5ff84-523">10.0.0.10</span></span> |
| <span data-ttu-id="5ff84-524">第二部 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="5ff84-524">Second DNS server</span></span> |<span data-ttu-id="5ff84-525">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-525">domcontr-1</span></span> |<span data-ttu-id="5ff84-526">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-526">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="5ff84-527">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="5ff84-527">10.0.0.11</span></span> |

### <span data-ttu-id="5ff84-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> SAP ASCS/SCS 叢集執行個體及 DBMS 叢集執行個體的主機名稱和靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="5ff84-529">對於內部部署，您需要下列保留的主機名稱和 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="5ff84-529">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="5ff84-530">虛擬主機名稱角色</span><span class="sxs-lookup"><span data-stu-id="5ff84-530">Virtual host name role</span></span> | <span data-ttu-id="5ff84-531">虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-531">Virtual host name</span></span> | <span data-ttu-id="5ff84-532">虛擬靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-532">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ff84-533">SAP ASCS/SCS 第一個叢集虛擬主機名稱 (用於叢集管理)</span><span class="sxs-lookup"><span data-stu-id="5ff84-533">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="5ff84-534">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="5ff84-534">pr1-ascs-vir</span></span> |<span data-ttu-id="5ff84-535">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="5ff84-535">10.0.0.42</span></span> |
| <span data-ttu-id="5ff84-536">SAP ASCS/SCS 執行個體虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-536">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="5ff84-537">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="5ff84-537">pr1-ascs-sap</span></span> |<span data-ttu-id="5ff84-538">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="5ff84-538">10.0.0.43</span></span> |
| <span data-ttu-id="5ff84-539">SAP DBMS 第二個叢集虛擬主機名稱 (叢集管理)</span><span class="sxs-lookup"><span data-stu-id="5ff84-539">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="5ff84-540">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="5ff84-540">pr1-dbms-vir</span></span> |<span data-ttu-id="5ff84-541">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="5ff84-541">10.0.0.32</span></span> |

<span data-ttu-id="5ff84-542">當您建立叢集時，請建立虛擬主機名稱 **pr1-ascs-vir** 和 **pr1-dbms-vir**，以及管理叢集本身的相關 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-542">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="5ff84-543">如需如何執行這項操作的詳細資訊，請參閱[在叢集組態中收集叢集節點][sap-ha-guide-8.12.1]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-543">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="5ff84-544">您可以在 DNS 伺服器上手動建立其他兩個虛擬主機名稱，**pr1-ascs-sap** 和 **pr1-dbms-sap**，以及相關的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-544">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="5ff84-545">叢集 SAP ASCS/SCS 執行個體和叢集 DBMS 執行個體使用這些資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-545">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="5ff84-546">如需如何執行這項操作的詳細資訊，請參閱[建立叢集 SAP ASCS/SCS 執行個體的虛擬主機名稱][sap-ha-guide-9.1.1]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-546">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="5ff84-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> 設定 SAP 虛擬機器的靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="5ff84-548">部署要在叢集中使用的虛擬機器之後，您需要設定所有虛擬機器的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-548">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="5ff84-549">在 Azure 虛擬網路組態中執行此動作，而非在客體作業系統中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-549">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="5ff84-550">在 Azure 入口網站中選取 [資源群組] > [網路卡] > [設定] > [IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-550">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="5ff84-551">在 [IP 位址] 刀鋒視窗 [指派] 下，選取 [靜態]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-551">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="5ff84-552">在 [IP 位址] 方塊中，輸入您要使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-552">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5ff84-553">如果您變更網路卡的 IP 位址，您就必須重新啟動 Azure 虛擬機器，才能套用變更。</span><span class="sxs-lookup"><span data-stu-id="5ff84-553">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![圖 13：為每個虛擬機器的網路卡設定靜態 IP 位址][sap-ha-guide-figure-3002]

  <span data-ttu-id="5ff84-555">_**圖 13：**為每個虛擬機器的網路卡設定靜態 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="5ff84-555">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="5ff84-556">為所有網路介面重複此步驟，亦即為所有虛擬機器，包括您要用於 Active Directory/DNS 服務的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-556">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="5ff84-557">在我們的範例中，有下列虛擬機器和靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="5ff84-557">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="5ff84-558">虛擬機器角色</span><span class="sxs-lookup"><span data-stu-id="5ff84-558">Virtual machine role</span></span> | <span data-ttu-id="5ff84-559">虛擬機器主機名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-559">Virtual machine host name</span></span> | <span data-ttu-id="5ff84-560">網路卡名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-560">Network card name</span></span> | <span data-ttu-id="5ff84-561">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-561">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5ff84-562">第一部 SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-562">First SAP Application Server instance</span></span> |<span data-ttu-id="5ff84-563">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-563">pr1-di-0</span></span> |<span data-ttu-id="5ff84-564">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-564">pr1-nic-di-0</span></span> |<span data-ttu-id="5ff84-565">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="5ff84-565">10.0.0.50</span></span> |
| <span data-ttu-id="5ff84-566">第二部 SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-566">Second SAP Application Server instance</span></span> |<span data-ttu-id="5ff84-567">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-567">pr1-di-1</span></span> |<span data-ttu-id="5ff84-568">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-568">pr1-nic-di-1</span></span> |<span data-ttu-id="5ff84-569">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="5ff84-569">10.0.0.51</span></span> |
| <span data-ttu-id="5ff84-570">...</span><span class="sxs-lookup"><span data-stu-id="5ff84-570">...</span></span> |<span data-ttu-id="5ff84-571">...</span><span class="sxs-lookup"><span data-stu-id="5ff84-571">...</span></span> |<span data-ttu-id="5ff84-572">...</span><span class="sxs-lookup"><span data-stu-id="5ff84-572">...</span></span> |<span data-ttu-id="5ff84-573">...</span><span class="sxs-lookup"><span data-stu-id="5ff84-573">...</span></span> |
| <span data-ttu-id="5ff84-574">最後一部 SAP 應用程式伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-574">Last SAP Application Server instance</span></span> |<span data-ttu-id="5ff84-575">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="5ff84-575">pr1-di-5</span></span> |<span data-ttu-id="5ff84-576">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="5ff84-576">pr1-nic-di-5</span></span> |<span data-ttu-id="5ff84-577">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="5ff84-577">10.0.0.55</span></span> |
| <span data-ttu-id="5ff84-578">ASCS/SCS 執行個體的第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-578">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5ff84-579">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-579">pr1-ascs-0</span></span> |<span data-ttu-id="5ff84-580">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-580">pr1-nic-ascs-0</span></span> |<span data-ttu-id="5ff84-581">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="5ff84-581">10.0.0.40</span></span> |
| <span data-ttu-id="5ff84-582">ASCS/SCS 執行個體的第二個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-582">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5ff84-583">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-583">pr1-ascs-1</span></span> |<span data-ttu-id="5ff84-584">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-584">pr1-nic-ascs-1</span></span> |<span data-ttu-id="5ff84-585">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="5ff84-585">10.0.0.41</span></span> |
| <span data-ttu-id="5ff84-586">DBMS 執行個體的第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-586">First cluster node for DBMS instance</span></span> |<span data-ttu-id="5ff84-587">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-587">pr1-db-0</span></span> |<span data-ttu-id="5ff84-588">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="5ff84-588">pr1-nic-db-0</span></span> |<span data-ttu-id="5ff84-589">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="5ff84-589">10.0.0.30</span></span> |
| <span data-ttu-id="5ff84-590">DBMS 執行個體的第二個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-590">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="5ff84-591">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-591">pr1-db-1</span></span> |<span data-ttu-id="5ff84-592">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="5ff84-592">pr1-nic-db-1</span></span> |<span data-ttu-id="5ff84-593">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="5ff84-593">10.0.0.31</span></span> |

### <span data-ttu-id="5ff84-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> 為 Azure 內部負載平衡器設定靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="5ff84-595">SAP Azure Resource Manager 範本會建立用於 SAP ASCS/SCS 執行個體叢集和用於 DBMS 叢集的 Azure 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-595">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ff84-596">SAP ASCS/SCS 之虛擬主機名稱的 IP 位址與 SAP ASCS/SCS 內部負載平衡器：**pr1-lb-ascs** 的 IP 位址相同。</span><span class="sxs-lookup"><span data-stu-id="5ff84-596">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="5ff84-597">DBMS 之虛擬名稱的 IP 位址與 DBMS 內部負載平衡器：**pr1-lb-dbms** 的 IP 位址相同。</span><span class="sxs-lookup"><span data-stu-id="5ff84-597">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="5ff84-598">若要為 Azure 內部負載平衡器設定靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="5ff84-598">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="5ff84-599">初始部署會將內部負載平衡器的 IP 位址設定為 [動態]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-599">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="5ff84-600">在 Azure 入口網站 [IP 位址] 刀鋒視窗 [指派] 下，選取 [靜態]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-600">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="5ff84-601">請將「內部負載平衡器」**pr1-lb-ascs** 的 IP 位址設定為 SAP ASCS/SCS 執行個體的虛擬主機名稱 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-601">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="5ff84-602">請將「內部負載平衡器」**pr1-lb-dbms** 的 IP 位址設定為 DBMS 執行個體的虛擬主機名稱 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-602">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![圖 14：為 SAP ASCS/SCS 執行個體的內部負載平衡器設定靜態 IP 位址][sap-ha-guide-figure-3003]

  <span data-ttu-id="5ff84-604">_**圖 14：**為 SAP ASCS/SCS 執行個體的內部負載平衡器設定靜態 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="5ff84-604">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="5ff84-605">在我們的範例中，有兩個 Azure 內部負載平衡器具備這些靜態 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="5ff84-605">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="5ff84-606">Azure 內部負載平衡器角色</span><span class="sxs-lookup"><span data-stu-id="5ff84-606">Azure internal load balancer role</span></span> | <span data-ttu-id="5ff84-607">Azure 內部負載平衡器名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-607">Azure internal load balancer name</span></span> | <span data-ttu-id="5ff84-608">靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ff84-608">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ff84-609">SAP ASCS/SCS 執行個體內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5ff84-609">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="5ff84-610">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5ff84-610">pr1-lb-ascs</span></span> |<span data-ttu-id="5ff84-611">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="5ff84-611">10.0.0.43</span></span> |
| <span data-ttu-id="5ff84-612">SAP DBMS 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5ff84-612">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="5ff84-613">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="5ff84-613">pr1-lb-dbms</span></span> |<span data-ttu-id="5ff84-614">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="5ff84-614">10.0.0.33</span></span> |


### <span data-ttu-id="5ff84-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Azure 內部負載平衡器的預設 ASCS/SCS 負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="5ff84-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="5ff84-616">SAP Azure Resource Manager 範本會建立所需的連接埠：</span><span class="sxs-lookup"><span data-stu-id="5ff84-616">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="5ff84-617">ABAP ASCS 執行個體預設的執行個體號碼為 **00**</span><span class="sxs-lookup"><span data-stu-id="5ff84-617">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="5ff84-618">Java SCS 執行個體預設的執行個體號碼為 **01**</span><span class="sxs-lookup"><span data-stu-id="5ff84-618">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="5ff84-619">當您安裝 SAP ASCS/SCS 執行個體時，必須為 ABAP ASCS 執行個體使用預設的執行個體號碼 **00**，並為 Java SCS 執行個體使用預設的執行個體號碼 **01**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-619">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="5ff84-620">接著，為 SAP NetWeaver 連接埠建立下列必要的內部負載平衡端點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-620">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="5ff84-621">若要建立必要的內部負載平衡端點，首先，為 SAP NetWeaver ABAP ASCS 連接埠建立下列必要的內部負載平衡端點：</span><span class="sxs-lookup"><span data-stu-id="5ff84-621">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="5ff84-622">服務/負載平衡規則名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-622">Service/load balancing rule name</span></span> | <span data-ttu-id="5ff84-623">預設連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="5ff84-623">Default port numbers</span></span> | <span data-ttu-id="5ff84-624">(執行個體號碼為 00 的 ASCS 執行個體) (ERS 為 10) 的具體連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-624">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ff84-625">加入佇列伺服器 / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="5ff84-625">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="5ff84-626">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-626">32<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-627">3200</span><span class="sxs-lookup"><span data-stu-id="5ff84-627">3200</span></span> |
| <span data-ttu-id="5ff84-628">ABAP 訊息伺服器 / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="5ff84-628">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="5ff84-629">36<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-629">36<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-630">3600</span><span class="sxs-lookup"><span data-stu-id="5ff84-630">3600</span></span> |
| <span data-ttu-id="5ff84-631">內部 ABAP 訊息 / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="5ff84-631">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="5ff84-632">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-632">39<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-633">3900</span><span class="sxs-lookup"><span data-stu-id="5ff84-633">3900</span></span> |
| <span data-ttu-id="5ff84-634">訊息伺服器 HTTP / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="5ff84-634">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="5ff84-635">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-635">81<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-636">8100</span><span class="sxs-lookup"><span data-stu-id="5ff84-636">8100</span></span> |
| <span data-ttu-id="5ff84-637">SAP 啟動服務 ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="5ff84-637">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="5ff84-638">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="5ff84-638">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5ff84-639">50013</span><span class="sxs-lookup"><span data-stu-id="5ff84-639">50013</span></span> |
| <span data-ttu-id="5ff84-640">SAP 啟動服務 ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="5ff84-640">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="5ff84-641">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="5ff84-641">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5ff84-642">50014</span><span class="sxs-lookup"><span data-stu-id="5ff84-642">50014</span></span> |
| <span data-ttu-id="5ff84-643">加入佇列複寫 / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="5ff84-643">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="5ff84-644">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="5ff84-644">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="5ff84-645">50016</span><span class="sxs-lookup"><span data-stu-id="5ff84-645">50016</span></span> |
| <span data-ttu-id="5ff84-646">SAP 啟動服務 ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="5ff84-646">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="5ff84-647">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="5ff84-647">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5ff84-648">51013</span><span class="sxs-lookup"><span data-stu-id="5ff84-648">51013</span></span> |
| <span data-ttu-id="5ff84-649">SAP 啟動服務 ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="5ff84-649">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="5ff84-650">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="5ff84-650">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5ff84-651">51014</span><span class="sxs-lookup"><span data-stu-id="5ff84-651">51014</span></span> |
| <span data-ttu-id="5ff84-652">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="5ff84-652">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="5ff84-653">5985</span><span class="sxs-lookup"><span data-stu-id="5ff84-653">5985</span></span> |
| <span data-ttu-id="5ff84-654">檔案共用 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="5ff84-654">File Share *Lbrule445*</span></span> | |<span data-ttu-id="5ff84-655">445</span><span class="sxs-lookup"><span data-stu-id="5ff84-655">445</span></span> |

<span data-ttu-id="5ff84-656">_**表 1：**SAP NetWeaver ABAP ASCS 執行個體的連接埠號碼_</span><span class="sxs-lookup"><span data-stu-id="5ff84-656">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="5ff84-657">接著，為 SAP NetWeaver Java SCS 連接埠建立下列負載平衡端點：</span><span class="sxs-lookup"><span data-stu-id="5ff84-657">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="5ff84-658">服務/負載平衡規則名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-658">Service/load balancing rule name</span></span> | <span data-ttu-id="5ff84-659">預設連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="5ff84-659">Default port numbers</span></span> | <span data-ttu-id="5ff84-660">(執行個體號碼為 01 的 SCS 執行個體) (ERS 為 11) 的具體連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-660">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ff84-661">加入佇列伺服器 / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="5ff84-661">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="5ff84-662">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-662">32<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-663">3201</span><span class="sxs-lookup"><span data-stu-id="5ff84-663">3201</span></span> |
| <span data-ttu-id="5ff84-664">閘道伺服器 / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="5ff84-664">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="5ff84-665">33<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-665">33<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-666">3301</span><span class="sxs-lookup"><span data-stu-id="5ff84-666">3301</span></span> |
| <span data-ttu-id="5ff84-667">Java 訊息伺服器 / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="5ff84-667">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="5ff84-668">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-668">39<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-669">3901</span><span class="sxs-lookup"><span data-stu-id="5ff84-669">3901</span></span> |
| <span data-ttu-id="5ff84-670">訊息伺服器 HTTP / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="5ff84-670">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="5ff84-671">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5ff84-671">81<*InstanceNumber*></span></span> |<span data-ttu-id="5ff84-672">8101</span><span class="sxs-lookup"><span data-stu-id="5ff84-672">8101</span></span> |
| <span data-ttu-id="5ff84-673">SAP 啟動服務 SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="5ff84-673">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="5ff84-674">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="5ff84-674">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5ff84-675">50113</span><span class="sxs-lookup"><span data-stu-id="5ff84-675">50113</span></span> |
| <span data-ttu-id="5ff84-676">SAP 啟動服務 SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="5ff84-676">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="5ff84-677">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="5ff84-677">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5ff84-678">50114</span><span class="sxs-lookup"><span data-stu-id="5ff84-678">50114</span></span> |
| <span data-ttu-id="5ff84-679">加入佇列複寫 / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="5ff84-679">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="5ff84-680">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="5ff84-680">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="5ff84-681">50116</span><span class="sxs-lookup"><span data-stu-id="5ff84-681">50116</span></span> |
| <span data-ttu-id="5ff84-682">SAP 啟動服務 ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="5ff84-682">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="5ff84-683">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="5ff84-683">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5ff84-684">51113</span><span class="sxs-lookup"><span data-stu-id="5ff84-684">51113</span></span> |
| <span data-ttu-id="5ff84-685">SAP 啟動服務 ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="5ff84-685">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="5ff84-686">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="5ff84-686">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5ff84-687">51114</span><span class="sxs-lookup"><span data-stu-id="5ff84-687">51114</span></span> |
| <span data-ttu-id="5ff84-688">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="5ff84-688">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="5ff84-689">5985</span><span class="sxs-lookup"><span data-stu-id="5ff84-689">5985</span></span> |
| <span data-ttu-id="5ff84-690">檔案共用 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="5ff84-690">File Share *Lbrule445*</span></span> | |<span data-ttu-id="5ff84-691">445</span><span class="sxs-lookup"><span data-stu-id="5ff84-691">445</span></span> |

<span data-ttu-id="5ff84-692">_**表 2：**SAP NetWeaver Java SCS 執行個體的連接埠號碼_</span><span class="sxs-lookup"><span data-stu-id="5ff84-692">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![圖 15：Azure 內部負載平衡器的預設 ASCS/SCS 負載平衡規][sap-ha-guide-figure-3004]

<span data-ttu-id="5ff84-694">_**圖 15：**Azure 內部負載平衡器的預設 ASCS/SCS 負載平衡規_</span><span class="sxs-lookup"><span data-stu-id="5ff84-694">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="5ff84-695">將負載平衡器 **pr1-lb-dbms** 的 IP 位址設定為 DBMS 執行個體之虛擬主機名稱的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-695">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="5ff84-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> 變更 Azure 內部負載平衡器的 ASCS/SCS 預設負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="5ff84-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="5ff84-697">如果您想要將其他號碼用於 SAP ASCS 或 SCS 執行個體，您就必須從預設值變更其連接埠的名稱和值。</span><span class="sxs-lookup"><span data-stu-id="5ff84-697">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="5ff84-698">在 Azure 入口網站中，選取 **<*SID*>-lb-ascs 負載平衡器** > **[負載平衡規則]**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-698">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="5ff84-699">針對屬於 SAP ASCS 或 SCS 執行個體的所有負載平衡規則，變更下列值：</span><span class="sxs-lookup"><span data-stu-id="5ff84-699">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="5ff84-700">名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-700">Name</span></span>
  * <span data-ttu-id="5ff84-701">連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-701">Port</span></span>
  * <span data-ttu-id="5ff84-702">後端連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-702">Back-end port</span></span>

  <span data-ttu-id="5ff84-703">例如，如果您要將預設 ASCS 執行個體號碼從 00 變更為 31，您需要針對表 1 中所列的所有通訊埠進行變更。</span><span class="sxs-lookup"><span data-stu-id="5ff84-703">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="5ff84-704">以下是連接埠 *lbrule3200*的更新範例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-704">Here's an example of an update for port *lbrule3200*.</span></span>

  ![圖 16：變更 Azure 內部負載平衡器的 ASCS/SCS 預設負載平衡規則][sap-ha-guide-figure-3005]

  <span data-ttu-id="5ff84-706">_**圖 16：**變更 Azure 內部負載平衡器的 ASCS/SCS 預設負載平衡規則_</span><span class="sxs-lookup"><span data-stu-id="5ff84-706">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="5ff84-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> 將 Windows 虛擬機器新增至網域</span><span class="sxs-lookup"><span data-stu-id="5ff84-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="5ff84-708">將靜態 IP 位址指派給虛擬機器之後，請將虛擬機器新增至網域。</span><span class="sxs-lookup"><span data-stu-id="5ff84-708">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![圖 17：將虛擬機器新增至網域][sap-ha-guide-figure-3006]

<span data-ttu-id="5ff84-710">_**圖 17：**將虛擬機器新增至網域_</span><span class="sxs-lookup"><span data-stu-id="5ff84-710">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="5ff84-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> 在 SAP ASCS/SCS 執行個體的兩個叢集節點上都新增登錄項目</span><span class="sxs-lookup"><span data-stu-id="5ff84-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="5ff84-712">Azure Load Balancer 具有內部負載平衡器，會在連線閒置一段時間 (閒置逾時) 時關閉連線。</span><span class="sxs-lookup"><span data-stu-id="5ff84-712">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="5ff84-713">對話方塊執行個體中的 SAP 工作程序則會在需要傳送第一個加入佇列/清除佇列要求時，立即開啟對SAP 加入佇列程序的連線。</span><span class="sxs-lookup"><span data-stu-id="5ff84-713">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="5ff84-714">這些連線通常會持續維持已建立狀態，直到工作程序或加入佇列程序重新啟動為止。</span><span class="sxs-lookup"><span data-stu-id="5ff84-714">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="5ff84-715">不過，如果連線閒置一段時間，Azure 內部負載平衡器就會關閉連線。</span><span class="sxs-lookup"><span data-stu-id="5ff84-715">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="5ff84-716">這不是問題，因為如果連線不存在，SAP 工作程序會對加入佇列程序重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="5ff84-716">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="5ff84-717">這些活動會記載於 SAP 程序的開發人員追蹤，但它們會對這些追蹤建立大量額外的內容。</span><span class="sxs-lookup"><span data-stu-id="5ff84-717">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="5ff84-718">因此，最好先變更兩個叢集節點上的 TCP/IP `KeepAliveTime` 和 `KeepAliveInterval`。</span><span class="sxs-lookup"><span data-stu-id="5ff84-718">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="5ff84-719">結合這些 TCP/IP 參數中的變更與 SAP 設定檔參數中的變更，稍後在本文中會加以描述。</span><span class="sxs-lookup"><span data-stu-id="5ff84-719">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="5ff84-720">若要在 SAP ASCS/SCS 執行個體的兩個叢集節點上新增登錄項目，首先，在 SAP ASCS/SCS 的兩個 Windows 叢集節點上新增這些 Windows 登錄項目︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-720">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="5ff84-721">路徑</span><span class="sxs-lookup"><span data-stu-id="5ff84-721">Path</span></span> | <span data-ttu-id="5ff84-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="5ff84-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="5ff84-723">變數名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-723">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="5ff84-724">變數類型</span><span class="sxs-lookup"><span data-stu-id="5ff84-724">Variable type</span></span> |<span data-ttu-id="5ff84-725">REG_DWORD (十進位)</span><span class="sxs-lookup"><span data-stu-id="5ff84-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="5ff84-726">值</span><span class="sxs-lookup"><span data-stu-id="5ff84-726">Value</span></span> |<span data-ttu-id="5ff84-727">120000</span><span class="sxs-lookup"><span data-stu-id="5ff84-727">120000</span></span> |
| <span data-ttu-id="5ff84-728">文件連結</span><span class="sxs-lookup"><span data-stu-id="5ff84-728">Link to documentation</span></span> |[<span data-ttu-id="5ff84-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="5ff84-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="5ff84-730">_**表 3：**變更第一個 TCP/IP 參數_</span><span class="sxs-lookup"><span data-stu-id="5ff84-730">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="5ff84-731">然後，在 SAP ASCS/SCS 的兩個 Windows 叢集節點上都新增下列 Windows 登錄項目：</span><span class="sxs-lookup"><span data-stu-id="5ff84-731">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="5ff84-732">路徑</span><span class="sxs-lookup"><span data-stu-id="5ff84-732">Path</span></span> | <span data-ttu-id="5ff84-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="5ff84-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="5ff84-734">變數名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-734">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="5ff84-735">變數類型</span><span class="sxs-lookup"><span data-stu-id="5ff84-735">Variable type</span></span> |<span data-ttu-id="5ff84-736">REG_DWORD (十進位)</span><span class="sxs-lookup"><span data-stu-id="5ff84-736">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="5ff84-737">值</span><span class="sxs-lookup"><span data-stu-id="5ff84-737">Value</span></span> |<span data-ttu-id="5ff84-738">120000</span><span class="sxs-lookup"><span data-stu-id="5ff84-738">120000</span></span> |
| <span data-ttu-id="5ff84-739">文件連結</span><span class="sxs-lookup"><span data-stu-id="5ff84-739">Link to documentation</span></span> |[<span data-ttu-id="5ff84-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="5ff84-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="5ff84-741">_**表 4：**變更第二個 TCP/IP 參數_</span><span class="sxs-lookup"><span data-stu-id="5ff84-741">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="5ff84-742">**若要套用變更，請重新啟動這兩個叢集節點**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-742">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="5ff84-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> 設定 SAP ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="5ff84-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="5ff84-744">設定 SAP ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-744">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="5ff84-745">收集叢集組態中的叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-745">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="5ff84-746">設定叢集檔案共用見證</span><span class="sxs-lookup"><span data-stu-id="5ff84-746">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="5ff84-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> 收集叢集組態中的叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="5ff84-748">在新增角色及功能精靈中，將容錯移轉叢集新增至這兩個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-748">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="5ff84-749">使用 [容錯移轉叢集管理員] 來設定容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5ff84-749">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="5ff84-750">在容錯移轉叢集管理員中，選取 [建立叢集]，然後僅新增第一個叢集、節點 A 的名稱。還不要新增第二個節點；您將在稍後的步驟新增第二個節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-750">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![圖 18：加入第一個叢集節點的伺服器或虛擬機器名稱][sap-ha-guide-figure-3007]

  <span data-ttu-id="5ff84-752">_**圖 18：**加入第一個叢集節點的伺服器或虛擬機器名稱_</span><span class="sxs-lookup"><span data-stu-id="5ff84-752">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="5ff84-753">輸入叢集的網路名稱 (虛擬主機名稱)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-753">Enter the network name (virtual host name) of the cluster.</span></span>

  ![圖 19︰輸入叢集名稱][sap-ha-guide-figure-3008]

  <span data-ttu-id="5ff84-755">_**圖 19︰**輸入叢集名稱_</span><span class="sxs-lookup"><span data-stu-id="5ff84-755">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="5ff84-756">建立叢集之後，會執行叢集驗證測試。</span><span class="sxs-lookup"><span data-stu-id="5ff84-756">After you've created the cluster, run a cluster validation test.</span></span>

  ![圖 20：執行叢集驗證檢查][sap-ha-guide-figure-3009]

  <span data-ttu-id="5ff84-758">_**圖 20：**執行叢集驗證檢查_</span><span class="sxs-lookup"><span data-stu-id="5ff84-758">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="5ff84-759">您可以忽略此時程序中有關磁碟的任何警告。</span><span class="sxs-lookup"><span data-stu-id="5ff84-759">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="5ff84-760">稍後您將新增檔案共用見證與 SIOS 共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-760">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="5ff84-761">在這個階段，您不必擔心有仲裁。</span><span class="sxs-lookup"><span data-stu-id="5ff84-761">At this stage, you don't need to worry about having a quorum.</span></span>

  ![圖 21：找不到仲裁磁碟][sap-ha-guide-figure-3010]

  <span data-ttu-id="5ff84-763">_**圖 21：**_</span><span class="sxs-lookup"><span data-stu-id="5ff84-763">_**Figure 21:** No quorum disk is found_</span></span>

  ![圖 22：核心叢集資源需要新的 IP 位址][sap-ha-guide-figure-3011]

  <span data-ttu-id="5ff84-765">_**圖 22：**核心叢集資源需要新的 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="5ff84-765">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="5ff84-766">變更核心叢集服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ff84-766">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="5ff84-767">直到您變更核心叢集服務的 IP 位址之前皆無法啟動叢集，因為伺服器的 IP 位址指向其中一個虛擬機器節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-767">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="5ff84-768">在核心叢集服務 IP 資源的**屬性**頁面上執行此動作。</span><span class="sxs-lookup"><span data-stu-id="5ff84-768">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="5ff84-769">例如，我們需要為叢集虛擬主機名稱 **pr1-ascs-vir** 指派 IP 位址 (在我們的範例中為 **10.0.0.42**)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-769">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![圖 23：在 [屬性] 對話方塊中，變更 IP 位址][sap-ha-guide-figure-3012]

  <span data-ttu-id="5ff84-771">_**圖 23：**在 [屬性]  對話方塊中，變更 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="5ff84-771">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![圖 24：指派為叢集保留的 IP 位址][sap-ha-guide-figure-3013]

  <span data-ttu-id="5ff84-773">_**圖 24：**指派為叢集保留的 IP 位址_</span><span class="sxs-lookup"><span data-stu-id="5ff84-773">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="5ff84-774">將叢集虛擬主機名稱上線。</span><span class="sxs-lookup"><span data-stu-id="5ff84-774">Bring the cluster virtual host name online.</span></span>

  ![圖 25：叢集核心服務以正確的 IP 位址啟動並正常執行][sap-ha-guide-figure-3014]

  <span data-ttu-id="5ff84-776">_**圖 25：**叢集核心服務以正確的 IP 位址啟動並正常執行_</span><span class="sxs-lookup"><span data-stu-id="5ff84-776">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="5ff84-777">新增第二個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-777">Add the second cluster node.</span></span>

  <span data-ttu-id="5ff84-778">既然核心叢集服務已啟動並正常執行，您便可以新增第二個叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-778">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![圖 26：新增第二個叢集節點][sap-ha-guide-figure-3015]

  <span data-ttu-id="5ff84-780">_**圖 26：**_</span><span class="sxs-lookup"><span data-stu-id="5ff84-780">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="5ff84-781">輸入第二個叢集節點主機的名稱。</span><span class="sxs-lookup"><span data-stu-id="5ff84-781">Enter a name for the second cluster node host.</span></span>

  ![圖 27︰輸入第二個叢集節點主機名稱][sap-ha-guide-figure-3016]

  <span data-ttu-id="5ff84-783">_**圖 27︰**輸入第二個叢集節點主機名稱_</span><span class="sxs-lookup"><span data-stu-id="5ff84-783">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5ff84-784">請確定**沒有**選取 [新增適合的儲存裝置到叢集] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5ff84-784">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![圖 28：請勿選取核取方塊][sap-ha-guide-figure-3017]

  <span data-ttu-id="5ff84-786">_**圖 28：**請**勿**選取核取方塊_</span><span class="sxs-lookup"><span data-stu-id="5ff84-786">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="5ff84-787">您可以忽略有關仲裁和磁碟的警告。</span><span class="sxs-lookup"><span data-stu-id="5ff84-787">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="5ff84-788">您將在稍後設定仲裁和共用磁碟，如[為 SAP ASCS/SCS 叢集共用磁碟安裝 SIOS DataKeeper Cluster Edition][sap-ha-guide-8.12.3] 中所述。</span><span class="sxs-lookup"><span data-stu-id="5ff84-788">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![圖 29：忽略有關磁碟仲裁的警告][sap-ha-guide-figure-3018]

  <span data-ttu-id="5ff84-790">_**圖 29：**忽略有關磁碟仲裁的警告_</span><span class="sxs-lookup"><span data-stu-id="5ff84-790">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="5ff84-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> 設定叢集檔案共用見證</span><span class="sxs-lookup"><span data-stu-id="5ff84-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="5ff84-792">設定叢集檔案共用見證包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-792">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="5ff84-793">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="5ff84-793">Creating a file share</span></span>
- <span data-ttu-id="5ff84-794">在容錯移轉叢集管理員中設定檔案共用見證仲裁</span><span class="sxs-lookup"><span data-stu-id="5ff84-794">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="5ff84-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> 建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="5ff84-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="5ff84-796">選取檔案共用見證，而不是仲裁磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-796">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="5ff84-797">SIOS DataKeeper 支援此選項。</span><span class="sxs-lookup"><span data-stu-id="5ff84-797">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="5ff84-798">在本文的範例中，檔案共用見證是在 Azure 中執行的 Active Directory/DNS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5ff84-798">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="5ff84-799">檔案共用見證稱為 **domcontr-0**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-799">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="5ff84-800">因為您已設定 Azure 的 VPN 連線 (透過網站間 VPN 或 Azure ExpressRoute)，所以您的 Active Directory/DNS 服務是內部部署，而且不適用於執行檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="5ff84-800">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5ff84-801">如果您的 Active Directory/DNS 服務僅在內部部署上執行，請勿在執行內部部署的 Active Directory/DNS Windows 作業系統上設定檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="5ff84-801">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="5ff84-802">在 Azure 和 Active Directory DNS 內部部署中執行之叢集節點之間的網路延遲可能太大，而且會造成連線問題。</span><span class="sxs-lookup"><span data-stu-id="5ff84-802">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="5ff84-803">請務必在執行位置靠近叢集節點的 Azure 虛擬機器上設定檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="5ff84-803">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="5ff84-804">仲裁磁碟機至少需要 1,024 MB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="5ff84-804">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="5ff84-805">我們建議使用 2,048 MB 的仲裁磁碟機可用空間。</span><span class="sxs-lookup"><span data-stu-id="5ff84-805">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="5ff84-806">新增叢集名稱物件。</span><span class="sxs-lookup"><span data-stu-id="5ff84-806">Add the cluster name object.</span></span>

  ![圖 30：為叢集名稱物件指派共用上的權限][sap-ha-guide-figure-3019]

  <span data-ttu-id="5ff84-808">_**圖 30：**為叢集名稱物件指派共用上的權限_</span><span class="sxs-lookup"><span data-stu-id="5ff84-808">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="5ff84-809">請確定權限能夠為叢集名稱物件 (在我們的範例中為 **pr1-ascs-vir$**) 變更共用中的資料。</span><span class="sxs-lookup"><span data-stu-id="5ff84-809">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="5ff84-810">若要將叢集名稱物件新增至清單中，請選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-810">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="5ff84-811">變更篩選，以檢查電腦物件，除了圖 31 所示的項目以外。</span><span class="sxs-lookup"><span data-stu-id="5ff84-811">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![圖 31：變更物件類型以包含電腦][sap-ha-guide-figure-3020]

  <span data-ttu-id="5ff84-813">_**圖 31：**變更物件類型以包含電腦_</span><span class="sxs-lookup"><span data-stu-id="5ff84-813">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![圖 32︰選取電腦核取方塊][sap-ha-guide-figure-3021]

  <span data-ttu-id="5ff84-815">_**圖 32︰**選取**電腦**核取方塊_</span><span class="sxs-lookup"><span data-stu-id="5ff84-815">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="5ff84-816">輸入叢集名稱物件，如圖 31 所示。</span><span class="sxs-lookup"><span data-stu-id="5ff84-816">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="5ff84-817">由於已經建立記錄，因此您可以變更權限，如圖 30 所示。</span><span class="sxs-lookup"><span data-stu-id="5ff84-817">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="5ff84-818">選取共用的 [安全性] 索引標籤，然後為叢集名稱物件設定更詳細的權限。</span><span class="sxs-lookup"><span data-stu-id="5ff84-818">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![圖 33：為叢集名稱物件設定檔案共用仲裁上的安全性屬性][sap-ha-guide-figure-3022]

  <span data-ttu-id="5ff84-820">_**圖 33：**為叢集名稱物件設定檔案共用仲裁上的安全性屬性_</span><span class="sxs-lookup"><span data-stu-id="5ff84-820">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="5ff84-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> 在容錯移轉叢集管理員中設定檔案共用見證仲裁</span><span class="sxs-lookup"><span data-stu-id="5ff84-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="5ff84-822">開啟設定仲裁設定精靈。</span><span class="sxs-lookup"><span data-stu-id="5ff84-822">Open the Configure Quorum Setting Wizard.</span></span>

  ![圖 34：啟動設定叢集仲裁設定精靈][sap-ha-guide-figure-3023]

  <span data-ttu-id="5ff84-824">_**圖 34：**啟動設定叢集仲裁設定精靈_</span><span class="sxs-lookup"><span data-stu-id="5ff84-824">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="5ff84-825">在 [選取仲裁設定] 頁面上，選取 [選取仲裁見證]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-825">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![圖 35：您可以選擇的仲裁組態][sap-ha-guide-figure-3024]

  <span data-ttu-id="5ff84-827">_**圖 35：**您可以選擇的仲裁組態_</span><span class="sxs-lookup"><span data-stu-id="5ff84-827">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="5ff84-828">在 [選取仲裁見證] 頁面上，選取 [設定檔案共用見證]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-828">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![圖 36︰選取檔案共用見證][sap-ha-guide-figure-3025]

  <span data-ttu-id="5ff84-830">_**圖 36︰**選取檔案共用見證_</span><span class="sxs-lookup"><span data-stu-id="5ff84-830">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="5ff84-831">輸入檔案共用的 UNC 路徑 (在我們的範例中為 \\domcontr-0\FSW)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-831">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="5ff84-832">若要查看您可進行變更的清單，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-832">To see a list of the changes you can make, select **Next**.</span></span>

  ![圖 37：定義見證共用的檔案共用位置][sap-ha-guide-figure-3026]

  <span data-ttu-id="5ff84-834">_**圖 37：**定義見證共用的檔案共用位置_</span><span class="sxs-lookup"><span data-stu-id="5ff84-834">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="5ff84-835">選取您要的變更，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-835">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="5ff84-836">您需要成功重新設定叢集組態，如圖 38 中所示。</span><span class="sxs-lookup"><span data-stu-id="5ff84-836">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![圖 38：確認您已重新設定叢集][sap-ha-guide-figure-3027]

  <span data-ttu-id="5ff84-838">_**圖 38：**確認您已重新設定叢集_</span><span class="sxs-lookup"><span data-stu-id="5ff84-838">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="5ff84-839">成功安裝 Windows 容錯移轉叢集之後，有些閾值需要變更，讓容錯移轉偵測適應 Azure 中的條件。</span><span class="sxs-lookup"><span data-stu-id="5ff84-839">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="5ff84-840">需要變更的參數記載於此部落格中︰https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/。</span><span class="sxs-lookup"><span data-stu-id="5ff84-840">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="5ff84-841">假設為 ASCS/SCS 建置 Windows 叢集組態的兩部 VM 位於相同子網路中，則必須將下列參數變更為這些值︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-841">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="5ff84-842">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="5ff84-842">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="5ff84-843">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="5ff84-843">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="5ff84-844">這些設定已經過客戶測試，一方面提供有足夠彈性的折衷辦法。</span><span class="sxs-lookup"><span data-stu-id="5ff84-844">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="5ff84-845">另一方面，這些設定會在 SAP 軟體或節點/VM 失敗的真實錯誤情況中，提供夠快的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5ff84-845">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="5ff84-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> 為 SAP ASCS/SCS 叢集共用磁碟安裝 SIOS DataKeeper Cluster Edition</span><span class="sxs-lookup"><span data-stu-id="5ff84-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="5ff84-847">您現在在 Azure 中有運作中的 Windows Server 容錯移轉叢集組態。</span><span class="sxs-lookup"><span data-stu-id="5ff84-847">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="5ff84-848">但是，若要安裝 SAP ASCS/SCS 執行個體，您需要有一個共用磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-848">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="5ff84-849">您無法在 Azure 中建立所需的共用磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-849">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="5ff84-850">SIOS DataKeeper Cluster Edition 是一種可用來建立共用磁碟資源的協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="5ff84-850">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="5ff84-851">為 SAP ASCS/SCS 叢集共用磁碟安裝 SIOS DataKeeper Cluster Edition 包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-851">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="5ff84-852">新增 .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="5ff84-852">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="5ff84-853">安裝 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5ff84-853">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="5ff84-854">設定 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5ff84-854">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="5ff84-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> 新增 .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="5ff84-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="5ff84-856">Microsoft .NET Framework 3.5 不會自動啟用或安裝在 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="5ff84-856">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="5ff84-857">因為 SIOS DataKeeper 需要 .NET Framework 位於您安裝 DataKeeper 的所有節點上，您必須在叢集中所有虛擬機器的客體作業系統上安裝 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="5ff84-857">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="5ff84-858">有兩種方式可以新增 .NET Framework 3.5：</span><span class="sxs-lookup"><span data-stu-id="5ff84-858">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="5ff84-859">在 Windows 中使用 [新增角色及功能精靈]，如圖 39 所示。</span><span class="sxs-lookup"><span data-stu-id="5ff84-859">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![圖 39：使用 [新增角色及功能精靈] 安裝 .NET Framework 3.5][sap-ha-guide-figure-3028]

  <span data-ttu-id="5ff84-861">_**圖 39：**使用 [新增角色及功能精靈] 安裝 .NET Framework 3.5_</span><span class="sxs-lookup"><span data-stu-id="5ff84-861">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![圖 40︰當您使用 [新增角色及功能精靈] 安裝 .NET Framework 3.5 時的安裝進度列][sap-ha-guide-figure-3029]

  <span data-ttu-id="5ff84-863">_**圖 40︰**當您使用 [新增角色及功能精靈] 安裝 .NET Framework 3.5 時的安裝進度列_</span><span class="sxs-lookup"><span data-stu-id="5ff84-863">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="5ff84-864">使用命令列工具 dism.exe。</span><span class="sxs-lookup"><span data-stu-id="5ff84-864">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="5ff84-865">針對這類型的安裝，您需要存取 Windows 安裝媒體上的 SxS 目錄。</span><span class="sxs-lookup"><span data-stu-id="5ff84-865">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="5ff84-866">在提高權限的命令提示字元上，輸入：</span><span class="sxs-lookup"><span data-stu-id="5ff84-866">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="5ff84-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> 安裝 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5ff84-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="5ff84-868">在叢集中的每個節點上安裝 SIOS DataKeeper Cluster Edition。</span><span class="sxs-lookup"><span data-stu-id="5ff84-868">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="5ff84-869">若要使用 SIOS DataKeeper 建立虛擬共用儲存體，請建立同步處理的鏡像，然後模擬叢集共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-869">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="5ff84-870">安裝 SIOS 軟體之前，請先建立網域使用者 **DataKeeperSvc**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-870">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-871">將 **DataKeeperSvc** 使用者同時新增到兩個叢集節點上的 [本機管理員] 群組中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-871">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="5ff84-872">若要安裝 SIOS DataKeeper：</span><span class="sxs-lookup"><span data-stu-id="5ff84-872">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="5ff84-873">在兩個叢集節點上都安裝 SIOS 軟體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-873">Install the SIOS software on both cluster nodes.</span></span>

  ![SIOS 安裝程式][sap-ha-guide-figure-3030]

  ![圖 41：第一個 SIOS DataKeeper 安裝頁面][sap-ha-guide-figure-3031]

  <span data-ttu-id="5ff84-876">_**圖 41：**第一個 SIOS DataKeeper 安裝頁面_</span><span class="sxs-lookup"><span data-stu-id="5ff84-876">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="5ff84-877">在圖 42 所示的對話方塊中，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-877">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![圖 42：DataKeeper 通知將停用某個服務][sap-ha-guide-figure-3032]

  <span data-ttu-id="5ff84-879">_**圖 42：**DataKeeper 通知將停用某個服務_</span><span class="sxs-lookup"><span data-stu-id="5ff84-879">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="5ff84-880">在圖 43 顯示的對話方塊中，建議您選取 [網域或伺服器帳戶]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-880">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![圖 43：SIOS DataKeeper 的使用者選項][sap-ha-guide-figure-3033]

  <span data-ttu-id="5ff84-882">_**圖 43：**SIOS DataKeeper 的使用者選項_</span><span class="sxs-lookup"><span data-stu-id="5ff84-882">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="5ff84-883">輸入您為 SIOS DataKeeper 建立的網域帳戶使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-883">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![圖 44：為 SIOS DataKeeper 安裝輸入網域使用者名稱和密碼][sap-ha-guide-figure-3034]

  <span data-ttu-id="5ff84-885">_**圖 44：**為 SIOS DataKeeper 安裝輸入網域使用者名稱和密碼_</span><span class="sxs-lookup"><span data-stu-id="5ff84-885">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="5ff84-886">為您的 SIOS DataKeeper 執行個體安裝授權金鑰，如圖 45 所示。</span><span class="sxs-lookup"><span data-stu-id="5ff84-886">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![圖 45：輸入您的 SIOS DataKeeper 授權金鑰][sap-ha-guide-figure-3035]

  <span data-ttu-id="5ff84-888">_**圖 45：**輸入您的 SIOS DataKeeper 授權金鑰_</span><span class="sxs-lookup"><span data-stu-id="5ff84-888">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="5ff84-889">出現提示時，重新啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5ff84-889">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="5ff84-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> 設定 SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5ff84-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="5ff84-891">在兩個節點上都安裝 SIOS DataKeeper 之後，您必須開始設定組態。</span><span class="sxs-lookup"><span data-stu-id="5ff84-891">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="5ff84-892">組態的目標是要在連接至每個虛擬機器的額外磁碟之間進行同步資料複寫。</span><span class="sxs-lookup"><span data-stu-id="5ff84-892">The goal of the configuration is to have synchronous data replication between the additional disks attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="5ff84-893">啟動 DataKeeper 管理與組態工具，然後選取 [連線伺服器]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-893">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="5ff84-894">(在圖 46 中，此選項是用紅色圈起來的部分。)</span><span class="sxs-lookup"><span data-stu-id="5ff84-894">(In Figure 46, this option is circled in red.)</span></span>

  ![圖 46：SIOS DataKeeper 管理和組態工具][sap-ha-guide-figure-3036]

  <span data-ttu-id="5ff84-896">_**圖 46：**SIOS DataKeeper 管理和組態工具_</span><span class="sxs-lookup"><span data-stu-id="5ff84-896">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="5ff84-897">輸入管理和組態工具應連接之第一個節點的名稱或 TCP/IP 位址，然後在第二個步驟中，插入第二個節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-897">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![圖 47：插入管理和組態工具應連接之第一個節點的名稱或 TCP/IP 位址，然後在第二個步驟中，插入第二個節點][sap-ha-guide-figure-3037]

  <span data-ttu-id="5ff84-899">_**圖 47：**插入管理和組態工具應連接之第一個節點的名稱或 TCP/IP 位址，然後在第二個步驟中，插入第二個節點_</span><span class="sxs-lookup"><span data-stu-id="5ff84-899">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="5ff84-900">在兩個節點之間建立複寫作業。</span><span class="sxs-lookup"><span data-stu-id="5ff84-900">Create the replication job between the two nodes.</span></span>

  ![圖 48：建立複寫作業][sap-ha-guide-figure-3038]

  <span data-ttu-id="5ff84-902">_**圖 48：**建立複寫作業_</span><span class="sxs-lookup"><span data-stu-id="5ff84-902">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="5ff84-903">精靈會引導您完成建立複寫作業的程序。</span><span class="sxs-lookup"><span data-stu-id="5ff84-903">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="5ff84-904">定義名稱、TCP/IP 位址和來源節點的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ff84-904">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![圖 49：定義複寫作業的名稱][sap-ha-guide-figure-3039]

  <span data-ttu-id="5ff84-906">_**圖 49：**定義複寫作業的名稱_</span><span class="sxs-lookup"><span data-stu-id="5ff84-906">_**Figure 49:** Define the name of the replication job_</span></span>

  ![圖 50：定義節點 (應該是目前的來源節點) 的基底資料][sap-ha-guide-figure-3040]

  <span data-ttu-id="5ff84-908">_**圖 50：**定義節點 (應該是目前的來源節點) 的基底資料_</span><span class="sxs-lookup"><span data-stu-id="5ff84-908">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="5ff84-909">定義名稱、TCP/IP 位址和目標節點的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ff84-909">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![圖 51：定義節點 (應該是目前的目標節點) 的基底資料][sap-ha-guide-figure-3041]

  <span data-ttu-id="5ff84-911">_**圖 51：**定義節點 (應該是目前的目標節點) 的基底資料_</span><span class="sxs-lookup"><span data-stu-id="5ff84-911">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="5ff84-912">定義壓縮演算法。</span><span class="sxs-lookup"><span data-stu-id="5ff84-912">Define the compression algorithms.</span></span> <span data-ttu-id="5ff84-913">在我們的範例中，建議壓縮複寫資料流。</span><span class="sxs-lookup"><span data-stu-id="5ff84-913">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="5ff84-914">尤其是在重新同步處理的情況下，壓縮複寫資料流可大幅縮短重新同步處理時間。</span><span class="sxs-lookup"><span data-stu-id="5ff84-914">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="5ff84-915">請注意，壓縮會使用虛擬機器的 CPU 和 RAM 資源。</span><span class="sxs-lookup"><span data-stu-id="5ff84-915">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="5ff84-916">隨著壓縮率增加，使用的 CPU 資源數量也跟著增加。</span><span class="sxs-lookup"><span data-stu-id="5ff84-916">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="5ff84-917">您也可以稍後調整此設定。</span><span class="sxs-lookup"><span data-stu-id="5ff84-917">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="5ff84-918">另一個您需要檢查的設定是複寫是以非同步方式還是同步方式進行。</span><span class="sxs-lookup"><span data-stu-id="5ff84-918">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="5ff84-919">*當您保護 SAP ASCS/SCS 組態時，您必須使用同步複寫*。</span><span class="sxs-lookup"><span data-stu-id="5ff84-919">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![圖 52︰定義複寫詳細資料][sap-ha-guide-figure-3042]

  <span data-ttu-id="5ff84-921">_**圖 52︰**定義複寫詳細資料_</span><span class="sxs-lookup"><span data-stu-id="5ff84-921">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="5ff84-922">定義是否應該向 Windows Server 容錯移轉叢集的叢集組態指出複寫作業所複寫的磁碟區是共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-922">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="5ff84-923">就 SAP ASCS/SCS 組態而言，選取 [是] ，如此 Windows 叢集才會將複寫的磁碟區視為可用來作為叢集磁碟區的共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-923">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![圖 53：選取 [是] 以將複寫的磁碟區設定為叢集磁碟區][sap-ha-guide-figure-3043]

  <span data-ttu-id="5ff84-925">_**圖 53：**選取 [是] 以將複寫的磁碟區設定為叢集磁碟區_</span><span class="sxs-lookup"><span data-stu-id="5ff84-925">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="5ff84-926">建立磁碟區之後，DataKeeper 管理和組態工具會顯示複寫作業是使用中。</span><span class="sxs-lookup"><span data-stu-id="5ff84-926">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![圖 54：SAP ASCS/SCS 共用磁碟的 DataKeeper 同步鏡像處於作用中狀態][sap-ha-guide-figure-3044]

  <span data-ttu-id="5ff84-928">_**圖 54：**SAP ASCS/SCS 共用磁碟的 DataKeeper 同步鏡像處於作用中狀態_</span><span class="sxs-lookup"><span data-stu-id="5ff84-928">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="5ff84-929">「容錯移轉叢集管理員」現在會顯示磁碟為 DataKeeper 磁碟，如圖 55 所示。</span><span class="sxs-lookup"><span data-stu-id="5ff84-929">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![圖 55：「容錯移轉叢集管理員」顯示 DataKeeper 複寫的磁碟][sap-ha-guide-figure-3045]

  <span data-ttu-id="5ff84-931">_**圖 55：**「容錯移轉叢集管理員」顯示 DataKeeper 複寫的磁碟_</span><span class="sxs-lookup"><span data-stu-id="5ff84-931">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="5ff84-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> 安裝 SAP NetWeaver 系統</span><span class="sxs-lookup"><span data-stu-id="5ff84-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="5ff84-933">我們將不會說明 DBMS 設定，因為設定會視您使用的 DBMS 系統而異。</span><span class="sxs-lookup"><span data-stu-id="5ff84-933">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="5ff84-934">不過，我們會假設 DBMS 在高可用性方面的疑慮已藉由不同 DBMS 廠商為 Azure 提供的功能支援而獲得解決。</span><span class="sxs-lookup"><span data-stu-id="5ff84-934">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="5ff84-935">例如，適用於 SQL Server 的 Always On 或資料庫鏡像，以及適用於 Oracle 資料庫的 Oracle Data Guard。</span><span class="sxs-lookup"><span data-stu-id="5ff84-935">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="5ff84-936">在本文使用的案例中，我們並未對 DBMS 加入更多保護。</span><span class="sxs-lookup"><span data-stu-id="5ff84-936">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="5ff84-937">當不同的 DBMS 服務與 Azure 中這種叢集 SAP ASCS/SCS 組態互動時，沒有任何特殊的考量。</span><span class="sxs-lookup"><span data-stu-id="5ff84-937">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-938">SAP NetWeaver ABAP 系統、Java 系統及 ABAP+Java 系統的安裝程序幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="5ff84-938">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="5ff84-939">最顯著的差異在於 SAP ABAP 系統有一個 ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-939">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="5ff84-940">SAP Java 系統有一個 SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-940">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="5ff84-941">SAP ABAP+Java 系統有一個 ASCS 執行個體和一個 SCS 執行個體在相同 Microsoft 容錯移轉叢集群組中執行。</span><span class="sxs-lookup"><span data-stu-id="5ff84-941">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="5ff84-942">我們會明確說明每個 SAP NetWeaver 安裝堆疊的所有安裝差異。</span><span class="sxs-lookup"><span data-stu-id="5ff84-942">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="5ff84-943">您可以假設所有其他部分都相同。</span><span class="sxs-lookup"><span data-stu-id="5ff84-943">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="5ff84-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> 使用高可用性 ASCS/SCS 執行個體安裝 SAP</span><span class="sxs-lookup"><span data-stu-id="5ff84-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ff84-945">請不要將分頁檔放在 DataKeeper 鏡像磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="5ff84-945">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="5ff84-946">DataKeeper 不支援鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ff84-946">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="5ff84-947">您可以將分頁檔留在 Azure 虛擬機器的暫存磁碟機 D 中，此為預設值。</span><span class="sxs-lookup"><span data-stu-id="5ff84-947">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="5ff84-948">如果還不在此磁碟機中，請將 Windows 分頁檔移至 Azure 虛擬機器的磁碟機 D:。</span><span class="sxs-lookup"><span data-stu-id="5ff84-948">If it's not already there, move the Windows page file to drive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="5ff84-949">使用高可用性 ASCS/SCS 執行個體安裝 SAP 包含下列工作︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-949">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="5ff84-950">建立叢集 SAP ASCS/SCS 執行個體的虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-950">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="5ff84-951">安裝 SAP 的第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-951">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="5ff84-952">修改 ASCS/SCS 執行個體的 SAP 設定檔</span><span class="sxs-lookup"><span data-stu-id="5ff84-952">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="5ff84-953">新增探查連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-953">Adding a probe port</span></span>
- <span data-ttu-id="5ff84-954">開啟 Windows 防火牆探查連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-954">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="5ff84-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> 建立叢集 SAP ASCS/SCS 執行個體的虛擬主機名稱</span><span class="sxs-lookup"><span data-stu-id="5ff84-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="5ff84-956">在「Windows DNS 管理員」中，為 ASCS/SCS 執行個體的虛擬主機名稱建立 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="5ff84-956">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5ff84-957">您指派給 ASCS/SCS 執行個體之虛擬主機名稱的 IP 位址必須與指派給 Azure Load Balancer (**<*SID*>-lb-ascs**) 的 IP 位址相同。</span><span class="sxs-lookup"><span data-stu-id="5ff84-957">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="5ff84-958">虛擬 SAP ASCS/SCS 主機名稱 (**pr1-ascs-sap**) 的 IP 位址與 Azure Load Balancer (**pr1-lb-ascs**) 的 IP 位址相同。</span><span class="sxs-lookup"><span data-stu-id="5ff84-958">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![圖 56：定義 SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目][sap-ha-guide-figure-3046]

  <span data-ttu-id="5ff84-960">_**圖 56：**定義 SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目_</span><span class="sxs-lookup"><span data-stu-id="5ff84-960">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="5ff84-961">若要定義指派給虛擬主機名稱的 IP 位址，選取 [DNS 管理員] > [網域]</span><span class="sxs-lookup"><span data-stu-id="5ff84-961">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![圖 57：SAP ASCS/SCS 叢集組態的新虛擬名稱和 TCP/IP 位址][sap-ha-guide-figure-3047]

  <span data-ttu-id="5ff84-963">_**圖 57：**SAP ASCS/SCS 叢集組態的新虛擬名稱和 TCP/IP 位址_</span><span class="sxs-lookup"><span data-stu-id="5ff84-963">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="5ff84-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> 安裝 SAP 的第一個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="5ff84-965">在叢集節點 A 上執行第一個叢集節點選項。例如，在 **pr1-ascs-0** 主機上。</span><span class="sxs-lookup"><span data-stu-id="5ff84-965">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="5ff84-966">如果要為 Azure 內部負載平衡器保留預設連接埠，請選取：</span><span class="sxs-lookup"><span data-stu-id="5ff84-966">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="5ff84-967">**ABAP 系統**：**ASCS** 執行個體號碼 **00**</span><span class="sxs-lookup"><span data-stu-id="5ff84-967">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="5ff84-968">**Java 系統**：**SCS** 執行個體號碼 **01**</span><span class="sxs-lookup"><span data-stu-id="5ff84-968">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="5ff84-969">**ABAP+Java 系統**：**ASCS** 執行個體號碼 **00** 和 **SCS** 執行個體號碼 **01**</span><span class="sxs-lookup"><span data-stu-id="5ff84-969">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="5ff84-970">如果要針對 ABAP ASCS 執行個體使用 00 以外的執行個體號碼，以及針對 Java SCS 執行個體使用 01 以外的執行個體號碼，您必須先變更 Azure 內部負載平衡器預設的負載平衡規則，如[變更 Azure 內部負載平衡器的 ASCS/SCS 預設負載平衡規則所述][sap-ha-guide-8.9]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-970">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="5ff84-971">接下來幾個步驟並未在標準 SAP 安裝文件中說明。</span><span class="sxs-lookup"><span data-stu-id="5ff84-971">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-972">SAP 安裝文件說明如何安裝第一個 ASCS/SCS 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5ff84-972">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="5ff84-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> 修改 ASCS/SCS 執行個體的 SAP 設定檔</span><span class="sxs-lookup"><span data-stu-id="5ff84-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="5ff84-974">您需要新增新的設定檔參數。</span><span class="sxs-lookup"><span data-stu-id="5ff84-974">You need to add a new profile parameter.</span></span> <span data-ttu-id="5ff84-975">此設定檔參數可避免 SAP 工作程序與加入佇列伺服器之間的連線在閒置時間太長時關閉。</span><span class="sxs-lookup"><span data-stu-id="5ff84-975">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="5ff84-976">我們在本文中的[在 SAP ASCS/SCS 執行個體的兩個叢集節點上都新增登錄項目][sap-ha-guide-8.11]已提到問題案例。</span><span class="sxs-lookup"><span data-stu-id="5ff84-976">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="5ff84-977">在該部分，我們也介紹了對一些基本 TCP/IP 連線參數所做的兩項變更。</span><span class="sxs-lookup"><span data-stu-id="5ff84-977">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="5ff84-978">在第二個步驟中，您必須設定讓加入佇列伺服器傳送 `keep_alive` 訊號，如此連線才不會達到 Azure 內部負載平衡器的閒置臨界值。</span><span class="sxs-lookup"><span data-stu-id="5ff84-978">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="5ff84-979">若要修改 ASCS/SCS 執行個體的 SAP 設定檔：</span><span class="sxs-lookup"><span data-stu-id="5ff84-979">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="5ff84-980">將此設定檔參數新增至 SAP ASCS/SCS 執行個體設定檔：</span><span class="sxs-lookup"><span data-stu-id="5ff84-980">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="5ff84-981">在我們的範例中，路徑為：</span><span class="sxs-lookup"><span data-stu-id="5ff84-981">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="5ff84-982">例如，新增到 SAP SCS 執行個體設定檔和對應的路徑：</span><span class="sxs-lookup"><span data-stu-id="5ff84-982">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="5ff84-983">若要套用變更，請重新啟動 SAP ASCS /SCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ff84-983">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="5ff84-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> 新增探查連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="5ff84-985">使用內部負載平衡器探查功能，讓整個叢集組態使用 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="5ff84-985">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="5ff84-986">Azure 內部負載平衡器通常會在參與的虛擬機器之間，平均分配內送的工作負載。</span><span class="sxs-lookup"><span data-stu-id="5ff84-986">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="5ff84-987">不過，這對某些叢集組態不會產生作用，因為只有一個執行個體是主動的。</span><span class="sxs-lookup"><span data-stu-id="5ff84-987">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="5ff84-988">另一個執行個體是被動的，而且不接受任何工作負載。</span><span class="sxs-lookup"><span data-stu-id="5ff84-988">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="5ff84-989">Azure 內部負載平衡器僅將工作指派給主動的執行個體時，探查功能才可提供協助。</span><span class="sxs-lookup"><span data-stu-id="5ff84-989">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="5ff84-990">使用探查功能，內部負載平衡器便能夠偵測哪些執行個體是主動的，然後只以該執行個體作為工作負載的目標。</span><span class="sxs-lookup"><span data-stu-id="5ff84-990">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="5ff84-991">若要新增探查連接埠︰</span><span class="sxs-lookup"><span data-stu-id="5ff84-991">To add a probe port:</span></span>

1.  <span data-ttu-id="5ff84-992">執行 PowerShell 命令檢查目前 **ProbePort** 設定。</span><span class="sxs-lookup"><span data-stu-id="5ff84-992">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="5ff84-993">在叢集組態中的其中一個虛擬機器中執行該檢查。</span><span class="sxs-lookup"><span data-stu-id="5ff84-993">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="5ff84-994">定義探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="5ff84-994">Define a probe port.</span></span> <span data-ttu-id="5ff84-995">預設探查連接埠號碼為 **0**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-995">The default probe port number is **0**.</span></span> <span data-ttu-id="5ff84-996">在我們的範例中，我們會使用探查連接埠 **62000**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-996">In our example, we use probe port **62000**.</span></span>

  ![圖 58：叢集組態探查連接埠預設為 0][sap-ha-guide-figure-3048]

  <span data-ttu-id="5ff84-998">_**圖 58：**預設叢集組態探查連接埠為 0_</span><span class="sxs-lookup"><span data-stu-id="5ff84-998">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="5ff84-999">SAP Azure Resource Manager 範本中已定義連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-999">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="5ff84-1000">您可以在 PowerShell 中指派連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1000">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="5ff84-1001">若要針對 **SAP <*SID*> IP** 叢集資源設定新的 ProbePort 值，執行下列 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1001">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="5ff84-1002">請更新您環境的 PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1002">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="5ff84-1003">指令碼執行之後，系統會提示您重新啟動 SAP 叢集群組，以啟動變更。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1003">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

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
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

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

  <span data-ttu-id="5ff84-1004">讓 **SAP <*SID*>** 叢集角色上線之後，請確認 **ProbePort** 已設定為新值。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1004">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![圖 59：設定新值之後，探查叢集連接埠][sap-ha-guide-figure-3049]

  <span data-ttu-id="5ff84-1006">_**圖 59：**設定新值之後，探查叢集連接埠_</span><span class="sxs-lookup"><span data-stu-id="5ff84-1006">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="5ff84-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> 開啟 Windows 防火牆探查連接埠</span><span class="sxs-lookup"><span data-stu-id="5ff84-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="5ff84-1008">您需要開啟這兩個叢集節點上的 Windows 防火牆探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1008">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="5ff84-1009">使用下列指令碼開啟 Windows 防火牆探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1009">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="5ff84-1010">請更新您環境的 PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1010">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="5ff84-1011">**ProbePort** 已設為 **62000**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1011">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="5ff84-1012">現在您可以從其他主機存取檔案共用 **\\\ascsha-clsap\sapmnt**，例如從 **ascsha-dbas**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1012">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="5ff84-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> 安裝資料庫執行個體</span><span class="sxs-lookup"><span data-stu-id="5ff84-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="5ff84-1014">若要安裝資料庫執行個體，請依照 SAP 安裝文件中所述的程序。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1014">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="5ff84-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> 安裝第二個叢集節點</span><span class="sxs-lookup"><span data-stu-id="5ff84-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="5ff84-1016">若要安裝第二個叢集，請依照 SAP 安裝指南中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1016">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="5ff84-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> 變更 SAP ERS Windows 服務執行個體的啟動類型</span><span class="sxs-lookup"><span data-stu-id="5ff84-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="5ff84-1018">將兩個叢集節點上 SAP ERS Windows 服務的啟動類型都變更為 [自動 (延遲啟動)]。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1018">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![圖 60：將 SAP ERS 執行個體的服務類型變更為延遲的自動類型][sap-ha-guide-figure-3050]

<span data-ttu-id="5ff84-1020">_**圖 60：**將 SAP ERS 執行個體的服務類型變更為延遲的自動類型_</span><span class="sxs-lookup"><span data-stu-id="5ff84-1020">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="5ff84-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> 安裝 SAP 主要應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="5ff84-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="5ff84-1022">在您指派來裝載 PAS 的虛擬機器上安裝主要應用程式伺服器 (PAS) 執行個體 <*SID*>-di-0。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1022">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="5ff84-1023">Azure 或 DataKeeper 特定的設定沒有相依性。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1023">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="5ff84-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> 安裝 SAP 其他應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="5ff84-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="5ff84-1025">在您指派來裝載 SAP 應用程式伺服器執行個體的所有虛擬機器上安裝 SAP 其他應用程式伺服器 (AAS)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1025">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="5ff84-1026">例如，在 <*SID*>-di-1 到 <*SID*>-di-&lt;n&gt;。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1026">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff84-1027">這樣就完成高可用性的 SAP NetWeaver 系統的安裝。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1027">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="5ff84-1028">接下來，繼續進行容錯移轉測試。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1028">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="5ff84-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> 測試 SAP ASCS/SCS 執行個體容錯移轉和 SIOS 複寫</span><span class="sxs-lookup"><span data-stu-id="5ff84-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="5ff84-1030">使用「容錯移轉叢集管理員」和 SIOS DataKeeper 管理和組態工具，可輕鬆地測試及監視 SAP ASCS/SCS 執行個體容錯移轉和 SIOS 磁碟複寫。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1030">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="5ff84-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS 執行個體在叢集節點 A 上執行</span><span class="sxs-lookup"><span data-stu-id="5ff84-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="5ff84-1032">**SAP PR1**叢集群組在叢集節點 A 上執行，例如，在 **pr1-ascs-0** 上。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1032">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="5ff84-1033">將屬於 **SAP PR1** 叢集群組並由 ASCS/SCS 執行個體使用的共用磁碟 S，指派給叢集節點 A。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1033">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![圖 61：容錯移轉叢集管理員︰SAP <SID> 叢集群組在叢集節點 A 上執行][sap-ha-guide-figure-5000]

<span data-ttu-id="5ff84-1035">_**圖 61：**容錯移轉叢集管理員︰SAP <SID> 叢集群組在叢集節點 A 上執行_</span><span class="sxs-lookup"><span data-stu-id="5ff84-1035">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="5ff84-1036">在 SIOS DataKeeper 管理和組態工具中，您可以看到共用磁碟資料以同步方式從叢集節點 A 上的來源磁碟區 S 複寫到叢集節點 B 上的目標磁碟區 S。例如，從 **pr1-ascs-0 [10.0.0.40]** 複寫到 **pr1-ascs-1 [10.0.0.41]**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1036">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![圖 62：在 SIOS DataKeeper 中，將本機磁碟區從叢集節點 A 的磁碟區複寫到叢集節點 B][sap-ha-guide-figure-5001]

<span data-ttu-id="5ff84-1038">_**圖 62：**在 SIOS DataKeeper 中，將本機磁碟區從叢集節點 A 的磁碟區複寫到叢集節點 B_</span><span class="sxs-lookup"><span data-stu-id="5ff84-1038">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="5ff84-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> 從節點 A 到節點 B 進行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5ff84-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="5ff84-1040">使用下列其中一個選項以起始將 SAP <SID> 叢集群組從叢集節點 A 到叢集節點 B 的容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="5ff84-1040">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="5ff84-1041">使用容錯移轉叢集管理員</span><span class="sxs-lookup"><span data-stu-id="5ff84-1041">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="5ff84-1042">使用容錯移轉叢集 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ff84-1042">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="5ff84-1043">在 Windows 客體作業系統內重新啟動叢集節點 A (這會起始將 SAP <SID> 叢集群組從節點 A 容錯移轉到節點 B 的自動容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1043">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="5ff84-1044">從 Azure 入口網站重新啟動叢集節點 A (這會起始將 SAP <SID> 叢集群組從節點 A 到節點 B 的自動容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1044">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="5ff84-1045">使用 Azure PowerShell 重新啟動叢集節點 A (這會起始將 SAP <SID> 叢集群組從節點 A 到節點 B 的自動容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1045">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="5ff84-1046">容錯移轉之後，SAP <SID> 叢集群組會在叢集節點 B 上執行。例如，在 **pr1-ascs-1** 上執行。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1046">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![圖 63：在「容錯移轉叢集管理員」中，SAP <SID> 叢集群組在叢集節點 B 上執行][sap-ha-guide-figure-5002]

  <span data-ttu-id="5ff84-1048">_**圖 63**：在「容錯移轉叢集管理員」中，SAP <*SID*> 叢集群組在叢集節點 B 上執行_</span><span class="sxs-lookup"><span data-stu-id="5ff84-1048">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="5ff84-1049">共用磁碟現在已掛接在叢集節點 B 上。SIOS DataKeeper 正在將資料從叢集節點 B 上的來源磁碟區 S 複寫到叢集節點 A 上的目標磁碟區 S。例如，從 **pr1-ascs-1 [10.0.0.41]** 複寫到 **pr1-ascs-0 [10.0.0.40]**。</span><span class="sxs-lookup"><span data-stu-id="5ff84-1049">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![圖 64：SIOS DataKeeper 將本機磁碟區從叢集節點 B 複寫到叢集節點 A][sap-ha-guide-figure-5003]

  <span data-ttu-id="5ff84-1051">_**圖 64：**SIOS DataKeeper 將本機磁碟區從叢集節點 B 複寫到叢集節點 A_</span><span class="sxs-lookup"><span data-stu-id="5ff84-1051">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
