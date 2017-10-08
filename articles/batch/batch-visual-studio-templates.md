---
title: "建置 Visual Studio 專案範本 Azure 批次方案 aaaStart |Microsoft 文件"
description: "了解 Visual Studio 專案範本如何協助您在 Azure Batch 中實作和執行計算密集型工作負載。"
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>使用 Visual Studio 專案範本 toojump 啟動批次方案

hello**作業管理員**和**工作處理器 Visual Studio 範本**批次提供的程式碼 toohelp 您 tooimplement 及執行運算密集的工作負載，以批次上至少 hello 的投入時間量。 本文件說明這些範本，並提供的指導 toouse 它們。

> [!IMPORTANT]
> 這篇文章討論唯一資訊適用 toothese 兩個範本，並假設您熟悉 hello 批次服務和主要概念相關的 tooit： 集區，計算節點、 工作和工作、 作業管理員工作、 環境變數和其他相關的資訊。 您可以找到更多資訊[Azure Batch 基本概念](batch-technical-overview.md)，[批次功能概觀，讓開發人員](batch-api-basics.md)，和[開始使用 hello Azure Batch library for.NET](batch-dotnet-get-started.md)。
> 
> 

## <a name="high-level-overview"></a>高階概述
hello 工作管理員] 和 [工作處理器範本可以是使用的 toocreate 兩個有用元件：

* 作業管理員工作，此工作會實作作業分割器，後者可將作業細分為多個可以平行且獨立執行的工作。
* 可以使用的 tooperform 前置處理和應用程式的命令列周圍的後續處理工作處理器。

比方說，在影片轉譯案例中，hello 作業分隔器會變成單一的電影作業數百或數千個不同的工作會分開處理個別畫面格。 相對的 hello 工作處理器會叫用 hello 呈現應用程式和所有相依的程序所需的 toorender 每個畫面格，以及執行任何額外的動作 （例如，複製 hello 轉譯畫面格 tooa 儲存位置）。

> [!NOTE]
> hello 工作管理員] 和 [工作處理器範本無關，因此兩者，或只有一個項目，視您計算的工作並在您的喜好設定的 hello 需求而定，您可以選擇 toouse。
> 
> 

Hello 如下圖所示，計算作業會使用這些範本會經歷三個階段：

1. hello 用戶端程式碼 （例如，應用程式、 web 服務等） 會提交作業 toohello 批次服務在 Azure 上，指定為其作業管理員工作 hello 工作管理員程式。
2. hello 批次服務在計算節點上執行 hello 作業管理員工作和 hello 作業分隔器會啟動 hello 工作處理器工作數目，在上指定做為許多計算節點做為必要項目，根據 hello 參數和 hello 作業分隔器程式碼中的規格。
3. hello 工作處理器工作獨立作業，以平行方式執行，tooprocess hello 輸入的資料，並產生 hello 輸出資料。

![顯示以 hello 批次服務用戶端程式碼的互動方式的圖表][diagram01]

## <a name="prerequisites"></a>必要條件
toouse hello 批次的範本，您需要下列 hello:

* 已安裝 Visual Studio 2015 的電腦。 目前只有針對 Visual Studio 2015 支援批次範本。
* hello 批次範本都是從 hello [Visual Studio 組件庫][ vs_gallery]做為 Visual Studio 擴充功能。 有兩種方式 tooget hello 範本：
  
  * 安裝使用 hello hello 範本**擴充功能和更新**Visual Studio 中的對話方塊 (如需詳細資訊，請參閱[尋找及使用 Visual Studio 擴充功能][vs_find_use_ext])。 在 hello**擴充功能和更新**對話方塊中，下列兩個延伸模組的搜尋和下載 hello:
    
    * 具有作業分割器的 Azure Batch 作業管理員
    * Azure Batch 工作處理器
  * 從 hello 線上組件庫下載 hello 範本，適用於 Visual Studio: [Microsoft Azure 批次的專案範本][vs_gallery_templates]
* 如果您計劃 toouse hello[應用程式封裝](batch-application-packages.md)功能 toodeploy hello 工作管理員和工作處理器 toohello 批次計算節點，您必須 toolink 儲存體帳戶 tooyour Batch 帳戶。

## <a name="preparation"></a>準備工作
我們建議您建立工作管理員，以及您工作的處理器，可包含的方案，因為這樣可以使它與您的作業管理員工作處理器程式更容易 tooshare 程式碼。 toocreate 此解決方案，請遵循下列步驟：

1. 開啟 Visual Studio，然後選取 [檔案] > [新增] > [專案]。
2. 在 [範本] 底下展開 [其他專案類型]、按一下 [Visual Studio 方案]，然後選取 [空白方案]。
3. 輸入描述您應用程式和 hello 的用途，此解決方案 (例如，"LitwareBatchTaskPrograms") 的名稱。
4. toocreate hello 新方案時，按一下 **確定**。

## <a name="job-manager-template"></a>作業管理員範本
hello 作業管理員範本可協助您 tooimplement 可以執行下列動作的 hello 作業管理員工作：

* 將作業分割成多個工作。
* 提交這些批次的工作 toorun。

> [!NOTE]
> 如需作業管理員工作的詳細資訊，請參閱 [適用於開發人員的 Batch 功能概觀](batch-api-basics.md#job-manager-task)。
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>建立作業管理員使用 hello 範本
tooadd 作業管理員 toohello 建立的方案，您更早版本，請遵循下列步驟：

1. 在 Visual Studio 中開啟現有方案。
2. 在 方案總管 中，以滑鼠右鍵按一下 hello 方案中，按一下 **新增** > **新專案**。
3. 在 Visual C# 底下按一下 雲端，然後按一下具有作業分割器的 Azure Batch 作業管理員。
4. 輸入描述您的應用程式，且 （例如識別為 hello 作業管理員的這個專案的名稱"LitwareJobManager")。
5. toocreate hello 專案中，按一下 **確定**。
6. 最後，建置 hello 專案 tooforce Visual Studio tooload 所有參考的 NuGet 封裝，並 hello 專案的 tooverify 有效，然後再開始進行修改。

### <a name="job-manager-template-files-and-their-purpose"></a>作業管理員範本檔案及其用途
當您使用範本建立專案 hello 工作管理員時，它會產生三個群組的程式碼檔案：

* hello 主要程式檔案 (Program.cs)。 這包含 hello 程式進入點和最上層的例外狀況處理。 您通常不應該這樣需要 toomodify。
* hello Framework 目錄。 這包含 hello 檔案負責 hello 工作管理員程式-解除封裝參數，加入等工作 toohello 批次作業所完成的 hello '未定案' 工作。您通常應該不需要 toomodify 這些檔案。
* hello 作業分隔檔 (JobSplitter.cs)。 此處可供存放用於將作業分割成多個工作的應用程式特定邏輯。

當然您可以加入其他檔案，需要 toosupport 做您工作分隔器的程式碼，視分割邏輯 hello 作業 hello 複雜度而定。

hello 範本也會產生標準的.NET 專案檔，例如.csproj 檔案、 app.config、 packages.config 等等。

hello 本節其餘部分描述 hello 不同的檔案和程式碼結構，並說明每個類別的用途。

![Visual Studio 方案總管中顯示 hello 作業管理員範本解決方案][solution_explorer01]

**架構檔案**

* `Configuration.cs`： 封裝 hello 載入的工作組態資料，例如批次帳戶詳細資料、 連結的儲存體帳戶認證、 作業和工作資訊和作業參數。 它也提供存取 tooBatch 定義環境變數 （請參閱 hello 批次的文件中的工作環境設定） 透過 hello Configuration.EnvironmentVariable 類別。
* `IConfiguration.cs`： 摘要 hello hello 設定類別的實作，單元，讓您可以測試您的工作分隔器使用假或模擬的組態物件。
* `JobManager.cs`： 會協調 hello hello 工作管理員程式元件。 它會負責初始化 hello 作業分隔器，叫用 hello 作業分隔器的 hello 和分派 hello 工作 hello 作業分隔器 toohello 工作傳送者所傳回。
* `JobManagerException.cs`： 表示需要 hello 作業管理員 tooterminate 發生錯誤。 JobManagerException 是使用的 toowrap '必須是' 錯誤，即提供特定的診斷資訊，做為終止的一部分。
* `TaskSubmitter.cs`： 這個類別是負責 tooadding hello 作業分隔器 toohello 批次作業所傳回的工作。 hello JobManager 類別彙總成有效但及時加法 toohello 作業，批次工作 hello 順序，然後在背景執行緒上呼叫 TaskSubmitter.SubmitTasks，每個批次。

**作業分割器**

`JobSplitter.cs`： 這個類別包含應用程式特有邏輯將 hello 工作分割成多個工作。 hello 架構會叫用 hello JobSplitter.Split 方法 tooobtain 一連串的工作，它會將它們做為 hello 方法 toohello 作業傳回。 這是您會在此插入您工作的 hello 邏輯 hello 類別。 實作 hello 分割方法 tooreturn CloudTask 代表 hello 工作要 toopartition hello 作業的執行個體的序列。

**標準 .NET 命令列專案檔**

* `App.config`︰標準的 .NET 應用程式組態檔。
* `Packages.config`︰標準的 NuGet 套件相依性檔案。
* `Program.cs`： 包含 hello 程式進入點和最上層的例外狀況處理。

### <a name="implementing-hello-job-splitter"></a>實作 hello 作業分隔器
當您開啟 hello 作業管理員範本專案時，hello 專案將會有預設開啟的 hello JobSplitter.cs 檔案。 您可以實作 hello 分割您的工作負載中的 hello 工作邏輯使用 hello Split() 方法顯示如下：

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> hello 附註 > 一節中 hello`Split()`方法是 hello 只有 hello 僅供您 toomodify 將 hello 邏輯 toosplit 您的工作新增至不同的工作的作業管理員範本程式碼區段。 如果您想 toomodify hello 範本的其他部分，請確定您以批次的運作方式，請嘗試幾個 hello 和[批次程式碼範例][github_samples]。
> 
> 

Split() 實作具有下列項目的存取權︰

* hello 工作參數，透過 hello`_parameters`欄位。
* hello CloudJob 物件代表 hello 工作，透過 hello`_job`欄位。
* hello CloudTask 物件代表 hello 作業管理員工作，透過 hello`_jobManagerTask`欄位。

您`Split()`實作不直接需要 tooadd 工作 toohello 作業。 相反地，您的程式碼應該傳回 CloudTask 物件序列，這些會被加入 toohello 作業會自動叫用 hello 作業分隔器的 hello 架構類別。 它是一般 toouse C# 的迭代器 (`yield return`) 功能 tooimplement 作業分隔器，因為這可讓 hello 工作 toostart 儘速執行，而不是等待所有工作 toobe 計算。

**作業分割器失敗**

如果作業分割器發生錯誤，它應該︰

* 終止使用 hello C# 的 hello 順序`yield break`陳述式，在其中案例 hello 作業管理員會被處理為成功; 或
* 會擲回例外狀況，case hello 作業管理員會被視為失敗，取決於 hello 用戶端的設定方式，它可能會重試）。

在這兩種情況下，hello 作業分隔器已經傳回的任何工作，並加入的 toohello 批次作業將會符合資格 toorun。 如果您不想這個 toohappen，然後您可以：

* 傳回從 hello 作業分隔器之前終止 hello 工作
* 編寫 hello 整個工作集合，再加以傳回 (也就是傳回`ICollection<CloudTask>`或`IList<CloudTask>`而不是實作您使用的 C# 迭代器的作業分隔器)
* 使用所有的工作取決於 hello hello 作業管理員成功完成的工作相依性 toomake

**作業管理員重試**

如果 hello 作業管理員失敗，可能會重試 hello 批次服務取決於 hello 用戶端重試設定。 一般情況下，這是安全的因為當 hello 架構就會將工作 toohello 作業，它會忽略任何存在的工作。 不過，如果計算的工作是高度耗費資源，您可能不希望 tooincur hello 成本的重新計算已加入 toohello 作業; 的工作相反地，如果 hello 重新執行不是保證的 toogenerate hello 相同工作 Id 則 hello 「 略過重複的項目 」 行為不會開始運作。 在這些情況下，您應該設計工作分隔器 toodetect hello 工作已完成且不重複，例如啟動 tooyield 工作之前執行 CloudJob.ListTasks。

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>結束碼和 hello 作業管理員範本中的例外狀況
結束代碼和例外狀況提供機制 toodetermine hello 結果執行的程式時，它們可協助 tooidentify hello hello 程式執行的任何問題。 hello 作業管理員範本實作 hello 結束碼和本節中所述的例外狀況。

實作與 hello 作業管理員範本的作業管理員工作可能會傳回三個可能的結束代碼：

| 代碼 | 說明 |
| --- | --- |
| 0 |hello 作業管理員已順利完成。 作業的分隔器程式碼執行 toocompletion，和所有工作都已都加入 toohello 作業。 |
| 1 |hello 作業管理員工作失敗，'必須是' hello 程式一部分的例外狀況。 hello 發生例外狀況轉譯的 tooa JobManagerException 與診斷資訊，並解決建議盡可能 hello 失敗。 |
| 2 |hello 作業管理員工作失敗，意外' 的例外狀況。 hello 發生例外狀況記錄的 toostandard 輸出，但 hello 作業管理員無法 tooadd 任何額外的診斷或修復資訊。 |

在作業管理員工作失敗的 hello 情況下，某些工作可能仍已新增 toohello 服務 hello 錯誤發生之前。 這些工作會如常執行。 請參閱上面的「作業分割器失敗」以取得有關此程式碼路徑的討論。

所有例外狀況所傳回的 hello 資訊會寫入 stdout.txt 和 stderr.txt 檔案。 如需詳細資訊，請參閱 [錯誤處理](batch-api-basics.md#error-handling)。

### <a name="client-considerations"></a>用戶端考量
本節說明在根據此範本叫用作業管理員時的一些用戶端實作需求。 請參閱[toopass 參數和環境變數從 hello 用戶端程式碼](#pass-environment-settings)如傳遞參數和環境設定的詳細資訊。

**必要認證**

在訂單 tooadd 工作 toohello Azure 批次作業，hello 作業管理員工作需要您的 Azure Batch 帳戶 URL 和金鑰。 您必須在名為 YOUR_BATCH_URL 和 YOUR_BATCH_KEY 的環境變數中傳遞這些資料。 您可以設定在 hello 作業管理員工作環境設定。 例如，在 C# 用戶端︰

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**儲存體認證**

通常，hello 用戶端不需要 tooprovide hello 連結儲存體帳戶認證 toohello 作業管理員工作 （a） 大部分的工作管理員不需要 tooexplicitly 存取 hello 連結儲存體帳戶，而且 （b) hello 連結儲存體帳戶通常是因為常見的環境設定為 hello 工作 tooall 工作。 如果您未提供 hello 連結 hello 一般環境設定，透過儲存體帳戶，hello 作業管理員需要存取 toolinked 儲存體，然後您就應該提供 hello 連結儲存體認證，如下所示：

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**作業管理員工作設定**

hello 用戶端應該設定 hello 作業管理員*killJobOnCompletion*旗標太**false**。

通常可以放心的 hello 用戶端 tooset *runExclusive*太**false**。

hello 用戶端應使用 hello *resourceFiles*或*applicationPackageReferences*集合 toohave hello 作業管理員可執行檔 （和其所需的 Dll） 部署 toohello 計算節點。

根據預設，hello 作業管理員將不會失敗時的重試。 根據您的工作管理員邏輯 hello 用戶端可能會想透過 tooenable 重試*條件約束*/*maxTaskRetryCount*。

**作業設定**

如果 hello 作業分隔器發出工作具相依性，hello 用戶端必須設定 hello 作業 usesTaskDependencies tootrue。

在 hello 作業分隔器模型中，它並不常見的用戶端 toowish tooadd 工作 toojobs 除了哪些 hello 作業分隔器會建立項目。 hello 用戶端應該因此通常設定 hello 作業*onAllTasksComplete*太**terminatejob**。

## <a name="task-processor-template"></a>工作處理器範本
工作處理器範本可協助您 tooimplement 工作處理器可以執行下列動作的 hello:

* 設定所需的每個批次工作 toorun hello 資訊。
* 執行每個 Batch 工作所需的所有動作。
* 儲存工作輸出 toopersistent 儲存體。

雖然工作處理器不需要的 toorun 工作批次，但 hello 主要優點使用工作處理器是它提供包裝函式 tooimplement 某一個位置中的所有工作執行動作。 例如，如果您需要 toorun hello 內容中數個應用程式的每項工作，或如果您需要 toocopy toopersistent 儲存資料之後完成各項工作。

hello hello 工作處理器所執行的動作可能也為簡單或複雜，和最大數量越少，所需的工作負載。 此外，藉由實作所有的工作動作到一個工作的處理器，您可以輕易地更新或新增根據變更 tooapplications 或工作負載需求的動作。 不過，在某些情況下工作處理器可能會無法 hello 最佳化解決方案實作作為它可以將不必要的複雜性，例如當執行可以快速地從簡單的命令列啟動的工作。

### <a name="create-a-task-processor-using-hello-template"></a>建立工作處理器使用 hello 範本
tooadd 工作處理器 toohello 建立的方案，您更早版本，請遵循下列步驟：

1. 在 Visual Studio 中開啟現有方案。
2. 在 方案總管 中，以滑鼠右鍵按一下 hello 方案中，按一下 **新增**，然後按一下**新專案**。
3. 在 Visual C# 底下按一下 雲端，然後按一下Azure Batch 工作處理器。
4. 輸入的名稱來描述您的應用程式，以及識別這個專案時 （例如 hello 工作處理器"LitwareTaskProcessor")。
5. toocreate hello 專案中，按一下 **確定**。
6. 最後，建置 hello 專案 tooforce Visual Studio tooload 所有參考的 NuGet 封裝，並 hello 專案的 tooverify 有效，然後再開始進行修改。

### <a name="task-processor-template-files-and-their-purpose"></a>工作處理器範本檔案及其用途
當您使用範本建立專案 hello 工作處理器時，它會產生三個群組的程式碼檔案：

* hello 主要程式檔案 (Program.cs)。 這包含 hello 程式進入點和最上層的例外狀況處理。 您通常不應該這樣需要 toomodify。
* hello Framework 目錄。 這包含 hello 檔案負責 hello 工作管理員程式-解除封裝參數，加入等工作 toohello 批次作業所完成的 hello '未定案' 工作。您通常應該不需要 toomodify 這些檔案。
* hello 工作處理器檔案 (TaskProcessor.cs)。 這是您將在其中放置您應用程式特定的邏輯 （通常是藉由呼叫出 tooan 現有可執行檔） 執行工作。 前置和後置處理程式碼 (例如下載額外資料或上傳結果檔案) 也存放在此。

當然您可以加入其他檔案，需要 toosupport 做您工作處理器的程式碼，視分割邏輯 hello 作業 hello 複雜度而定。

hello 範本也會產生標準的.NET 專案檔，例如.csproj 檔案、 app.config、 packages.config 等等。

hello 本節其餘部分描述 hello 不同的檔案和程式碼結構，並說明每個類別的用途。

![Visual Studio 方案總管中顯示 hello 工作處理器範本解決方案][solution_explorer02]

**架構檔案**

* `Configuration.cs`： 封裝 hello 載入的工作組態資料，例如批次帳戶詳細資料、 連結的儲存體帳戶認證、 作業和工作資訊和作業參數。 它也提供存取 tooBatch 定義環境變數 （請參閱 hello 批次的文件中的工作環境設定） 透過 hello Configuration.EnvironmentVariable 類別。
* `IConfiguration.cs`： 摘要 hello hello 設定類別的實作，單元，讓您可以測試您的工作分隔器使用假或模擬的組態物件。
* `TaskProcessorException.cs`： 表示需要 hello 作業管理員 tooterminate 發生錯誤。 TaskProcessorException 是使用的 toowrap '必須是' 錯誤，即提供特定的診斷資訊，做為終止的一部分。

**工作處理器**

* `TaskProcessor.cs`： 執行 hello 工作。 hello 架構會叫用 hello TaskProcessor.Run 方法。 這是工作的您會在此插入您 hello 特定應用程式邏輯 hello 類別。 實作 hello Run 方法：
  * 剖析及驗證任何工作參數
  * 撰寫 hello 命令列的任何外部程式，您想 tooinvoke
  * 記錄為了偵錯所可能需要的任何診斷資訊
  * 使用該命令列開始處理序
  * 等候 hello 程序 tooexit
  * 擷取 hello 程序 toodetermine hello 結束代碼，如果它是成功或是失敗
  * 儲存所有您想要的輸出檔案 tookeep toopersistent 儲存體

**標準 .NET 命令列專案檔**

* `App.config`︰標準的 .NET 應用程式組態檔。
* `Packages.config`︰標準的 NuGet 套件相依性檔案。
* `Program.cs`： 包含 hello 程式進入點和最上層的例外狀況處理。

## <a name="implementing-hello-task-processor"></a>實作 hello 工作處理器
當您開啟 hello 工作處理器範本專案時，hello 專案將會有預設開啟的 hello TaskProcessor.cs 檔案。 您可以實作您的工作負載中的 hello 工作執行的 hello 邏輯使用 hello run （） 方法，如下所示：

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> hello hello run （） 方法中的註解式的區段是 hello 只有 hello 工作處理器範本之程式碼區段供您 toomodify 加入您的工作負載中的 hello 工作的 hello 執行邏輯。 如果您想 toomodify hello 範本的其他部分，請先熟悉批次檢閱 hello 批次的文件，並嘗試幾個 hello 批次的程式碼範例的運作方式。
> 
> 

hello run （） 方法負責啟動 hello 命令列、 啟動一或多個處理序，等候所有處理序 toocomplete、 儲存 hello 結果，以及最後傳回，結束代碼。 hello run （） 方法是您用來實作 hello 處理您的工作的邏輯。 hello 工作處理器架構會叫用 hello run （） 方法。您不需要 toocall 它自己。

Run() 實作具有下列項目的存取權︰

* hello 工作參數，透過 hello`_parameters`欄位。
* hello 作業和工作的識別碼，透過 hello`_jobId`和`_taskId`欄位。
* hello 工作設定，透過 hello`_configuration`欄位。

**工作失敗**

發生失敗時，您可以結束 hello run （） 方法擲回例外狀況，但這會保留 hello 上方層級例外狀況處理常式中的 hello 工作結束代碼的控制項。 或如果您需要 toocontrol hello 結束代碼，以便您可以進行診斷，例如區分不同類型的失敗，因為某些失敗模式應該終止 hello 工作和其他項目不應該則您應該藉由傳回結束 hello run （） 方法非零結束代碼。 這會成為 hello 工作結束代碼。

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>結束碼和 hello 工作處理器範本中的例外狀況
結束代碼和例外狀況提供機制 toodetermine hello 結果執行的程式時，它們可協助您識別 hello hello 程式執行的任何問題。 hello 工作處理器範本實作 hello 結束碼和本節中所述的例外狀況。

實作與 hello 處理器工作範本的工作處理器工作可能會傳回三個可能的結束代碼：

| 代碼 | 說明 |
| --- | --- |
| [Process.ExitCode][process_exitcode] |hello 工作處理器已 toocompletion。 請注意，這不表示您叫用該 hello 程式已順利完成，只有該 hello 工作處理器順利叫用及執行任何後置處理，沒有例外狀況。 hello hello 結束程式碼的意義取決於 hello 叫用程式 – 通常結束碼 0 表示成功 hello 程式和任何其他的結束代碼表示 hello 程式失敗。 |
| 1 |hello 工作處理器失敗 '必須是' hello 程式一部分的例外狀況。 hello 發生例外狀況轉譯的 tooa`TaskProcessorException`與診斷資訊以及解決建議盡可能 hello 失敗。 |
| 2 |hello 工作處理器無法以 '預期' 的例外狀況。 hello 例外狀況記錄的 toostandard 輸出，但 hello 工作處理器是無法 tooadd 任何額外的診斷或修復資訊。 |

> [!NOTE]
> 如果您叫用的 hello 程式使用結束碼 1 和 2 tooindicate 特定失敗模式，然後使用工作處理器錯誤結束代碼 1 和 2 模稜兩可。 您可以變更這些工作處理器錯誤代碼 toodistinctive 結束代碼，藉由編輯 hello Program.cs 檔案中的 hello 例外狀況。
> 
> 

所有例外狀況所傳回的 hello 資訊會寫入 stdout.txt 和 stderr.txt 檔案。 如需詳細資訊，請參閱錯誤處理，hello 批次的文件。

### <a name="client-considerations"></a>用戶端考量
**儲存體認證**

如果您工作的處理器會使用 Azure blob 儲存體 toopersist 輸出，例如使用 hello 檔慣例協助程式程式庫，則它需要存取太*任一*hello 雲端儲存體帳戶認證*或*blob 容器 URL，其中包含共用的存取簽章 (SAS)。 hello 範本包括提供認證能夠透過常見的環境變數的支援。 您的用戶端可以傳遞 hello 儲存體認證，如下所示：

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

hello 儲存體帳戶位於然後 hello TaskProcessor 類別，透過 hello`_configuration.StorageAccount`屬性。

如果您偏好 toouse SAS 的容器 URL，您也可以將這個工作一般環境設定，透過但 hello 工作處理器範本目前不包括內建支援。

**儲存體設定**

建議的 hello 的用戶端或作業管理員工作建立任何所需的工作，然後再加入 hello 工作 toohello 工作的容器。 這是強制性，如果您使用 SAS 容器 URL，因此 URL 未包含的權限 toocreate hello 容器。 建議即使傳遞儲存體帳戶認證，因為它會將儲存每個工作各自 toocall CloudBlobContainer.CreateIfNotExistsAsync 具有 hello 容器。

## <a name="pass-parameters-and-environment-variables"></a>傳遞參數和環境變數
### <a name="pass-environment-settings"></a>傳遞環境設定
用戶端傳遞資訊的環境設定 hello 形式 toohello 作業管理員工作。 這項資訊然後 hello 作業管理員工作所使用，當產生 hello 工作的處理器工作會執行一部分 hello 計算作業。 您可以傳遞做為環境設定的 hello 資訊的範例如下：

* 儲存體帳戶名稱和帳戶金鑰
* Batch 帳戶 URL
* Batch 帳戶金鑰

hello 批次服務有簡單的機制，toopass 環境設定 tooa 作業管理員工作使用 hello`EnvironmentSettings`屬性[Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask]。

例如，tooget hello`BatchClient`執行個體批次帳戶，您可以將傳遞為環境變數從 hello 用戶端 hello URL 的程式碼和共用金鑰 hello 批次帳戶的認證。 同樣地，tooaccess hello 儲存體帳戶連結 toohello 批次帳戶，您可以為環境變數傳遞 hello 儲存體帳戶名稱和 hello 儲存體帳戶金鑰。

### <a name="pass-parameters-toohello-job-manager-template"></a>傳遞參數 toohello 作業管理員範本
在許多情況下，它有用 toopass 每個作業參數 toohello 作業管理員工作，可能是 toocontrol hello 工作分割程序或 tooconfigure hello 工作 hello 作業。 您可以上傳 parameters.json 稱為 hello 作業管理員工作的資源檔的 JSON 檔案。 hello 參數可供在 hello `JobSplitter._parameters` hello 作業管理員範本中的欄位。

> [!NOTE]
> hello 內建的參數處理常式支援只有字串的字串字典。 如果您想 toopass 複雜 JSON 值做為參數值時，您將需要 toopass 這些字串的形式和剖析它們在 hello 作業分隔器，或修改 hello framework`Configuration.GetJobParameters`方法。
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>傳遞參數 toohello 處理器工作範本
您也可以傳遞參數 tooindividual 工作使用 hello 工作處理器樣板實作。 就像 hello 作業管理員範本，與 hello 工作處理器範本會尋找名為

parameters.json 和如果找到它載入為 hello 參數字典。 有幾個選項的方式 toopass 參數 toohello 工作處理器工作：

* 重複使用 JSON 的 hello 作業參數。 這適用於 hello 參數可用作業範圍 （適用於範例中，呈現高度和寬度） 的情況。 toodo，建立時 CloudTask hello 作業分隔器中，新增參考 toohello parameters.json 資源檔案物件從 hello 作業管理員工作的 ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask ResourceFiles 集合。
* 產生並上傳工作特有 parameters.json 文件一部分的分隔器執行作業，以及參考該 hello 工作的資源檔案集合中的 blob。 如果不同的工作有不同的參數，就必須這麼做。 範例可能是其中 hello 框架索引時，會當做參數傳遞 toohello 工作的 3D 轉譯案例。

> [!NOTE]
> hello 內建的參數處理常式支援只有字串的字串字典。 如果您想 toopass 複雜 JSON 值做為參數值時，您將需要 toopass 這些字串的形式和剖析它們在 hello 工作處理器，或修改 hello framework`Configuration.GetTaskParameters`方法。
> 
> 

## <a name="next-steps"></a>後續步驟
### <a name="persist-job-and-task-output-tooazure-storage"></a>保存工作和工作輸出 tooAzure 儲存體
開發 Batch 解決方案時的另一個實用工具是 [Azure Batch 檔案慣例][nuget_package]。 使用這個.NET 類別庫 （目前處於預覽階段） 在批次.NET 應用程式 tooeasily 存放區，並擷取工作輸出 tooand 從 Azure 儲存體。 [保存 Azure 批次作業和工作的輸出](batch-task-output.md)包含 hello 程式庫和其使用方式的完整討論。

### <a name="batch-forum"></a>Batch 論壇
hello [Azure Batch 論壇][ forum] MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。 請前去查看很有幫助的「便利貼」文章，在建立 Batch 解決方案時，出現問題就張貼。

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
