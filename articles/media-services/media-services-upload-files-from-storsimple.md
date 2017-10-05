---
title: "從 Azure StorSimple 將檔案上傳至 Azure 媒體服務帳戶 | Microsoft Docs"
description: "本文提供 Azure StorSimple Data Manager 的簡短概述。 本文也會連結至教學課程，說明如何從 StorSimple 擷取資料，並將它當作資產上傳至 Azure 媒體服務帳戶。"
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
ms.openlocfilehash: 636d55c15aa383208ffb39d5224123831af962c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="4afcc-104">從 Azure StorSimple 將檔案上傳至 Azure 媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="4afcc-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="4afcc-105">本文提供 Azure StorSimple Data Manager 的簡短概述。</span><span class="sxs-lookup"><span data-stu-id="4afcc-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="4afcc-106">本文也會連結至教學課程，說明如何從 StorSimple 擷取資料，並將此資料當作資產上傳至 Azure 媒體服務 (AMS) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4afcc-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="4afcc-107">Azure StorSimple Data Manager 目前處於私人預覽階段。</span><span class="sxs-lookup"><span data-stu-id="4afcc-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="4afcc-108">概觀</span><span class="sxs-lookup"><span data-stu-id="4afcc-108">Overview</span></span>

<span data-ttu-id="4afcc-109">在媒體服務中，您會將數位檔案上傳到到資產。</span><span class="sxs-lookup"><span data-stu-id="4afcc-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="4afcc-110">「資產」可以包含視訊、音訊、影像、縮圖集合、文字播放軌及隱藏式輔助字幕檔案 (以及這些檔案的相關中繼資料)。上傳檔案之後，您的內容會安全地儲存在雲端，以進一步進行處理和串流處理。</span><span class="sxs-lookup"><span data-stu-id="4afcc-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="4afcc-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) 使用雲端儲存體做為內部部署解決方案的擴充功能，並且跨內部部署儲存體和雲端儲存體自動將資料分層。</span><span class="sxs-lookup"><span data-stu-id="4afcc-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="4afcc-112">StorSimple 裝置會先刪除重複資料並加以壓縮，再將資料傳送至雲端，以非常有效率的方式將大型檔案傳送至雲端。</span><span class="sxs-lookup"><span data-stu-id="4afcc-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span></span> <span data-ttu-id="4afcc-113">[StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) 服務提供 API，可讓您從 StorSimple 擷取資料並將它呈現為 AMS 資產。</span><span class="sxs-lookup"><span data-stu-id="4afcc-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="4afcc-114">開始使用</span><span class="sxs-lookup"><span data-stu-id="4afcc-114">Get started</span></span>

1. <span data-ttu-id="4afcc-115">[建立媒體服務帳戶](media-services-portal-create-account.md)以便將資產傳輸至其中。</span><span class="sxs-lookup"><span data-stu-id="4afcc-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span></span>
2. <span data-ttu-id="4afcc-116">註冊 Data Manager 預覽版本，如 [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md)一文所述。</span><span class="sxs-lookup"><span data-stu-id="4afcc-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="4afcc-117">建立 StorSimple Data Manager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4afcc-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="4afcc-118">建立資料轉換作業，以在執行時從 StorSimple 裝置擷取資料並將它傳輸到 AMS 帳戶中做為資產。</span><span class="sxs-lookup"><span data-stu-id="4afcc-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="4afcc-119">當作業開始執行時，會建立儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="4afcc-119">When the job starts running, a storage queue is created.</span></span> <span data-ttu-id="4afcc-120">此佇列中會填入已轉換的 blob 備妥時的相關訊息。</span><span class="sxs-lookup"><span data-stu-id="4afcc-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="4afcc-121">此佇列的名稱與作業定義的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="4afcc-121">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="4afcc-122">您可以使用此佇列來判斷資產何時準備就緒，並呼叫您所需的媒體服務作業以在其上執行。</span><span class="sxs-lookup"><span data-stu-id="4afcc-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span></span> <span data-ttu-id="4afcc-123">例如，您可以使用此佇列來觸發 Azure Function，其中有所需的媒體服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="4afcc-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="4afcc-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4afcc-124">See also</span></span>

[<span data-ttu-id="4afcc-125">使用 .Net SDK 在 Data Manager 中觸發作業</span><span class="sxs-lookup"><span data-stu-id="4afcc-125">Use the .Net SDK to trigger jobs in the Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="4afcc-126">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="4afcc-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4afcc-127">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="4afcc-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4afcc-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4afcc-128">Next steps</span></span>

<span data-ttu-id="4afcc-129">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="4afcc-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="4afcc-130">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="4afcc-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
