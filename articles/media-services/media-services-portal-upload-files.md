---
title: "aaa\"上傳檔案至 Media Services 帳戶使用 hello Azure 入口網站 |Microsoft 文件 」"
description: "本教學課程中引導您 hello 步驟的上傳檔案至媒體服務帳戶使用 hello Azure 入口網站"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="00f00-103">將檔案上傳到 Media Services 帳戶使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="00f00-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00f00-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="00f00-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="00f00-105">.NET</span><span class="sxs-lookup"><span data-stu-id="00f00-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="00f00-106">REST</span><span class="sxs-lookup"><span data-stu-id="00f00-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="00f00-107">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="00f00-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="00f00-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="00f00-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="00f00-109">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="00f00-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="00f00-110">hello 資產可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。</span><span class="sxs-lookup"><span data-stu-id="00f00-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="00f00-111">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="00f00-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="00f00-112">沒有支援 Media Services 中的處理限制 toohello 最大檔案大小。</span><span class="sxs-lookup"><span data-stu-id="00f00-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="00f00-113">請參閱[這](media-services-quotas-and-limitations.md)hello 檔案大小限制的詳細主題。</span><span class="sxs-lookup"><span data-stu-id="00f00-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="00f00-114">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="00f00-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="00f00-115">在 hello**設定**刀鋒視窗中，按一下 **資產**。</span><span class="sxs-lookup"><span data-stu-id="00f00-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![上傳檔案](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="00f00-117">按一下 hello**上傳** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="00f00-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="00f00-118">hello**上載視訊資產** 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="00f00-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="00f00-119">檔案大小不受限。</span><span class="sxs-lookup"><span data-stu-id="00f00-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="00f00-120">瀏覽您的電腦上的預期 toohello 視訊、 加以選取，並點擊 [確定]。</span><span class="sxs-lookup"><span data-stu-id="00f00-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="00f00-121">hello 上載啟動，而且您可以看見 hello 進度 hello 檔名底下。</span><span class="sxs-lookup"><span data-stu-id="00f00-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="00f00-122">Hello 上傳完成之後，您會看到 hello hello 中所列的新資產**資產**視窗。</span><span class="sxs-lookup"><span data-stu-id="00f00-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="00f00-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00f00-123">Next steps</span></span>
<span data-ttu-id="00f00-124">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="00f00-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="00f00-125">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="00f00-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="00f00-126">您也可以使用 Azure 函式 tootrigger 抵達 hello 設定容器中的檔案為基礎的編碼工作。</span><span class="sxs-lookup"><span data-stu-id="00f00-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="00f00-127">如需詳細資訊，請參閱[此範例](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )。</span><span class="sxs-lookup"><span data-stu-id="00f00-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="00f00-128">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="00f00-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="00f00-129">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="00f00-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

