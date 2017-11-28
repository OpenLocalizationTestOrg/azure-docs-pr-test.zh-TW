---
title: "aaaReset hello 密碼或在 Azure 中的 Windows VM 上的遠端桌面組態 |Microsoft 文件"
description: "了解如何使用 hello 傳統部署模型使用的帳戶密碼或 Windows VM 上的遠端桌面服務建立的 tooreset hello Azure 入口網站或 Azure PowerShell。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="4dd12-103">如何 tooreset hello 遠端桌面服務或其登入密碼的 Windows VM 中建立使用 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="4dd12-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4dd12-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="4dd12-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4dd12-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4dd12-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4dd12-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="4dd12-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4dd12-107">您也可以[針對與 hello 資源管理員部署模型所建立的 Vm 執行這些步驟](../reset-rdp.md)。</span><span class="sxs-lookup"><span data-stu-id="4dd12-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="4dd12-108">如果您無法連接 tooa Windows 虛擬機器 (VM)，您可以重設 hello 本機系統管理員密碼，或重設 hello 遠端桌面服務設定。</span><span class="sxs-lookup"><span data-stu-id="4dd12-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="4dd12-109">您可以使用任一 hello Azure 入口網站或 hello VM 存取擴充功能在 Azure PowerShell tooreset hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="4dd12-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="4dd12-110">方式 tooreset 組態或認證</span><span class="sxs-lookup"><span data-stu-id="4dd12-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="4dd12-111">根據您的需求而定，您可以透過數種不同方式來重設遠端桌面服務和認證：</span><span class="sxs-lookup"><span data-stu-id="4dd12-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="4dd12-112">使用 hello Azure 入口網站重設</span><span class="sxs-lookup"><span data-stu-id="4dd12-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="4dd12-113">使用 Azure PowerShell 重設</span><span class="sxs-lookup"><span data-stu-id="4dd12-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="4dd12-114">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4dd12-114">Azure portal</span></span>
<span data-ttu-id="4dd12-115">您可以使用 hello [Azure 入口網站](https://portal.azure.com)tooreset hello 遠端桌面服務。</span><span class="sxs-lookup"><span data-stu-id="4dd12-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="4dd12-116">tooexpand hello 入口網站功能表上，按一下 hello 三條 hello 左上角，然後按一下**虛擬機器 （傳統）**:</span><span class="sxs-lookup"><span data-stu-id="4dd12-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![瀏覽您的 Azure VM](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="4dd12-118">選取您的 Windows 虛擬機器，然後按一下**重設遠端...**。 hello 會出現下列對話方塊 tooreset hello 遠端桌面組態：</span><span class="sxs-lookup"><span data-stu-id="4dd12-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![重設 RDP 組態頁面](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="4dd12-120">您也可以重設 hello 使用者名稱和密碼的 hello 本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="4dd12-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="4dd12-121">從您的 VM，按一下 [支援與疑難排解] > [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="4dd12-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="4dd12-122">hello 密碼重設 刀鋒視窗會顯示：</span><span class="sxs-lookup"><span data-stu-id="4dd12-122">hello password reset blade is displayed:</span></span>

![密碼重設頁面](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="4dd12-124">您輸入 hello 新的使用者名稱和密碼之後，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="4dd12-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="4dd12-125">VMAccess 延伸模組和 PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dd12-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="4dd12-126">請確定 hello hello 虛擬機器安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4dd12-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="4dd12-127">hello VMAccess 擴充功能不需要 toobe 安裝之前，您可以使用它，只要 hello VM 代理程式可用。</span><span class="sxs-lookup"><span data-stu-id="4dd12-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="4dd12-128">請確認已安裝 VM 代理程式使用下列命令的 hello 該 hello。</span><span class="sxs-lookup"><span data-stu-id="4dd12-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="4dd12-129">（取代"myCloudService"和"myVM"hello 您雲端服務名稱及您的 VM，分別。</span><span class="sxs-lookup"><span data-stu-id="4dd12-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="4dd12-130">您可以執行不搭配任何參數的 `Get-AzureVM` 來知道這些名稱)。</span><span class="sxs-lookup"><span data-stu-id="4dd12-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="4dd12-131">如果 hello**寫入主機**命令便會顯示**True**，hello 安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4dd12-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="4dd12-132">如果它顯示**False**，請參閱 hello 指示及在 hello 下載連結 toohello [VM 代理程式和擴充功能-第 2 部分](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409)Azure 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="4dd12-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="4dd12-133">如果您使用 hello 入口網站建立 hello 虛擬機器，請檢查是否`$vm.GetInstance().ProvisionGuestAgent`傳回**True**。</span><span class="sxs-lookup"><span data-stu-id="4dd12-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="4dd12-134">否則，請使用此命令加以設定︰</span><span class="sxs-lookup"><span data-stu-id="4dd12-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="4dd12-135">此命令可防止下列錯誤，如果您執行 hello hello**組 AzureVMExtension**命令 hello 接下來的步驟: 「 佈建客體代理程式上必須啟用 hello VM 物件才能設定 IaaS VM 存取擴充功能。 」</span><span class="sxs-lookup"><span data-stu-id="4dd12-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="4dd12-136">**重設 hello 本機系統管理員帳戶密碼**</span><span class="sxs-lookup"><span data-stu-id="4dd12-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="4dd12-137">建立登入認證與 hello 目前本機系統管理員帳戶名稱和新的密碼，然後再執行 hello `Set-AzureVMAccessExtension` ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4dd12-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="4dd12-138">如果您輸入 hello 目前的帳戶不同的名稱，hello VMAccess 擴充功能就會重新命名 hello 本機系統管理員帳戶、 指派 toothat hello 密碼的帳戶，以及發出登出遠端桌面。Hello 本機系統管理員帳戶已停用，hello VMAccess 擴充功能可讓它。</span><span class="sxs-lookup"><span data-stu-id="4dd12-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="4dd12-139">這些命令也會重設 hello 遠端桌面服務設定。</span><span class="sxs-lookup"><span data-stu-id="4dd12-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="4dd12-140">**重設 hello 遠端桌面服務設定**</span><span class="sxs-lookup"><span data-stu-id="4dd12-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="4dd12-141">tooreset hello 遠端桌面服務組態，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4dd12-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="4dd12-142">hello VMAccess 擴充功能 hello 虛擬機器上執行兩個命令：</span><span class="sxs-lookup"><span data-stu-id="4dd12-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="4dd12-143">此命令會啟用 hello 內建的 Windows 防火牆群組允許連入的遠端桌面流量，會使用 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="4dd12-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="4dd12-144">此命令會設定 hello fDenyTSConnections 登錄值 too0，啟用遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="4dd12-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dd12-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4dd12-145">Next steps</span></span>
<span data-ttu-id="4dd12-146">如果 hello Azure VM 存取擴充功能不會回應並無法 tooreset hello 密碼，您可以[重設 hello 本機 Windows 密碼離線](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4dd12-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="4dd12-147">這個方法是更進階的程序，並要求您 tooconnect hello 虛擬硬碟的問題 VM tooanother hello VM。</span><span class="sxs-lookup"><span data-stu-id="4dd12-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="4dd12-148">首先，本文章中所述步驟 hello 和就只能嘗試 hello 離線密碼重設方法的最後手段。</span><span class="sxs-lookup"><span data-stu-id="4dd12-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="4dd12-149">Azure VM 延伸模組與功能</span><span class="sxs-lookup"><span data-stu-id="4dd12-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="4dd12-150">透過 RDP 或 SSH 連接 tooan Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4dd12-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="4dd12-151">疑難排解遠端桌面連線 tooa windows Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4dd12-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

