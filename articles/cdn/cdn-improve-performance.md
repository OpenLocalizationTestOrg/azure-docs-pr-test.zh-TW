---
title: "壓縮檔案，在 Azure CDN aaaImprove 效能 |Microsoft 文件"
description: "了解 tooimprove 檔案壓縮 Azure CDN 中的檔案所傳輸的速度以及增加負載效能。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>在 Azure CDN 中壓縮檔案以改善效能
壓縮是簡單且有效的方法 tooimprove 檔案傳輸速度以及增加網頁載入效能，藉由減少檔案大小之前從傳送 hello 伺服器。 它會降低頻寬成本，並提供回應速度更快的體驗給使用者。

有兩種方式 tooenable 壓縮：

* 在此情況下 hello CDN 通過 hello 壓縮的檔案和傳遞要求的壓縮的檔 tooclients，您可以在您的原始伺服器上啟用壓縮。
* 您可以啟用壓縮，直接在 CDN 邊緣伺服器案例的 hello CDN 壓縮 hello 檔案並提供服務給其 tooend 使用者，即使它們不會壓縮 hello 原始伺服器上。

> [!IMPORTANT]
> CDN 設定變更都會透過 hello 網路某些時間 toopropagate。  若為 <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。  若為 <b>來自 Verizon 的 Azure CDN</b> 設定檔，您通常會在 90 分鐘之內看到變更套用。  如果這是 hello 您為您的 CDN 端點設定壓縮的第一次，您應該考慮等候 1-2 小時 toobe 確定 hello 壓縮設定都已傳播 toohello 快顯的疑難排解
> 
> 

## <a name="enabling-compression"></a>啟用壓縮
> [!NOTE]
> hello Standard 和 Premium CDN 層提供 hello 相同的壓縮功能，但是 hello 使用者介面有所不同。  如需 hello Standard 和 Premium CDN 的各層之間的差異的詳細資訊，請參閱[Azure CDN 概觀](cdn-overview.md)。
> 
> 

### <a name="standard-tier"></a>標準層
> [!NOTE]
> 本章節適用於太**Azure CDN 標準從 Verizon**和**Azure 標準 Akamai CDN**設定檔。
> 
> 

1. 從 hello CDN 設定檔 頁面上，按一下您想 toomanage hello CDN 端點。
   
    ![[CDN 設定檔] 頁面端點](./media/cdn-file-compression/cdn-endpoints.png)
   
    hello CDN 端點頁面隨即開啟。
2. 按一下 hello**設定** 按鈕。
   
    ![[CDN 設定檔] 頁面的 [管理] 按鈕](./media/cdn-file-compression/cdn-config-btn.png)
   
    hello CDN 組態 頁面隨即開啟。
3. 開啟 [ **壓縮**]。
   
    ![CDN 壓縮的選項](./media/cdn-file-compression/cdn-compress-standard.png)
4. 使用 hello 預設類型，或修改 hello 清單移除或新增檔案類型。
   
   > [!TIP]
   > While 可行的建議您不要 tooapply 壓縮 toocompressed 格式，例如 ZIP、 MP3、 MP4、 JPG 等等。
   > 
   > 
5. 在您的變更後，按一下 [hello**儲存**] 按鈕。

### <a name="premium-tier"></a>高階層
> [!NOTE]
> 本章節適用於太**Verizon 從 Azure CDN Premium**設定檔。
> 
> 

1. 從 hello CDN 設定檔 頁面上，按一下 hello**管理** 按鈕。
   
    ![[CDN 設定檔] 頁面的 [管理] 按鈕](./media/cdn-file-compression/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 暫留在 hello **HTTP 大型** 索引標籤，然後暫留在 hello**快取設定**彈出式視窗。  按一下 [ **壓縮**]。

    ![檔案壓縮選項](./media/cdn-file-compression/cdn-compress-select.png)
   
    隨即顯示 [壓縮] 的選項。
   
    ![檔案壓縮](./media/cdn-file-compression/cdn-compress-files.png)
3. 啟用壓縮，依序按一下 hello**啟用壓縮**選項按鈕。  輸入 hello MIME 型別想成以逗號分隔清單 （無空格） 在 hello toocompress**檔案類型**文字方塊。
   
   > [!TIP]
   > While 可行的建議您不要 tooapply 壓縮 toocompressed 格式，例如 ZIP、 MP3、 MP4、 JPG 等等。 
   > 
   > 
4. 在您的變更後，按一下 [hello**更新**] 按鈕。

## <a name="compression-rules"></a>壓縮規則
這些資料表描述每個案例的 Azure CDN 壓縮行為。

> [!IMPORTANT]
> 若為 **來自 Verizon 的 Azure CDN** (標準和進)，只會壓縮合格的檔案。  toobe 能夠壓縮，檔案必須：
> 
> * 超過 128 個位元組。
> * 小於 1 MB。
> 
> 若為 **來自 Akamai 的 Azure CDN**，所有檔案都符合壓縮資格。
> 
> 對於所有的 Azure CDN 產品，檔案必須為已 [設定壓縮](#enabling-compression)的 MIME 類型。
> 
> **來自 Verizon 的 Azure CDN** 設定檔 (標準和進階) 支援 **gzip** (GNU zip)、**deflate**、**bzip2** 或 **br** (Brotli) 編碼。 Brotli 編碼方式，是只在 hello 邊緣完成 hello 壓縮。 hello 用戶端瀏覽器必須傳送嗨要求 Brotli 編碼方式和 hello 壓縮的資產必須已壓縮 hello 原點端上第一次。 
>
>**來自 Akamai 的 Azure CDN** 設定檔只支援 **gzip** 編碼。
> 
> **Azure CDN 從 Akamai**端點永遠要求**gzip**編碼 hello 原點，不論 hello 用戶端要求中的檔案。 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>已停用壓縮或檔案不適合進行壓縮
| 用戶端要求的格式 (透過 Accept-encoding 標頭) | 快取的檔案格式 | CDN 回應 toohello 用戶端 | 注意事項 |
| --- | --- | --- | --- |
| 已壓縮 |已壓縮 |已壓縮 | |
| 已壓縮 |未壓縮 |未壓縮 | |
| 已壓縮 |不快取 |已壓縮或未壓縮 |取決於原始回應 |
| 未壓縮 |已壓縮 |未壓縮 | |
| 未壓縮 |未壓縮 |未壓縮 | |
| 未壓縮 |不快取 |未壓縮 | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>啟用壓縮和檔案適合進行壓縮
| 用戶端要求的格式 (透過 Accept-encoding 標頭) | 快取的檔案格式 | CDN 回應 toohello 用戶端 | 注意事項 |
| --- | --- | --- | --- |
| 已壓縮 |已壓縮 |已壓縮 |支援格式之間的 CDN 轉碼 |
| 已壓縮 |未壓縮 |已壓縮 |CDN 執行壓縮 |
| 已壓縮 |不快取 |已壓縮 |如果來源傳回未壓縮，則 CDN 會執行壓縮。  **Azure CDN 從 Verizon**傳遞 hello 上 hello 第一個要求，然後壓縮未壓縮的檔案和快取 hello 的後續要求的檔案。  具有 `Cache-Control: no-cache` 標頭的檔案永遠不會經過壓縮。 |
| 未壓縮 |已壓縮 |未壓縮 |CDN 執行解壓縮 |
| 未壓縮 |未壓縮 |未壓縮 | |
| 未壓縮 |不快取 |未壓縮 | |

## <a name="media-services-cdn-compression"></a>媒體服務 CDN 壓縮
依預設，下列內容類型的 hello Media Services CDN 啟用的串流端點，啟用壓縮： 應用程式/vnd.ms-sstr + xml、 application/dash+xml,application/vnd.apple.mpegurl、 應用程式/f4m + xml。 您無法啟用/停用壓縮 hello 提及使用 hello Azure 入口網站的類型。  

## <a name="see-also"></a>另請參閱
* [CDN 檔案壓縮疑難排解](cdn-troubleshoot-compression.md)    

