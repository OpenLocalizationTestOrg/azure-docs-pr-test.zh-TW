---
title: "Azure VM 的 WinRM 存取 aaaSet |Microsoft 文件"
description: "設定用於 WinRM 存取與 hello Resource Manager 部署模型中建立 Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>在 Azure Resource Manager 中設定虛擬機器的 WinRM 存取
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>Azure Service Management 與 Azure Resource Manager 中的 WinRM

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* 如需 hello Azure 資源管理員的概觀，請參閱本[發行項](../../azure-resource-manager/resource-group-overview.md)
* 如需 Azure Service Management 與 Azure Resource Manager 之間的差異性，請參閱 [本文章](../../resource-manager-deployment-model.md)

hello 中設定 WinRM 組態 hello 兩個堆疊之間的主要差異是 hello 憑證 hello VM 上安裝的方式。 Hello Azure Resource Manager 堆疊中 hello 憑證會模型化為 hello 金鑰保存庫資源提供者所管理的資源。 因此，hello 使用者需要 tooprovide 自己的憑證，並將它上傳 tooa 金鑰保存庫之前使用的 VM 中。

以下是您需要將 vm 與 WinRM 連線 tootake tooset hello 步驟

1. 建立金鑰保存庫
2. 建立自我簽署憑證
3. 上傳您的自我簽署的憑證 tooKey 保存庫
4. 取得您的自我簽署憑證 hello 金鑰保存庫中的 hello URL
5. 在建立 VM 時參考您的自我簽署憑證的 URL

## <a name="step-1-create-a-key-vault"></a>步驟 1︰建立金鑰保存庫
您可以使用下列命令 toocreate hello 金鑰保存庫的 hello

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>步驟 2：建立自我簽署憑證
您可以使用下列 PowerShell 指令碼建立自我簽署憑證

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>步驟 3： 上傳您的自我簽署的憑證 toohello 金鑰保存庫
步驟 1 中上傳 hello 憑證 toohello 金鑰保存庫建立之前，它會需要 tooconverted 成格式 hello Microsoft.Compute 資源提供者就可以了解。 下列 PowerShell 指令碼的 hello 可讓您執行此動作

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>步驟 4： 取得您的自我簽署憑證 hello 金鑰保存庫中的 hello URL
hello Microsoft.Compute 資源提供者佈建 hello VM 時，需要 hello 金鑰保存庫內的 URL toohello 密碼。 這可讓 hello Microsoft.Compute 資源提供者 toodownload hello 密碼，並在 hello VM 上建立 hello 對等憑證。

> [!NOTE]
> hello 密碼 hello URL 必須 tooinclude hello 版本。 範例 URL 如下所示：https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>範本
您可以取得 hello 連結 toohello URL 中使用程式碼底下的 hello hello 範本

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
您可以取得此 URL 使用下列 PowerShell 命令的 hello

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>步驟 5：在建立 VM 時參考您的自我簽署憑證的 URL
#### <a name="azure-resource-manager-templates"></a>Azure Resource Manager 範本
在建立時透過範本的 VM，hello 憑證取得參考 hello 機密資料區段和 hello winRM 區段，如下所示：

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

Hello 上述的範例範本可以在這裡找到在[201 vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

此範本的原始程式碼位於 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>步驟 6： 連接 toohello VM
您可以連接 toohello VM 之前，您必須先確定您的電腦已設定 WinRM 遠端管理 toomake。 系統管理員身分啟動 PowerShell 並執行以下命令 toomake 確定您設定好 hello。

    Enable-PSRemoting -Force

> [!NOTE]
> 您可能需要 toomake 確定 hello WinRM 服務正在執行，如果上述 hello 無法運作。 您可以使用 `Get-Service WinRM`
> 
> 

一旦 hello 安裝完成後，您可以連接 toohello VM 使用下列命令 hello

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
