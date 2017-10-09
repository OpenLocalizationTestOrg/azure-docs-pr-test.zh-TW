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
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="7592e-103">如何 tooencrypt Linux VM 上的虛擬磁碟</span><span class="sxs-lookup"><span data-stu-id="7592e-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="7592e-104">如需強化虛擬機器 (VM) 安全性與法規遵循，可以將 Azure 中的虛擬磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="7592e-105">磁碟會使用 Azure 金鑰保存庫中受保護的密碼編譯金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="7592e-106">您可控制這些密碼編譯金鑰，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="7592e-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="7592e-107">這篇文章說明如何使用 Linux VM 上的虛擬磁碟 tooencrypt hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="7592e-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="7592e-108">您也可以執行下列步驟以 hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7592e-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="7592e-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="7592e-109">Quick commands</span></span>
<span data-ttu-id="7592e-110">如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello 基底的 hello 命令 tooencrypt VM 上的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="7592e-111">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#overview-of-disk-encryption)。</span><span class="sxs-lookup"><span data-stu-id="7592e-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="7592e-112">您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="7592e-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="7592e-113">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="7592e-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7592e-114">範例參數名稱包括 *myResourceGroup*、*myKey* 及 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="7592e-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="7592e-115">首先，啟用 hello Azure 金鑰保存庫提供者與您 Azure 訂用帳戶內[az 提供者登錄](/cli/azure/provider#register)，並建立與資源群組[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="7592e-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7592e-116">hello 下列範例會建立資源群組名稱*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="7592e-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7592e-117">建立與 Azure 金鑰保存庫[az keyvault 建立](/cli/azure/keyvault#create)並啟用 hello 金鑰保存庫，磁碟加密搭配使用。</span><span class="sxs-lookup"><span data-stu-id="7592e-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="7592e-118">針對 *keyvault_name* 指定一個唯一的 Key Vault 名稱，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7592e-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="7592e-119">使用 [az keyvault key create](/cli/azure/keyvault/key#create) 在 Key Vault 中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="7592e-120">hello 下列範例會建立名為*myKey*:</span><span class="sxs-lookup"><span data-stu-id="7592e-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="7592e-121">使用 Azure Active Directory 搭配 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="7592e-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="7592e-122">hello 服務主體的控制代碼 hello 驗證與金鑰保存庫中的密碼編譯金鑰交換。</span><span class="sxs-lookup"><span data-stu-id="7592e-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="7592e-123">下列範例中的 hello 讀取 hello 服務主體的 hello 值識別碼和密碼，以在更新版本的命令中使用：</span><span class="sxs-lookup"><span data-stu-id="7592e-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="7592e-124">當您建立 hello 服務主體時，只是輸出 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="7592e-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="7592e-125">如有需要，檢視並錄製 hello 密碼 (`echo $sp_password`)。</span><span class="sxs-lookup"><span data-stu-id="7592e-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="7592e-126">您可以使用 [az ad sp list](/cli/azure/ad/sp#list) 列出服務主體，以及使用 [az ad sp show](/cli/azure/ad/sp#show) 檢視特定服務主體的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7592e-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="7592e-127">使用 [az keyvault set-policy](/cli/azure/keyvault#set-policy) 設定 Key Vault 的權限。</span><span class="sxs-lookup"><span data-stu-id="7592e-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="7592e-128">在下列範例的 hello，hello 服務主體的識別碼會提供從 hello 上述命令：</span><span class="sxs-lookup"><span data-stu-id="7592e-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="7592e-129">使用 [az vm create](/cli/azure/vm#create) 建立 VM 並連結 5GB 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="7592e-130">只有某些 Marketplace 映像支援磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="7592e-131">hello 下列範例會建立名為的 VM`myVM`使用**CentOS 7.2n**映像：</span><span class="sxs-lookup"><span data-stu-id="7592e-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="7592e-132">SSH tooyour VM 使用 hello `publicIpAddress` hello 輸出的 hello 前面命令中所示。</span><span class="sxs-lookup"><span data-stu-id="7592e-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="7592e-133">建立分割區和檔案系統，然後掛接 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="7592e-134">如需詳細資訊，請參閱[連接 tooa Linux VM toomount hello 新磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)。</span><span class="sxs-lookup"><span data-stu-id="7592e-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="7592e-135">關閉 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="7592e-135">Close your SSH session.</span></span>

<span data-ttu-id="7592e-136">使用 [az vm encryption enable](/cli/azure/vm/encryption#enable) 將您的 VM 加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="7592e-137">hello 下列範例會使用 hello`$sp_id`和`$sp_password`變數從上述 hello`ad sp create-for-rbac`命令：</span><span class="sxs-lookup"><span data-stu-id="7592e-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="7592e-138">花一些時間 hello 磁碟加密程序 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7592e-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="7592e-139">監視 hello 程序與 hello 狀態[az vm 加密顯示](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="7592e-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7592e-140">hello 狀態顯示**EncryptionInProgress**。</span><span class="sxs-lookup"><span data-stu-id="7592e-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="7592e-141">等候 hello OS 磁碟報告 hello 狀態直到**VMRestartPending**，然後重新啟動您的 VM 與[az vm 重新啟動](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="7592e-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7592e-142">hello 磁碟加密程序完成 hello 開機程序期間，因此請稍候幾分鐘再檢查一次使用加密 hello 狀態**az vm 加密顯示**:</span><span class="sxs-lookup"><span data-stu-id="7592e-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7592e-143">hello OS 磁碟和資料磁碟，現在應報告 hello 狀態**加密**。</span><span class="sxs-lookup"><span data-stu-id="7592e-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="7592e-144">磁碟加密概觀</span><span class="sxs-lookup"><span data-stu-id="7592e-144">Overview of disk encryption</span></span>
<span data-ttu-id="7592e-145">Linux VM 上的待用虛擬磁碟會使用 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt) 進行加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="7592e-146">將 Azure 中的虛擬磁碟加密完全免費。</span><span class="sxs-lookup"><span data-stu-id="7592e-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="7592e-147">密碼編譯金鑰會儲存在 Azure 金鑰保存庫使用軟體保護，或者您可以匯入或產生您的金鑰，在硬體安全性模組 (Hsm) 認證 tooFIPS 140-2 層級 2 標準。</span><span class="sxs-lookup"><span data-stu-id="7592e-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="7592e-148">您可保留這些密碼編譯金鑰的控制權，並可稽核其使用情況。</span><span class="sxs-lookup"><span data-stu-id="7592e-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="7592e-149">這些密碼編譯金鑰會使用的 tooencrypt，並解密附加的 tooyour VM 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="7592e-150">Azure Active Directory 服務主體會提供一個安全機制，以便在 VM 開機或關機時發出這些密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="7592e-151">加密 VM hello 程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="7592e-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="7592e-152">在 Azure 金鑰保存庫中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="7592e-153">設定 hello 密碼編譯金鑰 toobe 可用來加密磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="7592e-154">tooread hello 密碼編譯金鑰從 hello Azure 金鑰保存庫，建立 Azure Active Directory 服務主體具有 hello 適當的權限。</span><span class="sxs-lookup"><span data-stu-id="7592e-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="7592e-155">您的虛擬磁碟，指定 hello Azure Active Directory 服務主體 」 和 「 使用適當密碼編譯 toobe 發出 hello 命令 tooencrypt。</span><span class="sxs-lookup"><span data-stu-id="7592e-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="7592e-156">hello Azure Active Directory 服務主體要求 hello 必要的密碼編譯金鑰，從 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7592e-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="7592e-157">hello 虛擬磁碟會使用提供的 hello 密碼編譯金鑰來加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="7592e-158">加密程序</span><span class="sxs-lookup"><span data-stu-id="7592e-158">Encryption process</span></span>
<span data-ttu-id="7592e-159">磁碟加密依賴 hello 下列額外的元件：</span><span class="sxs-lookup"><span data-stu-id="7592e-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="7592e-160">**Azure 金鑰保存庫**-使用 toosafeguard 密碼編譯金鑰和 hello 磁碟加密/解密程序所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="7592e-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="7592e-161">如果有的話，您可以使用現有的 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7592e-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="7592e-162">您沒有 toodedicate 金鑰保存庫 tooencrypting 磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="7592e-163">系統管理界限使用 tooseparate 和索引鍵的可見性，您可以建立專用的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7592e-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="7592e-164">**Azure Active Directory** -控點 hello 必要的密碼編譯金鑰的安全交換和驗證要求的動作。</span><span class="sxs-lookup"><span data-stu-id="7592e-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="7592e-165">您通常使用現有的 Azure Active Directory 執行個體來裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7592e-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="7592e-166">提供安全機制 toorequest hello 服務主體，並發出 hello 適當的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="7592e-167">您並未開發與 Azure Active Directory 整合的實際應用程式。</span><span class="sxs-lookup"><span data-stu-id="7592e-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="7592e-168">需求和限制</span><span class="sxs-lookup"><span data-stu-id="7592e-168">Requirements and limitations</span></span>
<span data-ttu-id="7592e-169">磁碟加密支援的案例和需求：</span><span class="sxs-lookup"><span data-stu-id="7592e-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="7592e-170">下列 Linux 伺服器 Sku-Ubuntu、 CentOS、 SUSE 和 SUSE Linux Enterprise Server (SLES) 和 Red Hat Enterprise Linux hello。</span><span class="sxs-lookup"><span data-stu-id="7592e-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="7592e-171">所有資源 （例如金鑰保存庫、 儲存體帳戶和 VM） 都必須在 hello 相同的 Azure 地區和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7592e-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="7592e-172">標準 A、D、DS、G 和 GS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="7592e-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="7592e-173">磁碟加密目前不支援在下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="7592e-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="7592e-174">基本層 VM。</span><span class="sxs-lookup"><span data-stu-id="7592e-174">Basic tier VMs.</span></span>
* <span data-ttu-id="7592e-175">使用 hello 傳統部署模型所建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="7592e-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="7592e-176">在 Linux VM 上停用作業系統磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="7592e-177">正在更新 hello 已加密的 Linux VM 上的密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="7592e-178">建立 Azure Key Vault 和金鑰</span><span class="sxs-lookup"><span data-stu-id="7592e-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="7592e-179">您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="7592e-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="7592e-180">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="7592e-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7592e-181">範例參數名稱包括 *myResourceGroup*、*myKey* 及 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="7592e-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="7592e-182">hello 第一個步驟是 toocreate Azure 金鑰保存庫 toostore 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="7592e-183">Azure 金鑰保存庫可以儲存金鑰，密碼，或密碼，可讓您 toosecurely 它們實作中，您的應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="7592e-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="7592e-184">虛擬磁碟加密，您可以使用金鑰保存庫 toostore 使用的 tooencrypt 的密碼編譯金鑰或解密您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="7592e-185">啟用 hello Azure 金鑰保存庫提供者與您 Azure 訂用帳戶內[az 提供者登錄](/cli/azure/provider#register)，並建立與資源群組[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="7592e-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7592e-186">hello 下列範例會建立資源群組名稱*myResourceGroup*在 hello`eastus`位置：</span><span class="sxs-lookup"><span data-stu-id="7592e-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7592e-187">hello Azure 金鑰保存庫包含 hello 密碼編譯金鑰與相關聯的計算資源，例如儲存體和 hello VM 本身必須位在 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="7592e-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="7592e-188">建立與 Azure 金鑰保存庫[az keyvault 建立](/cli/azure/keyvault#create)並啟用 hello 金鑰保存庫，磁碟加密搭配使用。</span><span class="sxs-lookup"><span data-stu-id="7592e-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="7592e-189">針對 *keyvault_name* 指定一個唯一的 Key Vault 名稱，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7592e-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="7592e-190">您可以使用軟體或硬體安全性模型 (HSM) 保護功能來儲存密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="7592e-191">使用 HSM 時需要進階金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7592e-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="7592e-192">沒有額外的成本 toocreating 高階金鑰保存庫，而不是標準儲存軟體保護金鑰的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7592e-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="7592e-193">高階金鑰保存庫、 hello 前面步驟中的加入的 toocreate `--sku Premium` toohello 命令。</span><span class="sxs-lookup"><span data-stu-id="7592e-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="7592e-194">hello 下列範例會使用受軟體保護的金鑰因為我們建立標準的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="7592e-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="7592e-195">這兩種保護模型中，hello Azure 平台必須 toobe hello VM 開機 toodecrypt hello 虛擬磁碟時，授與存取 toorequest hello 密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="7592e-196">使用 [az keyvault key create](/cli/azure/keyvault/key#create) 在 Key Vault 中建立密碼編譯金鑰。</span><span class="sxs-lookup"><span data-stu-id="7592e-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="7592e-197">hello 下列範例會建立名為*myKey*:</span><span class="sxs-lookup"><span data-stu-id="7592e-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="7592e-198">建立 hello Azure Active Directory 服務主體</span><span class="sxs-lookup"><span data-stu-id="7592e-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="7592e-199">當虛擬磁碟加密或解密時，您可以指定帳戶 toohandle hello 驗證與金鑰保存庫中的密碼編譯金鑰交換。</span><span class="sxs-lookup"><span data-stu-id="7592e-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="7592e-200">此帳戶時，Azure Active Directory 服務主體可讓 hello Azure 平台 toorequest hello 適當的密碼編譯金鑰代表 hello VM。</span><span class="sxs-lookup"><span data-stu-id="7592e-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="7592e-201">雖然許多組織都有專用的 Azure Active Directory 目錄，但您的訂用帳戶中會有預設 Azure Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7592e-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="7592e-202">使用 Azure Active Directory 搭配 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="7592e-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="7592e-203">下列範例中的 hello 讀取 hello 服務主體的 hello 值識別碼和密碼，以在更新版本的命令中使用：</span><span class="sxs-lookup"><span data-stu-id="7592e-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="7592e-204">當您建立 hello 服務主體時，才會顯示 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="7592e-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="7592e-205">如有需要，檢視並錄製 hello 密碼 (`echo $sp_password`)。</span><span class="sxs-lookup"><span data-stu-id="7592e-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="7592e-206">您可以使用 [az ad sp list](/cli/azure/ad/sp#list) 列出服務主體，以及使用 [az ad sp show](/cli/azure/ad/sp#show) 檢視特定服務主體的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7592e-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="7592e-207">toosuccessfully 加密或解密虛擬磁碟，儲存在金鑰保存庫中的 hello 密碼編譯金鑰的權限必須是集 toopermit hello Azure Active Directory 服務主體 tooread hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7592e-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="7592e-208">使用 [az keyvault set-policy](/cli/azure/keyvault#set-policy) 設定 Key Vault 的權限。</span><span class="sxs-lookup"><span data-stu-id="7592e-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="7592e-209">在下列範例的 hello，hello 服務主體的識別碼會提供從 hello 上述命令：</span><span class="sxs-lookup"><span data-stu-id="7592e-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="7592e-210">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="7592e-210">Create virtual machine</span></span>
<span data-ttu-id="7592e-211">tooactually 加密某些虛擬磁碟，可讓建立 VM 和加入資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="7592e-212">建立與 VM tooencrypt [az vm 建立](/cli/azure/vm#create)5 Gb 資料磁碟並將。</span><span class="sxs-lookup"><span data-stu-id="7592e-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="7592e-213">只有某些 Marketplace 映像支援磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="7592e-214">hello 下列範例會建立名為的 VM *myVM*使用**CentOS 7.2n**映像：</span><span class="sxs-lookup"><span data-stu-id="7592e-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="7592e-215">SSH tooyour VM 使用 hello `publicIpAddress` hello 輸出的 hello 前面命令中所示。</span><span class="sxs-lookup"><span data-stu-id="7592e-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="7592e-216">建立分割區和檔案系統，然後掛接 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="7592e-217">如需詳細資訊，請參閱[連接 tooa Linux VM toomount hello 新磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)。</span><span class="sxs-lookup"><span data-stu-id="7592e-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="7592e-218">關閉 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="7592e-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="7592e-219">將虛擬機器加密</span><span class="sxs-lookup"><span data-stu-id="7592e-219">Encrypt virtual machine</span></span>
<span data-ttu-id="7592e-220">tooencrypt hello 虛擬磁碟，您將一起所有 hello 舊版元件：</span><span class="sxs-lookup"><span data-stu-id="7592e-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="7592e-221">指定 hello Azure Active Directory 服務主體和密碼。</span><span class="sxs-lookup"><span data-stu-id="7592e-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="7592e-222">指定 hello 金鑰保存庫 toostore hello 中繼資料的加密磁碟。</span><span class="sxs-lookup"><span data-stu-id="7592e-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="7592e-223">指定 hello hello 實際加密和解密的密碼編譯金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="7592e-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="7592e-224">指定是否要 tooencrypt hello OS 磁碟、 hello 資料磁碟，或全部。</span><span class="sxs-lookup"><span data-stu-id="7592e-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="7592e-225">使用 [az vm encryption enable](/cli/azure/vm/encryption#enable) 將您的 VM 加密。</span><span class="sxs-lookup"><span data-stu-id="7592e-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="7592e-226">hello 下列範例會使用 hello`$sp_id`和`$sp_password`變數從上述 hello`ad sp create-for-rbac`命令：</span><span class="sxs-lookup"><span data-stu-id="7592e-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="7592e-227">花一些時間 hello 磁碟加密程序 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7592e-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="7592e-228">監視 hello 程序與 hello 狀態[az vm 加密顯示](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="7592e-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7592e-229">hello 輸出類似 toohello 之後，截斷的範例：</span><span class="sxs-lookup"><span data-stu-id="7592e-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="7592e-230">等候 hello OS 磁碟報告 hello 狀態直到**VMRestartPending**，然後重新啟動您的 VM 與[az vm 重新啟動](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="7592e-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7592e-231">hello 磁碟加密程序完成 hello 開機程序期間，因此請稍候幾分鐘再檢查一次使用加密 hello 狀態**az vm 加密顯示**:</span><span class="sxs-lookup"><span data-stu-id="7592e-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7592e-232">hello OS 磁碟和資料磁碟，現在應報告 hello 狀態**加密**。</span><span class="sxs-lookup"><span data-stu-id="7592e-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="7592e-233">新增其他資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7592e-233">Add additional data disks</span></span>
<span data-ttu-id="7592e-234">一旦您已加密資料磁碟，您可以稍後新增其他虛擬磁碟 tooyour VM，並也加密它們。</span><span class="sxs-lookup"><span data-stu-id="7592e-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="7592e-235">例如，可讓新增第二個虛擬磁碟 tooyour VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7592e-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="7592e-236">重新執行 hello 命令 tooencrypt hello 虛擬磁碟，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7592e-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="7592e-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7592e-237">Next steps</span></span>
* <span data-ttu-id="7592e-238">如需有關管理 Azure 金鑰保存庫 (包括刪除密碼編譯金鑰和保存庫) 的詳細資訊，請參閱[使用 CLI 管理金鑰保存庫](../../key-vault/key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="7592e-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="7592e-239">如需有關磁碟加密，例如準備的加密自訂 VM tooupload tooAzure，請參閱[Azure 磁碟加密](../../security/azure-security-disk-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="7592e-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
