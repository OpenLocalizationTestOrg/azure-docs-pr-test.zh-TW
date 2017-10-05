---
title: "不使用 Azure 代理程式重設本機 Windows 密碼 | Microsoft Docs"
description: "在 Azure 客體代理程式未安裝或運作於 VM 的情況下，如何重設本機 Windows 使用者帳戶的密碼"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: 880f5e5967298401fc2522124af3746d9906ffa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-windows-password-for-azure-vm"></a><span data-ttu-id="059d9-103">如何重設 Azure VM 的本機 Windows 密碼</span><span class="sxs-lookup"><span data-stu-id="059d9-103">How to reset local Windows password for Azure VM</span></span>
<span data-ttu-id="059d9-104">您可以使用 [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 在 Azure 中重設 VM 的本機 Windows 密碼 (假設已安裝 Azure 客體代理程式)。</span><span class="sxs-lookup"><span data-stu-id="059d9-104">You can reset the local Windows password of a VM in Azure using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided the Azure guest agent is installed.</span></span> <span data-ttu-id="059d9-105">這個方法是為 Azure VM 重設密碼的主要方式。</span><span class="sxs-lookup"><span data-stu-id="059d9-105">This method is the primary way to reset a password for an Azure VM.</span></span> <span data-ttu-id="059d9-106">如果您遇到 Azure 客體代理程式沒有回應，或無法在上傳自訂映像後進行安裝等問題，您可以手動重設 Windows 密碼。</span><span class="sxs-lookup"><span data-stu-id="059d9-106">If you encounter issues with the Azure guest agent not responding, or failing to install after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="059d9-107">本文將詳細說明如何將來源 OS 虛擬磁碟連接至另一部 VM，以重設本機帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="059d9-107">This article details how to reset a local account password by attaching the source OS virtual disk to another VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="059d9-108">只能使用此程序做為最後手段。</span><span class="sxs-lookup"><span data-stu-id="059d9-108">Only use this process as a last resort.</span></span> <span data-ttu-id="059d9-109">一律先嘗試使用 [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 重設密碼。</span><span class="sxs-lookup"><span data-stu-id="059d9-109">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-the-process"></a><span data-ttu-id="059d9-110">程序概觀</span><span class="sxs-lookup"><span data-stu-id="059d9-110">Overview of the process</span></span>
<span data-ttu-id="059d9-111">無法存取 Azure 客體代理程式時，在 Azure 中為 Windows VM 執行本機密碼重設的核心步驟如下所示︰</span><span class="sxs-lookup"><span data-stu-id="059d9-111">The core steps for performing a local password reset for a Windows VM in Azure when there is no access to the Azure guest agent is as follows:</span></span>

* <span data-ttu-id="059d9-112">刪除來源 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-112">Delete the source VM.</span></span> <span data-ttu-id="059d9-113">虛擬磁碟會保留下來。</span><span class="sxs-lookup"><span data-stu-id="059d9-113">The virtual disks are retained.</span></span>
* <span data-ttu-id="059d9-114">將來源 VM 的 OS 磁碟連接到 Azure 訂用帳戶內位於相同位置的另一部 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-114">Attach the source VM's OS disk to another VM on the same location within your Azure subscription.</span></span> <span data-ttu-id="059d9-115">此 VM 也稱為疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-115">This VM is referred to as the troubleshooting VM.</span></span>
* <span data-ttu-id="059d9-116">使用疑難排解 VM，在來源 VM 的 OS 磁碟上建立一些組態檔。</span><span class="sxs-lookup"><span data-stu-id="059d9-116">Using the troubleshooting VM, create some config files on the source VM's OS disk.</span></span>
* <span data-ttu-id="059d9-117">從疑難排解 VM 卸離 VM 的 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="059d9-117">Detach the VM's OS disk from the troubleshooting VM.</span></span>
* <span data-ttu-id="059d9-118">使用原始虛擬磁碟，透過 Resource Manager 範本建立 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-118">Use a Resource Manager template to create a VM, using the original virtual disk.</span></span>
* <span data-ttu-id="059d9-119">當新的 VM 開機時，您建立的組態檔會更新所需使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="059d9-119">When the new VM boots, the config files you create update the password of the required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="059d9-120">詳細步驟</span><span class="sxs-lookup"><span data-stu-id="059d9-120">Detailed steps</span></span>
<span data-ttu-id="059d9-121">一律先嘗試使用 [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 重設密碼，再嘗試下列步驟。</span><span class="sxs-lookup"><span data-stu-id="059d9-121">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying the following steps.</span></span> <span data-ttu-id="059d9-122">在開始之前，確定您有 VM 的備份。</span><span class="sxs-lookup"><span data-stu-id="059d9-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="059d9-123">在 Azure 入口網站中刪除受影響的 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-123">Delete the affected VM in Azure portal.</span></span> <span data-ttu-id="059d9-124">刪除 VM 只會刪除中繼資料 (Azure 內 VM 的參考)。</span><span class="sxs-lookup"><span data-stu-id="059d9-124">Deleting the VM only deletes the metadata, the reference of the VM within Azure.</span></span> <span data-ttu-id="059d9-125">刪除 VM 時會保留虛擬磁碟：</span><span class="sxs-lookup"><span data-stu-id="059d9-125">The virtual disks are retained when the VM is deleted:</span></span>
   
   * <span data-ttu-id="059d9-126">在 Azure 入口網站中選取 VM，請按一下 [刪除]：</span><span class="sxs-lookup"><span data-stu-id="059d9-126">Select the VM in the Azure portal, click *Delete*:</span></span>
     
     ![刪除現有的 VM](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="059d9-128">將來源 VM 的 OS 磁碟連接到疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-128">Attach the source VM’s OS disk to the troubleshooting VM.</span></span> <span data-ttu-id="059d9-129">疑難排解 VM 必須位於與來源 VM 的作業系統磁碟相同的區域 (例如 `West US`)：</span><span class="sxs-lookup"><span data-stu-id="059d9-129">The troubleshooting VM must be in the same region as the source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="059d9-130">在 Azure 入口網站中選取疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-130">Select the troubleshooting VM in the Azure portal.</span></span> <span data-ttu-id="059d9-131">按一下 [磁碟] | [連接現有項目]：</span><span class="sxs-lookup"><span data-stu-id="059d9-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![連接現有磁碟](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="059d9-133">選取 [VHD 檔案]，然後選取包含來源 VM 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="059d9-133">Select *VHD File* and then select the storage account that contains your source VM:</span></span>
     
     ![選取儲存體帳戶](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="059d9-135">選取來源容器。</span><span class="sxs-lookup"><span data-stu-id="059d9-135">Select the source container.</span></span> <span data-ttu-id="059d9-136">來源容器通常是 vhd：</span><span class="sxs-lookup"><span data-stu-id="059d9-136">The source container is typically *vhds*:</span></span>
     
     ![選取儲存體容器](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="059d9-138">選取要連接的 OS vhd。</span><span class="sxs-lookup"><span data-stu-id="059d9-138">Select the OS vhd to attach.</span></span> <span data-ttu-id="059d9-139">按一下 [選取]，完成此程序：</span><span class="sxs-lookup"><span data-stu-id="059d9-139">Click *Select* to complete the process:</span></span>
     
     ![選取來源虛擬磁碟](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="059d9-141">使用遠端桌面連接到疑難排解 VM，並確定看得見來源 VM 的 OS 磁碟︰</span><span class="sxs-lookup"><span data-stu-id="059d9-141">Connect to the troubleshooting VM using Remote Desktop and ensure the source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="059d9-142">在 Azure 入口網站中選取疑難排解 VM，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="059d9-142">Select the troubleshooting VM in the Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="059d9-143">開啟下載的 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="059d9-143">Open the RDP file that downloads.</span></span> <span data-ttu-id="059d9-144">輸入疑難排解 VM 的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="059d9-144">Enter the username and password of the troubleshooting VM.</span></span>
   * <span data-ttu-id="059d9-145">在檔案總管中，尋找您所連接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="059d9-145">In File Explorer, look for the data disk you attached.</span></span> <span data-ttu-id="059d9-146">如果來源 VM 的 VHD 是連接到疑難排解 VM 的唯一資料磁碟，則應該是 F: 磁碟機︰</span><span class="sxs-lookup"><span data-stu-id="059d9-146">If the source VM’s VHD is the only data disk attached to the troubleshooting VM, it should be the F: drive:</span></span>
     
     ![檢視連接的資料磁碟](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="059d9-148">在來源 VM 磁碟機的 `\Windows\System32\GroupPolicy` 中建立 `gpt.ini` (如果存在 gpt.ini，請將它重新命名為 gpt.ini.bak)︰</span><span class="sxs-lookup"><span data-stu-id="059d9-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on the source VM’s drive (if gpt.ini exists, rename to gpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="059d9-149">確保您不會在 C:\Windows (疑難排解 VM 的 OS 磁碟機) 中不小心建立下列檔案。</span><span class="sxs-lookup"><span data-stu-id="059d9-149">Make sure that you do not accidentally create the following files in C:\Windows, the OS drive for the troubleshooting VM.</span></span> <span data-ttu-id="059d9-150">在連接成為資料磁碟的來源 VM OS 磁碟機中建立下列檔案。</span><span class="sxs-lookup"><span data-stu-id="059d9-150">Create the following files in the OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="059d9-151">將下列幾行新增至您建立的 `gpt.ini` 檔案：</span><span class="sxs-lookup"><span data-stu-id="059d9-151">Add the following lines into the `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![建立 gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="059d9-153">在 `\Windows\System32\GroupPolicy\Machine\Scripts` 中建立 `scripts.ini`。</span><span class="sxs-lookup"><span data-stu-id="059d9-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="059d9-154">確定已顯示隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="059d9-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="059d9-155">如有需要，請建立 `Machine` 或 `Scripts` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="059d9-155">If needed, create the `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="059d9-156">將下列幾行新增至您建立的 `scripts.ini` 檔案：</span><span class="sxs-lookup"><span data-stu-id="059d9-156">Add the following lines the `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![建立 scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="059d9-158">使用下列內容在 `\Windows\System32` 中建立 `FixAzureVM.cmd`，並以您自己的值取代 `<username>` 和 `<newpassword>`：</span><span class="sxs-lookup"><span data-stu-id="059d9-158">Create `FixAzureVM.cmd` in `\Windows\System32` with the following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![建立 FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="059d9-160">定義新的密碼時，必須符合針對 VM 設定的密碼複雜性需求。</span><span class="sxs-lookup"><span data-stu-id="059d9-160">You must meet the configured password complexity requirements for your VM when defining the new password.</span></span>
7. <span data-ttu-id="059d9-161">在 Azure 入口網站中，從疑難排解 VM 卸離磁碟：</span><span class="sxs-lookup"><span data-stu-id="059d9-161">In Azure portal, detach the disk from the troubleshooting VM:</span></span>
   
   * <span data-ttu-id="059d9-162">在 Azure 入口網站中選取疑難排解 VM，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="059d9-162">Select the troubleshooting VM in the Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="059d9-163">選取在步驟 2 中連接的資料磁碟，按一下 [卸離]：</span><span class="sxs-lookup"><span data-stu-id="059d9-163">Select the data disk attached in step 2, click *Detach*:</span></span>
     
     ![卸離磁碟](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="059d9-165">建立 VM 之前，取得來源 OS 磁碟的 URI：</span><span class="sxs-lookup"><span data-stu-id="059d9-165">Before you create a VM, obtain the URI to your source OS disk:</span></span>
   
   * <span data-ttu-id="059d9-166">在 Azure 入口網站中選取儲存體帳戶，按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="059d9-166">Select the storage account in the Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="059d9-167">選取容器。</span><span class="sxs-lookup"><span data-stu-id="059d9-167">Select the container.</span></span> <span data-ttu-id="059d9-168">來源容器通常是 vhd：</span><span class="sxs-lookup"><span data-stu-id="059d9-168">The source container is typically *vhds*:</span></span>
     
     ![選取儲存體帳戶 Blob](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="059d9-170">選取您的來源 VM OS VHD，然後按一下 [URL] 名稱旁邊的 [複製] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="059d9-170">Select your source VM OS VHD and click the *Copy* button next to the *URL* name:</span></span>
     
     ![複製磁碟 URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="059d9-172">從來源 VM 的 OS 磁碟建立 VM：</span><span class="sxs-lookup"><span data-stu-id="059d9-172">Create a VM from the source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="059d9-173">使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)，從特定的 VHD 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) to create a VM from a specialized VHD.</span></span> <span data-ttu-id="059d9-174">按一下 `Deploy to Azure` 按鈕開啟 Azure 入口網站，其中包含為您填入的樣板化詳細資料。</span><span class="sxs-lookup"><span data-stu-id="059d9-174">Click the `Deploy to Azure` button to open the Azure portal with the templated details populated for you.</span></span>
   * <span data-ttu-id="059d9-175">如果您想要保留 VM 的所有先前設定，請選取 [編輯範本] 以提供現有的 VNet、子網路、網路介面卡或公用 IP。</span><span class="sxs-lookup"><span data-stu-id="059d9-175">If you want to retain all the previous settings for the VM, select *Edit template* to provide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="059d9-176">在 `OSDISKVHDURI` 參數文字方塊中，貼上您在前一個步驟中取得的來源 VHD URI︰</span><span class="sxs-lookup"><span data-stu-id="059d9-176">In the `OSDISKVHDURI` parameter text box, paste the URI of your source VHD obtain in the preceding step:</span></span>
     
     ![從範本建立 VM](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="059d9-178">執行新的 VM 後，使用您在 `FixAzureVM.cmd` 指令碼指定中的新密碼，透過遠端桌面連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="059d9-178">After the new VM is running, connect to the VM using Remote Desktop with the new password you specified in the `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="059d9-179">從新 VM 的遠端工作階段，移除下列檔案以清理環境︰</span><span class="sxs-lookup"><span data-stu-id="059d9-179">From your remote session to the new VM, remove the following files to clean up the environment:</span></span>
    
    * <span data-ttu-id="059d9-180">從 %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="059d9-180">From %windir%\System32</span></span>
      * <span data-ttu-id="059d9-181">移除 FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="059d9-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="059d9-182">從 %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="059d9-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="059d9-183">移除 scripts.ini</span><span class="sxs-lookup"><span data-stu-id="059d9-183">remove scripts.ini</span></span>
    * <span data-ttu-id="059d9-184">從 %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="059d9-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="059d9-185">移除 gpt.ini (如果 gpt.ini 早已存在，且您已將它重新命名為 gpt.ini.bak，請將此 .bak 檔案重新命名為 gpt.ini)</span><span class="sxs-lookup"><span data-stu-id="059d9-185">remove gpt.ini (if gpt.ini existed before, and you renamed it to gpt.ini.bak, rename the .bak file back to gpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="059d9-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="059d9-186">Next steps</span></span>
<span data-ttu-id="059d9-187">如果您仍然無法使用遠端桌面進行連接，請參閱 [RDP 疑難排解指南](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="059d9-187">If you still cannot connect using Remote Desktop, see the [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="059d9-188">[詳細的 RDP 疑難排解指南](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)會探討疑難排解方法，而不是特定的步驟。</span><span class="sxs-lookup"><span data-stu-id="059d9-188">The [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="059d9-189">您也可以[開啟 Azure 支援要求](https://azure.microsoft.com/support/options/)，以取得實際操作協助。</span><span class="sxs-lookup"><span data-stu-id="059d9-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

