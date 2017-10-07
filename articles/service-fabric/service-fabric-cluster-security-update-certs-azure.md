---
title: "Azure Service Fabric 叢集中的 aaaManage 憑證 |Microsoft 文件"
description: "描述如何 tooadd 新的憑證、 變換憑證，以及移除憑證 tooor 從 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>新增或移除 Azure 中 Service Fabric 叢集的憑證
建議您先熟悉 Service Fabric 如何使用 X.509 憑證，並熟悉 hello[叢集安全性案例](service-fabric-cluster-security.md)。 您必須瞭解什麼是叢集憑證及其用途，方可繼續進行後續作業。

服務網狀架構可讓您指定兩個叢集憑證中，主要和次要複本，當您設定叢集建立期間，加法 tooclient 憑證中的憑證安全性。 請參閱太[建立透過入口網站的 azure 叢集](service-fabric-cluster-creation-via-portal.md)或[建立 azure 的叢集透過 Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)它們設定在詳細資料建立時間。 如果您指定只有一個叢集憑證在建立時，然後作為 hello 主要憑證。 在叢集建立完成後，您可新增憑證做為次要憑證。

> [!NOTE]
> 安全的叢集，您永遠必須至少一個有效的 （未撤銷和未到期） 叢集 （主要或次要） 部署憑證 （如果沒有，hello 叢集會停止運作）。 90 天的所有有效憑證到達到期日之前 hello 系統會產生警告追蹤以及 hello 節點上的警告健全狀況事件。 目前並無 Service Fabric 針對此主題送出的電子郵件或其他任何通知。 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>新增次要叢集憑證使用 hello 入口網站

無法透過 hello Azure 入口網站中加入次要叢集憑證。 您有 toouse Azure powershell 的。 在本文件稍後所述 hello 程序。

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>交換 hello 叢集憑證使用 hello 入口網站

您已成功部署次要叢集憑證中，如果您想 tooswap hello 主要和次要之後，瀏覽 toohello 安全性刀鋒視窗中，然後選取 hello '交換主要與' 選項從 hello 內容功能表 tooswap hello 次要憑證與hello 主要憑證。

![交換憑證][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>移除叢集憑證使用 hello 入口網站

安全的叢集，您永遠必須至少一個有效 （未撤銷和未到期） 的憑證 （主要或次要） 部署否則 hello 叢集會停止運作。

tooremove 用於叢集安全性、 瀏覽 toohello 安全性刀鋒視窗，然後選取 hello 'Delete' 選項從 hello 快顯功能表 hello 次要憑證上的次要憑證。

如果您的意圖是標示為主要，則需要 tooswap tooremove hello 憑證與 hello 次要在第一次，並 hello 升級完成之後，再刪除次要 hello。

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>使用 Resource Manager Powershell 來新增次要憑證

這些步驟假設您熟悉資源管理員的運作方式，和已部署至少一個 Service Fabric 叢集，使用資源管理員範本，且有您用方便的 hello 叢集 tooset hello 範本。 此外亦假設您可輕鬆自如地使用 JSON。

> [!NOTE]
> 如果您要尋找範例範本和參數，您可以使用 toofollow 沿著或做為起點，然後從下載這[git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)。 
> 
> 

### <a name="edit-your-resource-manager-template"></a>編輯您的 Resource Manager 範本

範例 5-VM-1-NodeTypes-Secure_Step2.JSON 沿著下列簡易，包含我們將會進行所有的 hello 編輯作業。 hello 範例位於[git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)。

**請確定 toofollow hello 的所有步驟**

**步驟 1:** hello Resource Manager 範本使用您要叢集化的 toodeploy 開啟。 （如果您已從上述儲存機制的 hello 下載 hello 範例，然後使用 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy 安全的叢集，然後開啟該範本。）

**步驟 2:**新增**兩個新的參數**"secCertificateThumbprint"和"secCertificateUrlValue 」 類型的"string"toohello 參數區段，您的範本。 您可以複製下列程式碼片段的 hello，並將它加入 toohello 範本。 根據您的範本 hello 來源，您可能已經已定義，如果是這樣移動 toohello 下一個步驟。 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**步驟 3:**變更 toohello **Microsoft.ServiceFabric/clusters**資源-您在範本中找出 hello"Microsoft.ServiceFabric/clusters 」 資源定義。 在定義的屬性，您會發現 「 憑證 」 JSON 標記，這看起來應該類似下列 JSON 片段 hello:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

加入新標籤「thumbprintSecondary」，並為它提供值「[parameters('secCertificateThumbprint')]」。  

因此現在 hello 資源定義應該看起來像下列 hello （根據您的 hello 範本的來源，可能無法完全一樣 hello 以下程式碼片段）。 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

如果您想太**變換 hello cert**，然後將 hello 新憑證指定為主要及移動 hello 目前主要複本為次要資料庫。 這會導致您的目前主要憑證 toohello 新憑證在一個部署步驟中的 hello 換用。

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**步驟 4:**進行過變更**所有**hello **Microsoft.Compute/virtualMachineScaleSets**資源定義的尋找 hello Microsoft.Compute/virtualMachineScaleSets 資源定義。 捲動 toohello 「 發行者 」: 「 Microsoft.Azure.ServiceFabric"，"virtualMachineProfile"下的。

在 hello 服務網狀架構 「 發行者 」 設定，您應該看到類似下面的。

![Json_Pub_Setting1][Json_Pub_Setting1]

加入新的憑證項目 tooit hello

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

hello 屬性現在看起來應該像這樣

![Json_Pub_Setting2][Json_Pub_Setting2]

如果您想太**變換 hello cert**，然後將 hello 新憑證指定為主要及移動 hello 目前主要複本為次要資料庫。 這會導致您的目前憑證 toohello 新憑證在一個部署步驟中的 hello 換用。 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
hello 屬性現在看起來應該像這樣

![Json_Pub_Setting3][Json_Pub_Setting3]


**步驟 5:**變更太**所有**hello **Microsoft.Compute/virtualMachineScaleSets**資源定義的尋找 hello Microsoft.Compute/virtualMachineScaleSets 資源定義。 捲動 toohello"vaultCertificates":，"OSProfile"下。 您應該會看到類似下面的畫面。


![Json_Pub_Setting4][Json_Pub_Setting4]

新增 hello secCertificateUrlValue tooit。 使用下列程式碼片段的 hello:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
立即產生 Json hello 看起來應該像這樣。
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> 請確定您有重複的步驟 4 和 5 所有 hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets 資源定義中您的範本。 如果您錯過其中一個方法，該 VMSS 上不會安裝 hello 憑證，而且您必須在叢集中，包括 hello 叢集停機 （如果您不得到該 hello 叢集可以使用安全性的任何有效憑證無法預期結果。 因此，在進一步進行之前，請先仔細檢查。
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>編輯您範本檔案 tooreflect hello 新參數加入之上
如果您使用從 hello hello 範例[git 儲存機制](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)toofollow 以及，您可以在 hello 範例 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 啟動 toomake 變更 

編輯您的資源管理員範本參數檔案，加入 hello 兩個新的參數 secCertificateThumbprint 和 secCertificateUrlValue。 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>部署 hello 範本 tooAzure

- 您會立即準備 toodeploy 範本 tooAzure。 開啟 Azure PS 版本 1+ 命令提示字元。
- 登入 tooyour Azure 帳戶，並選取 hello 特定的 azure 訂用帳戶。 這是擁有超過一個 azure 訂用帳戶的存取 toomore 同仁的一個重要步驟。

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

測試 hello 範本先前 toodeploying 它。 使用 hello 叢集目前已部署至同一個資源群組。

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

部署 hello 範本 tooyour 資源群組。 使用 hello 叢集目前已部署至同一個資源群組。 執行 hello 新增 AzureRmResourceGroupDeployment 命令。 您不需要 toospecify hello 模式中，由於 hello 預設值為**累加**。

> [!NOTE]
> 如果您將設定模式 tooComplete，您可以不小心刪除不在範本中的資源。 因此請勿在此案例中使用該模式。
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

以下是已填入出 hello 的範例相同的 powershell。

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Tooyour 叢集使用 hello 部署完成之後，連接 hello 新的憑證，以及執行某些查詢。 如果您無法 toodo。 然後您可以刪除 hello 舊的憑證。 

如果您使用自我簽署的憑證，別忘了 tooimport 為本機的 TrustedPeople 憑證存放區。

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
快速參考如下 hello 命令 tooconnect tooa 安全叢集 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
快速參考如下 hello 命令 tooget 叢集健全狀況

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>部署應用程式憑證 toohello 叢集。

您可以使用相同的步驟中所述的步驟 5 上方 toohave hello 憑證從 keyvault toohello 節點部署的 hello。 您只需定義和使用不同的參數即可。


## <a name="adding-or-removing-client-certificates"></a>新增或移除用戶端憑證

在加法 toohello 叢集憑證，您可以加入用戶端憑證 tooperform service fabric 叢集上的管理作業。

您可以新增兩種用戶端憑證 - 系統管理員或唯讀。 這些然後可使用的 toocontrol 存取 toohello 管理作業和 hello 叢集上的查詢作業。 根據預設，hello 叢集憑證會加入 toohello 允許系統管理員的憑證清單。

您可以指定任何數目的用戶端憑證。 每個新增/刪除導致組態更新 toohello service fabric 叢集


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>透過入口網站新增用戶端憑證 - 系統管理員或唯讀

1. 瀏覽 toohello 安全性刀鋒視窗中，並選取 hello '+ 驗證' hello 安全性刀鋒視窗頂端的按鈕。
2. 在 hello 新增驗證刀鋒視窗中，選擇 hello '驗證類型'-'唯讀用戶端' 或 '管理用戶端'
3. 現在選擇 hello 授權方法。 是否它應使用 hello 主體名稱或 hello 指紋查閱此憑證，這表示 tooService 網狀架構。 一般情況下，它不是很好的安全性作法 toouse hello 授權方法的主體名稱。 

![新增用戶端憑證][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>刪除的用戶端憑證-系統管理員或唯讀使用 hello 入口網站

tooremove 叢集安全性、 瀏覽 toohello 安全性刀鋒視窗，然後選取 hello 'Delete' 選項從 hello 內容功能表上 hello 特定憑證的正在使用的次要憑證。



## <a name="next-steps"></a>後續步驟
如需有關叢集管理的詳細資訊，請參閱下列文件︰

* [Service Fabric 叢集升級程序與您的期望](service-fabric-cluster-upgrade.md)
* [設定用戶端的角色型存取](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


