---
title: "利用 Azure 入口網站開始使用 Azure DNS | Microsoft Docs"
description: "了解如何在 Azure DNS 中建立 DNS 區域和記錄。 這份逐步指南將引導您使用 Azure 入口網站建立和管理第一個 DNS 區域和記錄。"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 93b24e3d9fbb3fbb3ea995271fd63d1e82eb9c9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-the-azure-portal"></a><span data-ttu-id="dab7a-104">利用 Azure 入口網站開始使用 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="dab7a-104">Get started with Azure DNS using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dab7a-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dab7a-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="dab7a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dab7a-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="dab7a-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dab7a-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="dab7a-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dab7a-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="dab7a-109">本文將逐步引導您使用 Azure 入口網站建立第一個 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-109">This article walks you through the steps to create your first DNS zone and record using the Azure portal.</span></span> <span data-ttu-id="dab7a-110">您也可以使用 Azure PowerShell 或跨平台 Azure CLI 執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="dab7a-110">You can also perform these steps using Azure PowerShell or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="dab7a-111">DNS 區域用來裝載特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="dab7a-112">若要開始將網域裝載到 Azure DNS 中，您必須建立該網域名稱的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dab7a-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="dab7a-113">接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="dab7a-114">最後，若要將 DNS 區域發佈至網際網路，您需要設定網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="dab7a-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="dab7a-115">下列步驟會說明每個步驟。</span><span class="sxs-lookup"><span data-stu-id="dab7a-115">Each of these steps is described in the following steps.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="dab7a-116">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="dab7a-116">Create a DNS zone</span></span>

1. <span data-ttu-id="dab7a-117">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dab7a-117">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="dab7a-118">在 [中樞] 功能表上，按一下 [新增] > [網路] > [DNS 區域] 以開啟 [建立 DNS 區域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dab7a-118">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-getstarted-portal/openzone650.png)

4. <span data-ttu-id="dab7a-120">在 [建立 DNS 區域] 刀鋒視窗中輸入下列的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="dab7a-120">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="dab7a-121">**設定**</span><span class="sxs-lookup"><span data-stu-id="dab7a-121">**Setting**</span></span> | <span data-ttu-id="dab7a-122">**值**</span><span class="sxs-lookup"><span data-stu-id="dab7a-122">**Value**</span></span> | <span data-ttu-id="dab7a-123">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="dab7a-123">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="dab7a-124">**名稱**</span><span class="sxs-lookup"><span data-stu-id="dab7a-124">**Name**</span></span>|<span data-ttu-id="dab7a-125">contoso.com</span><span class="sxs-lookup"><span data-stu-id="dab7a-125">contoso.com</span></span>|<span data-ttu-id="dab7a-126">DNS 區域的名稱</span><span class="sxs-lookup"><span data-stu-id="dab7a-126">The name of the DNS zone</span></span>|
   |<span data-ttu-id="dab7a-127">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="dab7a-127">**Subscription**</span></span>|<span data-ttu-id="dab7a-128">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="dab7a-128">[Your subscription]</span></span>|<span data-ttu-id="dab7a-129">選取要建立 DNS 區域的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dab7a-129">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="dab7a-130">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="dab7a-130">**Resource group**</span></span>|<span data-ttu-id="dab7a-131">**建立新的︰**contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="dab7a-131">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="dab7a-132">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="dab7a-132">Create a resource group.</span></span> <span data-ttu-id="dab7a-133">資源群組名稱在您選取的訂用帳戶中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="dab7a-133">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="dab7a-134">若要深入了解資源群組，請閱讀 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 概觀。</span><span class="sxs-lookup"><span data-stu-id="dab7a-134">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="dab7a-135">**位置**</span><span class="sxs-lookup"><span data-stu-id="dab7a-135">**Location**</span></span>|<span data-ttu-id="dab7a-136">美國西部</span><span class="sxs-lookup"><span data-stu-id="dab7a-136">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="dab7a-137">資源群組是指資源群組的位置，不會對 DNS 區域有任何影響。</span><span class="sxs-lookup"><span data-stu-id="dab7a-137">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="dab7a-138">DNS 區域一定是「全域」位置，並不會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="dab7a-138">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="dab7a-139">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="dab7a-139">Create a DNS record</span></span>

<span data-ttu-id="dab7a-140">下列範例將逐步引導您完成建立新的 'A' 記錄的程序。</span><span class="sxs-lookup"><span data-stu-id="dab7a-140">The following example walks you through the process of creating new 'A' record.</span></span> <span data-ttu-id="dab7a-141">關於其他記錄類型和修改現有的記錄，請參閱[使用 Azure 入口網站管理 DNS 記錄和記錄集](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="dab7a-141">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span> 

1. <span data-ttu-id="dab7a-142">建立 DNS 區域之後，在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="dab7a-142">With the DNS Zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="dab7a-143">在 [所有資源] 刀鋒視窗中，按一下 [contoso.com] DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dab7a-143">Click the **contoso.com** DNS zone in the All resources blade.</span></span> <span data-ttu-id="dab7a-144">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選...] 方塊中輸入 **contoso.com**，</span><span class="sxs-lookup"><span data-stu-id="dab7a-144">If the subscription you selected already has several resources in it, you can enter **contoso.com** in the **Filter by name…**</span></span> <span data-ttu-id="dab7a-145">輕鬆地存取 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dab7a-145">box to easily access the DNS Zone.</span></span>

1. <span data-ttu-id="dab7a-146">在 [DNS 區域] 刀鋒視窗頂端，選取 [+ 記錄集] 以開啟 [新增記錄集] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dab7a-146">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

1. <span data-ttu-id="dab7a-147">在 [新增記錄集] 刀鋒視窗上，輸入下列的值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="dab7a-147">On the **Add record set** blade, enter the following values, and click **OK**.</span></span> <span data-ttu-id="dab7a-148">在此範例中，我們會建立 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-148">In this example, you are creating an A record.</span></span>

   |<span data-ttu-id="dab7a-149">**設定**</span><span class="sxs-lookup"><span data-stu-id="dab7a-149">**Setting**</span></span> | <span data-ttu-id="dab7a-150">**值**</span><span class="sxs-lookup"><span data-stu-id="dab7a-150">**Value**</span></span> | <span data-ttu-id="dab7a-151">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="dab7a-151">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="dab7a-152">**名稱**</span><span class="sxs-lookup"><span data-stu-id="dab7a-152">**Name**</span></span>|<span data-ttu-id="dab7a-153">www</span><span class="sxs-lookup"><span data-stu-id="dab7a-153">www</span></span>|<span data-ttu-id="dab7a-154">記錄的名稱</span><span class="sxs-lookup"><span data-stu-id="dab7a-154">Name of the record</span></span>|
   |<span data-ttu-id="dab7a-155">**類型**</span><span class="sxs-lookup"><span data-stu-id="dab7a-155">**Type**</span></span>|<span data-ttu-id="dab7a-156">具有使用 </span><span class="sxs-lookup"><span data-stu-id="dab7a-156">A</span></span>| <span data-ttu-id="dab7a-157">要建立的 DNS 記錄類型，可接受的值為 A、AAAA、CNAME、MX、NS、SRV、TXT 和 PTR。</span><span class="sxs-lookup"><span data-stu-id="dab7a-157">Type of DNS record to create, acceptable values are A, AAAA, CNAME, MX, NS, SRV, TXT, and PTR.</span></span>  <span data-ttu-id="dab7a-158">如需記錄類型的詳細資訊，請參閱 [DNS 區域和記錄的概觀](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="dab7a-158">For more information about record types, visit [Overview of DNS zones and records](dns-zones-records.md)</span></span>|
   |<span data-ttu-id="dab7a-159">**TTL**</span><span class="sxs-lookup"><span data-stu-id="dab7a-159">**TTL**</span></span>|<span data-ttu-id="dab7a-160">1</span><span class="sxs-lookup"><span data-stu-id="dab7a-160">1</span></span>|<span data-ttu-id="dab7a-161">DNS 要求的存留時間。</span><span class="sxs-lookup"><span data-stu-id="dab7a-161">Time-to-live of the DNS request.</span></span>|
   |<span data-ttu-id="dab7a-162">**TTL 單位**</span><span class="sxs-lookup"><span data-stu-id="dab7a-162">**TTL unit**</span></span>|<span data-ttu-id="dab7a-163">小時</span><span class="sxs-lookup"><span data-stu-id="dab7a-163">Hours</span></span>|<span data-ttu-id="dab7a-164">TTL 值的時間測量。</span><span class="sxs-lookup"><span data-stu-id="dab7a-164">Measurement of time for TTL value.</span></span>|
   |<span data-ttu-id="dab7a-165">**IP 位址**</span><span class="sxs-lookup"><span data-stu-id="dab7a-165">**IP address**</span></span>|<span data-ttu-id="dab7a-166">ipAddressValue</span><span class="sxs-lookup"><span data-stu-id="dab7a-166">ipAddressValue</span></span>| <span data-ttu-id="dab7a-167">這個值是 DNS 記錄解析的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dab7a-167">This value is the IP address that the DNS record resolves.</span></span>|

## <a name="view-records"></a><span data-ttu-id="dab7a-168">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="dab7a-168">View records</span></span>

<span data-ttu-id="dab7a-169">在 [DNS 區域] 刀鋒視窗的下半部，您可以看到 DNS 區域的記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-169">In the lower part of the DNS zone blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="dab7a-170">您應該會看到預設 DNS 和 SOA 記錄 (在每個區域中建立)，還有您已建立的任何新記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-170">You should see the default DNS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

![區域](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a><span data-ttu-id="dab7a-172">更新名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="dab7a-172">Update name servers</span></span>

<span data-ttu-id="dab7a-173">當您滿意 DNS 區域且已正確設定記錄之後，您必須設定網域名稱來使用 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="dab7a-173">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="dab7a-174">這可讓網際網路上的其他使用者找到您的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="dab7a-174">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="dab7a-175">Azure 入口網站中會提供您區域的名稱伺服器：</span><span class="sxs-lookup"><span data-stu-id="dab7a-175">The name servers for your zone are given in the Azure portal:</span></span>

![區域](./media/dns-getstarted-portal/viewzonens500.png)

<span data-ttu-id="dab7a-177">這些名稱伺服器應該向網域名稱註冊機構 (您購買網域名稱的來源) 設定。</span><span class="sxs-lookup"><span data-stu-id="dab7a-177">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="dab7a-178">您的註冊機構會提供選項來設定網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="dab7a-178">Your registrar offers the option to set up the name servers for the domain.</span></span> <span data-ttu-id="dab7a-179">如需詳細資訊，請參閱[將網域委派給 Azure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="dab7a-179">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="dab7a-180">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="dab7a-180">Delete all resources</span></span>

<span data-ttu-id="dab7a-181">若要刪除這篇文章中建立的所有資源，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="dab7a-181">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="dab7a-182">在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="dab7a-182">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="dab7a-183">在 [所有資源] 刀鋒視窗中，按一下 [MyResourceGroup] 資源群組。</span><span class="sxs-lookup"><span data-stu-id="dab7a-183">Click the **MyResourceGroup** resource group in the All resources blade.</span></span> <span data-ttu-id="dab7a-184">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選...] 方塊中輸入 **MyResourceGroup**，</span><span class="sxs-lookup"><span data-stu-id="dab7a-184">If the subscription you selected already has several resources in it, you can enter **MyResourceGroup** in the **Filter by name…**</span></span> <span data-ttu-id="dab7a-185">輕鬆地存取資源群組。</span><span class="sxs-lookup"><span data-stu-id="dab7a-185">box to easily access the resource group.</span></span>
1. <span data-ttu-id="dab7a-186">在 [MyResourceGroup] 刀鋒視窗中，按一下 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dab7a-186">In the **MyResourceGroup** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="dab7a-187">入口網站會要求您輸入資源群組的名稱，以確認您想要刪除它。</span><span class="sxs-lookup"><span data-stu-id="dab7a-187">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="dab7a-188">按一下 [刪除]，輸入 *MyResourceGroup* 作為資源群組名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="dab7a-188">Click **Delete**, Type *MyResourceGroup* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="dab7a-189">刪除資源群組會刪除資源群組內的所有資源，所以務必確認資源群組的內容，然後再刪除它。</span><span class="sxs-lookup"><span data-stu-id="dab7a-189">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="dab7a-190">入口網站會刪除資源群組內包含的所有資源，然後刪除資源群組本身。</span><span class="sxs-lookup"><span data-stu-id="dab7a-190">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="dab7a-191">這個程序需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="dab7a-191">This process takes several minutes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dab7a-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dab7a-192">Next steps</span></span>

<span data-ttu-id="dab7a-193">若要深入了解 Azure DNS，請參閱 [Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dab7a-193">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="dab7a-194">若要深入了解在 Azure DNS 中管理 DNS 記錄，請參閱[使用 Azure 入口網站管理 DNS 記錄和記錄集](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="dab7a-194">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

