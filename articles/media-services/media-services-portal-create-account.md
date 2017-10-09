---
title: "aaaCreate hello Azure 入口網站的 Azure Media Services 帳戶 |Microsoft 文件"
description: "本教學課程會引導您建立 Azure Media Services 帳戶以 hello Azure 入口網站的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="a7cda-103">建立 Azure 媒體服務帳戶使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a7cda-103">Create an Azure Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7cda-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="a7cda-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="a7cda-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7cda-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="a7cda-106">REST</span><span class="sxs-lookup"><span data-stu-id="a7cda-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="a7cda-107">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="a7cda-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a7cda-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="a7cda-109">hello Azure 入口網站提供 tooquickly 建立 Azure 媒體服務 (AMS) 帳戶的方法。</span><span class="sxs-lookup"><span data-stu-id="a7cda-109">hello Azure portal provides a way tooquickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="a7cda-110">您可以使用您的帳戶 tooaccess Media Services 可讓您 toostore、 加密、 編碼、 管理和串流處理媒體內容，在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a7cda-110">You can use your account tooaccess Media Services that enable you toostore, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="a7cda-111">在您建立 Media Services 帳戶 hello 階段，您也建立相關聯的儲存體帳戶 （或使用現有） 在 hello 與 hello Media Services 帳戶的相同地理區域。</span><span class="sxs-lookup"><span data-stu-id="a7cda-111">At hello time you create a Media Services account, you also create an associated storage account (or use an existing one) in hello same geographic region as hello Media Services account.</span></span>

<span data-ttu-id="a7cda-112">本文說明常見的一些概念，並顯示 toocreate Media Services 帳戶以 hello Azure 入口網站的方式。</span><span class="sxs-lookup"><span data-stu-id="a7cda-112">This article explains some common concepts and shows how toocreate a Media Services account with hello Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="a7cda-113">概念</span><span class="sxs-lookup"><span data-stu-id="a7cda-113">Concepts</span></span>
<span data-ttu-id="a7cda-114">存取媒體服務時需要有兩個相關聯的帳戶：</span><span class="sxs-lookup"><span data-stu-id="a7cda-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="a7cda-115">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-115">A Media Services account.</span></span> <span data-ttu-id="a7cda-116">您的帳戶可讓您存取 tooa 組以雲端為基礎的媒體服務，可在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a7cda-116">Your account gives you access tooa set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="a7cda-117">媒體服務帳戶並不會儲存實際媒體內容。</span><span class="sxs-lookup"><span data-stu-id="a7cda-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="a7cda-118">而它將 hello 媒體內容和媒體處理作業相關的中繼資料儲存在您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-118">Instead it stores metadata about hello media content and media processing jobs in your account.</span></span> <span data-ttu-id="a7cda-119">在您建立 hello 帳戶 hello 階段，您可以選取可用的 Media Services 地區。</span><span class="sxs-lookup"><span data-stu-id="a7cda-119">At hello time you create hello account, you select an available Media Services region.</span></span> <span data-ttu-id="a7cda-120">您選取的 hello 區是儲存您的帳戶的 hello 中繼資料記錄的資料中心。</span><span class="sxs-lookup"><span data-stu-id="a7cda-120">hello region you select is a data center that stores hello metadata records for your account.</span></span>
  
* <span data-ttu-id="a7cda-121">一個 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-121">An Azure storage account.</span></span> <span data-ttu-id="a7cda-122">儲存體帳戶必須位於 hello 與 hello Media Services 帳戶的相同地理區域。</span><span class="sxs-lookup"><span data-stu-id="a7cda-122">Storage accounts must be located in hello same geographic region as hello Media Services account.</span></span> <span data-ttu-id="a7cda-123">當您建立 Media Services 帳戶時，您可以選擇現有的儲存體帳戶在 hello 相同的區域，或您可以建立新的儲存體帳戶中 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="a7cda-123">When you create a Media Services account, you can either choose an existing storage account in hello same region, or you can create a new storage account in hello same region.</span></span> <span data-ttu-id="a7cda-124">如果您刪除 Media Services 帳戶時，不會刪除相關的儲存體帳戶中的 hello blob。</span><span class="sxs-lookup"><span data-stu-id="a7cda-124">If you delete a Media Services account, hello blobs in your related storage account are not deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="a7cda-125">如需不同區域中 Azure 媒體服務功能可用性的資訊，請參閱[跨資料中心的 AMS 功能可用性](scenarios-and-availability.md#availability)。</span><span class="sxs-lookup"><span data-stu-id="a7cda-125">For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="a7cda-126">建立 AMS 帳戶</span><span class="sxs-lookup"><span data-stu-id="a7cda-126">Create an AMS account</span></span>
<span data-ttu-id="a7cda-127">hello 步驟，在這個主題顯示如何 toocreate AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-127">hello steps in this section show how toocreate an AMS account.</span></span>

1. <span data-ttu-id="a7cda-128">在 hello 登入[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="a7cda-128">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a7cda-129">按一下 [+新增] > [Web + 行動] > [媒體服務]。</span><span class="sxs-lookup"><span data-stu-id="a7cda-129">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![建立媒體服務](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="a7cda-131">在 [建立媒體服務帳戶]  中輸入必要的值。</span><span class="sxs-lookup"><span data-stu-id="a7cda-131">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![建立媒體服務](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="a7cda-133">在**帳戶名稱**，輸入 hello hello 新 AMS 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a7cda-133">In **Account Name**, enter hello name of hello new AMS account.</span></span> <span data-ttu-id="a7cda-134">Media Services 帳戶名稱是所有小寫字母或數字，不含空格，也 3 too24 個字元的長度。</span><span class="sxs-lookup"><span data-stu-id="a7cda-134">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 too24 characters in length.</span></span>
   2. <span data-ttu-id="a7cda-135">在訂用帳戶，請在 hello 不同 Azure 訂用帳戶具有存取權之中選取。</span><span class="sxs-lookup"><span data-stu-id="a7cda-135">In Subscription, select among hello different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="a7cda-136">在**資源群組**，選取 hello 新的或現有的資源。</span><span class="sxs-lookup"><span data-stu-id="a7cda-136">In **Resource Group**, select hello new or existing resource.</span></span>  <span data-ttu-id="a7cda-137">資源群組是共用生命週期、權限及原則的資源集合。</span><span class="sxs-lookup"><span data-stu-id="a7cda-137">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="a7cda-138">[在此](../azure-resource-manager/resource-group-overview.md#resource-groups)深入了解。</span><span class="sxs-lookup"><span data-stu-id="a7cda-138">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="a7cda-139">在**位置**，選取 hello 將會使用的 toostore hello 媒體和中繼資料記錄您的 Media Services 帳戶的地理區域。</span><span class="sxs-lookup"><span data-stu-id="a7cda-139">In **Location**,  select hello geographic region that will be used toostore hello media and metadata records for your Media Services account.</span></span> <span data-ttu-id="a7cda-140">此區域會使用的 tooprocess 並串流媒體。</span><span class="sxs-lookup"><span data-stu-id="a7cda-140">This  region will be used tooprocess and stream your media.</span></span> <span data-ttu-id="a7cda-141">只有 hello 可用媒體服務區域會出現在 [hello] 下拉式清單方塊中。</span><span class="sxs-lookup"><span data-stu-id="a7cda-141">Only hello available Media Services regions appear in hello drop-down list box.</span></span> 
   5. <span data-ttu-id="a7cda-142">在**儲存體帳戶**，Media Services 帳戶從選取的儲存體帳戶 tooprovide blob 儲存體的 hello 媒體內容。</span><span class="sxs-lookup"><span data-stu-id="a7cda-142">In **Storage Account**, select a storage account tooprovide blob storage of hello media content from your Media Services account.</span></span> <span data-ttu-id="a7cda-143">您可以在 hello 中選取現有的儲存體帳戶相同的地理區域，為您的 Media Services 帳戶，或您可以建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-143">You can select an existing storage account in hello same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="a7cda-144">新的儲存體帳戶會在 hello 相同區域。</span><span class="sxs-lookup"><span data-stu-id="a7cda-144">A new storage account is created in hello same region.</span></span> <span data-ttu-id="a7cda-145">儲存體帳戶名稱的 hello 規則 hello 相同與 Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-145">hello rules for storage account names are hello same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="a7cda-146">在 [這裡](../storage/common/storage-introduction.md)深入了解儲存體。</span><span class="sxs-lookup"><span data-stu-id="a7cda-146">Learn more about storage [here](../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="a7cda-147">選取**Pin toodashboard** toosee hello hello 帳戶部署進度。</span><span class="sxs-lookup"><span data-stu-id="a7cda-147">Select **Pin toodashboard** toosee hello progress of hello account deployment.</span></span>
4. <span data-ttu-id="a7cda-148">按一下**建立**在 hello hello 表單底部。</span><span class="sxs-lookup"><span data-stu-id="a7cda-148">Click **Create** at hello bottom of hello form.</span></span>
   
    <span data-ttu-id="a7cda-149">已成功建立 hello 帳戶之後, 載入概觀 頁面。</span><span class="sxs-lookup"><span data-stu-id="a7cda-149">Once hello account is successfully created, overview page loads.</span></span> <span data-ttu-id="a7cda-150">Hello 串流端點資料表 hello 帳戶會有預設串流端點在 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="a7cda-150">In hello streaming endpoint table hello account will have a default streaming endpoint in hello **Stopped** state.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="a7cda-151">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="a7cda-151">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a7cda-152">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="a7cda-152">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
   
## <a name="toomanage-your-ams-account"></a><span data-ttu-id="a7cda-153">toomanage AMS 帳戶</span><span class="sxs-lookup"><span data-stu-id="a7cda-153">toomanage your AMS account</span></span>

<span data-ttu-id="a7cda-154">toomanage AMS 帳戶 （例如，連接 toohello AMS API 以程式設計方式、 上傳影片、 編碼資產、 設定內容保護、 監視作業進度） 選取**設定**上 hello hello 入口網站的左側。</span><span class="sxs-lookup"><span data-stu-id="a7cda-154">toomanage your AMS account (for example, connect toohello AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="a7cda-155">從 hello**設定**，瀏覽 tooone 的 hello 可用刀鋒視窗 (例如： **API 存取**，**資產**，**作業**， **內容保護**)。</span><span class="sxs-lookup"><span data-stu-id="a7cda-155">From hello **Settings**, navigate tooone of hello available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7cda-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7cda-156">Next steps</span></span>

<span data-ttu-id="a7cda-157">您現在可以將檔案上傳到 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7cda-157">You can now upload files into your AMS account.</span></span> <span data-ttu-id="a7cda-158">如需詳細資訊，請參閱 [上傳檔案](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="a7cda-158">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="a7cda-159">如果您計劃 tooaccess AMS API 以程式設計的方式，請參閱[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a7cda-159">If you plan tooaccess AMS API programmatically, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a7cda-160">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="a7cda-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7cda-161">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a7cda-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

