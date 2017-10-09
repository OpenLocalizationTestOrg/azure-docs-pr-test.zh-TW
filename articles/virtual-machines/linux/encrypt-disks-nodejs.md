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
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="e03a7-103">加密使用 Azure CLI 1.0 hello 的 Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="e03a7-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="e03a7-104">如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的待用虛擬磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e03a7-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="e03a7-105">磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="e03a7-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="e03a7-106">您可控制這些密碼編譯金鑰，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="e03a7-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e03a7-107">這篇文章說明如何使用 Linux VM 上的虛擬磁碟 tooencrypt hello Azure CLI 1.0 和 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="e03a7-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e03a7-108">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="e03a7-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e03a7-109">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="e03a7-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e03a7-110">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="e03a7-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e03a7-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="e03a7-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e03a7-112">快速命令</span><span class="sxs-lookup"><span data-stu-id="e03a7-112">Quick commands</span></span>
<span data-ttu-id="e03a7-113">如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello 基底的 hello 命令 tooencrypt VM 上的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="e03a7-114">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#overview-of-disk-encryption)。</span><span class="sxs-lookup"><span data-stu-id="e03a7-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="e03a7-115">您需要 hello[最新的 Azure CLI 1.0](../../xplat-cli-install.md)安裝並登入，如下所示使用 hello Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="e03a7-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e03a7-116">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="e03a7-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e03a7-117">範例參數名稱包含 `myResourceGroup`、`myKeyVault` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="e03a7-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="e03a7-118">首先，啟用您的 Azure 訂用帳戶內的 hello Azure 金鑰保存庫提供者，並建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="e03a7-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="e03a7-119">hello 下列範例會建立資源群組名稱`myResourceGroup`在 hello`WestUS`位置：</span><span class="sxs-lookup"><span data-stu-id="e03a7-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="e03a7-120">建立 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e03a7-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="e03a7-121">hello 下列範例會建立名為金鑰保存庫`myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="e03a7-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="e03a7-122">在您的金鑰保存庫中建立密碼編譯金鑰，並針對磁碟加密加以啟用。</span><span class="sxs-lookup"><span data-stu-id="e03a7-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="e03a7-123">hello 下列範例會建立名為`myKey`:</span><span class="sxs-lookup"><span data-stu-id="e03a7-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="e03a7-124">建立使用 Azure Active Directory 處理 hello 驗證與金鑰保存庫中的密碼編譯金鑰交換的端點。</span><span class="sxs-lookup"><span data-stu-id="e03a7-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e03a7-125">hello`--home-page`和`--identifier-uris`不需要 toobe 實際路由的位址。</span><span class="sxs-lookup"><span data-stu-id="e03a7-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="e03a7-126">Hello 最高等級的安全性，您應該使用的用戶端密碼，而不是密碼。</span><span class="sxs-lookup"><span data-stu-id="e03a7-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="e03a7-127">hello Azure CLI 目前無法產生的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e03a7-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="e03a7-128">只能在 hello Azure 入口網站中產生的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e03a7-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="e03a7-129">hello 下列範例會建立名為 Azure Active Directory 端點`myAADApp`和使用的密碼`myPassword`。</span><span class="sxs-lookup"><span data-stu-id="e03a7-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="e03a7-130">指定您自己的密碼，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e03a7-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="e03a7-131">請注意 hello `applicationId` hello hello 前面命令的輸出所示。</span><span class="sxs-lookup"><span data-stu-id="e03a7-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="e03a7-132">此應用程式中使用了識別碼 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e03a7-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="e03a7-133">加入現有的 VM 資料磁碟 tooan。</span><span class="sxs-lookup"><span data-stu-id="e03a7-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="e03a7-134">hello 下列範例會將名為 VM 資料磁碟 tooa `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e03a7-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="e03a7-135">檢閱您所建立的金鑰保存庫和 hello 金鑰的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e03a7-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="e03a7-136">您需要在金鑰保存庫識別碼、 URI 和金鑰 hello hello 最後一個步驟中的 URL。</span><span class="sxs-lookup"><span data-stu-id="e03a7-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="e03a7-137">hello 下列範例會檢閱 hello 詳細資料的金鑰保存庫名為`myKeyVault`和名為機碼`myKey`:</span><span class="sxs-lookup"><span data-stu-id="e03a7-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="e03a7-138">如下所示，始終輸入您自己的參數名稱，將您的磁碟加密︰</span><span class="sxs-lookup"><span data-stu-id="e03a7-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="e03a7-139">hello Azure CLI hello 加密程序期間不會提供詳細的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e03a7-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="e03a7-140">如需其他疑難排解資訊，請檢閱 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`。</span><span class="sxs-lookup"><span data-stu-id="e03a7-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="e03a7-141">Hello 前面命令有許多變數可能不會得到多指示 as toowhy hello 程序就會失敗，完整的命令範例應如下：</span><span class="sxs-lookup"><span data-stu-id="e03a7-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="e03a7-142">最後，檢閱 hello 加密狀態再次 tooconfirm 有現在已加密您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="e03a7-143">hello 下列範例會檢查名為的 VM hello 狀態`myVM`在 hello`myResourceGroup`資源群組：</span><span class="sxs-lookup"><span data-stu-id="e03a7-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="e03a7-144">磁碟加密概觀</span><span class="sxs-lookup"><span data-stu-id="e03a7-144">Overview of disk encryption</span></span>
<span data-ttu-id="e03a7-145">Linux VM 上的待用虛擬磁碟會使用 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt) 進行加密。</span><span class="sxs-lookup"><span data-stu-id="e03a7-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="e03a7-146">將 Azure 中的虛擬磁碟加密完全免費。</span><span class="sxs-lookup"><span data-stu-id="e03a7-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="e03a7-147">密碼編譯金鑰會儲存在 Azure 金鑰保存庫使用軟體保護，或者您可以匯入或產生您的金鑰，在硬體安全性模組 (Hsm) 認證 tooFIPS 140-2 層級 2 標準。</span><span class="sxs-lookup"><span data-stu-id="e03a7-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="e03a7-148">您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="e03a7-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e03a7-149">這些密碼編譯金鑰會使用的 tooencrypt，並解密附加的 tooyour VM 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="e03a7-150">Azure Active Directory 端點提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="e03a7-151">加密 VM hello 程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="e03a7-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="e03a7-152">在 Azure 金鑰保存庫中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="e03a7-153">設定 hello 密碼編譯金鑰 toobe 可用來加密磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="e03a7-154">hello Azure 金鑰保存庫，從 tooread hello 密碼編譯金鑰會建立使用 Azure Active Directory 與 hello 適當的權限的端點。</span><span class="sxs-lookup"><span data-stu-id="e03a7-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="e03a7-155">您的虛擬磁碟，指定 hello Azure Active Directory 端點，並使用適當密碼編譯 toobe 發出 hello 命令 tooencrypt。</span><span class="sxs-lookup"><span data-stu-id="e03a7-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="e03a7-156">hello Azure Active Directory 端點要求 Azure 金鑰保存庫中的 hello 必要的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="e03a7-157">hello 虛擬磁碟會使用提供的 hello 密碼編譯金鑰來加密。</span><span class="sxs-lookup"><span data-stu-id="e03a7-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="e03a7-158">支援服務和加密程序</span><span class="sxs-lookup"><span data-stu-id="e03a7-158">Supporting services and encryption process</span></span>
<span data-ttu-id="e03a7-159">磁碟加密依賴 hello 下列額外的元件：</span><span class="sxs-lookup"><span data-stu-id="e03a7-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="e03a7-160">**Azure 金鑰保存庫**-使用 toosafeguard 密碼編譯金鑰和 hello 磁碟加密/解密程序所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="e03a7-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="e03a7-161">如果有的話，您可以使用現有的 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e03a7-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="e03a7-162">您沒有 toodedicate 金鑰保存庫 tooencrypting 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="e03a7-163">系統管理界限使用 tooseparate 和索引鍵的可見性，您可以建立專用的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e03a7-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="e03a7-164">**Azure Active Directory** -控點 hello 必要的密碼編譯金鑰的安全交換和驗證要求的動作。</span><span class="sxs-lookup"><span data-stu-id="e03a7-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="e03a7-165">您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e03a7-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="e03a7-166">較高的 hello 金鑰保存庫的端點和虛擬機器服務 toorequest hello 應用程式，並取得發出 hello 適當的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="e03a7-167">您並未開發與 Azure Active Directory 整合的實際應用程式。</span><span class="sxs-lookup"><span data-stu-id="e03a7-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="e03a7-168">需求和限制</span><span class="sxs-lookup"><span data-stu-id="e03a7-168">Requirements and limitations</span></span>
<span data-ttu-id="e03a7-169">磁碟加密支援的案例和需求：</span><span class="sxs-lookup"><span data-stu-id="e03a7-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="e03a7-170">下列 Linux 伺服器 Sku-Ubuntu、 CentOS、 SUSE 和 SUSE Linux Enterprise Server (SLES) 和 Red Hat Enterprise Linux hello。</span><span class="sxs-lookup"><span data-stu-id="e03a7-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="e03a7-171">所有資源 （例如金鑰保存庫、 儲存體帳戶和 VM） 都必須在 hello 相同的 Azure 地區和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e03a7-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="e03a7-172">標準 A、D、DS、G 和 GS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="e03a7-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="e03a7-173">磁碟加密目前不支援在下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="e03a7-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="e03a7-174">基本層 VM。</span><span class="sxs-lookup"><span data-stu-id="e03a7-174">Basic tier VMs.</span></span>
* <span data-ttu-id="e03a7-175">使用 hello 傳統部署模型所建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e03a7-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="e03a7-176">在 Linux VM 上停用作業系統磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e03a7-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="e03a7-177">正在更新 hello 已加密的 Linux VM 上的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="e03a7-178">建立 hello Azure 金鑰保存庫和金鑰</span><span class="sxs-lookup"><span data-stu-id="e03a7-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="e03a7-179">本指南的 toocomplete hello 其餘部分，您需要 hello[最新的 Azure CLI 1.0](../../xplat-cli-install.md)安裝並登入，如下所示使用 hello Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="e03a7-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e03a7-180">整個 hello 命令範例，所有範例參數都取代您自己的名稱、 位置和索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="e03a7-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="e03a7-181">hello 下列範例會使用的慣例`myResourceGroup`， `myKeyVault`，`myAADApp`等等。</span><span class="sxs-lookup"><span data-stu-id="e03a7-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="e03a7-182">hello 第一個步驟是 toocreate Azure 金鑰保存庫 toostore 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="e03a7-183">Azure 金鑰保存庫可以儲存金鑰，密碼，或密碼，可讓您 toosecurely 它們實作中，您的應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="e03a7-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="e03a7-184">虛擬磁碟加密，您可以使用金鑰保存庫 toostore 使用的 tooencrypt 的密碼編譯金鑰或解密您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="e03a7-185">啟用您 Azure 訂用帳戶中的 hello Azure 金鑰保存庫提供者，然後建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="e03a7-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="e03a7-186">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUS`位置：</span><span class="sxs-lookup"><span data-stu-id="e03a7-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="e03a7-187">hello Azure 金鑰保存庫包含 hello 密碼編譯金鑰與相關聯的計算資源，例如儲存體和 hello VM 本身必須位在 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="e03a7-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="e03a7-188">hello 下列範例會建立名為 Azure 金鑰保存庫`myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="e03a7-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="e03a7-189">您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="e03a7-190">使用 HSM 時需要進階金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e03a7-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="e03a7-191">沒有額外的成本 toocreating 高階金鑰保存庫，而不是標準儲存軟體保護金鑰的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e03a7-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="e03a7-192">高階金鑰保存庫、 hello 前面步驟中的加入的 toocreate `--sku Premium` toohello 命令。</span><span class="sxs-lookup"><span data-stu-id="e03a7-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="e03a7-193">hello 下列範例會使用受軟體保護的金鑰因為我們建立標準的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e03a7-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="e03a7-194">這兩種保護模型中，hello Azure 平台必須 toobe hello VM 開機 toodecrypt hello 虛擬磁碟時，授與存取 toorequest hello 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="e03a7-195">在您的金鑰保存庫中建立加密金鑰，然後加以啟用以便用於虛擬磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e03a7-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="e03a7-196">hello 下列範例會建立名為`myKey`然後再啟用它，磁碟加密：</span><span class="sxs-lookup"><span data-stu-id="e03a7-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="e03a7-197">建立 hello Azure Active Directory 應用程式</span><span class="sxs-lookup"><span data-stu-id="e03a7-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="e03a7-198">當虛擬磁碟加密或解密時，您可以使用端點 toohandle hello 驗證，以及交換的金鑰保存庫中的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e03a7-199">此端點，Azure Active Directory 應用程式，可讓 hello Azure 平台 toorequest hello 適當的密碼編譯金鑰代表 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e03a7-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="e03a7-200">雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e03a7-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="e03a7-201">您不會建立完整的 Azure Active Directory 應用程式，如 hello`--home-page`和`--identifier-uris`hello 下列範例中的參數不需要 toobe 實際路由的位址。</span><span class="sxs-lookup"><span data-stu-id="e03a7-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="e03a7-202">hello 下列範例也會指定密碼為基礎的密碼，而不是來自 hello Azure 入口網站中產生的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="e03a7-203">為此階段中，無法從 hello Azure CLI 完成產生的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e03a7-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="e03a7-204">建立 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e03a7-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="e03a7-205">hello 下列範例會建立名為應用程式`myAADApp`和使用的密碼`myPassword`。</span><span class="sxs-lookup"><span data-stu-id="e03a7-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="e03a7-206">指定您自己的密碼，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e03a7-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="e03a7-207">請記下 hello `applicationId` hello 前面命令從 hello 輸出中傳回。</span><span class="sxs-lookup"><span data-stu-id="e03a7-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="e03a7-208">在某些其他步驟的 hello 使用這個應用程式 ID。</span><span class="sxs-lookup"><span data-stu-id="e03a7-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="e03a7-209">接下來，建立服務主體名稱 (SPN)，以便 hello 應用程式都可存取您的環境。</span><span class="sxs-lookup"><span data-stu-id="e03a7-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="e03a7-210">toosuccessfully 加密或解密虛擬磁碟，儲存在金鑰保存庫中的 hello 密碼編譯金鑰的權限必須是集 toopermit hello Azure Active Directory 應用程式 tooread hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e03a7-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="e03a7-211">建立 hello SPN，並設定 hello 適當的權限，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e03a7-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="e03a7-212">新增虛擬磁碟並檢閱加密狀態</span><span class="sxs-lookup"><span data-stu-id="e03a7-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="e03a7-213">tooactually 加密某些虛擬磁碟，可讓您加入現有的 VM 磁碟 tooan。</span><span class="sxs-lookup"><span data-stu-id="e03a7-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="e03a7-214">加入現有的 VM，如下所示的 5 Gb 資料磁碟 tooan:</span><span class="sxs-lookup"><span data-stu-id="e03a7-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="e03a7-215">目前未加密 hello 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="e03a7-216">請檢閱您 VM 的 hello 目前加密狀態，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e03a7-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="e03a7-217">將虛擬磁碟加密</span><span class="sxs-lookup"><span data-stu-id="e03a7-217">Encrypt virtual disks</span></span>
<span data-ttu-id="e03a7-218">toonow 加密 hello 虛擬磁碟，同時讓所有 hello 舊版元件：</span><span class="sxs-lookup"><span data-stu-id="e03a7-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="e03a7-219">指定 hello Azure Active Directory 應用程式和密碼。</span><span class="sxs-lookup"><span data-stu-id="e03a7-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="e03a7-220">指定 hello 金鑰保存庫 toostore hello 中繼資料的加密磁碟。</span><span class="sxs-lookup"><span data-stu-id="e03a7-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="e03a7-221">指定 hello hello 實際加密和解密的密碼編譯金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="e03a7-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="e03a7-222">指定是否要 tooencrypt hello OS 磁碟、 hello 資料磁碟，或全部。</span><span class="sxs-lookup"><span data-stu-id="e03a7-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="e03a7-223">可讓檢視您的 Azure 金鑰保存庫和 hello 金鑰您建立的您需要 hello 金鑰保存庫識別碼 URI，然後在最後一個步驟中 hello 金鑰 URL hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="e03a7-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="e03a7-224">加密您的虛擬磁碟使用 hello hello 輸出`azure keyvault show`和`azure keyvault key show`命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e03a7-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="e03a7-225">Hello 前述的命令有許多變數，如 hello 下列範例是 hello 完整命令參考：</span><span class="sxs-lookup"><span data-stu-id="e03a7-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

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

<span data-ttu-id="e03a7-226">hello Azure CLI hello 加密程序期間不會提供詳細的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e03a7-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="e03a7-227">如需其他疑難排解資訊，請檢閱`/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`hello 要加密的 VM 上。</span><span class="sxs-lookup"><span data-stu-id="e03a7-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="e03a7-228">最後，可讓檢閱 hello 加密狀態再次 tooconfirm 有現在已加密您的虛擬磁碟：</span><span class="sxs-lookup"><span data-stu-id="e03a7-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="e03a7-229">新增其他資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e03a7-229">Add additional data disks</span></span>
<span data-ttu-id="e03a7-230">一旦您已加密資料磁碟，您可以稍後新增其他虛擬磁碟 tooyour VM，並也加密它們。</span><span class="sxs-lookup"><span data-stu-id="e03a7-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="e03a7-231">當您執行 hello`azure vm enable-disk-encryption`命令、 遞增 hello 順序版本使用 hello`--sequence-version`參數。</span><span class="sxs-lookup"><span data-stu-id="e03a7-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="e03a7-232">此順序的 version 參數可讓您 tooperform 上的重複的作業 hello 相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="e03a7-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="e03a7-233">例如，可讓新增第二個虛擬磁碟 tooyour VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e03a7-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="e03a7-234">重新執行 hello 命令 tooencrypt hello 的虛擬磁碟，這次加入 hello`--sequence-version`參數，而遞增 hello 值我們第一個執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e03a7-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="e03a7-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e03a7-235">Next steps</span></span>
* <span data-ttu-id="e03a7-236">如需有關管理 Azure 金鑰保存庫 (包括刪除密碼編譯金鑰和保存庫) 的詳細資訊，請參閱[使用 CLI 管理金鑰保存庫](../../key-vault/key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="e03a7-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="e03a7-237">如需有關磁碟加密，例如準備的加密自訂 VM tooupload tooAzure，請參閱[Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="e03a7-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
