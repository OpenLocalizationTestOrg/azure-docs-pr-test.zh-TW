---
title: "aaaInstall 和在 Azure 中設定 Terraform tooprovision Vm 和其他基礎結構 |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定 Terraform toocreate Azure 資源"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>安裝和設定 Terraform tooprovision Vm 和其他基礎結構至 Azure 
本文描述 hello 必要步驟 tooinstall，並將 Terraform tooprovision 資源，例如虛擬機器設定到 Azure。 您將學習如何 toocreate 與使用 Azure 認證 tooenable Terraform tooprovision 雲端資源以安全的方式。

HashiCorp Terraform 提供簡單的方式 toodefine，並使用稱為 HashiCorp 設定語言 (HCL) 的自訂範本化語言部署雲端基礎結構。 這個自訂的語言是[輕鬆 toowrite 和輕鬆 toounderstand](terraform-create-complete-vm.md)。 此外，透過 hello`terraform plan`命令時，您在認可之前，您可以視覺化 hello 變更 tooyour 基礎結構。 請遵循這些步驟 toostart，搭配 Azure 使用 Terraform。

## <a name="install-terraform"></a>安裝 Terraform
tooinstall Terraform，[下載](https://www.terraform.io/downloads.html)hello 封裝適用於您的作業系統，到個別的安裝目錄。 hello 下載項目包含單一的可執行檔，您也應該為其定義通用的路徑。 如需 tooset 如何 hello 路徑在 Linux 和 Mac 上的指示，請移過[此網頁](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux)。 如需 tooset hello 在 Windows 上，路徑的方式的指示，請移過[此網頁](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)。 tooverify 您的安裝，請執行 hello`terraform`命令。 您應該會在輸出看到一份可用的 Terraform 選項清單。

接下來，您需要 tooallow Terraform 存取 tooyour Azure 訂用帳戶 tooperform 基礎結構佈建。

## <a name="set-up-terraform-access-tooazure"></a>設定 Terraform 存取 tooAzure
tooenable Terraform tooprovision 至 Azure 資源，您需要 toocreate Azure Active Directory (Azure AD) 中的兩個實體： Azure AD 應用程式與 Azure AD 服務主體。 然後，您可以在 Terraform 指令碼中使用這些實體的識別碼。 服務主體是全域 Azure AD 應用程式的本機執行個體。 服務主體可讓本機細微的存取控制 tooglobal 資源。

有數種方式 toocreate Azure AD 應用程式和 Azure AD 服務主體。 hello 最簡單且最快方式現今是 toouse Azure CLI 2.0 中，其中[您可以下載並安裝在 Windows、 Linux 或 Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。 您也可以使用 PowerShell 或 Azure CLI 1.0 toocreate hello 必要的安全性基礎結構。 接下來的 hello 指示告訴您如何使用這些方法的所有 tooconfigure Terraform azure。

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>使用 Azure CLI 2.0 (適用於 Windows、Linux 或 Mac 使用者) 
下載並安裝 hello 之後[Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)，登入 tooadminister 您 Azure 訂用帳戶發出下列命令的 hello:

```
az login
```

>[!NOTE]
>如果您使用 hello 中國、 Azure 德國或 Azure 政府雲端，您需要 toofirst hello Azure CLI toowork 設定與該雲端。 您可以執行下列 hello:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

如果您有多個 Azure 訂用帳戶，其詳細資料會由 hello`az login`命令。 設定 hello `SUBSCRIPTION_ID` hello 的環境變數 toohold hello 值傳回`id`hello 訂用帳戶的欄位想 toouse。 

設定此工作階段需 toouse hello 訂用帳戶。

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

查詢 hello 帳戶 tooget hello 訂用帳戶 ID 和租用戶的識別碼值。

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

接下來，為 Terraform 建立不同的認證。

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

會傳回您的 appId、密碼、sp_name 和租用戶。 請記下 hello appId 和密碼。

tooconfirm 您的認證 （服務主體），開啟新的殼層並執行下列命令的 hello。 傳回值 sp_name、 密碼及租用戶的替代 hello:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>使用 PowerShell (適用於 Windows 使用者) 
toouse Windows 電腦 toowrite 並執行您 Terraform 指令碼和組態工作 toouse PowerShell 設定您的電腦與 hello 權限的 PowerShell 工具。 

1. 中的 hello 步驟來安裝 PowerShell tools[安裝和設定 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)。 

2. 下載並執行 hello [azure setup.ps1 指令碼](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1)從 hello PowerShell 主控台。

3. toorun hello azure setup.ps1 指令碼中，下載並執行 hello`./azure-setup.ps1 setup`命令從 hello PowerShell 主控台。 然後登入 tooyour 具有系統管理權限的 Azure 訂用帳戶。

4. 出現提示時，提供應用程式名稱 (任意字串，必填)。 出現提示時，選擇性提供強式密碼。 如果您未提供密碼，則會使用 .NET 安全性程式庫為您產生強式密碼。

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>使用 Azure CLI 1.0 (適用於 Linux 或 Mac 使用者)
tooget 入門 Terraform Linux 機器上使用 Azure CLI 1.0 的 Mac 電腦上安裝 hello 適當庫。  

1. 中的 hello 步驟來安裝 Azure xPlat CLI 工具[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。 

2. 下載並安裝 JSON 處理器中的 hello 指示[下載 jq](https://stedolan.github.io/jq/download/)。

3. 下載並執行 hello [azure setup.sh 指令碼](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh)撞 hello 主控台從指令碼。

4. toorun hello azure setup.sh 指令碼中，下載並執行 hello `./azure-setup setup` hello 主控台命令。 然後登入 tooyour 具有系統管理權限的 Azure 訂用帳戶。
 
5. 出現提示時，提供應用程式名稱 (任意字串，必填)。 出現提示時，選擇性提供強式密碼。 如果您未提供密碼，則會使用 .NET 安全性程式庫為您產生強式密碼。

所有的 hello 前一個指令碼建立 Azure AD 應用程式和服務主體。 hello 服務主體取得 hello 訂用帳戶上的參與者或擁有者層級存取。 因為 hello 高層級的授與存取權，您應該一律保護 hello 這些指令碼所產生的安全性資訊。 記下那些指令碼所提供的四個安全性資訊：appId、密碼、subscription_id 和 tenant_id。

## <a name="set-environment-variables"></a>設定環境變數
您建立及設定 Azure AD 服務主體之後，您會需要 toolet Terraform 知道 hello 租用戶識別碼、 訂用帳戶 ID、 用戶端識別碼和用戶端秘密 toouse。 您可以如[使用 Terraform 建立基本基礎結構](terraform-create-complete-vm.md)所述，在 Terraform 指令碼中內嵌這些值來執行此作業。 或者，您可以設定下列環境變數的 hello （並因此避免不小心簽入，或共用您的認證）：

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

您可以使用這個範例的殼層指令碼 tooset 這些變數：

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

此外，如果您使用 Terraform 搭配 Azure 在中國或可能是 Azure 政府或德國 Azure 時，您需要 tooset hello 環境變數適當。

## <a name="next-steps"></a>後續步驟
您現在已安裝 Terraform 並設定 Azure 認證，可以開始將基礎結構部署到您的 Azure 訂用帳戶中。 接下來，了解如何太[建立基礎結構與 Terraform](terraform-create-complete-vm.md)。
