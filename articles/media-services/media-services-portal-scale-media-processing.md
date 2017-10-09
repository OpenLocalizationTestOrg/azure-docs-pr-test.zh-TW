---
title: "處理使用 aaaScale 媒體 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您完成處理使用 hello Azure 入口網站的調整 media hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>變更 hello 保留單位類型
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [入口網站](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>概觀

Media Services 帳戶會決定 hello 速度與媒體處理工作會處理保留單位類型相關聯。 您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。 例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。

此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您帳戶的**保留單位**(RUs)。 佈建之俄文的 hello 數目會決定 hello 可以指定帳戶中並行處理的媒體工作數目。

>[!NOTE]
>RU 用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引作業。 不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。

> [!IMPORTANT]
> 請確定 tooreview hello[概觀](media-services-scale-media-processing-overview.md)主題 tooget 調整媒體處理主題的詳細資訊。
> 
> 

## <a name="scale-media-processing"></a>調整媒體處理
toochange hello 保留單位類型和 hello 保留單位數目，請勿 hello 遵循：

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 hello**設定**視窗中，選取**媒體保留單位**。
   
    hello 的保留單元 toochange hello 數目選取保留的單位類型，請使用 hello**媒體服務單位**滑桿。
   
    toochange hello**保留單位類型**，請按 S1、 S2 或 S3。
   
    ![Processors page](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. 按 hello 儲存按鈕 toosave 您的變更。
   
    當您按下 儲存配置 hello 新保留的單位。

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

