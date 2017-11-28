---
title: "使用 Azure 入口網站建立 Azure 媒體服務帳戶 | Microsoft Docs"
description: "本教學課程逐步引導您完成使用 Azure 入口網站建立 Azure 媒體服務帳戶的步驟。"
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
ms.openlocfilehash: 919a0b2f390bab353d24423d7f216e7031581aba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-media-services-account-using-the-azure-portal"></a><span data-ttu-id="94e10-103">使用 Azure 入口網站建立 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="94e10-103">Create an Azure Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94e10-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="94e10-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="94e10-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94e10-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="94e10-106">REST</span><span class="sxs-lookup"><span data-stu-id="94e10-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="94e10-107">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="94e10-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="94e10-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="94e10-109">Azure 入口網站提供一種方法來快速建立 Azure 媒體服務 (AMS) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-109">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="94e10-110">您可以使用自己的帳戶，來存取讓您在 Azure 中儲存、加密、編碼、管理和串流播放媒體內容的媒體服務。</span><span class="sxs-lookup"><span data-stu-id="94e10-110">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="94e10-111">當您建立媒體服務帳戶時，您也會在與媒體服務帳戶相同的地理區域中建立相關聯的儲存體帳戶 (或使用現有儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="94e10-111">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span></span>

<span data-ttu-id="94e10-112">本文說明一些常見的概念，並示範如何使用 Azure 入口網站建立媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-112">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="94e10-113">概念</span><span class="sxs-lookup"><span data-stu-id="94e10-113">Concepts</span></span>
<span data-ttu-id="94e10-114">存取媒體服務時需要有兩個相關聯的帳戶：</span><span class="sxs-lookup"><span data-stu-id="94e10-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="94e10-115">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-115">A Media Services account.</span></span> <span data-ttu-id="94e10-116">您的帳戶可讓您存取 Azure 中提供的一組雲端型媒體服務。</span><span class="sxs-lookup"><span data-stu-id="94e10-116">Your account gives you access to a set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="94e10-117">媒體服務帳戶並不會儲存實際媒體內容。</span><span class="sxs-lookup"><span data-stu-id="94e10-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="94e10-118">而是在您的帳戶中儲存媒體內容和媒體處理工作的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="94e10-118">Instead it stores metadata about the media content and media processing jobs in your account.</span></span> <span data-ttu-id="94e10-119">當您建立帳戶時，您會選取一個可用的媒體服務區域。</span><span class="sxs-lookup"><span data-stu-id="94e10-119">At the time you create the account, you select an available Media Services region.</span></span> <span data-ttu-id="94e10-120">所選取的區域會是儲存您帳戶之中繼資料記錄的資料中心。</span><span class="sxs-lookup"><span data-stu-id="94e10-120">The region you select is a data center that stores the metadata records for your account.</span></span>
  
* <span data-ttu-id="94e10-121">一個 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-121">An Azure storage account.</span></span> <span data-ttu-id="94e10-122">儲存體帳戶必須與媒體服務帳戶位於相同的地理區域中。</span><span class="sxs-lookup"><span data-stu-id="94e10-122">Storage accounts must be located in the same geographic region as the Media Services account.</span></span> <span data-ttu-id="94e10-123">建立媒體服務帳戶時，可以選擇相同區域中的現有儲存體帳戶，也可以在相同區域中建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-123">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span></span> <span data-ttu-id="94e10-124">如果您刪除媒體服務帳戶，並不會刪除相關儲存體帳戶中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="94e10-124">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="94e10-125">如需不同區域中 Azure 媒體服務功能可用性的資訊，請參閱[跨資料中心的 AMS 功能可用性](scenarios-and-availability.md#availability)。</span><span class="sxs-lookup"><span data-stu-id="94e10-125">For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="94e10-126">建立 AMS 帳戶</span><span class="sxs-lookup"><span data-stu-id="94e10-126">Create an AMS account</span></span>
<span data-ttu-id="94e10-127">本節中的步驟示範如何建立 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-127">The steps in this section show how to create an AMS account.</span></span>

1. <span data-ttu-id="94e10-128">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="94e10-128">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="94e10-129">按一下 [+新增] > [Web + 行動] > [媒體服務]。</span><span class="sxs-lookup"><span data-stu-id="94e10-129">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![建立媒體服務](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="94e10-131">在 [建立媒體服務帳戶]  中輸入必要的值。</span><span class="sxs-lookup"><span data-stu-id="94e10-131">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![建立媒體服務](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="94e10-133">在 [帳戶名稱] 中，輸入新 AMS 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="94e10-133">In **Account Name**, enter the name of the new AMS account.</span></span> <span data-ttu-id="94e10-134">媒體服務帳戶名稱為全部小寫且不含空格的字母或數字，且長度是 3 到 24 個字元。</span><span class="sxs-lookup"><span data-stu-id="94e10-134">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span></span>
   2. <span data-ttu-id="94e10-135">在訂用帳戶中，從您可存取的不同 Azure 訂用帳戶中進行選取。</span><span class="sxs-lookup"><span data-stu-id="94e10-135">In Subscription, select among the different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="94e10-136">在 [資源群組] 中，選取新的或現有資源。</span><span class="sxs-lookup"><span data-stu-id="94e10-136">In **Resource Group**, select the new or existing resource.</span></span>  <span data-ttu-id="94e10-137">資源群組是共用生命週期、權限及原則的資源集合。</span><span class="sxs-lookup"><span data-stu-id="94e10-137">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="94e10-138">[在此](../azure-resource-manager/resource-group-overview.md#resource-groups)深入了解。</span><span class="sxs-lookup"><span data-stu-id="94e10-138">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="94e10-139">在 [位置] 中，選取您將用來為媒體服務帳戶儲存媒體和中繼資料記錄的地理區域。</span><span class="sxs-lookup"><span data-stu-id="94e10-139">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span></span> <span data-ttu-id="94e10-140">此區域將用於處理和串流媒體。</span><span class="sxs-lookup"><span data-stu-id="94e10-140">This  region will be used to process and stream your media.</span></span> <span data-ttu-id="94e10-141">只有可用的媒體服務區域才會出現在下拉式清單方塊中。</span><span class="sxs-lookup"><span data-stu-id="94e10-141">Only the available Media Services regions appear in the drop-down list box.</span></span> 
   5. <span data-ttu-id="94e10-142">在 [儲存體帳戶] 中，選取儲存體帳戶以從媒體服務帳戶提供媒體內容的 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94e10-142">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span></span> <span data-ttu-id="94e10-143">您可以選取與媒體服務帳戶相同地理區域中的現有儲存體帳戶，也可以建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-143">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="94e10-144">新的儲存體帳戶會建立於相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="94e10-144">A new storage account is created in the same region.</span></span> <span data-ttu-id="94e10-145">儲存體帳戶名稱的規則會與媒體服務帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="94e10-145">The rules for storage account names are the same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="94e10-146">在 [這裡](../storage/common/storage-introduction.md)深入了解儲存體。</span><span class="sxs-lookup"><span data-stu-id="94e10-146">Learn more about storage [here](../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="94e10-147">選取 **[釘選到儀表板]**  以查看帳戶部署的進度。</span><span class="sxs-lookup"><span data-stu-id="94e10-147">Select **Pin to dashboard** to see the progress of the account deployment.</span></span>
4. <span data-ttu-id="94e10-148">按一下表單底部的 [建立]  。</span><span class="sxs-lookup"><span data-stu-id="94e10-148">Click **Create** at the bottom of the form.</span></span>
   
    <span data-ttu-id="94e10-149">成功建立帳戶後，隨即載入概觀頁面。</span><span class="sxs-lookup"><span data-stu-id="94e10-149">Once the account is successfully created, overview page loads.</span></span> <span data-ttu-id="94e10-150">在串流端點資料表中，此帳戶將具有 [已停止] 狀態的預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="94e10-150">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="94e10-151">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-151">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="94e10-152">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="94e10-152">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
   
## <a name="to-manage-your-ams-account"></a><span data-ttu-id="94e10-153">管理 AMS 帳戶</span><span class="sxs-lookup"><span data-stu-id="94e10-153">To manage your AMS account</span></span>

<span data-ttu-id="94e10-154">若要管理 AMS 帳戶 (例如，以程式設計方式連線至 AMS API、上傳影片、編碼資產、設定內容保護、監視作業進度)，請選取入口網站左側的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="94e10-154">To manage your AMS account (for example, connect to the AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on the left side of the portal.</span></span> <span data-ttu-id="94e10-155">從 [設定] 中，導覽至其中一個可用的刀鋒視窗 (例如：[API 存取]、[資產]、[作業]、[內容保護])。</span><span class="sxs-lookup"><span data-stu-id="94e10-155">From the **Settings**, navigate to one of the available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="94e10-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94e10-156">Next steps</span></span>

<span data-ttu-id="94e10-157">您現在可以將檔案上傳到 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94e10-157">You can now upload files into your AMS account.</span></span> <span data-ttu-id="94e10-158">如需詳細資訊，請參閱 [上傳檔案](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="94e10-158">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="94e10-159">如果您要以程式設計方式存取 AMS API，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="94e10-159">If you plan to access AMS API programmatically, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="94e10-160">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="94e10-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="94e10-161">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="94e10-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

