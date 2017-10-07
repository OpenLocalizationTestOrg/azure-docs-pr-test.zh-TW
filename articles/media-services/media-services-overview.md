---
title: "aaaAzure Media Services 概觀 |Microsoft 文件"
description: "本主題提供 Azure 媒體服務的概觀"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Azure 媒體服務概觀 

Microsoft Azure Media Services 是可擴充雲端為基礎的平台，可讓開發人員 toobuild 可擴充媒體管理和傳遞應用程式。 Media Services 為基礎的 REST Api 可讓您 toosecurely 上傳、 儲存、 編碼，和封裝視訊或音訊內容的隨選及即時串流傳遞 toovarious 用戶端 （例如，電視、 PC 和行動裝置）。

您可以建置完全採用媒體服務的端對端工作流程。 您也可以選擇 toouse 協力廠商元件工作流程的某些部分。 例如，使用第三方編碼器來進行編碼； 然後使用媒體服務上傳、保護、封裝、傳遞。

您可以選擇 toostream 即時內容，或提供點播內容。 hello 主題也會連結 tooother 相關主題。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
您可以在此檢視 AMS 學習路徑：

* [AMS 即時資料流工作流程](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [AMS 隨選串流工作流程](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>必要條件

toostart 使用 Azure Media Services 中，您應該有下列 hello:

* 一個 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com)。
* Azure 媒體服務帳戶。 如需詳細資訊，請參閱[建立帳戶](media-services-portal-create-account.md)。
* (選擇性) 設定開發環境。 針對開發環境選擇 .NET 或 REST API。 如需詳細資訊，請參閱 [設定環境](media-services-dotnet-how-to-use.md)。

    此外，了解如何太[以程式設計方式連接 tooAMS API](media-services-use-aad-auth-to-access-ams-api.md)。
* 已啟動狀態的標準或進階串流端點。  如需詳細資訊，請參閱[管理串流端點](media-services-portal-manage-streaming-endpoints.md)

## <a name="sdks-and-tools"></a>SDK 及工具

toobuild Media Services 解決方案，您可以使用：

* [媒體服務 REST API](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* 其中一個 hello 可用的用戶端 Sdk:
    * [Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services)、
    * [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java)、
    * [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)、
    * [Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (這是非 Microsoft 版本的 Node.js SDK。 它由社群維護並目前並沒有 100%的涵蓋範圍 hello AMS 應用程式開發介面）。
* 現有的工具：
    * [Azure 入口網站](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure 媒體服務總管 (AMSE) 是適用於 Windows 的 Winforms/C# 應用程式)

## <a name="concepts-and-overview"></a>概念和概觀
如需 Azure 媒體服務概念，請參閱 [概念](media-services-concepts.md)。

如何為 tooseries 介紹 Azure Media services tooall hello 主要元件，請參閱[Azure 媒體服務的逐步教學課程](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series)。 此序列有很棒的概念概觀，並使用 hello AMSE 工具 toodemonstrate AMS 工作。 AMSE 工具是一種 Windows 工具。 這項工具支援大部分的 hello 工作，可讓您以程式設計的方式與[AMS SDK for.NET](https://github.com/Azure/azure-sdk-for-media-services)， [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java)，或[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)。

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>跨資料中心支援的媒體服務情節和可用性

如需詳細資訊，請參閱[跨資料中心的 AMS 功能和服務情節和可用性](scenarios-and-availability.md)。

## <a name="service-level-agreement-sla"></a>服務等級協定 (SLA)

* 對於媒體服務編碼，我們保證 REST API 交易可用性高達 99.9%。
* 對於串流，我們在購買一個標準或近界串流端點時，針對現有的媒體內容，可保證以 99.9% 的可用性成功服務要求。
* 即時通道，我們保證，執行通道將會具有外部連線能力至少 99.9%的 hello 時間。
* 內容保護，我們保證，我們將會成功地滿足金鑰要求至少 99.9%的 hello 時間。
* 索引子，我們將會成功服務索引子工作要求處理編碼保留單元 99.9%的 hello 時間。

如需詳細資訊，請參閱 [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/)。

如需在資料中心內的可用性資訊，請參閱 hello [Avaiability](scenarios-and-availability.md#availability) > 一節。

## <a name="support"></a>支援

[Azure 支援](https://azure.microsoft.com/support/options/) 提供 Azure 的支援選項，包括媒體服務。

## <a name="provide-feedback"></a>提供意見反應

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
