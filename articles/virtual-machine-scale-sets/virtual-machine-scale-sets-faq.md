---
title: "aaaAzure 虛擬機器規模設定常見問題集 |Microsoft 文件"
description: "取得虛擬機器擴展集相關常見問題的解答 toofrequently。"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Azure 虛擬機器擴展集常見問題集

取得在 Azure 中設定 toofrequently 關於虛擬機器規模集的解答。

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>什麼是 Azure 自動調整的最佳做法？

如需自動調整的最佳做法，請參閱[自動調整虛擬機器的最佳做法](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices)。

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>哪裡可以找到使用主機型計量自動調整的計量名稱？

如需使用主機型計量之自動調整的計量名稱，請參閱[支援的 Azure 監視器度量](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/)。

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>是否有任何根據 Azure 服務匯流排主題和佇列長度自動調整的範例？

是。 如需根據 Azure 服務匯流排主題和佇列長度自動調整的範例，請參閱 [Azure 監視器的自動調整常用計量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)。

服務匯流排佇列，請使用下列 JSON hello:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

儲存體佇列，請使用下列 JSON hello:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

以您資源的統一資源識別項 (URI) 取代範例值。


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>我應該使用主機型計量或診斷擴充功能進行自動調整？

您可以建立自動調整設定在 VM toouse 主機層級度量或客體作業系統為基礎的度量。

如需支援的計量資訊，請參閱 [Azure 監視器的自動調整常見計量](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics)。 

如需虛擬機器擴展集的完整範例，請參閱[使用虛擬機器擴展集的 Resource Manager 範本進行進階自動調整設定](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets)。 

hello 範例會使用 hello 主機層級 CPU 度量和訊息計數 」 指標。



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>如何設定虛擬機器擴展集的警示規則？

您可以透過 PowerShell 或 Azure CLI，建立虛擬機器擴展集計量的警示。 如需詳細資訊，請參閱 [Azure 監視器 PowerShell 快速入門範例](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules)和 [Azure 監視器跨平台 CLI 快速入門範例](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts)。

hello TargetResourceId hello 虛擬機器擴展集看起來像這樣： 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

您可以選擇任何 VM 效能計數器為 hello 度量 tooset 的警示。 如需詳細資訊，請參閱[資源管理員為基礎的 Windows Vm 的客體 OS 度量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms)和[適用於 Linux Vm 的客體 OS 度量](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms)在 hello [Azure 監視自動調整常見標準](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)發行項。

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>如何使用 PowerShell 在虛擬機器擴展集上設定自動調整？

tooset 設定自動調整規模上的虛擬機器擴展集使用 PowerShell，請參閱 hello 部落格文章[tooadd 自動調整規模 tooan Azure 虛擬機器規模的設定方式](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/)。




## <a name="certificates"></a>憑證

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>如何安全地發行憑證 toohello VM？ 如何佈建虛擬機器規模集 toorun 其中 hello hello 網站的 SSL 於安全的憑證設定的網站？ (hello 常見的憑證旋轉作業將會幾乎 hello 相同的組態更新作業。)您是否有如何的範例 toodo 這？ 

toosecurely 出貨憑證 toohello VM，您可以直接在 hello 客戶的金鑰保存庫中的 Windows 憑證存放區安裝客戶憑證。

使用下列 JSON hello:

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

hello 的程式碼支援 Windows 和 Linux。

如需詳細資訊，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/mt589035.aspx)。


### <a name="example-of-self-signed-certificate"></a>自我簽署憑證的範例

1.  在金鑰保存庫中建立自我簽署憑證。

    使用下列 PowerShell 命令的 hello:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    此命令提供下列 hello hello Azure Resource Manager 範本的輸入。

    如需如何 toocreate 自我簽署的憑證中金鑰保存庫，請參閱[Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)。

2.  變更 hello Resource Manager 範本。

    新增此屬性太**virtualMachineProfile**，hello 一部分的虛擬機器規模集資源：

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>可以指定 SSH 驗證 SSH 金鑰組的 toouse 設定資源管理員範本中的 Linux 虛擬機器比例嗎？  

是。 hello REST API 的**osProfile**是類似 toohello 標準 VM REST API。 

在您的範本中包含 **osProfile**︰

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
在中使用此 JSON 區塊[hello 101-vm-sshkey GitHub 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)。
 
hello OS 設定檔也會用於[hello grelayhost.json GitHub 快速啟動範本](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json)。

如需詳細資訊，請參閱[建立或更新虛擬機器擴展集](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration)。
  

### <a name="how-do-i-remove-deprecated-certificates"></a>如何移除已被取代的憑證？ 

tooremove 取代 hello 保存庫憑證清單中移除 hello 舊憑證的憑證。 將保留的 tooremain hello 清單中電腦上的所有 hello 憑證。 這不會移除 hello 憑證所有 Vm。 它也不會新增 hello 憑證 toonew hello 虛擬機器規模集中建立的 Vm。 

現有的 Vm 所傳來的 tooremove hello 憑證撰寫自訂指令碼延伸 toomanually 移除 hello 憑證從憑證存放區。
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>我如何插入現有的 SSH 公開金鑰 hello 虛擬機器規模集 SSH 層佈建期間？ 我想 toostore hello SSH 公開金鑰值在 Azure 金鑰保存庫，然後在 我的資源管理員範本中使用它們。

如果您要提供 hello Vm 只能與 SSH 公開金鑰，您不需要 tooput hello 公用金鑰在金鑰保存庫。 公開金鑰不是密碼。
 
您可以在建立 Linux VM 時以純文字提供 SSH 公開金鑰：

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
linuxConfiguration 元素名稱 | 必要 | 類型 | 說明
--- | --- | --- | --- |  ---
ssh | 否 | 集合 | 指定 Linux 作業系統的 hello SSH 金鑰設定
路徑 | 是 | String | 指定其中 hello SSH 金鑰或憑證應該位於 hello Linux 檔案路徑
keyData | 是 | String | 指定 base64 編碼的 SSH 公開金鑰

如需範例，請參閱[hello 101-vm-sshkey GitHub 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)。

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>當我執行`Update-AzureRmVmss`之後從 hello 加入一個以上的憑證相同金鑰保存庫，我看到下列訊息 hello:
 
>Update-AzureRmVmss: 清單密碼包含重複的 /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev 執行個體，不允許這種情況。
 
如果您嘗試 toore 此情形-新增的 hello 相同保存庫而不是使用新的保存庫憑證 hello 現有來源保存庫。 hello`Add-AzureRmVmssSecret`命令無法正常運作如果您要新增其他機密資料。
 
tooadd hello 從多個密碼相同的金鑰保存庫中，更新 hello $vmss.properties.osProfile.secrets[0].vaultCertificates 清單。
 
如 hello 預期輸入的結構，請參閱 <<c0> [ 建立或更新虛擬機器設定](https://msdn.microsoft.com/library/azure/mt589035.aspx)。
 
尋找在 hello 虛擬機器規模集物件的 hello 金鑰保存庫中的 hello 密碼。 接著，新增您 hello 保存庫相關聯的憑證 （hello URL 和 hello 密碼存放區名稱） 的參考 toohello 清單。

> [!NOTE] 
> 目前，您無法使用 hello 虛擬機器規模集 API，從 Vm 移除憑證。
>

新的 Vm 不會有 hello 舊的憑證。 不過，具有 hello 憑證，且其已部署的 Vm 會具備 hello 舊憑證。
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>可以推播憑證 toohello 虛擬機器擴展集而不需 hello 密碼存放區 hello 憑證時提供 hello 密碼嗎？

您不需要 toohard 程式碼在指令碼中的密碼。 您可以動態擷取密碼與 hello 權限，您使用 toorun hello 部署指令碼。 如果您將憑證移動 hello 密碼存放區的金鑰保存庫中的指令碼，hello 密碼存放區`get certificate`命令也會輸出 hello hello.pfx 檔案的密碼。
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>虛擬機器規模的 virtualMachineProfile.osProfile hello 機密屬性如何設定工作？ 當使用 hello certificateUrl 屬性 hello 憑證的絕對 URI 的 toospecify 為什麼需要 hello sourceVault 值？ 

Windows 遠端管理 (WinRM) 憑證參考中必須要有 hello hello OS 設定檔的密碼屬性。 

指出 hello 來源保存庫的 hello 目的是 tooenforce 存取控制清單 (ACL) 原則存在於使用者的 Azure 雲端服務模型中。 如果未指定 hello 來源保存庫，沒有權限 toodeploy 或存取機密資料 tooa 金鑰保存庫的使用者將能夠 toothrough 計算資源提供者 (CRP)。 甚至不存在的資源也會有 ACL。

如果您提供有效的金鑰保存庫 URL 但不正確的來源保存庫識別碼，輪詢 hello 作業時報告錯誤。
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>如果我要加入現有的虛擬機器規模集的密碼 tooan，hello 機密資料插入到現有的 Vm，或只有新的嗎？ 

憑證會加入 tooall Vm，即使預先存在的。 如果您的虛擬機器規模集 upgradePolicy 屬性設定太**手動**，hello 憑證會新增 toohello VM，當您在 hello VM 上執行的手動更新。
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>將 Linux VM 的憑證放在哪裡？

如何 toodeploy 憑證適用於 Linux Vm，請參閱的 toolearn[部署從客戶管理的金鑰保存庫憑證 tooVMs](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/)。
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>如何新增新保存庫憑證 tooa 新憑證的物件？

tooadd 保存庫憑證 tooan 現有密碼，請參閱下列 PowerShell 範例 hello。 只使用一個密碼物件。
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>發生什麼情況 toocertificates VM 重新製作映像？

如果您重新安裝 VM 映像，則會刪除憑證。 刪除 hello 整個作業系統磁碟重新安裝映像。 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>如果您從 hello 金鑰保存庫刪除憑證，怎樣？

如果從 hello 金鑰保存庫中刪除 hello 密碼，然後執行`stop deallocate`為您的 Vm，然後再次啟動，您將遇到失敗。 hello 失敗發生因為 hello CRP 需要 tooretrieve hello 金鑰保存庫中的 hello 機密資料，但它不能。 在此案例中，您可以刪除 hello 憑證從 hello 虛擬機器規模集模型。 

hello CRP 元件不會保留客戶機密資料。 如果您執行`stop deallocate`hello 虛擬機器規模集中的所有 vm，已刪除的 hello 快取。 在此案例中，從 hello 金鑰保存庫擷取密碼。

向外延展，因為沒有快取的密碼的複本 hello Azure Service Fabric 中 （在 hello 單一網狀架構租用戶模型） 時，不會遇到這個問題。
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>為什麼必須 hello 憑證 URL 的 toospecify hello 確切位置 (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>)，如下所示[Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)？
 
hello Azure Key Vault 文件會指出該 hello 取得密碼 REST API 應傳回 hello hello 密碼的最新的版本，如果未指定 hello 版本。
 
方法 | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{密碼-名稱}/{密碼-版本}?api-version={api-版本}

取代 {*密碼名稱*} 與 hello 名稱取代 {*密碼-版本*} 想 tooretrieve hello 版本 hello 密碼。 可能會排除 hello 密碼版本。 在此情況下，會擷取 hello 目前版本。
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>為什麼當我使用金鑰保存庫有 toospecify hello 憑證版本？

hello 目的 hello 金鑰保存庫需求 toospecify hello 憑證版本是的 toomake 它清除 toohello 使用者 Vm 上部署何種憑證。

如果您建立的 VM，然後更新您的密碼在 hello 金鑰保存庫 hello 新憑證不是下載的 tooyour Vm。 但您的 Vm 會出現 tooreference，且新的 Vm 取得 hello 新密碼。 tooavoid，您會需要的 tooreference 密碼版本。

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>我的小組會搭配幾個散發 toous 為.cer 公開金鑰的憑證。 什麼是建議的方法來部署這些憑證 tooa 虛擬機器規模集的 hello？

toodeploy.cer 公開金鑰 tooa 虛擬機器規模集，您可以產生僅包含.cer 檔案的.pfx 檔案。 toodo 此，請使用`X509ContentType = Pfx`。 例如，當做 C# 或 PowerShell 中的 x509Certificate2 物件載入 hello.cer 檔案，然後呼叫 hello 方法。 

如需詳細資訊，請參閱 [X509Certificate.Export 方法 (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx))。

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>我看不到憑證中的使用者 toopass 選項 base64 字串。 大部分其他資源提供者都有這個選項。

tooemulate 傳入做為 base64 字串憑證，您可以擷取 hello 最新版本 URL 中的資源管理員範本。 包括下列資源管理員範本中的 JSON 屬性的 hello:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>有金鑰保存庫中的 JSON 物件中 toowrap 憑證嗎？

在虛擬機器擴展集和 VM 中，憑證必須包裝在 JSON 物件中。 

我們也支援 hello 內容類型的應用程式/x-pkcs12。 如需使用 application/x-pkcs12 的相關指示，請參閱 [Azure Key Vault 中的 PFX 憑證](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/)。
 
我們目前不支援 .cer 檔案。 toouse.cer 檔案，將它們匯出到.pfx 容器。



## <a name="compliance"></a>法規遵循

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>虛擬機器擴展集符合 PCI 規範嗎？

虛擬機器擴展集是之上 hello CRP 精簡型的應用程式開發介面層級。 兩個元件均 hello Azure 服務樹狀目錄中的 hello 運算平台的一部分。

相容性的觀點而言，虛擬機器擴展集是 hello Azure 運算平台的基礎部分。 它們 hello CRP 本身的情況下，共用小組、 工具、 處理程序、 部署方法，安全性控制，在 just-in-time (JIT) 編譯、 監視、 警示與等等。 虛擬機器擴展集是付款卡產業 (PCI)-因為 hello CRP 屬於 hello 目前 PCI 資料安全標準 (DSS) 情況證明相容。

如需詳細資訊，請參閱[hello Microsoft 信任中心](https://www.microsoft.com/TrustCenter/Compliance/PCI)。






## <a name="extensions"></a>擴充功能

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>如何刪除虛擬機器擴展集擴充功能？

toodelete 的虛擬機器擴展集延伸模組，使用下列 PowerShell 範例的 hello:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
您可以找到中的 hello extensionName 值`$vmss`。
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>是否有與 Operations Management Suite 整合的虛擬機器擴展集範本範例？

虛擬機器擴展集整合與 Operations Management Suite 的範本範例，請參閱中的 hello 第二個範例[部署 Azure Service Fabric 叢集，並啟用監視，可使用記錄分析](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric)。
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>延伸模組看起來 toorun 以平行方式上的虛擬機器規模集。 這會導致我的自訂指令碼延伸 toofail。 怎麼 toofix 這？

請參閱 < 關於虛擬機器擴展集，在擴充功能順序 toolearn[在 Azure 虛擬機器擴展集延伸模組排序](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)。
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>如何重設 hello 密碼對於 Vm 在我的虛擬機器規模集？

Vm 的虛擬機器規模的 tooreset hello 密碼設定，請使用 VM 存取擴充功能。 

使用下列 PowerShell 範例 hello:

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>如何在我的虛擬機器規模集中新增擴充功能 tooall Vm？

如果更新原則設定太**自動**，重新部署的 hello 新延伸模組屬性的 hello 範本更新所有 Vm。

如果更新原則設定太**手動**，第一次更新 hello 副檔名，並以手動方式更新您的 Vm 中的所有執行個體。

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Hello 與現有的虛擬機器規模集相關聯的延伸模組更新時，如果現有的 Vm 會受到影響？ (也就是將 hello Vm*不*相符 hello 虛擬機器擴充集模型嗎？)或者會忽略它們？ 當現有的機器是服務修復或重新安裝映像時，會 hello hello 虛擬機器規模集執行，目前設定的指令碼或 hello 指令碼已設定使用時，會先建立 VM 的 hello？

如果 hello 延伸定義在 hello 虛擬機器擴展集模型已更新，而且 hello upgradePolicy 屬性設定太**自動**，它會更新 hello Vm。 如果 hello upgradePolicy 屬性設定太**手動**，延伸模組已標示為不符合 hello 模型。 

如果服務修復現有的 VM，它會顯示為重新開機，並 hello 擴充功能不會重新執行。 如果它的映像後，就像是 hello 作業系統磁碟機取代 hello 來源映像。 執行從 hello 最新的模型，例如延伸模組的任何特製化。
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>如何將虛擬機器規模集 tooan Azure AD 網域的聯結？

toojoin 虛擬機器規模集 tooan Azure Active Directory (Azure AD) 網域，您可以定義擴充功能。 

toodefine 擴充功能，使用 hello JsonADDomainExtension 屬性：

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>我的虛擬機器規模集擴充功能正嘗試 tooinstall 而需要重新開機的項目。 例如："commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"

如果虛擬機器規模集擴充功能會嘗試 tooinstall 而需要重新開機的項目，您可以使用 hello Azure 自動化 Desired State Configuration (Automation DSC) 的延伸模組。 如果 hello 作業系統是 Windows Server 2012 R2，Azure 會提取在 hello Windows Management Framework (WMF) 5.0 安裝程式中重新開機，然後再繼續執行 hello 組態。 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>如何在虛擬機器擴展集中開啟反惡意程式碼？

tooturn 虛擬機器的標尺上的反惡意程式碼上設定，請使用下列 PowerShell 範例 hello:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>我需要 tooexecute 裝載在私人儲存體帳戶中之自訂指令碼。 hello 指令碼順利執行時 hello 儲存體是公用的但是當我嘗試 toouse 共用存取簽章 (SAS)，它將會失敗。 隨即顯示此訊息：「遺漏有效的共用存取簽章的強制參數」。 Link+SAS 可從我的本機瀏覽器正常運作。

tooexecute 裝載在私人儲存體帳戶之自訂指令碼會設定與 hello 儲存體帳戶金鑰和名稱的受保護的設定。 如需詳細資訊，請參閱[適用於 Windows 的自訂指令碼擴充功能](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings)。







## <a name="networking"></a>網路
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>是否可能 tooassign 網路安全性群組 (NSG) tooa 縮放設定，讓它將會套用在 hello 集中 tooall hello VM Nic？

是。 直接 tooa 規模調整集合參考 hello networkInterfaceConfigurations hello 網路設定檔 區段中，可以套用網路安全性群組。 範例：

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>如何進行 VIP 交換的虛擬機器規模集中 hello 相同訂用帳戶和相同的區域？

如果您有兩個虛擬機器規模設定具有 Azure 負載平衡器前端，而且它們處於 hello 相同訂用帳戶和地區，您無法取消配置每個從 hello 公用 IP 位址，並指派其他 toohello。 例如，請參閱 [VIP 交換：Azure Resource Manager 中藍綠色版本部署](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) \(英文\)。 雖然 hello 資源會取消配置/配置在 hello 網路層級意味著延遲。 更快的選項是使用兩個後端集區和路由規則 toouse Azure 應用程式閘道。 或者，您可以透過 [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/) 裝載應用程式，以提供在預備與生產位置之間快速切換的支援。
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>如何指定的私人 IP 位址 toouse 靜態私人 IP 位址配置的範圍？

系統會從您指定的子網路選取 IP 位址。 

hello 配置方法的虛擬機器規模集的 IP 位址永遠是 「 動態 」，但這並不表示這些 IP 位址，可以變更。 在此情況下，「 動態 」 只表示您沒有在 PUT 要求中指定 hello IP 位址。 指定 hello 靜態使用 hello 子網路設定。 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>我要如何部署虛擬機器規模集 tooan 現有 Azure 虛擬網路？ 

toodeploy 的虛擬機器擴展集 tooan 現有的 Azure 虛擬網路，請參閱[部署虛擬機器規模集 tooan 現有虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet)。 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>如何新增 hello IP 位址第一個 VM 中的虛擬機器擴展集 toohello 範本輸出的 hello？

hello tooadd hello IP 位址第一個 VM 範本時，虛擬機器規模集 toohello 輸出中的看到[ARM： 取得 VMSS 私用 Ip](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips)。

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>我可以搭配加速的網路使用擴展集嗎？

是。 網路功能，加速 toouse enableAcceleratedNetworking tootrue 在設定中設定您的標尺集的 networkInterfaceConfigurations。 例如
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>如何設定規模集所使用的 hello DNS 伺服器？

toocreate VM 規模調整設定自訂的 DNS 設定，並將 dnsSettings JSON 封包 toohello 規模調整集合 networkInterfaceConfigurations > 一節。 範例：
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>我要如何設定公用 IP 位址 tooeach VM 規模集 tooassign？

toocreate VM 規模調整集合，會將指派的公用 IP 位址 tooeach VM，請確定 hello API 版的 hello Microsoft.Compute/virtualMAchineScaleSets 資源 2017年-03-30，並新增_publicipaddressconfiguration_ JSON 封包toohello 規模調整集合 ipConfigurations > 一節。 範例：

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>可以與多個應用程式閘道設定小數位數組 toowork 嗎？

是。 您可以加入 hello 資源識別碼的多個應用程式閘道後端位址集區 toohello _applicationGatewayBackendAddressPools_列入 hello _ipConfigurations_規模集的區段網路設定檔。

## <a name="scale"></a>調整

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>在何種情況下，我會建立具有兩部以下 VM 的虛擬機器擴展集？

其中一個原因 toocreate 的虛擬機器擴展集少於兩個 Vm 會 toouse hello 彈性屬性的虛擬機器規模設定。 比方說，您無法部署虛擬機器規模集與零 Vm toodefine 基礎結構而不必付出 VM 執行成本。 然後，當您準備好 toodeploy Vm，增加 hello 「 容量 」 的 hello 虛擬機器擴充集 toohello 生產執行個體計數。

建立具有兩部以下 VM 的虛擬機器擴展集的另一個原因，就是相較於使用具有離散 VM 的可用性設定組，您可能比較不擔心可用性。 虛擬機器擴展集可讓您使用無的計算的單位，可替代方式 toowork。 此種一致性是虛擬機器擴展集與可用性設定組的關鍵區別指標。 許多無狀態的工作負載都不會追蹤個別的單位。 Hello 工作負載會卸除，您可以縮小 tooone 計算單位，並再 toomany 向上延展 hello 工作負載增加時。

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>如何變更虛擬機器規模集中的 Vm hello 數目？

toochange hello 數目 Vm 規模集中的虛擬機器，請參閱[變更 hello 的虛擬機器規模集的執行個體計數](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/)。

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>如何定義觸達特定臨界值時的自訂警示？

您在處理指定之臨界值的警示時有一些彈性。 例如，您可以定義自訂的 webhook。 hello 下列 webhook 範例是從資源管理員範本：

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

在此範例中，警示會進入 tooPagerduty.com 達到臨界值時。



## <a name="patching-and-operations"></a>修補和作業

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>我如何在現有資源群組中建立擴展集？

建立小數位數的集合中現有的資源群組還不能從 hello Azure 入口網站，但部署小數位數設定的 Azure Resource Manager 範本時，您可以指定現有的資源群組。 您也可以在使用 Azure PowerShell 或 CLI 建立擴展集時，指定現有的資源群組。

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>我們可以將規模調整集合 tooanother 資源群組嗎？

是，您可以移動標尺組資源 tooa 新訂用帳戶或資源群組。

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>如何更新 tooI 我虛擬機器規模集 tooa 新映像嗎？ 如何管理修補？

請參閱您的虛擬機器規模集 tooa 新的映像，以及 toomanage 修補的 tooupdate[升級虛擬機器規模集](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set)。

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>可以使用 hello 重新安裝映像作業 tooreset VM 而不需要變更 hello 映像嗎？ (也就是，我想重設 VM toofactory 設定而不是 tooa 新映像。)

是，您可以使用 hello 重新安裝映像作業 tooreset VM 而不需要變更 hello 映像。 不過，如果虛擬機器規模集參考與平台映像`version = latest`，您的 VM 可以更新 tooa 更新的 OS 映像，當您呼叫`reimage`。

如需詳細資訊，請參閱[管理虛擬機器擴展集中的所有 VM](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set)。



## <a name="troubleshooting"></a>疑難排解

### <a name="how-do-i-turn-on-boot-diagnostics"></a>如何開啟開機診斷？

開機診斷 tooturn 首先，建立儲存體帳戶。 然後，將此 JSON 區塊放在您的虛擬機器規模集**virtualMachineProfile**，並更新 hello 虛擬機器規模集：

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

建立新的 VM 時，hello hello VM InstanceView 屬性會顯示 hello 螢幕擷取畫面和等等的 hello 詳細資料。 以下是範例：
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>虛擬機器屬性

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>如何取得每部 VM 的屬性資訊，而不進行多次呼叫？ 例如，如何會取得 hello 容錯網域 hello 的每個 100 Vm 在我的虛擬機器規模集？

為每個 VM，而不需要進行多次呼叫 tooget 屬性資訊，您可以呼叫`ListVMInstanceViews`藉由 REST API `GET` hello 下列資源 URI 上：

/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>可以傳入不同延伸引數 toodifferent Vm 虛擬機器規模集嗎？

否，您無法傳遞不同的延伸引數 toodifferent Vm 中虛擬機器規模集。 不過，擴充功能可做根據 hello 的 hello VM，執行在 hello 電腦名稱的唯一屬性。 延伸模組也可以查詢執行個體中繼資料上 http://169.254.169.254 tooget hello VM 的詳細資訊。

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>為何我的虛擬機器擴展集 VM 電腦名稱與 VM 識別碼之間會有落差？ 例如：0、1、3...

會虛擬機器規模集 VM 電腦名稱與 VM 識別碼之間的間距，因為虛擬機器規模集**overprovision**屬性設定為 toohello 預設值的**true**。 如果過度佈建太設定**true**，要求會建立多個 Vm。 然後會刪除額外的 VM。 在此情況下，您會取得部署增加的可靠性，但在 hello 費用連續命名連續網路位址轉譯 (NAT) 規則。 

您可以設定此屬性太**false**。 若為小型虛擬機器擴展集，這就不會大幅影響部署可靠性。

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Hello 刪除虛擬機器規模集中的 VM 和解除配置 hello VM 之間的差異為何？ 我何時應該選擇一種其他 hello？

hello 刪除虛擬機器規模集中的 VM 和解除配置 hello VM 之間的主要差異在於`deallocate`並不會刪除 hello 虛擬硬碟 (Vhd)。 執行 `stop deallocate` 會產生相關的儲存體成本。 您可能會使用其中一個或另一個用於 hello 下列原因之一 hello:

- 您想 toostop 支付計算費用，但是您想要的 hello Vm tookeep hello 磁碟狀態。
- 您無法擴充虛擬機器規模集比快速 toostart 一組的 Vm。
  - 相關的 toothis 案例中，您可能已建立您自己的自動調整引擎和想更快的端對端小數位數。
- 您的虛擬機器擴展集並未平均分散於各容錯網域或更新網域。 這可能是因為您選擇性地刪除 VM，或是因為 VM 在過度佈建之後遭到刪除。 執行`stop deallocate`後面`start`hello 虛擬機器擴展集平均分散 hello Vm 容錯網域或更新網域。

