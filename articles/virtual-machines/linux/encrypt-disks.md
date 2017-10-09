---
title: "在 Azure 中的 Linux VM 上 aaaEncrypt 磁碟 |Microsoft 文件"
description: "Tooencrypt 增強式的安全性使用 Linux VM 上的虛擬磁碟 hello Azure CLI 2.0 的方式"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>如何 tooencrypt Linux VM 上的虛擬磁碟
如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的虛擬磁碟加密。 磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。 您可控制這些密碼編譯金鑰，並可稽核其使用情況。 這篇文章說明如何使用 Linux VM 上的虛擬磁碟 tooencrypt hello Azure CLI 2.0。 您也可以執行下列步驟以 hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="quick-commands"></a>快速命令
如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello 基底的 hello 命令 tooencrypt VM 上的虛擬磁碟。 詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#overview-of-disk-encryption)。

您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。 在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包括 *myResourceGroup*、*myKey* 及 *myVM*。

首先，啟用 hello Azure 金鑰保存庫提供者與您 Azure 訂用帳戶內[az 提供者登錄](/cli/azure/provider#register)，並建立與資源群組[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立資源群組名稱*myResourceGroup*在 hello *eastus*位置：

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

建立與 Azure 金鑰保存庫[az keyvault 建立](/cli/azure/keyvault#create)並啟用 hello 金鑰保存庫，磁碟加密搭配使用。 針對 *keyvault_name* 指定一個唯一的 Key Vault 名稱，如下所示︰

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

使用 [az keyvault key create](/cli/azure/keyvault/key#create) 在 Key Vault 中建立密碼編譯金鑰。 hello 下列範例會建立名為*myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

使用 Azure Active Directory 搭配 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體。 hello 服務主體的控制代碼 hello 驗證與金鑰保存庫中的密碼編譯金鑰交換。 下列範例中的 hello 讀取 hello 服務主體的 hello 值識別碼和密碼，以在更新版本的命令中使用：

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

當您建立 hello 服務主體時，只是輸出 hello 密碼。 如有需要，檢視並錄製 hello 密碼 (`echo $sp_password`)。 您可以使用 [az ad sp list](/cli/azure/ad/sp#list) 列出服務主體，以及使用 [az ad sp show](/cli/azure/ad/sp#show) 檢視特定服務主體的其他相關資訊。

使用 [az keyvault set-policy](/cli/azure/keyvault#set-policy) 設定 Key Vault 的權限。 在下列範例的 hello，hello 服務主體的識別碼會提供從 hello 上述命令：

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

使用 [az vm create](/cli/azure/vm#create) 建立 VM 並連結 5GB 資料磁碟。 只有某些 Marketplace 映像支援磁碟加密。 hello 下列範例會建立名為的 VM`myVM`使用**CentOS 7.2n**映像：

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM 使用 hello `publicIpAddress` hello 輸出的 hello 前面命令中所示。 建立分割區和檔案系統，然後掛接 hello 資料磁碟。 如需詳細資訊，請參閱[連接 tooa Linux VM toomount hello 新磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)。 關閉 SSH 工作階段。

使用 [az vm encryption enable](/cli/azure/vm/encryption#enable) 將您的 VM 加密。 hello 下列範例會使用 hello`$sp_id`和`$sp_password`變數從上述 hello`ad sp create-for-rbac`命令：

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

花一些時間 hello 磁碟加密程序 toocomplete。 監視 hello 程序與 hello 狀態[az vm 加密顯示](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello 狀態顯示**EncryptionInProgress**。 等候 hello OS 磁碟報告 hello 狀態直到**VMRestartPending**，然後重新啟動您的 VM 與[az vm 重新啟動](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

hello 磁碟加密程序完成 hello 開機程序期間，因此請稍候幾分鐘再檢查一次使用加密 hello 狀態**az vm 加密顯示**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello OS 磁碟和資料磁碟，現在應報告 hello 狀態**加密**。

## <a name="overview-of-disk-encryption"></a>磁碟加密概觀
Linux VM 上的待用虛擬磁碟會使用 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt) 進行加密。 將 Azure 中的虛擬磁碟加密完全免費。 密碼編譯金鑰會儲存在 Azure 金鑰保存庫使用軟體保護，或者您可以匯入或產生您的金鑰，在硬體安全性模組 (Hsm) 認證 tooFIPS 140-2 層級 2 標準。 您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。 這些密碼編譯金鑰會使用的 tooencrypt，並解密附加的 tooyour VM 虛擬磁碟。 Azure Active Directory 服務主體會提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。

加密 VM hello 程序如下所示：

1. 在 Azure 金鑰保存庫中建立密碼編譯金鑰。
2. 設定 hello 密碼編譯金鑰 toobe 可用來加密磁碟。
3. tooread hello 密碼編譯金鑰從 hello Azure 金鑰保存庫，建立 Azure Active Directory 服務主體具有 hello 適當的權限。
4. 您的虛擬磁碟，指定 hello Azure Active Directory 服務主體 」 和 「 使用適當密碼編譯 toobe 發出 hello 命令 tooencrypt。
5. hello Azure Active Directory 服務主體要求 hello 必要的密碼編譯金鑰，從 Azure 金鑰保存庫。
6. hello 虛擬磁碟會使用提供的 hello 密碼編譯金鑰來加密。

## <a name="encryption-process"></a>加密程序
磁碟加密依賴 hello 下列額外的元件：

* **Azure 金鑰保存庫**-使用 toosafeguard 密碼編譯金鑰和 hello 磁碟加密/解密程序所使用的密碼。
  * 如果有的話，您可以使用現有的 Azure 金鑰保存庫。 您沒有 toodedicate 金鑰保存庫 tooencrypting 磁碟。
  * 系統管理界限使用 tooseparate 和索引鍵的可見性，您可以建立專用的金鑰保存庫。
* **Azure Active Directory** -控點 hello 必要的密碼編譯金鑰的安全交換和驗證要求的動作。
  * 您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。
  * 提供安全機制 toorequest hello 服務主體，並發出 hello 適當的密碼編譯金鑰。 您並未開發與 Azure Active Directory 整合的實際應用程式。

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

## <a name="create-azure-key-vault-and-keys"></a>建立 Azure Key Vault 和金鑰
您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。 在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包括 *myResourceGroup*、*myKey* 及 *myVM*。

hello 第一個步驟是 toocreate Azure 金鑰保存庫 toostore 密碼編譯金鑰。 Azure 金鑰保存庫可以儲存金鑰，密碼，或密碼，可讓您 toosecurely 它們實作中，您的應用程式和服務。 虛擬磁碟加密，您可以使用金鑰保存庫 toostore 使用的 tooencrypt 的密碼編譯金鑰或解密您的虛擬磁碟。

啟用 hello Azure 金鑰保存庫提供者與您 Azure 訂用帳戶內[az 提供者登錄](/cli/azure/provider#register)，並建立與資源群組[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立資源群組名稱*myResourceGroup*在 hello`eastus`位置：

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

hello Azure 金鑰保存庫包含 hello 密碼編譯金鑰與相關聯的計算資源，例如儲存體和 hello VM 本身必須位在 hello 相同的區域。 建立與 Azure 金鑰保存庫[az keyvault 建立](/cli/azure/keyvault#create)並啟用 hello 金鑰保存庫，磁碟加密搭配使用。 針對 *keyvault_name* 指定一個唯一的 Key Vault 名稱，如下所示︰

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。 使用 HSM 時需要進階金鑰保存庫。 沒有額外的成本 toocreating 高階金鑰保存庫，而不是標準儲存軟體保護金鑰的金鑰保存庫。 高階金鑰保存庫、 hello 前面步驟中的加入的 toocreate `--sku Premium` toohello 命令。 hello 下列範例會使用受軟體保護的金鑰因為我們建立標準的金鑰保存庫。

這兩種保護模型中，hello Azure 平台必須 toobe hello VM 開機 toodecrypt hello 虛擬磁碟時，授與存取 toorequest hello 密碼編譯金鑰。 使用 [az keyvault key create](/cli/azure/keyvault/key#create) 在 Key Vault 中建立密碼編譯金鑰。 hello 下列範例會建立名為*myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>建立 hello Azure Active Directory 服務主體
當虛擬磁碟加密或解密時，您可以指定帳戶 toohandle hello 驗證與金鑰保存庫中的密碼編譯金鑰交換。 此帳戶時，Azure Active Directory 服務主體可讓 hello Azure 平台 toorequest hello 適當的密碼編譯金鑰代表 hello VM。 雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。

使用 Azure Active Directory 搭配 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體。 下列範例中的 hello 讀取 hello 服務主體的 hello 值識別碼和密碼，以在更新版本的命令中使用：

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

當您建立 hello 服務主體時，才會顯示 hello 密碼。 如有需要，檢視並錄製 hello 密碼 (`echo $sp_password`)。 您可以使用 [az ad sp list](/cli/azure/ad/sp#list) 列出服務主體，以及使用 [az ad sp show](/cli/azure/ad/sp#show) 檢視特定服務主體的其他相關資訊。

toosuccessfully 加密或解密虛擬磁碟，儲存在金鑰保存庫中的 hello 密碼編譯金鑰的權限必須是集 toopermit hello Azure Active Directory 服務主體 tooread hello 索引鍵。 使用 [az keyvault set-policy](/cli/azure/keyvault#set-policy) 設定 Key Vault 的權限。 在下列範例的 hello，hello 服務主體的識別碼會提供從 hello 上述命令：

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Create virtual machine
tooactually 加密某些虛擬磁碟，可讓建立 VM 和加入資料磁碟。 建立與 VM tooencrypt [az vm 建立](/cli/azure/vm#create)5 Gb 資料磁碟並將。 只有某些 Marketplace 映像支援磁碟加密。 hello 下列範例會建立名為的 VM *myVM*使用**CentOS 7.2n**映像：

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM 使用 hello `publicIpAddress` hello 輸出的 hello 前面命令中所示。 建立分割區和檔案系統，然後掛接 hello 資料磁碟。 如需詳細資訊，請參閱[連接 tooa Linux VM toomount hello 新磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)。 關閉 SSH 工作階段。


## <a name="encrypt-virtual-machine"></a>將虛擬機器加密
tooencrypt hello 虛擬磁碟，您將一起所有 hello 舊版元件：

1. 指定 hello Azure Active Directory 服務主體和密碼。
2. 指定 hello 金鑰保存庫 toostore hello 中繼資料的加密磁碟。
3. 指定 hello hello 實際加密和解密的密碼編譯金鑰 toouse。
4. 指定是否要 tooencrypt hello OS 磁碟、 hello 資料磁碟，或全部。

使用 [az vm encryption enable](/cli/azure/vm/encryption#enable) 將您的 VM 加密。 hello 下列範例會使用 hello`$sp_id`和`$sp_password`變數從上述 hello`ad sp create-for-rbac`命令：

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

花一些時間 hello 磁碟加密程序 toocomplete。 監視 hello 程序與 hello 狀態[az vm 加密顯示](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello 輸出類似 toohello 之後，截斷的範例：

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

等候 hello OS 磁碟報告 hello 狀態直到**VMRestartPending**，然後重新啟動您的 VM 與[az vm 重新啟動](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

hello 磁碟加密程序完成 hello 開機程序期間，因此請稍候幾分鐘再檢查一次使用加密 hello 狀態**az vm 加密顯示**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello OS 磁碟和資料磁碟，現在應報告 hello 狀態**加密**。


## <a name="add-additional-data-disks"></a>新增其他資料磁碟
一旦您已加密資料磁碟，您可以稍後新增其他虛擬磁碟 tooyour VM，並也加密它們。 例如，可讓新增第二個虛擬磁碟 tooyour VM，如下所示：

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

重新執行 hello 命令 tooencrypt hello 虛擬磁碟，如下所示：

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>後續步驟
* 如需有關管理 Azure 金鑰保存庫 (包括刪除密碼編譯金鑰和保存庫) 的詳細資訊，請參閱[使用 CLI 管理金鑰保存庫](../../key-vault/key-vault-manage-with-cli2.md)。
* 如需有關磁碟加密，例如準備的加密自訂 VM tooupload tooAzure，請參閱[Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。
