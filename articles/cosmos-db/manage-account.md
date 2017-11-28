---
title: "透過 Azure 入口網站管理 Azure Cosmos DB 帳戶 | Microsoft Docs"
description: "了解如何透過 Azure 入口網站管理 Azure Cosmos DB 帳戶。 尋找使用 Azure 入口網站來檢視、複製、刪除和存取帳戶的指南。"
keywords: "Azure 入口網站, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="c9e6d-105">如何管理 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="c9e6d-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="c9e6d-106">了解如何在 Azure 入口網站中設定全域一致性、使用金鑰，以及刪除 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="c9e6d-107"><a id="consistency"></a>管理 Azure Cosmos DB 一致性設定</span><span class="sxs-lookup"><span data-stu-id="c9e6d-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="c9e6d-108">根據您應用程式的語意選取正確的一致性層級。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="c9e6d-109">您應該已藉由閱讀[使用一致性層級以最大化 Azure Cosmos DB 中的可用性和效能][consistency]，來熟悉 Azure Cosmos DB 中可用的一致性層級。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="c9e6d-110">Azure Cosmos DB 會在您資料庫帳戶可用的每個一致性層級提供一致性、可用性和效能保證。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="c9e6d-111">使用強式一致性層級設定您的資料庫帳戶，需要將您的資料限制為單一 Azure 區域且無法全域使用。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="c9e6d-112">另一方面，寬鬆的一致性層級 (限定過期、工作階段或最終) 讓您能夠將任意數目的 Azure 區域與您的資料庫帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="c9e6d-113">下列簡單步驟示範如何針對您的資料庫帳戶選取預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="c9e6d-114">指定 Azure Cosmos DB 帳戶的預設一致性</span><span class="sxs-lookup"><span data-stu-id="c9e6d-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="c9e6d-115">在 [Azure 入口網站](https://portal.azure.com/)中，存取您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="c9e6d-116">在帳戶刀鋒視窗中，按一下 [預設一致性] 。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="c9e6d-117">在 [預設一致性] 刀鋒視窗中，選取新的一致性層級，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="c9e6d-118">![預設一致性工作階段][5]</span><span class="sxs-lookup"><span data-stu-id="c9e6d-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="c9e6d-119"><a id="keys"></a>檢視、複製和重新產生存取金鑰</span><span class="sxs-lookup"><span data-stu-id="c9e6d-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="c9e6d-120">當您建立 Azure Cosmos DB 帳戶時，服務會產生兩個主要存取金鑰，用於存取 Azure Cosmos DB 帳戶時的驗證。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="c9e6d-121">透過提供這兩個存取金鑰，Azure Cosmos DB 讓您可以重新產生金鑰，同時又不需中斷 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="c9e6d-122">在 [Azure 入口網站](https://portal.azure.com/)中，從 [Azure Cosmos DB 帳戶] 刀鋒視窗上的資源功能表存取 [金鑰] 刀鋒視窗，以檢視、複製及重新產生用來存取 Azure Cosmos DB 帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Azure 入口網站 [金鑰] 刀鋒視窗的螢幕擷取畫面](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="c9e6d-124">[金鑰] 刀鋒視窗也包含主要和次要連接字串，可用來從[資料移轉工具](import-data.md)連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="c9e6d-125">此刀鋒視窗上也有唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="c9e6d-126">讀取和查詢為唯讀作業，建立、刪除和取代則並非唯讀作業。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="c9e6d-127">在 Azure 入口網站中複製存取金鑰</span><span class="sxs-lookup"><span data-stu-id="c9e6d-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="c9e6d-128">在 [金鑰] 刀鋒視窗上，按一下要複製之金鑰旁的 [複製] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![在 Azure 入口網站 [金鑰] 刀鋒視窗中檢視並複製存取金鑰](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="c9e6d-130">重新產生存取金鑰</span><span class="sxs-lookup"><span data-stu-id="c9e6d-130">Regenerate access keys</span></span>
<span data-ttu-id="c9e6d-131">您應定期變更 Azure Cosmos DB 帳戶的存取金鑰，讓連線更加安全。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="c9e6d-132">指派的兩個存取金鑰可讓您在重新產生一個存取金鑰的同時，使用另一個存取金鑰維持 Azure Cosmos DB 帳戶連線。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="c9e6d-133">重新產生存取金鑰會影響任何相依於目前金鑰的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="c9e6d-134">所有使用存取金鑰來存取 Azure Cosmos DB 帳戶的用戶端，都必須更新為使用新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="c9e6d-135">如果您的應用程式或雲端服務正在使用 Azure Cosmos DB 帳戶，除非您變換金鑰，否則會在重新產生金鑰後失去連線。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="c9e6d-136">下列步驟概述變換金鑰所牽涉的程序。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="c9e6d-137">更新應用程式程式碼中的存取金鑰，以參考 Azure Cosmos DB 帳戶的次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="c9e6d-138">重新產生 Azure Cosmos DB 帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="c9e6d-139">在 [Azure 入口網站](https://portal.azure.com/)中，存取您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="c9e6d-140">在 [Azure Cosmos DB 帳戶] 刀鋒視窗中，按一下 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="c9e6d-141">在 [金鑰] 刀鋒視窗中，按一下 [重新產生] 按鈕，然後按一下 [確定] 以確認要產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="c9e6d-142">![重新產生存取金鑰](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="c9e6d-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="c9e6d-143">一旦確認新的金鑰可供使用後 (重新產生後約 5 分鐘)，更新應用程式程式碼中的存取金鑰，以參考新的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="c9e6d-144">重新產生次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-144">Regenerate the secondary access key.</span></span>
   
    ![重新產生存取金鑰](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="c9e6d-146">新產生的金鑰可能需要經過幾分鐘之後才能用來存取 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="c9e6d-147">取得連接字串</span><span class="sxs-lookup"><span data-stu-id="c9e6d-147">Get the  connection string</span></span>
<span data-ttu-id="c9e6d-148">若要擷取連接字串，請執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="c9e6d-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="c9e6d-149">在 [Azure 入口網站](https://portal.azure.com)中，存取您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="c9e6d-150">在資源功能表中，按一下 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="c9e6d-151">按一下 [主要連接字串] 或 [次要連接字串] 方塊旁邊的 [複製] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="c9e6d-152">如果您要在 [Azure Cosmos DB 資料庫移轉工具](import-data.md)中使用連接字串，請在連接字串結尾加上資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="c9e6d-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="c9e6d-154"><a id="delete"></a> 刪除 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="c9e6d-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="c9e6d-155">若要從 Azure 入口網站中移除您不再使用的 Azure Cosmos DB 帳戶，請以滑鼠右鍵按一下帳戶名稱，然後按一下 [刪除帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![如何在 Azure 入口網站中刪除 Azure Cosmos DB 帳戶](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="c9e6d-157">在 [Azure 入口網站](https://portal.azure.com/)中，存取要刪除的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="c9e6d-158">在 [Azure Cosmos DB 帳戶] 刀鋒視窗上，以滑鼠右鍵按一下帳戶，然後按一下 [刪除帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="c9e6d-159">在後續的確認刀鋒視窗中輸入 Azure Cosmos DB 帳戶名稱，以確認您想要刪除該帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="c9e6d-160">按一下 [刪除]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-160">Click the **Delete** button.</span></span>

![如何在 Azure 入口網站中刪除 Azure Cosmos DB 帳戶](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="c9e6d-162"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="c9e6d-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="c9e6d-163">了解如何[開始使用 Azure Cosmos DB 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=402364)。</span><span class="sxs-lookup"><span data-stu-id="c9e6d-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
