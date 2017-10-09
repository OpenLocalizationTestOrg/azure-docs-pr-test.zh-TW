---
title: "藉由加入編碼單位-Azure 處理 aaaScale 媒體 | Microsoft 文件"
description: "深入了解如何搭配.NET toohow tooadd 編碼單元"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>如何使用.NET SDK 編碼 tooscale
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>概觀
> [!IMPORTANT]
> 請確定 tooreview hello[概觀](media-services-scale-media-processing-overview.md)主題 tooget 調整媒體處理主題的詳細資訊。
> 
> 

toochange hello 保留單位類型及 hello 數目編碼保留的單位使用.NET SDK hello 遵循：

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>建立支援票證
根據預設，每個 Media Services 帳戶可以調整 tooup too25 編碼和 5 個隨選串流保留單元。 您可以建立支援票證來要求更高的限制。

### <a name="open-a-support-ticket"></a>開啟支援票證
請勿 hello tooopen 支援票證，遵循：

1. 按一下 [取得支援](https://manage.windowsazure.com/?getsupport=true)。 如果您未登入，您將會提示的 tooenter 您的認證。
2. 選取您的訂用帳戶。
3. 在支援類型下，選取 [技術]。
4. 按一下 [建立票證]。
5. 選取 Azure Media Services"hello 產品清單中顯示 hello 下一個頁面。
6. 選取適合您的問題的 [問題類型]。
7. 按一下 [繼續]。
8. 遵循下一頁的指示，然後輸入問題的詳細資訊。
9. 按一下 提交 tooopen hello 票證。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

