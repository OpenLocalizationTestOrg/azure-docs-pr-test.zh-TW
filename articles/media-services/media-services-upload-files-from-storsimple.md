---
title: "從 Azure StorSimple 的 Azure Media Services 帳戶將 aaaUpload 檔案 |Microsoft 文件"
description: "本文提供 Azure StorSimple Data Manager 的簡短概述。 hello 發行項也會連結 tootutorials，教您如何從 StorSimple tooextract 資料並將它上傳為資產 tooan Azure Media Services 帳戶。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="9c80a-104">從 Azure StorSimple 將檔案上傳至 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="9c80a-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="9c80a-105">本文提供 Azure StorSimple Data Manager 的簡短概述。</span><span class="sxs-lookup"><span data-stu-id="9c80a-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="9c80a-106">hello 發行項也會連結 tootutorials，教您如何從 StorSimple tooextract 資料並將此資料上傳為資產 tooan Azure 媒體服務 (AMS) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c80a-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="9c80a-107">Azure StorSimple Data Manager 目前處於私人預覽階段。</span><span class="sxs-lookup"><span data-stu-id="9c80a-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="9c80a-108">概觀</span><span class="sxs-lookup"><span data-stu-id="9c80a-108">Overview</span></span>

<span data-ttu-id="9c80a-109">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="9c80a-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="9c80a-110">hello 資產可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。</span><span class="sxs-lookup"><span data-stu-id="9c80a-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="9c80a-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) hello 的延伸模組在內部部署方案並自動層 hello 在內部部署儲存體和雲端存放裝置之間的資料，使用雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c80a-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="9c80a-112">hello StorSimple 裝置 dedupes，並將您的資料壓縮再將它傳送 toohello 雲端進行傳送大型檔案 toohello 雲端非常有效率。</span><span class="sxs-lookup"><span data-stu-id="9c80a-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="9c80a-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md)服務提供 Api，可讓您 tooextract 資料從 StorSimple，並加以呈現為 AMS 資產。</span><span class="sxs-lookup"><span data-stu-id="9c80a-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="9c80a-114">開始使用</span><span class="sxs-lookup"><span data-stu-id="9c80a-114">Get started</span></span>

1. <span data-ttu-id="9c80a-115">[建立 Media Services 帳戶](media-services-portal-create-account.md)要 tootransfer hello 資產。</span><span class="sxs-lookup"><span data-stu-id="9c80a-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="9c80a-116">註冊資料管理員預覽 hello 中所述[StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9c80a-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="9c80a-117">建立 StorSimple Data Manager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c80a-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="9c80a-118">建立資料轉換作業，以在執行時從 StorSimple 裝置擷取資料並將它傳輸到 AMS 帳戶中做為資產。</span><span class="sxs-lookup"><span data-stu-id="9c80a-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="9c80a-119">Hello 作業啟動時執行，則會建立儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="9c80a-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="9c80a-120">此佇列中會填入已轉換的 blob 備妥時的相關訊息。</span><span class="sxs-lookup"><span data-stu-id="9c80a-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="9c80a-121">hello 這個佇列名稱是 hello 與 hello hello 工作定義名稱相同。</span><span class="sxs-lookup"><span data-stu-id="9c80a-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="9c80a-122">您可以使用這個佇列 toodetermine 時資產是準備以及您想要的媒體服務作業 toorun 呼叫它。</span><span class="sxs-lookup"><span data-stu-id="9c80a-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="9c80a-123">例如，您可以使用這個佇列 tootrigger hello 必要的媒體服務程式碼中擁有 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="9c80a-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="9c80a-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9c80a-124">See also</span></span>

[<span data-ttu-id="9c80a-125">使用 hello.Net SDK tootrigger hello 資料管理員中的工作</span><span class="sxs-lookup"><span data-stu-id="9c80a-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="9c80a-126">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="9c80a-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9c80a-127">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="9c80a-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9c80a-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c80a-128">Next steps</span></span>

<span data-ttu-id="9c80a-129">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="9c80a-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="9c80a-130">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="9c80a-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
