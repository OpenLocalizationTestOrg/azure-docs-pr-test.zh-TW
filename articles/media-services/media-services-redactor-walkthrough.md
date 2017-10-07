---
title: "Azure 媒體分析逐步解說 aaaRedact 字體 |Microsoft 文件"
description: "本主題說明如何逐步解說指示 toorun 使用 Azure 媒體服務總管 (AMSE) 和 Azure 媒體 Redactor 視覺化檢視 （開放原始碼工具） 的完整 redaction 工作流程。"
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
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="3aab8-103">使用 Azure 媒體分析修訂臉部逐步解說</span><span class="sxs-lookup"><span data-stu-id="3aab8-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="3aab8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3aab8-104">Overview</span></span>

<span data-ttu-id="3aab8-105">**Azure 媒體 Redactor**是[Azure 媒體分析](media-services-analytics-overview.md)提供可擴充的字體 redaction hello 雲端中的媒體處理器 (MP)。</span><span class="sxs-lookup"><span data-stu-id="3aab8-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="3aab8-106">字體 redaction 可讓您 toomodify 順序 tooblur 表面選取個人視訊。</span><span class="sxs-lookup"><span data-stu-id="3aab8-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="3aab8-107">您可以在公用的安全性和新聞媒體案例 toouse hello 朝 redaction 服務。</span><span class="sxs-lookup"><span data-stu-id="3aab8-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="3aab8-108">幾分鐘的影片，其中包含多個字型都會小時 tooredact 以手動方式，但具有此服務的 hello 圖示 redaction 程序將需要幾個簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="3aab8-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="3aab8-109">如需詳細資訊，請參閱[此](https://azure.microsoft.com/blog/azure-media-redactor/)部落格。</span><span class="sxs-lookup"><span data-stu-id="3aab8-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="3aab8-110">如需詳細資訊**Azure 媒體 Redactor**，請參閱 hello[朝 redaction 概觀](media-services-face-redaction.md)主題。</span><span class="sxs-lookup"><span data-stu-id="3aab8-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="3aab8-111">本主題說明如何逐步解說指示 toorun 使用 Azure 媒體服務總管 (AMSE) 和 Azure 媒體 Redactor 視覺化檢視 （開放原始碼工具） 的完整 redaction 工作流程。</span><span class="sxs-lookup"><span data-stu-id="3aab8-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="3aab8-112">hello **Azure 媒體 Redactor** MP 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="3aab8-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="3aab8-113">在所有公開的 Azure 區域及美國政府和中國的數據中心皆有提供。</span><span class="sxs-lookup"><span data-stu-id="3aab8-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="3aab8-114">此預覽版本目前以免費方式提供。</span><span class="sxs-lookup"><span data-stu-id="3aab8-114">This preview is currently free of charge.</span></span> <span data-ttu-id="3aab8-115">在 hello 目前版本中，沒有 10 分鐘限制處理視訊的長度。</span><span class="sxs-lookup"><span data-stu-id="3aab8-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="3aab8-116">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) 。</span><span class="sxs-lookup"><span data-stu-id="3aab8-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="3aab8-117">Azure 媒體服務總管工作流程</span><span class="sxs-lookup"><span data-stu-id="3aab8-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="3aab8-118">hello 最簡單的方式 tooget 入門 Redactor 是 toouse hello 開放原始碼 github 上的 AMSE 工具。</span><span class="sxs-lookup"><span data-stu-id="3aab8-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="3aab8-119">您可以執行簡單的工作流程，經由**結合**模式，如果您不需要存取 toohello 註釋 json 或 hello 朝 jpg 影像。</span><span class="sxs-lookup"><span data-stu-id="3aab8-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="3aab8-120">下載及安裝</span><span class="sxs-lookup"><span data-stu-id="3aab8-120">Download and setup</span></span>

1. <span data-ttu-id="3aab8-121">下載 hello AMSE 工具從[這裡](https://github.com/Azure/Azure-Media-Services-Explorer)。</span><span class="sxs-lookup"><span data-stu-id="3aab8-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="3aab8-122">登入 tooyour Media Services 帳戶使用您的服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="3aab8-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="3aab8-123">tooobtain hello 帳戶名稱和金鑰資訊，請移 toohello [Azure 入口網站](https://portal.azure.com/)選取 AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3aab8-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="3aab8-124">選取 [Settings] \(設定) > [Keys] \(金鑰)。</span><span class="sxs-lookup"><span data-stu-id="3aab8-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="3aab8-125">hello 管理金鑰 windows 顯示 hello 帳戶名稱，並顯示 hello 主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="3aab8-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="3aab8-126">將複製 hello 帳戶名稱和 hello 主索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="3aab8-126">Copy values of hello account name and hello primary key.</span></span>

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="3aab8-128">第一階段 – 分析模式</span><span class="sxs-lookup"><span data-stu-id="3aab8-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="3aab8-129">透過 [Asset] \(資產) –> [Upload] \(上傳) 或以拖放方式上傳您的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="3aab8-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="3aab8-130">按一下滑鼠右鍵，使用 [Media Analytics] \(媒體分析) –> [Azure Media Redactor] \(Azure 媒體修訂器) –> [Analyze mode] \(分析模式) 處理您的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="3aab8-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="3aab8-133">hello 輸出將包括字體位置資料，使用的註解 json 檔案，以及每個偵測到的字體的 jpg。</span><span class="sxs-lookup"><span data-stu-id="3aab8-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="3aab8-135">第二階段 – 修訂模式</span><span class="sxs-lookup"><span data-stu-id="3aab8-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="3aab8-136">上傳您原始視訊資產 toohello 來自 hello 第一次傳遞的輸出，並將設為主要的資產。</span><span class="sxs-lookup"><span data-stu-id="3aab8-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="3aab8-138">（選擇性）上傳包含 hello 想 tooredact Id 的新行字元分隔清單的 'Dance_idlist.txt' 檔案。</span><span class="sxs-lookup"><span data-stu-id="3aab8-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="3aab8-140">（選擇性）將任何編輯 toohello annotations.json 檔案例如增加 hello 週框方塊的界限。</span><span class="sxs-lookup"><span data-stu-id="3aab8-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="3aab8-141">以滑鼠右鍵按一下從 hello 第一次傳遞 hello 輸出資產、 選取 hello Redactor，並執行以 hello **Redact**模式。</span><span class="sxs-lookup"><span data-stu-id="3aab8-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="3aab8-143">下載或共用 hello 最終經過校訂輸出資產。</span><span class="sxs-lookup"><span data-stu-id="3aab8-143">Download or share hello final redacted output asset.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="3aab8-145">Azure 媒體修訂器視覺化檢視開放原始碼工具</span><span class="sxs-lookup"><span data-stu-id="3aab8-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="3aab8-146">開放原始碼[視覺化檢視工具](https://github.com/Microsoft/azure-media-redactor-visualizer)是剛開始使用剖析和 hello 輸出 hello 註解格式的設計的 toohelp 開發人員。</span><span class="sxs-lookup"><span data-stu-id="3aab8-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="3aab8-147">您複製 hello 儲存機制，在訂單 toorun hello 專案中之後, 您將需要 toodownload FFMPEG 從其[官方網站](https://ffmpeg.org/download.html)。</span><span class="sxs-lookup"><span data-stu-id="3aab8-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="3aab8-148">如果您是開發人員嘗試 tooparse hello JSON 註解資料，尋找內部 Models.MetaData 範例程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="3aab8-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="3aab8-149">設定 hello 工具</span><span class="sxs-lookup"><span data-stu-id="3aab8-149">Set up hello tool</span></span>

1.  <span data-ttu-id="3aab8-150">下載並建置 hello 整個方案。</span><span class="sxs-lookup"><span data-stu-id="3aab8-150">Download and build hello entire solution.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="3aab8-152">從[這裡](https://ffmpeg.org/download.html)下載 FFMPEG。</span><span class="sxs-lookup"><span data-stu-id="3aab8-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="3aab8-153">此專案原先是使用含靜態連結的版本 be1d324 (2016-10-04) 所開發。</span><span class="sxs-lookup"><span data-stu-id="3aab8-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="3aab8-154">複製 ffmpeg.exe 和 ffprobe.exe toohello AzureMediaRedactor.exe 與相同的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="3aab8-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="3aab8-156">執行 AzureMediaRedactor.exe。</span><span class="sxs-lookup"><span data-stu-id="3aab8-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="3aab8-157">使用 hello 工具</span><span class="sxs-lookup"><span data-stu-id="3aab8-157">Use hello tool</span></span>

1. <span data-ttu-id="3aab8-158">處理您在 Azure Media Services 帳戶以 hello Redactor 管理組件中進行分析 模式中的視訊。</span><span class="sxs-lookup"><span data-stu-id="3aab8-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="3aab8-159">下載 hello 原始視訊檔和 hello Redaction hello 輸出-分析工作。</span><span class="sxs-lookup"><span data-stu-id="3aab8-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="3aab8-160">執行 hello 視覺化檢視應用程式並選擇上述 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="3aab8-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="3aab8-162">預覽檔案。</span><span class="sxs-lookup"><span data-stu-id="3aab8-162">Preview your file.</span></span> <span data-ttu-id="3aab8-163">選取以您想要透過 hello [資訊看板] 上 hello tooblur 右。</span><span class="sxs-lookup"><span data-stu-id="3aab8-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="3aab8-165">hello 朝識別碼將會更新 hello 下文字欄位。</span><span class="sxs-lookup"><span data-stu-id="3aab8-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="3aab8-166">建立名為 "idlist.txt" 的檔案，其中包含這些識別碼清單 (以新行分隔)。</span><span class="sxs-lookup"><span data-stu-id="3aab8-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="3aab8-167">hello idlist.txt 應該儲存在 ANSI。</span><span class="sxs-lookup"><span data-stu-id="3aab8-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="3aab8-168">您可以使用 [記事本] toosave ansi。</span><span class="sxs-lookup"><span data-stu-id="3aab8-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="3aab8-169">上傳這個檔案 toohello 輸出資產的步驟 1 中。</span><span class="sxs-lookup"><span data-stu-id="3aab8-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="3aab8-170">上傳 hello 原始視訊 toothis 資產也，並將設定為主要的資產。</span><span class="sxs-lookup"><span data-stu-id="3aab8-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="3aab8-171">這項 「 Redact 」 模式 tooget hello 最終經過校訂視訊資產上執行 Redaction 工作。</span><span class="sxs-lookup"><span data-stu-id="3aab8-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3aab8-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3aab8-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3aab8-173">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3aab8-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="3aab8-174">相關連結</span><span class="sxs-lookup"><span data-stu-id="3aab8-174">Related links</span></span>
[<span data-ttu-id="3aab8-175">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="3aab8-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="3aab8-176">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="3aab8-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="3aab8-177">宣布推出適用於 Azure 媒體分析的臉部修訂功能</span><span class="sxs-lookup"><span data-stu-id="3aab8-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
