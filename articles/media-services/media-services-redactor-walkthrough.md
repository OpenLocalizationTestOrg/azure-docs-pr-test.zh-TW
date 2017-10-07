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
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>使用 Azure 媒體分析修訂臉部逐步解說

## <a name="overview"></a>概觀

**Azure 媒體 Redactor**是[Azure 媒體分析](media-services-analytics-overview.md)提供可擴充的字體 redaction hello 雲端中的媒體處理器 (MP)。 字體 redaction 可讓您 toomodify 順序 tooblur 表面選取個人視訊。 您可以在公用的安全性和新聞媒體案例 toouse hello 朝 redaction 服務。 幾分鐘的影片，其中包含多個字型都會小時 tooredact 以手動方式，但具有此服務的 hello 圖示 redaction 程序將需要幾個簡單的步驟。 如需詳細資訊，請參閱[此](https://azure.microsoft.com/blog/azure-media-redactor/)部落格。

如需詳細資訊**Azure 媒體 Redactor**，請參閱 hello[朝 redaction 概觀](media-services-face-redaction.md)主題。

本主題說明如何逐步解說指示 toorun 使用 Azure 媒體服務總管 (AMSE) 和 Azure 媒體 Redactor 視覺化檢視 （開放原始碼工具） 的完整 redaction 工作流程。

hello **Azure 媒體 Redactor** MP 目前為預覽狀態。 在所有公開的 Azure 區域及美國政府和中國的數據中心皆有提供。 此預覽版本目前以免費方式提供。 在 hello 目前版本中，沒有 10 分鐘限制處理視訊的長度。

如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) 。

## <a name="azure-media-services-explorer-workflow"></a>Azure 媒體服務總管工作流程

hello 最簡單的方式 tooget 入門 Redactor 是 toouse hello 開放原始碼 github 上的 AMSE 工具。 您可以執行簡單的工作流程，經由**結合**模式，如果您不需要存取 toohello 註釋 json 或 hello 朝 jpg 影像。

### <a name="download-and-setup"></a>下載及安裝

1. 下載 hello AMSE 工具從[這裡](https://github.com/Azure/Azure-Media-Services-Explorer)。
1. 登入 tooyour Media Services 帳戶使用您的服務金鑰。

    tooobtain hello 帳戶名稱和金鑰資訊，請移 toohello [Azure 入口網站](https://portal.azure.com/)選取 AMS 帳戶。 選取 [Settings] \(設定) > [Keys] \(金鑰)。 hello 管理金鑰 windows 顯示 hello 帳戶名稱，並顯示 hello 主要和次要金鑰。 將複製 hello 帳戶名稱和 hello 主索引鍵的值。

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>第一階段 – 分析模式

1. 透過 [Asset] \(資產) –> [Upload] \(上傳) 或以拖放方式上傳您的媒體檔案。 
1. 按一下滑鼠右鍵，使用 [Media Analytics] \(媒體分析) –> [Azure Media Redactor] \(Azure 媒體修訂器) –> [Analyze mode] \(分析模式) 處理您的媒體檔案。 


![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

hello 輸出將包括字體位置資料，使用的註解 json 檔案，以及每個偵測到的字體的 jpg。 

![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>第二階段 – 修訂模式

1. 上傳您原始視訊資產 toohello 來自 hello 第一次傳遞的輸出，並將設為主要的資產。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. （選擇性）上傳包含 hello 想 tooredact Id 的新行字元分隔清單的 'Dance_idlist.txt' 檔案。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. （選擇性）將任何編輯 toohello annotations.json 檔案例如增加 hello 週框方塊的界限。 
4. 以滑鼠右鍵按一下從 hello 第一次傳遞 hello 輸出資產、 選取 hello Redactor，並執行以 hello **Redact**模式。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. 下載或共用 hello 最終經過校訂輸出資產。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Azure 媒體修訂器視覺化檢視開放原始碼工具

開放原始碼[視覺化檢視工具](https://github.com/Microsoft/azure-media-redactor-visualizer)是剛開始使用剖析和 hello 輸出 hello 註解格式的設計的 toohelp 開發人員。

您複製 hello 儲存機制，在訂單 toorun hello 專案中之後, 您將需要 toodownload FFMPEG 從其[官方網站](https://ffmpeg.org/download.html)。

如果您是開發人員嘗試 tooparse hello JSON 註解資料，尋找內部 Models.MetaData 範例程式碼範例。

### <a name="set-up-hello-tool"></a>設定 hello 工具

1.  下載並建置 hello 整個方案。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  從[這裡](https://ffmpeg.org/download.html)下載 FFMPEG。 此專案原先是使用含靜態連結的版本 be1d324 (2016-10-04) 所開發。 
3.  複製 ffmpeg.exe 和 ffprobe.exe toohello AzureMediaRedactor.exe 與相同的輸出資料夾。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. 執行 AzureMediaRedactor.exe。 

### <a name="use-hello-tool"></a>使用 hello 工具

1. 處理您在 Azure Media Services 帳戶以 hello Redactor 管理組件中進行分析 模式中的視訊。 
2. 下載 hello 原始視訊檔和 hello Redaction hello 輸出-分析工作。 
3. 執行 hello 視覺化檢視應用程式並選擇上述 hello 檔案。 

    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. 預覽檔案。 選取以您想要透過 hello [資訊看板] 上 hello tooblur 右。 
    
    ![臉部修訂](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  hello 朝識別碼將會更新 hello 下文字欄位。 建立名為 "idlist.txt" 的檔案，其中包含這些識別碼清單 (以新行分隔)。 

    >[!NOTE]
    > hello idlist.txt 應該儲存在 ANSI。 您可以使用 [記事本] toosave ansi。
    
6.  上傳這個檔案 toohello 輸出資產的步驟 1 中。 上傳 hello 原始視訊 toothis 資產也，並將設定為主要的資產。 
7.  這項 「 Redact 」 模式 tooget hello 最終經過校訂視訊資產上執行 Redaction 工作。 

## <a name="next-steps"></a>後續步驟 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[宣布推出適用於 Azure 媒體分析的臉部修訂功能](https://azure.microsoft.com/blog/azure-media-redactor/)
