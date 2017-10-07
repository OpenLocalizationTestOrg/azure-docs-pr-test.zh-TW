---
title: "aaaHow tooannotate 資料來源 |Microsoft 文件"
description: "如何 tooarticle 反白顯示如何在 Azure 資料目錄中，包括易記名稱、 標籤、 描述和專家 tooannotate 資料資產。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>如何 tooannotate 資料來源
## <a name="introduction"></a>簡介
**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。 換句話說，資料目錄就是要協助大眾探索、 了解，以及使用資料來源，以及幫助組織 tooget 多個值，從現有的資料。 當資料來源已向資料目錄時，它的中繼資料會複製，並以 hello 服務編製索引但 hello 劇本那里未結束。 資料類別目錄可讓使用者 tooprovide hello 資料來源，從擷取他們自己描述性的中繼資料 – 例如描述和標記 – toosupplement hello 中繼資料和 toomake hello 資料來源的更多容易了解 toomore 人。

## <a name="annotation-and-crowdsourcing"></a>註解與群眾外包
每個人都有意見。 而這是一件好事。
資料目錄了解不同的使用者對企業資料來源有不同的觀點，而每個觀點都具有潛在的價值。 請考慮下列案例中的 hello:

* hello 系統管理員知道 hello 的服務等級協定 hello 伺服器或服務主機 hello 資料來源。
* hello 資料庫管理員知道 hello 備份排程為每個資料庫，並 hello 允許 etl 程序的 windows。
* hello 系統擁有者知道使用者 toorequest access toohello 資料來源的 hello 程序。
* hello 資料管理人知道如何 hello 資產和 hello 資料來源中的屬性對應 toohello 企業資料模型。
* hello 分析師知道 hello 資料 hello hello 他所支援的商務程序內容中的使用方式。

這些檢視方塊的每一個都是相當重要，和資料目錄使用 crowdsourcing 方法 toometadata，可讓每一個 toobe 擷取，並使用 tooprovide 完整的已註冊的資料來源。 使用 hello 資料目錄入口網站，每位使用者可以加入並編輯其註解，同時會提供其他使用者所能 tooview 註解。

## <a name="different-types-of-annotations"></a>不同類型的註解
資料目錄支援 hello 下列類型的附註：

| 註解 | 注意事項 |
| --- | --- |
| 易記名稱 |易記名稱可以提供層級 hello 資料資產，更容易了解 toomake hello 資料資產。 隱密、 縮寫或否則沒有意義 toousers hello 基礎物件名稱時，易記名稱會是最有用。 |
| 說明 |可以在 hello 資料資產和屬性提供描述 / 資料行層級。 描述會描述 hello 使用者的觀點來看，在 hello 資料資產或其用法的簡短的自由格式文字註解。 |
| 標籤 (使用者標籤) |標籤可以提供在 hello 資料資產和屬性 / 資料行層級。 使用者標記是使用者定義的標籤，以使用的 toocategorize 資料資產或屬性。 |
| 標籤 (詞彙標籤) |標籤可以提供在 hello 資料資產和屬性 / 資料行層級。 詞彙標記是集中定義詞彙可以使用的 toocategorize 資料資產或使用通用的商務分類的屬性。 如需詳細資訊，請參閱[向上 tooset 來控管標記所 hello 的商務字彙](data-catalog-how-to-business-glossary.md) |
| 專家 |您可以提供專家 hello 資料資產的層級。 專家識別與 hello 資料專家檢視方塊的使用者或群組，而且可以服務探索 hello 的使用者的連絡點登錄資料來源，並具有未回答的 hello 現有的註解的問題。 |
| 要求存取 |要求存取資訊可以提供層級 hello 資料資產。 這項資訊是探索資料來源，它們還沒有權限 tooaccess 專為使用者。 使用者可以輸入 hello 電子郵件地址 hello 使用者或群組授與存取權、 hello hello 程序的 URL 或工具的使用者需要 toogain 存取，或可以輸入 hello 程序本身為文字。 |
| 文件 |文件可以提供層級 hello 資料資產。 資產文件是 RTF 格式的資訊，其中可以包含連結和影像，並可提供未透過描述和標籤傳達的任何資訊。 |

## <a name="annotating-multiple-assets"></a>註解多個資產
當選取多個資料資產中的 hello 資料目錄入口網站，使用者可以標註在單一作業中所有選取的資產。 註解將套用選取的 tooall 資產，讓您輕鬆 tooselect，並為相關的資料資產，提供一致的描述和標記和專家的集合。

> [!NOTE]
> 標記和專家，也可以提供註冊使用 hello 資料目錄資料的資料資產來源註冊工具時。
>
>

當選取多個資料表和檢視表，只有資料行，所有選取的資產有通用的資料將會顯示 hello 資料目錄入口網站中。 這可讓使用者 tooprovide 標籤和描述的所有資料行名稱相同的 hello 與所有選取的資產。

## <a name="annotations-and-discovery"></a>註解和探索
就像 hello 註冊期間 hello 資料來源擷取的中繼資料新增 toohello 資料類別目錄搜尋索引，使用者提供的中繼資料也編製索引。 這表示不只進行註解方便使用者 toounderstand hello 資料使用者探索，註釋也可讓更容易使用者 toodiscover hello 標註的資料資產的使用，讓有意義 toothem hello 詞彙搜尋。

## <a name="summary"></a>摘要
以資料目錄註冊的資料來源，讓該資料可探索 hello 資料來源的結構化及描述性的中繼資料複製 hello 類別目錄服務。 一旦註冊資料來源之後，使用者可以提供註解 toomake 更容易 toodiscover，並了解從 hello 資料目錄入口網站中。

## <a name="see-also"></a>另請參閱
* [開始使用 Azure 資料目錄](data-catalog-get-started.md)方式的逐步詳細的教學課程，tooannotate 資料來源。
