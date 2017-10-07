---
title: "向上 hello 管標記，在 Azure 資料目錄中的商務詞彙 aaaSet |Microsoft 文件"
description: "如何 tooarticle 反白顯示 hello 商務字彙中定義及使用通用的商務詞彙 tootag Azure 資料目錄註冊的資料資產。"
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
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>設定決定標記 hello 商務字彙
## <a name="introduction"></a>簡介
Azure 資料目錄可讓資料來源探索，因此您可以輕鬆地找出並了解 hello 資料來源，您需要 tooperform 分析和做出決策。 時，您可以尋找並了解可用的資料來源的 hello 大範圍，這些功能會構成 hello 大影響。

正在標記一個資料目錄功能，可提升對資產資料的了解。 藉由使用標記，您可以與資產或資料行，接著使其更容易 toodiscover hello 資產透過搜尋或瀏覽關聯關鍵字。 標記也可協助您更輕鬆地了解 hello 內容和 hello 資產的意圖。

不過，標記有時會造成自己的問題。 標記可能會造成問題的部分範例如下：

* hello 使用上的某些資產的縮寫與在其他的展開的文字。 此不一致性所妨礙 hello 探索的資產，即使 hello 意圖是以 hello tootag hello 資產相同的標記。
* 意義的潛在變化取決於內容。 例如，標記稱為*營收*某個客戶的資料集可能表示營收的客戶，但 hello 每季的銷售資料集上的相同標記可能代表每季 hello 公司營收。  

toohelp 解決這些和其他類似的挑戰，資料目錄包含商務字彙。

藉由使用 hello 資料目錄商務字彙，組織可以記錄關鍵商務字詞以及其定義 toocreate 通用的商務詞彙。 此控管 hello 組織內啟用使用量資料的一致性。 Hello 商務字彙中定義的詞彙之後，它可以指派 tooa hello 目錄中的資料資產。 這種方式，*控管標記*，是 hello 一樣標記的方法。

## <a name="glossary-availability-and-privileges"></a>詞彙可用性和權限
hello 商務字彙是只能在 hello 標準版本的 Azure 資料目錄。 hello 的資料目錄免費 Edition 不包括詞彙，且不提供功能來管標記。

您可以存取透過 hello hello 商務字彙**詞彙**hello 資料目錄入口網站的瀏覽功能表中的選項。  

![存取 hello 商務字彙](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

資料目錄管理員和系統管理員角色可以建立、 hello 詞彙的成員編輯和刪除在 hello 的商務詞彙的詞彙。 所有的資料目錄使用者可以檢視 hello 詞彙定義和字彙字詞標籤資產。

![新增字彙](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>建立詞彙
資料目錄管理員和詞彙的系統管理員可以建立詞彙即可 hello**新詞彙**] 按鈕。 每個詞彙的詞彙包含下列欄位的 hello:

* Hello 詞彙的商務定義
* 擷取預期的 hello 用途或商務規則 hello 資產或資料行的描述
* 專案關係人知道 hello hello 詞彙的最相關的清單
* hello 父系字詞定義詞彙組織中的 hello hello 階層

## <a name="glossary-term-hierarchies"></a>詞彙階層
藉由使用 hello 資料目錄商務字彙，組織可以為階層的詞彙，描述其商務詞彙，而且可以建立的詞彙更能代表其商務分類的分類。

字詞在階層的給定層級中必須是唯一項目。 不允許使用重複的名稱。 在階層中，層級的數量沒有限制 toohello 但階層通常更容易了解時有三個層級或更少。

階層中 hello 商務字彙 hello 使用是選擇性的。 讓 hello 父詞彙欄位空白的字彙字詞 hello 詞彙中建立詞彙 （非階層式） 的一般的清單。  

## <a name="tagging-assets-with-glossary-terms"></a>利用詞彙標記資產
詞彙定義 hello 目錄中之後，標記資產 hello 體驗為最佳化的 toosearch hello 詞彙使用者類型標記。 hello 資料目錄入口網站會顯示從相符詞彙條款 toochoose 的清單。 如果 hello 使用者從 hello 清單中選取的詞彙的詞彙，hello 詞彙加入 toohello 資產 （也稱為詞彙標記） 的標記。 hello 使用者也可以選擇 toocreate 新標記輸入不是處於 hello 的詞彙 （也稱為使用者標記） 的詞彙。

![使用一個使用者標籤和兩個詞彙標籤標記的資料資產](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> 使用者標記的標記中支援的型別 hello 的資料目錄免費 Edition 只有在已經 hello。
>
>

### <a name="hover-behavior-on-tags"></a>將滑鼠游標停留在標記上的行為
在 hello 資料目錄入口網站 hello 兩種類型的標記都是以視覺化方式不同，且有不同的動態顯示行為。 當您將滑鼠停留在使用者標記時，您可以看到 hello 標記文字和 hello 使用者或使用者已新增 hello 標記。 您將滑鼠停留在詞彙標記，您也看到 hello 字彙 hello 定義及連結 tooopen hello 商務字彙 tooview hello 完整定義 hello 詞彙。

### <a name="search-filters-for-tags"></a>標籤的搜尋篩選
詞彙標籤和使用者標籤都可供搜尋，您可以將它們套用到搜尋中作為篩選。

## <a name="summary"></a>摘要
您可以藉由使用 Azure 資料目錄，和 hello 控管標記它可讓 hello 商務字彙，識別、 管理及探索資料資產以一致的方式。 hello 商務字彙可以升級學習的組織成員 hello 的商務詞彙。 hello 詞彙也支援擷取有意義的中繼資料，可簡化資產探索及了解。

## <a name="next-steps"></a>後續步驟
* [商務詞彙作業的 REST API 文件](https://msdn.microsoft.com/library/mt708855.aspx)
