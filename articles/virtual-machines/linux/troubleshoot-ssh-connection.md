---
title: "aaaTroubleshoot SSH 連線問題 tooan Azure VM |Microsoft 文件"
description: "如何 tootroubleshoot 發出例如 'SSH 連線失敗' 或 'SSH 連線被拒' 的 Azure vm 執行 Linux。"
keywords: "ssh 連線被拒, ssh 錯誤, azure ssh, ssh 連線失敗"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="e3988-104">疑難排解 SSH 連線 tooan Azure Linux VM 失敗，錯誤，或被拒</span><span class="sxs-lookup"><span data-stu-id="e3988-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="e3988-105">有各種原因發生安全殼層 (SSH) 錯誤，SSH 連線失敗，或當您嘗試 tooconnect tooa Linux 虛擬機器 (VM) 時，就會拒絕 SSH。</span><span class="sxs-lookup"><span data-stu-id="e3988-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="e3988-106">這篇文章可協助您尋找和正確的 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="e3988-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="e3988-107">您可以用於 Linux tootroubleshoot hello Azure 入口網站，Azure CLI 或 VM 存取擴充功能，並解決連線問題。</span><span class="sxs-lookup"><span data-stu-id="e3988-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e3988-108">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](http://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="e3988-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e3988-109">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="e3988-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e3988-110">移 toohello [Azure 支援服務網站](http://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="e3988-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="e3988-111">使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](http://azure.microsoft.com/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="e3988-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="e3988-112">快速疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="e3988-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="e3988-113">每個疑難排解的步驟之後，嘗試重新連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="e3988-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="e3988-114">重設 hello SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="e3988-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="e3988-115">重設 hello hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="e3988-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="e3988-116">確認 hello[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)規則允許 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="e3988-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="e3988-117">請確認網路安全性群組規則存在 toopermit SSH 流量 （依預設，TCP 連接埠 22）。</span><span class="sxs-lookup"><span data-stu-id="e3988-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="e3988-118">若未使用 Azure 負載平衡器，則無法使用連接埠重新導向 / 對應功能。</span><span class="sxs-lookup"><span data-stu-id="e3988-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="e3988-119">檢查 hello [VM 資源健全狀況](../../resource-health/resource-health-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e3988-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="e3988-120">請確定該 hello VM 為狀況良好的報表。</span><span class="sxs-lookup"><span data-stu-id="e3988-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="e3988-121">如果您有開機診斷功能，請確認 hello VM 未回報開機 hello 記錄檔中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e3988-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="e3988-122">重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e3988-122">Restart hello VM.</span></span>
6. <span data-ttu-id="e3988-123">重新部署 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e3988-123">Redeploy hello VM.</span></span>

<span data-ttu-id="e3988-124">如需更詳細的疑難排解步驟與說明，請繼續閱讀。</span><span class="sxs-lookup"><span data-stu-id="e3988-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="e3988-125">可用的方法 tootroubleshoot SSH 連線問題</span><span class="sxs-lookup"><span data-stu-id="e3988-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="e3988-126">您可以重設認證或使用其中一種下列方法 hello 的 SSH 組態：</span><span class="sxs-lookup"><span data-stu-id="e3988-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="e3988-127">[Azure 入口網站](#use-the-azure-portal)-太好了，如果您需要 tooquickly 重設 hello SSH 組態或 SSH 金鑰，並不 hello Azure tools 安裝。</span><span class="sxs-lookup"><span data-stu-id="e3988-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="e3988-128">[Azure CLI 2.0](#use-the-azure-cli-20) -如果您已經在 hello 命令列，快速地重設 hello SSH 組態或認證。</span><span class="sxs-lookup"><span data-stu-id="e3988-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="e3988-129">您也可以使用 hello [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="e3988-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="e3988-130">[Azure VMAccessForLinux 延伸模組](#use-the-vmaccess-extension)-建立和重複使用 json 定義檔案 tooreset hello SSH 組態或使用者認證。</span><span class="sxs-lookup"><span data-stu-id="e3988-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="e3988-131">每個疑難排解的步驟之後，請再次嘗試連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="e3988-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="e3988-132">如果仍然無法連線，請嘗試 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="e3988-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="e3988-133">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e3988-133">Use hello Azure portal</span></span>
<span data-ttu-id="e3988-134">hello Azure 入口網站提供快速 tooreset hello SSH 組態或使用者認證不會安裝在本機電腦上的任何工具。</span><span class="sxs-lookup"><span data-stu-id="e3988-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="e3988-135">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e3988-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="e3988-136">捲動 toohello**支援 + 疑難排解**區段，然後選取**重設密碼**如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e3988-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![重設 SSH 組態或 hello Azure 入口網站中的認證](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="e3988-138">重設 hello SSH 設定</span><span class="sxs-lookup"><span data-stu-id="e3988-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="e3988-139">第一個步驟中，選取`Reset configuration only`從 hello**模式**下拉式功能表如在 hello 前面螢幕擷取畫面，然後按一下 [hello**重設**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3988-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="e3988-140">完成此動作後，tooaccess VM 再試一次。</span><span class="sxs-lookup"><span data-stu-id="e3988-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e3988-141">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="e3988-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e3988-142">tooreset hello 認證之現有的使用者，選取 `Reset SSH public key`或`Reset password`從 hello**模式**下拉式選單，如 hello 前面螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="e3988-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="e3988-143">指定 hello 使用者名稱和 SSH 金鑰或新的密碼，然後按一下 [hello**重設**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3988-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="e3988-144">您也可以建立具有 sudo hello VM 從這個功能表上的權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="e3988-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="e3988-145">輸入新的使用者名稱和相關聯的密碼或 SSH 金鑰，然後按一下hello**重設** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3988-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="e3988-146">使用 Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="e3988-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="e3988-147">如果您還沒有這麼做，安裝 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="e3988-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e3988-148">如果您建立及上傳自訂 Linux 磁碟映像時，請確定 hello [Microsoft Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)版本 2.0.5 安裝或更新。</span><span class="sxs-lookup"><span data-stu-id="e3988-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="e3988-149">若為使用資源庫映像建立的 VM，系統已經為您安裝和設定此存取擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e3988-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="e3988-150">重設 SSH 組態</span><span class="sxs-lookup"><span data-stu-id="e3988-150">Reset SSH configuration</span></span>
<span data-ttu-id="e3988-151">您一開始可以再試一次重設 hello SSH 組態 toodefault 值和 hello VM 上的重新開機 hello SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e3988-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="e3988-152">請注意，這不會變更 hello 使用者帳戶名稱、 密碼或 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e3988-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="e3988-153">hello 下列範例會使用[az vm 使用者重設-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH 組態 hello 名為 VM 上的`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-154">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e3988-155">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="e3988-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e3988-156">hello 下列範例會使用[az vm 的使用者更新](/cli/azure/vm/user#update)tooreset hello 認證`myUsername`toohello 值中指定`myPassword`，hello 名為 VM 上`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-157">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="e3988-158">如果使用 SSH 金鑰驗證，您可以重設 hello SSH 金鑰指定的使用者。</span><span class="sxs-lookup"><span data-stu-id="e3988-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="e3988-159">hello 下列範例會使用**az vm 存取設定 linux 使用者**tooupdate hello SSH 金鑰儲存在`~/.ssh/id_rsa.pub`hello 使用者名為`myUsername`，hello 名為 VM 上`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-160">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="e3988-161">使用 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="e3988-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="e3988-162">hello 適用於 Linux VM 存取延伸模組會定義動作 toocarry 出的 json 檔案中讀取。這些動作包括重設 SSHD、重設 SSH 金鑰，或新增使用者。</span><span class="sxs-lookup"><span data-stu-id="e3988-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="e3988-163">您仍然可以使用 hello Azure CLI toocall hello VMAccess 擴充功能，但您可以重複 hello json 檔案使用跨多個 Vm，視。</span><span class="sxs-lookup"><span data-stu-id="e3988-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="e3988-164">這種方法可讓您 toocreate 便可以呼叫的特定案例的 json 檔案的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e3988-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="e3988-165">重設 SSHD</span><span class="sxs-lookup"><span data-stu-id="e3988-165">Reset SSHD</span></span>
<span data-ttu-id="e3988-166">建立名為`settings.json`以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="e3988-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="e3988-167">使用 Azure CLI hello，接著您便呼叫 hello`VMAccessForLinux`延伸 tooreset SSHD 連線藉由指定 json 檔案。</span><span class="sxs-lookup"><span data-stu-id="e3988-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="e3988-168">hello 下列範例會使用[az vm 延伸模組集](/cli/azure/vm/extension#set)tooreset SSHD hello 名為 VM 上的`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-169">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e3988-170">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="e3988-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e3988-171">如果 SSHD 正確出現 toofunction，您可以重設 hello 酬謝使用者認證。</span><span class="sxs-lookup"><span data-stu-id="e3988-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="e3988-172">tooreset hello 密碼的使用者，建立名為`settings.json`。</span><span class="sxs-lookup"><span data-stu-id="e3988-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="e3988-173">hello 下列範例會重設 hello 認證`myUsername`toohello 值中指定`myPassword`。</span><span class="sxs-lookup"><span data-stu-id="e3988-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="e3988-174">輸入下列行至 hello 您`settings.json`檔案，使用您自己的值：</span><span class="sxs-lookup"><span data-stu-id="e3988-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="e3988-175">或 tooreset hello SSH 金鑰的使用者，先建立名為`settings.json`。</span><span class="sxs-lookup"><span data-stu-id="e3988-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="e3988-176">hello 下列範例會重設 hello 認證`myUsername`toohello 值中指定`myPassword`，hello 名為 VM 上`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-177">輸入下列行至 hello 您`settings.json`檔案，使用您自己的值：</span><span class="sxs-lookup"><span data-stu-id="e3988-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="e3988-178">建立 json 檔案之後，使用 hello Azure CLI toocall hello`VMAccessForLinux`延伸 tooreset 藉由指定 json 檔案的 SSH 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="e3988-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="e3988-179">hello 下列範例會重設 hello 名為 VM 上的認證`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-180">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="e3988-181">使用 Azure CLI 1.0 hello</span><span class="sxs-lookup"><span data-stu-id="e3988-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="e3988-182">如果您還沒有這麼做，[安裝 hello Azure CLI 1.0，而且連接 tooyour Azure 訂用帳戶](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="e3988-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="e3988-183">確定您使用的是 Resource Manager 模式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e3988-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e3988-184">如果您建立及上傳自訂 Linux 磁碟映像時，請確定 hello [Microsoft Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)版本 2.0.5 安裝或更新。</span><span class="sxs-lookup"><span data-stu-id="e3988-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="e3988-185">若為使用資源庫映像建立的 VM，系統已經為您安裝和設定此存取擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e3988-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="e3988-186">重設 SSH 組態</span><span class="sxs-lookup"><span data-stu-id="e3988-186">Reset SSH configuration</span></span>
<span data-ttu-id="e3988-187">hello SSHD 設定本身可能設定錯誤或 hello 服務發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e3988-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="e3988-188">您可以重設 SSHD toomake 確定本身 hello SSH 組態有效。</span><span class="sxs-lookup"><span data-stu-id="e3988-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="e3988-189">重設 SSHD 應該是第一個 hello 您需要疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="e3988-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="e3988-190">hello 下列範例會重設名為的 VM 上 SSHD `myVM` hello 資源群組中名為`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e3988-191">使用您自己的 VM 和資源群組名稱，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e3988-192">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="e3988-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e3988-193">如果 SSHD 正確出現 toofunction，您可以重設 hello 酬謝使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="e3988-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="e3988-194">hello 下列範例會重設 hello 認證`myUsername`toohello 值中指定`myPassword`，hello 名為 VM 上`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-195">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="e3988-196">如果使用 SSH 金鑰驗證，您可以重設 hello SSH 金鑰指定的使用者。</span><span class="sxs-lookup"><span data-stu-id="e3988-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="e3988-197">下列範例會更新 hello hello SSH 金鑰儲存在`~/.ssh/id_rsa.pub`hello 使用者名為`myUsername`，hello 名為 VM 上`myVM`中`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e3988-198">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="e3988-199">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="e3988-199">Restart a VM</span></span>
<span data-ttu-id="e3988-200">如果您重設 hello SSH 組態和使用者認證，或發生錯誤，在此情況下，您可以嘗試重新啟動 hello VM tooaddress 基礎計算的問題。</span><span class="sxs-lookup"><span data-stu-id="e3988-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e3988-201">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e3988-201">Azure portal</span></span>
<span data-ttu-id="e3988-202">VM 使用 toorestart hello Azure 入口網站中，選取您的 VM，然後按一下 hello**重新啟動**按鈕如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e3988-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![在 hello Azure 入口網站中重新啟動 VM](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="e3988-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e3988-204">Azure CLI 1.0</span></span>
<span data-ttu-id="e3988-205">下列範例會重新啟動的 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e3988-206">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="e3988-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e3988-207">Azure CLI 2.0</span></span>
<span data-ttu-id="e3988-208">hello 下列範例會使用[az vm 重新啟動](/cli/azure/vm#restart)toorestart hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e3988-209">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="e3988-210">重新部署 VM</span><span class="sxs-lookup"><span data-stu-id="e3988-210">Redeploy a VM</span></span>
<span data-ttu-id="e3988-211">您可以重新部署 VM tooanother 節點在 Azure 中，這可能會修正任何基礎網路問題。</span><span class="sxs-lookup"><span data-stu-id="e3988-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="e3988-212">如需重新部署 VM，請參閱[重新部署 Azure 節點的虛擬機器 toonew](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e3988-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="e3988-213">這項作業完成之後，暫時磁碟資料將會遺失，並將更新與 hello 虛擬機器相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e3988-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="e3988-214">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e3988-214">Azure portal</span></span>
<span data-ttu-id="e3988-215">VM 使用 tooredeploy hello Azure 入口網站中，選取，您的 VM 和捲動 toohello**支援 + 疑難排解**> 一節。</span><span class="sxs-lookup"><span data-stu-id="e3988-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="e3988-216">按一下 hello**重新部署**按鈕如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e3988-216">Click hello **Redeploy** button as in hello following example:</span></span>

![重新部署 hello Azure 入口網站中的 VM](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="e3988-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e3988-218">Azure CLI 1.0</span></span>
<span data-ttu-id="e3988-219">下列範例重新部署的 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e3988-220">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="e3988-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e3988-221">Azure CLI 2.0</span></span>
<span data-ttu-id="e3988-222">下列範例會使用 hello [az vm 重新部署](/cli/azure/vm#redeploy)tooredeploy hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="e3988-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e3988-223">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e3988-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="e3988-224">使用 hello 傳統部署模型所建立的 Vm</span><span class="sxs-lookup"><span data-stu-id="e3988-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="e3988-225">對於使用 hello 傳統部署模型所建立的 Vm，請嘗試這些步驟 tooresolve hello 最常見 SSH 連線失敗。</span><span class="sxs-lookup"><span data-stu-id="e3988-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="e3988-226">每個步驟之後，嘗試重新連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="e3988-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="e3988-227">重設遠端存取從 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e3988-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e3988-228">在 hello Azure 入口網站，選取您的 VM，然後按一下 hello**重設遠端...**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3988-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="e3988-229">重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e3988-229">Restart hello VM.</span></span> <span data-ttu-id="e3988-230">在 [hello [Azure 入口網站](https://portal.azure.com)，選取您的 VM，然後按一下 hello**重新啟動**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3988-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="e3988-231">重新部署 hello VM tooa 新 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="e3988-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="e3988-232">如需有關資訊 tooredeploy VM，請參閱[重新部署 Azure 節點的虛擬機器 toonew](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e3988-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="e3988-233">這項作業完成之後，暫時磁碟資料將會遺失，並將更新與 hello 虛擬機器相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e3988-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="e3988-234">請依照下列中的 hello 指示[如何 tooreset 密碼或 SSH Linux 型虛擬機器](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)至：</span><span class="sxs-lookup"><span data-stu-id="e3988-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="e3988-235">重設 hello 密碼或 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e3988-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="e3988-236">建立 *sudo* 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e3988-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="e3988-237">重設 hello SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="e3988-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="e3988-238">檢查有任何平台問題 hello VM 資源健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e3988-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="e3988-239">選取您的虛擬機器並向下捲動 [設定]  >  [檢查健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="e3988-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3988-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="e3988-240">Additional resources</span></span>
* <span data-ttu-id="e3988-241">如果您仍然無法 tooSSH tooyour VM 之後下列 hello 步驟之後，請參閱[更詳細的疑難排解步驟](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooreview 額外步驟 tooresolve 您的問題。</span><span class="sxs-lookup"><span data-stu-id="e3988-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="e3988-242">如需疑難排解應用程式存取的詳細資訊，請參閱[疑難排解存取 tooan 應用程式在 Azure 虛擬機器上執行](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e3988-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="e3988-243">如需有關如何疑難排解使用 hello 傳統部署模型所建立的虛擬機器的詳細資訊，請參閱[如何 tooreset 密碼或 SSH Linux 型虛擬機器](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e3988-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

