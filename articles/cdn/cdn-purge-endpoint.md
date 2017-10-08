---
title: "aaaPurge Azure CDN 端點 |Microsoft 文件"
description: "了解如何 toopurge 所有快取來自 Azure CDN 端點的內容。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>清除 Azure CDN 端點
## <a name="overview"></a>概觀
Azure CDN 邊緣節點會快取資產，直到過期 hello 資產的存留時間 (TTL)。  Hello 資產的 TTL 到期，用戶端要求來自 hello 邊緣節點的 hello 資產之後，會擷取已更新的全新的 hello 資產 tooserve hello 用戶端要求 hello 邊緣節點，並將其重新整理 hello 快取儲存。

hello 最佳作法 toomake 確定您的使用者永遠取得 hello 您資產的最新的複本是的 tooversion 更新每個資產，並將其發行為新的 Url。  CDN 將會立即擷取 hello hello 下一個用戶端要求新的資產。  有時候您可能希望 toopurge 快取來自所有邊緣節點的內容，強制其所有 tooretrieve 新更新的資產。  這可能是由於 tooupdates tooyour web 應用程式或包含不正確的資訊的 tooquickly 更新資產。

> [!TIP]
> 請注意，只清除清除 hello 快取 hello CDN 邊緣伺服器的內容。  任何下游快取 proxy 伺服器和本機瀏覽器快取中，例如可能仍會保留 hello 檔案的快取的副本。  它是重要的 tooremember 這樣當您將設定檔的存留時間。  您可以強制下游的用戶端 toorequest hello 最新版本的檔案，為它指定唯一的名稱，每次您更新，或藉由運用[查詢字串快取](cdn-query-string.md)。  
> 
> 

本教學會逐步引導您清除端點的所有邊緣節點的資產。

## <a name="walkthrough"></a>逐步介紹
1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello CDN 設定檔包含您想 toopurge hello 端點。
2. 從 hello CDN 設定檔刀鋒視窗中，按一下 hello 清除 按鈕。
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    hello 清除刀鋒視窗隨即開啟。
   
    ![CDN 清除刀鋒視窗](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Hello 上清除刀鋒視窗中，選取您想 toopurge 從 hello URL 下拉式清單中的 hello 服務位址。
   
    ![清除表單](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > 您也可以取得 toohello 清除刀鋒視窗中，依序按一下 hello**清除**hello CDN 端點刀鋒視窗上的按鈕。  在此情況下，hello **URL**欄位會預先填入該特定端點 hello 服務位址。
   > 
   > 
4. 選取的資產您想從 hello toopurge 邊緣節點。  如果您想 tooclear 所有資產，按一下 hello **全部清除**核取方塊。  否則，每個資產的型別 hello 路徑想 toopurge 在 hello**路徑**文字方塊。 下面格式支援 hello 路徑中。
    1. **單一 URL 清除**: hello 副檔名，例如，含指定 hello 完整的 URL，來清除個別資產`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **萬用字元清除**︰星號 (\*) 可作為萬用字元。 清除所有資料夾、 子資料夾和檔案底下的端點`/*`hello 路徑或都清除所有的子資料夾和特定資料夾下的檔案，藉由指定後面的 hello 資料夾`/*`，例如，`/pictures/*`。  請注意，來自 Akamai 的 Azure CDN 目前不支援萬用字元清除。 
    3. **根網域清除**: hello 端點以"/"hello 路徑中的清除 hello 根。
   
   > [!TIP]
   > 路徑必須指定清除，而且必須是相對的 URL 納入 hello 下列[規則運算式](https://msdn.microsoft.com/library/az24scfc.aspx)。 **來自 Akamai 的 Azure CDN** 目前不支援**全部清除**和**萬用字元清除**。
   > > 單一 URL 清除 `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > 查詢字串 `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > 萬用字元清除 `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`。 
   > 
   > 多個**路徑**文字方塊會出現在輸入文字 tooallow 之後 toobuild 多個資產的清單。  您可以在 hello 省略符號 （...） 按鈕，即可從 hello 清單刪除資產。
   > 
5. 按一下 hello**清除** 按鈕。
   
    ![清除按鈕](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> 清除要求需要大約 2-3 分鐘 tooprocess 與**Verizon 從 Azure CDN** （Standard 和 Premium） 和大約 7 分鐘與**Akamai 從 Azure CDN**。  Azure CDN 隨時都有 50 個並行清除要求的限制。 
> 
> 

## <a name="see-also"></a>另請參閱
* [在 Azure CDN 端點上預先載入資產](cdn-preload-endpoint.md)
* [Azure CDN REST API 參考資料 - 清除或預先載入端點](https://msdn.microsoft.com/library/mt634451.aspx)

