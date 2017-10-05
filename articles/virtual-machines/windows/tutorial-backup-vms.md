---
title: "備份 Azure Windows VM | Microsoft Docs"
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
ms.openlocfilehash: 8e58a2290e5034ef393f65cbcddb86e18cf4a6ec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="55ed2-103">備份 Azure 中的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="55ed2-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="55ed2-104">您可以定期建立備份以保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="55ed2-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="55ed2-105">Azure 備份會建立復原點，並儲存在異地備援復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="55ed2-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="55ed2-106">當您從復原點還原時，可以還原整個 VM 或只還原特定檔案。</span><span class="sxs-lookup"><span data-stu-id="55ed2-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="55ed2-107">本文說明如何將單一檔案還原成執行 Windows Server 和 IIS 的 VM。</span><span class="sxs-lookup"><span data-stu-id="55ed2-107">This article explains how to restore a single file to a VM running Windows Server and IIS.</span></span> <span data-ttu-id="55ed2-108">如果您還沒有 VM 可以使用，請用 [Windows 快速入門](quick-create-portal.md)中的步驟建立一個。</span><span class="sxs-lookup"><span data-stu-id="55ed2-108">If you don't already have a VM to use, you can create one using the [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="55ed2-109">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="55ed2-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55ed2-110">建立 VM 的備份</span><span class="sxs-lookup"><span data-stu-id="55ed2-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="55ed2-111">排定每日備份</span><span class="sxs-lookup"><span data-stu-id="55ed2-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="55ed2-112">從備份還原檔案</span><span class="sxs-lookup"><span data-stu-id="55ed2-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="55ed2-113">備份概觀</span><span class="sxs-lookup"><span data-stu-id="55ed2-113">Backup overview</span></span>

<span data-ttu-id="55ed2-114">Azure 備份服務開始備份作業時，會觸發備份擴充功能以建立時間點快照集。</span><span class="sxs-lookup"><span data-stu-id="55ed2-114">When the Azure Backup service initiates a backup job, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="55ed2-115">Azure 備份服務使用 VMSnapshot 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="55ed2-115">The Azure Backup service uses the _VMSnapshot_ extension.</span></span> <span data-ttu-id="55ed2-116">如果 VM 正在執行，會在第一次 VM 備份期間安裝此擴充功能。</span><span class="sxs-lookup"><span data-stu-id="55ed2-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="55ed2-117">如果 VM 未在執行中，則備份服務會擷取基礎儲存體的快照集 (因為 VM 停止時不會發生任何應用程式寫入)。</span><span class="sxs-lookup"><span data-stu-id="55ed2-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="55ed2-118">當擷取 Windows VM 的快照集時，備份服務會與磁碟區陰影複製服務 (VSS) 協調，以取得虛擬機器磁碟一致的快照集。</span><span class="sxs-lookup"><span data-stu-id="55ed2-118">When taking a snapshot of Windows VMs, the Backup service coordinates with the Volume Shadow Copy Service (VSS) to get a consistent snapshot of the virtual machine's disks.</span></span> <span data-ttu-id="55ed2-119">Azure 備份服務擷取快照集之後，資料會傳輸至保存庫。</span><span class="sxs-lookup"><span data-stu-id="55ed2-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="55ed2-120">為了能更有效率，服務只會找出並傳輸自上次備份之後有變更的資料區塊。</span><span class="sxs-lookup"><span data-stu-id="55ed2-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="55ed2-121">資料傳輸完畢後，系統會移除快照集並建立復原點。</span><span class="sxs-lookup"><span data-stu-id="55ed2-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="55ed2-122">建立備份</span><span class="sxs-lookup"><span data-stu-id="55ed2-122">Create a backup</span></span>
<span data-ttu-id="55ed2-123">建立復原服務保存庫的簡單排程每日備份。</span><span class="sxs-lookup"><span data-stu-id="55ed2-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="55ed2-124">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="55ed2-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="55ed2-125">在左邊的功能表上，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="55ed2-126">從清單中選取要備份的 VM。</span><span class="sxs-lookup"><span data-stu-id="55ed2-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="55ed2-127">在 VM 刀鋒視窗的 [設定] 區段中，按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="55ed2-128">[啟用備份] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="55ed2-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="55ed2-129">在 [復原服務保存庫] 中，按一下 [新建] 並提供新保存庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="55ed2-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="55ed2-130">新保存庫已在與虛擬機器相同的資源群組和位置中建立。</span><span class="sxs-lookup"><span data-stu-id="55ed2-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="55ed2-131">按一下 [備份原則]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-131">Click **Backup policy**.</span></span> <span data-ttu-id="55ed2-132">在此範例中請保留預設值，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="55ed2-133">在 [啟用備份] 刀鋒視窗上，按一下 [啟用備份]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="55ed2-134">這會根據預設排程建立每日備份。</span><span class="sxs-lookup"><span data-stu-id="55ed2-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="55ed2-135">若要建立初始復原點，在 [備份] 刀鋒視窗中按一下 [立即備份]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="55ed2-136">在 [立即備份] 刀鋒視窗上，按一下日曆圖示，使用日曆控制項選取此復原點保留的最後一天，然後按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="55ed2-137">在 VM 的 [備份] 刀鋒視窗中，您會看到已完成的復原點數目。</span><span class="sxs-lookup"><span data-stu-id="55ed2-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![復原點](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="55ed2-139">第一次備份大約需要 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="55ed2-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="55ed2-140">在備份完成之後，繼續進行本教學課程的下一個部分。</span><span class="sxs-lookup"><span data-stu-id="55ed2-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="55ed2-141">復原檔案</span><span class="sxs-lookup"><span data-stu-id="55ed2-141">Recover a file</span></span>

<span data-ttu-id="55ed2-142">如果您不小心刪除或變更某個檔案，可以使用「檔案復原」從您的備份保存庫復原檔案。</span><span class="sxs-lookup"><span data-stu-id="55ed2-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="55ed2-143">檔案復原使用在 VM 上執行的指令碼，將復原點掛接為本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="55ed2-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="55ed2-144">這些磁碟機將保持掛接達 12 小時，讓您可以從復原點複製檔案，並將它們還原至 VM。</span><span class="sxs-lookup"><span data-stu-id="55ed2-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="55ed2-145">在此範例中，我們會示範如何復原用於 IIS 預設網頁的影像檔案。</span><span class="sxs-lookup"><span data-stu-id="55ed2-145">In this example, we show how to recover the image file that is used in the default web page for IIS.</span></span> 

1. <span data-ttu-id="55ed2-146">開啟瀏覽器，連線到 VM 的 IP 位址，以顯示預設的 IIS 網頁。</span><span class="sxs-lookup"><span data-stu-id="55ed2-146">Open a browser and connect to the IP address of the VM to show the default IIS page.</span></span>

    ![預設的 IIS 網頁](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="55ed2-148">連線至 VM。</span><span class="sxs-lookup"><span data-stu-id="55ed2-148">Connect to the VM.</span></span>
3. <span data-ttu-id="55ed2-149">在 VM 上開啟 [檔案總管]，瀏覽至 \inetpub\wwwroot，刪除案 iisstart.png 檔。</span><span class="sxs-lookup"><span data-stu-id="55ed2-149">On the VM, open **File Explorer** and navigate to \inetpub\wwwroot and delete the file **iisstart.png**.</span></span>
4. <span data-ttu-id="55ed2-150">在您的本機電腦上，重新整理瀏覽器，應該會看到預設 IIS 網頁上的影像已不存在。</span><span class="sxs-lookup"><span data-stu-id="55ed2-150">On your local computer, refresh the browser to see that the image on the default IIS page is gone.</span></span>

    ![預設的 IIS 網頁](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="55ed2-152">在您的本機電腦上，開啟新的索引標籤並前往 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="55ed2-152">On your local computer, open a new tab and go the the [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="55ed2-153">在左邊的功能表上，選取 [虛擬機器]，然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="55ed2-153">In the menu on the left, select **Virtual machines** and select the VM form the list.</span></span>
8. <span data-ttu-id="55ed2-154">在 VM 刀鋒視窗的 [設定] 區段中，按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-154">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="55ed2-155">[備份] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="55ed2-155">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="55ed2-156">在刀鋒視窗頂端的功能表中，選取 [檔案復原]。</span><span class="sxs-lookup"><span data-stu-id="55ed2-156">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="55ed2-157">[檔案復原] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="55ed2-157">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="55ed2-158">在 [步驟 1︰選取復原點] 中，從下拉式清單選取復原點。</span><span class="sxs-lookup"><span data-stu-id="55ed2-158">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="55ed2-159">在 [步驟 2：下載指令碼以瀏覽及復原檔案] 中，按一下 [下載執行檔] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55ed2-159">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="55ed2-160">將檔案儲存至您的 **Downloads** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="55ed2-160">Save the file to your **Downloads** folder.</span></span>
12. <span data-ttu-id="55ed2-161">在您的本機電腦上，開啟 [檔案總管] 並瀏覽至 **Downloads** 資料夾，複製下載的 .exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="55ed2-161">On your local computer, open **File Explorer** and navigate to your **Downloads** folder and copy the downloaded .exe file.</span></span> <span data-ttu-id="55ed2-162">檔案名稱前面會加上您的 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="55ed2-162">The filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="55ed2-163">在您的 VM 上 (透過 RDP 連線)，將 .exe 檔案貼到 VM 桌面上。</span><span class="sxs-lookup"><span data-stu-id="55ed2-163">On your VM (over the RDP connection) paste the .exe file to the Desktop of your VM.</span></span> 
14. <span data-ttu-id="55ed2-164">瀏覽至 VM 桌面，按兩下 .exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="55ed2-164">Navigate to the desktop of your VM and double-click on the .exe.</span></span> <span data-ttu-id="55ed2-165">這會啟動命令提示字元，並將復原點掛接為您可以存取的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="55ed2-165">This will launch a command prompt and then mount the recovery point as a file share that you can access.</span></span> <span data-ttu-id="55ed2-166">當共用建立完成時，輸入 **q** 關閉命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="55ed2-166">When it is finished creating the share, type **q** to close the command prompt.</span></span>
15. <span data-ttu-id="55ed2-167">在您的 VM 上，開啟[檔案總管] 並瀏覽至此檔案共用所使用的磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="55ed2-167">On your VM, open **File Explorer** and navigate to the drive letter that was used for the file share.</span></span>
16. <span data-ttu-id="55ed2-168">瀏覽到 \inetpub\wwwroot，複製檔案共用中的 **iisstart.png**，並將它貼到 \inetpub\wwwroot。</span><span class="sxs-lookup"><span data-stu-id="55ed2-168">Navigate to \inetpub\wwwroot and copy **iisstart.png** from the file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="55ed2-169">例如，複製 F:\inetpub\wwwroot\iisstart.png，並將其貼到 c:\inetpub\wwwroot 以復原檔案。</span><span class="sxs-lookup"><span data-stu-id="55ed2-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot to recover the file.</span></span>
17. <span data-ttu-id="55ed2-170">在您的本機電腦上開啟瀏覽器索引標籤，您已連線到顯示 IIS 預設網頁之 VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="55ed2-170">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the IIS default page.</span></span> <span data-ttu-id="55ed2-171">按 CTRL + F5 重新整理瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="55ed2-171">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="55ed2-172">您現在應該會看到已還原的影像。</span><span class="sxs-lookup"><span data-stu-id="55ed2-172">You should now see that the image has been restored.</span></span>
18. <span data-ttu-id="55ed2-173">在您的本機電腦上，回到 Azure 入口網站的瀏覽器索引標籤，並在 [步驟 3︰在復原後取消掛接磁碟] 按一下 [取消掛接磁碟] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55ed2-173">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="55ed2-174">如果您忘記執行此步驟，與此掛接點的連線會在 12 小時後自動關閉。</span><span class="sxs-lookup"><span data-stu-id="55ed2-174">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="55ed2-175">在這 12 小時後，您必須下載新的指令碼來建立新的掛接點。</span><span class="sxs-lookup"><span data-stu-id="55ed2-175">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55ed2-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55ed2-176">Next steps</span></span>

<span data-ttu-id="55ed2-177">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="55ed2-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55ed2-178">建立 VM 的備份</span><span class="sxs-lookup"><span data-stu-id="55ed2-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="55ed2-179">排定每日備份</span><span class="sxs-lookup"><span data-stu-id="55ed2-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="55ed2-180">從備份還原檔案</span><span class="sxs-lookup"><span data-stu-id="55ed2-180">Restore a file from a backup</span></span>

<span data-ttu-id="55ed2-181">請前進到下一個教學課程，了解如何監視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="55ed2-181">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55ed2-182">監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="55ed2-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









