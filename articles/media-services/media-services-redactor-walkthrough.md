---
title: "使用 Azure 媒體分析修訂臉部逐步解說 | Microsoft Docs"
description: "本主題逐步說明如何使用 Azure 媒體服務總管 (AMSE) 和 Azure 媒體修訂器視覺化檢視 (開放原始碼工具) 來執行完整的修訂工作流程。"
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="daa14-103">使用 Azure 媒體分析修訂臉部逐步解說</span><span class="sxs-lookup"><span data-stu-id="daa14-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="daa14-104">概觀</span><span class="sxs-lookup"><span data-stu-id="daa14-104">Overview</span></span>

<span data-ttu-id="daa14-105">**Azure 媒體修訂器** 是 [Azure 媒體分析](media-services-analytics-overview.md) 媒體處理器 (MP)，可在雲端提供可調整的臉部修訂。</span><span class="sxs-lookup"><span data-stu-id="daa14-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="daa14-106">臉部修訂可讓您修改視訊，以模糊所選人物的臉部。</span><span class="sxs-lookup"><span data-stu-id="daa14-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="daa14-107">在公共安全和新聞媒體案例中，您可能會想要使用臉部修訂服務。</span><span class="sxs-lookup"><span data-stu-id="daa14-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="daa14-108">若要手動修訂包含多個臉部的幾分鐘影片，可能要花上數小時的時間，若使用此服務，則只需要幾個簡單的步驟就能完成臉部修訂程序。</span><span class="sxs-lookup"><span data-stu-id="daa14-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="daa14-109">如需詳細資訊，請參閱[此](https://azure.microsoft.com/blog/azure-media-redactor/)部落格。</span><span class="sxs-lookup"><span data-stu-id="daa14-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="daa14-110">如需 **Azure 媒體修訂器**的詳細資訊，請參閱[臉部修訂概觀](media-services-face-redaction.md)主題。</span><span class="sxs-lookup"><span data-stu-id="daa14-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="daa14-111">本主題逐步說明如何使用 Azure 媒體服務總管 (AMSE) 和 Azure 媒體修訂器視覺化檢視 (開放原始碼工具) 來執行完整的修訂工作流程。</span><span class="sxs-lookup"><span data-stu-id="daa14-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="daa14-112">**Azure 媒體修訂器** MP 目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="daa14-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="daa14-113">在所有公開的 Azure 區域及美國政府和中國的數據中心皆有提供。</span><span class="sxs-lookup"><span data-stu-id="daa14-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="daa14-114">此預覽版本目前以免費方式提供。</span><span class="sxs-lookup"><span data-stu-id="daa14-114">This preview is currently free of charge.</span></span> <span data-ttu-id="daa14-115">在目前的版本中，處理的視訊長度限制為 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="daa14-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="daa14-116">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) 。</span><span class="sxs-lookup"><span data-stu-id="daa14-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="daa14-117">Azure 媒體服務總管工作流程</span><span class="sxs-lookup"><span data-stu-id="daa14-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="daa14-118">開始使用修訂器最簡單的方法，是使用 github 上的開放原始碼 AMSE 工具。</span><span class="sxs-lookup"><span data-stu-id="daa14-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="daa14-119">如果您不需要註解 json 或臉部 jpg 影像的存取權，您可以透過 [Combined] \(合併) 模式執行簡單的工作流程。</span><span class="sxs-lookup"><span data-stu-id="daa14-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="daa14-120">下載及安裝</span><span class="sxs-lookup"><span data-stu-id="daa14-120">Download and setup</span></span>

1. <span data-ttu-id="daa14-121">從[這裡](https://github.com/Azure/Azure-Media-Services-Explorer)下載 AMSE 工具。</span><span class="sxs-lookup"><span data-stu-id="daa14-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="daa14-122">使用您的服務金鑰登入您的媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="daa14-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="daa14-123">若要取得帳戶名稱和金鑰資訊，請移至 [Azure 入口網站](https://portal.azure.com/)，然後選取 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="daa14-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="daa14-124">選取 [Settings] \(設定) > [Keys] \(金鑰)。</span><span class="sxs-lookup"><span data-stu-id="daa14-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="daa14-125">[管理金鑰] 視窗會顯示帳戶名稱以及主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="daa14-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="daa14-126">複製帳戶名稱和主要金鑰的值。</span><span class="sxs-lookup"><span data-stu-id="daa14-126">Copy values of the account name and the primary key.</span></span>

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="daa14-128">第一階段 – 分析模式</span><span class="sxs-lookup"><span data-stu-id="daa14-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="daa14-129">透過 [Asset] \(資產) –> [Upload] \(上傳) 或以拖放方式上傳您的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="daa14-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="daa14-130">按一下滑鼠右鍵，使用 [Media Analytics] \(媒體分析) –> [Azure Media Redactor] \(Azure 媒體修訂器) –> [Analyze mode] \(分析模式) 處理您的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="daa14-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="daa14-133">輸出會包含具有臉部位置資料的註解 json 檔案，以及每個所偵測臉部的 jpg。</span><span class="sxs-lookup"><span data-stu-id="daa14-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="daa14-135">第二階段 – 修訂模式</span><span class="sxs-lookup"><span data-stu-id="daa14-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="daa14-136">將原始的視訊資產上傳至第一階段中的輸出，並設為主要資產。</span><span class="sxs-lookup"><span data-stu-id="daa14-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="daa14-138">(選擇性) 上傳包含您想修訂之識別碼清單 (以新行分隔) 的 'Dance_idlist.txt' 檔案。</span><span class="sxs-lookup"><span data-stu-id="daa14-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="daa14-140">(選擇性) 編輯 annotations.json 檔案，例如增加周框方塊界限。</span><span class="sxs-lookup"><span data-stu-id="daa14-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="daa14-141">以滑鼠右鍵按一下第一階段中的輸出資產，選取修訂器，並以 [Redact] \(修訂) 模式執行。</span><span class="sxs-lookup"><span data-stu-id="daa14-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="daa14-143">下載或分享最終修訂的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="daa14-143">Download or share the final redacted output asset.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="daa14-145">Azure 媒體修訂器視覺化檢視開放原始碼工具</span><span class="sxs-lookup"><span data-stu-id="daa14-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="daa14-146">開放原始碼[視覺化檢視工具](https://github.com/Microsoft/azure-media-redactor-visualizer)旨在協助剛開始註解格式操作的開發人員剖析和使用輸出。</span><span class="sxs-lookup"><span data-stu-id="daa14-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="daa14-147">複製儲存機制後，為了執行專案，您必須從[官方網站](https://ffmpeg.org/download.html)下載 FFMPEG。</span><span class="sxs-lookup"><span data-stu-id="daa14-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="daa14-148">如果您是嘗試剖析 JSON 註解資料的開發人員，請在 Models.MetaData 內尋找範例程式碼的範例。</span><span class="sxs-lookup"><span data-stu-id="daa14-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="daa14-149">設定工具</span><span class="sxs-lookup"><span data-stu-id="daa14-149">Set up the tool</span></span>

1.  <span data-ttu-id="daa14-150">下載和建置整個方案。</span><span class="sxs-lookup"><span data-stu-id="daa14-150">Download and build the entire solution.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="daa14-152">從[這裡](https://ffmpeg.org/download.html)下載 FFMPEG。</span><span class="sxs-lookup"><span data-stu-id="daa14-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="daa14-153">此專案原先是使用含靜態連結的版本 be1d324 (2016-10-04) 所開發。</span><span class="sxs-lookup"><span data-stu-id="daa14-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="daa14-154">將 ffmpeg.exe 和 ffprobe.exe 複製到和 AzureMediaRedactor.exe 相同的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="daa14-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="daa14-156">執行 AzureMediaRedactor.exe。</span><span class="sxs-lookup"><span data-stu-id="daa14-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="daa14-157">使用工具</span><span class="sxs-lookup"><span data-stu-id="daa14-157">Use the tool</span></span>

1. <span data-ttu-id="daa14-158">在您的 Azure 媒體服務帳戶中使用 [Analyze] \(分析) 模式的 [Redactor MP] \(修訂器 MP) 處理您的視訊。</span><span class="sxs-lookup"><span data-stu-id="daa14-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="daa14-159">下載原始視訊檔和「修訂 - 分析」工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="daa14-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="daa14-160">執行視覺化檢視應用程式，然後選擇上述檔案。</span><span class="sxs-lookup"><span data-stu-id="daa14-160">Run the visualizer application and choose the files above.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="daa14-162">預覽檔案。</span><span class="sxs-lookup"><span data-stu-id="daa14-162">Preview your file.</span></span> <span data-ttu-id="daa14-163">透過右側資訊看板選取您想要模糊化的臉部。</span><span class="sxs-lookup"><span data-stu-id="daa14-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="daa14-165">下方的文字欄位會更新為臉部識別碼。</span><span class="sxs-lookup"><span data-stu-id="daa14-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="daa14-166">建立名為 "idlist.txt" 的檔案，其中包含這些識別碼清單 (以新行分隔)。</span><span class="sxs-lookup"><span data-stu-id="daa14-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="daa14-167">idlist.txt 應該以 ANSI 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="daa14-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="daa14-168">您可以使用 [記事本] 來儲存為 ANSI 格式。</span><span class="sxs-lookup"><span data-stu-id="daa14-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="daa14-169">將這個檔案上傳到步驟 1 中的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="daa14-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="daa14-170">另將原始的視訊上傳到這個資產，並設為主要資產。</span><span class="sxs-lookup"><span data-stu-id="daa14-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="daa14-171">在這個資產上使用「修訂」模式執行「修訂」工作，以取得最終修訂的視訊。</span><span class="sxs-lookup"><span data-stu-id="daa14-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="daa14-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="daa14-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="daa14-173">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="daa14-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="daa14-174">相關連結</span><span class="sxs-lookup"><span data-stu-id="daa14-174">Related links</span></span>
[<span data-ttu-id="daa14-175">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="daa14-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="daa14-176">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="daa14-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="daa14-177">宣布推出適用於 Azure 媒體分析的臉部修訂功能</span><span class="sxs-lookup"><span data-stu-id="daa14-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
