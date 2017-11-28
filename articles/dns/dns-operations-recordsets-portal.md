---
title: "aaaManage DNS 記錄集而且要使用 Azure DNS 記錄 |Microsoft 文件"
description: "Azure DNS 提供 hello 功能 toomanage DNS 記錄設定和裝載您的網域時，記錄。"
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
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="33ae8-103">使用 hello Azure 入口網站管理 DNS 記錄和資料錄集</span><span class="sxs-lookup"><span data-stu-id="33ae8-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="33ae8-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="33ae8-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="33ae8-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="33ae8-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="33ae8-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="33ae8-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="33ae8-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33ae8-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="33ae8-108">本文章將示範如何 toomanage 資料錄集和您所使用的 DNS 區域的記錄 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="33ae8-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="33ae8-109">它是重要的 toounderstand hello 差異 DNS 資料錄集和個別的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="33ae8-110">資料錄集是在區域中有的 hello 相同名稱，且會 hello 相同類型的記錄的集合。</span><span class="sxs-lookup"><span data-stu-id="33ae8-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="33ae8-111">如需詳細資訊，請參閱[建立 DNS 記錄集而且要使用的記錄 hello Azure 入口網站](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="33ae8-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="33ae8-112">建立新的記錄集和記錄</span><span class="sxs-lookup"><span data-stu-id="33ae8-112">Create a new record set and record</span></span>

<span data-ttu-id="33ae8-113">請參閱 toocreate hello Azure 入口網站中設定的記錄[建立 DNS 記錄，使用 hello Azure 入口網站](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="33ae8-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="33ae8-114">檢視記錄集</span><span class="sxs-lookup"><span data-stu-id="33ae8-114">View a record set</span></span>

1. <span data-ttu-id="33ae8-115">在 hello Azure 入口網站，移 toohello **DNS 區域**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="33ae8-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="33ae8-116">搜尋 hello 資料錄集，並選取它。</span><span class="sxs-lookup"><span data-stu-id="33ae8-116">Search for hello record set and select it.</span></span> <span data-ttu-id="33ae8-117">這會開啟 hello 記錄集屬性。</span><span class="sxs-lookup"><span data-stu-id="33ae8-117">This opens hello record set properties.</span></span>

    ![搜尋資料錄集](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="33ae8-119">加入新的記錄 tooa 資料錄集</span><span class="sxs-lookup"><span data-stu-id="33ae8-119">Add a new record tooa record set</span></span>

<span data-ttu-id="33ae8-120">您可以加總 too20 記錄 tooany 記錄集。</span><span class="sxs-lookup"><span data-stu-id="33ae8-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="33ae8-121">記錄集不能包含兩筆相同的記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="33ae8-122">可以建立空的資料錄集 （具有零的記錄），但不是會出現在 hello Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="33ae8-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="33ae8-123">類型為 CNAME 的記錄集最多只能包含一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="33ae8-124">在 hello**記錄設定屬性**刀鋒視窗，您的 DNS 區域，按一下 hello 記錄設定您想 tooadd 某筆記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![選取記錄集](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="33ae8-126">指定 hello 記錄填入 hello 欄位中設定屬性。</span><span class="sxs-lookup"><span data-stu-id="33ae8-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![新增記錄](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="33ae8-128">按一下**儲存**在 hello 頂端 hello 刀鋒視窗 toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="33ae8-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="33ae8-129">然後關閉 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="33ae8-129">Then close hello blade.</span></span>
4. <span data-ttu-id="33ae8-130">在 hello 角中，您會看到 hello 記錄會儲存。</span><span class="sxs-lookup"><span data-stu-id="33ae8-130">In hello corner, you will see that hello record is saving.</span></span>

    ![儲存記錄集](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="33ae8-132">儲存 hello 記錄之後，hello 上 hello 值**DNS 區域**刀鋒視窗中會反映 hello 新記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="33ae8-133">更新記錄</span><span class="sxs-lookup"><span data-stu-id="33ae8-133">Update a record</span></span>

<span data-ttu-id="33ae8-134">當您更新現有的記錄組中的記錄時，您可以更新 hello 欄位，取決於 hello 您正在使用的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="33ae8-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="33ae8-135">在 hello**記錄設定屬性**刀鋒視窗中為您的資料錄集，hello 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="33ae8-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="33ae8-136">修改 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-136">Modify hello record.</span></span> <span data-ttu-id="33ae8-137">當您修改記錄時，您可以變更 hello hello 記錄可用的設定。</span><span class="sxs-lookup"><span data-stu-id="33ae8-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="33ae8-138">在下列範例的 hello，hello **IP 位址**選取欄位，而且 hello IP 位址為正在修改的 hello 程序中。</span><span class="sxs-lookup"><span data-stu-id="33ae8-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![修改記錄](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="33ae8-140">按一下**儲存**在 hello 頂端 hello 刀鋒視窗 toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="33ae8-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="33ae8-141">Hello 右上角，您會看到已保存 hello 記錄的 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="33ae8-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![已儲存記錄集](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="33ae8-143">Hello 記錄的 hello 值儲存 hello 記錄之後，設定 hello **DNS 區域**刀鋒視窗中會反映 hello 更新記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="33ae8-144">從記錄集移除記錄</span><span class="sxs-lookup"><span data-stu-id="33ae8-144">Remove a record from a record set</span></span>

<span data-ttu-id="33ae8-145">您可以使用的記錄組從 hello Azure 入口網站 tooremove 記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="33ae8-146">請注意，從資料錄集移除 hello 最後一筆記錄並不會刪除 hello 記錄集。</span><span class="sxs-lookup"><span data-stu-id="33ae8-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="33ae8-147">在 hello**記錄設定屬性**刀鋒視窗中為您的資料錄集，hello 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="33ae8-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="33ae8-148">按一下您想 tooremove hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="33ae8-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="33ae8-149">然後選取 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="33ae8-149">Then select **Remove**.</span></span>

    ![移除記錄](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="33ae8-151">按一下**儲存**在 hello 頂端 hello 刀鋒視窗 toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="33ae8-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="33ae8-152">移除 hello 記錄之後，hello 上 hello hello 記錄的值**DNS 區域**刀鋒視窗中會反映 hello 移除。</span><span class="sxs-lookup"><span data-stu-id="33ae8-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="33ae8-153"><a name="delete"></a>刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="33ae8-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="33ae8-154">在 hello**記錄設定屬性**刀鋒視窗中為您的資料錄集，按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="33ae8-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![刪除記錄集](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="33ae8-156">訊息會出現，詢問您是否 toodelete hello 記錄集。</span><span class="sxs-lookup"><span data-stu-id="33ae8-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="33ae8-157">請確認您想 toodelete，，然後按一下設定 hello 名稱相符項目 hello 記錄**是**。</span><span class="sxs-lookup"><span data-stu-id="33ae8-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="33ae8-158">在 hello **DNS 區域**刀鋒視窗中，確認 hello 記錄集不再顯示。</span><span class="sxs-lookup"><span data-stu-id="33ae8-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="33ae8-159">使用 NS 和 SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="33ae8-159">Work with NS and SOA records</span></span>

<span data-ttu-id="33ae8-160">自動建立之 NS 和 SOA 記錄的管理方式不同於其他記錄類型。</span><span class="sxs-lookup"><span data-stu-id="33ae8-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="33ae8-161">修改 SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="33ae8-161">Modify SOA records</span></span>

<span data-ttu-id="33ae8-162">您無法加入或移除 hello 自動建立在 hello 區域的 apex 設定 SOA 記錄中的記錄 (名稱 ="@")。</span><span class="sxs-lookup"><span data-stu-id="33ae8-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="33ae8-163">不過，您可以修改任何 hello （除了 「 主機 」） 的 SOA 記錄中的 hello 參數，而且 hello 記錄設定的 TTL。</span><span class="sxs-lookup"><span data-stu-id="33ae8-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="33ae8-164">修改在 hello 區域的 apex NS 記錄</span><span class="sxs-lookup"><span data-stu-id="33ae8-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="33ae8-165">在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="33ae8-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="33ae8-166">它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="33ae8-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="33ae8-167">您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。</span><span class="sxs-lookup"><span data-stu-id="33ae8-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="33ae8-168">您也可以修改 hello TTL 和此記錄集的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="33ae8-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="33ae8-169">不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="33ae8-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="33ae8-170">請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。</span><span class="sxs-lookup"><span data-stu-id="33ae8-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="33ae8-171">如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。</span><span class="sxs-lookup"><span data-stu-id="33ae8-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="33ae8-172">刪除 SOA 或 NS 記錄集</span><span class="sxs-lookup"><span data-stu-id="33ae8-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="33ae8-173">您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (名稱 ="@")，會自動建立時，建立 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="33ae8-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="33ae8-174">當您刪除 hello 區域時，它們會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="33ae8-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33ae8-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33ae8-175">Next steps</span></span>

* <span data-ttu-id="33ae8-176">如需有關 Azure DNS 的詳細資訊，請參閱 hello [Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="33ae8-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="33ae8-177">如需有關如何自動化 DNS 的詳細資訊，請參閱[建立 DNS 區域和使用資料錄集 hello.NET SDK](dns-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="33ae8-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="33ae8-178">如需反向 DNS 記錄的詳細資訊，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="33ae8-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
