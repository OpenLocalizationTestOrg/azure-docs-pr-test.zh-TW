---
title: "aaaCannot 刪除 Azure 中的虛擬網路 |Microsoft 文件"
description: "了解如何 tootroubleshoot hello 無法刪除 Azure 中的虛擬網路的問題。"
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="d1036-103">疑難排解： 無法 toodelete Azure 中的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d1036-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="d1036-104">當您嘗試 toodelete Microsoft Azure 中的虛擬網路時，您可能會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="d1036-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="d1036-105">本文章提供疑難排解步驟 toohelp 解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="d1036-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="d1036-106">疑難排解指引</span><span class="sxs-lookup"><span data-stu-id="d1036-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="d1036-107">[檢查是否正在執行 hello 虛擬網路中的虛擬網路閘道](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="d1036-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="d1036-108">[檢查是否正在執行 hello 虛擬網路中的應用程式閘道](#check-whether-an-application-gateway-is-running-in-the-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="d1036-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="d1036-109">[檢查是否已啟用 hello 虛擬網路中的 Azure Active Directory 網域服務](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="d1036-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="d1036-110">[檢查 hello 虛擬網路是否連線的 tooother 資源](#check-whether-the-virtual-network-is-connected-to-other-resource)。</span><span class="sxs-lookup"><span data-stu-id="d1036-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="d1036-111">[請檢查虛擬機器是否仍在執行 hello 虛擬網路中](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="d1036-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="d1036-112">[檢查 hello 虛擬網路是否陷入移轉](#check-whether-the-virtual-network-is-stuck-in-migration)。</span><span class="sxs-lookup"><span data-stu-id="d1036-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="d1036-113">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="d1036-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="d1036-114">檢查是否正在執行 hello 虛擬網路中的虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="d1036-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="d1036-115">tooremove hello 虛擬網路，您必須先移除 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d1036-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="d1036-116">傳統的虛擬網路，請移 toohello**概觀**hello 傳統中虛擬網路的 hello Azure 入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="d1036-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="d1036-117">在 hello **VPN 連線**區段中，如果 hello 閘道正在執行 hello 虛擬網路中，您會看到 hello IP hello 閘道位址。</span><span class="sxs-lookup"><span data-stu-id="d1036-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![檢查閘道是否正在執行](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="d1036-119">虛擬網路，請移 toohello**概觀**hello 虛擬網路的頁面。</span><span class="sxs-lookup"><span data-stu-id="d1036-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="d1036-120">請檢查**連接的裝置**hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d1036-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![檢查 hello 連接的裝置](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="d1036-122">您可以移除 hello 閘道之前，先移除任何**連接**hello 閘道中的物件。</span><span class="sxs-lookup"><span data-stu-id="d1036-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="d1036-123">檢查是否正在執行 hello 虛擬網路中的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d1036-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="d1036-124">移 toohello**概觀**hello 虛擬網路的頁面。</span><span class="sxs-lookup"><span data-stu-id="d1036-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="d1036-125">檢查 hello**連接的裝置**hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d1036-125">Check hello **Connected devices** for hello application gateway.</span></span>

![檢查 hello 連接的裝置](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="d1036-127">如果沒有應用程式閘道，您必須移除它，才能刪除 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1036-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="d1036-128">檢查是否已啟用 hello 虛擬網路中的 Azure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="d1036-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="d1036-129">如果已啟用，且已連線的 toohello 虛擬網路 hello Active Directory 網域服務，您無法刪除此虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1036-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![檢查 hello 連接的裝置](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="d1036-131">toodisable hello 服務，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1036-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="d1036-132">移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="d1036-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d1036-133">Hello 左窗格中，選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="d1036-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="d1036-134">選取已啟用的 Active Directory 網域服務的 hello Azure Active Directory (Azure AD) 目錄。</span><span class="sxs-lookup"><span data-stu-id="d1036-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="d1036-135">選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d1036-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="d1036-136">在下**網域服務**，變更 hello**啟用這個目錄的網域服務**太選項**否**。</span><span class="sxs-lookup"><span data-stu-id="d1036-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="d1036-137">檢查 hello 虛擬網路是否連線的 tooother 資源</span><span class="sxs-lookup"><span data-stu-id="d1036-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="d1036-138">檢查線路連結、連線和虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1036-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="d1036-139">任何一項都可能會造成虛擬網路刪除 toofail。</span><span class="sxs-lookup"><span data-stu-id="d1036-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="d1036-140">hello 建議的刪除順序如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1036-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="d1036-141">閘道連線</span><span class="sxs-lookup"><span data-stu-id="d1036-141">Gateway connections</span></span>
2. <span data-ttu-id="d1036-142">閘道</span><span class="sxs-lookup"><span data-stu-id="d1036-142">Gateways</span></span>
3. <span data-ttu-id="d1036-143">IP</span><span class="sxs-lookup"><span data-stu-id="d1036-143">IPs</span></span>
4. <span data-ttu-id="d1036-144">虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="d1036-144">Virtual network peerings</span></span>
5. <span data-ttu-id="d1036-145">App Service Environment (ASE)</span><span class="sxs-lookup"><span data-stu-id="d1036-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="d1036-146">請檢查虛擬機器是否仍在執行中 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d1036-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="d1036-147">請確定沒有虛擬機器 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1036-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="d1036-148">檢查 hello 虛擬網路是否陷入移轉</span><span class="sxs-lookup"><span data-stu-id="d1036-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="d1036-149">如果 hello 虛擬網路卡在移轉狀態，無法刪除。</span><span class="sxs-lookup"><span data-stu-id="d1036-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="d1036-150">執行 hello 命令 tooabort hello 在移轉之後，然後再刪除 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1036-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="d1036-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1036-151">Next steps</span></span>

- [<span data-ttu-id="d1036-152">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d1036-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="d1036-153">Azure 虛擬網路的常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="d1036-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)