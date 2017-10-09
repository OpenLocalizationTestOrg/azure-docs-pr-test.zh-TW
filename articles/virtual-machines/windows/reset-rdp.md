---
title: "aaaReset hello 密碼或 Windows VM 上的遠端桌面組態 |Microsoft 文件"
description: "了解如何 tooreset 帳戶密碼或 Windows VM，使用遠端桌面服務 hello Azure 入口網站或 Azure PowerShell。"
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
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="082fb-103">如何 tooreset hello 遠端桌面服務或 Windows VM 中的其登入密碼</span><span class="sxs-lookup"><span data-stu-id="082fb-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="082fb-104">如果您無法連接 tooa Windows 虛擬機器 (VM)，您可以重設 hello 本機系統管理員密碼，或重設 hello 遠端桌面服務設定。</span><span class="sxs-lookup"><span data-stu-id="082fb-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="082fb-105">您可以使用任一 hello Azure 入口網站或 hello VM 存取擴充功能在 Azure PowerShell tooreset hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="082fb-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="082fb-106">如果您使用 PowerShell，請確定您擁有 hello[最新的 PowerShell 模組安裝並設定](/powershell/azure/overview)和登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="082fb-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="082fb-107">您也可以[針對與 hello 傳統部署模型所建立的 Vm 執行這些步驟](reset-rdp.md)。</span><span class="sxs-lookup"><span data-stu-id="082fb-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="082fb-108">方式 tooreset 組態或認證</span><span class="sxs-lookup"><span data-stu-id="082fb-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="082fb-109">根據您的需求而定，您可以透過數種不同方式來重設遠端桌面服務和認證：</span><span class="sxs-lookup"><span data-stu-id="082fb-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="082fb-110">使用 hello Azure 入口網站重設</span><span class="sxs-lookup"><span data-stu-id="082fb-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="082fb-111">使用 Azure PowerShell 重設</span><span class="sxs-lookup"><span data-stu-id="082fb-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="082fb-112">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="082fb-112">Azure portal</span></span>
<span data-ttu-id="082fb-113">tooexpand hello 入口網站功能表上，按一下 hello 三條 hello 左上角，然後按一下**虛擬機器**:</span><span class="sxs-lookup"><span data-stu-id="082fb-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![瀏覽您的 Azure VM](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="082fb-115">**重設 hello 本機系統管理員帳戶密碼**</span><span class="sxs-lookup"><span data-stu-id="082fb-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="082fb-116">選取您的 Windows 虛擬機器，然後按一下 [支援與疑難排解] > [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="082fb-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="082fb-117">hello 密碼重設 刀鋒視窗會顯示：</span><span class="sxs-lookup"><span data-stu-id="082fb-117">hello password reset blade is displayed:</span></span>

![密碼重設頁面](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="082fb-119">輸入 hello 使用者名稱和新的密碼，然後按一下 **更新**。</span><span class="sxs-lookup"><span data-stu-id="082fb-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="082fb-120">請再次嘗試連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="082fb-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="082fb-121">**重設 hello 遠端桌面服務設定**</span><span class="sxs-lookup"><span data-stu-id="082fb-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="082fb-122">選取您的 Windows 虛擬機器，然後按一下 [支援與疑難排解] > [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="082fb-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="082fb-123">hello 密碼重設 刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="082fb-123">hello password reset blade is displayed.</span></span> 

![重設 RDP 組態](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="082fb-125">選取**只能重設組態**從 hello 下拉式選單，然後按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="082fb-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="082fb-126">請再次嘗試連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="082fb-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="082fb-127">VMAccess 延伸模組和 PowerShell</span><span class="sxs-lookup"><span data-stu-id="082fb-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="082fb-128">請確定您擁有 hello[最新的 PowerShell 模組安裝並設定](/powershell/azure/overview)和登入 Azure 訂用帳戶以 hello tooyour `Login-AzureRmAccount` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="082fb-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="082fb-129">**重設 hello 本機系統管理員帳戶密碼**</span><span class="sxs-lookup"><span data-stu-id="082fb-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="082fb-130">重設 hello 系統管理員密碼或使用者名稱與 hello[組 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="082fb-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="082fb-131">建立您的帳戶認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="082fb-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="082fb-132">如果您在 VM 上輸入 hello 目前的本機系統管理員帳戶與不同的名稱，hello VMAccess 擴充功能就會重新命名 hello 本機系統管理員帳戶、 指派您指定的密碼 toothat 的帳戶，以及發出遠端桌面登出事件。</span><span class="sxs-lookup"><span data-stu-id="082fb-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="082fb-133">Hello VM 上的本機系統管理員帳戶已停用，hello VMAccess 擴充功能可讓它。</span><span class="sxs-lookup"><span data-stu-id="082fb-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="082fb-134">下列範例會更新 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`toohello 指定的認證。</span><span class="sxs-lookup"><span data-stu-id="082fb-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="082fb-135">**重設 hello 遠端桌面服務設定**</span><span class="sxs-lookup"><span data-stu-id="082fb-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="082fb-136">重設遠端存取 tooyour VM 以 hello[組 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="082fb-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="082fb-137">hello 下列範例會重設名為 hello 存取延伸`myVMAccess`hello 名為 VM 上`myVM`在 hello`myResourceGroup`資源群組：</span><span class="sxs-lookup"><span data-stu-id="082fb-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="082fb-138">不論如何，一部 VM 只能有一個 VM 存取代理程式。</span><span class="sxs-lookup"><span data-stu-id="082fb-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="082fb-139">tooset hello VM 存取代理程式內容成功，hello`-ForceRerun`選項才能使用。</span><span class="sxs-lookup"><span data-stu-id="082fb-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="082fb-140">當使用`-ForceRerun`，請確定 toouse hello hello VM 存取代理程式在任何先前命令中使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="082fb-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="082fb-141">如果您仍然無法連線遠端 tooyour 虛擬機器，請參閱 < 在多個步驟 tootry[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="082fb-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="082fb-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="082fb-142">Next steps</span></span>
<span data-ttu-id="082fb-143">如果 hello Azure VM 存取擴充功能不會回應並無法 tooreset hello 密碼，您可以[重設 hello 本機 Windows 密碼離線](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="082fb-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="082fb-144">這個方法是更進階的程序，並要求您 tooconnect hello 虛擬硬碟的問題 VM tooanother hello VM。</span><span class="sxs-lookup"><span data-stu-id="082fb-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="082fb-145">首先，本文章中所述步驟 hello 和就只能嘗試 hello 離線密碼重設方法的最後手段。</span><span class="sxs-lookup"><span data-stu-id="082fb-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="082fb-146">Azure VM 延伸模組與功能</span><span class="sxs-lookup"><span data-stu-id="082fb-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="082fb-147">透過 RDP 或 SSH 連接 tooan Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="082fb-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="082fb-148">疑難排解遠端桌面連線 tooa windows Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="082fb-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

