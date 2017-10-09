---
title: "端對端金鑰輪替和稽核與 Azure 金鑰保存庫註冊 aaaSet |Microsoft 文件"
description: "使用此方式 tootoohelp 利用金鑰輪替與監視的金鑰保存庫記錄檔取得設定。"
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>使用端對端金鑰輪替和稽核設定 Azure 金鑰保存庫
## <a name="introduction"></a>簡介
建立金鑰保存庫之後, 您就會使用該保存庫 toostore，您的金鑰和秘密可以 toostart。 您的應用程式不需要再 toopersist 您的金鑰或密碼，但而是會視需要要求它們 hello 金鑰保存庫中。 這可讓您 tooupdate 金鑰和密碼而不會影響 hello 應用程式的行為，開啟您的金鑰和秘密管理周圍的可能值範圍。

本文逐步解說示範如何使用 Azure 金鑰保存庫 toostore 密碼，在此情況下存取應用程式的 Azure 儲存體帳戶金鑰。 文中也會示範如何實作該儲存體帳戶金鑰的排程輪替。 最後，它逐步解說示範如何 toomonitor hello 金鑰保存庫稽核記錄檔，以及進行非預期的要求時發出警示。

> [!NOTE]
> 本教學課程不預期的 tooexplain 詳細 hello 初始設定金鑰保存庫中。 如需這方面的資訊，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。 如需跨平台命令列介面的指示，請參閱[使用 CLI 管理金鑰保存庫](key-vault-manage-with-cli2.md)。
>
>

## <a name="set-up-key-vault"></a>設定金鑰保存庫
tooenable 應用程式 tooretrieve 密碼從金鑰保存庫，您必須先建立 hello 密碼並將它上傳 tooyour 保存庫。 這可藉由啟動 Azure PowerShell 工作階段然後登入 tooyour Azure 帳戶以 hello 下列命令：

```powershell
Login-AzureRmAccount
```

在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。 PowerShell 會取得與此帳戶相關聯的所有 hello 訂閱。 PowerShell 會使用 hello 預設第一個。

如果您有多個訂閱，您可能必須 toospecify hello 分別為使用的 toocreate 金鑰保存庫。 輸入下列帳戶 toosee hello 訂閱 hello:

```powershell
Get-AzureRmSubscription
```

輸入 toospecify hello 訂用帳戶與 hello 金鑰保存庫，您將記錄、 相關聯：

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

因為本文會示範如何將儲存體帳戶金鑰儲存為密碼，所以您必須取得該儲存體帳戶金鑰。

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

擷取後您的密碼 （在此情況下，儲存體帳戶金鑰），您必須轉換該 tooa 安全字串，然後建立該密碼金鑰保存庫中。

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
接下來，您所建立的 hello 密碼取得 hello URI。 這用在稍後步驟中，當您呼叫 hello 金鑰保存庫 tooretrieve 您的密碼。 執行下列 PowerShell 命令的 hello，並記下 hello ID 值為 hello 密碼 URI:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>設定 hello 應用程式
既然您已儲存的密碼，您可以使用程式碼 tooretrieve，並使用它。 有幾個步驟需要的 tooachieve 這。 hello 第一個且最重要步驟是向 Azure Active Directory 中註冊您的應用程式，然後告訴金鑰保存庫的應用程式資訊，使它可以讓您的應用程式的要求。

> [!NOTE]
> 您的應用程式必須在建立 hello 相同金鑰保存庫以 Azure Active Directory 租用戶。
>
>

開啟 Azure Active Directory hello 應用程式 索引標籤。

![在 Azure Active Directory 中開啟應用程式](./media/keyvault-keyrotation/AzureAD_Header.png)

選擇**新增**tooadd 應用程式 tooyour Azure Active Directory。

![選擇 [新增]](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

保留 hello 應用程式類型為**WEB 應用程式和/或 WEB API**並提供您的應用程式名稱。

![名稱 hello 應用程式](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

為應用程式提供 [登入 URL] 和 [應用程式識別碼 URI]。 這些可以是任何想用於此示範的值，並可在稍後視需要加以變更。

![提供必要的 URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Hello 應用程式會加入 tooAzure Active Directory 之後，您將帶入 hello 應用程式頁面。 按一下 hello**設定**索引標籤，然後尋找並複製 hello**用戶端識別碼**值。 記下稍後步驟中的 hello 用戶端識別碼。

接下來，產生金鑰，以便應用程式與 Azure Active Directory 互動。 您可以在 hello 下建立這個**金鑰**> 一節中 hello**組態** 索引標籤。記下稍後步驟中使用的新產生的 hello 金鑰從 Azure Active Directory 應用程式。

![Azure Active Directory 應用程式金鑰](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

建立應用程式分成 hello 金鑰保存庫中的任何呼叫之前, 您必須告訴 hello 金鑰保存庫有關您的應用程式和其權限。 hello 下列命令會使用 hello 保存庫名稱和 hello 用戶端識別碼，從您的 Azure Active Directory 應用程式和授與**取得**hello 應用程式的存取 tooyour 金鑰保存庫。

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

此時，您就準備好 toostart 建置您的應用程式呼叫。 在您的應用程式中，您必須安裝 hello NuGet 套件需要的 toointeract 使用 Azure 金鑰保存庫與 Azure Active Directory。 Hello Visual Studio 封裝管理員主控台中，輸入下列命令的 hello。 Hello 撰寫這篇文章，hello 目前 hello Azure Active Directory 封裝會版 3.10.305231913，因此您可能會想 tooconfirm hello 最新版本，並據此更新。

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

在您的應用程式程式碼建立類別 toohold hello 方法的 Azure Active Directory 驗證。 在此範例中，該類別稱為 **Utils**。 新增 hello 下列 using 陳述式：

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

接下來，新增 Azure Active Directory 中的下列方法 tooretrieve hello JWT 權杖中的 hello。 為方便維護，您可能想 toomove hello 硬式編碼的字串值至 web 或應用程式組態中。

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

新增 hello 必要的程式碼 toocall 金鑰保存庫，和擷取您的密碼值。 您必須在第一次加入 hello 下列 using 陳述式：

```csharp
using Microsoft.Azure.KeyVault;
```

新增 hello 方法呼叫 tooinvoke 金鑰保存庫，和擷取您的密碼。 在此方法中，您可以提供 hello 機密您在上一個步驟中儲存的 URI。 請記下的 hello hello 使用**GetToken**方法從 hello **Utils**先前建立的類別。

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

當您執行您的應用程式時，您應該立即驗證 tooAzure Active Directory，然後從 Azure 金鑰保存庫擷取您的密碼值。

## <a name="key-rotation-using-azure-automation"></a>使用 Azure 自動化的金鑰輪替
針對儲存為 Azure 金鑰保存庫密碼的值，有各種選項可用來實作其輪替策略。 密碼可以在進行手動程序時輪替、使用 API 呼叫以程式設計的方式輪替，或是透過自動化指令碼來輪替。 基於 hello 這篇文章，您將無法使用 Azure PowerShell 結合 Azure 自動化 toochange 的 Azure 儲存體帳戶存取金鑰。 然後您將使用這個新金鑰來更新金鑰保存庫密碼。

tooallow Azure 自動化 tooset 祕密值在金鑰保存庫中的，您必須取得名為 AzureRunAsConnection，建立您的 Azure 自動化執行個體時所建立的 hello 連接 hello 用戶端識別碼。 從 Azure 自動化執行個體選擇 [資產]，即可尋找這個識別碼。 在您選擇從該處，**連線**]，然後選取 [hello **AzureRunAsConnection**服務主體。 記下 hello**應用程式識別碼**。

![Azure 自動化用戶端識別碼](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

在 [資產] 中，選擇 [模組]。 從**模組**，選取**圖庫**，然後搜尋和**匯入**更新版本的每個 hello 下列模組：

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> Hello 撰寫這篇文章時，只有 hello 前面所述的模組所需 toobe 更新 hello 下列指令碼。 如果您發現自動化作業失敗，請確認您已匯入所有必要的模組及其相依項目。
>
>

Hello 應用程式識別碼擷取您的 Azure 自動化連線之後，您必須告訴您金鑰保存庫這個應用程式已存取 tooupdate 機密資料，您的保存庫中。 可以使用下列 PowerShell 命令的 hello 完成這個動作：

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

接下來，選取 Azure 自動化執行個體底下的 [Runbook] 資源，然後選取 [新增 Runbook]。 選取 [快速建立] 。 命名您的 runbook，並選取**PowerShell** hello runbook 類型。 您有 hello 選項 tooadd 描述。 最後，按一下 [建立]。

![建立 Runbook](./media/keyvault-keyrotation/Create_Runbook.png)

貼上下列 PowerShell 指令碼，在新的 runbook 的 hello 編輯器窗格中的 hello:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

從 hello 編輯器窗格中，選擇 **測試窗格**tootest 指令碼。 一旦 hello 指令碼執行時並沒有錯誤，您可以選取**發行**，然後您可以套用回在 hello runbook 設定 窗格中的 hello runbook 的排程。

## <a name="key-vault-auditing-pipeline"></a>金鑰保存庫稽核管線
當您設定金鑰保存庫時，您可以開啟稽核功能 toocollect 提出 toohello 金鑰保存庫的存取要求的記錄檔。 這些記錄檔會儲存在指定的 Azure 儲存體帳戶中，以供提取、監視和分析。 hello 下列案例使用 Azure 函式、 Azure 邏輯應用程式和金鑰保存庫的稽核記錄檔 toocreate 管線 toosend 電子郵件時的應用程式，並符合 hello hello web 應用程式的應用程式識別碼 hello 保存庫中擷取機密資料。

首先，您必須在金鑰保存庫上啟用記錄功能。 這可透過下列 PowerShell 命令的 hello (完整詳細資料，可以看到在[金鑰保存庫記錄](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

啟用此選項之後，稽核記錄，到指定的儲存體帳戶的 hello 收集的開始。 這些記錄檔包含有關金鑰保存庫存取方式、時間和存取者的事件。

> [!NOTE]
> 您可以存取您的記錄資訊 hello 金鑰保存庫作業後 10 分鐘。 但通常不用這麼久。
>
>

hello 下一個步驟太[建立 Azure 服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。 這是金鑰保存庫稽核記錄檔的推送位置。 Hello 佇列中 hello 稽核記錄檔訊息時，hello 邏輯應用程式會拾取它們，並充當他們。 建立服務匯流排與 hello 下列步驟：

1. 建立服務匯流排命名空間 (如果您已有您想要這麼做，toouse 略過 tooStep 2)。
2. 瀏覽 toohello hello Azure 入口網站和選取 hello 命名空間中要 toocreate hello 佇列中的服務匯流排。
3. 選取**新增**選擇**Service Bus > 佇列**並輸入所需的 hello 詳細資料。
4. 選擇 hello 命名空間，並按一下選取 hello 服務匯流排連接資訊**連接資訊**。 您將需要這項資訊 hello 下一節。

下一步[建立 Azure 的函式](../azure-functions/functions-create-first-azure-function.md)toopoll 金鑰保存庫的記錄檔內 hello 儲存體帳戶，並挑選新的事件。 這是會依排程觸發的函式。

toocreate Azure 的函式，選擇**新增 > 函式應用程式**hello Azure 入口網站中。 在建立期間，您可以使用現有的主控方案，或建立新的方案。 您也可以選擇動態主控。 需函式裝載選項的詳細資訊，請參閱[如何 tooscale Azure 函式](../azure-functions/functions-scale.md)。

建立 hello Azure 函式時，瀏覽 tooit，並選擇計時器，函式和 C\#。 然後按一下 [建立此函式]。

![Azure Functions 啟動刀鋒視窗](./media/keyvault-keyrotation/Azure_Functions_Start.png)

在 hello**開發**索引標籤上，hello run.csx 程式碼取代 hello 下列：

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> 請確定 tooreplace hello 變數在上述程式碼 toopoint tooyour 儲存體帳戶寫入記錄檔-金鑰保存庫 hello hello hello 您稍早建立的服務匯流排和 hello 特定路徑 toohello 金鑰保存庫儲存體記錄。
>
>

hello 函式挑選 hello 最新記錄檔從 hello 儲存體帳戶 hello 金鑰保存庫的記錄檔可寫入，該檔案中，從 grabs hello 最新事件，並將它們推送 tooa 服務匯流排佇列。 由於單一檔案可以擁有多個事件，您應該建立 hello 函式也會查看已收取 hello 最後一個事件 toodetermine hello 時間戳記 sync.txt 檔案。 這可確保您不推送 hello 多次相同的事件。 這個 sync.txt 檔案包含 hello 最後發生之事件的時間戳記。 hello 記錄檔，載入時，已排序的 toobe 根據 hello 時間戳記 tooensure 正確排序。

這個函式中，我們會參考數個立即可用 hello Azure 函式中所沒有的額外程式庫。 tooinclude，我們需要 Azure 函式 toopull 它們使用 NuGet。 選擇 hello**檢視檔案**選項。

![檢視檔案選項](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

然後使用下列內容新增名為 project.json 的檔案︰

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
根據**儲存**，Azure 函式會下載所需的 hello 二進位檔。

切換 toohello**整合**索引標籤，然後在 hello 函式有意義的名稱 toouse 命名 hello 計時器的參數。 在上述程式碼的 hello，它會預期呼叫 hello 計時器 toobe *myTimer*。 指定[CRON 運算式](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON)，如下所示： 0 \* \* \* \* \*的 hello 計時器會導致 hello 函式 toorun 一分鐘一次。

在 hello 相同**整合**索引標籤上，新增 hello 類型的輸入**Azure Blob 儲存體**。 這將會為 toohello sync.txt 檔案，其中包含 hello hello 看 hello 函式的最後一個事件時間戳記。 這將可依 hello 參數名稱的 hello 函式內。 在上述程式碼的 hello，hello Azure Blob 儲存體輸入預期 hello 參數名稱 toobe *inputBlob*。 選擇 hello hello sync.txt 檔案所在的儲存體帳戶 （它可能是 hello 相同或不同的儲存體帳戶）。 在 [hello 路徑] 欄位中提供 hello 路徑 hello 檔案所在 hello 格式 {container-name}/path/to/sync.txt。

將輸出 hello 型別的*Azure Blob 儲存體*輸出。 這將會為您所定義 hello 輸入 toohello sync.txt 檔案。 這會使用 hello 函式 toowrite hello 的時間戳記 hello 探討的最後一個事件。 hello 上述程式碼需要呼叫此參數 toobe *outputBlob*。

此時，hello 函式已準備。 請確定 tooswitch 後 toohello**開發**索引標籤，然後儲存 hello 程式碼。 請檢查有任何編譯錯誤 hello 輸出 視窗，並據此進行更正。 如果 hello 程式碼會編譯，hello 程式碼應該現在會檢查 hello 金鑰保存庫記錄每隔一分鐘，然後推送到 hello 的任何新事件定義服務匯流排佇列。 您應該會看到每次觸發 hello 函式會寫出 toohello 記錄視窗的記錄資訊。

### <a name="azure-logic-app"></a>Azure 邏輯應用程式
接下來，您必須建立 Azure 邏輯應用程式收取 hello 事件 hello 函式在推入 toohello Service Bus 佇列、 剖析 hello 內容，並傳送電子郵件根據條件的比對。

[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)太移**新增 > 邏輯應用程式**。

Hello 邏輯應用程式建立之後，瀏覽 tooit 並選擇**編輯**。 在 [hello 邏輯應用程式編輯器] 中，選擇**服務匯流排佇列**並輸入您的服務匯流排認證 tooconnect 它 toohello 佇列。

![Azure 邏輯應用程式服務匯流排](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

接下來選擇 [新增條件]。 在 hello 條件切換 toohello 進階編輯器，並輸入下列程式碼，取代 hello APP_ID hello 實際 APP_ID web 應用程式：

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

這個運算式基本上會傳回**false**如果 hello *appid* hello 從內送事件 （這是 hello hello Service Bus 訊息本文） 不是 hello *appid*的 hello應用程式。

現在，在 [若為否，則不執行任何動作]  選項底下建立動作。

![Azure 邏輯應用程式選擇動作](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Hello 動作選擇**Office 365-傳送電子郵件**。 填寫 hello 欄位 toocreate 電子郵件 toosend hello 定義條件傳回**false**。 如果您沒有 Office 365，您無法查看替代項目 tooachieve hello 相同的結果。

此時，您必須尋找一分鐘一次新的金鑰保存庫稽核記錄檔結束 tooend 管線。 推入新的記錄檔找到 tooa 服務匯流排佇列。 新訊息放置於 hello 佇列時，會觸發 hello 邏輯應用程式。 如果 hello *appid*內 hello 事件不符合 hello 應用程式識別碼 hello 呼叫應用程式時，會傳送一封電子郵件。
