---
title: "aaa 管理速度和並行的編碼方式，透過 Azure Media Services |Microsoft 文件"
description: "本文提供如何使用 Azure 媒體服務管理編碼作業/工作之速度和並行的簡短概觀。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>管理編碼的速度和並行

本文提供如何管理編碼作業/工作之速度和並行的簡短概觀。

## <a name="overview"></a>概觀

在 Media Services**保留單位類型**決定 hello 與媒體處理工作會處理的速度。 您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。 例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。 hello[調整編碼單元](media-services-scale-media-processing-overview.md)主題說明可協助您做出決策選擇不同的編碼速度時的資料表。

此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您帳戶的**保留單位**。 hello 佈建的保留單元數目決定 hello 可以指定帳戶中並行處理的媒體工作數目。 例如，如果您的帳戶有五個媒體工作將會執行同時只要 5 個保留的單位，為有工作 toobe 處理。 hello 其餘的工作會在 hello 佇列中等候，而且會取得收取正在執行的工作完成時，依序處理。 如果帳戶未佈建任何保留單元，則會循序地挑選工作。 在此情況下，hello 之間的等候時間一個工作完成並 hello 一開始會相依於資源的 hello 可用性 hello 系統中。

詳細的資訊和範例，顯示如何 tooscale 編碼單元，請參閱[這](media-services-scale-media-processing-overview.md)主題。

## <a name="next-step"></a>後續步驟

[調整編碼單位](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

