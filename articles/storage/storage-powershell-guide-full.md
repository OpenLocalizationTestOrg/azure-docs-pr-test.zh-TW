---
title: "與 Azure 儲存體的 Azure PowerShell aaaUsing |Microsoft 文件"
description: "了解 toouse hello 適用於 Azure 儲存體 toocreate Azure PowerShell cmdlet，並管理儲存體帳戶。使用 blob、 資料表、 佇列和檔案。設定並查詢儲存體分析，並建立共用的存取簽章。"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>搭配使用 Azure PowerShell 與 Azure 儲存體
## <a name="overview"></a>概觀
Azure PowerShell 是提供 cmdlet toomanage 透過 Windows PowerShell 的 Azure 模組。 它是以工作為基礎的命令列殼層和指令碼語言，特別為系統管理所設計。 使用 PowerShell，您可以輕鬆地控制及自動化 hello 管理您的 Azure 服務和應用程式。 例如，您可以使用相同的工作，您可以執行透過 hello hello cmdlet tooperform hello [Azure 入口網站](https://portal.azure.com)。

本指南中，我們將探討如何 toouse hello [Azure 儲存體 Cmdlet](/powershell/module/azurerm.storage/#storage) tooperform 各種開發和管理工作與 Azure 儲存體。

本指南假設您過去有使用 [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)和 [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx) 的經驗。 hello 指南提供的指令碼數目 toodemonstrate hello PowerShell 與 Azure 儲存體使用量。 您應該更新 hello 指令碼變數，根據您的設定，才能執行每個指令碼。

本指南中的 hello 第一節提供 Azure 儲存體和 PowerShell 快速概覽。 如需詳細的資訊和指示，請從 hello 啟動[與 Azure 儲存體使用 Azure PowerShell 的必要條件](#prerequisites-for-using-azure-powershell-with-azure-storage)。

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>在 5 分鐘內開始使用 Azure 儲存體和 PowerShell
本節說明如何在 5 分鐘內 tooaccess 透過 PowerShell 的 Azure 儲存體。

**新 tooAzure:**取得 Microsoft Azure 訂用帳戶和該訂用帳戶相關聯的 Microsoft 帳戶。 如需 Azure 購買選項的資訊，請參閱[免費試用](https://azure.microsoft.com/pricing/free-trial/)、[購買選項](https://azure.microsoft.com/pricing/purchase-options/)和[會員優惠](https://azure.microsoft.com/pricing/member-offers/) (適用於 MSDN、Microsoft 合作夥伴網路、BizSpark 和其他 Microsoft 方案的成員)。

如需 Azure 訂用帳戶的詳細資訊，請參閱 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](https://msdn.microsoft.com/library/azure/hh531793.aspx) 。

**建立 Microsoft Azure 訂用帳戶和帳戶之後：**

1. 下載並安裝最新的 hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest)。
2. 啟動 Windows PowerShell 整合式指令碼環境 (ISE): 在本機電腦，到 toohello**啟動**功能表。 型別**系統管理工具**按一下 toorun 它。 在 hello**系統管理工具**視窗中，以滑鼠右鍵按一下**Windows PowerShell ISE**，按一下 **系統管理員身分執行**。
3. 在**Windows PowerShell ISE**，按一下 **檔案** > **新增**toocreate 新的指令碼檔。
4. 現在，我們會提供簡單的指令碼會顯示基本的 PowerShell 命令 tooaccess Azure 儲存體。 hello 指令碼會先問問您的 Azure 帳戶認證 tooadd Azure 帳戶 toohello 本機 PowerShell 環境。 然後，hello 指令碼會設定 hello 預設 Azure 訂用帳戶，並在 Azure 中建立新的儲存體帳戶。 接下來，hello 指令碼會在這個新的儲存體帳戶中建立新的容器，並上傳現有的映像檔案 (blob) toothat 容器。 Hello 指令碼會列出該容器中的所有 blob 之後，它會在本機電腦中建立新的目的地目錄，並下載 hello 映像檔案。
5. 在下列程式碼區段的 hello，選取 hello hello 註解之間的指令碼**#begin**和**#end**。 按下 CTRL + C toocopy 它 toohello 剪貼簿。

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. 在**Windows PowerShell ISE**，按下 CTRL + V 鍵 toocopy hello 指令碼。 按一下 檔案 > 儲存。 在 hello**存**對話方塊視窗中，輸入 hello 名稱 hello 指令碼檔案，例如"mystoragescript。 」 按一下 [儲存] 。
7. 現在，您必須根據您的組態設定 tooupdate hello 指令碼變數。 您必須更新 hello **$SubscriptionName**變數與您的訂用帳戶。 您可以保留 hello hello 指令碼中所指定的其他變數或在您希望的位置加以更新。
   
   * **$SubscriptionName：** 您必須使用自己的訂用帳戶名稱更新此變數。 請遵循下列三種方式 toolocate hello 您訂用帳戶名稱的 hello 的其中一個：
     
    a. 在**Windows PowerShell ISE**，按一下 **檔案** > **新增**toocreate 新的指令碼檔。 複製 hello 下列指令碼 toohello 新指令碼檔案，然後按一下**偵錯** > **執行**。 hello 下列指令碼會先詢問您的 Azure 帳戶認證 tooadd Azure 帳戶 toohello 本機 PowerShell 環境，然後顯示所有 hello 的訂用帳戶連線的 toohello 本機 PowerShell 工作階段。 記下 hello hello 訂用帳戶名稱的 toouse 本教學課程：
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate 和複製您訂用帳戶名稱在 hello [Azure 入口網站](https://portal.azure.com)，在 hello hello 留在中樞功能表中按一下**訂閱**。 將複製 hello 的 toouse 執行本指南中的 hello 指令碼時的訂用帳戶名稱。
     
     ![Azure 入口網站](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate 和複製您訂用帳戶名稱在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)、 向下捲動並按一下**設定**上 hello hello 入口網站的左側。 按一下**訂閱**toosee 訂用帳戶的清單。 複製 hello 想 toouse 執行本指南中提供的 hello 指令碼時的訂用帳戶的名稱。
     
     ![Azure 傳統入口網站](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:**使用給定名稱 hello 指令碼中的 hello 或輸入您的儲存體帳戶的新名稱。 **重要事項：** hello hello 儲存體帳戶名稱必須是唯一在 Azure 中。 而且必須是小寫字母！
   * **$Location:** hello 指令碼中使用給定 「 美國西部"hello，或選擇其他的 Azure 位置，例如，美國東部、 北歐、 等等。
   * **$ContainerName:**使用給定名稱 hello 指令碼中的 hello 或輸入您的容器的新名稱。
   * **$ImageToUpload:**您本機電腦上，輸入路徑 tooa 圖片，例如:"C:\Images\HelloWorld.png"。
   * **$DestinationFolder:** Enter 路徑 tooa 本機目錄 toostore 下載檔案，從 Azure 儲存體，例如:"C:\DownloadImages"。
8. 在更新之後 hello hello"mystoragescript.ps1"檔案中的指令碼變數，按一下 **檔案** > **儲存**。 然後，按一下 **偵錯** > **執行**或按**F5** toorun hello 指令碼。  

Hello 指令碼執行之後，您應該有包含 hello 下載映像檔的本機目的資料夾。 下列螢幕擷取畫面的 hello 顯示範例輸出：

![下載 Blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> hello"Getting started 與 Azure 儲存體和 PowerShell 在 5 分鐘內"區段快速介紹如何 toouse 與 Azure 儲存體的 Azure PowerShell。 如需詳細的資訊和指示，我們建議您 tooread hello 下列各節。
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>搭配使用 Azure PowerShell 與 Azure 儲存體的先決條件
您需要 Azure 訂用帳戶和帳戶 toorun hello PowerShell cmdlet 提供本指南中，如上面所述。

Azure PowerShell 是提供 cmdlet toomanage 透過 Windows PowerShell 的 Azure 模組。 如需安裝及設定 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 我們建議您下載和安裝或使用本指南之前升級 toohello 最新的 Azure PowerShell 模組。

您可以在 hello 標準 Windows PowerShell 主控台或 hello Windows PowerShell 整合式指令碼環境 (ISE) 中執行 hello cmdlet。 例如，tooopen **Windows PowerShell ISE**toohello [開始] 功能表中，輸入 [系統管理工具]，請按一下 toorun 它。 在 hello 系統管理工具 視窗中，以滑鼠右鍵按一下 Windows PowerShell ISE 中，按一下 以系統管理員身分執行。

## <a name="how-toomanage-storage-accounts-in-azure"></a>Toomanage 儲存體帳戶在 Azure 中的方式

讓我們看看如何使用 PowerShell 在 Azure 中管理儲存體帳戶

### <a name="how-tooset-a-default-azure-subscription"></a>如何 tooset 預設的 Azure 訂用帳戶
toomanage 使用 Azure PowerShell 的 Azure 儲存體，您需要 tooauthenticate 利用 Azure 將用戶端環境透過 Azure Active Directory 驗證或憑證式驗證。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)教學課程。 本指南使用 hello Azure Active Directory 驗證。

1. 在 Windows PowerShell ISE 中，輸入下列命令 tooadd hello Azure 帳戶 toohello 本機 PowerShell 環境：

    ```powershell
    Add-AzureAccount
    ```

2. Hello 「 登入 tooMicrosoft Azure 」 在視窗中，輸入 hello 電子郵件地址與您的帳戶相關聯的密碼。 Azure 驗證並儲存 hello 認證資訊，，然後關閉 [hello] 視窗。

3. 接著，執行下列命令 tooview hello Azure 的 hello 帳戶在本機 PowerShell 環境中，並確認已列出您的帳戶：
   
    ```powershell
    Get-AzureAccount
    ```
4. 然後，執行下列 cmdlet tooview hello 所有 hello 的訂用帳戶連線的 toohello 本機 PowerShell 工作階段，並確認已列出您的訂用帳戶：

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. 執行 hello Select-azuresubscription cmdlet tooset Azure 訂用帳戶中，預設值：

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. 執行 hello Get-azuresubscription cmdlet 以驗證 hello hello 預設訂用帳戶名稱：

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee 所有 hello 可用的 PowerShell cmdlet Azure 儲存體，都執行：
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>如何 toocreate 新的 Azure 儲存體帳戶
toouse Azure 儲存體，您需要儲存體帳戶。 設定您的電腦 tooconnect tooyour 訂用帳戶之後，您可以建立新的 Azure 儲存體帳戶。

1. 執行 hello Get AzureLocation cmdlet toofind hello 的所有可用的資料中心位置：

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. 接下來，執行 hello 新增 AzureStorageAccount cmdlet toocreate 新的儲存體帳戶。 hello 下列範例會建立新的儲存體帳戶在 hello 「 美國西部 」 資料中心內。
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> hello 您的儲存體帳戶名稱必須是唯一在 Azure 中，而且必須是小寫。 如需命名慣例與限制，請參閱[關於 Azure 儲存體帳戶](storage-create-storage-account.md)和[命名和參考容器、Blob 及中繼資料](http://msdn.microsoft.com/library/azure/dd135715.aspx)。
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>如何 tooset 預設 Azure 儲存體帳戶
您可以在訂用帳戶中有多個儲存體帳戶。 您可以選擇其中一個，並將它設定為 hello 預設儲存體帳戶的所有 hello 儲存體中的命令 hello 相同的 PowerShell 工作階段。 這可讓您 toorun hello Azure PowerShell 儲存命令但未明確指定 hello 儲存內容。

1. tooset 訂用帳戶的預設儲存體帳戶，您可以執行 hello 組 AzureSubscription cmdlet。

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. 接下來，執行 hello Get-azuresubscription cmdlet tooverify hello 儲存體帳戶是預設訂用帳戶的帳戶相關聯。 此命令會傳回 hello 訂閱屬性，包括其目前的儲存體帳戶 hello 目前訂用帳戶。

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>如何 toolist 所有 Azure 儲存體帳戶的訂用帳戶中
每個 Azure 訂用帳戶可以有 too100 儲存體帳戶。 Hello 最新限制的資訊，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)。

執行下列 cmdlet toofind 出 hello 名稱和狀態的 hello hello 目前訂用帳戶的儲存體帳戶的 hello:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>如何 toocreate Azure 儲存體內容
Azure 儲存體內容是 PowerShell tooencapsulate hello 儲存體認證中的物件。 執行任何後續的 cmdlet 時使用的儲存體內容可讓您 tooauthenticate 您的要求未明確指定 hello 儲存體帳戶和其存取金鑰。 您可以用很多方式建立儲存體內容，例如使用儲存體帳戶名稱和存取金鑰、共用存取簽章 (SAS) 權杖、連接字串或匿名。 如需詳細資訊，請參閱 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext)。  

使用下列三種方式 toocreate hello 的其中一個儲存體內容：

* 執行 hello [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind 出 hello Azure 儲存體帳戶的主要儲存體存取金鑰。 接下來，呼叫 hello[新增 AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate 儲存體內容：

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* 產生 Azure 儲存體容器的共用的存取簽章 token，並使用它 toocreate 儲存體內容：

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    如需詳細資訊，請參閱 [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) 和[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。

* 在某些情況下，您可能想 toospecify hello 服務端點，當您建立新的存放裝置內容。 當您儲存體帳戶的自訂網域名稱註冊與 hello Blob 服務或您想 toouse 共用的存取簽章存取儲存體資源，這可能是必要。 設定連接字串中的 hello 服務端點並使用新的儲存體內容 toocreate 如下所示：

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

如需有關如何 tooconfigure 儲存體連接字串，請參閱[設定連接字串](storage-configure-connection-string.md)。

現在，您必須設定您的電腦，並學到如何 toomanage 訂閱和儲存體帳戶使用 Azure PowerShell toohello toomanage Azure blob 的方式下一個區段 toolearn 去 blob 快照集。

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>如何 tooretrieve 和重新產生 Azure 儲存體金鑰
Azure 儲存體帳戶會隨附兩個帳戶金鑰。 您可以使用下列 cmdlet tooretrieve hello 您的金鑰。

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

使用下列 cmdlet tooretrieve 特定索引鍵的 hello。 有效值為 Primary 和 Secondary。  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

如果您想要 tooregenerate 您的金鑰使用下列 cmdlet 的 hello。 -KeyType 的有效值為 "Primary" 和 "Secondary"

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Toomanage Azure 的 blob
Azure Blob 儲存體是用於儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。 本節假設您已熟悉 hello Azure Blob 儲存體服務的概念。 如需詳細資訊，請參閱[以 .NET 開始使用 Blob 儲存體](storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](http://msdn.microsoft.com/library/azure/dd179376.aspx)。

### <a name="how-toocreate-a-container"></a>如何 toocreate 容器
Azure 儲存體中的每個 Blob 必須位於一個容器中。 您可以建立私用容器使用 hello New-azurestoragecontainer cmdlet:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> 匿名讀取權限有三個層級：**Off**、**Blob** 和 **Container**。 tooprevent 匿名存取 tooblobs，集 hello 權限的參數太**關閉**。 根據預設，hello 新容器是私人的而且只有 hello 帳戶擁有者可存取。 tooallow 匿名公用讀取存取 tooblob 資源，但不是 toocontainer 中繼資料或 toohello 清單 hello 容器中的 blob、 設定 hello 權限的參數太**Blob**。 tooallow 完整公用讀取存取 tooblob 資源、 容器中繼資料及 hello hello 容器中的 blob 清單中，設定 hello 權限的參數太**容器**。 如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)。
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>如何 tooupload blob 容器
Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。 如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。

tooupload tooa 容器中的 blob，您可以使用 hello [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet。 根據預設，此命令會將 hello 本機檔案 tooa 區塊 blob 上傳。 toospecify hello hello blob 類型，您可以使用 hello-BlobType 參數。

hello 下列範例會執行 hello [Get-childitem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget 所有 hello hello 指定的資料夾中的檔案，然後將它們傳送 toohello 下一個指令程式使用 hello 管線運算子。 hello [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet 上傳 hello 本機檔案 tooyour 容器：

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Toodownload 從容器的 blob
下列範例中的 hello 示範 toodownload 從容器的 blob。 hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包含 hello 儲存體帳戶名稱以及其主要存取金鑰。 然後，hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet。 接下來，hello 範例會使用 hello [Get AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blob hello 本機目的資料夾。

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Toocopy 從一個儲存體容器 tooanother 的 blob
您可以跨儲存體帳戶和區域以非同步方式複製 Blob。 hello 下列範例示範 toocopy 從一個儲存體容器 tooanother 兩個不同的儲存體帳戶中的 blob。 hello 範例先設定來源和目的地儲存體帳戶的變數，並接著會建立每個帳戶的儲存體內容。 接下來，hello 範例會將 blob 複製從 hello 來源容器 toohello 目的地容器使用 hello[開始 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet。 hello 範例假設 hello 來源和目的地儲存體帳戶和容器已經存在。

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

請注意，此範例會執行非同步複製。 您可以監視的每個複本的 hello 狀態執行 hello [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet。

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Toocopy 從次要位置的 blob
您可以從 hello 次要位置的 RA GRS 啟用帳戶複製 blob。

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>如何 toodelete blob
toodelete blob，先取得 blob 的參考，然後在其上呼叫 hello 移除 AzureStorageBlob cmdlet。 hello 下列範例會刪除指定的容器中的所有 hello blob。 hello 範例第一次設定儲存體帳戶的變數，並接著會建立儲存體內容。 接下來，hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet，並執行 hello[移除 AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet 從 Azure 儲存體中容器的 tooremove blob。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>如何 toomanage Azure blob 快照集
Azure 可讓您建立 Blob 的快照集。 快照集是在某個點時間取得的唯讀 Blob 版本。 一旦建立快照集後，即可加以讀取、複製或刪除，但不能修改。 快照集提供 blob 向上方式 tooback 出現在時間點。 如需詳細資訊，請參閱 [建立 Blob 的快照集](http://msdn.microsoft.com/library/azure/hh488361.aspx)。

### <a name="how-toocreate-a-blob-snapshot"></a>如何 toocreate blob 快照集
blob 的 snaphot toocreate 先取得 blob 的參考，然後再呼叫 hello`ICloudBlob.CreateSnapshot`方法。 hello 下列範例先設定儲存體帳戶的變數，然後建立儲存體內容。 接下來，hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet，並執行 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx)方法 toocreate 快照集。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>如何 toolist blob 的快照集
您可以對 Blob 建立您所需數量的快照集。 您可以列出 blob tootrack 與相關聯的 hello 快照目前的快照集。 hello 下列範例會使用預先定義的 blob 和呼叫 hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob)該 blob 的 cmdlet toolist hello 快照集。  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>如何 toocopy blob 的快照集
您可以複製 blob toorestore hello 快照集的快照集。 如需詳細的資訊及限制，請參閱 [建立 Blob 的快照集](http://msdn.microsoft.com/library/azure/hh488361.aspx)。 hello 下列範例先設定儲存體帳戶的變數，然後建立儲存體內容。 接下來，hello 範例會定義 hello 容器和 blob 名稱的變數。 hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet，並執行 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx)方法 toocreate 快照集。 然後，hello 範例會執行 hello[開始 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello blob 快照集使用 hello ICloudBlob 物件 hello 來源 blob。 確定 tooupdate hello 變數根據您之前執行 hello 範例的組態。 請注意下列範例的 hello 假設 hello 來源和目的地容器和 hello 來源 blob 已經存在。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

既然您已經學會如何 toomanage Azure blob，blob 快照集，使用 Azure PowerShell，請移 toohello 下一個區段 toolearn toomanage 資料表、 佇列與檔案的方式。

## <a name="how-toomanage-azure-tables-and-table-entities"></a>如何 toomanage Azure 資料表和資料表實體
Azure 資料表儲存體服務是 NoSQL 資料存放區，您可以使用 toostore 及查詢大型資料集的結構化、 非關聯式。 hello 的 hello 服務的主要元件是資料表、 實體和屬性。 資料表是一組實體。 實體是一組屬性。 每個實體可以有 too252 屬性，也就是所有的名稱 / 值組。 本節假設您已熟悉 hello Azure 資料表儲存體服務的概念。 如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)和[開始使用適用於.NET 的 Azure 資料表儲存體使用](storage-dotnet-how-to-use-tables.md)。

在下列各小節 hello，您將學習如何 toomanage Azure 資料表儲存體服務使用 Azure PowerShell。 hello 涵蓋案例包括**建立**，**刪除**，和**擷取****資料表**，以及**加入**，**查詢**，和**刪除資料表實體**。

### <a name="how-toocreate-a-table"></a>如何 toocreate 資料表
每個資料表必須位於 Azure 儲存體帳戶中。 hello 下列範例會示範如何 toocreate Azure 儲存體中的資料表。 hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。 接下來，它會使用 hello[新增 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate Azure 儲存體中的資料表。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>如何 tooretrieve 資料表
您可以查詢和擷取儲存體帳戶中的一個或所有資料表。 hello 下列範例會示範如何指定的資料表使用 tooretrieve hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

如果您呼叫 hello Get AzureStorageTable cmdlet 不含任何參數，它會取得所有儲存體資料表儲存體帳戶。

### <a name="how-toodelete-a-table"></a>如何 toodelete 資料表
您可以從儲存體帳戶刪除資料表，使用 hello[移除 AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet。  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>如何 toomanage 資料表實體
目前，Azure PowerShell 不會直接提供 cmdlet toomanage 資料表實體。 tooperform 作業在資料表實體上的，您可以使用在 hello hello 類別[適用於.NET 的 Azure 儲存體用戶端程式庫](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)。

#### <a name="how-tooadd-table-entities"></a>如何 tooadd 資料表實體
tooadd 實體 tooa 資料表，第一次建立物件，定義實體屬性。 實體可以有 too255 屬性，包括 3 個系統屬性： **PartitionKey**， **RowKey**，和**時間戳記**。 您必須負責插入及更新的 hello 值**PartitionKey**和**RowKey**。 hello 伺服器負責管理 hello 值**時間戳記**，無法修改。 一起 hello **PartitionKey**和**RowKey**唯一識別資料表中的每個實體。

* **PartitionKey**： 決定 hello 實體儲存在中的 hello 磁碟分割。
* **RowKey**： 唯一識別 hello hello 磁碟分割內的實體。

您可以定義 too252 實體的自訂屬性。 如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。

hello 下列範例會示範如何 tooadd 實體 tooa 資料表。 hello 範例示範如何 tooretrieve hello 員工資料表，以及加入數個項目。 首先，它會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。 接下來，它會擷取給定資料表中使用 hello hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。 如果 hello 資料表不存在，hello[新增 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable)指令程式是使用的 toocreate Azure 儲存體中的資料表。 接下來，hello 範例會定義自訂函式加入實體 tooadd 實體 toohello 資料表，藉由指定每個實體磁碟分割和資料列索引鍵。 加入實體 hello 函式呼叫 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx)類別 toocreate 實體物件。 稍後，hello 範例會呼叫 hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx)方法在此實體物件 tooadd 它 tooa 資料表。

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>如何 tooquery 資料表實體
tooquery 資料表時，使用 hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx)類別。 hello 下列範例假設您已已經執行 hello 指令碼中 hello 如何提供本指南的 tooadd [實體] 區段。 hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存內容，包括 hello 儲存體帳戶名稱和其存取金鑰。 接下來，它會嘗試使用 hello tooretrieve hello 先前建立 「 員工 」 資料表[Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。 呼叫 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) hello Microsoft.WindowsAzure.Storage.Table.TableQuery 類別上的指令程式會建立新的查詢物件。 hello 範例會尋找具有 'ID' 資料行，其值為 1 所指定字串篩選條件中的 hello 實體。 如需詳細資訊，請參閱 [查詢資料表和實體](http://msdn.microsoft.com/library/azure/dd894031.aspx)。 當您執行此查詢時，它會傳回符合 hello 篩選準則的所有實體。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>如何 toodelete 資料表實體
您可以使用實體的資料分割和資料列索引鍵來刪除實體。 hello 下列範例假設您已已經執行 hello 指令碼中 hello 如何提供本指南的 tooadd [實體] 區段。 hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存內容，包括 hello 儲存體帳戶名稱和其存取金鑰。 接下來，它會嘗試使用 hello tooretrieve hello 先前建立 「 員工 」 資料表[Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。 如果 hello 資料表存在，hello 範例會呼叫 hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx)方法 tooretrieve 實體會根據其資料分割和資料列的索引鍵值。 然後，傳遞 hello 實體 toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx)方法 toodelete。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Toomanage Azure 佇列的方式，以及佇列訊息
Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。 本節假設您已熟悉 hello Azure 佇列儲存體服務的概念。 如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](storage-dotnet-how-to-use-queues.md)。

本章節將說明如何 toomanage Azure 佇列儲存體服務使用 Azure PowerShell。 hello 涵蓋案例包括**插入**和**刪除**佇列訊息，以及**建立**，**刪除**，和**擷取佇列**。

### <a name="how-toocreate-a-queue"></a>如何 toocreate 佇列
hello 下列範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。 接下來，它會呼叫[新增 AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate 名為 'queuename' 的佇列。

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

如需 Azure 佇列服務命名慣例的資訊，請參閱 [為佇列和中繼資料命名](http://msdn.microsoft.com/library/azure/dd179349.aspx)。

### <a name="how-tooretrieve-a-queue"></a>如何 tooretrieve 佇列
您可以查詢及擷取特定的佇列或所有儲存體帳戶中的 hello 佇列的清單。 hello 下列範例會示範如何指定的佇列，使用 tooretrieve hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet。

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

如果您呼叫 hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue)沒有任何參數的 cmdlet，它會取得所有 hello 佇列的清單。

### <a name="how-toodelete-a-queue"></a>如何 toodelete 佇列
toodelete 佇列和所有 hello 訊息包含在它呼叫 hello 移除 AzureStorageQueue cmdlet。 hello 下列範例顯示如何指定的佇列，使用 toodelete hello 移除 AzureStorageQueue cmdlet。

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>如何將訊息插入佇列 tooinsert
tooinsert 將訊息插入現有佇列，先建立的新執行個體的 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx)類別。 接下來，呼叫 hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx)方法。 您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 CloudQueueMessage。

hello 下列範例會示範如何 tooadd 訊息 tooa 佇列。 hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。 接下來，它會擷取使用 hello hello 指定的佇列[Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet。 如果 hello 佇列存在，hello [New-object](http://technet.microsoft.com/library/hh849885.aspx)指令程式是使用的 toocreate hello 的執行個體[Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx)類別。 稍後，hello 範例會呼叫 hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx)方法在此訊息物件 tooadd 它 tooa 佇列。 以下是程式碼以擷取佇列，並插入 hello 訊息 'MessageInfo':

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>在 hello toode 佇列下一個訊息
您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。 當您呼叫 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx)方法，您會收到 hello 下一個訊息佇列中。 傳回訊息**GetMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 toofinish 移除 hello 訊息從 hello 佇列，您必須呼叫 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx)方法。 這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。 您的程式碼呼叫**DeleteMessage**處理 hello 訊息之後，以滑鼠右鍵。

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>如何 toomanage Azure 檔案共用及檔案
Azure 檔案儲存體提供共用存放裝置使用 hello 標準 SMB 通訊協定的應用程式。 Microsoft Azure 虛擬機器和雲端服務可以透過掛接共用，應用程式元件之間共用檔案資料，並在內部部署應用程式可以存取檔案共用，以透過 hello 檔案儲存體 API 或 Azure PowerShell 中的資料。

如需 Azure 檔案儲存體的詳細資訊，請參閱[在 Windows 上開始使用 Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)和[檔案服務 REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx)。

## <a name="how-tooset-and-query-storage-analytics"></a>如何 tooset 並查詢儲存體分析
您可以使用[Azure 儲存體分析](storage-analytics.md)toocollect 度量資訊。 您的 Azure 儲存體帳戶和記錄資料要求的相關傳送 tooyour 儲存體帳戶。 您可以使用儲存體度量 toomonitor hello 健全狀況的儲存體帳戶和儲存體記錄 toodiagnose 和疑難排解您的儲存體帳戶中的問題。 您可以使用設定監視 hello Azure 入口網站或 Windows PowerShell 或以程式設計方式使用 hello 儲存體用戶端程式庫。 儲存體記錄發生於用戶端，並讓您的儲存體帳戶中的成功和失敗要求的 toorecord 詳細資料。 這些記錄檔可讓您讀取、 寫入和刪除作業，針對您資料表、 佇列和 blob 以及 hello 失敗要求的理由 toosee 詳細資料。

如何使用 PowerShell、 tooenable 和檢視儲存體度量資料，請參閱的 toolearn[如何 tooenable 儲存體度量使用 PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell)。

如何 tooenable 並擷取儲存體記錄資料使用 PowerShell，請參閱 < 的 toolearn[如何 tooenable 儲存體記錄使用 PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell)和[尋找儲存體記錄 」 記錄檔資料](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata)。
如需使用儲存體度量 」 和 「 儲存體記錄 tootroubleshoot 儲存體問題的詳細資訊，請參閱[監控、 診斷及排解 Microsoft Azure 儲存體](storage-monitoring-diagnosing-troubleshooting.md)。

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>如何 toomanage 共用存取簽章 (SAS) 和預存存取原則
共用的存取簽章是使用 Azure 儲存體的任何應用程式的 hello 安全性模型的重要一環。 它們可用於提供有限的權限 tooyour 儲存體帳戶 tooclients 不應有任何 hello 帳戶金鑰。 根據預設，只有 hello 儲存體帳戶的 hello 擁有者可以存取 blob、 資料表，以及該帳戶內的佇列。 如果您的服務或應用程式需要 toomake 這些資源可用 tooother 用戶端而不需要共用您的存取金鑰，您會有三個選項：

* 設定容器的權限 toopermit 匿名讀取權限 toohello 容器和其 blob。 這不適用於資料表或佇列。
* 使用共用的存取簽章，授與特定時間間隔的有限的存取權限 toocontainers、 blob、 佇列和資料表。
* 容器或其 blob、 佇列或資料表，請使用預存的存取原則 tooobtain 一層額外的控制共用的存取簽章。 hello 預存的存取原則可讓您 toochange hello 開始時間、 到期時間或權限的簽章，或 toorevoke 它之後發出。

共用存取簽章可以是下列其中一種格式：

* **臨機操作 SAS**： 當您建立臨機操作 SAS、 hello 開始時間、 到期時間，並 hello SAS 的權限會指定在 hello SAS URI。 您可以在容器、Blob、資料表或佇列上建立此類型的 SAS，而且無法撤銷它。
* **與預存的存取原則 SAS**： 資源容器的 blob 容器、 資料表或佇列-佇列上定義的預存的存取原則，您可以使用它 toomanage 條件約束的一個或多個共用的存取簽章。 當您建立 SAS 關聯與預存的存取原則時，hello SAS 繼承 hello 的條件約束-hello 開始時間、 到期時間和權限-hello 預存存取原則的定義。 這種類型的 SAS 是可撤銷的。

如需詳細資訊，請參閱[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)和[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)。

在 hello 下一步 區段中，您將學習如何 toocreate Azure 資料表的共用的存取簽章語彙基元和預存存取原則。 Azure PowerShell 也會為容器、Blob 和佇列提供類似的 Cmdlet。 在本節中的 toorun hello 指令碼下載中心 hello [Azure PowerShell 版本 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409)或更新版本。

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>如何以原則為基礎的 toocreate 共用存取簽章語彙基元
使用 hello 新增 AzureStorageTableStoredAccessPolicy cmdlet toocreate 新的預存的存取原則。 然後，呼叫 hello[新增 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate Azure 儲存體資料表的新原則為基礎的共用的存取簽章 token。

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>如何 toocreate 臨機操作 （非廢止） 的共用存取簽章語彙基元
使用 hello[新增 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate 新臨機操作 （非廢止） 共用存取簽章的權杖的 Azure 儲存體資料表：

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>如何 toocreate 預存的存取原則
使用 Azure 儲存體資料表 hello 新增 AzureStorageTableStoredAccessPolicy cmdlet toocreate 新的預存的存取原則：

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>如何 tooupdate 預存的存取原則
使用 Azure 儲存體資料表 hello 組 AzureStorageTableStoredAccessPolicy cmdlet tooupdate 現有的預存的存取原則：

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>如何 toodelete 預存的存取原則
Azure 儲存體資料表上使用 hello 移除 AzureStorageTableStoredAccessPolicy cmdlet toodelete 預存的存取原則：

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>如何為美國政府和 Azure China toouse Azure 儲存體
Azure 環境是 Microsoft Azure 的獨立部署，例如[適用於美國政府的 Azure Government](https://azure.microsoft.com/features/gov/)、[適用於全球 Azure 的 AzureCloud](https://portal.azure.com) 和[由中國世紀互聯運作的 AzureChinaCloud for Azure](http://www.windowsazure.cn/)。 您可以針對美國政府與 Azure 中國部署新的 Azure 環境。

toouse AzureChinaCloud 與 Azure 儲存體，您需要 toocreate AzureChinaCloud 相關聯的儲存體內容。 請遵循這些步驟 tooget，您已啟動：

1. 執行 hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 可用的 Azure 環境：
   
    ```powershell
    Get-AzureEnvironment
    ```

2. 新增 Azure China 帳戶 tooWindows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. 建立 AzureChinaCloud 帳戶的儲存體內容：
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse Azure 儲存體與[美國Azure Government ](https://azure.microsoft.com/features/gov/) 搭配使用，請定義一個新環境，然後在此環境中建立新的儲存體內容：

1. 執行 hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 可用的 Azure 環境：

    ```powershell
    Get-AzureEnvironment
    ```

2. 新增 Azure 美國政府帳戶 tooWindows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. 建立 AzureUSGovernment 帳戶的儲存體內容：
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
如需詳細資訊，請參閱：

* [Microsoft Azure Government 開發人員指南](../azure-government-developer-guide.md)。
* [在 China 服務上建立應用程式時差異的概觀](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>後續步驟
本指南中，您學到如何 toomanage 使用 Azure PowerShell 的 Azure 儲存體。 以下是有助於您深入了解的一些相關文章和資源。

* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)
* [Azure 儲存體 PowerShell Cmdlet](/powershell/module/azurerm.storage/#storage)
* [Windows PowerShell 參考](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
