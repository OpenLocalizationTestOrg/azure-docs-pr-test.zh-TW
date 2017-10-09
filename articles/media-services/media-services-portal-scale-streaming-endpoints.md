---
title: "aaaScale 串流端點，其中包含 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您 hello 步驟調整串流端點，其中包含 hello Azure 入口網站。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a>調整串流端點，其中包含 hello Azure 入口網站
## <a name="overview"></a>概觀

> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
> 
> 

**進階**串流端點適合進階工作，提供專用並能靈活調整的頻寬容量。 擁有**進階**串流端點的客戶預設會取得一個串流單位 (SU)。 可以藉由新增 SUs 調整串流端點的 hello。 每個 SU 提供額外的頻寬容量 toohello 應用程式。 如需有關資料流端點類型及 CDN 組態的詳細資訊，請參閱 hello[串流端點概觀](media-services-portal-manage-streaming-endpoints.md)主題。
 
本主題說明如何 tooscale 串流端點。

如需定價詳細資料的相關資訊，請參閱＜ [媒體服務定價詳細資料](http://go.microsoft.com/fwlink/?LinkId=275107)＞。

## <a name="scale-streaming-endpoints"></a>調整串流端點

資料流處理單位，toochange hello 數目不要 hello 遵循：

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 hello**設定**視窗中，選取**串流端點**。
3. 按一下您想 tooscale hello 串流端點。 

    [!NOTE] 您只能調整 [Premium] \(進階\) 串流端點。

4. 移動 hello 滑桿 toospecify hello 資料流單位數目。

    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

