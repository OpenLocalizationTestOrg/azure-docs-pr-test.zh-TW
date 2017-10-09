---
title: "aaaAzure Media Services 編碼錯誤碼 |Microsoft 文件"
description: "本主題列出以防 hello 編碼工作執行期間發生錯誤，可能會傳回的錯誤碼..."
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
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="e4446-103">編碼錯誤碼</span><span class="sxs-lookup"><span data-stu-id="e4446-103">Encoding error codes</span></span>

<span data-ttu-id="e4446-104">hello 下表列出可能會傳回，以防 hello 編碼工作執行期間發生錯誤的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="e4446-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="e4446-105">tooget 錯誤詳細資料，您的.NET 程式碼，使用 hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="e4446-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="e4446-106">tooget 錯誤詳細資料，您的其餘程式碼中使用 hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API。</span><span class="sxs-lookup"><span data-stu-id="e4446-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="e4446-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="e4446-107">ErrorDetail.Code</span></span> | <span data-ttu-id="e4446-108">導致發生錯誤的可能原因</span><span class="sxs-lookup"><span data-stu-id="e4446-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="e4446-109">不明</span><span class="sxs-lookup"><span data-stu-id="e4446-109">Unknown</span></span> |<span data-ttu-id="e4446-110">執行 hello 工作時發生未知的錯誤</span><span class="sxs-lookup"><span data-stu-id="e4446-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="e4446-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="e4446-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="e4446-112">涵蓋下載輸入資產中之錯誤 (例如無效的檔案名稱、長度為零檔案、錯誤格式等等) 的錯誤類別。</span><span class="sxs-lookup"><span data-stu-id="e4446-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="e4446-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="e4446-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="e4446-114">涵蓋 hello 服務端的網路或存放裝置錯誤的範例下載時的問題的錯誤分類。</span><span class="sxs-lookup"><span data-stu-id="e4446-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="e4446-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="e4446-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="e4446-116">錯誤分類其中工作<see cref="MediaTask.PrivateData"/>（組態） 無效，例如 hello 組態並不是有效的系統預設值或包含無效的 XML。</span><span class="sxs-lookup"><span data-stu-id="e4446-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="e4446-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="e4446-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="e4446-118">Hello hello 問題輸入媒體檔案造成失敗的 hello 工作執行期間發生的錯誤分類。</span><span class="sxs-lookup"><span data-stu-id="e4446-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="e4446-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="e4446-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="e4446-120">分類的錯誤，其中 hello 媒體處理器無法處理提供 hello 檔案-媒體格式不受支援，或者不符合 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="e4446-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="e4446-121">例如，嘗試 tooproduce 具有唯一的視訊資產的僅限音訊輸出</span><span class="sxs-lookup"><span data-stu-id="e4446-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="e4446-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="e4446-122">ErrorProcessingTask</span></span> |<span data-ttu-id="e4446-123">在 hello 的不相關的 toocontent hello 工作處理期間所遇到 hello 媒體處理器的其他錯誤分類。</span><span class="sxs-lookup"><span data-stu-id="e4446-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="e4446-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="e4446-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="e4446-125">上傳 hello 輸出資產時的錯誤分類</span><span class="sxs-lookup"><span data-stu-id="e4446-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="e4446-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="e4446-126">ErrorCancelingTask</span></span> |<span data-ttu-id="e4446-127">分類的錯誤 toocover 失敗時嘗試 toocancel hello 工作</span><span class="sxs-lookup"><span data-stu-id="e4446-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="e4446-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="e4446-128">TransientError</span></span> |<span data-ttu-id="e4446-129">問題分類的錯誤 toocover 暫時性 （例如。</span><span class="sxs-lookup"><span data-stu-id="e4446-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="e4446-130">Azure 儲存體發生暫時性網路問題)</span><span class="sxs-lookup"><span data-stu-id="e4446-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="e4446-131">從 hello tooget 說明**Media Services**小組，請開啟[支援票證](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="e4446-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e4446-132">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e4446-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e4446-133">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e4446-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="e4446-134">相關文章</span><span class="sxs-lookup"><span data-stu-id="e4446-134">Related articles</span></span>
* [<span data-ttu-id="e4446-135">透過自訂 Media Encoder Standard 預設值來執行進階編碼工作</span><span class="sxs-lookup"><span data-stu-id="e4446-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="e4446-136">配額和限制</span><span class="sxs-lookup"><span data-stu-id="e4446-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
