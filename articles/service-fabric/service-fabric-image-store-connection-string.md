---
title: "aaaAzure Service Fabric 映像存放區連接字串 |Microsoft 文件"
description: "了解 hello 映像存放區連接字串"
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
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a><span data-ttu-id="868b4-103">了解 hello ImageStoreConnectionString 設定</span><span class="sxs-lookup"><span data-stu-id="868b4-103">Understand hello ImageStoreConnectionString setting</span></span>

<span data-ttu-id="868b4-104">在某些文件，我們簡短提到 hello"ImageStoreConnectionString"參數存在而不描述它其實是表示。</span><span class="sxs-lookup"><span data-stu-id="868b4-104">In some of our documentation, we briefly mention hello existence of an "ImageStoreConnectionString" parameter without describing what it really means.</span></span> <span data-ttu-id="868b4-105">及之後的發行項，例如透過[使用 PowerShell 部署和移除應用程式][10]，它看起來像是您是複製/貼上 hello 值出現在 hello 叢集資訊清單中的 hello 目標叢集。</span><span class="sxs-lookup"><span data-stu-id="868b4-105">And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste hello value as it appears in hello cluster manifest of hello target cluster.</span></span> <span data-ttu-id="868b4-106">因此 hello 設定必須是可設定每個叢集，但是當您透過建立叢集 hello [Azure 入口網站][11]，沒有任何選項 tooconfigure 此設定，和它的一律"fabric: ImageStore"。</span><span class="sxs-lookup"><span data-stu-id="868b4-106">So hello setting must be configurable per cluster, but when you create a cluster through hello [Azure portal][11], there's no option tooconfigure this setting and it's always "fabric:ImageStore".</span></span> <span data-ttu-id="868b4-107">這項設定將 hello 用途為何？</span><span class="sxs-lookup"><span data-stu-id="868b4-107">What's hello purpose of this setting then?</span></span>

![叢集資訊清單][img_cm]

<span data-ttu-id="868b4-109">Service Fabric 開始內部 Microsoft 耗用量的平台由許多不同的小組，所以它的某些方面會高度可自訂-hello 「 映像存放區 」 是一個這類的層面。</span><span class="sxs-lookup"><span data-stu-id="868b4-109">Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - hello "Image Store" is one such aspect.</span></span> <span data-ttu-id="868b4-110">基本上，hello 映像存放區是隨插即用的儲存機制來儲存應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="868b4-110">Essentially, hello Image Store is a pluggable repository for storing application packages.</span></span> <span data-ttu-id="868b4-111">當您的應用程式部署的 tooa hello 叢集中的節點，該節點會從 hello 映像存放區下載 hello 的應用程式套件的內容。</span><span class="sxs-lookup"><span data-stu-id="868b4-111">When your application is deployed tooa node in hello cluster, that node downloads hello contents of your application package from hello Image Store.</span></span> <span data-ttu-id="868b4-112">hello ImageStoreConnectionString 是包含的用戶端和節點 toofind hello 正確映像存放區指定叢集中的 hello 必要資訊的設定。</span><span class="sxs-lookup"><span data-stu-id="868b4-112">hello ImageStoreConnectionString is a setting that includes all hello necessary information for both clients and nodes toofind hello correct Image Store for a given cluster.</span></span>

<span data-ttu-id="868b4-113">目前有三種可能的映像存放區提供者，其對應的連接字串如下︰</span><span class="sxs-lookup"><span data-stu-id="868b4-113">There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:</span></span>

1. <span data-ttu-id="868b4-114">映像存放服務："fabric:ImageStore"</span><span class="sxs-lookup"><span data-stu-id="868b4-114">Image Store Service: "fabric:ImageStore"</span></span>

2. <span data-ttu-id="868b4-115">檔案系統："file:[file system path]"</span><span class="sxs-lookup"><span data-stu-id="868b4-115">File System: "file:[file system path]"</span></span>

3. <span data-ttu-id="868b4-116">Azure 儲存體："xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span><span class="sxs-lookup"><span data-stu-id="868b4-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span></span>

<span data-ttu-id="868b4-117">用於生產環境的 hello 提供者類型為 hello 映像存放區的服務，這是可設定狀態的持續性的系統服務，您可以看到從 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="868b4-117">hello provider type used in production is hello Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer.</span></span> 

![映像存放服務][img_is]

<span data-ttu-id="868b4-119">裝載 hello 映像存放區本身 hello 叢集內的系統服務中排除 hello 封裝儲存機制的外部相依性，並讓我們更充分掌控 hello 位置的儲存體。</span><span class="sxs-lookup"><span data-stu-id="868b4-119">Hosting hello Image Store in a system service within hello cluster itself eliminates external dependencies for hello package repository and gives us more control over hello locality of storage.</span></span> <span data-ttu-id="868b4-120">首先，如果不是以獨佔方式時，未來的改良周圍 hello 映像存放區將會可能 tootarget hello 映像存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="868b4-120">Future improvements around hello Image Store are likely tootarget hello Image Store provider first, if not exclusively.</span></span> <span data-ttu-id="868b4-121">hello hello 映像存放區的服務提供者的連接字串不會有任何唯一資訊，因為 hello 用戶端已連線的 toohello 目標叢集。</span><span class="sxs-lookup"><span data-stu-id="868b4-121">hello connection string for hello Image Store Service provider doesn't have any unique information since hello client is already connected toohello target cluster.</span></span> <span data-ttu-id="868b4-122">hello 用戶端只需要 tooknow，應該使用目標 hello 系統服務的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="868b4-122">hello client only needs tooknow that protocols targeting hello system service should be used.</span></span>

<span data-ttu-id="868b4-123">hello 檔案系統提供者而 hello 映像存放區服務不是本機的其中一個方塊叢集期間用於開發 toobootstrap hello 叢集稍微更快。</span><span class="sxs-lookup"><span data-stu-id="868b4-123">hello File System provider is used instead of hello Image Store Service for local one-box clusters during development toobootstrap hello cluster slightly faster.</span></span> <span data-ttu-id="868b4-124">hello 差異是通常很小，但在開發期間大部分人的有用的最佳化。</span><span class="sxs-lookup"><span data-stu-id="868b4-124">hello difference is typically small, but it's a useful optimization for most folks during development.</span></span> <span data-ttu-id="868b4-125">它的可能 toodeploy 本機一個方塊叢集 hello 其他存放裝置提供者類型，但通常沒有理由 toodo 因此因為 hello 開發/測試工作流程仍然維持 hello 相同不論提供者。</span><span class="sxs-lookup"><span data-stu-id="868b4-125">It's possible toodeploy a local one-box cluster with hello other storage provider types as well, but there's usually no reason toodo so since hello develop/test workflow remains hello same regardless of provider.</span></span> <span data-ttu-id="868b4-126">這項用法以外 hello 檔案系統和 Azure 儲存體提供者只存在於舊版支援。</span><span class="sxs-lookup"><span data-stu-id="868b4-126">Other than this usage, hello File System and Azure Storage providers only exist for legacy support.</span></span>

<span data-ttu-id="868b4-127">因此 hello ImageStoreConnectionString 可設定時，您通常只使用 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="868b4-127">So while hello ImageStoreConnectionString is configurable, you generally just use hello default setting.</span></span> <span data-ttu-id="868b4-128">當發行 tooAzure 透過[Visual Studio][12]，hello 參數會自動設定為您據以。</span><span class="sxs-lookup"><span data-stu-id="868b4-128">When publishing tooAzure through [Visual Studio][12], hello parameter is automatically set for you accordingly.</span></span> <span data-ttu-id="868b4-129">對於裝載於 Azure 中以程式設計方式部署 tooclusters，hello 連接字串一律是"fabric: ImageStore"。</span><span class="sxs-lookup"><span data-stu-id="868b4-129">For programmatic deployment tooclusters hosted in Azure, hello connection string is always "fabric:ImageStore".</span></span> <span data-ttu-id="868b4-130">雖然有疑問，其值永遠可由驗證擷取 hello 叢集資訊清單所[PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest)， [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx)，或[REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest)。</span><span class="sxs-lookup"><span data-stu-id="868b4-130">Though when in doubt, its value can always be verified by retrieving hello cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest).</span></span> <span data-ttu-id="868b4-131">這兩個內部部署測試和實際執行叢集應該設定的 toouse hello 映像存放區的服務提供者以及。</span><span class="sxs-lookup"><span data-stu-id="868b4-131">Both on-premises test and production clusters should always be configured toouse hello Image Store Service provider as well.</span></span>

### <a name="next-steps"></a><span data-ttu-id="868b4-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="868b4-132">Next steps</span></span>
<span data-ttu-id="868b4-133">[使用 PowerShell 部署與移除應用程式][10]</span><span class="sxs-lookup"><span data-stu-id="868b4-133">[Deploy and remove applications using PowerShell][10]</span></span>

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
