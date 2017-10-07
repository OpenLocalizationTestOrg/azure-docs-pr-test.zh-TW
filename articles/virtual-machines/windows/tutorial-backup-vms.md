---
title: "aaaBackup Azure Windows Vm |Microsoft 文件 '"
description: "使用 Azure 備份來備份並保護 Windows VM。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="58bc3-103">備份 Azure 中的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="58bc3-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="58bc3-104">您可以定期建立備份以保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="58bc3-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="58bc3-105">Azure 備份會建立復原點，並儲存在異地備援復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="58bc3-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="58bc3-106">當您從復原點還原時，您可以還原 hello 整個 VM 或特定的檔案。</span><span class="sxs-lookup"><span data-stu-id="58bc3-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="58bc3-107">這篇文章說明如何 toorestore 單一檔案 tooa VM 執行 Windows Server 和 IIS。</span><span class="sxs-lookup"><span data-stu-id="58bc3-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="58bc3-108">如果您還沒有 VM toouse，您可以建立一個使用 hello [Windows 快速入門](quick-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="58bc3-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="58bc3-109">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="58bc3-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="58bc3-110">建立 VM 的備份</span><span class="sxs-lookup"><span data-stu-id="58bc3-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="58bc3-111">排定每日備份</span><span class="sxs-lookup"><span data-stu-id="58bc3-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="58bc3-112">從備份還原檔案</span><span class="sxs-lookup"><span data-stu-id="58bc3-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="58bc3-113">備份概觀</span><span class="sxs-lookup"><span data-stu-id="58bc3-113">Backup overview</span></span>

<span data-ttu-id="58bc3-114">當 hello Azure 備份服務啟動備份工作時，它就會觸發 hello 備用分機號碼 tootake 時間點快照集。</span><span class="sxs-lookup"><span data-stu-id="58bc3-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="58bc3-115">hello Azure 備份服務會使用 hello _VMSnapshot_延伸模組。</span><span class="sxs-lookup"><span data-stu-id="58bc3-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="58bc3-116">hello 延伸模組會安裝在第一個 VM 備份 hello hello VM 正在執行。</span><span class="sxs-lookup"><span data-stu-id="58bc3-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="58bc3-117">如果 hello 未執行 VM，hello Backup service 的快照 hello 基礎儲存體 （因為 VM 已停止的 hello 時，會不發生任何應用程式寫入）。</span><span class="sxs-lookup"><span data-stu-id="58bc3-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="58bc3-118">建立 Windows Vm 快照，hello 備份服務協調一致的快照集的 hello 虛擬機器的磁碟與 hello 磁碟區陰影複製服務 (VSS) tooget。</span><span class="sxs-lookup"><span data-stu-id="58bc3-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="58bc3-119">一旦 hello Azure 備份服務會擷取 hello 快照，hello 資料就是傳送的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="58bc3-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="58bc3-120">toomaximize 效率 hello 服務識別，以及傳輸只 hello 的 hello 上一次備份之後變更資料的區塊。</span><span class="sxs-lookup"><span data-stu-id="58bc3-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="58bc3-121">Hello 資料傳輸完成時，會移除 hello 快照集，並建立復原點。</span><span class="sxs-lookup"><span data-stu-id="58bc3-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="58bc3-122">建立備份</span><span class="sxs-lookup"><span data-stu-id="58bc3-122">Create a backup</span></span>
<span data-ttu-id="58bc3-123">建立簡單排定每日備份 tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="58bc3-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="58bc3-124">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="58bc3-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="58bc3-125">在左側 hello hello 功能表中選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="58bc3-126">從 hello 清單中，選取 VM tooback。</span><span class="sxs-lookup"><span data-stu-id="58bc3-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="58bc3-127">在 hello VM 刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="58bc3-128">hello**啟用備份**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="58bc3-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="58bc3-129">在**復原服務保存庫**，按一下 **建立新**並提供 hello hello 新的保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="58bc3-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="58bc3-130">新的保存庫中建立 hello 相同資源群組及做為 hello 虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="58bc3-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="58bc3-131">按一下 [備份原則]。</span><span class="sxs-lookup"><span data-stu-id="58bc3-131">Click **Backup policy**.</span></span> <span data-ttu-id="58bc3-132">此範例中，保留 hello 預設然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="58bc3-133">在 hello**啟用備份**刀鋒視窗中，按一下 **啟用備份**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="58bc3-134">這會建立根據 hello 預設排程每日備份。</span><span class="sxs-lookup"><span data-stu-id="58bc3-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="58bc3-135">toocreate 初始的復原點，在 hello**備份**刀鋒視窗中按一下**備份現在**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="58bc3-136">在 hello**立即備份**刀鋒視窗中，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="58bc3-137">在 hello**備份**刀鋒視窗中的 VM，您會看到 hello 都已完成的復原點數目。</span><span class="sxs-lookup"><span data-stu-id="58bc3-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![復原點](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="58bc3-139">hello 第一次備份大約需要 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="58bc3-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="58bc3-140">在您的備份完成之後，請繼續 toohello 本教學課程的下一個部分。</span><span class="sxs-lookup"><span data-stu-id="58bc3-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="58bc3-141">復原檔案</span><span class="sxs-lookup"><span data-stu-id="58bc3-141">Recover a file</span></span>

<span data-ttu-id="58bc3-142">如果您不小心刪除或變更 tooa 檔案，您可以使用檔案復原 toorecover hello 檔案從您的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="58bc3-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="58bc3-143">檔案復原使用 hello VM 執行的指令碼為本機磁碟機 toomount hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="58bc3-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="58bc3-144">這些磁碟機仍會掛接為 12 小時，讓您可以從 hello 復原點複製檔案並將它們還原 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="58bc3-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="58bc3-145">在此範例中，我們會示範如何 toorecover hello hello 預設 web 網頁中使用的 IIS 映像檔。</span><span class="sxs-lookup"><span data-stu-id="58bc3-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="58bc3-146">開啟瀏覽器並連線 toohello hello VM tooshow hello 預設 IIS 頁面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="58bc3-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![預設的 IIS 網頁](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="58bc3-148">連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="58bc3-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="58bc3-149">開啟 hello VM，**檔案總管**和瀏覽 too\inetpub\wwwroot，然後刪除 hello 檔案**iisstart.png**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="58bc3-150">在您的本機電腦上重新整理 hello 瀏覽器 toosee hello hello 預設 IIS 網頁上的映像，就會消失。</span><span class="sxs-lookup"><span data-stu-id="58bc3-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![預設的 IIS 網頁](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="58bc3-152">在您的本機電腦上開啟新索引標籤，然後移 hello hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="58bc3-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="58bc3-153">在左側 hello hello 功能表中選取**虛擬機器**和選取 hello VM 表單 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="58bc3-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="58bc3-154">在 hello VM 刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="58bc3-155">hello**備份**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="58bc3-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="58bc3-156">在 hello 在 hello hello 刀鋒視窗頂端的功能表中選取**檔案復原**。</span><span class="sxs-lookup"><span data-stu-id="58bc3-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="58bc3-157">hello**檔案復原**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="58bc3-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="58bc3-158">在**步驟 1： 選取的復原點**，從 hello 下拉式清單中選取的復原點。</span><span class="sxs-lookup"><span data-stu-id="58bc3-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="58bc3-159">在**步驟 2： 下載指令碼 toobrowse 並復原檔案**，按一下 hello**下載可執行檔** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="58bc3-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="58bc3-160">儲存 hello 檔案 tooyour**下載**資料夾。</span><span class="sxs-lookup"><span data-stu-id="58bc3-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="58bc3-161">在您的本機電腦上開啟**檔案總管**並瀏覽 tooyour**下載**資料夾，然後複製 hello 下載.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="58bc3-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="58bc3-162">hello 檔案名稱的前置詞將可以是您 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="58bc3-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="58bc3-163">在您的 VM （透過 hello RDP 連線) 上貼上 hello.exe 檔案 toohello VM 的桌面。</span><span class="sxs-lookup"><span data-stu-id="58bc3-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="58bc3-164">瀏覽您的 VM toohello 桌面並按兩下 hello.exe。</span><span class="sxs-lookup"><span data-stu-id="58bc3-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="58bc3-165">這會啟動命令提示字元，然後為您可以存取的檔案共用裝載 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="58bc3-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="58bc3-166">在完成時建立 hello 共用，請輸入**q** tooclose hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="58bc3-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="58bc3-167">在您的 VM 上開啟**檔案總管**並瀏覽 toohello hello 檔案共用所使用的磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="58bc3-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="58bc3-168">瀏覽 too\inetpub\wwwroot 和複製**iisstart.png** hello 檔案共用，並將它貼到 \inetpub\wwwroot。</span><span class="sxs-lookup"><span data-stu-id="58bc3-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="58bc3-169">例如，複製 F:\inetpub\wwwroot\iisstart.png，並將它貼到 c:\inetpub\wwwroot toorecover hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="58bc3-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="58bc3-170">在您的本機電腦上開啟 hello 瀏覽器索引標籤，您連接 toohello hello VM 顯示 hello IIS 預設頁面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="58bc3-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="58bc3-171">按 CTRL + F5 toorefresh hello 瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="58bc3-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="58bc3-172">您現在應該會看到該 hello 映像已還原。</span><span class="sxs-lookup"><span data-stu-id="58bc3-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="58bc3-173">在本機電腦，請返回 toohello 瀏覽器索引標籤的 hello Azure 入口網站，並在**步驟 3： 在復原之後卸載 hello 磁碟**按一下 hello**取消掛接磁碟**按鈕。</span><span class="sxs-lookup"><span data-stu-id="58bc3-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="58bc3-174">如果您忘記 toodo 此步驟中，hello 連接 toohello 掛接點在 12 小時後已自動關閉。</span><span class="sxs-lookup"><span data-stu-id="58bc3-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="58bc3-175">這些 12 小時之後，您需要 toodownload 新的指令碼 toocreate 新的掛接點。</span><span class="sxs-lookup"><span data-stu-id="58bc3-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="58bc3-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58bc3-176">Next steps</span></span>

<span data-ttu-id="58bc3-177">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="58bc3-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="58bc3-178">建立 VM 的備份</span><span class="sxs-lookup"><span data-stu-id="58bc3-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="58bc3-179">排定每日備份</span><span class="sxs-lookup"><span data-stu-id="58bc3-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="58bc3-180">從備份還原檔案</span><span class="sxs-lookup"><span data-stu-id="58bc3-180">Restore a file from a backup</span></span>

<span data-ttu-id="58bc3-181">前進 toohello 下一個教學課程的 toolearn 有關監視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="58bc3-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="58bc3-182">監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="58bc3-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









