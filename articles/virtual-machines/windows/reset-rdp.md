---
title: "重設 Windows VM 上的密碼或遠端桌面組態 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站或 Azure PowerShell 來重設 Windows VM 上的帳戶密碼或「遠端桌面」服務。"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 2e002e3f336422b8fa1eceece889cd083e355a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="bc396-103">如何在 Windows VM 中重設遠端桌面服務或其登入密碼</span><span class="sxs-lookup"><span data-stu-id="bc396-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="bc396-104">如果您無法連線倒 Windows 虛擬機器 (VM)，您可以重設本機系統管理員密碼或重設「遠端桌面」服務組態。</span><span class="sxs-lookup"><span data-stu-id="bc396-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="bc396-105">您可以使用 Azure 入口網站或 Azure PowerShell 中的 VM 存取延伸模組來重設密碼。</span><span class="sxs-lookup"><span data-stu-id="bc396-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="bc396-106">如果您使用的是 PowerShell，請確定您已[安裝並設定最新的 PowerShell 模組](/powershell/azure/overview)，並已登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc396-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="bc396-107">您也可以[針對使用傳統部署模型建立的 VM 執行這些步驟](reset-rdp.md)。</span><span class="sxs-lookup"><span data-stu-id="bc396-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="bc396-108">重設組態或認證的方式</span><span class="sxs-lookup"><span data-stu-id="bc396-108">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="bc396-109">根據您的需求而定，您可以透過數種不同方式來重設遠端桌面服務和認證：</span><span class="sxs-lookup"><span data-stu-id="bc396-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="bc396-110">使用 Azure 入口網站重設</span><span class="sxs-lookup"><span data-stu-id="bc396-110">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="bc396-111">使用 Azure PowerShell 重設</span><span class="sxs-lookup"><span data-stu-id="bc396-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="bc396-112">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bc396-112">Azure portal</span></span>
<span data-ttu-id="bc396-113">若要展開入口網站功能表，請按一下左上角的三個橫條，然後按一下 [虛擬機器]：</span><span class="sxs-lookup"><span data-stu-id="bc396-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![瀏覽您的 Azure VM](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="bc396-115">**重設本機系統管理員帳戶密碼**</span><span class="sxs-lookup"><span data-stu-id="bc396-115">**Reset the local administrator account password**</span></span>

<span data-ttu-id="bc396-116">選取您的 Windows 虛擬機器，然後按一下 [支援與疑難排解] > [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="bc396-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="bc396-117">將會顯示 [密碼重設] 刀鋒視窗︰</span><span class="sxs-lookup"><span data-stu-id="bc396-117">The password reset blade is displayed:</span></span>

![密碼重設頁面](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="bc396-119">輸入使用者名稱和新密碼，然後按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="bc396-119">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="bc396-120">嘗試再次連接到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="bc396-120">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="bc396-121">**重設遠端桌面服務組態**</span><span class="sxs-lookup"><span data-stu-id="bc396-121">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="bc396-122">選取您的 Windows 虛擬機器，然後按一下 [支援與疑難排解] > [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="bc396-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="bc396-123">隨即會顯示 [密碼重設] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bc396-123">The password reset blade is displayed.</span></span> 

![重設 RDP 組態](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="bc396-125">從下拉式功能表中選取 [僅重設設定]，然後按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="bc396-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="bc396-126">嘗試再次連接到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="bc396-126">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="bc396-127">VMAccess 延伸模組和 PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc396-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="bc396-128">請確定您已[安裝並設定最新的 PowerShell 模組](/powershell/azure/overview)，並使用 `Login-AzureRmAccount` Cmdlet 登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc396-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="bc396-129">**重設本機系統管理員帳戶密碼**</span><span class="sxs-lookup"><span data-stu-id="bc396-129">**Reset the local administrator account password**</span></span>
<span data-ttu-id="bc396-130">請使用 [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell Cmdlet，來重設系統管理員密碼或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bc396-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="bc396-131">建立您的帳戶認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bc396-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="bc396-132">如果您輸入與您 VM 上目前本機系統管理員帳戶不同的名稱，則 VMAccess 擴充功能會重新命名本機系統管理員帳戶、將您指定的密碼指派給該帳戶，並發出遠端桌面登出事件。</span><span class="sxs-lookup"><span data-stu-id="bc396-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="bc396-133">如果您 VM 上的本機系統管理員帳戶已停用，則 VMAccess 擴充功能會將它啟用。</span><span class="sxs-lookup"><span data-stu-id="bc396-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="bc396-134">下列範例會將資源群組 `myResourceGroup` 中的 VM `myVM` 更新為指定的認證。</span><span class="sxs-lookup"><span data-stu-id="bc396-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="bc396-135">**重設遠端桌面服務組態**</span><span class="sxs-lookup"><span data-stu-id="bc396-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="bc396-136">使用 [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell Cmdlet，重設對您 VM 的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="bc396-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="bc396-137">下列範例會在資源群組 `myResourceGroup` 中的 VM `myVM` 上重設存取擴充功能 `myVMAccess`：</span><span class="sxs-lookup"><span data-stu-id="bc396-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="bc396-138">不論如何，一部 VM 只能有一個 VM 存取代理程式。</span><span class="sxs-lookup"><span data-stu-id="bc396-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="bc396-139">若要成功設定 VM 存取代理程式屬性，可以使用 `-ForceRerun` 選項。</span><span class="sxs-lookup"><span data-stu-id="bc396-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="bc396-140">使用 `-ForceRerun` 時，請務必使用與任何前述命令中所使用之 VM 存取代理程式相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc396-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="bc396-141">如果您仍然無法從遠端連接虛擬機器，請參閱 [針對以 Windows 為基礎之 Azure 虛擬機器的遠端桌面連線進行疑難排解](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，以取得其他值得一試的步驟。</span><span class="sxs-lookup"><span data-stu-id="bc396-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="bc396-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc396-142">Next steps</span></span>
<span data-ttu-id="bc396-143">如果 Azure VM 存取延伸項目沒有回應，而且您無法重設密碼，可以[離線重設本機 Windows 密碼](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bc396-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="bc396-144">此方法是更進階的程序，會要求您將有問題的 VM 之中的虛擬硬碟連接至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="bc396-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="bc396-145">請先依照這篇文章中說明的步驟進行，並且只在最後無計可施時才嘗試離線密碼重設方法。</span><span class="sxs-lookup"><span data-stu-id="bc396-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="bc396-146">Azure VM 延伸模組與功能</span><span class="sxs-lookup"><span data-stu-id="bc396-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="bc396-147">透過 RDP 或 SSH 連接至 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bc396-147">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="bc396-148">疑難排解以 Windows 為基礎之 Azure 虛擬機器的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="bc396-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

