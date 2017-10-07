---
title: "開始使用 Azure CDN 的 aaaGetting |Microsoft 文件"
description: "本主題說明如何 tooenable hello Azure 內容傳遞網路 (CDN)。 hello 教學課程引導 hello 建立新的 CDN 設定檔和端點。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>開始使用 Azure CDN
本主題將逐步解說如何透過建立新的 CDN 設定檔和端點來啟用 Azure CDN。

> [!IMPORTANT]
> 如簡介 toohow CDN 如何運作，以及的功能清單，請參閱 hello [CDN 概觀](cdn-overview.md)。
> 
> 

## <a name="create-a-new-cdn-profile"></a>建立新的 CDN 設定檔
CDN 設定檔就是 CDN 端點的集合。  每個設定檔皆包含一或多個 CDN 端點。  您可能希望 toouse 多個設定檔 tooorganize 您的 CDN 端點的網際網路網域、 web 應用程式，或其他一些準則。

> [!NOTE]
> 根據預設，單一 Azure 訂用帳戶是有限的 tooeight CDN 設定檔。 每個 CDN 設定檔是有限的 tooten CDN 端點。
> 
> CDN 定價為套用於 hello CDN 設定檔層級。 如果您想 toouse 混合 Azure CDN 的定價層，您需要多個的 CDN 設定檔。
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>建立新的 CDN 端點
**toocreate 新的 CDN 端點**

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。  您可能已釘選它 toohello 儀表板 hello 上一個步驟中。  如果您不是，您可以找到它，即可**瀏覽**，然後**CDN 設定檔**，而且 hello 設定檔上按一下您想 tooadd 至您的端點。
   
    hello CDN 設定檔 刀鋒視窗隨即出現。
   
    ![CDN 設定檔][cdn-profile-settings]
2. 按一下 hello**加入端點** 按鈕。
   
    ![[加入端點] 按鈕][cdn-new-endpoint-button]
   
    hello**將端點加入**刀鋒視窗隨即出現。
   
    ![[加入端點] 刀鋒視窗][cdn-add-endpoint]
3. 輸入這個 CDN 端點的 [名稱]  。  此名稱將會使用的 tooaccess hello 網域您快取的資源`<endpointname>.azureedge.net`。
4. 在 hello**來源類型**下拉式清單中，選取您的來源類型。  針對 Azure 儲存體帳戶選取 [儲存體]、針對 Azure 雲端服務選取 [雲端服務]、針對 Azure Web 應用程式選取 [Web 應用程式]，若為其他任何可公開存取的 Web 伺服器來源 (裝載於 Azure 或其他位置)，則請選取 [自訂原始來源]。
   
    ![CDN 原始來源類型](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. 在 hello**來源主機名稱**下拉式清單中，選取或輸入您原始網域。  hello 下拉式清單中會列出所有可用的來源，您指定在步驟 4 中的 hello 型別。  如果您選取*自訂來源*做為您**來源類型**，您會輸入 hello 您自訂的原始網域。
6. 在 hello**原始路徑**文字方塊中，輸入您想要 toocache 或保持空白 tooallow 快取任何資源，您在步驟 5 中指定的 hello 網域 hello 路徑 toohello 資源。
7. 在 hello**原始主機標頭**，輸入您想要 hello 與每個要求，CDN toosend hello 主機標頭，或保留預設值，hello。
   
   > [!WARNING]
   > 原始來源，例如 Azure 儲存體和 Web 應用程式，某些類型需要 hello 主機標頭 toomatch hello hello 原始網域。 除非您需要從其網域不同的主機標頭的原始主機，您應該保留 hello 預設值。
   > 
   > 
8. 如**通訊協定**和**來源連接埠**、 指定 hello 通訊協定和連接埠使用的 tooaccess hello 原點在您的資源。  至少必須選取一個通訊協定 (HTTP 或 HTTPS)。
   
   > [!NOTE]
   > hello**來源連接埠**只會影響哪些連接埠 hello 端點會使用從 hello 原點 tooretrieve 資訊。  hello 本身的端點才會使用 tooend 用戶端 hello 預設 HTTP 和 HTTPS 連接埠 （80 和 443），不論 hello**來源連接埠**。  
   > 
   > **Azure CDN 從 Akamai**端點不允許 hello 完整 TCP 連接埠範圍的來源。  如需不允許的原始連接埠清單，請參閱 [來自 Akamai 的 Azure CDN 允許的原始連接埠](https://msdn.microsoft.com/library/mt757337.aspx)。  
   > 
   > 內容使用 HTTPS 存取 CDN 有下列條件約束的 hello:
   > 
   > * 您必須使用 hello hello CDN 所提供的 SSL 憑證。 不支援第三方憑證。
   > * 您必須使用 hello 提供 CDN 網域 (`<endpointname>.azureedge.net`) tooaccess HTTPS 內容。 HTTPS 支援不適用於自訂網域名稱 (Cname) 因為 hello CDN 目前不支援自訂憑證。
   > 
   > 
9. 按一下 hello**新增**按鈕 toocreate hello 新端點。
10. 一旦建立 hello 端點時，它會出現在 hello 設定檔的端點清單。 hello 清單檢視會顯示 hello URL toouse tooaccess 快取內容，以及 hello 原始網域。
    
    ![CDN 端點][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > hello 端點將不立即可供使用，因為它需要花費一些時間透過 hello CDN hello 註冊 toopropagate。  在 [通訊協定] <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。  若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。
    > 
    > 再試一次 toouse hello CDN 網域名稱之前傳播到 toohello 快顯 hello 端點組態的使用者會收到 HTTP 404 回應碼。  如果在端點建立好後已過了好幾個小時，而您仍然收到 404 回應，請參閱 [針對傳回 404 狀態的 CDN 端點進行疑難排解](cdn-troubleshoot-endpoint.md)。
    > 
    > 

## <a name="see-also"></a>另請參閱
* [使用查詢字串控制 CDN 要求的快取行為](cdn-query-string.md)
* [如何 tooMap CDN 內容 tooa 自訂網域](cdn-map-content-to-custom-domain.md)
* [在 Azure CDN 端點上預先載入資產](cdn-preload-endpoint.md)
* [清除 Azure CDN 端點](cdn-purge-endpoint.md)
* [針對傳回 404 狀態的 CDN 端點進行疑難排解](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
