---
title: "Azure CDN 端點上的 aaaPre 負載資產 |Microsoft 文件"
description: "了解如何 toopre 載入快取 Azure CDN 端點上的內容。"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>在 Azure CDN 端點上預先載入資產
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

根據預設，資產被要求時會先快取。 這表示 hello 從每個區域的第一個要求可能需要較長，因為不會有 hello 邊緣伺服器 hello 內容快取，而且必須 tooforward hello 要求 toohello 原始伺服器。 預先載入內容以避免此第一次點擊的延遲。

此外 tooproviding 較佳的客戶體驗，預先載入快取的資產也可降低 hello 原始伺服器上的網路流量。

> [!NOTE]
> 預先載入資產是適用於大量的事件，或成為同時可用 tooa 大量的使用者，例如新的影片版本或在軟體更新的內容。
> 
> 

本教學課程將逐步引導您在 Azure CDN 邊緣節點上預先載入快取的所有內容。

## <a name="walkthrough"></a>逐步介紹
1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello CDN 設定檔包含您想 toopre 負載 hello 端點。  hello 設定檔 刀鋒視窗隨即開啟。
2. 按一下 [hello] 清單中的 hello 端點。  hello 端點刀鋒視窗隨即開啟。
3. 從 hello CDN 端點刀鋒視窗中，按一下 hello 載入 按鈕。
   
    ![CDN 端點刀鋒視窗](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    hello 負載刀鋒視窗隨即開啟。
   
    ![CDN 載入刀鋒視窗](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. 輸入 hello 完整路徑的每個資產，您想 tooload (例如`/pictures/kitten.png`) 在 hello**路徑**文字方塊。
   
   > [!TIP]
   > 多個**路徑**文字方塊會出現在輸入文字 tooallow 之後 toobuild 多個資產的清單。  您可以在 hello 省略符號 （...） 按鈕，即可從 hello 清單刪除資產。
   > 
   > 路徑必須符合下列 hello 相對 URL[規則運算式](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >載入單一檔案路徑 `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`；  
   > >以查詢字串載入單一檔案 `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > 每個資產都必須有自己的路徑。  預先載入資產沒有萬用字元功能。
   > 
   > 
   
    ![載入按鈕](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. 按一下 hello**負載** 按鈕。
   
    ![載入按鈕](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> 每個 CDN 設定檔都有每分鐘 10 個載入要求的限制。 每個要求允許 50 個路徑。 每個路徑都有 1024 個字元的路徑長度限制。
> 
> 

## <a name="see-also"></a>另請參閱
* [清除 Azure CDN 端點](cdn-purge-endpoint.md)
* [Azure CDN REST API 參考資料 - 清除或預先載入端點](https://msdn.microsoft.com/library/mt634451.aspx)

