---
title: "沒有 Azure 代理程式的本機 Windows 密碼 aaaReset |Microsoft 文件"
description: "如何 tooreset hello 與本機 Windows 使用者帳戶的密碼時 hello Azure 客體代理程式未安裝或在 VM 上正常運作"
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
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="0f434-103">如何 tooreset 本機 Windows 密碼做為 Azure VM</span><span class="sxs-lookup"><span data-stu-id="0f434-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="0f434-104">您可以使用 hello 在 Azure 中 VM 的 hello 本機 Windows 密碼重設[Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)提供 hello Azure 客體代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="0f434-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="0f434-105">這個方法是 hello 主要方式 tooreset Azure VM 的密碼。</span><span class="sxs-lookup"><span data-stu-id="0f434-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="0f434-106">如果您使用 hello Azure 客體代理程式沒有回應，或上傳自訂映像之後失敗 tooinstall 遇到問題，您可以手動重設 Windows 密碼。</span><span class="sxs-lookup"><span data-stu-id="0f434-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="0f434-107">這篇文章說明如何藉由附加的本機帳戶密碼 tooreset hello 來源 OS 虛擬磁碟 tooanother VM。</span><span class="sxs-lookup"><span data-stu-id="0f434-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="0f434-108">只能使用此程序做為最後手段。</span><span class="sxs-lookup"><span data-stu-id="0f434-108">Only use this process as a last resort.</span></span> <span data-ttu-id="0f434-109">永遠嘗試使用 hello 密碼 tooreset [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)第一次。</span><span class="sxs-lookup"><span data-stu-id="0f434-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="0f434-110">Hello 程序概觀</span><span class="sxs-lookup"><span data-stu-id="0f434-110">Overview of hello process</span></span>
<span data-ttu-id="0f434-111">執行本機密碼，沒有存取 toohello Azure 客體代理程式時，針對 Windows VM 在 Azure 中重設 hello 核心步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="0f434-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="0f434-112">刪除 hello 來源 VM。</span><span class="sxs-lookup"><span data-stu-id="0f434-112">Delete hello source VM.</span></span> <span data-ttu-id="0f434-113">hello 虛擬磁碟會保留。</span><span class="sxs-lookup"><span data-stu-id="0f434-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="0f434-114">附加 hello 來源 VM 之 OS 磁碟 tooanother VM 上 hello Azure 訂用帳戶內的相同位置。</span><span class="sxs-lookup"><span data-stu-id="0f434-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="0f434-115">此 VM 是參照的 tooas hello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="0f434-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="0f434-116">使用 hello 疑難排解 VM 建立 hello 來源 VM 之 OS 磁碟上的某些組態檔。</span><span class="sxs-lookup"><span data-stu-id="0f434-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="0f434-117">卸離 hello 疑難排解 VM 中的 hello VM 之 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="0f434-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="0f434-118">使用資源管理員範本 toocreate 使用 hello 原始虛擬磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="0f434-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="0f434-119">當 hello 新 VM 馮鰹氶 a hello 設定檔會建立所需的 hello 使用者更新 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0f434-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="0f434-120">詳細步驟</span><span class="sxs-lookup"><span data-stu-id="0f434-120">Detailed steps</span></span>
<span data-ttu-id="0f434-121">永遠嘗試使用 hello 密碼 tooreset [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)之前嘗試 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="0f434-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="0f434-122">在開始之前，確定您有 VM 的備份。</span><span class="sxs-lookup"><span data-stu-id="0f434-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="0f434-123">刪除 hello 影響 VM 在 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0f434-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="0f434-124">正在刪除 hello VM 只會刪除 hello hello VM 在 Azure 中的 hello 參考中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0f434-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="0f434-125">hello VM 刪除時，會保留 hello 虛擬磁碟：</span><span class="sxs-lookup"><span data-stu-id="0f434-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="0f434-126">選取 hello VM hello Azure 入口網站中的按一下*刪除*:</span><span class="sxs-lookup"><span data-stu-id="0f434-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![刪除現有的 VM](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="0f434-128">附加 hello 來源 VM 之 OS 磁碟 toohello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="0f434-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="0f434-129">hello 疑難排解 VM 必須在 hello 與 hello 來源 VM 之 OS 磁碟相同的區域 (例如`West US`):</span><span class="sxs-lookup"><span data-stu-id="0f434-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="0f434-130">選取 VM 疑難排解 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f434-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="0f434-131">按一下 [磁碟] | [連接現有項目]：</span><span class="sxs-lookup"><span data-stu-id="0f434-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![連接現有磁碟](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="0f434-133">選取*VHD 檔案*，然後選取包含您的來源 VM 的 hello 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="0f434-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![選取儲存體帳戶](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="0f434-135">選取 hello 來源容器。</span><span class="sxs-lookup"><span data-stu-id="0f434-135">Select hello source container.</span></span> <span data-ttu-id="0f434-136">hello 來源容器是通常*vhd*:</span><span class="sxs-lookup"><span data-stu-id="0f434-136">hello source container is typically *vhds*:</span></span>
     
     ![選取儲存體容器](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="0f434-138">選取 hello OS vhd tooattach。</span><span class="sxs-lookup"><span data-stu-id="0f434-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="0f434-139">按一下*選取*toocomplete hello 程序：</span><span class="sxs-lookup"><span data-stu-id="0f434-139">Click *Select* toocomplete hello process:</span></span>
     
     ![選取來源虛擬磁碟](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="0f434-141">連接 toohello 疑難排解使用遠端桌面的 VM，並確認看見 hello 來源 VM 之 OS 磁碟：</span><span class="sxs-lookup"><span data-stu-id="0f434-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="0f434-142">選取 hello 疑難排解 hello Azure 入口網站中的 VM，然後按一下*連接*。</span><span class="sxs-lookup"><span data-stu-id="0f434-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="0f434-143">開啟下載的 hello RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="0f434-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="0f434-144">輸入 hello 使用者名稱和密碼的 hello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="0f434-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="0f434-145">在檔案總管 中，尋找您所連接的 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0f434-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="0f434-146">如果 hello 來源 VM 的 VHD 是 hello 唯一的資料磁碟附加 toohello 疑難排解 VM，它應該 hello f： 磁碟機：</span><span class="sxs-lookup"><span data-stu-id="0f434-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![檢視連接的資料磁碟](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="0f434-148">建立`gpt.ini`中`\Windows\System32\GroupPolicy`hello 來源 VM 的磁碟機上 （如果存在 gpt.ini，重新命名 toogpt.ini.bak）：</span><span class="sxs-lookup"><span data-stu-id="0f434-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="0f434-149">請確定，不會無意建立下列檔案中 C:\Windows hello、 hello hello 疑難排解 VM 的作業系統磁碟機。</span><span class="sxs-lookup"><span data-stu-id="0f434-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="0f434-150">建立 hello 下列來源當做資料磁碟所連接的 VM 的 hello 作業系統磁碟機中的檔案。</span><span class="sxs-lookup"><span data-stu-id="0f434-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="0f434-151">新增下列幾行到 hello hello`gpt.ini`您建立的檔案：</span><span class="sxs-lookup"><span data-stu-id="0f434-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![建立 gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="0f434-153">在 `\Windows\System32\GroupPolicy\Machine\Scripts` 中建立 `scripts.ini`。</span><span class="sxs-lookup"><span data-stu-id="0f434-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="0f434-154">確定已顯示隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f434-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="0f434-155">如有需要建立 hello`Machine`或`Scripts`資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f434-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="0f434-156">新增下列幾行 hello hello`scripts.ini`您建立的檔案：</span><span class="sxs-lookup"><span data-stu-id="0f434-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![建立 scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="0f434-158">建立`FixAzureVM.cmd`中`\Windows\System32`以下列內容，取代 hello`<username>`和`<newpassword>`以您自己的值：</span><span class="sxs-lookup"><span data-stu-id="0f434-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![建立 FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="0f434-160">定義 hello 新密碼時，必須符合您的 vm 設定 hello 密碼複雜性需求。</span><span class="sxs-lookup"><span data-stu-id="0f434-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="0f434-161">在 Azure 入口網站中卸離 hello hello 疑難排解 VM 磁碟：</span><span class="sxs-lookup"><span data-stu-id="0f434-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="0f434-162">選取 VM 疑難排解 hello Azure 入口網站中的 hello*磁碟*。</span><span class="sxs-lookup"><span data-stu-id="0f434-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="0f434-163">選取 hello 資料磁碟附加在步驟 2 中，按一下*卸離*:</span><span class="sxs-lookup"><span data-stu-id="0f434-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![卸離磁碟](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="0f434-165">建立 VM 之前，取得 hello URI tooyour 來源作業系統磁碟：</span><span class="sxs-lookup"><span data-stu-id="0f434-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="0f434-166">選取 hello hello Azure 入口網站中的儲存體帳戶，請按一下*Blob*。</span><span class="sxs-lookup"><span data-stu-id="0f434-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="0f434-167">選取 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="0f434-167">Select hello container.</span></span> <span data-ttu-id="0f434-168">hello 來源容器是通常*vhd*:</span><span class="sxs-lookup"><span data-stu-id="0f434-168">hello source container is typically *vhds*:</span></span>
     
     ![選取儲存體帳戶 Blob](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="0f434-170">選取您 VM OS VHD 的來源，然後按一下 hello*複製*按鈕的下一個 toohello *URL*名稱：</span><span class="sxs-lookup"><span data-stu-id="0f434-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![複製磁碟 URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="0f434-172">從 hello 來源 VM 之 OS 磁碟中建立 VM:</span><span class="sxs-lookup"><span data-stu-id="0f434-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="0f434-173">使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)toocreate 將 VM 從特定的 VHD。</span><span class="sxs-lookup"><span data-stu-id="0f434-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="0f434-174">按一下 hello`Deploy tooAzure`按鈕 tooopen hello 與 hello 樣板化詳細資料，擴展您的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0f434-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="0f434-175">如果您想 tooretain hello VM 的 hello 先前設定時，選取*編輯範本*tooprovide 現有 VNet、 子網路、 網路介面卡或公用 IP。</span><span class="sxs-lookup"><span data-stu-id="0f434-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="0f434-176">在 hello`OSDISKVHDURI`參數文字方塊中，貼上您的來源 VHD URI 取得 hello 前面步驟中的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f434-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![從範本建立 VM](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="0f434-178">新的 VM 正在執行中的 hello 之後, 連接 toohello hello hello 中所指定的新密碼與使用遠端桌面的 VM`FixAzureVM.cmd`指令碼。</span><span class="sxs-lookup"><span data-stu-id="0f434-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="0f434-179">從遠端工作階段 toohello 新的 VM，移除 hello 下列檔案 tooclean hello 環境：</span><span class="sxs-lookup"><span data-stu-id="0f434-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="0f434-180">從 %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="0f434-180">From %windir%\System32</span></span>
      * <span data-ttu-id="0f434-181">移除 FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="0f434-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="0f434-182">從 %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="0f434-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="0f434-183">移除 scripts.ini</span><span class="sxs-lookup"><span data-stu-id="0f434-183">remove scripts.ini</span></span>
    * <span data-ttu-id="0f434-184">從 %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="0f434-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="0f434-185">移除 gpt.ini （如果 gpt.ini 存在之前，但您重新命名了 toogpt.ini.bak，重新命名 hello.bak 檔案後 toogpt.ini）</span><span class="sxs-lookup"><span data-stu-id="0f434-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f434-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f434-186">Next steps</span></span>
<span data-ttu-id="0f434-187">如果您仍然無法連線使用遠端桌面，請參閱 hello [RDP 疑難排解指南](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0f434-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0f434-188">hello[詳細的疑難排解指南 RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)查看疑難排解方法，而不是特定的步驟。</span><span class="sxs-lookup"><span data-stu-id="0f434-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="0f434-189">您也可以[開啟 Azure 支援要求](https://azure.microsoft.com/support/options/)，以取得實際操作協助。</span><span class="sxs-lookup"><span data-stu-id="0f434-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

