---
title: "從範本的 aaaCreate Azure Service Fabric 叢集 |Microsoft 文件"
description: "本文說明如何 tooset 上安全的 Service Fabric 在 Azure 中使用叢集的 Azure 資源管理員，Azure 金鑰保存庫和 Azure Active Directory (Azure AD) 用戶端驗證。"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>使用 Azure Resource Manager 來建立 Service Fabric 叢集
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure 入口網站](service-fabric-cluster-creation-via-portal.md)
>
>

此逐步指南可逐步引導您使用 Azure Resource Manager 在 Azure 中設定安全的 Azure Service Fabric 叢集。 我們了解 hello 文件長度。 不過，除非您已徹底熟悉 hello 內容，是確定 toofollow 每個步驟謹慎。

hello 指南涵蓋下列程序的 hello:

* Azure 金鑰保存庫 tooupload 的憑證叢集和應用程式的安全性設定
* 使用 Azure Resource Manager 在 Azure 中建立受保護的叢集
* 使用適用於叢集管理的 Azure Active Directory (Azure AD) 來驗證使用者

需要安全的叢集，叢集來防止未經授權的存取 toomanagement 作業。 這包括部署、 升級，和刪除的應用程式、 服務，以及它們所包含的 hello 資料。 不安全的叢集是叢集的任何人都可以用來連接 tooat 任何時間，並執行管理作業。 雖然可能 toocreate 不安全的叢集，我們強烈建議您從 hello 一開始建立安全的叢集。 由於無法在稍後再針對不安全的叢集進行保護，因此必須建立新叢集。

建立安全叢集的 hello 概念是 hello 相同，，不論它們 Linux 或 Windows 叢集。 如需建立安全 Linux 叢集的詳細資訊和協助程式指令碼，請參閱[在 Linux 上建立安全叢集](#secure-linux-clusters)。

## <a name="sign-in-tooyour-azure-account"></a>Azure 帳戶登入 tooyour
本指南使用 [Azure PowerShell][azure-powershell]。 當您啟動新的 PowerShell 工作階段時，登入 tooyour Azure 帳戶，並選取您的訂用帳戶，然後再執行 Azure 命令。

Azure 帳戶登入 tooyour 中：

```powershell
Login-AzureRmAccount
```

選取您的訂用帳戶：

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>設定 Key Vault
本節說明如何為 Azure 中的 Service Fabric 叢集和為 Service Fabric 應用程式建立 Key Vault。 完整指南 tooAzure 金鑰保存庫，請參閱 toohello[金鑰保存庫快速入門指南][key-vault-get-started]。

服務網狀架構會使用 X.509 憑證 toosecure 叢集，並提供應用程式的安全性功能。 您可以使用金鑰保存庫 toomanage 憑證在 Azure 中的 Service Fabric 叢集。 在 Azure 中部署叢集時，會負責建立 Service Fabric 叢集的 hello Azure 資源提供者就會從金鑰保存庫提取憑證，並 hello 叢集 Vm 上進行安裝。

hello 下列圖表說明 hello Azure 金鑰保存庫、 Service Fabric 叢集和使用憑證時它會建立叢集儲存在金鑰保存庫中的 hello Azure 資源提供者之間的關聯性：

![憑證安裝圖][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>建立資源群組
hello 第一個步驟是 toocreate 特別針對金鑰保存庫的資源群組。 我們建議您將 hello 金鑰保存庫放入自己的資源群組。 這個動作可讓您移除 hello 運算和存放裝置資源群組，包括 hello 資源群組包含 Service Fabric 叢集，而不會遺失您的金鑰和密碼。 包含金鑰保存庫中的 hello 資源群組_hello 必須位於相同區域_為正在使用它的 hello 叢集。

如果您計劃在多個地區 toodeploy 叢集，我們建議您命名 hello 資源群組和 hello 金鑰保存庫中指出其所屬的區域的方式。  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
hello 輸出應該看起來像這樣：

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>在 hello 新資源群組中建立金鑰保存庫
hello 金鑰保存庫_必須為部署啟用_tooallow hello 計算資源提供者從它的 tooget 憑證，並將它安裝在虛擬機器執行個體上：

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

hello 輸出應該看起來像這樣：

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>使用現有的 Key Vault

toouse 現有的金鑰保存庫，您_必須為部署啟用_tooallow hello 計算資源提供者從它的 tooget 憑證，並將它安裝在叢集節點上：

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>新增憑證 tooyour 金鑰保存庫

憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。 如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例][service-fabric-cluster-security]。

### <a name="cluster-and-server-certificate-required"></a>叢集和伺服器憑證 (必要)
此憑證是必要的 toosecure 叢集，並防止未經授權的存取 tooit。 它會透過兩種方式提供叢集安全性：

* 叢集驗證：驗證叢集同盟的節點對節點通訊。 可以證明其身分識別與此憑證的節點可以加入 hello 叢集。
* 伺服器驗證： hello 叢集管理端點 tooa 管理會用戶端驗證，以便 hello 管理用戶端會知道它正在交涉 toohello 實際叢集。 此憑證也可提供 SSL hello HTTPS 管理 API 與 Service Fabric 總管透過 HTTPS。

這些的考量，hello 憑證必須符合下列需求的 hello tooserve:

* hello 憑證必須包含私密金鑰。
* 金鑰交換，也就是可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。
* hello 憑證的主體名稱必須符合您使用 tooaccess hello Service Fabric 叢集 hello 網域。 這項比對是必要的 tooprovide hello 叢集 HTTPS 管理端點的 SSL 和 Service Fabric 總管。 您無法從 hello 的憑證授權單位 (CA) 取得 SSL 憑證。 cloudapp.azure.com 網域。 您必須為您的叢集取得自訂網域名稱。 當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。

### <a name="application-certificates-optional"></a>應用程式憑證 (選用)
您可以針對應用程式安全性目的，在叢集上安裝任何數目的其他憑證。 之前建立您的叢集，請考慮需要這類 hello 節點上安裝憑證 toobe hello 應用程式安全性案例：

* 將應用程式組態值加密和解密。
* 在複寫期間將資料跨節點加密。

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>格式化憑證以供 Azure 資源提供者使用
您可以透過 Key Vault 來直接新增和使用私密金鑰檔案 (.pfx)。 不過，hello Azure 計算資源提供者需要特殊的 JavaScript Object Notation (JSON) 格式儲存的索引鍵 toobe。 hello 格式包括為 base 64 編碼的字串和 hello 私密金鑰密碼的 hello.pfx 檔案。 tooaccommodate 這些需求，機碼必須放置在 JSON 字串和儲存為 「 密碼 」 hello 機碼中的 hello 保存庫。

此程序會更方便地 toomake [PowerShell 模組是 github][service-fabric-rp-helpers]。 toouse hello 模組中，執行下列 hello:

1. Hello 的 hello 儲存機制的整個內容下載至本機目錄中。
2. 移 toohello 本機目錄。
2. 匯入您的 PowerShell 視窗中的 hello ServiceFabricRPHelpers 模組：

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

hello`Invoke-AddCertToKeyVault`此 PowerShell 模組中的命令自動將憑證的私密金鑰格式化為 JSON 字串，並將它上載 toohello 金鑰保存庫。 使用 hello 命令 tooadd hello 叢集憑證和任何其他應用程式憑證 toohello 金鑰保存庫。 任何額外的憑證，您要在叢集中的 tooinstall 重複此步驟。

#### <a name="uploading-an-existing-certificate"></a>上傳現有的憑證

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

如果您收到錯誤，例如 hello 其中一個在這裡顯示，通常表示您有資源 URL 衝突。 tooresolve hello 衝突，變更 hello 金鑰保存庫名稱。

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Hello 衝突解決後，hello 輸出看起來應該像這樣：

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>您需要 hello 三個上述字串，CertificateThumbprint，CertificateURL，安全 Service Fabric 叢集和 tooobtain tooset SourceVault，您也可以使用應用程式安全性的任何應用程式憑證。 如果您沒有儲存 hello 字串，可能很難 tooretrieve 稍後它們藉由查詢 hello 金鑰保存庫。

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>建立自我簽署的憑證，並將資料上傳 toohello 金鑰保存庫

如果您已上傳憑證 toohello 金鑰保存庫，請略過此步驟。 這個步驟是針對產生新的自我簽署的憑證，並將它上傳 tooyour 金鑰保存庫。 您變更 hello 下列指令碼中的 hello 參數，然後執行它之後，您應該會提示輸入憑證密碼。  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

如果您收到錯誤，例如 hello 其中一個在這裡顯示，通常表示您有資源 URL 衝突。 tooresolve hello 衝突、 變更 hello 金鑰保存庫名稱、 RG 名稱等等。

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Hello 衝突解決後，hello 輸出看起來應該像這樣：

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>您需要 hello 三個上述字串，CertificateThumbprint，CertificateURL，安全 Service Fabric 叢集和 tooobtain tooset SourceVault，您也可以使用應用程式安全性的任何應用程式憑證。 如果您沒有儲存 hello 字串，可能很難 tooretrieve 稍後它們藉由查詢 hello 金鑰保存庫。

 此時，您應該有下列項目就地 hello:

* hello 金鑰保存庫的資源群組。
* hello 金鑰保存庫和其 URL （hello 上述 PowerShell 輸出中稱為 SourceVault）。
* hello 叢集伺服器驗證憑證與它在 hello 金鑰保存庫的 URL。
* hello 應用程式憑證，且其 hello 金鑰保存庫中的 Url。


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>設定用戶端驗用的 Azure Active Directory

Azure AD 可讓組織 （也稱為租用戶） toomanage 使用者存取 tooapplications。 應用程式分成具有 Web 型登入 UI 的應用程式，以及具有原生用戶端體驗的應用程式。 在本文中，我們假設您已經建立租用戶。 如果您沒有這樣做，先閱讀[tooget Azure Active Directory 的租用戶][active-directory-howto-tenant]。

Service Fabric 叢集提供數個進入點 tooits 管理功能，包括 web 為基礎的 hello [Service Fabric 總管][ service-fabric-visualizing-your-cluster]和[Visual Studio][service-fabric-manage-application-in-visual-studio]. 如此一來，您會建立兩個 Azure AD 應用程式 toocontrol 存取 toohello 叢集、 一個 web 應用程式和一個原生應用程式。

toosimplify 部分 hello 步驟涉及設定 Azure AD 與 Service Fabric 叢集，我們已經建立一組 Windows PowerShell 指令碼。

> [!NOTE]
> 您必須完成下列步驟，才能建立 hello 叢集 hello。 Hello 指令碼預期的叢集名稱和端點，因為 hello 值應該計劃，而且不確定您已經建立的值。

1. [下載 hello 指令碼][ sf-aad-ps-script-download] tooyour 電腦。
2. 以滑鼠右鍵按一下 hello zip 檔，請選取**屬性**，選取 hello**解除封鎖**核取方塊，然後**套用**。
3. Hello zip 檔案解壓縮。
4. 執行`SetupApplications.ps1`，並提供 hello TenantId，ClusterName 和 WebApplicationReplyUrl 做為參數。 例如：

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    您可以藉由執行 hello PowerShell 命令來找到您 TenantId `Get-AzureSubscription`。 執行這個命令會顯示每個訂用帳戶的 hello TenantId。

    ClusterName 是使用的 tooprefix hello Azure AD 應用程式所建立的 hello 指令碼。 它不會完全不需要 toomatch hello 實際叢集名稱。 它會預期只有 toomake 它更容易 toomap Azure AD 成品 toohello Service Fabric 叢集是要搭配使用。

    WebApplicationReplyUrl 是 Azure AD 傳回 tooyour 使用者在完成登入之後的 hello 預設端點。 將此端點設定為叢集，其預設值是 hello Service Fabric 總管端點：

    https://&lt;cluster_domain&gt;:19080/Explorer

    您必須提示的 toosign tooan 帳戶具有系統管理權限 hello Azure AD 租用戶中。 登入之後，hello 指令碼會建立 hello web 和原生應用程式 toorepresent Service Fabric 叢集。 如果您查看 hello 租用戶的應用程式在 hello [Azure 傳統入口網站][azure-classic-portal]，您應該會看到兩個新項目：

   * *ClusterName*\_叢集
   * *ClusterName*\_用戶端

   hello 指令碼會列印的 hello JSON，因此它是個不錯的主意 tookeep hello PowerShell 視窗，在 hello 下一步 區段中，建立 hello 叢集時，所需的 hello Azure Resource Manager 範本開啟。

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>建立 Service Fabric 叢集 Resource Manager 範本
在本節中，hello 輸出的 hello 上述 Service Fabric 叢集資源管理員範本中使用 PowerShell 命令。

範例資源管理員範本位於 hello [GitHub 上的 Azure 快速入門範本圖庫][azure-quickstart-templates]。 這些範本可以用作叢集範本的起點。

### <a name="create-hello-resource-manager-template"></a>建立 hello Resource Manager 範本
本指南使用 hello [5 節點安全叢集][ service-fabric-secure-cluster-5-node-1-nodetype]範例範本和範本參數。 下載`azuredeploy.json`和`azuredeploy.parameters.json`tooyour 電腦並在您慣用的文字編輯器中開啟這兩個檔案。

### <a name="add-certificates"></a>新增憑證
您新增憑證 tooa 叢集資源管理員範本，藉由參考包含 hello 憑證金鑰的 hello 金鑰保存庫。 我們建議您在資源管理員範本參數檔案中放入 hello 金鑰保存庫的值。 這樣可防止 hello 資源管理員範本檔案可重複使用和可用的值特定 tooa 部署。

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>將所有憑證 toohello 虛擬機器規模都集 osProfile
安裝 hello 叢集中的每個憑證必須設定一節 hello osProfile hello 標尺之資源集 (Microsoft.Compute/virtualMachineScaleSets)。 這個動作會指示 hello 資源提供者 tooinstall hello 憑證 hello Vm 上。 此安裝包括 hello 叢集憑證和任何 toouse 規劃您的應用程式的應用程式的安全性憑證：

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>設定 hello Service Fabric 叢集憑證
hello 叢集驗證憑證必須由兩個 hello Service Fabric 叢集資源 (Microsoft.ServiceFabric/clusters) 和 hello Service Fabric 擴充功能的虛擬機器規模設定中 hello 虛擬機器規模集資源。 這種安排可讓 hello Service Fabric 資源提供者 tooconfigure 它用於叢集驗證及管理端點的伺服器驗證。

##### <a name="virtual-machine-scale-set-resource"></a>虛擬機器擴展集資源：
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Service Fabric 資源︰
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>插入 Azure AD 組態
您稍早建立的 hello Azure AD 設定直接插入 Resource Manager 範本。 不過，我們建議您先 hello 值擷取成參數檔案 tookeep hello 資源管理員範本可重複使用和可用值的特定 tooa 部署。

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a>設定 Resource Manager 範本參數
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
最後，使用從 hello 金鑰保存庫和 Azure AD PowerShell 命令 toopopulate hello 參數檔案的 hello 輸出值：

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
此時，您應該有下列項目就地 hello:

* Key Vault 資源群組
  * 金鑰保存庫
  * 叢集伺服器驗證憑證
  * 資料編密憑證
* Azure Active Directory 租用戶
  * 適用於 Web 型管理和 Service Fabric Explorer 的 Azure AD 應用程式
  * 適用於原生用戶端管理的 Azure AD 應用程式
  * 使用者及其獲指派的角色
* Service Fabric 叢集 Resource Manager 範本
  * 透過 Key Vault 設定的憑證
  * 已設定 Azure Active Directory

hello 下列圖表說明您的金鑰保存庫和 Azure AD 設定放入 Resource Manager 範本的位置。

![Resource Manager 相依性對應][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>建立 hello 叢集
現在您已經準備就緒 toocreate hello 叢集使用[Azure 資源範本部署][resource-group-template-deploy]。

#### <a name="test-it"></a>進行測試
使用下列 PowerShell 命令 tootest hello Resource Manager 範本參數檔案：

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>進行部署
如果 hello 資源管理員範本測試成功，使用下列 PowerShell 命令 toodeploy hello Resource Manager 範本參數檔案：

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>指派使用者 tooroles
您已建立 hello 應用程式 toorepresent 您的叢集之後，您的使用者 toohello 將角色指派支援的 Service Fabric： 唯讀和系統管理員。您可以使用 hello 指派 hello 角色[Azure 傳統入口網站][azure-classic-portal]。

1. 在 hello Azure 入口網站，移 tooyour 租用戶，然後選取**應用程式**。
2. 選取 hello web 應用程式，有一個名稱類似`myTestCluster_Cluster`。
3. 按一下 hello**使用者** 索引標籤。
4. 選取使用者 tooassign，，然後按一下hello**指派**在 hello 囉 」 畫面底部的按鈕。

    ![指派使用者 tooroles 按鈕][assign-users-to-roles-button]
5. 選取 hello 角色 tooassign toohello 使用者。

    ![[指派使用者] 對話方塊][assign-users-to-roles-dialog]

> [!NOTE]
> 如需 Service Fabric 中角色的詳細資訊，請參閱 [角色型存取控制 (適用於 Service Fabric 用戶端)](service-fabric-cluster-security-roles.md)。
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>在 Linux 上建立安全叢集
我們已提供 toomake hello 程序更容易， [helper 指令碼](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux)。 在使用此協助程式指令碼之前，請確定您已安裝 Azure 命令列介面 (CLI)，而且它位於您的路徑中。 請確定 hello 指令碼執行具有權限 tooexecute`chmod +x cert_helper.py`下載它之後。 hello 第一個步驟是 toosign tooyour Azure 帳戶中的使用以 hello CLI`azure login`命令。 登入 tooyour Azure 帳戶之後，使用 hello helper 簽署指令碼與您的 CA 憑證，以下列命令顯示 hello:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

hello-ifile 參數可以採用.pfx 檔案或.pem 檔案，做為輸入，與 hello 憑證類型 （pfx 或 pem 或如果它是自我簽署的憑證的 ss）。
hello 參數-h 會列印出 hello 說明文字。


此命令會傳回下列三個字串做為 hello 輸出 hello:

* SourceVaultID，是 hello 識別碼 hello 它為您建立新的 KeyVault 資源群組
* CertificateUrl 存取 hello 憑證
* CertificateThumbprint：用於驗證。

hello 下列範例顯示如何 toouse hello 命令：

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
執行上述命令可讓您 hello 三個字串，如下所示的 hello:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

hello 憑證的主體名稱必須符合您使用 tooaccess hello Service Fabric 叢集 hello 網域。 此比對會需要的 tooprovide hello 叢集 HTTPS 管理端點的 SSL 和 Service Fabric 總管。 您無法取得 SSL 憑證，從 CA hello`.cloudapp.azure.com`網域。 您必須為您的叢集取得自訂網域名稱。 當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。

這些主旨名稱是 hello 項目需要 toocreate 安全 Service Fabric 叢集 （不含 Azure AD)，依照[設定資源管理員範本參數](#configure-arm)。 您可以依照下列指示 hello 連接 toohello 安全叢集[驗證用戶端存取 tooa 叢集](service-fabric-connect-to-secure-cluster.md)。 Linux 預覽叢集不支援 Azure AD 驗證。 Hello 中所述，您可以指派系統管理員和用戶端角色[指派角色 toousers](#assign-roles) > 一節。 當您指定 Linux 預覽叢集的系統管理員和用戶端角色時，您必須驗證 tooprovide 憑證指紋。 （您未提供 hello 主體名稱，因為沒有鏈結驗證或撤銷執行在此預覽版本。）

如果您想 toouse 自我簽署憑證進行測試時，您可以使用 hello 相同的指令碼 toogenerate 其中一個。 您可以藉由提供 hello 旗標然後上傳 hello 憑證 tooyour 金鑰保存庫`ss`而不是提供 hello 憑證路徑和憑證名稱。 例如，請參閱下列命令來建立及上傳的自我簽署的憑證的 hello:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
此命令傳回 hello 相同的三個字串： SourceVault、 CertificateUrl 和 CertificateThumbprint。 然後，您可以使用 hello 字串 toocreate hello 自我簽署的憑證所在的位置和安全的 Linux 叢集。 您需要 hello 自我簽署的憑證 tooconnect toohello 叢集。 您可以依照下列指示 hello 連接 toohello 安全叢集[驗證用戶端存取 tooa 叢集](service-fabric-connect-to-secure-cluster.md)。

hello 憑證的主體名稱必須符合您使用 tooaccess hello Service Fabric 叢集 hello 網域。 此比對會需要的 tooprovide hello 叢集 HTTPS 管理端點的 SSL 和 Service Fabric 總管。 您無法取得 SSL 憑證，從 CA hello`.cloudapp.azure.com`網域。 您必須為您的叢集取得自訂網域名稱。 當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。

Hello 中所述，也可以填入 hello Azure 入口網站中的 hello helper 指令碼中的 hello 參數[hello Azure 入口網站中建立叢集](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)> 一節。

## <a name="next-steps"></a>後續步驟
此時，您已具有以 Azure Active Directory 提供管理驗證的安全叢集。 下一步 [tooyour 叢集連線](service-fabric-connect-to-secure-cluster.md)並了解如何太[管理應用程式密碼](service-fabric-application-secret-management.md)。

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>針對設定用戶端驗用的 Azure Active Directory 進行疑難排解
如果遇到問題時您正要設定 Azure AD 用戶端驗證，請，檢閱本節中的 hello 可能解決方案。

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric 總管會提示您 tooselect 憑證
#### <a name="problem"></a>問題
登入成功 tooAzure AD Service Fabric 總管中後，hello 瀏覽器傳回 toohello 首頁上，但會有訊息提示 tooselect 憑證。

![SFX 選取憑證對話方塊][sfx-select-certificate-dialog]

#### <a name="reason"></a>原因
hello 使用者未獲派 hello Azure AD 叢集應用程式中的角色。 因此，Azure AD 驗證在 Service Fabric 叢集上發生失敗。 Service Fabric 總管會回到 toocertificate 驗證。

#### <a name="solution"></a>方案
請依照 hello 指示來設定 Azure AD，與指派使用者角色。 此外，我們建議您開啟 「 指派必要的 tooaccess 應用程式的使用者 」，為`SetupApplications.ps1`沒有。

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>使用 PowerShell 連線失敗，發生錯誤: 「 hello 指定認證不正確 」
#### <a name="problem"></a>問題
當您使用 PowerShell tooconnect toohello 叢集使用 「 AzureActiveDirectory"安全性模式，您已成功 tooAzure AD 在登入後時，hello 連線會失敗並發生錯誤: 「 hello 指定認證不正確 」。

#### <a name="solution"></a>方案
這個解決方案相當的 hello 與相同 hello 之前。

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer 在您登入時傳回失敗："AADSTS50011"
#### <a name="problem"></a>問題
Hello 頁面當您嘗試 toosign tooAzure AD 中 Service Fabric 總管中的時，傳回的失敗:"AADSTS50011: hello 的回覆地址&lt;url&gt; hello hello 應用程式設定的回覆地址不符： &lt;guid&gt;."

![SFX 回覆地址不相符][sfx-reply-address-not-match]

#### <a name="reason"></a>原因
代表 Service Fabric 總管 hello 叢集 (web) 應用程式嘗試 tooauthenticate 針對 Azure AD，並為 hello 要求的一部分提供 hello 重新導向的傳回 URL。 Hello URL 未列在 hello Azure AD 應用程式，但是**回覆 URL**清單。

#### <a name="solution"></a>方案
在 [hello**設定**hello] 索引標籤叢集 (web) 應用程式，請新增 hello Service Fabric 總管 URL toohello**回覆 URL**清單，或取代其中一個 hello hello 清單中的項目。 完成時，請儲存變更。

![Web 應用程式回覆 url][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Hello 叢集連線使用透過 PowerShell 的 Azure AD 驗證
tooconnect hello Service Fabric 叢集將使用下列 PowerShell 命令範例 hello:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn 有關 hello Connect-servicefabriccluster cmdlet，請參閱[Connect-servicefabriccluster](https://msdn.microsoft.com/library/mt125938.aspx)。

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>可以重複使用多個群集中的 hello 相同的 Azure AD 租用戶嗎？
是。 但是請記住 tooadd hello Service Fabric 總管 URL tooyour 叢集 (web) 應用程式。 否則 Service Fabric Explorer 無法運作。

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>為什麼在已啟用 Azure AD 的情況下仍然需要伺服器憑證？
FabricClient 和 FabricGateway 會執行相互驗證。 Azure AD 在驗證期間，Azure AD 的整合會提供用戶端身分識別 toohello 伺服器，且 hello 伺服器憑證使用的 tooverify hello 伺服器身分識別。 如需有關 Service Fabric 憑證的詳細資訊，請參閱 [X.509 憑證和 Service Fabric][x509-certificates-and-service-fabric]。

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

