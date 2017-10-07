---
title: "aaaHow tooplan 您的 Azure RemoteApp 集合的虛擬網路 |Microsoft 文件"
description: "深入了解如何 tooplan 虛擬網路，以 Azure RemoteApp 集合。"
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
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a><span data-ttu-id="e66e0-103">如何 tooplan 的 Azure RemoteApp 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e66e0-103">How tooplan your virtual network for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e66e0-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="e66e0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e66e0-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e66e0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e66e0-106">本文件說明如何註冊您的 Azure 虛擬網路 (VNET) 和 Azure RemoteApp 的子網路 hello tooset。</span><span class="sxs-lookup"><span data-stu-id="e66e0-106">This document describes how tooset up your Azure virtual network (VNET) and hello subnet for Azure RemoteApp.</span></span> <span data-ttu-id="e66e0-107">如果您不熟悉 Azure 虛擬網路，這是一種功能，可協助您 toovirtualize 您網路基礎結構 toohello 雲端和 toocreate 混合式解決方案使用 Azure 和內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="e66e0-107">If you are unfamiliar with Azure virtual networks, this is a capability that helps you toovirtualize your network infrastructure toohello cloud and toocreate hybrid solutions with Azure and your on-premises resources.</span></span> <span data-ttu-id="e66e0-108">您可以在 [此處](../virtual-network/virtual-networks-overview.md)閱讀相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e66e0-108">You can read more about it [here](../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="e66e0-109">如果您想要 toodefine 安全性原則 （內送和外寄） 的流量部署 Azure RemoteApp 虛擬網路中，我們強烈建議建立不同的子網路的 Azure RemoteApp，於您在 hello Azure 中部署的 hello 其餘部分虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e66e0-109">If you want toodefine security policies for traffic (both incoming and outgoing) in your virtual network where you are deploying Azure RemoteApp, we strongly recommend creating a separate subnet for Azure RemoteApp from hello rest of your deployments in hello Azure virtual network.</span></span> <span data-ttu-id="e66e0-110">如需有關如何 toodefine 安全性原則，在您的 Azure 虛擬網路子網路的詳細資訊，請閱讀[網路安全性群組 (NSG) 是什麼？](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="e66e0-110">For more information on how toodefine security policies on your Azure virtual network subnet, please read [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a><span data-ttu-id="e66e0-111">具有 Azure 虛擬網路的 Azure RemoteApp 集合類型</span><span class="sxs-lookup"><span data-stu-id="e66e0-111">Types of Azure RemoteApp collections with Azure virtual networks</span></span>
<span data-ttu-id="e66e0-112">hello 下列圖形顯示 hello 兩個不同的集合選項時要 toouse 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e66e0-112">hello following graphics show hello two different collection options when you want toouse a virtual network.</span></span>

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a><span data-ttu-id="e66e0-113">具有 VNET 的 Azure RemoteApp 雲端集合</span><span class="sxs-lookup"><span data-stu-id="e66e0-113">Azure RemoteApp cloud collection with VNET</span></span>
 ![Azure RemoteApp - 具有 VNET 的雲端集合](./media/remoteapp-planvpn/ra-cloudvpn.png)

<span data-ttu-id="e66e0-115">這代表所有 hello 資源 hello RemoteApp 工作階段主機需要 tooaccess 在 Azure 中的都部署所在的 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="e66e0-115">This represents an Azure RemoteApp collection where all hello resources that hello RemoteApp session hosts need tooaccess are deployed in Azure.</span></span> <span data-ttu-id="e66e0-116">可以在 hello hello RemoteApp VNET 與同一個 VNET 或在 Azure 中不同的 VNET。</span><span class="sxs-lookup"><span data-stu-id="e66e0-116">They can be in hello same VNET as hello RemoteApp VNET or a different VNET in Azure.</span></span>

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a><span data-ttu-id="e66e0-117">具有 VNET 的 RemoteApp 混合式集合</span><span class="sxs-lookup"><span data-stu-id="e66e0-117">Azure RemoteApp hybrid collection with VNET</span></span>
![Azure RemoteApp - 具有 VNET 的混合式集合](./media/remoteapp-planvpn/ra-hybridvpn.png)

<span data-ttu-id="e66e0-119">這代表其中的某些 hello RemoteApp 工作階段主機需要 tooaccess hello 資源是在內部部署的 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="e66e0-119">This represents an Azure RemoteApp collection where some of hello resources that hello RemoteApp session hosts need tooaccess are deployed on-premises.</span></span> <span data-ttu-id="e66e0-120">hello RemoteApp VNET 是使用 Azure 的混合式技術，例如站台對站 VPN 或 Express Route 的連結的 toohello 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="e66e0-120">hello RemoteApp VNET is linked toohello on-premises network using Azure hybrid technologies like site-to-site VPN or Express Route.</span></span>

## <a name="how-hello-system-works"></a><span data-ttu-id="e66e0-121">Hello 系統的運作方式</span><span class="sxs-lookup"><span data-stu-id="e66e0-121">How hello system works</span></span>
<span data-ttu-id="e66e0-122">Hello 幕後 Azure RemoteApp 部署 Azure 虛擬機器 （使用您已上傳的映像） toohello 虛擬網路子網路，您選擇佈建期間。</span><span class="sxs-lookup"><span data-stu-id="e66e0-122">Under hello covers Azure RemoteApp deploys Azure virtual machines (with your uploaded image) toohello virtual network subnet that you chose during provisioning.</span></span> <span data-ttu-id="e66e0-123">如果您選擇混合式集合，我們會嘗試 tooresolve hello hello 在 hello 與 hello hello 虛擬網路中提供的 DNS 伺服器佈建工作流程中所輸入的網域控制站的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="e66e0-123">If you opted for a hybrid collection, we try tooresolve hello FQDN of hello domain controller you entered in hello provisioning workflow with hello DNS server provided in hello virtual network.</span></span>  
<span data-ttu-id="e66e0-124">如果您要連接 tooan 現有的虛擬網路，請確定 tooexpose hello 必要的連接埠中您 Azure RemoteApp 的子網路的網路安全性群組中。</span><span class="sxs-lookup"><span data-stu-id="e66e0-124">If you are connecting tooan existing virtual network, make sure tooexpose hello necessary ports in your network security groups in your Azure RemoteApp subnet.</span></span> 

<span data-ttu-id="e66e0-125">我們建議您改用 [Azure RemoteApp 夠大的子網路](remoteapp-vnetsizing.md)。</span><span class="sxs-lookup"><span data-stu-id="e66e0-125">We recommend you use a [large enough  subnet for Azure RemoteApp](remoteapp-vnetsizing.md).</span></span> <span data-ttu-id="e66e0-126">hello 最大支援的 Azure 虛擬網路是/8 （使用 CIDR 子網路定義）。</span><span class="sxs-lookup"><span data-stu-id="e66e0-126">hello largest supported by Azure Virtual network is /8 (using CIDR subnet definitions).</span></span> <span data-ttu-id="e66e0-127">您的子網路應夠大 tooaccommodate 期間所有 hello Azure RemoteApp Vm 向上延展，當多個使用者同時存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e66e0-127">Your subnet should be large enough tooaccommodate all hello Azure RemoteApp VMs during scale-up when more users are accessing hello apps.</span></span> 

<span data-ttu-id="e66e0-128">以下是您的虛擬網路子網路上，您將需要 tooenable hello 事情：</span><span class="sxs-lookup"><span data-stu-id="e66e0-128">Following are hello things you will need tooenable on your virtual network subnet:</span></span> 

1. <span data-ttu-id="e66e0-129">使用其中一個 hello 內部 Azure RemoteApp 服務的連接埠範圍 10101 10175 toocommunicate 應該允許 hello 子網路的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="e66e0-129">Outbound traffic from hello subnet should be allowed on port range 10101-10175 toocommunicate with one of hello internal Azure RemoteApp services.</span></span>
2. <span data-ttu-id="e66e0-130">允許輸出流量從您的子網路 tooconnect tooAzure 連接埠 443 上的儲存體</span><span class="sxs-lookup"><span data-stu-id="e66e0-130">Outbound traffic should be allowed from your subnet tooconnect tooAzure Storage on port 443</span></span>
3. <span data-ttu-id="e66e0-131">如果您有 Azure 中裝載的 Active Directory，請確定 hello 虛擬網路子網路的 Azure RemoteApp 內任何 VM 可以 tooconnect toothat 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="e66e0-131">If you have Active Directory hosted in Azure, make sure any VM within hello virtual network subnet for Azure RemoteApp is able tooconnect toothat domain controller.</span></span> <span data-ttu-id="e66e0-132">hello 虛擬網路中的 hello DNS 應該能夠 tooresolve hello 此網域控制站的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="e66e0-132">hello DNS in hello virtual network should be able tooresolve hello FQDN of this domain controller.</span></span>

## <a name="virtual-network-with-forced-tunneling"></a><span data-ttu-id="e66e0-133">具有強制通道的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e66e0-133">Virtual network with forced tunneling</span></span>
<span data-ttu-id="e66e0-134">[強制通道](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) 。</span><span class="sxs-lookup"><span data-stu-id="e66e0-134">[Forced tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) is now supported for all new Azure RemoteApp collections.</span></span> <span data-ttu-id="e66e0-135">我們目前不支援強制通道的現有集合 toosupport hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="e66e0-135">We currently do not support hello migration of an existing collection toosupport forced tunneling.</span></span>  <span data-ttu-id="e66e0-136">您必須 toodelete 使用 hello VNET，您要連結 tooAzure RemoteApp，並建立新的一個 tooget 強制通道的集合上啟用所有現有的集合。</span><span class="sxs-lookup"><span data-stu-id="e66e0-136">You will have toodelete all your existing collections using hello VNET that you are linking tooAzure RemoteApp and create a new one tooget forced tunneling enabled on your collections.</span></span> 

