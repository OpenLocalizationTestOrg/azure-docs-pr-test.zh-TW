---
title: "如何針對 Azure RemoteApp 集合規劃您的虛擬網路 | Microsoft Docs"
description: "了解如何針對 Azure RemoteApp 集合規劃您的虛擬網路。"
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 1eb8115b13fb18074b4c4726b69e3d9faf387c32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a><span data-ttu-id="c800d-103">如何針對 Azure RemoteApp 規劃您的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c800d-103">How to plan your virtual network for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c800d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="c800d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c800d-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="c800d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c800d-106">本文件說明如何針對 Azure RemoteApp 設定 Azure 虛擬網路 (VNET) 和子網路。</span><span class="sxs-lookup"><span data-stu-id="c800d-106">This document describes how to set up your Azure virtual network (VNET) and the subnet for Azure RemoteApp.</span></span> <span data-ttu-id="c800d-107">如果您不熟悉 Azure 虛擬網路，這可協助您將網路基礎結構虛擬化至雲端，以及利用 Azure 和內部部署資源建立混合式解決方案。</span><span class="sxs-lookup"><span data-stu-id="c800d-107">If you are unfamiliar with Azure virtual networks, this is a capability that helps you to virtualize your network infrastructure to the cloud and to create hybrid solutions with Azure and your on-premises resources.</span></span> <span data-ttu-id="c800d-108">您可以在 [此處](../virtual-network/virtual-networks-overview.md)閱讀相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c800d-108">You can read more about it [here](../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="c800d-109">如果您要在您部署 Azure RemoteApp 的虛擬網路中定義流量 (內送和外寄) 的安全性原則，我們強烈建議您在 Azure 虛擬網路中為 Azure RemoteApp 建立與您其餘的部署不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="c800d-109">If you want to define security policies for traffic (both incoming and outgoing) in your virtual network where you are deploying Azure RemoteApp, we strongly recommend creating a separate subnet for Azure RemoteApp from the rest of your deployments in the Azure virtual network.</span></span> <span data-ttu-id="c800d-110">如需有關如何在 Azure 虛擬網路子網路上定義安全性原則的詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="c800d-110">For more information on how to define security policies on your Azure virtual network subnet, please read [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a><span data-ttu-id="c800d-111">具有 Azure 虛擬網路的 Azure RemoteApp 集合類型</span><span class="sxs-lookup"><span data-stu-id="c800d-111">Types of Azure RemoteApp collections with Azure virtual networks</span></span>
<span data-ttu-id="c800d-112">下圖顯示您要使用虛擬網路時的兩個不同集合選項。</span><span class="sxs-lookup"><span data-stu-id="c800d-112">The following graphics show the two different collection options when you want to use a virtual network.</span></span>

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a><span data-ttu-id="c800d-113">具有 VNET 的 Azure RemoteApp 雲端集合</span><span class="sxs-lookup"><span data-stu-id="c800d-113">Azure RemoteApp cloud collection with VNET</span></span>
 ![Azure RemoteApp - 具有 VNET 的雲端集合](./media/remoteapp-planvpn/ra-cloudvpn.png)

<span data-ttu-id="c800d-115">這表示 Azure RemoteApp 集合，其中 RemoteApp 工作階段主機需要存取的所有資源都已部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="c800d-115">This represents an Azure RemoteApp collection where all the resources that the RemoteApp session hosts need to access are deployed in Azure.</span></span> <span data-ttu-id="c800d-116">也可以在 Azure 中與 RemoteApp VNET 相同的 VNET 或不同的 VNET 中。</span><span class="sxs-lookup"><span data-stu-id="c800d-116">They can be in the same VNET as the RemoteApp VNET or a different VNET in Azure.</span></span>

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a><span data-ttu-id="c800d-117">具有 VNET 的 RemoteApp 混合式集合</span><span class="sxs-lookup"><span data-stu-id="c800d-117">Azure RemoteApp hybrid collection with VNET</span></span>
![Azure RemoteApp - 具有 VNET 的混合式集合](./media/remoteapp-planvpn/ra-hybridvpn.png)

<span data-ttu-id="c800d-119">這表示 Azure RemoteApp 集合，其中 RemoteApp 工作階段主機需要存取的某些資源已在內部部署。</span><span class="sxs-lookup"><span data-stu-id="c800d-119">This represents an Azure RemoteApp collection where some of the resources that the RemoteApp session hosts need to access are deployed on-premises.</span></span> <span data-ttu-id="c800d-120">RemoteApp VNET 會使用 Azure 混合式技術 (像是站對站 VPN 或 Express Route) 連結到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="c800d-120">The RemoteApp VNET is linked to the on-premises network using Azure hybrid technologies like site-to-site VPN or Express Route.</span></span>

## <a name="how-the-system-works"></a><span data-ttu-id="c800d-121">系統的運作方式</span><span class="sxs-lookup"><span data-stu-id="c800d-121">How the system works</span></span>
<span data-ttu-id="c800d-122">實際上，Azure RemoteApp 會將 Azure 虛擬機器 (與您上傳的映像) 部署到您在佈建期間所選擇的虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="c800d-122">Under the covers Azure RemoteApp deploys Azure virtual machines (with your uploaded image) to the virtual network subnet that you chose during provisioning.</span></span> <span data-ttu-id="c800d-123">如果您選擇了混合式集合，我們會嘗試解析您在佈建工作流程中輸入的網域控制站的 FQDN，以及虛擬網路中提供的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c800d-123">If you opted for a hybrid collection, we try to resolve the FQDN of the domain controller you entered in the provisioning workflow with the DNS server provided in the virtual network.</span></span>  
<span data-ttu-id="c800d-124">如果您要連接到現有的虛擬網路，請務必公開 Azure RemoteApp 子網路的網路安全性群組中的必要連接埠。</span><span class="sxs-lookup"><span data-stu-id="c800d-124">If you are connecting to an existing virtual network, make sure to expose the necessary ports in your network security groups in your Azure RemoteApp subnet.</span></span> 

<span data-ttu-id="c800d-125">我們建議您改用 [Azure RemoteApp 夠大的子網路](remoteapp-vnetsizing.md)。</span><span class="sxs-lookup"><span data-stu-id="c800d-125">We recommend you use a [large enough  subnet for Azure RemoteApp](remoteapp-vnetsizing.md).</span></span> <span data-ttu-id="c800d-126">Azure 虛擬網路最大支援 /8 (使用 CIDR 子網路定義)。</span><span class="sxs-lookup"><span data-stu-id="c800d-126">The largest supported by Azure Virtual network is /8 (using CIDR subnet definitions).</span></span> <span data-ttu-id="c800d-127">當更多使用者存取應用程式時，您的子網路在相應增加期間應足以容納所有的 Azure RemoteApp VM。</span><span class="sxs-lookup"><span data-stu-id="c800d-127">Your subnet should be large enough to accommodate all the Azure RemoteApp VMs during scale-up when more users are accessing the apps.</span></span> 

<span data-ttu-id="c800d-128">以下是您必須在虛擬網路子網路上啟用的事項：</span><span class="sxs-lookup"><span data-stu-id="c800d-128">Following are the things you will need to enable on your virtual network subnet:</span></span> 

1. <span data-ttu-id="c800d-129">連接埠範圍 10101-10175 應允許來自子網路的輸出流量，才能與其中一個內部 Azure RemoteApp 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="c800d-129">Outbound traffic from the subnet should be allowed on port range 10101-10175 to communicate with one of the internal Azure RemoteApp services.</span></span>
2. <span data-ttu-id="c800d-130">輸出流量應可來自您的子網路以連接到連接埠 443 上的 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="c800d-130">Outbound traffic should be allowed from your subnet to connect to Azure Storage on port 443</span></span>
3. <span data-ttu-id="c800d-131">如果您有 Azure 中裝載的 Active Directory，請確定 Azure RemoteApp 的虛擬網路子網路內的任何 VM 都能夠連接到該網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c800d-131">If you have Active Directory hosted in Azure, make sure any VM within the virtual network subnet for Azure RemoteApp is able to connect to that domain controller.</span></span> <span data-ttu-id="c800d-132">虛擬網路中的 DNS 應該能夠解析此網域控制站的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="c800d-132">The DNS in the virtual network should be able to resolve the FQDN of this domain controller.</span></span>

## <a name="virtual-network-with-forced-tunneling"></a><span data-ttu-id="c800d-133">具有強制通道的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c800d-133">Virtual network with forced tunneling</span></span>
<span data-ttu-id="c800d-134">[強制通道](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) 。</span><span class="sxs-lookup"><span data-stu-id="c800d-134">[Forced tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) is now supported for all new Azure RemoteApp collections.</span></span> <span data-ttu-id="c800d-135">我們目前不支援現有集合的移轉，而支援強制通道。</span><span class="sxs-lookup"><span data-stu-id="c800d-135">We currently do not support the migration of an existing collection to support forced tunneling.</span></span>  <span data-ttu-id="c800d-136">您必須使用您要連結至 Azure RemoteApp 的 VNET 來刪除所有現有的集合，並建立新的集合以在集合上啟用強制通道。</span><span class="sxs-lookup"><span data-stu-id="c800d-136">You will have to delete all your existing collections using the VNET that you are linking to Azure RemoteApp and create a new one to get forced tunneling enabled on your collections.</span></span> 

