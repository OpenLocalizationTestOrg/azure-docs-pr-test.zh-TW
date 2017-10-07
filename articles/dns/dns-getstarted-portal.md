---
title: "aaaGet 開始使用 Azure DNS 使用 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate DNS 區域與在 Azure DNS 記錄。 這是逐步指南 toocreate 和管理您的第一個 DNS 區域和使用 hello Azure 入口網站的記錄。"
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
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a><span data-ttu-id="c5ac5-104">開始使用 Azure DNS 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5ac5-104">Get started with Azure DNS using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5ac5-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5ac5-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="c5ac5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5ac5-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="c5ac5-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c5ac5-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="c5ac5-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c5ac5-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="c5ac5-109">這篇文章會引導您透過 hello 步驟 toocreate 您的第一個 DNS 區域和使用 hello Azure 入口網站的記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-109">This article walks you through hello steps toocreate your first DNS zone and record using hello Azure portal.</span></span> <span data-ttu-id="c5ac5-110">您也可以使用 Azure PowerShell 執行這些步驟，或 hello 跨平台 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-110">You can also perform these steps using Azure PowerShell or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="c5ac5-111">DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="c5ac5-112">toostart 裝載您的網域在 Azure DNS 中，您需要該網域名稱 toocreate DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="c5ac5-113">接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="c5ac5-114">最後，toopublish 您的 DNS 區域 toohello 網際網路，您需要 tooconfigure hello 名稱伺服器 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="c5ac5-115">每個步驟所述步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-115">Each of these steps is described in hello following steps.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="c5ac5-116">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="c5ac5-116">Create a DNS zone</span></span>

1. <span data-ttu-id="c5ac5-117">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5ac5-117">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="c5ac5-118">在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-118">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-getstarted-portal/openzone650.png)

4. <span data-ttu-id="c5ac5-120">在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="c5ac5-120">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="c5ac5-121">**設定**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-121">**Setting**</span></span> | <span data-ttu-id="c5ac5-122">**值**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-122">**Value**</span></span> | <span data-ttu-id="c5ac5-123">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-123">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="c5ac5-124">**名稱**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-124">**Name**</span></span>|<span data-ttu-id="c5ac5-125">contoso.com</span><span class="sxs-lookup"><span data-stu-id="c5ac5-125">contoso.com</span></span>|<span data-ttu-id="c5ac5-126">hello hello DNS 區域名稱</span><span class="sxs-lookup"><span data-stu-id="c5ac5-126">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="c5ac5-127">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-127">**Subscription**</span></span>|<span data-ttu-id="c5ac5-128">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="c5ac5-128">[Your subscription]</span></span>|<span data-ttu-id="c5ac5-129">選取的訂用帳戶 toocreate hello DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-129">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="c5ac5-130">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-130">**Resource group**</span></span>|<span data-ttu-id="c5ac5-131">**建立新的︰**contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="c5ac5-131">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="c5ac5-132">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-132">Create a resource group.</span></span> <span data-ttu-id="c5ac5-133">hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-133">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="c5ac5-134">深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-134">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="c5ac5-135">**位置**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-135">**Location**</span></span>|<span data-ttu-id="c5ac5-136">美國西部</span><span class="sxs-lookup"><span data-stu-id="c5ac5-136">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="c5ac5-137">hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-137">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="c5ac5-138">hello DNS 區域位置一定是 「 全域 」，而且不會顯示。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-138">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="c5ac5-139">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="c5ac5-139">Create a DNS record</span></span>

<span data-ttu-id="c5ac5-140">hello 下列範例會引導您完成建立新的 'A' 記錄 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-140">hello following example walks you through hello process of creating new 'A' record.</span></span> <span data-ttu-id="c5ac5-141">其他的記錄類型和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-141">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span> 

1. <span data-ttu-id="c5ac5-142">Hello DNS 區域，在中建立 hello Azure 入口網站**我的最愛**] 窗格中，按一下 [**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-142">With hello DNS Zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="c5ac5-143">按一下 hello **contoso.com** hello 資源刀鋒視窗中所有 DNS 都區域。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-143">Click hello **contoso.com** DNS zone in hello All resources blade.</span></span> <span data-ttu-id="c5ac5-144">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**contoso.com**在 hello**依名稱篩選...**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-144">If hello subscription you selected already has several resources in it, you can enter **contoso.com** in hello **Filter by name…**</span></span> <span data-ttu-id="c5ac5-145">方塊 tooeasily 存取 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-145">box tooeasily access hello DNS Zone.</span></span>

1. <span data-ttu-id="c5ac5-146">頂端的 hello hello **DNS 區域**刀鋒視窗中，選取**+ 記錄集**tooopen hello**加入資料錄集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-146">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

1. <span data-ttu-id="c5ac5-147">在 hello**加入資料錄集**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-147">On hello **Add record set** blade, enter hello following values, and click **OK**.</span></span> <span data-ttu-id="c5ac5-148">在此範例中，我們會建立 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-148">In this example, you are creating an A record.</span></span>

   |<span data-ttu-id="c5ac5-149">**設定**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-149">**Setting**</span></span> | <span data-ttu-id="c5ac5-150">**值**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-150">**Value**</span></span> | <span data-ttu-id="c5ac5-151">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-151">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="c5ac5-152">**名稱**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-152">**Name**</span></span>|<span data-ttu-id="c5ac5-153">www</span><span class="sxs-lookup"><span data-stu-id="c5ac5-153">www</span></span>|<span data-ttu-id="c5ac5-154">Hello 記錄名稱</span><span class="sxs-lookup"><span data-stu-id="c5ac5-154">Name of hello record</span></span>|
   |<span data-ttu-id="c5ac5-155">**類型**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-155">**Type**</span></span>|<span data-ttu-id="c5ac5-156">A</span><span class="sxs-lookup"><span data-stu-id="c5ac5-156">A</span></span>| <span data-ttu-id="c5ac5-157">類型的 DNS 記錄 toocreate，可接受的值為 A、 AAAA、 CNAME、 MX、 NS、 SRV、 TXT、 和 PTR。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-157">Type of DNS record toocreate, acceptable values are A, AAAA, CNAME, MX, NS, SRV, TXT, and PTR.</span></span>  <span data-ttu-id="c5ac5-158">如需記錄類型的詳細資訊，請參閱 [DNS 區域和記錄的概觀](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-158">For more information about record types, visit [Overview of DNS zones and records](dns-zones-records.md)</span></span>|
   |<span data-ttu-id="c5ac5-159">**TTL**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-159">**TTL**</span></span>|<span data-ttu-id="c5ac5-160">1</span><span class="sxs-lookup"><span data-stu-id="c5ac5-160">1</span></span>|<span data-ttu-id="c5ac5-161">-存留時間的 hello DNS 要求。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-161">Time-to-live of hello DNS request.</span></span>|
   |<span data-ttu-id="c5ac5-162">**TTL 單位**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-162">**TTL unit**</span></span>|<span data-ttu-id="c5ac5-163">小時</span><span class="sxs-lookup"><span data-stu-id="c5ac5-163">Hours</span></span>|<span data-ttu-id="c5ac5-164">TTL 值的時間測量。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-164">Measurement of time for TTL value.</span></span>|
   |<span data-ttu-id="c5ac5-165">**IP 位址**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-165">**IP address**</span></span>|<span data-ttu-id="c5ac5-166">ipAddressValue</span><span class="sxs-lookup"><span data-stu-id="c5ac5-166">ipAddressValue</span></span>| <span data-ttu-id="c5ac5-167">此值為 hello hello DNS 記錄所解析的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-167">This value is hello IP address that hello DNS record resolves.</span></span>|

## <a name="view-records"></a><span data-ttu-id="c5ac5-168">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="c5ac5-168">View records</span></span>

<span data-ttu-id="c5ac5-169">在 hello 的 hello DNS 區域刀鋒視窗的下半部，您可以看到 hello hello DNS 區域的記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-169">In hello lower part of hello DNS zone blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="c5ac5-170">您應該會看到 hello 預設 DNS 和 SOA 記錄，也就建立在每個區域中加上您建立任何新記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-170">You should see hello default DNS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

![區域](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a><span data-ttu-id="c5ac5-172">更新名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="c5ac5-172">Update name servers</span></span>

<span data-ttu-id="c5ac5-173">您可以在該程式的 DNS 區域與記錄已設定正確，您需要 tooconfigure 滿足您的網域名稱 toouse hello Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-173">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="c5ac5-174">這可讓其他使用者 hello 網際網路 toofind DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-174">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="c5ac5-175">您的區域 hello 名稱伺服器提供 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="c5ac5-175">hello name servers for your zone are given in hello Azure portal:</span></span>

![區域](./media/dns-getstarted-portal/viewzonens500.png)

<span data-ttu-id="c5ac5-177">這些名稱伺服器應該設有 hello 網域名稱註冊機構 （您購買 hello 網域名稱）。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-177">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="c5ac5-178">您的註冊機構提供 hello 選項 tooset hello hello 網域名稱伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-178">Your registrar offers hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="c5ac5-179">如需詳細資訊，請參閱[委派您網域 tooAzure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-179">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="c5ac5-180">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="c5ac5-180">Delete all resources</span></span>

<span data-ttu-id="c5ac5-181">在本文中完成下列步驟的 hello 建立 toodelete 所有資源：</span><span class="sxs-lookup"><span data-stu-id="c5ac5-181">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="c5ac5-182">在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-182">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="c5ac5-183">按一下 hello **MyResourceGroup** hello 資源刀鋒視窗中所有資源都群組。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-183">Click hello **MyResourceGroup** resource group in hello All resources blade.</span></span> <span data-ttu-id="c5ac5-184">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**MyResourceGroup**在 hello**依名稱篩選...**</span><span class="sxs-lookup"><span data-stu-id="c5ac5-184">If hello subscription you selected already has several resources in it, you can enter **MyResourceGroup** in hello **Filter by name…**</span></span> <span data-ttu-id="c5ac5-185">方塊 tooeasily 存取 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-185">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="c5ac5-186">在 [hello **MyResourceGroup**刀鋒視窗中，按一下 hello**刪除**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-186">In hello **MyResourceGroup** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="c5ac5-187">hello 入口網站需要您想要 toodelete hello 資源群組 tooconfirm tootype hello 名稱它。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-187">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="c5ac5-188">按一下**刪除**，型別*MyResourceGroup* hello 資源群組名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-188">Click **Delete**, Type *MyResourceGroup* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="c5ac5-189">刪除資源群組會刪除 hello 資源群組中的所有資源，所以一定會確定 tooconfirm hello 內容的資源群組然後再刪除。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-189">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="c5ac5-190">hello 入口網站刪除 hello 的資源群組中包含的所有資源，然後都刪除本身 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-190">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="c5ac5-191">這個程序需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-191">This process takes several minutes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c5ac5-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5ac5-192">Next steps</span></span>

<span data-ttu-id="c5ac5-193">toolearn 進一步了解 Azure DNS，請參閱[Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-193">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="c5ac5-194">進一步了解管理 Azure DNS 的 DNS 記錄 toolearn 看到[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c5ac5-194">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

