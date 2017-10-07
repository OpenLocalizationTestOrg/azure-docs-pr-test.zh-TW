---
title: "aaaEncode hello Azure 入口網站使用的媒體編碼器標準資產 |Microsoft 文件"
description: "本教學課程會引導您編碼資產 hello Azure 入口網站使用的媒體編碼器標準 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>編碼資產 hello Azure 入口網站使用標準的媒體編碼器
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
> 
> 

當使用 Azure Media Services hello 最常見的案例之一傳遞彈性位元速率串流 tooyour 用戶端。 Media Services 支援下列彈性位元速率串流技術的 hello: HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。 tooprepare 視訊彈性位元速率串流，您需要 tooencode 您的來源視訊多位元速率檔案。 您應該使用 hello**媒體編碼器標準**編碼器 tooencode 視訊。  

Media Services 也提供可讓您 toodeliver 動態封裝中遵循的串流格式 hello 您多位元速率 mp4 集： MPEG DASH、 HLS、 Smooth Streaming，不需要您 toore 封裝到這些資料流的格式。 使用動態封裝您只需要 toostore 及支付一種儲存格式，以及 Media Services 中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。

tootake 利用動態封裝，您需要 tooencode 原始程式檔成一組多位元速率 MP4 檔案 （hello 編碼步驟會示範稍後這一節）。

tooscale 媒體處理，請參閱[這](media-services-portal-scale-media-processing.md)主題。

## <a name="encode-with-hello-azure-portal"></a>編碼以 hello Azure 入口網站
本章節描述 hello 步驟可讓您 tooencode 媒體編碼器標準內容。

1. 在 [hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 [hello**設定**視窗中，選取**資產**。  
3. 在 [hello**資產**視窗中，您想要 tooencode 選取 hello 資產。
4. 按 hello**編碼**] 按鈕。
5. 在 [hello**編碼資產**視窗中選取 hello 「 媒體編碼器標準 」 的處理器，並預先設定。 如需預設值的相關資訊，請參閱[自動產生的位元速率排行榜](media-services-autogen-bitrate-ladder-with-mes.md)和 [MES 的工作預設值](media-services-mes-presets-overview.md)。 如果您打算使用的編碼預設 toocontrol，記住這： 請務必 tooselect hello 預先設定的最適合您輸入的視訊。 比方說，如果您知道輸入的視訊具有 1920 x 1080 像素的解析度，然後您可以使用 hello"H264 多重位元速率 1080p 」 預設。 如果您有低解析度 (640x360) 視訊，則不應該使用 [H264 多重位元速率 1080p] 預設值。
   
   為了方便管理，您必須編輯 hello 名稱 hello 輸出資產，以及 hello hello 作業名稱的選項。
   
   ![為資產編碼](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. 按下 [建立] 。

## <a name="next-step"></a>後續步驟
中所述，您可以監視以 hello Azure 入口網站的編碼工作進度[這](media-services-portal-check-job-progress.md)發行項。  

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

