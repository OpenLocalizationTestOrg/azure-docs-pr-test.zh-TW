---
title: "Windows hello Azure 入口網站的疑難排解 VM 的 aaaUse |Microsoft 文件"
description: "了解如何 tootroubleshoot Windows 虛擬機器問題在 Azure 中的連接 hello OS 磁碟 tooa 復原 VM 使用 hello Azure 入口網站"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="e1242-103">疑難排解 Windows VM，藉由附加 hello OS 磁碟 tooa 復原 VM 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e1242-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="e1242-104">如果 Windows 虛擬機器 (VM) 在 Azure 中會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。</span><span class="sxs-lookup"><span data-stu-id="e1242-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="e1242-105">常見範例是防止 hello VM 可以 tooboot 成功失敗的應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="e1242-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="e1242-106">本文詳細說明如何 toouse hello Azure 入口網站 tooconnect 虛擬硬碟磁碟 tooanother Windows VM toofix 任何錯誤，然後重新建立原始 VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="e1242-107">復原程序概觀</span><span class="sxs-lookup"><span data-stu-id="e1242-107">Recovery process overview</span></span>
<span data-ttu-id="e1242-108">hello 疑難排解程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="e1242-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e1242-109">刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="e1242-110">附加和掛接 hello Windows VM 的虛擬硬碟 tooanother 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="e1242-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e1242-111">連接 toohello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="e1242-112">編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。</span><span class="sxs-lookup"><span data-stu-id="e1242-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="e1242-113">取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="e1242-114">使用建立 VM hello 原始虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e1242-115">判斷開機問題</span><span class="sxs-lookup"><span data-stu-id="e1242-115">Determine boot issues</span></span>
<span data-ttu-id="e1242-116">為什麼您的 VM 不能 tooboot 正確，toodetermine 檢查 hello 開機診斷 VM 螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="e1242-116">toodetermine why your VM is not able tooboot correctly, examine hello boot diagnostics VM screenshot.</span></span> <span data-ttu-id="e1242-117">常見的例子是應用程式更新無效，或因為刪除或移動基礎虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e1242-118">在 hello 入口網站中選取您的 VM，然後捲動 toohello**支援 + 疑難排解**> 一節。</span><span class="sxs-lookup"><span data-stu-id="e1242-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="e1242-119">按一下**開機診斷**tooview hello 螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="e1242-119">Click **Boot diagnostics** tooview hello screenshot.</span></span> <span data-ttu-id="e1242-120">請注意，任何特定的錯誤訊息或錯誤碼 toohelp 判斷 hello VM 為何發生問題。</span><span class="sxs-lookup"><span data-stu-id="e1242-120">Note any specific error messages or error codes toohelp determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="e1242-121">hello 下列範例示範正在等候停止服務的 VM:</span><span class="sxs-lookup"><span data-stu-id="e1242-121">hello following example shows a VM waiting on stopping services:</span></span>

![檢視 VM 開機診斷主控台記錄](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="e1242-123">您也可以按一下**螢幕擷取畫面**toodownload hello VM 螢幕擷取畫面的擷取。</span><span class="sxs-lookup"><span data-stu-id="e1242-123">You can also click **Screenshot** toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e1242-124">檢視現有的虛擬硬碟詳細資料</span><span class="sxs-lookup"><span data-stu-id="e1242-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="e1242-125">您可以將附加您的虛擬硬碟 tooanother VM 之前，您會需要 tooidentify hello hello 虛擬硬碟 (VHD) 名稱。</span><span class="sxs-lookup"><span data-stu-id="e1242-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="e1242-126">從 hello 入口網站中，選取您的資源群組，然後選取您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1242-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="e1242-127">按一下**Blob**，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1242-127">Click **Blobs**, as in hello following example:</span></span>

![選取儲存體 Blob](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="e1242-129">一般來說，您會有一個名為 **vhds** 的容器，以儲存虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="e1242-130">選取 hello 容器 tooview 虛擬硬碟的清單。</span><span class="sxs-lookup"><span data-stu-id="e1242-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="e1242-131">請注意您的 VHD hello 名稱 （hello 前置詞通常是您 VM hello 名稱）：</span><span class="sxs-lookup"><span data-stu-id="e1242-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![識別儲存體容器中的 VHD](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="e1242-133">從 hello 清單中選取現有虛擬硬碟，並複製 hello 步驟中使用的 hello URL:</span><span class="sxs-lookup"><span data-stu-id="e1242-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![複製現有的虛擬硬碟 URL](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="e1242-135">刪除現有的 VM</span><span class="sxs-lookup"><span data-stu-id="e1242-135">Delete existing VM</span></span>
<span data-ttu-id="e1242-136">虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。</span><span class="sxs-lookup"><span data-stu-id="e1242-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e1242-137">虛擬硬碟是存放 hello 作業系統本身、 應用程式和組態的位置。</span><span class="sxs-lookup"><span data-stu-id="e1242-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e1242-138">hello VM 本身是定義 hello 大小或位置，並參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC) 的只是中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e1242-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e1242-139">每個虛擬硬碟已連接時，指派租用 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="e1242-140">雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="e1242-141">hello 租用會繼續 tooassociate hello OS 磁碟 vm，即使該 VM 是處於已停止和取消配置狀態。</span><span class="sxs-lookup"><span data-stu-id="e1242-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e1242-142">hello 第一個步驟 toorecover VM 是 toodelete hello VM 資源本身。</span><span class="sxs-lookup"><span data-stu-id="e1242-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="e1242-143">刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="e1242-144">刪除 VM hello 之後, 您附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="e1242-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="e1242-145">選取您的 VM 在 hello 入口網站，然後按一下 **刪除**:</span><span class="sxs-lookup"><span data-stu-id="e1242-145">Select your VM in hello portal, then click **Delete**:</span></span>

![顯示開機錯誤的 VM 開機診斷螢幕擷取畫面](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="e1242-147">請等到完成刪除附加 hello 虛擬硬碟 tooanother VM 之前 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="e1242-148">hello 租用 hello 虛擬硬碟關聯 hello VM 需要 toobe 附加 hello 虛擬硬碟 tooanother VM 之前釋出。</span><span class="sxs-lookup"><span data-stu-id="e1242-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="e1242-149">附加現有的虛擬硬碟 tooanother VM</span><span class="sxs-lookup"><span data-stu-id="e1242-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="e1242-150">如 hello 接下來的幾個步驟，您可以使用另一個 VM 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="e1242-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e1242-151">附加 hello 疑難排解 VM toobe 無法 toobrowse 現有虛擬硬碟 toothis 並編輯 hello 磁碟的內容。</span><span class="sxs-lookup"><span data-stu-id="e1242-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="e1242-152">此程序可讓您 toocorrect 任何組態錯誤或檢閱其他應用程式或系統記錄檔，例如。</span><span class="sxs-lookup"><span data-stu-id="e1242-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e1242-153">選擇或建立另一個 VM toouse 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="e1242-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="e1242-154">從 hello 入口網站中，選取您的資源群組，然後選取您疑難排解的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="e1242-155">選取 磁碟，然後按一下連結現有項目：</span><span class="sxs-lookup"><span data-stu-id="e1242-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![將 hello 入口網站中的現有磁碟](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="e1242-157">tooselect 現有虛擬硬碟，按一下  **VHD 檔案**:</span><span class="sxs-lookup"><span data-stu-id="e1242-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![瀏覽現有 VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="e1242-159">選取儲存體帳戶和容器，然後按一下您現有的 VHD。</span><span class="sxs-lookup"><span data-stu-id="e1242-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="e1242-160">按一下 hello**選取**按鈕 tooconfirm 您選擇：</span><span class="sxs-lookup"><span data-stu-id="e1242-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![選取現有 VHD](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="e1242-162">您現在已選取的 VHD，然後按一下**確定**tooattach hello 現有虛擬硬碟：</span><span class="sxs-lookup"><span data-stu-id="e1242-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![確認連結現有虛擬硬碟](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="e1242-164">幾秒之後，hello**磁碟**vm 的窗格會列出您現有虛擬硬碟連接當做資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="e1242-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![現有虛擬硬碟已連結為資料磁碟](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="e1242-166">掛接 hello 連接的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1242-166">Mount hello attached data disk</span></span>

1. <span data-ttu-id="e1242-167">開啟 遠端桌面連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-167">Open a Remote Desktop connection tooyour VM.</span></span> <span data-ttu-id="e1242-168">Hello 入口網站中選取您的 VM，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="e1242-168">Select your VM in hello portal and click **Connect**.</span></span> <span data-ttu-id="e1242-169">下載並開啟 hello RDP 連接檔案。</span><span class="sxs-lookup"><span data-stu-id="e1242-169">Download and open hello RDP connection file.</span></span> <span data-ttu-id="e1242-170">輸入認證 toolog tooyour VM 中如下所示：</span><span class="sxs-lookup"><span data-stu-id="e1242-170">Enter your credentials toolog in tooyour VM as follows:</span></span>

    ![登入 tooyour VM 使用遠端桌面](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="e1242-172">開啟 [伺服器管理員]，然後選取 [檔案和存放服務]。</span><span class="sxs-lookup"><span data-stu-id="e1242-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![選取伺服器管理員內的檔案和存放服務](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="e1242-174">自動偵測並附加 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-174">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="e1242-175">toosee hello 一份連接磁碟上，選取**磁碟**。</span><span class="sxs-lookup"><span data-stu-id="e1242-175">toosee a list of hello connected disks, select **Disks**.</span></span> <span data-ttu-id="e1242-176">您可以選取您的資料磁碟 tooview 磁碟區的資訊，包括 hello 磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="e1242-176">You can select your data disk tooview volume information, including hello drive letter.</span></span> <span data-ttu-id="e1242-177">下列範例顯示 hello 連接資料磁碟和使用 hello **f:**:</span><span class="sxs-lookup"><span data-stu-id="e1242-177">hello following example shows hello data disk attached and using **F:**:</span></span>

    ![伺服器管理員中的已連接磁碟和磁碟區資訊](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e1242-179">修正原始虛擬硬碟的問題</span><span class="sxs-lookup"><span data-stu-id="e1242-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e1242-180">與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。</span><span class="sxs-lookup"><span data-stu-id="e1242-180">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e1242-181">一旦解決 hello 問題之後，繼續進行步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="e1242-181">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e1242-182">卸載並中斷連結原始虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="e1242-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e1242-183">一旦解決的錯誤，卸離 hello 現有虛擬硬碟從您疑難排解的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-183">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e1242-184">您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。</span><span class="sxs-lookup"><span data-stu-id="e1242-184">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e1242-185">Hello RDP 工作階段 tooyour VM，從開啟**伺服器管理員**，然後選取**檔案和存放服務**:</span><span class="sxs-lookup"><span data-stu-id="e1242-185">From hello RDP session tooyour VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![在伺服器管理員中選取檔案和存放服務](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="e1242-187">依序選取 [磁碟] 及您的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="e1242-188">在資料磁碟上按一下滑鼠右鍵，然後選取 [離線]：</span><span class="sxs-lookup"><span data-stu-id="e1242-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![設定為離線的伺服器管理員 中的 hello 資料磁碟](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="e1242-190">現在您可以卸離 hello 虛擬硬碟從 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-190">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="e1242-191">Hello Azure 入口網站中選取您的 VM，然後按一下**磁碟**。</span><span class="sxs-lookup"><span data-stu-id="e1242-191">Select your VM in hello Azure portal and click **Disks**.</span></span> <span data-ttu-id="e1242-192">選取您現有的虛擬硬碟，然後按一下中斷連結：</span><span class="sxs-lookup"><span data-stu-id="e1242-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![將現有虛擬硬碟中斷連結](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="e1242-194">請等到 hello VM 已成功中斷 hello 資料磁碟連結才能繼續。</span><span class="sxs-lookup"><span data-stu-id="e1242-194">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e1242-195">從原始硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="e1242-195">Create VM from original hard disk</span></span>
<span data-ttu-id="e1242-196">toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="e1242-196">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="e1242-197">hello 範本會將 VM 部署到現有的虛擬網路，使用從 hello hello VHD URL 稍早的命令。</span><span class="sxs-lookup"><span data-stu-id="e1242-197">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="e1242-198">按一下 hello**部署 tooAzure**按鈕，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e1242-198">Click hello **Deploy tooAzure** button as follows:</span></span>

![從 Github 的範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="e1242-200">hello 範本會載入至 hello 部署的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e1242-200">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="e1242-201">輸入您新的 VM 和現有的 Azure 資源的 hello 名稱，然後貼上 hello URL tooyour 現有虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="e1242-201">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="e1242-202">toobegin hello 部署中，按一下 **購買**:</span><span class="sxs-lookup"><span data-stu-id="e1242-202">toobegin hello deployment, click **Purchase**:</span></span>

![從範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e1242-204">重新啟用開機診斷</span><span class="sxs-lookup"><span data-stu-id="e1242-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="e1242-205">當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="e1242-205">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e1242-206">toocheck hello 的開機診斷狀態，然後開啟有需要在 hello 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1242-206">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="e1242-207">在 [監視] 底下，按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="e1242-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="e1242-208">確定 hello 狀態**上**，太接下來 hello 核取記號和**開機診斷**已選取。</span><span class="sxs-lookup"><span data-stu-id="e1242-208">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="e1242-209">如果有進行任何變更，請按一下 [儲存]：</span><span class="sxs-lookup"><span data-stu-id="e1242-209">If you make any changes, click **Save**:</span></span>

![更新開機診斷設定](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="e1242-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1242-211">Next steps</span></span>
<span data-ttu-id="e1242-212">如果您有連接 tooyour VM 的問題，請參閱[疑難排解 RDP 連線 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e1242-212">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e1242-213">如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Windows VM 上的應用程式連線問題進行疑難排解](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e1242-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e1242-214">如需使用 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e1242-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>