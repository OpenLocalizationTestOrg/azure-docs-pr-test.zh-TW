---
title: "aaaManage hello Azure 入口網站透過 Azure Cosmos DB 帳戶 |Microsoft 文件"
description: "了解如何 toomanage Azure Cosmos DB 帳戶透過 hello Azure 入口網站。 尋找有關使用 hello Azure 入口網站 tooview、 複製、 刪除和存取帳戶的指南。"
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
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="2dd6b-105">如何 toomanage Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="2dd6b-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="2dd6b-106">深入了解 tooset 全域一致性，具有索引鍵，運作的方式，並刪除 Azure Cosmos DB 中的帳戶 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="2dd6b-107"><a id="consistency"></a>管理 Azure Cosmos DB 一致性設定</span><span class="sxs-lookup"><span data-stu-id="2dd6b-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="2dd6b-108">選取 hello 右一致性層級取決於您的應用程式的 hello 語意。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="2dd6b-109">您應該熟悉 Azure Cosmos DB 中的 hello 可用的一致性層級讀取[toomaximize 可用性和效能 Azure Cosmos DB 中的使用的一致性層級][consistency]。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="2dd6b-110">Azure Cosmos DB 會在您資料庫帳戶可用的每個一致性層級提供一致性、可用性和效能保證。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="2dd6b-111">設定您的資料庫帳戶的強式一致性層級需要您的資料是局部的 tooa 單一 Azure 區域和全域使用。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="2dd6b-112">Hello 另一方面，hello 鬆散的一致性層級已繫結的失效，工作階段或最終啟用您 tooassociate 任意數目的資料庫帳戶的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="2dd6b-113">hello 下列簡單步驟會告訴您如何 tooselect hello 資料庫帳戶的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="2dd6b-114">Azure Cosmos DB 帳戶 toospecify hello 預設一致性</span><span class="sxs-lookup"><span data-stu-id="2dd6b-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="2dd6b-115">在 hello [Azure 入口網站](https://portal.azure.com/)，存取您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="2dd6b-116">在 hello 帳戶刀鋒視窗中，按一下 **預設一致性**。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="2dd6b-117">在 hello**預設一致性**刀鋒視窗中，選取 hello 新一致性層級，然後按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="2dd6b-118">![預設一致性工作階段][5]</span><span class="sxs-lookup"><span data-stu-id="2dd6b-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="2dd6b-119"><a id="keys"></a>檢視、複製和重新產生存取金鑰</span><span class="sxs-lookup"><span data-stu-id="2dd6b-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="2dd6b-120">當您建立 Azure Cosmos DB 帳戶時，hello 服務就會產生兩個存取 hello Azure Cosmos DB 帳戶時可以用於驗證的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="2dd6b-121">藉由提供兩個存取金鑰，Azure Cosmos DB 可讓您使用不中斷 tooyour Azure Cosmos DB 帳戶 tooregenerate hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="2dd6b-122">在 hello [Azure 入口網站](https://portal.azure.com/)，存取 hello**金鑰**hello 資源] 功能表的 [hello] 刀鋒視窗**Azure Cosmos DB 帳戶**刀鋒視窗 tooview、 複製和重新產生 hello 存取金鑰會使用的 tooaccess Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Azure 入口網站 [金鑰] 刀鋒視窗的螢幕擷取畫面](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="2dd6b-124">hello**金鑰**刀鋒視窗中也包含主要和次要連接字串可能是使用的 tooconnect tooyour 帳戶從 hello[資料移轉工具](import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="2dd6b-125">此刀鋒視窗上也有唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="2dd6b-126">讀取和查詢為唯讀作業，建立、刪除和取代則並非唯讀作業。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="2dd6b-127">Hello Azure 入口網站中複製存取金鑰</span><span class="sxs-lookup"><span data-stu-id="2dd6b-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="2dd6b-128">在 hello**金鑰**刀鋒視窗中，按一下 hello**複製**想 toocopy 按鈕 toohello hello 機碼的權限。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![檢視與 hello Azure 入口網站中，索引鍵 刀鋒視窗中複製存取金鑰](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="2dd6b-130">重新產生存取金鑰</span><span class="sxs-lookup"><span data-stu-id="2dd6b-130">Regenerate access keys</span></span>
<span data-ttu-id="2dd6b-131">您應該變更 hello 存取金鑰 tooyour Azure Cosmos DB 帳戶 toohelp 定期更新您的連接更安全。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="2dd6b-132">兩個存取金鑰指派 tooenable 您 toomaintain 連線 toohello 使用一個存取金鑰，當您重新產生 Azure Cosmos DB 帳戶 hello 其他存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="2dd6b-133">重新產生存取金鑰會影響任何相依於 hello 目前金鑰的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="2dd6b-134">使用 hello 存取金鑰 tooaccess hello Azure Cosmos DB 帳戶的所有用戶端必須更新的 toouse hello 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="2dd6b-135">如果您有應用程式或使用 hello Azure Cosmos DB 帳戶的雲端服務，您將會遺失 hello 連線如果您重新產生金鑰，除非您復原您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="2dd6b-136">hello 下列步驟概述 hello 參與復原您金鑰的程序。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="2dd6b-137">更新您的應用程式程式碼 tooreference hello 次要存取金鑰的 hello Azure Cosmos DB 帳戶中的 hello 存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="2dd6b-138">重新產生 hello Azure Cosmos DB 帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="2dd6b-139">在 hello [Azure 入口網站](https://portal.azure.com/)，存取您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="2dd6b-140">在 hello **Azure Cosmos DB 帳戶**刀鋒視窗中，按一下 **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="2dd6b-141">Hello 上**金鑰**刀鋒視窗中，按一下 hello 重新產生] 按鈕，然後按一下 [**確定**tooconfirm 想 toogenerate 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="2dd6b-142">![重新產生存取金鑰](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="2dd6b-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="2dd6b-143">一旦您已確認該 hello 新索引鍵是可供使用 （大約 5 分鐘之後重新產生），就會更新 hello 的應用程式程式碼 tooreference hello 新主要存取金鑰的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="2dd6b-144">重新產生 hello 次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-144">Regenerate hello secondary access key.</span></span>
   
    ![重新產生存取金鑰](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="2dd6b-146">它可能需要幾分鐘後才可以使用的 tooaccess 新產生的金鑰。 您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="2dd6b-147">取得 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="2dd6b-147">Get hello  connection string</span></span>
<span data-ttu-id="2dd6b-148">tooretrieve 您的連接字串中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="2dd6b-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="2dd6b-149">在 hello [Azure 入口網站](https://portal.azure.com)，存取您的 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="2dd6b-150">在 hello 資源功能表上，按一下 **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="2dd6b-151">按一下 hello**複製**按鈕的下一個 toohello**主要連接字串**或**次要連接字串**方塊。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="2dd6b-152">如果您使用 hello 連接字串中的 hello [Azure Cosmos DB 資料庫移轉工具](import-data.md)，附加 hello hello 連接字串的資料庫名稱 toohello 結尾。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="2dd6b-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="2dd6b-154"><a id="delete"></a> 刪除 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="2dd6b-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="2dd6b-155">tooremove Azure Cosmos DB 帳戶從 hello Azure 入口網站，您無法再使用，以滑鼠右鍵按一下 hello 帳戶名稱，再按一下**刪除帳戶**。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![如何在帳戶 toodelete Azure Cosmos DB hello Azure 入口網站](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="2dd6b-157">在 hello [Azure 入口網站](https://portal.azure.com/)，存取您想 toodelete hello Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="2dd6b-158">在 hello **Azure Cosmos DB 帳戶**刀鋒視窗中，以滑鼠右鍵按一下 hello 帳戶，然後按一下**刪除帳戶**。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="2dd6b-159">在 hello 產生確認刀鋒視窗中，輸入您想 toodelete hello 帳戶 hello Azure Cosmos DB 帳戶名稱 tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="2dd6b-160">按一下 hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-160">Click hello **Delete** button.</span></span>

![如何在帳戶 toodelete Azure Cosmos DB hello Azure 入口網站](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="2dd6b-162"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="2dd6b-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="2dd6b-163">了解如何太[開始使用 Azure Cosmos DB 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=402364)。</span><span class="sxs-lookup"><span data-stu-id="2dd6b-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
