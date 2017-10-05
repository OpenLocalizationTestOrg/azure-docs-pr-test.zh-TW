---
title: "整合 Azure 儲存體帳戶與 Azure CDN | Microsoft Docs"
description: "了解如何使用 Azure 內容傳遞網路 (CDN)，透過快取 Azure 儲存體中的 Blob 來傳遞高頻寬內容。"
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
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="05adf-103">整合 Azure 儲存體帳戶與 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="05adf-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="05adf-104">可以啟用 CDN，以從您的 Azure 儲存體快取內容。</span><span class="sxs-lookup"><span data-stu-id="05adf-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="05adf-105">它透過將計算執行個體 Blob 與靜態內容快取到位於美國、歐洲、亞洲、澳洲與南美洲的實體節點中，為開發人員提供一套傳遞高頻寬內容的全球解決方案。</span><span class="sxs-lookup"><span data-stu-id="05adf-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="05adf-106">步驟 1：建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="05adf-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="05adf-107">使用下列程序，為 Azure 訂用帳戶建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="05adf-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="05adf-108">有了儲存體帳戶，才能存取 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="05adf-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="05adf-109">儲存體帳戶代表最高層級的命名空間，用於存取每個 Azure 儲存體服務元件：Blob 服務、佇列服務和資料表服務。</span><span class="sxs-lookup"><span data-stu-id="05adf-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="05adf-110">如需詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="05adf-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="05adf-111">若要建立儲存體帳戶，您必須是服務管理員或是相關聯訂用帳戶的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="05adf-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="05adf-112">您可使用數種方法來建立儲存體帳戶，包括 Azure 入口網站和 Powershell。</span><span class="sxs-lookup"><span data-stu-id="05adf-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="05adf-113">針對本教學課程，我們將使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="05adf-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="05adf-114">**為 Azure 訂用帳戶建立儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="05adf-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="05adf-115">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="05adf-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05adf-116">在左下角，選取 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="05adf-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="05adf-117">在 [新增] 對話方塊中，選取 [資料 + 儲存體]，然後按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="05adf-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="05adf-118">此時會顯示 [建立儲存體帳戶]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="05adf-118">The **Create storage account** blade appears.</span></span>   

    ![建立儲存體帳戶][create-new-storage-account]  

3. <span data-ttu-id="05adf-120">在 [名稱]  欄位中，輸入子網域名稱。</span><span class="sxs-lookup"><span data-stu-id="05adf-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="05adf-121">此項目可以包含 3 至 24 個小寫字母與數字。</span><span class="sxs-lookup"><span data-stu-id="05adf-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="05adf-122">此值會成為 URI 內用來將訂用帳戶的 Blob、「佇列」或「資料表」資源定址的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="05adf-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="05adf-123">若要將 Blob 服務中的容器資源定址，您需要使用下列格式的 URI，其中 &lt;StorageAccountLabel&gt; 是指在 [輸入 URL] 中輸入的值：</span><span class="sxs-lookup"><span data-stu-id="05adf-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="05adf-124">http://&lt;StorageAcountLabel&gt;.blob.core.windows.net/&lt;mycontainer&gt;</span><span class="sxs-lookup"><span data-stu-id="05adf-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="05adf-125">**重要事項：** URL 標籤會形成儲存體帳戶 URI 的子網域，而且必須在 Azure 中的所有代管服務間是唯一的。</span><span class="sxs-lookup"><span data-stu-id="05adf-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="05adf-126">此值也用作這個儲存體帳戶在入口網站中的名稱，或用於透過程式設計方式存取此帳戶時。</span><span class="sxs-lookup"><span data-stu-id="05adf-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="05adf-127">保留 [部署模型]、[帳戶種類]、[效能] 和 [複寫] 的預設值。</span><span class="sxs-lookup"><span data-stu-id="05adf-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="05adf-128">選取將與儲存體帳戶搭配使用的 [ **訂用帳戶** ]。</span><span class="sxs-lookup"><span data-stu-id="05adf-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="05adf-129">選取或建立 **資源群組**。</span><span class="sxs-lookup"><span data-stu-id="05adf-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="05adf-130">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="05adf-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="05adf-131">選取儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="05adf-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="05adf-132">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="05adf-132">Click **Create**.</span></span> <span data-ttu-id="05adf-133">建立儲存體帳戶的程序可能需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="05adf-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="05adf-134">步驟 2︰啟用儲存體帳戶的 CDN</span><span class="sxs-lookup"><span data-stu-id="05adf-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="05adf-135">您現在可以利用最新的整合啟用儲存體帳戶的 CDN，而不需要離開儲存體入口網站延伸模組。</span><span class="sxs-lookup"><span data-stu-id="05adf-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="05adf-136">選取儲存體帳戶，搜尋 "CDN" 或從左側導覽功能表向下捲動，然後按一下 [Azure CDN]。</span><span class="sxs-lookup"><span data-stu-id="05adf-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="05adf-137">[Azure CDN] 刀鋒視窗隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="05adf-137">The **Azure CDN** blade appears.</span></span>

    ![CDN 啟用導覽][cdn-enable-navigation]
    
2. <span data-ttu-id="05adf-139">輸入所需的資訊建立新端點</span><span class="sxs-lookup"><span data-stu-id="05adf-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="05adf-140">**CDN 設定檔**：您可以建立新的設定檔，或使用現有設定檔。</span><span class="sxs-lookup"><span data-stu-id="05adf-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="05adf-141">**定價層**︰如果您建立新的 CDN 設定檔，則只需選取定價層。</span><span class="sxs-lookup"><span data-stu-id="05adf-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="05adf-142">**CDN 端點名稱**︰依照您的選擇輸入端點名稱。</span><span class="sxs-lookup"><span data-stu-id="05adf-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="05adf-143">根據預設，建立的 CDN 端點會使用儲存體帳戶的主機名稱作為來源。</span><span class="sxs-lookup"><span data-stu-id="05adf-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="05adf-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="05adf-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="05adf-145">建立之後，新的端點會出現在上面的端點清單。</span><span class="sxs-lookup"><span data-stu-id="05adf-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![CDN 儲存體新端點][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="05adf-147">您也可以移至 Azure CDN 延伸模組以啟用 CDN，[教學課程](#Tutorial-cdn-create-profile)。</span><span class="sxs-lookup"><span data-stu-id="05adf-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="05adf-148">步驟 3︰ 啟用其他 CDN 功能</span><span class="sxs-lookup"><span data-stu-id="05adf-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="05adf-149">從儲存體帳戶 [Azure CDN] 刀鋒視窗中，按一下清單中的 CDN 端點，以開啟 CDN 組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="05adf-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="05adf-150">您可以為傳遞啟用其他的 CDN 功能，例如壓縮、查詢字串、地理篩選。</span><span class="sxs-lookup"><span data-stu-id="05adf-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="05adf-151">您也可以將自訂網域對應新增至 CDN 端點，並啟用自訂網域 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="05adf-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN 儲存體 CDN 組態][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="05adf-153">步驟 4：存取 CDN 內容</span><span class="sxs-lookup"><span data-stu-id="05adf-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="05adf-154">若要存取 CDN 上快取的內容，請使用入口網站中提供的 CDN URL。</span><span class="sxs-lookup"><span data-stu-id="05adf-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="05adf-155">所快取 Blob 的位址將類似如下：</span><span class="sxs-lookup"><span data-stu-id="05adf-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="05adf-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="05adf-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="05adf-157">啟用 CDN 存取儲存體帳戶後，所有公開可用的物件皆適用於 CDN 邊緣快取。</span><span class="sxs-lookup"><span data-stu-id="05adf-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="05adf-158">如果您修改的物件目前是 CDN 中的快取物件，在快取內容的有效存留期已滿，且 CDN 重新整理內容之前，都無法透過 CDN 取得新的內容。</span><span class="sxs-lookup"><span data-stu-id="05adf-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="05adf-159">步驟 5：從 CDN 移除內容</span><span class="sxs-lookup"><span data-stu-id="05adf-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="05adf-160">如果不想要將內容快取到 Azure 內容傳遞網路 (CDN) 中，您可以採取下列其中一個步驟：</span><span class="sxs-lookup"><span data-stu-id="05adf-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="05adf-161">您可以將容器設為私人而非公用。</span><span class="sxs-lookup"><span data-stu-id="05adf-161">You can make the container private instead of public.</span></span> <span data-ttu-id="05adf-162">如需詳細資訊，請參閱 [管理對容器和 Blob 的匿名讀取權限](../storage/blobs/storage-manage-access-to-resources.md) 。</span><span class="sxs-lookup"><span data-stu-id="05adf-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="05adf-163">您可以使用管理入口網站來停用或刪除 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="05adf-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="05adf-164">您可以修改託管服務，使其不再回應物件的要求。</span><span class="sxs-lookup"><span data-stu-id="05adf-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="05adf-165">已在 CDN 中快取的物件會保持快取狀態，直到物件的有效存留期已過或端點已清除為止。</span><span class="sxs-lookup"><span data-stu-id="05adf-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="05adf-166">有效存留期間已滿時，CDN 將查看 CDN 端點是否仍然有效，以及物件是否仍可匿名存取。</span><span class="sxs-lookup"><span data-stu-id="05adf-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="05adf-167">如果不是的話，將不再快取物件。</span><span class="sxs-lookup"><span data-stu-id="05adf-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05adf-168">其他資源</span><span class="sxs-lookup"><span data-stu-id="05adf-168">Additional resources</span></span>
* [<span data-ttu-id="05adf-169">如何將 CDN 內容對應至自訂網域</span><span class="sxs-lookup"><span data-stu-id="05adf-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="05adf-170">啟用自訂網域的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="05adf-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
