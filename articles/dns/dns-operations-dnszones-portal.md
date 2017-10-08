---
title: "aaaManage DNS 區域中 Azure DNS-Azure 入口網站 |Microsoft 文件"
description: "您可以管理使用 hello Azure 入口網站的 DNS 區域。 本文說明如何刪除 tooupdate，，和 Azure DNS 上建立 DNS 區域"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="7c074-104">如何在 toomanage DNS 區域 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7c074-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c074-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="7c074-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="7c074-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c074-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="7c074-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7c074-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="7c074-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7c074-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="7c074-109">本文章將示範如何 toomanage 您的 DNS 區域使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7c074-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="7c074-110">您也可以管理您的 DNS 區域使用 hello 跨平台[Azure CLI](dns-operations-dnszones-cli.md)或 hello Azure [PowerShell](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="7c074-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="7c074-111">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="7c074-111">Create a DNS zone</span></span>

1. <span data-ttu-id="7c074-112">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7c074-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="7c074-113">在 hello 中樞功能表中，按一下，然後按一下**新增 > 網路 >** ，然後按一下 **DNS 區域**tooopen hello 建立 DNS 區域刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7c074-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 區域](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="7c074-115">在 hello**建立 DNS 區域**刀鋒視窗中輸入 hello 下列值，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="7c074-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="7c074-116">**設定**</span><span class="sxs-lookup"><span data-stu-id="7c074-116">**Setting**</span></span> | <span data-ttu-id="7c074-117">**值**</span><span class="sxs-lookup"><span data-stu-id="7c074-117">**Value**</span></span> | <span data-ttu-id="7c074-118">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="7c074-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7c074-119">**名稱**</span><span class="sxs-lookup"><span data-stu-id="7c074-119">**Name**</span></span>|<span data-ttu-id="7c074-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="7c074-120">contoso.com</span></span>|<span data-ttu-id="7c074-121">hello hello DNS 區域名稱</span><span class="sxs-lookup"><span data-stu-id="7c074-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="7c074-122">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="7c074-122">**Subscription**</span></span>|<span data-ttu-id="7c074-123">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="7c074-123">[Your subscription]</span></span>|<span data-ttu-id="7c074-124">選取的訂用帳戶 toocreate hello DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="7c074-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="7c074-125">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="7c074-125">**Resource group**</span></span>|<span data-ttu-id="7c074-126">**建立新的︰**contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="7c074-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="7c074-127">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="7c074-127">Create a resource group.</span></span> <span data-ttu-id="7c074-128">hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="7c074-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="7c074-129">深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="7c074-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7c074-130">**位置**</span><span class="sxs-lookup"><span data-stu-id="7c074-130">**Location**</span></span>|<span data-ttu-id="7c074-131">美國西部</span><span class="sxs-lookup"><span data-stu-id="7c074-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="7c074-132">hello 資源群組是指 toohello hello 資源群組中，位置且不會影響 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="7c074-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="7c074-133">hello DNS 區域位置一定是 「 全域 」，而且不會顯示。</span><span class="sxs-lookup"><span data-stu-id="7c074-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="7c074-134">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="7c074-134">List DNS zones</span></span>

<span data-ttu-id="7c074-135">在 hello Azure 入口網站中瀏覽過**更多服務** > **網路** > **DNS 區域**。</span><span class="sxs-lookup"><span data-stu-id="7c074-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="7c074-136">每個 DNS 區域都是它自己的資源，記錄集數目和名稱伺服器數目等資訊皆可在此檢視中檢視。</span><span class="sxs-lookup"><span data-stu-id="7c074-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="7c074-137">hello 資料行**名稱伺服器**不在 hello 預設檢視中，tooadd 按一下**資料行**，選取**名稱伺服器**按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="7c074-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![列出 DNS 區域](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="7c074-139">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="7c074-139">Delete a DNS zone</span></span>

<span data-ttu-id="7c074-140">瀏覽 tooa hello 入口網站中的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="7c074-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="7c074-141">在 hello **DNS 區域**刀鋒視窗中，按一下 **刪除區域**。</span><span class="sxs-lookup"><span data-stu-id="7c074-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="7c074-142">您必須提示的 tooconfirm，您會想 toodelete hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="7c074-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="7c074-143">刪除 DNS 區域時，也會刪除所有包含在 hello 區域的 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="7c074-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c074-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c074-144">Next steps</span></span>

<span data-ttu-id="7c074-145">深入了解如何與您的 DNS 區域記錄造訪 toowork[開始使用 Azure DNS 使用 hello Azure 入口網站](dns-getstarted-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7c074-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
