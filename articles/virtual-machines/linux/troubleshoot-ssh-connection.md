---
title: "針對 Azure VM 的 SSH 連線問題進行疑難排解 | Microsoft Docs"
description: "如何針對執行 Linux 的 Azure 虛擬機器進行「SSH 連線失敗」或「SSH 連線被拒」等問題的疑難排解。"
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
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="0b040-104">針對 SSH 連線至 Azure Linux VM 失敗、發生錯誤或被拒進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0b040-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="0b040-105">當您嘗試連接到 Linux 虛擬機器 (VM) 時，有許多原因可能會導致您遇到安全殼層 (SSH) 錯誤、SSH 連線失敗或 SSH 被拒。</span><span class="sxs-lookup"><span data-stu-id="0b040-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="0b040-106">本文可協助您找出原因並加以更正。</span><span class="sxs-lookup"><span data-stu-id="0b040-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="0b040-107">您可以使用 Azure 入口網站、Azure CLI 或適用於 Linux 的 VM 存取擴充功能，針對連線問題進行疑難排解並予以解決。</span><span class="sxs-lookup"><span data-stu-id="0b040-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0b040-108">如果您在本文中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](http://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="0b040-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="0b040-109">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="0b040-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="0b040-110">請移至 [Azure 支援網站](http://azure.microsoft.com/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="0b040-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="0b040-111">如需使用 Azure 支援的資訊，請參閱 [Microsoft Azure 支援常見問題集](http://azure.microsoft.com/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="0b040-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="0b040-112">快速疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="0b040-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="0b040-113">在每個疑難排解步驟完成之後，請嘗試重新連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="0b040-114">重設 SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="0b040-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="0b040-115">重設使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="0b040-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="0b040-116">確認[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)規則允許 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="0b040-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="0b040-117">確定網路安全性群組規則存在，以允許 SSH 流量 (預設為 TCP 連接埠 22)。</span><span class="sxs-lookup"><span data-stu-id="0b040-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="0b040-118">若未使用 Azure 負載平衡器，則無法使用連接埠重新導向 / 對應功能。</span><span class="sxs-lookup"><span data-stu-id="0b040-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="0b040-119">檢查 [VM 資源健康狀態](../../resource-health/resource-health-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0b040-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="0b040-120">確定 VM 回報告為狀況良好。</span><span class="sxs-lookup"><span data-stu-id="0b040-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="0b040-121">如果您已啟用開機診斷，請確認 VM 並未在記錄檔中回報開機錯誤。</span><span class="sxs-lookup"><span data-stu-id="0b040-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="0b040-122">重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-122">Restart the VM.</span></span>
6. <span data-ttu-id="0b040-123">重新部署 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-123">Redeploy the VM.</span></span>

<span data-ttu-id="0b040-124">如需更詳細的疑難排解步驟與說明，請繼續閱讀。</span><span class="sxs-lookup"><span data-stu-id="0b040-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="0b040-125">針對 SSH 連線問題進行疑難排解的可用方法</span><span class="sxs-lookup"><span data-stu-id="0b040-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="0b040-126">您可以使用下列方法之一重設認證或 SSH 組態：</span><span class="sxs-lookup"><span data-stu-id="0b040-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="0b040-127">[Azure 入口網站](#use-the-azure-portal) - 適用於您需要快速重設 SSH 組態或 SSH 金鑰，而且未安裝 Azure 工具時。</span><span class="sxs-lookup"><span data-stu-id="0b040-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="0b040-128">[Azure CLI 2.0](#use-the-azure-cli-20) - 如果您已在命令列上，請快速重設 SSH 組態或認證。</span><span class="sxs-lookup"><span data-stu-id="0b040-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="0b040-129">您也可以使用 [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="0b040-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="0b040-130">[Azure VMAccessForLinux 擴充功能](#use-the-vmaccess-extension) - 建立並重複使用 json 定義檔案，以重設 SSH 組態或使用者認證。</span><span class="sxs-lookup"><span data-stu-id="0b040-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="0b040-131">在每個疑難排解步驟完成之後，請再次嘗試連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="0b040-132">如果仍然無法連線，請嘗試下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="0b040-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="0b040-133">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0b040-133">Use the Azure portal</span></span>
<span data-ttu-id="0b040-134">Azure 入口網站可供快速重設 SSH 組態或使用者認證，而不需在本機電腦上安裝任何工具。</span><span class="sxs-lookup"><span data-stu-id="0b040-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="0b040-135">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="0b040-136">向下捲動至 [支援 + 疑難排解] 區段，然後選取 [重設密碼]，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![在 Azure 入口網站中重設 SSH 組態或認證](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="0b040-138">重設 SSH 組態</span><span class="sxs-lookup"><span data-stu-id="0b040-138">Reset the SSH configuration</span></span>
<span data-ttu-id="0b040-139">第一個步驟，從 [模式] 下拉式功能表中選取 `Reset configuration only` (如前面的螢幕擷取畫面所示)，然後按一下 [重設] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b040-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="0b040-140">完成此動作後，嘗試再次存取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="0b040-141">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="0b040-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="0b040-142">若要重設現有使用者的認證，請從 模式 下拉式功能表中選取  `Reset SSH public key` 或 `Reset password`，如前面的螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="0b040-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="0b040-143">指定使用者名稱和 SSH 金鑰或新的密碼，然後按一下 [重設] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b040-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="0b040-144">您也可以經由此功能表，在此 VM 上建立具備 sudo 權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="0b040-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="0b040-145">輸入新的使用者名稱和相關聯的密碼或 SSH 金鑰，然後按一下 [重設] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b040-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="0b040-146">使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0b040-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="0b040-147">如果尚未安裝，請安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b040-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0b040-148">如果您已建立並上傳自訂 Linux 磁碟映像，請確定已安裝 [Microsoft Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 2.0.5 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0b040-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="0b040-149">若為使用資源庫映像建立的 VM，系統已經為您安裝和設定此存取擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0b040-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="0b040-150">重設 SSH 組態</span><span class="sxs-lookup"><span data-stu-id="0b040-150">Reset SSH configuration</span></span>
<span data-ttu-id="0b040-151">您可以一開始先嘗試將 SSH 組態重設為預設值，然後將虛擬機器上的 SSH 伺服器重新開機。</span><span class="sxs-lookup"><span data-stu-id="0b040-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="0b040-152">請注意，這不會變更使用者帳戶名稱、密碼或 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b040-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="0b040-153">下列範例會使用 [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh)，在 `myResourceGroup` 中名為 `myVM` 的虛擬機器上重設 SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="0b040-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-154">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="0b040-155">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="0b040-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="0b040-156">下列範例會使用 [az vm user update](/cli/azure/vm/user#update)，在 `myResourceGroup` 中名為 `myVM` 的虛擬機器上，將 `myUsername` 的認證重設為 `myPassword` 中指定的值。</span><span class="sxs-lookup"><span data-stu-id="0b040-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-157">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="0b040-158">如果使用 SSH 金鑰驗證，您可以針對指定的使用者重設 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b040-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="0b040-159">下列範例會使用 **az vm access set-linux-user**，在 `myResourceGroup` 中名為 `myVM` 的 VM 上，針對名為 `myUsername` 的使用者更新儲存在 `~/.ssh/id_rsa.pub` 中的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b040-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-160">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="0b040-161">使用 VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="0b040-161">Use the VMAccess extension</span></span>
<span data-ttu-id="0b040-162">適用於 Linux 的 VM 存取擴充功能會讀入 json 檔案，該檔案會定義所要執行的動作。這些動作包括重設 SSHD、重設 SSH 金鑰，或新增使用者。</span><span class="sxs-lookup"><span data-stu-id="0b040-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="0b040-163">您仍可使用 Azure CLI 來呼叫 VMAccess 擴充功能，但您可以視需要將 json 檔案重複使用於多個 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="0b040-164">這種方法可讓您建立 json 檔案的儲存機制，以便之後針對特定案例進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="0b040-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="0b040-165">重設 SSHD</span><span class="sxs-lookup"><span data-stu-id="0b040-165">Reset SSHD</span></span>
<span data-ttu-id="0b040-166">使用下列內容，建立名為 `settings.json` 的檔案︰</span><span class="sxs-lookup"><span data-stu-id="0b040-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="0b040-167">使用 Azure CLI，接著呼叫 `VMAccessForLinux` 擴充功能，藉由指定 json 檔案來重設 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="0b040-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="0b040-168">下列範例會使用 [az vm extension set](/cli/azure/vm/extension#set)，在 `myResourceGroup` 中名為 `myVM` 的虛擬機器上重設 SSHD。</span><span class="sxs-lookup"><span data-stu-id="0b040-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-169">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="0b040-170">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="0b040-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="0b040-171">如果 SSHD 似乎能正常運作，您可以針對指定的使用者重設認證。</span><span class="sxs-lookup"><span data-stu-id="0b040-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="0b040-172">若要重設使用者的密碼，請建立名為 `settings.json` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="0b040-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="0b040-173">下列範例會將 `myUsername` 的認證重設為在 `myPassword` 中指定的值。</span><span class="sxs-lookup"><span data-stu-id="0b040-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="0b040-174">使用您自己的值，將下列幾行程式碼輸入到 `settings.json` 檔案中︰</span><span class="sxs-lookup"><span data-stu-id="0b040-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="0b040-175">或者，若要重設使用者的 SSH 金鑰，請先建立名為 `settings.json` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="0b040-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="0b040-176">下列範例會在 `myResourceGroup` 中名為 `myVM` 的 VM 上，將 `myUsername` 的認證重設為在 `myPassword` 中指定的值。</span><span class="sxs-lookup"><span data-stu-id="0b040-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-177">使用您自己的值，將下列幾行程式碼輸入到 `settings.json` 檔案中︰</span><span class="sxs-lookup"><span data-stu-id="0b040-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="0b040-178">建立 json 檔案之後，使用 Azure CLI 來呼叫 `VMAccessForLinux` 擴充功能，藉由指定 json 檔案來重設 SSH 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="0b040-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="0b040-179">下列範例會在 `myResourceGroup` 中名為 `myVM` 的 VM 上重設認證。</span><span class="sxs-lookup"><span data-stu-id="0b040-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-180">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="0b040-181">使用 Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b040-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="0b040-182">如果尚未安裝，請 [安裝 Azure CLI 1.0 並連線至您的 Azure 訂用帳戶](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="0b040-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="0b040-183">確定您使用的是 Resource Manager 模式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0b040-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="0b040-184">如果您已建立並上傳自訂 Linux 磁碟映像，請確定已安裝 [Microsoft Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 2.0.5 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0b040-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="0b040-185">若為使用資源庫映像建立的 VM，系統已經為您安裝和設定此存取擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0b040-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="0b040-186">重設 SSH 組態</span><span class="sxs-lookup"><span data-stu-id="0b040-186">Reset SSH configuration</span></span>
<span data-ttu-id="0b040-187">SSHD 組態本身可能設定錯誤，或服務發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="0b040-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="0b040-188">您可以重設 SSH 以確定 SSH 組態本身有效。</span><span class="sxs-lookup"><span data-stu-id="0b040-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="0b040-189">重設 SSHD 應該是您所採取的第一個疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="0b040-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="0b040-190">下列範例會在名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM 上重設 SSHD。</span><span class="sxs-lookup"><span data-stu-id="0b040-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="0b040-191">使用您自己的 VM 和資源群組名稱，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="0b040-192">重設使用者的 SSH 認證</span><span class="sxs-lookup"><span data-stu-id="0b040-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="0b040-193">如果 SSHD 似乎能正常運作，您可以針對指定的使用者重設密碼。</span><span class="sxs-lookup"><span data-stu-id="0b040-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="0b040-194">下列範例會在 `myResourceGroup` 中名為 `myVM` 的 VM 上，將 `myUsername` 的認證重設為在 `myPassword` 中指定的值。</span><span class="sxs-lookup"><span data-stu-id="0b040-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-195">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="0b040-196">如果使用 SSH 金鑰驗證，您可以針對指定的使用者重設 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b040-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="0b040-197">下列範例會在 `myResourceGroup` 中名為 `myVM` 的 VM 上，針對名為 `myUsername` 的使用者，更新 `~/.ssh/id_rsa.pub` 中儲存的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b040-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="0b040-198">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="0b040-199">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="0b040-199">Restart a VM</span></span>
<span data-ttu-id="0b040-200">如果您重設 SSH 組態和使用者認證，或在執行此作業時發生錯誤，您可以嘗試重新啟動 VM 以處理基礎計算問題。</span><span class="sxs-lookup"><span data-stu-id="0b040-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="0b040-201">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0b040-201">Azure portal</span></span>
<span data-ttu-id="0b040-202">若要使用 Azure 入口網站來重新啟動 VM，請選取您的 VM，然後按一下 [重新啟動] 按鈕，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![在 Azure 入口網站中重新啟動 VM](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="0b040-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b040-204">Azure CLI 1.0</span></span>
<span data-ttu-id="0b040-205">下列範例會重新啟動名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="0b040-206">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="0b040-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0b040-207">Azure CLI 2.0</span></span>
<span data-ttu-id="0b040-208">下列範例會使用 [az vm restart](/cli/azure/vm#restart) 來重新啟動名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="0b040-209">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="0b040-210">重新部署 VM</span><span class="sxs-lookup"><span data-stu-id="0b040-210">Redeploy a VM</span></span>
<span data-ttu-id="0b040-211">您可以將 VM 重新部署到 Azure 中的另一個節點，這可能會修正任何的基礎網路問題。</span><span class="sxs-lookup"><span data-stu-id="0b040-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="0b040-212">如需重新部署 VM 的相關資訊，請參閱[將虛擬機器重新部署至新的 Azure 節點](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0b040-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="0b040-213">此作業完成之後，暫時磁碟機資料將會遺失，且將會更新與虛擬機器相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0b040-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="0b040-214">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0b040-214">Azure portal</span></span>
<span data-ttu-id="0b040-215">若要使用 Azure 入口網站重新部署 VM，請選取您的 VM 並向下捲動至 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="0b040-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="0b040-216">按一下 [重新部署] 按鈕，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-216">Click the **Redeploy** button as in the following example:</span></span>

![在 Azure 入口網站中重新部署 VM](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="0b040-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b040-218">Azure CLI 1.0</span></span>
<span data-ttu-id="0b040-219">下列範例會重新部署名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="0b040-220">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="0b040-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0b040-221">Azure CLI 2.0</span></span>
<span data-ttu-id="0b040-222">下列範例會使用 [az vm redeploy](/cli/azure/vm#redeploy) 來重新部署名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="0b040-223">使用您自己的值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0b040-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="0b040-224">使用傳統部署模型建立的 VM</span><span class="sxs-lookup"><span data-stu-id="0b040-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="0b040-225">請嘗試下列步驟，來解決使用傳統部署模型所建立之 VM 中最常見的 SSH 連線失敗。</span><span class="sxs-lookup"><span data-stu-id="0b040-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="0b040-226">在每個步驟完成後，請嘗試重新連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="0b040-227">透過 [Azure 入口網站](https://portal.azure.com)，重設遠端存取。</span><span class="sxs-lookup"><span data-stu-id="0b040-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0b040-228">在 Azure 入口網站上選取您的 VM，然後按一下 [重設遠端...] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b040-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="0b040-229">重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="0b040-229">Restart the VM.</span></span> <span data-ttu-id="0b040-230">在 [Azure 入口網站](https://portal.azure.com)上選取您的 VM，然後按一下 [重新啟動] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b040-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="0b040-231">將 VM 重新部署到新的 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="0b040-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="0b040-232">如需如何重新部署 VM 的資訊，請參閱[將虛擬機器重新部署至新的 Azure 節點](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0b040-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="0b040-233">此作業完成之後，暫時磁碟機資料將會遺失，且將會更新與虛擬機器相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0b040-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="0b040-234">請依循[如何為 Linux 虛擬機器重設密碼或 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 中的指示進行，以：</span><span class="sxs-lookup"><span data-stu-id="0b040-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="0b040-235">重設密碼或 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b040-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="0b040-236">建立 *sudo* 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b040-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="0b040-237">重設 SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="0b040-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="0b040-238">檢查 VM 的資源健康狀態是否有任何平台問題。</span><span class="sxs-lookup"><span data-stu-id="0b040-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="0b040-239">選取您的虛擬機器並向下捲動 [設定]  >  [檢查健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="0b040-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b040-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="0b040-240">Additional resources</span></span>
* <span data-ttu-id="0b040-241">如果在依循這些步驟之後仍無法以 SSH 連線到您的 VM，請參閱[更詳細的疑難排解步驟](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)以檢閱其他的步驟來解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="0b040-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="0b040-242">如需疑難排解應用程式存取的詳細資訊，請參閱[針對存取在 Azure 虛擬機器上執行的應用程式進行疑難排解](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0b040-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="0b040-243">如需針對使用傳統部署模型所建立之虛擬機器進行疑難排解的詳細資訊，請參閱[如何為 Linux 虛擬機器重設密碼或 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0b040-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>
