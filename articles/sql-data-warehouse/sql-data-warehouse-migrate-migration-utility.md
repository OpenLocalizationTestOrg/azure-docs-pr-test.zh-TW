---
title: "移轉：資料倉儲移轉公用程式 | Microsoft Docs"
description: "移轉 tooSQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>資料倉儲移轉公用程式 (預覽)
> [!div class="op_single_selector"]
> * [下載移轉公用程式][Download Migration Utility]
> 
> 

hello 資料倉儲移轉公用程式是一項工具設計 toomigrate 結構描述和資料從 SQL Server 和 Azure SQL Database tooAzure SQL 資料倉儲。 結構描述移轉期間，hello 工具會自動對應從來源 toodestination hello 對應的結構描述。 移轉 hello 結構描述之後，hello 工具提供的自動產生的指令碼與 hello 選項 toomove 資料。

此外 tooschema 和資料移轉，hello 選項 toogenerate 相容性報告 hello 目標和來源執行個體而這可避免之間的不相容性摘要列出此工具可提供流暢的移轉。

## <a name="get-started"></a>開始使用
為安裝的必要元件，您將需要 hello BCP 命令列公用程式 toorun 移轉指令碼和 Office tooview hello 相容性報告。 之後啟動 hello hello 工具會在安裝之前就會下載您的可執行檔時，將會提示的 tooaccept 標準的使用者授權合約。

此外，toorun hello 移轉 Utiliy，您將需要 hello 其中一個您要尋找 toomigrate hello 資料庫上下列權限： CREATE DATABASE、 ALTER ANY DATABASE 或 VIEW ANY DEFINITION。

### <a name="launching-hello-tool-and-connecting"></a>啟動 hello 工具和連線
Hello 桌面圖示會出現後即可啟動 hello 工具安裝。 在開啟 hello 工具，您將會提示您可以在其中選擇您的來源和目的地 hello 移轉工具的初始連接頁面。 目前，此工具支援 SQL Server 和 Azure SQL Database 做為來源，SQL 資料倉儲做為目的地。 選取這之後將會要求您 tooconnect tooyour 來源伺服器填入伺服器名稱和驗證，然後按一下連線。

驗證之後，hello 工具將顯示一份在於 hello 伺服器連線到資料庫。 您可以選取您想要 toomigrate，然後按一下選取的移轉' 的資料庫來開始 hello 移轉。

## <a name="migration-report"></a>移轉報告
選取 '檢查資料庫相容性' hello 工具中將會產生彙總所有的物件不相容的報表要求 toomigrate hello 資料庫中。 一些 hello 不存在於 SQL 資料倉儲的 SQL Server 功能的廣泛清單位於我們[移轉文件][migration documentation]。 產生 hello 報告之後您將會無法 toosave 並且在 Excel 中的開啟 hello 報表。

請注意，當產生 hello 移轉結構描述，大部分的問題識別為 'Object' 將會調整的該資料的順序 tooallow 即時移轉。 請檢閱 hello 變更 tooensure 套用 hello 結構描述之前不要 toomake 其他調整。

## <a name="migrate-schema"></a>移轉結構描述
連接之後，請選取 '移轉結構描述' 會產生 hello 選取資料表的結構描述移轉指令碼。 此指令碼的連接埠 hello 資料表的結構 hello，對應不相容的資料型別 toomore 相容表單，並建立安全性認證和結構描述如果 hello 移轉設定中的 hello 使用者表示這一點。 此程式碼可以對目標的 hello SQL 資料倉儲執行個體執行、 儲存 tooa 檔案、 複製 tooyour 剪貼簿，或甚至編輯內嵌採取進一步的動作之前。  

為前面所述，當移轉的結構描述檢閱 hello 移轉變更該 hello 工具所做的順序 tooensure，您完全了解它們。  

## <a name="migrate-data"></a>移轉資料
按一下 hello 移轉資料的選項，您可以產生會移動資料第一次 tooflat 檔案在伺服器上的 BCP 指令碼，然後直接將您的 SQL 資料倉儲。 我們建議此程序來移動少量的資料，以及重試次數為不是內建的 hello 網路連線中斷時，可能會發生失敗。 在順序 toorun，您將需要 toohave hello BCP 命令列公用程式安裝而且 hello hello 資料的結構描述必須已經建立。

您已填入處理 hello 參數之後高於您只需要 tooclick 執行移轉，而且會產生一組兩個封裝 tooyour 指定的位置。 在一般檔案，從您移轉的來源執行 hello 匯出檔案中訂單 tooexport 資料並執行 hello 匯入檔案中順序 tooimport 資料到 SQL 資料倉儲。

## <a name="next-steps"></a>後續步驟
既然您已移轉的某些資料，請參閱如何太[開發][develop]。

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
