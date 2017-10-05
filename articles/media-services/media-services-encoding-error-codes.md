---
title: "Azure 媒體服務編碼錯誤代碼 | Microsoft Docs"
description: "本主題列出在編碼工作執行期間發生錯誤時下可能傳回的錯誤碼。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="dfbad-103">編碼錯誤碼</span><span class="sxs-lookup"><span data-stu-id="dfbad-103">Encoding error codes</span></span>

<span data-ttu-id="dfbad-104">下表列出在編碼工作執行期間發生錯誤的情況下可能傳回的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="dfbad-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="dfbad-105">若要取得 .NET 程式碼中的錯誤詳細資料，請使用 [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) 類別。</span><span class="sxs-lookup"><span data-stu-id="dfbad-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="dfbad-106">若要取得 REST 程式碼中的錯誤詳細資料，請使用 [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API。</span><span class="sxs-lookup"><span data-stu-id="dfbad-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="dfbad-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="dfbad-107">ErrorDetail.Code</span></span> | <span data-ttu-id="dfbad-108">導致發生錯誤的可能原因</span><span class="sxs-lookup"><span data-stu-id="dfbad-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="dfbad-109">不明</span><span class="sxs-lookup"><span data-stu-id="dfbad-109">Unknown</span></span> |<span data-ttu-id="dfbad-110">執行工作時發生不明錯誤</span><span class="sxs-lookup"><span data-stu-id="dfbad-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="dfbad-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="dfbad-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="dfbad-112">涵蓋下載輸入資產中之錯誤 (例如無效的檔案名稱、長度為零檔案、錯誤格式等等) 的錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="dfbad-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="dfbad-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="dfbad-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="dfbad-114">涵蓋服務端問題 (例如下載時發生網路或儲存體錯誤) 的錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="dfbad-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="dfbad-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="dfbad-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="dfbad-116">工作 <see cref="MediaTask.PrivateData"/> (設定) 無效時的錯誤類別，例如設定不是有效的系統預設或包含無效的 XML。</span><span class="sxs-lookup"><span data-stu-id="dfbad-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="dfbad-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="dfbad-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="dfbad-118">在工作執行期間因輸入媒體檔案內部問題導致失敗的錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="dfbad-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="dfbad-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="dfbad-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="dfbad-120">媒體處理器無法處理提供之檔案 (不支援的媒體格式或與組態不符) 的錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="dfbad-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="dfbad-121">例如，嘗試從只有影片的資產產生只含音訊的輸出</span><span class="sxs-lookup"><span data-stu-id="dfbad-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="dfbad-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="dfbad-122">ErrorProcessingTask</span></span> |<span data-ttu-id="dfbad-123">媒體處理器在處理和內容不相關的工作時發生的其他錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="dfbad-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="dfbad-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="dfbad-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="dfbad-125">上傳輸出資產時的錯誤類別</span><span class="sxs-lookup"><span data-stu-id="dfbad-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="dfbad-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="dfbad-126">ErrorCancelingTask</span></span> |<span data-ttu-id="dfbad-127">涵蓋嘗試取消工作時失敗的錯誤類別</span><span class="sxs-lookup"><span data-stu-id="dfbad-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="dfbad-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="dfbad-128">TransientError</span></span> |<span data-ttu-id="dfbad-129">涵蓋暫時性問題的錯誤類別 (例如</span><span class="sxs-lookup"><span data-stu-id="dfbad-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="dfbad-130">Azure 儲存體發生暫時性網路問題)</span><span class="sxs-lookup"><span data-stu-id="dfbad-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="dfbad-131">若要獲得 **媒體服務** 小組的協助，請開啟 [支援票證](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="dfbad-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="dfbad-132">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="dfbad-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dfbad-133">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="dfbad-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="dfbad-134">相關文章</span><span class="sxs-lookup"><span data-stu-id="dfbad-134">Related articles</span></span>
* [<span data-ttu-id="dfbad-135">透過自訂 Media Encoder Standard 預設值來執行進階編碼工作</span><span class="sxs-lookup"><span data-stu-id="dfbad-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="dfbad-136">配額和限制</span><span class="sxs-lookup"><span data-stu-id="dfbad-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
