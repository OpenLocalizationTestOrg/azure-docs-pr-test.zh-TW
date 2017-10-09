---
title: "Azure 媒體服務帳戶使用 Aspera aaaUpload 檔案 |Microsoft 文件"
description: "本教學課程會引導您完成 hello 步驟將檔案上傳至儲存體帳戶使用 hello Media Services 帳戶有關聯的 * * Aspera 伺服器上指定 * * Azure 上的服務。"
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="86c69-103">將檔案上傳到 Media Services 帳戶在 Azure 上使用 hello 隨選 Aspera 伺服器服務</span><span class="sxs-lookup"><span data-stu-id="86c69-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="86c69-104">概觀</span><span class="sxs-lookup"><span data-stu-id="86c69-104">Overview</span></span>

<span data-ttu-id="86c69-105">**Aspera** 是高速檔案傳輸軟體。</span><span class="sxs-lookup"><span data-stu-id="86c69-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="86c69-106">適用於 Azure 的 **Aspera Server On Demand** 可讓大型檔案直接高速上傳和下載到 Azure Blob 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="86c69-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="86c69-107">如需有關資訊**Aspera 隨選**，請參閱 hello [Aspera 雲端](http://cloud.asperasoft.com/)站台。</span><span class="sxs-lookup"><span data-stu-id="86c69-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="86c69-108">**隨選 Aspera 伺服器**Azure 是可以從 hello 購買[Azure marketplace](https://azure.microsoft.com/en-us/marketplace/)。</span><span class="sxs-lookup"><span data-stu-id="86c69-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="86c69-109">在順序 toocomplete 購買**隨選 Aspera 伺服器**azure，請登入 Azure Marketplace 與您的 Windows Live id。</span><span class="sxs-lookup"><span data-stu-id="86c69-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="86c69-110">本教學課程會引導您完成 hello 步驟將檔案上傳至儲存體帳戶與使用 hello Media Services 帳戶相關聯之**隨選 Aspera 伺服器**Azure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="86c69-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="86c69-111">您可以找到範例顯示如何 toouse Azure 函式與 Aspera 以及 Media Services[這裡](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest)。</span><span class="sxs-lookup"><span data-stu-id="86c69-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="86c69-112">沒有與 Azure Media Services 處理媒體處理器 (Mp) 支援的限制 toohello 最大檔案大小。</span><span class="sxs-lookup"><span data-stu-id="86c69-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="86c69-113">請參閱[這](media-services-quotas-and-limitations.md)hello 檔案大小限制的詳細主題。</span><span class="sxs-lookup"><span data-stu-id="86c69-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="86c69-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="86c69-114">Prerequisites</span></span> 

<span data-ttu-id="86c69-115">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="86c69-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="86c69-116">Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="86c69-116">A Windows Live ID</span></span>
* <span data-ttu-id="86c69-117">[Azure 帳戶](https://azure.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="86c69-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="86c69-118">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="86c69-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="86c69-119">[Azure 媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="86c69-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="86c69-120">購買適用於 Azure 的 Aspera On Demand</span><span class="sxs-lookup"><span data-stu-id="86c69-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="86c69-121">一旦您登入 Azure Marketplace，遵循這些基本步驟 toocomplete Aspera 隨選 azure 的購買。</span><span class="sxs-lookup"><span data-stu-id="86c69-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="86c69-122">搜尋 Aspera，並選取「Server On Demand」。</span><span class="sxs-lookup"><span data-stu-id="86c69-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="86c69-124">檢閱 hello 訂用帳戶的計劃，然後按一下 登入 '</span><span class="sxs-lookup"><span data-stu-id="86c69-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="86c69-126">填寫 hello 規格需要訂用帳戶上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="86c69-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="86c69-128">按一下 hello**定價層**hello sub 面板中選取您想要每月的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="86c69-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="86c69-129">在 hello**計劃的詳細資料**面板中，選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="86c69-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="86c69-130">然後，在 hello**選擇定價層**] 面板中，按一下 [**選取**。</span><span class="sxs-lookup"><span data-stu-id="86c69-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="86c69-132">按一下**法律條款**tooview 並接受 hello sub 面板中的 hello 法律條款。</span><span class="sxs-lookup"><span data-stu-id="86c69-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="86c69-133">一旦您已檢閱 hello 法律條款，按一下 **購買**。</span><span class="sxs-lookup"><span data-stu-id="86c69-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="86c69-135">按一下完成 hello 購買**建立**。</span><span class="sxs-lookup"><span data-stu-id="86c69-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="86c69-137">hello Azure 儀表板會宣布，它會佈建 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="86c69-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="86c69-138">它使用佈建完成後，您可以透過搜尋 hello hello 服務名稱的資源中尋找 hello 新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="86c69-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="86c69-139">一旦找到 hello 服務，在其上按兩下 toolaunch hello 服務管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="86c69-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="86c69-141">啟動 hello Aspera 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="86c69-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="86c69-142">一旦找到新 Aspera 服務，您可以獲得存取 toohello 管理入口網站中，按一下 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="86c69-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="86c69-143">新的面板就會啟動。</span><span class="sxs-lookup"><span data-stu-id="86c69-143">A new panel will be launched.</span></span> <span data-ttu-id="86c69-144">從內該新面板中，您需要在 hello tooclick**資源名稱**的新服務。</span><span class="sxs-lookup"><span data-stu-id="86c69-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="86c69-145">在下列螢幕擷取畫面的 hello，hello 資源名稱會是 'AsperaTransferDemo'。</span><span class="sxs-lookup"><span data-stu-id="86c69-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="86c69-146">一旦您按一下 hello 資源名稱，就會啟動另一個面板。</span><span class="sxs-lookup"><span data-stu-id="86c69-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="86c69-147">在該新推出的面板中，您會看到 [管理] 連結。</span><span class="sxs-lookup"><span data-stu-id="86c69-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="86c69-148">按一下 [管理] 5d 連結 toolaunch hello Aspera 管理入口網站上 hello。</span><span class="sxs-lookup"><span data-stu-id="86c69-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="86c69-150">Hello 上的 管理連結上，您會得到 toohello 註冊頁面上，都需要 tooaccess hello 服務。</span><span class="sxs-lookup"><span data-stu-id="86c69-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="86c69-152">此時，您應該有存取 toohello Aspera 服務管理入口網站中，其中建立便捷鍵，請下載 Aspera 用戶端和授權、 檢視使用量並了解 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="86c69-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="86c69-153">hello 下列螢幕擷取畫面顯示 hello 存取建立。</span><span class="sxs-lookup"><span data-stu-id="86c69-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="86c69-155">hello 下列螢幕擷取畫面顯示 hello 使用方式報告 hello 入口網站中的介面。</span><span class="sxs-lookup"><span data-stu-id="86c69-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="86c69-157">透過 Aspera 上傳檔案</span><span class="sxs-lookup"><span data-stu-id="86c69-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="86c69-158">下載並安裝 hello Aspera 用戶端軟體：</span><span class="sxs-lookup"><span data-stu-id="86c69-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="86c69-159">瀏覽器外掛程式</span><span class="sxs-lookup"><span data-stu-id="86c69-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="86c69-160">豐富型用戶端</span><span class="sxs-lookup"><span data-stu-id="86c69-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="86c69-161">進行第一次傳送。</span><span class="sxs-lookup"><span data-stu-id="86c69-161">Make your first transfer.</span></span> <span data-ttu-id="86c69-162">在訂單 toouse hello Aspera 用戶端 tootransfer 以 hello Aspera 傳輸服務，您會需要 toocomplete hello 下列：</span><span class="sxs-lookup"><span data-stu-id="86c69-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="86c69-163">建立使用 hello Aspera 入口網站的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="86c69-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="86c69-164">下載、 安裝和授權 hello Aspera 用戶端 （hello Aspera 入口網站中可以找到軟體）。</span><span class="sxs-lookup"><span data-stu-id="86c69-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="86c69-165">請閱讀 hello Aspera 用戶端指南以取得組態資訊。</span><span class="sxs-lookup"><span data-stu-id="86c69-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="86c69-166">擷取儲存體帳戶使用 hello Azure Media 帳戶有關聯的某些資訊[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="86c69-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="86c69-167">具體而言，名稱和金鑰，以及 hello 儲存體 blob 容器名稱中 toowhich 想 tooplace 您的內容。</span><span class="sxs-lookup"><span data-stu-id="86c69-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="86c69-168">tooget hello 儲存資訊從 hello 入口網站： 找不到儲存體帳戶，請按一下 hello 存取金鑰，然後複製 hello 名稱和 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="86c69-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="86c69-169">tooget hello 容器名稱： 尋找您的儲存體帳戶，請選取**Blob**，選取您想要 tooupload hello 內容 hello 容器 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="86c69-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="86c69-170">以下是 hello Aspera 用戶端 hello 螢幕擷取畫面**連線管理員**您必須在其中指定 hello 'Azure' 的儲存類型和認證，以及 hello blob 容器。</span><span class="sxs-lookup"><span data-stu-id="86c69-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="86c69-172">資源</span><span class="sxs-lookup"><span data-stu-id="86c69-172">Resources</span></span>

<span data-ttu-id="86c69-173">這篇文章中提及 hello 下列資源。</span><span class="sxs-lookup"><span data-stu-id="86c69-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="86c69-174">Connect 瀏覽器外掛程式</span><span class="sxs-lookup"><span data-stu-id="86c69-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="86c69-175">Connect 指南</span><span class="sxs-lookup"><span data-stu-id="86c69-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="86c69-176">Aspera 用戶端</span><span class="sxs-lookup"><span data-stu-id="86c69-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="86c69-177">用戶端指南</span><span class="sxs-lookup"><span data-stu-id="86c69-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="86c69-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86c69-178">Next steps</span></span>

<span data-ttu-id="86c69-179">您現在可以[從儲存體帳戶將 Blob 複製到 AMS 帳戶](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account)。</span><span class="sxs-lookup"><span data-stu-id="86c69-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="86c69-180">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="86c69-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86c69-181">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="86c69-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

