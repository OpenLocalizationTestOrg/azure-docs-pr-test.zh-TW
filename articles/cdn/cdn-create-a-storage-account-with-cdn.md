---
title: "aaaIntegrate Azure CDN 的 Azure 儲存體帳戶 |Microsoft 文件"
description: "了解 toouse hello Azure 內容傳遞網路 (CDN) toodeliver 高頻寬內容快取從 Azure 儲存體的 blob。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="418dc-103">整合 Azure 儲存體帳戶與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="418dc-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="418dc-104">CDN 可啟用的 toocache 來自您 Azure 儲存體的內容。</span><span class="sxs-lookup"><span data-stu-id="418dc-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="418dc-105">它提供開發人員一套傳遞高頻寬內容的快取 blob 和靜態計算執行個體上的 hello 美國、 歐洲、 亞洲、 澳大利亞及南美洲的實體節點內容的全球解決方案。</span><span class="sxs-lookup"><span data-stu-id="418dc-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="418dc-106">步驟 1：建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="418dc-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="418dc-107">使用下列程序 toocreate Azure 訂用帳戶的新儲存體帳戶的 hello。</span><span class="sxs-lookup"><span data-stu-id="418dc-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="418dc-108">有了儲存體帳戶，才能存取 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="418dc-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="418dc-109">hello 儲存體帳戶代表 hello hello 存取 hello Azure 儲存體服務元件的每個命名空間的最高層級： Blob 服務、 佇列服務和表格服務。</span><span class="sxs-lookup"><span data-stu-id="418dc-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="418dc-110">如需詳細資訊，請參閱 toohello[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="418dc-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="418dc-111">toocreate 儲存體帳戶，您必須是 hello 服務系統管理員或共同管理員 hello 相關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="418dc-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="418dc-112">有數種方法，您可以使用 toocreate 儲存體帳戶，包括 hello Azure 入口網站和 Powershell。</span><span class="sxs-lookup"><span data-stu-id="418dc-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="418dc-113">此教學課程中，我們將使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="418dc-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="418dc-114">**toocreate Azure 訂用帳戶的儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="418dc-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="418dc-115">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="418dc-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="418dc-116">在 hello 左上角，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="418dc-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="418dc-117">在 hello**新增**對話方塊中，選取**資料 + 儲存體**，然後按一下**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="418dc-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="418dc-118">hello**建立儲存體帳戶**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="418dc-118">hello **Create storage account** blade appears.</span></span>   

    ![建立儲存體帳戶][create-new-storage-account]  

3. <span data-ttu-id="418dc-120">在 hello**名稱**欄位中，輸入的子網域名稱。</span><span class="sxs-lookup"><span data-stu-id="418dc-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="418dc-121">此項目可以包含 3 至 24 個小寫字母與數字。</span><span class="sxs-lookup"><span data-stu-id="418dc-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="418dc-122">這個值會成為 hello hello 用來定址 hello 訂用帳戶的 Blob、 佇列或表格資源的 URI 內的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="418dc-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="418dc-123">若要解決 hello Blob 服務中的容器資源，您會將 URI 中 hello 遵循格式，其中 *&lt;StorageAccountLabel&gt;* 是指您在輸入 toohello 值**輸入的URL**:</span><span class="sxs-lookup"><span data-stu-id="418dc-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="418dc-124">http://&lt;StorageAcountLabel&gt;.blob.core.windows.net/&lt;mycontainer&gt;</span><span class="sxs-lookup"><span data-stu-id="418dc-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="418dc-125">**重要事項：** hello URL 標籤 form hello 子網域的 hello 儲存體帳戶 URI，而且必須是唯一在 Azure 中的所有託管服務。</span><span class="sxs-lookup"><span data-stu-id="418dc-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="418dc-126">以程式設計方式存取此帳戶時，這個值也會用做為 hello hello 網站，或此儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="418dc-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="418dc-127">保留 hello 的預設值**部署模型**，**帳戶類型**，**效能**，和**複寫**。</span><span class="sxs-lookup"><span data-stu-id="418dc-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="418dc-128">選取 hello**訂用帳戶**hello 儲存體帳戶，將會搭配使用。</span><span class="sxs-lookup"><span data-stu-id="418dc-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="418dc-129">選取或建立 **資源群組**。</span><span class="sxs-lookup"><span data-stu-id="418dc-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="418dc-130">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="418dc-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="418dc-131">選取儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="418dc-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="418dc-132">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="418dc-132">Click **Create**.</span></span> <span data-ttu-id="418dc-133">建立 hello 儲存體帳戶的 hello 程序可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="418dc-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="418dc-134">步驟 2: Hello 儲存體帳戶啟用 CDN</span><span class="sxs-lookup"><span data-stu-id="418dc-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="418dc-135">與 hello 最新的整合，您現在可以啟用 CDN 的儲存體帳戶而不需離開您的儲存體入口網站擴充功能。</span><span class="sxs-lookup"><span data-stu-id="418dc-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="418dc-136">選取 hello 儲存體帳戶，向搜尋"CDN 」 或捲軸從 hello 左的導覽功能表，然後按一下 「 Azure CDN 」。</span><span class="sxs-lookup"><span data-stu-id="418dc-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="418dc-137">hello **Azure CDN**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="418dc-137">hello **Azure CDN** blade appears.</span></span>

    ![CDN 啟用導覽][cdn-enable-navigation]
    
2. <span data-ttu-id="418dc-139">輸入所需的 hello 資訊建立新的端點</span><span class="sxs-lookup"><span data-stu-id="418dc-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="418dc-140">**CDN 設定檔**：您可以建立新的設定檔，或使用現有設定檔。</span><span class="sxs-lookup"><span data-stu-id="418dc-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="418dc-141">**定價層**： 您只需要的 tooselect 定價層，如果您建立新的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="418dc-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="418dc-142">**CDN 端點名稱**︰依照您的選擇輸入端點名稱。</span><span class="sxs-lookup"><span data-stu-id="418dc-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="418dc-143">依預設，hello 建立 CDN 端點會使用儲存體帳戶的 hello 主機的名稱作為來源。</span><span class="sxs-lookup"><span data-stu-id="418dc-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="418dc-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="418dc-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="418dc-145">在建立之後，hello 新端點會出現在上述的 hello 端點清單。</span><span class="sxs-lookup"><span data-stu-id="418dc-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![CDN 儲存體新端點][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="418dc-147">您也可以移 tooAzure CDN 延伸 tooenable CDN。[教學課程](#Tutorial-cdn-create-profile)。</span><span class="sxs-lookup"><span data-stu-id="418dc-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="418dc-148">步驟 3︰ 啟用其他 CDN 功能</span><span class="sxs-lookup"><span data-stu-id="418dc-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="418dc-149">從儲存體帳戶"Azure CDN 」 刀鋒視窗中，按一下 從 hello 清單 tooopen CDN 組態刀鋒視窗的 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="418dc-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="418dc-150">您可以為傳遞啟用其他的 CDN 功能，例如壓縮、查詢字串、地理篩選。</span><span class="sxs-lookup"><span data-stu-id="418dc-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="418dc-151">您也可以新增自訂網域對應 tooyour CDN 端點，並啟用 HTTPS 的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="418dc-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN 儲存體 CDN 組態][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="418dc-153">步驟 4：存取 CDN 內容</span><span class="sxs-lookup"><span data-stu-id="418dc-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="418dc-154">使用 hello CDN URL tooaccess 快取上 hello CDN 的內容，hello 入口網站中提供。</span><span class="sxs-lookup"><span data-stu-id="418dc-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="418dc-155">快取之 blob 的 hello 位址會是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="418dc-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="418dc-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="418dc-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="418dc-157">一旦您啟用 CDN 存取 tooa 儲存體帳戶時，所有公開可用物件皆適用於 CDN 邊緣快取。</span><span class="sxs-lookup"><span data-stu-id="418dc-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="418dc-158">如果您修改目前在 hello CDN 中快取的物件，直到 hello CDN 快取的 hello 內容存留時間期限到期時重新整理內容，將無法使用透過 hello CDN hello 新內容。</span><span class="sxs-lookup"><span data-stu-id="418dc-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="418dc-159">步驟 5: Hello CDN 移除內容</span><span class="sxs-lookup"><span data-stu-id="418dc-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="418dc-160">如果您不再想 toocache 物件 hello Azure 內容傳遞網路 (CDN) 中，您可以採取下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="418dc-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="418dc-161">您可以進行 hello 容器私人而非公用。</span><span class="sxs-lookup"><span data-stu-id="418dc-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="418dc-162">請參閱[管理匿名讀取權限 toocontainers 和 blob](../storage/blobs/storage-manage-access-to-resources.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="418dc-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="418dc-163">您可以停用或刪除使用 hello 管理入口網站的 hello CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="418dc-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="418dc-164">您可以修改您的託管的服務 toono 長回應 toorequests hello 物件。</span><span class="sxs-lookup"><span data-stu-id="418dc-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="418dc-165">已在 hello CDN 中快取的物件會維持快取，直到 hello hello 物件的存留時間期間過期，或直到 hello 端點都會被清除。</span><span class="sxs-lookup"><span data-stu-id="418dc-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="418dc-166">Hello 存留時間期間過期時，hello CDN 會檢查 toosee hello CDN 端點是否仍然有效，hello 物件仍可匿名存取。</span><span class="sxs-lookup"><span data-stu-id="418dc-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="418dc-167">如果不存在，然後 hello 物件將不再快取。</span><span class="sxs-lookup"><span data-stu-id="418dc-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="418dc-168">其他資源</span><span class="sxs-lookup"><span data-stu-id="418dc-168">Additional resources</span></span>
* [<span data-ttu-id="418dc-169">如何 tooMap CDN 內容 tooa 自訂網域</span><span class="sxs-lookup"><span data-stu-id="418dc-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="418dc-170">啟用自訂網域的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="418dc-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
