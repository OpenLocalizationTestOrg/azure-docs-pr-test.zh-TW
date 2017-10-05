---
title: "使用 Azure DNS 管理 DNS 記錄集和記錄 |Microsoft Docs"
description: "Azure DNS 可在裝載您的網域時，提供管理 DNS 記錄集和記錄的功能。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="3aad6-103">使用 Azure 入口網站管理 DNS 記錄和記錄集</span><span class="sxs-lookup"><span data-stu-id="3aad6-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3aad6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3aad6-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="3aad6-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3aad6-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="3aad6-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3aad6-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="3aad6-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3aad6-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="3aad6-108">本文說明如何使用 Azure 入口網站管理 DNS 區域的記錄集和記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="3aad6-109">請務必了解 DNS 記錄集和個別 DNS 記錄之間的差別。</span><span class="sxs-lookup"><span data-stu-id="3aad6-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="3aad6-110">記錄集是指一個區域中有相同名稱和相同類型的記錄集合。</span><span class="sxs-lookup"><span data-stu-id="3aad6-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="3aad6-111">如需詳細資訊，請參閱 [使用 Azure 入口網站建立 DNS 記錄集和記錄](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3aad6-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="3aad6-112">建立新的記錄集和記錄</span><span class="sxs-lookup"><span data-stu-id="3aad6-112">Create a new record set and record</span></span>

<span data-ttu-id="3aad6-113">若要在 Azure 入口網站中建立記錄集，請參閱 [使用 Azure 入口網站建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3aad6-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="3aad6-114">檢視記錄集</span><span class="sxs-lookup"><span data-stu-id="3aad6-114">View a record set</span></span>

1. <span data-ttu-id="3aad6-115">在 Azure 入口網站中，移至 [DNS 區域]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3aad6-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="3aad6-116">搜尋記錄集並加以選取。</span><span class="sxs-lookup"><span data-stu-id="3aad6-116">Search for the record set and select it.</span></span> <span data-ttu-id="3aad6-117">這會開啟記錄集屬性。</span><span class="sxs-lookup"><span data-stu-id="3aad6-117">This opens the record set properties.</span></span>

    ![搜尋資料錄集](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="3aad6-119">將新記錄加入記錄集</span><span class="sxs-lookup"><span data-stu-id="3aad6-119">Add a new record to a record set</span></span>

<span data-ttu-id="3aad6-120">任何記錄集最多只能加入 20 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="3aad6-121">記錄集不能包含兩筆相同的記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="3aad6-122">您可以建立空的記錄集 (沒有記錄)，但該記錄集不會出現在 Azure DNS 名稱伺服器上。</span><span class="sxs-lookup"><span data-stu-id="3aad6-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="3aad6-123">類型為 CNAME 的記錄集最多只能包含一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="3aad6-124">在 DNS 區域的 [記錄集屬性]  刀鋒視窗中，按一下您想要在其中新增記錄的記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![選取記錄集](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="3aad6-126">在欄位中填入資料，藉以指定記錄集屬性。</span><span class="sxs-lookup"><span data-stu-id="3aad6-126">Specify the record set properties by filling in the fields.</span></span>

    ![新增記錄](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="3aad6-128">按一下刀鋒視窗頂端的 [儲存]  來儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="3aad6-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="3aad6-129">然後關閉刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3aad6-129">Then close the blade.</span></span>
4. <span data-ttu-id="3aad6-130">您會在角落中看到正在儲存記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-130">In the corner, you will see that the record is saving.</span></span>

    ![儲存記錄集](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="3aad6-132">儲存記錄之後，[DNS 區域]  刀鋒視窗上的值將會反映新的記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="3aad6-133">更新記錄</span><span class="sxs-lookup"><span data-stu-id="3aad6-133">Update a record</span></span>

<span data-ttu-id="3aad6-134">在更新現有記錄集中的記錄時，您可更新的欄位取決於您正在使用的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="3aad6-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="3aad6-135">在記錄集的 [記錄集屬性]  刀鋒視窗中搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="3aad6-136">修改記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-136">Modify the record.</span></span> <span data-ttu-id="3aad6-137">當您修改記錄時，您可以變更記錄的可用設定。</span><span class="sxs-lookup"><span data-stu-id="3aad6-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="3aad6-138">在下列範例中，已選取 [IP 位址]  欄位，而該 IP 位址正在進行修改。</span><span class="sxs-lookup"><span data-stu-id="3aad6-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![修改記錄](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="3aad6-140">按一下刀鋒視窗頂端的 [儲存]  來儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="3aad6-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="3aad6-141">您將會在右上角看到記錄已儲存的通知。</span><span class="sxs-lookup"><span data-stu-id="3aad6-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![已儲存記錄集](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="3aad6-143">儲存記錄之後，[DNS 區域]  刀鋒視窗上記錄集的值將會反映更新的記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="3aad6-144">從記錄集移除記錄</span><span class="sxs-lookup"><span data-stu-id="3aad6-144">Remove a record from a record set</span></span>

<span data-ttu-id="3aad6-145">您可以使用 Azure 入口網站來從記錄集移除記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="3aad6-146">請注意，移除記錄集的最後一筆記錄不會刪除記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="3aad6-147">在記錄集的 [記錄集屬性]  刀鋒視窗中搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="3aad6-148">按一下您想要移除的記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-148">Click the record that you want to remove.</span></span> <span data-ttu-id="3aad6-149">然後選取 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="3aad6-149">Then select **Remove**.</span></span>

    ![移除記錄](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="3aad6-151">按一下刀鋒視窗頂端的 [儲存]  來儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="3aad6-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="3aad6-152">移除記錄之後，[DNS 區域]  刀鋒視窗上記錄的值將會反映移除。</span><span class="sxs-lookup"><span data-stu-id="3aad6-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="3aad6-153"><a name="delete"></a>刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="3aad6-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="3aad6-154">在記錄集的 [記錄集屬性] 刀鋒視窗中，按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="3aad6-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![刪除記錄集](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="3aad6-156">隨即會出現訊息，詢問您是否要刪除記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="3aad6-157">確認該名稱符合您想要刪除的記錄集，然後按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="3aad6-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="3aad6-158">在 [DNS 區域]  刀鋒視窗中，確認不再看到該記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="3aad6-159">使用 NS 和 SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="3aad6-159">Work with NS and SOA records</span></span>

<span data-ttu-id="3aad6-160">自動建立之 NS 和 SOA 記錄的管理方式不同於其他記錄類型。</span><span class="sxs-lookup"><span data-stu-id="3aad6-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="3aad6-161">修改 SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="3aad6-161">Modify SOA records</span></span>

<span data-ttu-id="3aad6-162">您無法在區域頂點 (名稱 = "@") 自動建立的 SOA 記錄集中新增或移除記錄。</span><span class="sxs-lookup"><span data-stu-id="3aad6-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="3aad6-163">不過，您可以修改 SOA 記錄 (「主機」除外) 和記錄集 TTL 內的任何參數。</span><span class="sxs-lookup"><span data-stu-id="3aad6-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="3aad6-164">在區域頂點修改 NS 記錄</span><span class="sxs-lookup"><span data-stu-id="3aad6-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="3aad6-165">系統會自動使用每個 DNS 區域在區域頂點建立 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="3aad6-166">此記錄集包含指派給區域的 Azure DNS 名稱伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="3aad6-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="3aad6-167">您可以將其他名稱伺服器新增至此 NS 記錄集，以支援使用多個 DNS 提供者的共同裝載網域。</span><span class="sxs-lookup"><span data-stu-id="3aad6-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="3aad6-168">您也可以修改此記錄集的 TTL 和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3aad6-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="3aad6-169">不過，您無法移除或修改預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="3aad6-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="3aad6-170">請注意，這只適用於區域頂點的 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="3aad6-171">區域中的其他 NS 記錄集 (如用於委派子區域) 可以修改，沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="3aad6-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="3aad6-172">刪除 SOA 或 NS 記錄集</span><span class="sxs-lookup"><span data-stu-id="3aad6-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="3aad6-173">您無法在建立區域時所自動建立的區域頂點 (名稱 = "@") 刪除 SOA 和 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="3aad6-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="3aad6-174">當您刪除該區域時，就會自動刪除它們。</span><span class="sxs-lookup"><span data-stu-id="3aad6-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aad6-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3aad6-175">Next steps</span></span>

* <span data-ttu-id="3aad6-176">如需 Azure DNS 的詳細資訊，請參閱 [Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3aad6-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="3aad6-177">如需自動化 DNS 的相關資訊，請參閱 [使用 .NET SDK 建立 DNS 區域和記錄集](dns-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="3aad6-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="3aad6-178">如需反向 DNS 記錄的詳細資訊，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3aad6-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
