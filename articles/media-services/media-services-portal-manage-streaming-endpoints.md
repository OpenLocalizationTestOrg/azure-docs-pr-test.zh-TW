---
title: "aaaManage 串流端點，其中包含 hello Azure 入口網站 |Microsoft 文件"
description: "本主題說明如何 toomanage 串流端點，其中包含 hello Azure 入口網站。"
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>管理以 hello Azure 入口網站的串流端點

本主題說明如何 toouse hello Azure 入口網站 toomanage 串流端點。 

>[!NOTE]
>請確定 tooreview hello[概觀](media-services-streaming-endpoints-overview.md)主題。 

如需如何 tooscale hello 串流端點資訊，請參閱[這](media-services-portal-scale-streaming-endpoints.md)主題。

## <a name="start-managing-streaming-endpoints"></a>開始管理串流端點 

管理您的帳戶，串流端點 toostart hello 遵循。

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 hello**設定**刀鋒視窗中，選取**串流端點**。
   
    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> 只有當串流端點處於執行中狀態時，才會向您收取費用。

## <a name="adddelete-a-streaming-endpoint"></a>新增/移除串流端點

>[!NOTE]
>無法刪除 hello 預設串流端點。

tooadd/刪除串流端點使用 hello Azure 入口網站中，執行下列 hello:

1. tooadd 串流端點中，按一下 hello **+ 端點**hello 頁面頂端的 hello。 

    您可能會想多個串流端點，如果您計劃 toohave 不同 Cdn 或 CDN 和直接存取。

2. toodelete 串流端點，請按**刪除** 按鈕。      
3. 按一下 hello**啟動**按鈕 toostart hello 串流端點。
   
    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>設定 hello 串流端點
串流端點可讓您 tooconfigure hello 下列屬性：

* 存取控制
* 快取控制
* 跨站台存取原則

如需這些屬性的詳細資訊，請參閱 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。

您可以設定串流端點，藉由下列 hello:

1. 選取串流端點想 tooconfigure hello。
2. 按一下 [設定] 。

遵循 hello 欄位的簡短描述。

![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. 最大快取原則： 使用的 tooconfigure 資產的快取生命週期服務透過此串流端點。 如果未不設定任何值，則會使用 hello 預設值。 hello 預設值也可以直接在 Azure 儲存體中定義。 Hello 串流端點啟用 Azure CDN，如果您不應將 hello 快取原則值 tooless 比 600 秒。  
2. 允許的 IP 位址： 使用 toospecify tooconnect toohello 發佈串流端點允許的 IP 位址。 如果沒有指定的 IP 位址，任何 IP 位址是無法 tooconnect。 IP 位址可以指定為單一 IP 位址 (例如 ‘10.0.0.1’)、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如 ‘10.0.0.1/22’)，或是使用 IP 位址和小數點十進位子網路遮罩的 IP 範圍 (例如 ‘10.0.0.1(255.255.255.0)’)。
3. Akamai 簽章標頭驗證設定： 使用的 toospecify 設定來自 Akamai 伺服器的簽章標頭驗證要求的方式。 到期時間的格式為 UTC。

## <a name="scale-your-premium-streaming-endpoint"></a>調整您的進階串流端點

如需詳細資訊，請參閱 [這個](media-services-portal-scale-streaming-endpoints.md) 主題。

## <a id="enable_cdn"></a>啟用 Azure CDN 整合

當您建立新的帳戶時，依預設會啟用預設串流端點 Azure CDN 整合。

如果您稍後想 toodisable/啟用 hello CDN，您的串流端點必須在 hello**停止**狀態。 可能需要跨所有 hello CDN 快顯 hello Azure CDN 整合 tooget 啟用和使用中的 hello 變更 toobe too2 小時。 不過，您可以從串流端點的 hello 啟動串流端點和且不被中斷的資料流和 hello 整合完成之後，直接從 hello CDN 傳送嗨資料流。 在佈建期間 hello 期間您的串流端點將處於**啟動**狀態，而且您可能會發現 degredad 效能。

所有 hello Azure 資料中心 execpt 中國和美國聯邦公文區域中，會啟用 CDN 整合。

一旦啟用後，hello**存取控制**，**自訂主機名稱**和**Akamai 簽章驗證**組態取得停用。
 
> [!IMPORTANT]
> 如果是標準串流端點，Azure 媒體服務與 Azure CDN 的整合是在**來自 Verizon 的 Azure CDN** 上實作。 您可以使用所有 **Azure CDN 定價層和提供者**來設定進階串流端點。 如需有關 Azure CDN 功能的詳細資訊，請參閱 hello [CDN 概觀](../cdn/cdn-overview.md)。
 
### <a name="additional-considerations"></a>其他考量

* 為串流端點啟用 CDN 時，用戶端無法直接從 hello 原始要求內容。 如果您需要 hello 能力 tootest 您不論 CDN 的內容，您可以建立另一個未啟用 CDN 的串流端點。
* 您的串流端點主機名稱維持 hello 相同啟用 CDN 之後。 啟用 CDN 之後您不需要指定 toomake 任何變更 tooyour 媒體服務工作流程。 例如，如果您的串流端點主機名稱是 strasbourg.streaming.mediaservices.windows.net，啟用 CDN 之後，會使用 hello 完全相同的主機名稱。
* 針對新的資料流端點，您可以啟用 CDN 只是藉由建立新的端點。針對現有的資料流端點，您需要 toofirst 停止 hello 端點，然後啟用/停用 hello CDN。
* 只有透過 Azure 管理入口網站使用 **Verizon 標準 CDN 提供者**，才能設定標準串流端點。 不過，您可以使用 REST API 來啟用其他 Azure CDN 提供者。

## <a name="configure-cdn-profile"></a>設定 CDN 設定檔

您可以設定 hello 的 CDN 設定檔選取 hello**管理 CDN**從 hello 上方的按鈕。

![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

