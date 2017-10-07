---
title: "虛擬機器上，使用安全地儲存憑證 Azure 堆疊 aaaDeploy |Microsoft 文件"
description: "了解如何 toodeploy 虛擬機器和發送至其本身的憑證，使用金鑰保存庫中 Azure 堆疊"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: b5fa0a502ba582e10ff59b8af0568bf134d3d189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a>建立虛擬機器，並加入從金鑰保存庫擷取的憑證

這篇文章可協助您 toocreate Azure 堆疊和發送至其本身的憑證中的虛擬機器。 

## <a name="prerequisites"></a>必要條件

* Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello Azure 金鑰保存庫服務。  
* 使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。  
* [安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)  
* [設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)

Azure 堆疊中的金鑰保存庫是使用的 toostore 憑證。 憑證在許多不同情況下都很有幫助。 例如，假設您在 Azure Stack 中有一個虛擬機器正在執行需要憑證的應用程式。 此憑證可用來加密驗證 tooActive 目錄，或 SSL 的網站上。 具有 hello 憑證金鑰保存庫可以協助確定它是安全。

在本文中，我們逐步引導您 hello 步驟需要 toopush Azure 堆疊中的 Windows 虛擬機器的憑證。 如果您透過 VPN 連線，您可以使用下列步驟從 hello Azure 堆疊開發套件，或是從 windows 的外部用戶端。

hello 下列步驟說明 hello 所需程序 toopush hello 虛擬機器上的憑證：

1. 建立 Key Vault 祕密。
2. 更新 hello azuredeploy.parameters.json 檔案。
3. 部署 hello 範本

## <a name="create-a-key-vault-secret"></a>建立 Key Vault 祕密

hello 下列指令碼會建立 hello.pfx 格式的憑證、 建立金鑰保存庫，並儲存 hello 憑證 hello 做為密碼金鑰保存庫中。 您必須使用 hello`-EnabledForDeployment`參數，當您要建立 hello 金鑰保存庫。 這個參數可確保您可以從 Azure 資源管理員範本參考該 hello 金鑰保存庫。

```powershell

# Create a certificate in hello .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used tooexport hello certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in hello previous step>" `
  -FilePath "<Fully qualified path where hello exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload hello certificate into hello key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where hello exported certificate can be stored>"
$certPassword = "<Password used tooexport hello certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

當您執行 hello 至上一個指令碼時，hello 輸出會包括 hello 密碼 URI。 請記下此 URI。 您有 tooreference 在 hello[推播憑證 tooWindows Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows)。 下載 hello [vm 推播憑證-windows 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows)到開發電腦上的資料夾。 此資料夾包含 hello`azuredeploy.json`和`azuredeploy.parameters.json`hello 後續步驟中，您將需要的檔案。

修改 hello`azuredeploy.parameters.json`根據 tooyour 環境值的檔案。 特別感興趣的 hello 參數是 hello 保存庫名稱、 hello 保存庫的資源群組，以及 hello 密碼 URI （如 hello 至上一個指令碼所產生）。 下列檔 hello 是參數檔案的範例：

## <a name="update-hello-azuredeployparametersjson-file"></a>更新 hello azuredeploy.parameters.json 檔案

更新 hello azuredeploy.parameters.json 檔案 hello vaultName、 與密碼的 URI、 VmName，根據您的環境的其他值。 hello 下列 JSON 檔案顯示 hello 範本參數檔案的範例： 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-hello-template"></a>部署 hello 範本

現在使用下列 PowerShell 指令碼的 hello 部署 hello 範本：

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

Hello 範本順利部署時，它會產生下列輸出的 hello:

![部署輸出](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

在部署此虛擬機器時，Azure 堆疊推入 hello hello 虛擬機器上的憑證。 在 Windows hello 憑證會新增 toohello LocalMachine 存放區提供該 hello 使用者的憑證位置，與 hello 憑證。 在 Linux 中 hello 憑證會放在 hello 檔名的 hello /var/lib/waagent 目錄下&lt;UppercaseThumbprint&gt;.crt hello X509 憑證檔案和&lt;UppercaseThumbprint&gt;.prv hello私用的索引鍵。

## <a name="retire-certificates"></a>淘汰憑證

在前一節的 hello，我們也示範了您如何 toopush 虛擬機器到新的憑證。 舊的憑證仍在 hello 虛擬機器，且無法移除。 不過，您可以使用停用舊版 hello 密碼 hello hello `Set-AzureKeyVaultSecretAttribute` cmdlet。 hello 以下是這個 cmdlet 的範例使用方式。 請確定 tooreplace hello 保存庫名稱、 密碼的名稱和版本值根據 tooyour 環境：

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a>後續步驟

* [使用金鑰保存庫密碼部署 VM](azure-stack-kv-deploy-vm-with-secret.md)
* [允許應用程式 tooaccess 金鑰保存庫](azure-stack-kv-sample-app.md)


