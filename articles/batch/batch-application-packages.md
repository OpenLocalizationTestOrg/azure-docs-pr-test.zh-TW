---
title: "計算節點-Azure 批次上的 aaaInstall 應用程式封裝 |Microsoft 文件"
description: "使用 hello 應用程式封裝功能的 Azure 批次 tooeasily 管理多個應用程式，並可在批次上安裝的版本的計算節點。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>部署應用程式 toocompute 節點與批次應用程式套件

Azure 批次的 hello 應用程式封裝的功能提供便於管理工作的應用程式和其部署 toohello 計算集區中的節點。 與應用程式封裝，您可以上傳和管理多個版本的 hello 應用程式執行您的工作，包括其支援的檔案。 然後您可以自動部署一或多個這些應用程式 toohello 計算集區中的節點。

在本文中，您將學習如何 tooupload 和管理在 hello Azure 入口網站中的應用程式封裝。 然後您將學習 tooinstall 如何當它們在集區的計算節點與 hello[批次.NET] [ api_net]程式庫。

> [!NOTE]
> 
> 在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。 只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。 建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。
>
> hello 應用程式開發介面來建立和管理應用程式套件屬於 hello [Batch Management.NET] [[api_net_mgmt]] 文件庫。 hello 計算節點上安裝應用程式封裝的應用程式開發介面屬於 hello[批次.NET] [ api_net]程式庫。  
>
> 此處所述的 hello 應用程式套件 」 功能會取代 hello 批次應用程式中可用功能，舊版的 hello 服務。
> 
> 

## <a name="application-package-requirements"></a>應用程式封裝需求
toouse 應用程式封裝，您需要太[Azure 儲存體帳戶連結](#link-a-storage-account)tooyour Batch 帳戶。

已引入此功能[批次 REST API] [ api_rest]版本 2015年-12-01.2.2 和 hello 對應[批次.NET] [ api_net]程式庫版本3.1.0 來執行實驗。 我們建議使用批次時，一律使用最新 API 版本 hello。

> [!NOTE]
> 在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。 只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。 建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。
>
>

## <a name="about-applications-and-application-packages"></a>關於應用程式和應用程式封裝
Azure 批次內*應用程式*參考 tooa 組的建立版本的二進位檔可以自動下載的 toohello 計算節點的 程式集區。 *應用程式封裝*參考 tooa*組特定*這些二進位檔和代表給定*版本*hello 應用程式。

![應用程式和應用程式套件的高階圖表][1]

### <a name="applications"></a>應用程式
批次中的應用程式包含一或多個應用程式封裝，然後指定 hello 應用程式的組態選項。 例如，應用程式可以指定 hello 預設應用程式封裝版本 tooinstall 計算節點和其封裝是否可以更新或刪除。

### <a name="application-packages"></a>應用程式封裝
應用程式封裝是包含 hello 應用程式二進位檔.zip 檔案，以及所需的工作 toorun hello 應用程式支援檔案。 每個應用程式封裝代表 hello 應用程式的特定版本。

您可以指定在 hello 集區和工作層級的應用程式封裝。 當您建立集區或工作時，您可以指定這些套件之中的一個或多個，以及 (選擇性) 指定版本。

* **集區的應用程式封裝**太部署*每*hello 集區中的節點。 當節點加入集區以及重新啟動或重新安裝映像時，就會部署應用程式。
  
    當集區中的所有節點都執行某作業的工作時，便適合使用集區應用程式套件。 您可以在建立集區時指定一或多個應用程式套件，而且可以新增或更新現有集區的套件。 如果您更新現有的集區的應用程式封裝，您必須重新啟動節點 tooinstall hello 新封裝。
* **工作應用程式封裝**tooa 計算節點排程 toorun 工作之前執行 hello 工作的命令列只會部署。 如果 hello 指定應用程式套件與版本已 hello 節點上，未重新部署，使用 hello 現有套件。
  
    工作應用程式封裝是有用的共用集區，其中一個集區中，執行不同的工作，且環境中的工作完成時，不會刪除 hello 集區。 如果作業有 hello 集區中的節點比有較少的工作，工作應用程式封裝可以減少資料傳輸因為您的應用程式是執行工作的已部署的唯一 toohello 節點。
  
    其他可受益於工作應用程式套件的情節為執行大型應用程式，但只用於少數工作的作業。 例如，前置處理階段或合併工作，其中 hello 前置處理或合併式應用程式是重量級，可能會受益於使用工作應用程式套件。

> [!IMPORTANT]
> 有一些限制和 hello 應用程式最大封裝大小上的應用程式和批次帳戶內的應用程式套件的 hello 數目。 請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)這些限制的詳細資料。
> 
> 

### <a name="benefits-of-application-packages"></a>應用程式封裝的優點
應用程式封裝可以簡化 hello 批次的解決方案和低 hello 負擔必要的 toomanage hello 執行應用程式，您的工作中的程式碼。

應用程式封裝與集區的啟動工作沒有 toospecify 一長串的個別資源檔案 tooinstall hello 節點上。 您不需要 toomanually 管理應用程式檔案的 Azure 儲存體，或在節點上的多個版本。 而且，您不需要有關產生 tooworry [SAS Url](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide 存取 toohello 檔案在儲存體帳戶。 批次與 Azure 儲存體 toostore 應用程式套件的 hello 背景的運作方式，並將其部署 toocompute 節點。

> [!NOTE] 
> hello 啟動工作的總大小必須小於或等於 too32768 字元，包括資源檔和環境變數。 如果啟動工作超過此限制，就可另外選擇使用應用程式套件。 您可以也建立 zip 的封存包含資源檔、 將它上傳為 blob tooAzure 存放裝置，且然後將它解壓縮從 hello 命令列啟動工作。 
>
>

## <a name="upload-and-manage-applications"></a>上傳及管理應用程式
您可以使用 hello [Azure 入口網站][ portal]或 hello [Batch Management.NET](batch-management-dotnet.md)文件庫 toomanage hello 批次帳戶中的應用程式封裝。 在 hello 接下來的幾個章節，我們先說明如何 toolink 儲存體帳戶，然後討論新增應用程式及封裝並進行管理與 hello 入口網站。

### <a name="link-a-storage-account"></a>連結儲存體帳戶
toouse 應用程式封裝，您必須先連結的 Azure 儲存體帳戶 tooyour Batch 帳戶。 如果您尚未設定儲存體帳戶，hello Azure 入口網站會顯示警告 hello 第一次按一下 hello**應用程式**磚中 hello**批次帳戶**刀鋒視窗。

> [!IMPORTANT]
> 目前批次支援*只*hello**一般用途**步驟 5 中所述，儲存體帳戶類型[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)，請在[關於 Azure儲存體帳戶](../storage/common/storage-create-storage-account.md)。 當您將連結的 Azure 儲存體帳戶 tooyour 批次帳戶時，連結*只***一般用途**儲存體帳戶。
> 
> 

![Azure 入口網站中的「未設定儲存體帳戶」警告][9]

hello 批次服務會使用 hello 相關聯的儲存體帳戶 toostore 應用程式封裝。 連結 hello 兩個帳戶後，批次可自動部署 hello 封裝儲存在 hello 連結儲存體帳戶 tooyour 計算節點。 按一下 toolink 批次帳戶的儲存體帳戶 tooyour**儲存體帳戶設定**上 hello**警告**刀鋒視窗中，然後再按一下**儲存體帳戶**上 hello **儲存體帳戶**刀鋒視窗。

![Azure 入口網站中的選擇儲存體帳戶刀鋒視窗][10]

我們建議您建立「專門」用來與 Batch 帳戶搭配使用的儲存體帳戶，並在此處選取它。 如需詳細資訊，關於如何 toocreate 儲存體帳戶，請參閱 「 建立儲存體帳戶 」 中的[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 在您建立儲存體帳戶後，您可以再將它連結 tooyour 批次帳戶使用 hello**儲存體帳戶**刀鋒視窗。

> [!WARNING]
> hello 批次服務會使用 Azure 儲存體 toostore 應用程式封裝做為區塊 blob。 您是[收費像平常一樣][ storage_pricing] hello 區塊 blob 資料。 會確定 tooconsider hello 大小和數目的應用程式封裝，而定期移除已被取代的封裝 toominimize 成本。
> 
> 

### <a name="view-current-applications"></a>檢視目前的應用程式
在您的 Batch 帳戶 tooview hello 應用程式按一下 hello**應用程式**檢視 hello 時 hello 左側功能表中的功能表項目**批次帳戶**刀鋒視窗。

![應用程式圖格][2]

選取此功能表選項會開啟 hello**應用程式**刀鋒視窗中：

![列出應用程式][3]

hello**應用程式**刀鋒視窗會顯示 hello 您的帳戶中的每個應用程式識別碼及 hello 下列屬性：

* **封裝**: hello 與此應用程式相關聯的版本數目。
* **預設版本**: hello 如果當您指定 hello 應用程式集區並不表示版本安裝的應用程式版本。 這項設定是選擇性的。
* **允許更新**： 允許 hello 值，指定封裝是否更新、 刪除和新增項目。 如果設定太**否**，封裝更新和刪除停用 hello 應用程式。 而只能新增新的應用程式封裝版本。 hello 預設值是**是**。

### <a name="view-application-details"></a>檢視應用程式詳細資料
tooopen hello 刀鋒視窗，其中包含 hello 應用程式，請選取 hello 應用程式的詳細資料中 hello**應用程式**刀鋒視窗。

![應用程式詳細資料][4]

在 hello 應用程式詳細資料 刀鋒視窗，您可以設定下列應用程式設定的 hello。

* **允許更新**：指定是否可更新或刪除應用程式的應用程式套件。 請參閱本文稍後的＜更新或刪除應用程式封裝＞。
* **預設版本**： 指定預設應用程式封裝 toodeploy toocompute 節點。
* **顯示名稱**： 指定易記名稱，您解決方案可以使用時它會顯示 hello 應用程式的相關資訊，例如 hello 提供 tooyour 客戶透過批次服務的 UI 中的批次。

### <a name="add-a-new-application"></a>加入新的應用程式
toocreate 新的應用程式中，加入應用程式封裝，並指定新的、 唯一的應用程式識別碼。 hello 第一個應用程式套件，您將加入新的應用程式識別碼 hello 也會建立 hello 新應用程式。

按一下**新增**上 hello**應用程式**刀鋒視窗 tooopen hello**新的應用程式**刀鋒視窗。

![Azure 入口網站中的新增應用程式刀鋒視窗][5]

hello**新的應用程式**刀鋒視窗提供 hello 下列欄位 toospecify hello 設定新的應用程式和應用程式套件。

**應用程式識別碼**

此欄位會指定新的應用程式，也就是主體 toohello 標準 Azure 批次識別碼的驗證規則的 hello 識別碼。 提供應用程式識別碼 hello 規則如下所示：

* Windows 節點上 hello 識別碼可包含英數字元、 連字號及底線的任何組合。 在 Linux 節點上，只允許使用英數字元和底線。
* 不能包含超過 64 個字元。
* 必須是唯一 hello 批次帳戶內。
* 需保留大小寫和區分大小寫。

**版本**

此欄位指定 hello hello 您上傳的應用程式封裝版本。 版本字串為主體 toohello 下列驗證規則：

* Windows 節點上 hello 版本字串可以包含英數字元、 連字號、 底線和句號的任何組合。 在 Linux 節點上 hello 版本字串只能包含英數字元和底線。
* 不能包含超過 64 個字元。
* 必須是唯一 hello 應用程式中。
* 需保留大小寫和區分大小寫。

**應用程式封裝**

此欄位會指定包含 hello 應用程式二進位檔的 hello.zip 檔案，以及所需的 tooexecute hello 應用程式支援檔案。 按一下 hello**選取檔案**方塊或 hello 資料夾圖示 toobrowse tooand 選取包含您的應用程式檔案的.zip 檔案。

您已選取檔案之後，請按一下**確定**toobegin hello 上載 tooAzure 儲存體。 Hello 上傳作業完成時，hello 入口網站會顯示通知，並關閉 [hello] 刀鋒視窗。 根據您所上傳和 hello 您的網路連線速度的 hello 檔案 hello 大小，這項作業可能需要一些時間。

> [!WARNING]
> 請勿關閉 hello**新的應用程式**hello 上傳作業完成之前的刀鋒視窗。 如此一來，將會停止 hello 上傳程序。
> 
> 

### <a name="add-a-new-application-package"></a>加入新應用程式封裝
tooadd 新的應用程式封裝版本的現有應用程式中，選取應用程式在 hello**應用程式**刀鋒視窗中，按一下 **封裝**，然後按一下 **新增**tooopenhello**新增封裝**刀鋒視窗。

![Azure 入口網站中的新增應用程式套件刀鋒視窗][8]

如您所見，hello 欄位相符的 hello**新的應用程式**刀鋒視窗中，但 hello**應用程式識別碼**方塊已停用。 您可以如同 hello 新應用程式，指定 hello**版本**新套件中，瀏覽 tooyour**應用程式封裝**.zip 檔案，然後按一下  **確定** tooupload hello封裝。

### <a name="update-or-delete-an-application-package"></a>更新或刪除應用程式封裝
tooupdate 或刪除現有的應用程式封裝，開啟 hello hello 應用程式的詳細資料 刀鋒視窗按一下**封裝**tooopen hello**封裝**刀鋒視窗中，按一下 hello**省略**hello toomodify，並選取您想要 tooperform 的 hello 動作 hello 應用程式封裝的資料列中。

![在 Azure 入口網站中更新或刪除套件][7]

更新

當您按一下**更新**，hello*更新套件*刀鋒視窗會顯示。 此刀鋒視窗會類似 toohello*新應用程式封裝*刀鋒視窗中，但只 hello 封裝選取項目欄位才會啟用，讓您新增的 ZIP 檔案 tooupload toospecify。

![Azure 入口網站中的更新套件刀鋒視窗][11]

**刪除**

當您按一下**刪除**，系統會要求您 tooconfirm hello 刪除 hello 封裝版本，和批次刪除 hello 封裝從 Azure 儲存體。 如果您刪除 hello 預設版本的應用程式，hello**預設版本**hello 應用程式已移除設定。

![刪除應用程式][12]

## <a name="install-applications-on-compute-nodes"></a>將應用程式安裝在計算節點上
既然您已經學會如何 toomanage 應用程式封裝以 hello Azure 入口網站，我們可以在討論如何 toodeploy 它們 toocompute 節點與批次工作加以執行。

### <a name="install-pool-application-packages"></a>安裝集區應用程式套件
tooinstall 上所有應用程式封裝中集區的計算節點中，指定一或多個應用程式封裝*參考*hello 集區。 您指定的集區的 hello 應用程式封裝會安裝每個計算節點上，當該節點加入 hello 集區，以及當 hello 節點重新啟動或重新安裝映像。

在 Batch .NET 中，請在建立新集區時指定一或多個 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]，或為現有集區指定。 hello [ApplicationPackageReference] [ net_pkgref]類別會指定應用程式識別碼和版本的集區上的 tooinstall 計算節點。

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> 如果應用程式套件部署失敗，因為任何原因，hello 批次服務標 hello 節點[無法使用][net_nodestate]，和任何工作都會排定執行該節點上。 在此情況下，您應該**重新啟動**hello 節點 tooreinitiate hello 封裝部署。 重新啟動的 hello 節點也可以讓工作一次排程 hello 節點上。
> 
> 

### <a name="install-task-application-packages"></a>安裝工作應用程式套件
類似 tooa 集區中，指定應用程式套件*參考*工作。 在節點上的排程的 toorun 工作時，hello 封裝會下載並解壓縮之前執行 hello 工作的命令列。 如果 hello 節點上已安裝指定的封裝和版本，不會下載 hello 封裝，且 hello 現有的封裝。

tooinstall 工作應用程式封裝時，設定 hello 工作[CloudTask][net_cloudtask]。[ApplicationPackageReferences] [ net_cloudtask_pkgref]屬性：

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>執行 hello 安裝應用程式
hello 您所指定的集區或工作的封裝會下載並解壓縮 tooa 名為目錄內 hello `AZ_BATCH_ROOT_DIR` hello 節點。 批次也會建立包含名為目錄 hello 路徑 toohello 的環境變數。 參考 hello hello 節點上的應用程式時，您的工作命令列會使用這個環境變數。 

Windows 節點上 hello 變數是在 hello 下列格式：

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

在 Linux 節點上 hello 格式有些許不同。 句號 （.）、 連字號 （-） 和數字符號 （#） 都是扁平化的 toounderscores hello 環境變數中。 例如：

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`和`version`對應 toohello 應用程式和套件版本您為部署指定的值。 例如，如果您指定應用程式的版本 2.7 *blender*應該安裝 Windows 節點上的所有工作的命令列會都使用這個環境變數 tooaccess 及其檔案：

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

在 Linux 節點上指定 hello 環境變數以下列格式：

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

當您上傳應用程式封裝時，您可以指定預設版本 toodeploy tooyour 計算節點。 如果您已經指定應用程式的預設版本，您就可以省略 hello 版本尾碼，當您參考 hello 應用程式。 中所示，您可以在 hello hello 應用程式 刀鋒視窗上的 Azure 入口網站中指定 hello 預設應用程式版本[上傳和管理應用程式](#upload-and-manage-applications)。

例如，如果您設定 hello 應用程式的預設版本為"2.7" *blender*，而且您的工作參考 hello 下列環境變數，則 Windows 節點將會執行版本 2.7:

`AZ_BATCH_APP_PACKAGE_BLENDER`

hello 下列程式碼片段示範工作命令列範例，可啟動 hello 預設版的 hello *blender*應用程式：

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> 請參閱[工作的環境設定](batch-api-basics.md#environment-settings-for-tasks)在 hello[批次功能概觀](batch-api-basics.md)計算節點環境設定的詳細資訊。
> 
> 

## <a name="update-a-pools-application-packages"></a>更新集區的應用程式封裝
如果現有的集區已設定與應用程式套件，您可以指定新套件 hello 集區。 如果您指定的集區 hello 遵循套用新的封裝參考：

* hello 批次服務會在任何現有的節點重新啟動或重新安裝映像和新加入 hello 集區的所有節點上安裝 hello 新指定的封裝。
* 計算您 hello 封裝參考更新時就已位於 hello 集區的節點不會自動安裝新應用程式封裝 hello。 這些運算節點必須重新開機或安裝映像的 tooreceive hello 新的封裝。
* 部署新的封裝時，環境變數建立 hello 反映 hello 新應用程式封裝參考。

在此範例中，hello 現有集區具有 hello 2.7 版*blender*應用程式設定為其中一個其[CloudPool][net_cloudpool]。[ApplicationPackageReferences][net_cloudpool_pkgref]。 與版本 2.76b，tooupdate hello 集區的節點指定新[ApplicationPackageReference] [ net_pkgref] hello 新版本，與認可 hello 變更。

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

既然 hello 已設定新的版本，hello 批次服務會安裝版本 2.76b tooany*新*加入 hello 集區的節點。 hello 節點上的 tooinstall 2.76b*已經*hello 集區，在重新開機，或它們重新製作映像。 請注意，重新啟動的節點從先前的封裝部署的 hello 檔案。

## <a name="list-hello-applications-in-a-batch-account"></a>Hello 應用程式清單中的批次帳戶
您可以使用 hello 列出 hello 應用程式和其封裝中的批次帳戶[ApplicationOperations][net_appops]。[ListApplicationSummaries] [ net_appops_listappsummaries]方法。

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>總結
應用程式封裝，您可以幫助您選取 hello 應用程式為了完成其工作，並指定 hello 確切版本 toouse 時處理工作與批次啟用服務的客戶。 您也可能會提供客戶 tooupload hello 能力，並追蹤其自身應用程式在您的服務。

## <a name="next-steps"></a>後續步驟
* hello[批次 REST API] [ api_rest]也提供支援 toowork 與應用程式套件。 例如，請參閱 hello [applicationPackageReferences] [ rest_add_pool_with_packages]中的項目[加入集區 tooan 帳戶][ rest_add_pool]如需如何資訊使用 REST API hello toospecify 封裝 tooinstall。 請參閱[應用程式][ rest_applications]如需如何使用 tooobtain 應用程式資訊 hello 批次 REST API 詳細資料。
* 深入了解如何 tooprogrammatically[管理 Azure Batch 帳戶與配額使用 Batch Management.NET](batch-management-dotnet.md)。 hello [Batch Management.NET][api_net_mgmt]程式庫可以啟用的批次應用程式或服務的帳戶建立和刪除功能。

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "應用程式套件高階圖表"
[2]: ./media/batch-application-packages/app_pkg_02.png "Azure 入口網站中的應用程式圖格"
[3]: ./media/batch-application-packages/app_pkg_03.png "Azure 入口網站中的應用程式刀鋒視窗"
[4]: ./media/batch-application-packages/app_pkg_04.png "Azure 入口網站中的應用程式詳細資料刀鋒視窗"
[5]: ./media/batch-application-packages/app_pkg_05.png "Azure 入口網站中的新增應用程式刀鋒視窗"
[7]: ./media/batch-application-packages/app_pkg_07.png "Azure 入口網站中的更新或刪除套件下拉式清單"
[8]: ./media/batch-application-packages/app_pkg_08.png "Azure 入口網站中的新增應用程式套件刀鋒視窗"
[9]: ./media/batch-application-packages/app_pkg_09.png "沒有連結的儲存體帳戶警示"
[10]: ./media/batch-application-packages/app_pkg_10.png "Azure 入口網站中的選擇儲存體帳戶刀鋒視窗"
[11]: ./media/batch-application-packages/app_pkg_11.png "Azure 入口網站中的更新套件刀鋒視窗"
[12]: ./media/batch-application-packages/app_pkg_12.png "Azure 入口網站中的刪除套件確認對話方塊"
