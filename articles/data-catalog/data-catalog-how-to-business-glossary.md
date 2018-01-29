---
title: "在 Azure 資料目錄中設定控管標記的商務詞彙 | Microsoft Docs"
description: "強調 Azure 資料目錄中商務詞彙的操作說明文章，可定義和使用一般商務詞彙來標記註冊的資料資產。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/18/2018
ms.author: maroche
ms.openlocfilehash: a80b7fd0c21851a6670431e9b8647ca5cf5f51ec
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="set-up-the-business-glossary-for-governed-tagging"></a>設定控管標記的商務詞彙
## <a name="introduction"></a>簡介
Azure 資料目錄啟用了資料來源探索功能，讓您能夠輕鬆地探索和了解要執行分析和做出決策所需的資料來源。 當您能找到並了解最大範圍的可用資料來源時，這些功能就能發揮最大效果。

正在標記一個資料目錄功能，可提升對資產資料的了解。 藉由使用標記，您可以建立關鍵字與資產或資料行的關聯，進而透過搜尋或瀏覽更輕鬆地探索資產。 標記也可協助您更輕鬆地了解資產的內容和用途。

不過，標記有時會造成自己的問題。 標記可能會造成問題的部分範例如下：

* 對某些資產使用縮寫，但對其他資產使用展開的文字。 雖然目的是要使用相同的標籤標記資產，但是這項不一致會防礙資產的探索。
* 意義的潛在變化取決於內容。 例如，稱為「營收」的標籤在客戶資料集上可能表示客戶的營收，但是相同的標籤在每季銷售資料集上可能表示公司的每季營收。  

為了協助解決上述和其他類似的挑戰，資料目錄包含商務詞彙。

透過使用資料目錄商務詞彙，組織可記錄關鍵商務字詞及其定義，以建立常用的商務詞彙。 此控管可達成整個組織的資料使用一致性。 在商務詞彙中定義字詞之後，該字詞便可指派給目錄中的資料資產。 「控管標記」這種方法與標記方法相同。

## <a name="glossary-availability-and-privileges"></a>詞彙可用性和權限
商務詞彙只能在標準版 Azure 資料目錄中使用。 免費版的資料目錄不包含詞彙，而且不提供控管標記功能。

您可透過資料目錄入口網站之瀏覽功能表中的 [詞彙] 選項存取商務詞彙。  

![存取商務詞彙](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

資料目錄管理員和詞彙管理員角色的成員可以建立、編輯及刪除商務詞彙中的詞彙。 所有的資料目錄使用者都可以檢視字詞定義，而且可以利用詞彙標記資產。

![新增字彙](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>建立詞彙
資料目錄管理員和詞彙管理員可以按一下 [新增詞彙] 按鈕來建立詞彙。 每個詞彙包含下列欄位：

* 詞彙的商務定義
* 會擷取資產/資料行之指定用途或商務規則的描述
* 最了解這個詞彙的專案關係人清單
* 定義詞彙在其中組織之階層的父詞彙

## <a name="glossary-term-hierarchies"></a>詞彙階層
藉由使用資料目錄商務詞彙，組織可以用詞彙階層的方式描述其商務詞彙，而且可以建立詞彙分類，以便更能代表其商務分類。

字詞在階層的給定層級中必須是唯一項目。 不允許使用重複的名稱。 在單一階層中，層級數目沒有限制，但是三個層級以下的階層通常更容易了解。

商務詞彙中的階層使用是選擇性的。 讓詞彙的父字詞欄位保留空白會在詞彙中建立字詞的一般 (非階層式) 清單。  

## <a name="tagging-assets-with-glossary-terms"></a>利用詞彙標記資產
在目錄中定義詞彙之後，標記資產的體驗已最佳化，可在使用者輸入其標籤時搜尋詞彙。 資料目錄入口網站會顯示可以選擇的相符詞彙清單。 如果使用者從清單中選取一個詞彙，該字詞會新增至資產作為標籤 (也稱為詞彙標籤)。 使用者也可以選擇藉由鍵入不在詞彙中的字詞來建立新標籤 (也稱為使用者標籤)。

![使用一個使用者標籤和兩個詞彙標籤標記的資料資產](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> 使用者標籤是免費版資料目錄中唯一支援的標籤類型。
>
>

### <a name="hover-behavior-on-tags"></a>將滑鼠游標停留在標記上的行為
在資料目錄入口網站中，標籤的兩種類型在視覺上有所不同，而且將滑鼠游標停留的行為也不相同。 當您將滑鼠游標停留在使用者標籤上時，就可以看見標籤文字或新增該標籤的使用者。 當您將滑鼠游標停留在詞彙標籤上時，也會看見詞彙的定義，以及可開啟商務詞彙以檢視字詞完整定義的連結。

### <a name="search-filters-for-tags"></a>標籤的搜尋篩選
詞彙標籤和使用者標籤都可供搜尋，您可以將它們套用到搜尋中作為篩選。

## <a name="summary"></a>總結
透過使用 Azure 資料目錄中的商務詞彙和它啟用的控管標記，您可以利用一致的方式識別、管理與探索資料資產。 商務詞彙可提升組織成員對商務詞彙的學習。 詞彙也支援擷取有意義的中繼資料，其可簡化資產探索及了解。

## <a name="next-steps"></a>後續步驟
* [商務詞彙作業的 REST API 文件](https://msdn.microsoft.com/library/mt708855.aspx)
