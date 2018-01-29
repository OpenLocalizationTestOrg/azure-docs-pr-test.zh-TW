---
title: "使用 CLI 連線至 Azure Stack | Microsoft 文件"
description: "了解如何使用跨平台命令列介面 (CLI) 在 Azure Stack 上管理及部署資源"
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2017
ms.author: mabrigg
ms.openlocfilehash: 3ca71abb1b84f619cfafbf4c25b0c0cb95430858
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2018
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a>安裝並設定 CLI 以與 Azure Stack 搭配使用

在本文中，我們會引導您完成從 Linux 和 Mac 用戶端平台使用 Azure 命令列介面 (CLI) 來管理 Azure Stack 開發套件資源的程序。 

## <a name="install-cli"></a>安裝 CLI

接下來，登入您的開發工作站並安裝 CLI。 Azure Stack 需要有 Azure CLI 2.0 版。 您可以使用[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) 一文中所述的步驟來安裝它。 若要確認安裝是否成功，請開啟終端機或命令提示字元視窗，並執行下列命令：

```azurecli
az --version
```

您應該會看到 Azure CLI 的號碼和您電腦上安裝的其他相依程式庫。

## <a name="trust-the-azure-stack-ca-root-certificate"></a>信任 Azure Stack CA 根憑證

從 Azure Stack 操作員取得 Azure Stack CA 根憑證，並信任該憑證。 若要信任 Azure Stack CA 根憑證，請將它附加到現有的 Python 憑證。 如果您是從在 Azure Stack 環境內建立的 Linux 機器執行 CLI，請執行下列 Bash 命令：

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

如果您是從 Azure Stack 環境的外部機器執行 CLI，則必須先[設定 Azure Stack 的 VPN 連線](azure-stack-connect-azure-stack.md)。 現在，請將您稍早匯出的 PEM 憑證複製到開發工作站，然後視開發工作站的作業系統而定，執行下列命令。

### <a name="linux"></a>Linux

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a>macOS

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a>Windows

```powershell
$pemFile = "<Fully qualified path to the PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from the cert file"
$md5Hash    = (Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash   = (Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash = (Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry  = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry   = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry  = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry     = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry    = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry  = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path $pemFile -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding the certificate content to Python Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing the azure stack CA root certificate"
```

## <a name="get-the-virtual-machine-aliases-endpoint"></a>取得虛擬機器別名端點

使用者在使用 CLI 建立虛擬機器之前，必須連絡 Azure Stack 操作員，並取得虛擬機器別名端點 URI。 例如，Azure 使用以下 URI：https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json。 雲端系統管理員應該使用 Azure Stack 市集中可用的映像，為 Azure Stack 設定類似的端點。 使用者必須將端點 URI 的 `endpoint-vm-image-alias-doc` 參數傳遞至 `az cloud register` 命令，如下一節中所示。 
   

## <a name="connect-to-azure-stack"></a>連線至 Azure Stack

使用下列步驟連線至 Azure Stack：

1. 執行 `az cloud register` 命令來註冊 Azure Stack 環境。
   
   a. 若要註冊「雲端系統管理」環境，請使用：

      ```azurecli
      az cloud register \ 
        -n AzureStackAdmin \ 
        --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
        --suffix-storage-endpoint "local.azurestack.external" \ 
        --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
        --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
        --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
      ```

   b. 若要註冊「使用者」環境，請使用：

      ```azurecli
      az cloud register \ 
        -n AzureStackUser \ 
        --endpoint-resource-manager "https://management.local.azurestack.external" \ 
        --suffix-storage-endpoint "local.azurestack.external" \ 
        --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
        --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
        --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
      ```

2. 使用下列命令來設定作用中環境。

   a. 針對「雲端系統管理」環境，請使用：

      ```azurecli
      az cloud set \
        -n AzureStackAdmin
      ```

   b. 針對「使用者」環境，請使用：

      ```azurecli
      az cloud set \
        -n AzureStackUser
      ```

3. 將您的環境組態更新成使用 Azure Stack 特定的 API 版本設定檔。 若要更新組態，請執行下列命令：

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. 使用 `az login` 命令來登入 Azure Stack 環境。 您可以以使用者身分或以[服務主體](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)形式登入 Azure Stack 環境。 

   * 以「使用者」身分登入：您可以直接在 `az login` 命令內指定使用者名稱和密碼，或使用瀏覽器進行驗證。 如果您的帳戶已啟用多重要素驗證，則必須採用後者方式。

      ```azurecli
      az login \
        -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
        --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
      ```

      > [!NOTE]
      > 如果您的使用者帳戶已啟用多重要素驗證，則可以使用 `az login command` 命令，而不需提供 `-u` 參數。 執行此命令可提供您一個 URL 以及必須用來進行驗證的代碼。
   
   * 以*服務主體*形式登入：在登入之前，請[透過 Azure 入口網站](azure-stack-create-service-principals.md)或 CLI 建立服務主體，並為它指派角色。 現在，請使用下列命令登入：

      ```azurecli
      az login \
        --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
        --service-principal \
        -u <Application Id of the Service Principal> \
        -p <Key generated for the Service Principal>
      ```

## <a name="test-the-connectivity"></a>測試連線

一切都已準備就緒，接下來我們要使用 CLI 在 Azure Stack 中建立資源。 例如，您可以建立應用程式的資源群組，並新增虛擬機器。 若要建立名為 "MyResourceGroup" 的資源群組，請使用下列命令：

```azurecli
az group create \
  -n MyResourceGroup -l local
```

如果資源群組成功建立，先前的命令會輸出新建立資源的下列內容：

![資源群組建立輸出](media/azure-stack-connect-cli/image1.png)

## <a name="known-issues"></a>已知問題
使用 Azure Stack 中的 CLI 時，有一些已知問題必須留意：

* CLI 互動模式 (例如 `az interactive` 命令) 在 Azure Stack 中尚未支援。
* 若要取得 Azure Stack 中的可用虛擬機器映像清單，請使用 `az vm images list --all` 命令，而非 `az vm image list` 命令。 指定 `--all` 選項可確保回應只傳回您 Azure Stack 環境中的可用映像。 
* Azure 中可用的虛擬機器映像別名可能不適用於 Azure Stack。 使用虛擬機器映像時，您必須使用整個 URN 參數 (Canonical:UbuntuServer:14.04.3-LTS:1.0.0)，而非映像別名。 此 URN 必須符合從 `az vm images list` 命令衍生的映像規格。
* 根據預設值，CLI 2.0 使用 “Standard_DS1_v2” 作為預設虛擬機器映像大小。 不過，此大小在 Azure Stack 中還無法使用，因此您必須在建立虛擬機器時明確地指定 `--size` 參數。 您可以使用 `az vm list-sizes --location <locationName>` 命令來取得 Azure Stack 中的可用虛擬機器大小清單。


## <a name="next-steps"></a>後續步驟

[使用 Azure CLI 部署範本](azure-stack-deploy-template-command-line.md)

[管理使用者權限](azure-stack-manage-permissions.md)
