---
title: "Azure Service Fabric 映像存放區連接字串 | Microsoft Docs"
description: "了解映像存放區連接字串"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: f497006a8ba48da0032b82113702d8014952ca20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="understand-the-imagestoreconnectionstring-setting"></a><span data-ttu-id="eb601-103">了解 ImageStoreConnectionString 設定</span><span class="sxs-lookup"><span data-stu-id="eb601-103">Understand the ImageStoreConnectionString setting</span></span>

<span data-ttu-id="eb601-104">在某些文件中，我們簡單介紹 "ImageStoreConnectionString" 參數存在而不描述它真正的意義。</span><span class="sxs-lookup"><span data-stu-id="eb601-104">In some of our documentation, we briefly mention the existence of an "ImageStoreConnectionString" parameter without describing what it really means.</span></span> <span data-ttu-id="eb601-105">在瀏覽過[使用 PowerShell 部署和移除應用程式][10]類似的文章後，看起來您所要做的是如出現在目標叢集的叢集資訊清單中的值，將它是複製/貼上。</span><span class="sxs-lookup"><span data-stu-id="eb601-105">And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste the value as it appears in the cluster manifest of the target cluster.</span></span> <span data-ttu-id="eb601-106">所以每個叢集的設定必須是可設定，但當您透過 [Azure 入口網站][11]建立叢集時，沒有設定此設定的選項，而一律是 "fabric:ImageStore"。</span><span class="sxs-lookup"><span data-stu-id="eb601-106">So the setting must be configurable per cluster, but when you create a cluster through the [Azure portal][11], there's no option to configure this setting and it's always "fabric:ImageStore".</span></span> <span data-ttu-id="eb601-107">那麼這項設定的目的是什麼？</span><span class="sxs-lookup"><span data-stu-id="eb601-107">What's the purpose of this setting then?</span></span>

![叢集資訊清單][img_cm]

<span data-ttu-id="eb601-109">Service Fabric 由許多不同的小組以內部 Microsoft 耗用量的平台開始，所以其某些層面可以靈活自訂 -「映像存放區」就是這類項目。</span><span class="sxs-lookup"><span data-stu-id="eb601-109">Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - the "Image Store" is one such aspect.</span></span> <span data-ttu-id="eb601-110">基本上，映像存放區是可儲存應用程式封裝隨的插即用儲存機制。</span><span class="sxs-lookup"><span data-stu-id="eb601-110">Essentially, the Image Store is a pluggable repository for storing application packages.</span></span> <span data-ttu-id="eb601-111">當您的應用程式部署到叢集中的節點時，該節點會從映像存放區下載應用程式封裝的內容。</span><span class="sxs-lookup"><span data-stu-id="eb601-111">When your application is deployed to a node in the cluster, that node downloads the contents of your application package from the Image Store.</span></span> <span data-ttu-id="eb601-112">ImageStoreConnectionString 是包含所有用戶端與節點之必要資訊的設定，供指定叢集找到正確的映像存放區。</span><span class="sxs-lookup"><span data-stu-id="eb601-112">The ImageStoreConnectionString is a setting that includes all the necessary information for both clients and nodes to find the correct Image Store for a given cluster.</span></span>

<span data-ttu-id="eb601-113">目前有三種可能的映像存放區提供者，其對應的連接字串如下︰</span><span class="sxs-lookup"><span data-stu-id="eb601-113">There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:</span></span>

1. <span data-ttu-id="eb601-114">映像存放服務："fabric:ImageStore"</span><span class="sxs-lookup"><span data-stu-id="eb601-114">Image Store Service: "fabric:ImageStore"</span></span>

2. <span data-ttu-id="eb601-115">檔案系統："file:[file system path]"</span><span class="sxs-lookup"><span data-stu-id="eb601-115">File System: "file:[file system path]"</span></span>

3. <span data-ttu-id="eb601-116">Azure 儲存體："xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span><span class="sxs-lookup"><span data-stu-id="eb601-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span></span>

<span data-ttu-id="eb601-117">生產環境中使用的提供者類型是映像存放服務，這是您可以從 Service Fabric Explorer 看到的可設定狀態持續性系統服務。</span><span class="sxs-lookup"><span data-stu-id="eb601-117">The provider type used in production is the Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer.</span></span> 

![映像存放服務][img_is]

<span data-ttu-id="eb601-119">在叢集本身的系統服務中裝載映像存放可排除封裝儲存機制的外部相依性，並讓我們更充分掌控儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="eb601-119">Hosting the Image Store in a system service within the cluster itself eliminates external dependencies for the package repository and gives us more control over the locality of storage.</span></span> <span data-ttu-id="eb601-120">有關映像存放的未來增強功能應該會先將目標放在映像存放區提供者 (如果不是專用)。</span><span class="sxs-lookup"><span data-stu-id="eb601-120">Future improvements around the Image Store are likely to target the Image Store provider first, if not exclusively.</span></span> <span data-ttu-id="eb601-121">映像存放區服務提供者的連接字串沒有任何唯一的資訊，因為用戶端已連接至目標叢集。</span><span class="sxs-lookup"><span data-stu-id="eb601-121">The connection string for the Image Store Service provider doesn't have any unique information since the client is already connected to the target cluster.</span></span> <span data-ttu-id="eb601-122">用戶端只需要知道，應該使用目標為系統服務的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="eb601-122">The client only needs to know that protocols targeting the system service should be used.</span></span>

<span data-ttu-id="eb601-123">在開發期間會針對本機一整體叢集使用檔案系統提供者而非映像存放區服務，以稍微加速啟動叢集。</span><span class="sxs-lookup"><span data-stu-id="eb601-123">The File System provider is used instead of the Image Store Service for local one-box clusters during development to bootstrap the cluster slightly faster.</span></span> <span data-ttu-id="eb601-124">差別通常很小，但它在開發期間對於大部分人是有用的最佳化。</span><span class="sxs-lookup"><span data-stu-id="eb601-124">The difference is typically small, but it's a useful optimization for most folks during development.</span></span> <span data-ttu-id="eb601-125">可以使用其他存放裝置提供者類型部署本機一整體叢集，但通常沒有理由這麼做，因為開發/測試工作流程將保持不變，不論提供者為何。</span><span class="sxs-lookup"><span data-stu-id="eb601-125">It's possible to deploy a local one-box cluster with the other storage provider types as well, but there's usually no reason to do so since the develop/test workflow remains the same regardless of provider.</span></span> <span data-ttu-id="eb601-126">除了這項用法以外，檔案系統和 Azure 儲存體提供者只存在於舊版支援。</span><span class="sxs-lookup"><span data-stu-id="eb601-126">Other than this usage, the File System and Azure Storage providers only exist for legacy support.</span></span>

<span data-ttu-id="eb601-127">因此，當 ImageStoreConnectionString 可設定時，您通常只使用預設設定。</span><span class="sxs-lookup"><span data-stu-id="eb601-127">So while the ImageStoreConnectionString is configurable, you generally just use the default setting.</span></span> <span data-ttu-id="eb601-128">透過 [Visual Studio][12] 發佈至 Azure 時，參數會據以自動為您設定。</span><span class="sxs-lookup"><span data-stu-id="eb601-128">When publishing to Azure through [Visual Studio][12], the parameter is automatically set for you accordingly.</span></span> <span data-ttu-id="eb601-129">針對以程式設計方式部署至 Azure 中裝載的叢集，連接字串一律是 "fabric:ImageStore"。</span><span class="sxs-lookup"><span data-stu-id="eb601-129">For programmatic deployment to clusters hosted in Azure, the connection string is always "fabric:ImageStore".</span></span> <span data-ttu-id="eb601-130">但是當有疑問時，其值一律能夠藉由 [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest)[.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx) 或 [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest) 擷取叢集資訊清單來驗證。</span><span class="sxs-lookup"><span data-stu-id="eb601-130">Though when in doubt, its value can always be verified by retrieving the cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest).</span></span> <span data-ttu-id="eb601-131">內部部署測試與生產叢集也應該一律設定為使用映像存放區服務提供者。</span><span class="sxs-lookup"><span data-stu-id="eb601-131">Both on-premises test and production clusters should always be configured to use the Image Store Service provider as well.</span></span>

### <a name="next-steps"></a><span data-ttu-id="eb601-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb601-132">Next steps</span></span>
<span data-ttu-id="eb601-133">[使用 PowerShell 部署與移除應用程式][10]</span><span class="sxs-lookup"><span data-stu-id="eb601-133">[Deploy and remove applications using PowerShell][10]</span></span>

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
