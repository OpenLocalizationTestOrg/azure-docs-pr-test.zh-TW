---
title: "以 hello Azure CLI 1.0 Linux VM 上的 aaaEncrypt 磁碟 |Microsoft 文件"
description: "如何使用 Linux VM 上的 tooencrypt 磁碟 hello Azure CLI 1.0 和 hello Resource Manager 部署模型"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>加密使用 Azure CLI 1.0 hello 的 Linux VM 上的磁碟
如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的待用虛擬磁碟加密。 磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。 您可控制這些密碼編譯金鑰，並可稽核其使用情況。 這篇文章說明如何使用 Linux VM 上的虛擬磁碟 tooencrypt hello Azure CLI 1.0 和 hello Resource Manager 部署模型。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="quick-commands"></a>快速命令
如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello 基底的 hello 命令 tooencrypt VM 上的虛擬磁碟。 詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#overview-of-disk-encryption)。

您需要 hello[最新的 Azure CLI 1.0](../../xplat-cli-install.md)安裝並登入，如下所示使用 hello Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 `myResourceGroup`、`myKeyVault` 和 `myVM`。

首先，啟用您的 Azure 訂用帳戶內的 hello Azure 金鑰保存庫提供者，並建立資源群組。 hello 下列範例會建立資源群組名稱`myResourceGroup`在 hello`WestUS`位置：

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

建立 Azure 金鑰保存庫。 hello 下列範例會建立名為金鑰保存庫`myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

在您的金鑰保存庫中建立密碼編譯金鑰，並針對磁碟加密加以啟用。 hello 下列範例會建立名為`myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

建立使用 Azure Active Directory 處理 hello 驗證與金鑰保存庫中的密碼編譯金鑰交換的端點。 hello`--home-page`和`--identifier-uris`不需要 toobe 實際路由的位址。 Hello 最高等級的安全性，您應該使用的用戶端密碼，而不是密碼。 hello Azure CLI 目前無法產生的用戶端密碼。 只能在 hello Azure 入口網站中產生的用戶端密碼。 hello 下列範例會建立名為 Azure Active Directory 端點`myAADApp`和使用的密碼`myPassword`。 指定您自己的密碼，如下所示︰

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

請注意 hello `applicationId` hello hello 前面命令的輸出所示。 此應用程式中使用了識別碼 hello 下列步驟：

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

加入現有的 VM 資料磁碟 tooan。 hello 下列範例會將名為 VM 資料磁碟 tooa `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

檢閱您所建立的金鑰保存庫和 hello 金鑰的 hello 詳細資料。 您需要在金鑰保存庫識別碼、 URI 和金鑰 hello hello 最後一個步驟中的 URL。 hello 下列範例會檢閱 hello 詳細資料的金鑰保存庫名為`myKeyVault`和名為機碼`myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

如下所示，始終輸入您自己的參數名稱，將您的磁碟加密︰

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

hello Azure CLI hello 加密程序期間不會提供詳細的錯誤。 如需其他疑難排解資訊，請檢閱 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`。 Hello 前面命令有許多變數可能不會得到多指示 as toowhy hello 程序就會失敗，完整的命令範例應如下：

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

最後，檢閱 hello 加密狀態再次 tooconfirm 有現在已加密您的虛擬磁碟。 hello 下列範例會檢查名為的 VM hello 狀態`myVM`在 hello`myResourceGroup`資源群組：

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>磁碟加密概觀
Linux VM 上的待用虛擬磁碟會使用 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt) 進行加密。 將 Azure 中的虛擬磁碟加密完全免費。 密碼編譯金鑰會儲存在 Azure 金鑰保存庫使用軟體保護，或者您可以匯入或產生您的金鑰，在硬體安全性模組 (Hsm) 認證 tooFIPS 140-2 層級 2 標準。 您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。 這些密碼編譯金鑰會使用的 tooencrypt，並解密附加的 tooyour VM 虛擬磁碟。 Azure Active Directory 端點提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。

加密 VM hello 程序如下所示：

1. 在 Azure 金鑰保存庫中建立密碼編譯金鑰。
2. 設定 hello 密碼編譯金鑰 toobe 可用來加密磁碟。
3. hello Azure 金鑰保存庫，從 tooread hello 密碼編譯金鑰會建立使用 Azure Active Directory 與 hello 適當的權限的端點。
4. 您的虛擬磁碟，指定 hello Azure Active Directory 端點，並使用適當密碼編譯 toobe 發出 hello 命令 tooencrypt。
5. hello Azure Active Directory 端點要求 Azure 金鑰保存庫中的 hello 必要的密碼編譯金鑰。
6. hello 虛擬磁碟會使用提供的 hello 密碼編譯金鑰來加密。

## <a name="supporting-services-and-encryption-process"></a>支援服務和加密程序
磁碟加密依賴 hello 下列額外的元件：

* **Azure 金鑰保存庫**-使用 toosafeguard 密碼編譯金鑰和 hello 磁碟加密/解密程序所使用的密碼。
  * 如果有的話，您可以使用現有的 Azure 金鑰保存庫。 您沒有 toodedicate 金鑰保存庫 tooencrypting 磁碟。
  * 系統管理界限使用 tooseparate 和索引鍵的可見性，您可以建立專用的金鑰保存庫。
* **Azure Active Directory** -控點 hello 必要的密碼編譯金鑰的安全交換和驗證要求的動作。
  * 您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。
  * 較高的 hello 金鑰保存庫的端點和虛擬機器服務 toorequest hello 應用程式，並取得發出 hello 適當的密碼編譯金鑰。 您並未開發與 Azure Active Directory 整合的實際應用程式。

## <a name="requirements-and-limitations"></a>需求和限制
磁碟加密支援的案例和需求：

* 下列 Linux 伺服器 Sku-Ubuntu、 CentOS、 SUSE 和 SUSE Linux Enterprise Server (SLES) 和 Red Hat Enterprise Linux hello。
* 所有資源 （例如金鑰保存庫、 儲存體帳戶和 VM） 都必須在 hello 相同的 Azure 地區和訂用帳戶。
* 標準 A、D、DS、G 和 GS 系列 VM。

磁碟加密目前不支援在下列案例的 hello:

* 基本層 VM。
* 使用 hello 傳統部署模型所建立的 Vm。
* 在 Linux VM 上停用作業系統磁碟加密。
* 正在更新 hello 已加密的 Linux VM 上的密碼編譯金鑰。

## <a name="create-hello-azure-key-vault-and-keys"></a>建立 hello Azure 金鑰保存庫和金鑰
本指南的 toocomplete hello 其餘部分，您需要 hello[最新的 Azure CLI 1.0](../../xplat-cli-install.md)安裝並登入，如下所示使用 hello Resource Manager 模式：

```azurecli
azure config mode arm
```

整個 hello 命令範例，所有範例參數都取代您自己的名稱、 位置和索引鍵的值。 hello 下列範例會使用的慣例`myResourceGroup`， `myKeyVault`，`myAADApp`等等。

hello 第一個步驟是 toocreate Azure 金鑰保存庫 toostore 密碼編譯金鑰。 Azure 金鑰保存庫可以儲存金鑰，密碼，或密碼，可讓您 toosecurely 它們實作中，您的應用程式和服務。 虛擬磁碟加密，您可以使用金鑰保存庫 toostore 使用的 tooencrypt 的密碼編譯金鑰或解密您的虛擬磁碟。

啟用您 Azure 訂用帳戶中的 hello Azure 金鑰保存庫提供者，然後建立資源群組。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUS`位置：

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

hello Azure 金鑰保存庫包含 hello 密碼編譯金鑰與相關聯的計算資源，例如儲存體和 hello VM 本身必須位在 hello 相同的區域。 hello 下列範例會建立名為 Azure 金鑰保存庫`myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。 使用 HSM 時需要進階金鑰保存庫。 沒有額外的成本 toocreating 高階金鑰保存庫，而不是標準儲存軟體保護金鑰的金鑰保存庫。 高階金鑰保存庫、 hello 前面步驟中的加入的 toocreate `--sku Premium` toohello 命令。 hello 下列範例會使用受軟體保護的金鑰因為我們建立標準的金鑰保存庫。

這兩種保護模型中，hello Azure 平台必須 toobe hello VM 開機 toodecrypt hello 虛擬磁碟時，授與存取 toorequest hello 密碼編譯金鑰。 在您的金鑰保存庫中建立加密金鑰，然後加以啟用以便用於虛擬磁碟加密。 hello 下列範例會建立名為`myKey`然後再啟用它，磁碟加密：

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>建立 hello Azure Active Directory 應用程式
當虛擬磁碟加密或解密時，您可以使用端點 toohandle hello 驗證，以及交換的金鑰保存庫中的密碼編譯金鑰。 此端點，Azure Active Directory 應用程式，可讓 hello Azure 平台 toorequest hello 適當的密碼編譯金鑰代表 hello VM。 雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。

您不會建立完整的 Azure Active Directory 應用程式，如 hello`--home-page`和`--identifier-uris`hello 下列範例中的參數不需要 toobe 實際路由的位址。 hello 下列範例也會指定密碼為基礎的密碼，而不是來自 hello Azure 入口網站中產生的金鑰。 為此階段中，無法從 hello Azure CLI 完成產生的金鑰。

建立 Azure Active Directory 應用程式。 hello 下列範例會建立名為應用程式`myAADApp`和使用的密碼`myPassword`。 指定您自己的密碼，如下所示︰

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

請記下 hello `applicationId` hello 前面命令從 hello 輸出中傳回。 在某些其他步驟的 hello 使用這個應用程式 ID。 接下來，建立服務主體名稱 (SPN)，以便 hello 應用程式都可存取您的環境。 toosuccessfully 加密或解密虛擬磁碟，儲存在金鑰保存庫中的 hello 密碼編譯金鑰的權限必須是集 toopermit hello Azure Active Directory 應用程式 tooread hello 索引鍵。

建立 hello SPN，並設定 hello 適當的權限，如下所示：

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>新增虛擬磁碟並檢閱加密狀態
tooactually 加密某些虛擬磁碟，可讓您加入現有的 VM 磁碟 tooan。 加入現有的 VM，如下所示的 5 Gb 資料磁碟 tooan:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

目前未加密 hello 虛擬磁碟。 請檢閱您 VM 的 hello 目前加密狀態，如下所示：

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>將虛擬磁碟加密
toonow 加密 hello 虛擬磁碟，同時讓所有 hello 舊版元件：

1. 指定 hello Azure Active Directory 應用程式和密碼。
2. 指定 hello 金鑰保存庫 toostore hello 中繼資料的加密磁碟。
3. 指定 hello hello 實際加密和解密的密碼編譯金鑰 toouse。
4. 指定是否要 tooencrypt hello OS 磁碟、 hello 資料磁碟，或全部。

可讓檢視您的 Azure 金鑰保存庫和 hello 金鑰您建立的您需要 hello 金鑰保存庫識別碼 URI，然後在最後一個步驟中 hello 金鑰 URL hello 詳細資料：

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

加密您的虛擬磁碟使用 hello hello 輸出`azure keyvault show`和`azure keyvault key show`命令，如下所示：

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello 前述的命令有許多變數，如 hello 下列範例是 hello 完整命令參考：

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

hello Azure CLI hello 加密程序期間不會提供詳細的錯誤。 如需其他疑難排解資訊，請檢閱`/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`hello 要加密的 VM 上。

最後，可讓檢閱 hello 加密狀態再次 tooconfirm 有現在已加密您的虛擬磁碟：

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>新增其他資料磁碟
一旦您已加密資料磁碟，您可以稍後新增其他虛擬磁碟 tooyour VM，並也加密它們。 當您執行 hello`azure vm enable-disk-encryption`命令、 遞增 hello 順序版本使用 hello`--sequence-version`參數。 此順序的 version 參數可讓您 tooperform 上的重複的作業 hello 相同的 VM。

例如，可讓新增第二個虛擬磁碟 tooyour VM，如下所示：

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

重新執行 hello 命令 tooencrypt hello 的虛擬磁碟，這次加入 hello`--sequence-version`參數，而遞增 hello 值我們第一個執行，如下所示：

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>後續步驟
* 如需有關管理 Azure 金鑰保存庫 (包括刪除密碼編譯金鑰和保存庫) 的詳細資訊，請參閱[使用 CLI 管理金鑰保存庫](../../key-vault/key-vault-manage-with-cli2.md)。
* 如需有關磁碟加密，例如準備的加密自訂 VM tooupload tooAzure，請參閱[Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。
