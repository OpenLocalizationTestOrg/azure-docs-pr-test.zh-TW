---
title: "在多租用戶應用程式中使用 Azure SQL Database aaaProvision 新的租用戶 |Microsoft 文件"
description: "了解如何 tooprovision 和新的類別目錄中的租用戶 hello Wingtip SaaS 應用程式"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>新的租用戶佈建並 hello 目錄中註冊這些元件

在本教學課程中，您會了解 hello 佈建和類別目錄 SaaS 模式，以及在 hello Wingtip SaaS 應用程式中的實作方式。 您會建立並初始化新的租用戶資料庫和 hello 應用程式的租用戶目錄中註冊。 hello 目錄是資料庫中，維護 hello hello SaaS 應用程式的多個租用戶和其資料之間的對應。 hello 目錄扮演重要角色導向應用程式要求 toohello 正確的資料庫。  

在本教學課程中，您將了解如何：

> [!div class="checklist"]

> * 佈建單一的新租用戶，包括逐步執行其實作方式
> * 佈建一批額外的租用戶


toocomplete 完成本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-catalog-pattern"></a>簡介 toohello SaaS 目錄模式

在資料庫備份多租用戶 SaaS 應用程式中，很重要的 tooknow 儲存每個租用戶的資訊。 在 hello SaaS 目錄模式中，類別目錄資料庫是使用的 toohold hello 對應每個租用戶之間，以及其資料的儲存位置。 hello Wingtip SaaS 應用程式使用單一租用戶，每個資料庫架構，但儲存到資料庫租用戶對應的目錄中的 hello 基本模式適用於是否會使用多租用戶或單一租用戶的資料庫。

每個租用戶指派可識別它們 hello 目錄中的索引鍵，這是對應 toohello hello 適當資料庫位置。 Hello Wingtip SaaS 應用程式，在 hello 金鑰被正確從 hello 租用戶名稱的雜湊。 這可讓 hello 應用程式 URL toobe hello 租用戶名稱部分使用 tooconstruct hello 索引鍵。 您可以使用其他租用戶金鑰的配置。  

hello 類別目錄可讓 hello 名稱或位置 hello 資料庫 toobe 變更 hello 應用程式上的影響降到最低。  在多租用戶資料庫模型中，這也適用於在資料庫之間「移動」租用戶。  hello 目錄也可以使用的 tooindicate 是否租用戶，或資料庫已離線進行維護或其他動作。 這會探索在 hello[還原單一租用戶教學課程](sql-database-saas-tutorial-restore-single-tenant.md)。

此外，hello 目錄，也就是作用中 SaaS 應用程式管理資料庫，可以儲存其他租用戶或資料庫的中繼資料，例如 hello 層或版本的資料庫、 結構描述版本中，服務方案或 Sla 提供 tootenants 和其他資訊，可讓應用程式管理、 客戶支援或 devops 程序。  

Hello SaaS 應用程式，超出 hello 目錄可以啟用資料庫工具。  在 hello Wingtip SaaS 範例中，hello 目錄是使用的 tooenable 跨租用戶查詢中，瀏覽在 hello[臨機操作分析教學課程](sql-database-saas-tutorial-adhoc-analytics.md)。 跨資料庫作業管理會探索在 hello[結構描述管理](sql-database-saas-tutorial-schema-management.md)和[租用戶分析](sql-database-saas-tutorial-tenant-analytics.md)教學課程。 

Hello Wingtip SaaS 應用程式，在 hello 類別目錄會實作使用 hello 分區管理功能的 hello[彈性資料庫用戶端程式庫 (EDCL)](sql-database-elastic-database-client-library.md)。 hello EDCL 可讓應用程式 toocreate、 管理及使用的資料庫為基礎的分區對應。 分區對應包含一份分區 （資料庫） 的索引鍵 （租用戶） 與資料庫之間的 hello 對應。  EDCL 函式可從應用程式或 PowerShell 指令碼期間 toocreate hello 項目在 hello 分區對應中，佈建的租用戶，並從應用程式 tooefficiently 連接 toohello 正確的資料庫。 EDCL 快取連接資訊 toominimize hello 流量 toohello 類別目錄資料庫，並加快 hello 應用程式。  

> [!IMPORTANT]
> hello 對應資料可供存取在 hello 類別目錄資料庫中，但*不要編輯*！ 務必只使用彈性資料庫用戶端程式庫 API 編輯對應資料。 直接操控 hello 對應資料損毀 hello 風險目錄並不支援。


## <a name="introduction-toohello-saas-provisioning-pattern"></a>簡介 toohello SaaS 佈建模式

在使用單一租用戶資料庫模型的 SaaS 應用程式中將新的租用戶上線時，必須佈建新的租用戶資料庫。  它必須建立在 hello 適當的位置以及服務層，以適當的結構描述和參考資料，初始化，然後在 hello 適當的租用戶金鑰 hello 目錄中登錄。  

不同的方法可以是使用的 toodatabase 佈建時，可能包括執行 SQL 指令碼、 將 bacpac 部署或複製 '黃金' 的範本資料庫。  

hello 佈建的方法，就必須瞭解整體結構描述管理策略中，必須確保新的資料庫會佈建與 hello 最新的結構描述。  這會探索在 hello[結構描述管理教學課程](sql-database-saas-tutorial-schema-management.md)。  

hello Wingtip SaaS 應用程式佈建新租用戶藉由複製標準資料庫名為 basetenantdb，hello 類別目錄伺服器上部署。  佈建無法進行整合至 hello 應用程式的註冊體驗，及/或支援離線使用指令碼。 本教學課程將會使用 PowerShell 來探索佈建。 hello 佈建指令碼複製 hello basetenantdb toocreate 新的租用戶資料庫在彈性集區，然後初始化使用租用戶專屬的資訊並在 hello 目錄分區對應中註冊它。  Hello 範例應用程式，資料庫會根據指定名稱 hello 租用戶名稱，但這不是很重要的一部分 hello 模式 – hello 使用 hello 類別目錄可讓任何名稱 toobe 指派 toohello 資料庫。 + 


## <a name="get-hello-wingtip-application-scripts"></a>取得 hello Wingtip 應用程式指令碼

hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 [步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。


## <a name="provision-and-catalog-detailed-walkthrough"></a>佈建及編目的詳細逐步解說

toounderstand 如何 hello 的 Wingtip 應用程式會實作新的租用戶佈建、 加入中斷點和逐步執行 hello 工作流程中，佈建租用戶時：

1. 開啟...\\學習模組\\ProvisionAndCatalog\\_示範 ProvisionAndCatalog.ps1_和集 hello 下列參數：
   * **$TenantName** = hello hello 新地點名稱 (例如， *Bushwillow 則藍色*)。
   * **$VenueType** = hello 預先定義的法院類型之一：*則藍色*，classicalmusic，舞、 jazz、 judo、 用途，motorracing opera、 rockmusic、 足球。
   * **$DemoScenario** = **1**，太將**1**太*佈建單一租用戶*。

1. 將游標置於 48，hello 一行，指出上的任何位置加入中斷點：*新增租用戶 '*，然後按**F9**。

   ![中斷點](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. toorun hello 指令碼按**F5**。

1. Hello 中斷點停止 hello 指令碼執行之後，請按**F11** toostep hello 程式碼。

   ![中斷點](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



追蹤使用 hello hello 指令碼執行**偵錯**功能表選項- **F10**和**F11** toostep 透過或 hello 呼叫函式。 如需對 PowerShell 指令碼進行偵錯的詳細資訊，請參閱[使用 PowerShell 指令碼及對其進行偵錯的祕訣](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise) \(英文\)。


hello 下列不會遵循 tooexplicitly，步驟而 hello hello 指令碼偵錯時逐步執行的工作流程的說明：

1. **匯入 hello SubscriptionManagement.psm1**包含登入 tooAzure 並選取您正在使用的 Azure 訂用帳戶的 hello 函式的模組。
1. **匯入 hello CatalogAndDatabaseManagement.psm1**模組，以提供目錄和租用戶層級抽象 hello[分區管理](sql-database-elastic-scale-shard-map-management.md)函式。 這是重要的模組，用以封裝大部分 hello 目錄模式和值得瀏覽。
1. **取得設定詳細資料**。 逐步執行 Get-組態 （F11)，請參閱 < 如何指定 hello 應用程式組態。 資源名稱和其他應用程式專屬值所定義，但不要變更這些值直到您已經熟悉 hello 指令碼。
1. **取得 hello 目錄物件**。 逐步執行 Get 目錄撰寫，並傳回 hello 較高層級的指令碼中使用的目錄物件。  此函式會使用從 **AzureShardManagement.psm1** 匯入的分區管理函式。 hello 目錄物件由 hello 下列：
   * 使用 hello 標準 stem 加上您的使用者名稱來建構 $catalogServerFullyQualifiedName:_目錄-\<使用者\>。.database.windows.net_。
   * $catalogDatabaseName 擷取自 hello 組態： *tenantcatalog*。
   * $shardMapManager 物件會從 hello 類別目錄資料庫初始化。
   * $shardMap 物件會從 hello 進行初始化*tenantcatalog* hello 類別目錄資料庫中的分區對應。
   目錄物件是由和傳回，而且 hello 較高層級的指令碼中使用。
1. **計算新租用戶金鑰 hello**。 雜湊函式是使用的 toocreate hello 租用戶金鑰的 hello 租用戶名稱。
1. **請檢查 hello 租用戶金鑰是否已存在**。 hello 類別目錄會檢查 tooensure hello 的金鑰。
1. **hello 租用戶資料庫是透過新增 TenantDatabase 佈建。** 使用**F11** toostep 中的，並查看 hello 資料庫如何使用佈建[Azure Resource Manager 範本](../azure-resource-manager/resource-manager-template-walkthrough.md)。

hello 資料庫名稱是從 hello 租用戶名稱 toomake 它清除哪一個分區所屬 toowhich 租用戶所建構。 （其他資料庫命名的策略可以輕鬆地加以使用。）+ Resource Manager 範本是使用的 toocreate 租用戶資料庫複製 hello 類別目錄伺服器上的標準資料庫 (baseTenantDB)。 另一個方法無法被 toocreate 空白資料庫，然後予以初始化藉由匯入 bacpac 或 tooexecute 初始化指令碼，從已知的位置。  

hello Resource Manager 範本是 hello...\Learning Modules\Common\ 資料夾中： *tenantdatabasecopytemplate.json*

建立 hello 租用戶資料庫之後，就再進一步**hello 法院 （租用戶） 名稱與 hello 法院類型初始化**。 也可以在此進行其他初始化。

hello **hello 目錄中註冊租用戶資料庫**與*新增 TenantDatabaseToCatalog*使用 hello 租用戶金鑰。 使用**F11** toostep 到 hello 詳細資料：

* hello 類別目錄資料庫會加入 toohello 分區對應 （已知的資料庫中的 hello 清單）。
* 會建立對應的連結 hello 索引鍵值 toohello 分區的 hello。
* Hello 租用戶的相關額外的中繼資料 （hello 地點名稱） 會加入 toohello 租用戶資料表 hello 目錄中。  hello 租用戶資料表不 hello ShardManagement 結構描述的一部分，而且不會安裝 hello EDCL。  這份表格說明如何 hello 類別目錄資料庫可以擴充 toosupport 其他應用程式特定資料。   


佈建完成後，執行會傳回 toohello 原始*示範 ProvisionAndCatalog*指令碼，這會開啟 hello**事件**hello hello 瀏覽器中的新租用戶的頁面：

   ![活動](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>佈建一批租用戶

此練習會佈建一批 17 個租用戶。 建議您啟動其他 Wingtip SaaS 教學課程中，所以具有多個在短短幾資料庫 toowork 之前佈建的租用戶此批次。

1. 開啟...\\學習模組\\ProvisionAndCatalog\\*示範 ProvisionAndCatalog.ps1*在 hello *PowerShell ISE*並變更 hello *$DemoScenario*參數 too3:
   * **$DemoScenario** = **3**，也變更**3**太*佈建租用戶的批次*。
1. 按**F5**執行 hello 指令碼。

hello 指令碼會將部署其他租用戶批的次。 它會使用[Azure Resource Manager 範本](../azure-resource-manager/resource-manager-template-walkthrough.md)，控制 hello 批次，並委派給每個資料庫 tooa 連結範本的佈建。 使用範本以這種方式可讓 Azure Resource Manager toobroker hello 佈建指令碼的程序。 範本佈建資料庫，以平行方式，它可以和處理重試次數，如有需要最佳化 hello 整體處理序。 hello 指令碼等冪，如果失敗，或因為任何原因而停止執行一次。

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>確認成功部署的租用戶的 hello 批次

* 開啟 hello *tenants1*伺服器瀏覽伺服器 hello tooyour 清單[Azure 入口網站](https://portal.azure.com)，按一下  **SQL 資料庫**，並確認 hello 批次的 17 的額外資料庫現在是在 hello 清單：

   ![資料庫清單](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>其他佈建模式

未包含在此教學課程中的其他佈建模式包括：

**預先佈建資料庫。** 預先佈建模式 hello 利用 hello 事實無法增加彈性集區中的資料庫需要額外成本。 計費是 hello 彈性集區，不 hello 資料庫和閒置資料庫取用任何資源。 藉由在集區中預先佈建資料庫，並在需要時才配置它們，可以大幅降低租用戶上線時間。 時需要的 tookeep 適合 hello 緩衝區預期佈建速率，就無法調整 hello 預先佈建的資料庫數目。

**自動佈建。** 在 hello 自動佈建模式中，專用的佈建服務會使用的 tooprovision 伺服器、 集區和資料庫自動視需要 – 包括彈性集區中預先佈建的資料庫，如有需要。 和資料庫會解除委託和刪除，如果 hello 佈建所需的服務可以填入彈性集區中的間距。 此類服務可以是簡單或複雜的 (例如，跨多個地理位置處理佈建)，且如果已針對災害復原使用異地複寫，就可自動設定該策略。 Hello 自動佈建模式時，用戶端應用程式或指令碼會送出 hello 佈建服務，由處理佈建要求 tooa 佇列 toobe 與然後會輪詢 hello 服務 toodetermine 完成。 如果使用預先佈建時，會處理要求快速 hello 服務管理佈建的 hello 背景中執行的替代資料庫。



## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]

> * 佈建單一新租用戶
> * 佈建一批額外的租用戶
> * 逐步執行 hello 的佈建租用戶，以及登錄這些入 hello 類別目錄的詳細資料

再試一次 hello[效能監視的教學課程](sql-database-saas-tutorial-performance-monitoring.md)。

## <a name="additional-resources"></a>其他資源

* 其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [彈性資料庫用戶端程式庫](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [TooDebug 如何在 Windows PowerShell ISE 指令碼](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
