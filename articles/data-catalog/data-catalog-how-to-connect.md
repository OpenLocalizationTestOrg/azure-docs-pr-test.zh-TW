---
title: "aaaHow tooconnect toodata 來源 |Microsoft 文件"
description: "如何 tooarticle tooconnect toodata 來源與 Azure 資料目錄探索的方式反白顯示。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>如何 tooconnect toodata 來源
## <a name="introduction"></a>簡介
**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。 換句話說， **Azure 資料目錄**是協助人員相關的所有探索、 了解，以及使用資料來源，以及協助組織 tooget 其現有的資料來自多個值。 此案例中的重要層面使用的 hello 資料 – 一旦使用者探索資料來源，並了解其用途、 hello 下一個步驟是 tooconnect toohello 資料來源的 tooput 其資料 toouse。

## <a name="data-source-locations"></a>資料來源位置
資料來源在註冊期間， **Azure 資料目錄**收到 hello 資料來源的相關中繼資料。 此中繼資料包括 hello hello 資料來源的位置詳細資料。 hello hello 位置詳細資料也會因資料來源 toodata 來源，但它永遠包含 hello 所需的資訊 tooconnect。 比方說，SQL Server 資料表的 hello 位置包含 hello 伺服器名稱、 資料庫名稱、 結構描述名稱和資料表名稱，而 SQL Server Reporting Services 報表的 hello 位置包含 hello 伺服器名稱和 hello 路徑 toohello 報表。 其他資料來源類型必須反映 hello 結構和 hello 來源系統功能的位置。

## <a name="integrated-client-tools"></a>整合式用戶端工具
hello 最簡單方式 tooconnect tooa 資料來源為 toouse hello 」 中開啟。.." 在 [hello] 功能表**Azure 資料目錄**入口網站。 這個功能表會顯示一份連接 toohello 選取的資料資產的選項。
使用 hello 預設並排顯示檢視，這個功能表可用時，在 hello 每個圖格。

 ![在 Excel 中開啟 SQL Server 資料表從 hello 資料資產磚](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

使用 hello 清單檢視，hello 功能表會在 hello hello 入口網站視窗最上方的 hello 搜尋列中可用。

 ![在報表管理員開啟 SQL Server Reporting Services 報表，從 hello 搜尋列](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>支援的用戶端應用程式
當使用 hello 」 中開啟。.." hello Azure 資料目錄入口網站中的功能表上的資料來源，hello 正確的用戶端應用程式必須安裝在 hello 用戶端電腦上。

| 在應用程式中開啟 | 副檔名/通訊協定 | 支援的應用程式版本 |
| --- | --- | --- |
| Excel |.odc |Excel 2010 或更新版本 |
| Excel (前 1000 個) |.odc |Excel 2010 或更新版本 |
| Power Query |.xlsx |安裝 Excel 2016 或 Excel 2010 或 Excel 2013 hello Power Query for Excel 增益集 |
| Power BI Desktop |.pbix |Power BI Desktop 2016 年 7 月或更新版本 |
| SQL Server Data Tools |vsweb:// |安裝了 SQL Server 工具的 Visual Studio 2013 Update 4 或更新版本 |
| 報表管理員 |http:// |請參閱 [SQL Server Reporting Services 的瀏覽器需求](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>您的資料與工具
hello 功能表中的 hello 選項將取決於目前選取的資料資產的 hello 型別。 當然，並非所有可能的工具將會包含在 hello 」 中開啟。.." 功能表上，但它並使用任何用戶端工具仍然可以輕易 tooconnect toohello 資料來源。 Hello 中選取的資料資產時**Azure 資料目錄**入口網站中，hello 完整位置會顯示 hello 屬性 窗格中。

 ![SQL Server 資料表的連接資訊](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

hello 連接資訊詳細資料將會不同，從資料來源類型 toodata 來源類型，但 hello hello 入口網站中所包含的資訊可讓您需要在任何用戶端工具 tooconnect toohello 資料來源的所有項目。 使用者只能複製 hello 發現使用 hello 資料來源的連線詳細資料**Azure 資料目錄**，讓他們 toowork hello 中的資料其選擇的工具。

## <a name="connecting-and-data-source-permissions"></a>連接和資料來源的權限
雖然**Azure 資料目錄**可讓資料來源可探索，存取本身 toohello 資料會保留在 hello hello 資料來源擁有者或系統管理員的控制之下。 探索中的資料來源**Azure 資料目錄**並不提供使用者任何權限 tooaccess hello 資料來源本身。

toomake 方便使用者探索資料來源，但不會有權限 tooaccess 其資料，使用者可以在中提供資訊 hello 要求存取屬性加註解的資料來源時。 – 包括連結 toohello 程序或以存取資料來源的連絡點 – 此處提供的資訊會連同 hello hello 入口網站中的資料來源位置資訊。

 ![具有所提供之要求存取指示的連接資訊](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>摘要
登錄資料來源與**Azure 資料目錄**hello 資料來源的結構化及描述性的中繼資料複製 hello 類別目錄服務，讓該資料可探索。 一旦資料來源具有已註冊，並發現，使用者可以從 hello 連線 toohello 資料來源**Azure 資料目錄**入口網站 」 中開啟。.."" 功能表，或使用他們選擇的資料工具，連接到資料來源。

## <a name="see-also"></a>另請參閱
* [開始使用 Azure 資料目錄](data-catalog-get-started.md)方式的逐步詳細的教學課程，tooconnect toodata 來源。
