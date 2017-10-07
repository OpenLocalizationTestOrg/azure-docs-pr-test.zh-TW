---
title: "aaaUse 封包擷取 toodo 主動式網路監視的警示和 Azure 函式 |Microsoft 文件"
description: "本文說明如何 toocreate 警示觸發與 Azure 網路監看員的封包擷取"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>使用封包擷取搭配警示和 Azure Functions 進行主動式網路監視

網路監看員封包擷取會擷取工作階段建立 tootrack 流量進出虛擬機器。 hello 擷取檔案可以有篩選定義 tootrack 只 hello 想 toomonitor 的流量。 此資料會儲存在儲存體 blob，或在本機 hello 客體機器上。

這項功能可以從其他的自動化案例遠端啟動，例如 Azure Functions。 Hello 功能 toorun 主動式擷取根據封包擷取提供定義網路異常狀況。 其他用途包括收集網路統計資料、取得有關網路入侵的資訊，以及偵錯用戶端與伺服器間的通訊等等。

在 Azure 中部署的資源會全年無休地執行。 您和您的員工無法主動監視所有資源 24/7 hello 的狀態。 例如，如果凌晨 2 點發生問題，會發生什麼事？

使用網路監看員，警示，以及從 hello Azure 生態系統內的函式，您可以主動回應 hello 資料與工具 toosolve 問題與您網路中。

![案例][scenario]

## <a name="prerequisites"></a>必要條件

* hello 最新版本的[Azure PowerShell](/powershell/azure/install-azurerm-ps)。
* 網路監看員的現有執行個體。 如果您還沒有，請[建立網路監看員執行個體](network-watcher-create.md)。
* 在 [hello 中現有的虛擬機器網路監看員與相同的區域以 hello [Windows 擴充功能](../virtual-machines/windows/extensions-nwa.md)或[Linux 虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。

## <a name="scenario"></a>案例

在此範例中，您的 VM 正在傳送多個 TCP 區段比平常更久，而且您想 toobe 收到警示。 此處使用 TCP 區段做為範例，但您可以使用任何警示條件。

當您收到警示時，您想 tooreceive 封包層級資料 toounderstand 為什麼增加通訊。 然後您可以採取步驟 tooreturn hello 虛擬機器的 tooregular 通訊。

此案例假設您有現有的網路監看員執行個體，以及具有有效虛擬機器的資源群組。

下列清單中的 hello 是發生 hello 工作流程的概觀：

1. 會在您的 VM 上觸發警示。
1. hello 警示呼叫 webhook 透過您 Azure 函式。
1. 您的 Azure 函式會處理 hello 警示，並啟動網路監看員封包擷取工作階段。
1. hello 封包擷取 hello VM 上執行，並收集資料傳輸。
1. hello 封包擷取檔案上傳 tooa 檢閱及診斷的儲存體帳戶。

tooautomate 程序中，我們建立，並 hello 事件發生時，在我們的 VM tootrigger 連線警示。 我們也會建立到網路監看員的函式 toocall。

此案例中沒有 hello 遵循：

* 建立啟動封包擷取的 Azure 函式。
* 虛擬機器上建立警示規則並設定 hello 警示規則 toocall hello Azure 函式。

## <a name="create-an-azure-function"></a>建立 Azure 函式

hello 第一個步驟是 toocreate Azure 函式 tooprocess hello 警示，並建立封包擷取。

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，選取**新增** > **計算** > **函式應用程式**。

    ![建立函數應用程式][1-1]

2. 在 [hello**函式應用程式**刀鋒視窗中，輸入下列值的 hello，然後選取**確定**toocreate hello 應用程式：

    |**設定** | **值** | **詳細資料** |
    |---|---|---|
    |**應用程式名稱**|PacketCaptureExample|hello 的 hello 函式應用程式的名稱。|
    |**訂用帳戶**|[訂用帳戶] hello 哪些 toocreate hello 函式應用程式的訂用帳戶。||
    |**資源群組**|PacketCaptureRG|hello 資源群組 toocontain hello 函式應用程式。|
    |**主控方案**|取用方案| hello 類型的計劃您函式的應用程式使用。 選項有「取用」或 Azure App Service 方案。 |
    |**位置**|美國中部| 哪些 toocreate hello 函式應用程式中的 hello 區域。|
    |**儲存體帳戶**|{自動產生}| hello Azure 函式需要一般用途儲存體的儲存體帳戶。|

3. 在 [hello **PacketCaptureExample 函式應用程式**刀鋒視窗中，選取**函式** > **自訂函式** > ** +**.

4. 選取**HttpTrigger Powershell**，然後輸入 hello 剩餘資訊。 最後，toocreate hello 函式，選取**建立**。

    |**設定** | **值** | **詳細資料** |
    |---|---|---|
    |**案例**|實驗性|案例類型|
    |**函式命名**|AlertPacketCapturePowerShell|Hello 函式的名稱|
    |**授權層級**|函式|授權層級的 hello 函式|

![函式範例][functions1]

> [!NOTE]
> hello PowerShell 範本屬實驗性質，而且沒有完整的支援。

自訂所需的這個範例與 hello 步驟中說明。

### <a name="add-modules"></a>新增模組

toouse 網路監看員 PowerShell 指令程式上, 傳 hello 最新 PowerShell 模組 toohello 函式應用程式。

1. 在本機電腦與 hello 安裝最新 Azure PowerShell 模組，執行下列 PowerShell 命令的 hello:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    此範例提供下列 hello Azure PowerShell 模組的本機路徑。 在接下來的步驟中會用到這些資料夾。 此案例中使用的 hello 模組為：

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![PowerShell 資料夾][functions5]

1. 選取**函式應用程式設定** > **移 tooApp 服務編輯器**。

    ![函數應用程式設定][functions2]

1. 以滑鼠右鍵按一下 hello **AlertPacketCapturePowershell**資料夾，然後建立名為的資料夾**azuremodules**。 

4. 為您需要的每個模組建立子資料夾。

    ![資料夾和子資料夾][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. 以滑鼠右鍵按一下 hello **AzureRM.Network**子資料夾，然後再選取**上載檔案**。 

6. 移 tooyour Azure 模組。 Hello 本機**AzureRM.Network**資料夾中，選取 hello 資料夾中的 hello 的所有檔案。 然後選取 [確定]。 

7. 針對 **AzureRM.Profile** 和 **AzureRM.Resources** 重複這些步驟。

    ![上傳檔案][functions6]

1. 您已完成，每個資料夾應該具有 hello PowerShell 模組檔案從本機電腦。

    ![PowerShell 檔案][functions7]

### <a name="authentication"></a>驗證

toouse hello PowerShell cmdlet，您必須進行驗證。 您可以設定驗證 hello 函式應用程式中。 tooconfigure 驗證，您必須設定環境變數，並上傳加密的金鑰檔 toohello 函式應用程式。

> [!NOTE]
> 此案例中提供一個範例將示範如何搭配 Azure 函式的 tooimplement 驗證。 有其他方式 toodo 這。

#### <a name="encrypted-credentials"></a>加密的認證

下列 PowerShell 指令碼的 hello 建立金鑰檔稱為**PassEncryptKey.key**。 它也提供 hello 密碼所提供的加密的版本。 此密碼為 hello 定義用來驗證 hello Azure Active Directory 應用程式的相同密碼。

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

在 hello 的 hello 函式應用程式的應用程式服務編輯器，建立資料夾，稱為**金鑰**下**AlertPacketCapturePowerShell**。 然後上傳 hello **PassEncryptKey.key**在 hello 先前的 PowerShell 範例中所建立的檔案。

![函式金鑰][functions8]

### <a name="retrieve-values-for-environment-variables"></a>擷取環境變數的值

hello 最終的需求是 tooset hello 環境變數是可驗證的必要 tooaccess hello 值組成。 hello 下列清單顯示 hello 而建立的環境變數：

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

hello 用戶端識別碼是在 Azure Active Directory 之應用程式的應用程式識別碼 hello。

1. 如果您還沒有應用程式 toouse，執行下列範例 toocreate hello 應用程式。

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > hello 密碼時建立 hello 應用程式應該是 hello 使用您稍早建立 hello 金鑰檔案儲存時的相同密碼。

1. 在 [hello Azure 入口網站，選取 [**訂閱**。 選取 hello 訂用帳戶 toouse，，然後選取**存取控制 (IAM)**。

    ![函式 IAM][functions9]

1. 選擇 hello 帳戶 toouse，，然後選取**屬性**。 複製 hello 應用程式識別碼。

    ![函數應用程式識別碼][functions10]

#### <a name="azuretenant"></a>AzureTenant

藉由執行下列 PowerShell 範例 hello 取得 hello 租用戶識別碼：

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

您從執行下列 PowerShell 範例 hello 取得的 hello 值為 hello hello AzureCredPassword 環境變數值。 這個範例是 hello 同一個 hello 前面所示**加密認證**> 一節。 hello 所需的值是 hello hello 輸出`$Encryptedpassword`變數。  這是 hello 服務主體的密碼加密使用 hello PowerShell 指令碼。

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>存放區 hello 環境變數

1. 移 toohello 函式應用程式。 然後選取 [函數應用程式設定] > [設定應用程式設定]。

    ![進行應用程式設定][functions11]

1. 加入 hello 環境變數和其值 toohello 應用程式設定，然後選取**儲存**。

    ![應用程式設定][functions12]

### <a name="add-powershell-toohello-function"></a>新增 PowerShell toohello 函式

它是現在時間 toomake 內 hello Azure 函式呼叫從網路監看員。 根據 hello 的需求，此函式 hello 實作而有所不同。 不過，hello hello 程式碼的一般流程如下所示：

1. 處理輸入參數。
2. 查詢現有的封包擷取 tooverify 限制，並解決名稱衝突。
3. 使用適當的參數建立封包擷取。
4. 定期輪詢封包擷取，直到完成。
5. 通知 hello 使用者 hello 封包擷取工作階段已完成。

hello 下列範例是可以在 hello 函式中使用的 PowerShell 程式碼。 沒有需要 toobe 取代的值**subscriptionId**， **resourceGroupName**，和**storageAccountName**。

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>擷取 hello 函式 URL 
1. 您已建立您的函式之後，設定您的警示 toocall hello URL 與 hello 函式相關聯。 tooget 此值，請從您的函式應用程式複本 hello 函式的 URL。

    ![尋找 hello 函式 URL][functions13]

2. 複製應用程式函式的 hello 函式 URL。

    ![複製的 hello 函式 URL][2]

如果您需要在 hello 承載中的 hello webhook POST 要求的自訂屬性，請參閱太[Azure 度量警示上設定的 webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。

## <a name="configure-an-alert-on-a-vm"></a>在 VM 上設定警示

當特定的度量超出指定閾值時，警示可以是設定的 toonotify 個人 tooit。 在此範例中，hello 警示在 hello TCP 區段傳送，但可以用於許多其他的度量觸發 hello 警示。 在此範例中，警示會是設定的 toocall webhook toocall hello 函式。

### <a name="create-hello-alert-rule"></a>建立 hello 警示規則

移 tooan 現有的虛擬機器，然後再加入 [警示規則。 如需設定警示相關的詳細文件，請參閱[在 Azure 服務的 Azure 監視器中建立警示 - Azure 入口網站](../monitoring-and-diagnostics/insights-alerts-portal.md)。 輸入下列 hello 中的值的 hello**警示規則**刀鋒視窗中，然後再選取**確定**。

  |**設定** | **值** | **詳細資料** |
  |---|---|---|
  |**名稱**|TCP_Segments_Sent_Exceeded|Hello 警示規則的名稱。|
  |**說明**|傳送的 TCP 區段超出閾值|hello hello 警示規則的描述。||
  |**度量**|傳送的 TCP 區段| hello 度量 toouse tootrigger hello 警示。 |
  |**Condition**|大於| hello 條件 toouse 評估 hello 度量時。|
  |**閾值**|100| hello 觸發 hello 警示的 hello 標準值。 這個值應該設定 tooa 有效的值，為您的環境。|
  |**期間**|透過 hello 前五分鐘| 決定哪些 toolook 中的 hello 期間 hello 上 hello 度量的閾值。|
  |**Webhook**|[函數應用程式中的 Webhook URL]| hello 前述步驟中建立的 hello 函式應用程式中的 hello webhook URL。|

> [!NOTE]
> 預設不啟用 hello TCP 區段度量。 深入了解如何 tooenable 其他度量造訪[啟用監視和診斷](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)。

## <a name="review-hello-results"></a>檢閱 hello 結果

之後的 hello 警示觸發程序 hello 準則中，會建立封包擷取。 移 tooNetwork 監看員，然後再選取**封包擷取**。 這個頁面上，您可以選取 hello 封包擷取檔案連結 toodownload hello 封包擷取。

![檢視封包擷取][functions14]

如果在本機儲存 hello 擷取檔案，您可以登入 toohello 虛擬機器來擷取。

如需從 Azure 儲存體帳戶下載檔案的指示，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 另一個可用的工具是[儲存體總管](http://storageexplorer.com/)。

下載您的擷取後，您可以使用可讀取 **.cap** 檔案的任何工具來檢視它。 以下是這些工具的連結 tootwo:

- [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>後續步驟

了解如何 tooview 您擷取封包造訪[Wireshark 封包擷取分析](network-watcher-deep-packet-inspection.md)。


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
