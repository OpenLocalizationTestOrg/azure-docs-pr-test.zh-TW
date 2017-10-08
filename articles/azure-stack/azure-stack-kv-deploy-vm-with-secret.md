---
title: "最安全地儲存的密碼，Azure 堆疊上的 VM aaaDeploy |Microsoft 文件"
description: "了解如何 toodeploy VM 使用的密碼儲存在 Azure 堆疊金鑰保存庫"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: sngun
ms.openlocfilehash: 368addc1dfc5b7adadd2151fbd6d354f7892eea5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a>藉由擷取儲存在金鑰保存庫中的 hello 密碼來建立虛擬機器

當您在部署期間需要 toopass 安全的值，例如密碼時，可以將該值儲存為堆疊 Azure 金鑰保存庫中的密碼，並在 hello Azure 資源管理員範本中參考它。 您不需要 toomanually 輸入 hello 密碼每次部署 hello 資源，您也可以指定哪些使用者或服務主體可以存取 hello 密碼。 

在本文中，我們逐步引導您 hello 步驟需要 toodeploy Azure 堆疊中的 Windows 虛擬機器擷取 hello 密碼儲存在金鑰保存庫。 因此 hello 密碼永遠不會放在 hello 範本參數檔案中的純文字。 如果您透過 VPN 連線，您可以使用下列步驟從 hello Azure 堆疊開發套件，或從外部用戶端。

## <a name="prerequisites"></a>必要條件

* Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello Azure 金鑰保存庫服務。  
* 使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。  
* [安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)  
* [Hello Azure 堆疊使用者的 PowerShell 環境設定。](azure-stack-powershell-configure-user.md)

hello 下列步驟描述 hello 所需程序 toocreate 虛擬機器擷取儲存在金鑰保存庫中的 hello 密碼：

1. 建立 Key Vault 祕密。
2. 更新 hello azuredeploy.parameters.json 檔案。
3. 部署 hello 範本。

## <a name="create-a-key-vault-secret"></a>建立 Key Vault 祕密

hello 下列指令碼會建立金鑰保存庫，並會將密碼儲存在 hello 做為密碼金鑰保存庫。 使用 hello`-EnabledForDeployment`參數，當您要建立 hello 金鑰保存庫。 這個參數可確保您可以從 Azure 資源管理員範本參考該 hello 金鑰保存庫。

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

當您執行 hello 至上一個指令碼時，hello 輸出會包括 hello 密碼 URI。 請記下此 URI。 您有 tooreference 在 hello[部署 Windows 虛擬機器，以在金鑰保存庫範本中的密碼](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password)。 下載 hello [101-vm-安全性-密碼](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password)到開發電腦上的資料夾。 此資料夾包含 hello`azuredeploy.json`和`azuredeploy.parameters.json`hello 後續步驟中，您將需要的檔案。

修改 hello`azuredeploy.parameters.json`根據 tooyour 環境值的檔案。 特別感興趣的 hello 參數是 hello 保存庫名稱、 hello 保存庫的資源群組，以及 hello 密碼 URI （如 hello 至上一個指令碼所產生）。 下列檔 hello 是參數檔案的範例：

## <a name="update-hello-azuredeployparametersjson-file"></a>更新 hello azuredeploy.parameters.json 檔案

以 hello KeyVault URI、 secretName adminUsername hello 虛擬機器值，根據您的環境的 hello azuredeploy.parameters.json 檔案更新。 hello 下列 JSON 檔案顯示 hello 範本參數檔案的範例： 

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a>範本部署

現在使用下列 PowerShell 指令碼的 hello 部署 hello 範本：

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
Hello 範本順利部署時，它會產生下列輸出的 hello:

![部署輸出](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a>後續步驟
[使用 Key Vault 部署範例應用程式](azure-stack-kv-sample-app.md)

[使用 Key Vault 憑證部署 VM](azure-stack-kv-push-secret-into-vm.md)

