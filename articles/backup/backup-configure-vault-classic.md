---
title: "將 Windows 伺服器或工作站備份至 Azure (傳統模型) | Microsoft Docs"
description: "將 Windows 伺服器或用戶端備份至 Azure 中的備份保存庫。 瀏覽使用 Azure 備份代理程式將檔案和資料夾放入備份保存庫來保護的基本概念。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份保存庫；備份 Windows Server；備份Windows；"
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: a8daa6a4655b72936b6299c0fa5b80459ffa5da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-a-windows-server-or-workstation-to-azure-using-the-classic-portal"></a><span data-ttu-id="82219-105">使用傳統入口網站將 Windows 伺服器或工作站備份至 Azure</span><span class="sxs-lookup"><span data-stu-id="82219-105">Back up a Windows server or workstation to Azure using the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82219-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="82219-106">Classic portal</span></span>](backup-configure-vault-classic.md)
> * [<span data-ttu-id="82219-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="82219-107">Azure portal</span></span>](backup-configure-vault.md)
>
>

<span data-ttu-id="82219-108">本文涵蓋準備環境和將 Windows 伺服器 (或工作站) 備份至 Azure 所需依循的程序。</span><span class="sxs-lookup"><span data-stu-id="82219-108">This article covers the procedures that you need to follow to prepare your environment and back up a Windows server (or workstation) to Azure.</span></span> <span data-ttu-id="82219-109">它還涵蓋部署備份解決方案的考量。</span><span class="sxs-lookup"><span data-stu-id="82219-109">It also covers considerations for deploying your backup solution.</span></span> <span data-ttu-id="82219-110">如果您想要第一次嘗試 Azure 備份，這篇文章可快速引導您完成該程序。</span><span class="sxs-lookup"><span data-stu-id="82219-110">If you're interested in trying Azure Backup for the first time, this article quickly walks you through the process.</span></span>

<span data-ttu-id="82219-111">Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。</span><span class="sxs-lookup"><span data-stu-id="82219-111">Azure has two different deployment models for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="82219-112">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="82219-112">This article covers using the classic deployment model.</span></span> <span data-ttu-id="82219-113">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="82219-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="82219-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="82219-114">Before you start</span></span>
<span data-ttu-id="82219-115">若要將伺服器或用戶端備份至 Azure，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="82219-115">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="82219-116">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="82219-116">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-backup-vault"></a><span data-ttu-id="82219-117">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="82219-117">Create a backup vault</span></span>
<span data-ttu-id="82219-118">若要從伺服器或用戶端備份檔案與資料夾，您必須在要儲存這些資料的地理區域中建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-118">To back up files and folders from a server or client, you need to create a backup vault in the geographic region where you want to store the data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82219-119">從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-119">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="82219-120">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-120">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="82219-121">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="82219-121">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="82219-122">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-122">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="82219-123">在 **2017 年 10 月 15 日**之後，您就無法使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-123">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="82219-124">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="82219-124">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="82219-125">任何其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-125">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="82219-126">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="82219-126">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="82219-127">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="82219-127">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>


## <a name="download-the-vault-credential-file"></a><span data-ttu-id="82219-128">下載保存庫認證檔</span><span class="sxs-lookup"><span data-stu-id="82219-128">Download the vault credential file</span></span>
<span data-ttu-id="82219-129">內部部署機器必須先驗證備份保存庫，才能將資料備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="82219-129">The on-premises machine needs to be authenticated with a backup vault before it can back up data to Azure.</span></span> <span data-ttu-id="82219-130">驗證是透過「保存庫認證」 來達成。</span><span class="sxs-lookup"><span data-stu-id="82219-130">The authentication is achieved through *vault credentials*.</span></span> <span data-ttu-id="82219-131">保存庫認證檔會透過安全通道，從傳統入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="82219-131">The vault credential file is downloaded through a secure channel from the classic portal.</span></span> <span data-ttu-id="82219-132">憑證私密金鑰不會保存在入口網站或服務中。</span><span class="sxs-lookup"><span data-stu-id="82219-132">The certificate private key does not persist in the portal or the service.</span></span>

### <a name="to-download-the-vault-credential-file-to-a-local-machine"></a><span data-ttu-id="82219-133">將保存庫認證檔下載至本機電腦</span><span class="sxs-lookup"><span data-stu-id="82219-133">To download the vault credential file to a local machine</span></span>
1. <span data-ttu-id="82219-134">在左側導覽窗格中，按一下 [復原服務] ，然後選取您所建立的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-134">In the left navigation pane, click **Recovery Services**, and then select the backup vault that you created.</span></span>

    ![IR 已完成](./media/backup-configure-vault-classic/rs-left-nav.png)
2. <span data-ttu-id="82219-136">在 [快速入門] 頁面上，按一下 [ **下載保存庫認證**]。</span><span class="sxs-lookup"><span data-stu-id="82219-136">On the Quick Start page, click **Download vault credentials**.</span></span>

   <span data-ttu-id="82219-137">傳統入口網站會使用保存庫名稱和目前日期的組合來產生保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="82219-137">The classic portal generates a vault credential by using a combination of the vault name and the current date.</span></span> <span data-ttu-id="82219-138">保存庫認證檔僅在註冊工作流程期間使用，並於 48 小時後過期。</span><span class="sxs-lookup"><span data-stu-id="82219-138">The vault credentials file is used only during the registration workflow and expires after 48 hours.</span></span>

   <span data-ttu-id="82219-139">保存庫認證檔可以從入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="82219-139">The vault credential file can be downloaded from the portal.</span></span>
3. <span data-ttu-id="82219-140">按一下 [儲存]  將保存庫認證檔下載至本機帳戶的 [下載] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="82219-140">Click **Save** to download the vault credential file to the Downloads folder of the local account.</span></span> <span data-ttu-id="82219-141">您也可以從 [儲存] 功能表選取 [另存新檔]，以指定保存庫認證檔的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="82219-141">You can also select **Save As** from the **Save** menu to specify a location for the vault credential file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82219-142">請確保保存庫認證檔儲存在可從您的電腦存取的位置。</span><span class="sxs-lookup"><span data-stu-id="82219-142">Make sure the vault credential file is saved in a location that can be accessed from your machine.</span></span> <span data-ttu-id="82219-143">如果是儲存在檔案共用或伺服器訊息區塊中，請確認您擁有存取權限。</span><span class="sxs-lookup"><span data-stu-id="82219-143">If it is stored in a file share or server message block, verify that you have the permissions to access it.</span></span>
   >
   >

## <a name="download-install-and-register-the-backup-agent"></a><span data-ttu-id="82219-144">下載、安裝和註冊備份代理程式</span><span class="sxs-lookup"><span data-stu-id="82219-144">Download, install, and register the Backup agent</span></span>
<span data-ttu-id="82219-145">在您建立備份保存庫並下載保存庫認證檔之後，必須在您每一部 Windows 電腦上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="82219-145">After you create the backup vault and download the vault credential file, an agent must be installed on each of your Windows machines.</span></span>

### <a name="to-download-install-and-register-the-agent"></a><span data-ttu-id="82219-146">下載、安裝和註冊代理程式</span><span class="sxs-lookup"><span data-stu-id="82219-146">To download, install, and register the agent</span></span>
1. <span data-ttu-id="82219-147">按一下 [復原服務] ，然後選取您要向伺服器註冊的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="82219-147">Click **Recovery Services**, and then select the backup vault that you want to register with a server.</span></span>
2. <span data-ttu-id="82219-148">在 [快速啟動] 頁面上，按一下 [適用於 Windows Server 或 System Center Data Protection Manager 或 Windows 用戶端的代理程式] 代理程式。</span><span class="sxs-lookup"><span data-stu-id="82219-148">On the Quick Start page, click the agent **Agent for Windows Server or System Center Data Protection Manager or Windows client**.</span></span> <span data-ttu-id="82219-149">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="82219-149">Then click **Save**.</span></span>

    ![儲存代理程式](./media/backup-configure-vault-classic/agent.png)
3. <span data-ttu-id="82219-151">下載 MARSagentinstaller.exe 檔案之後，按一下 [執行] \(或從儲存的位置按兩下 **MARSAgentInstaller.exe**)。</span><span class="sxs-lookup"><span data-stu-id="82219-151">After the MARSagentinstaller.exe file has downloaded, click **Run** (or double-click **MARSAgentInstaller.exe** from the saved location).</span></span>
4. <span data-ttu-id="82219-152">選擇代理程式所需的安裝資料夾和快取資料夾，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="82219-152">Choose the installation folder and cache folder that are required for the agent, and then click **Next**.</span></span> <span data-ttu-id="82219-153">您指定的快取位置必須至少包含等於備份資料大小 5% 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="82219-153">The cache location you specify must have free space equal to at least 5 percent of the backup data.</span></span>
5. <span data-ttu-id="82219-154">您可以繼續透過預設 Proxy 設定連線網際網路。</span><span class="sxs-lookup"><span data-stu-id="82219-154">You can continue to connect to the Internet through the default proxy settings.</span></span>             <span data-ttu-id="82219-155">若您使用 Proxy 伺服器連線網際網路，請在 [Proxy 組態] 頁面上選取 [使用自訂 Proxy 設定]  核取方塊，然後輸入 Proxy 伺服器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="82219-155">If you use a proxy server to connect to the Internet, on the Proxy Configuration page, select the **Use custom proxy settings** check box, and then enter the proxy server details.</span></span> <span data-ttu-id="82219-156">若您使用已驗證的 Proxy，請輸入使用者名稱和密碼詳細資料，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="82219-156">If you use an authenticated proxy, enter the user name and password details, and then click **Next**.</span></span>
6. <span data-ttu-id="82219-157">按一下 [安裝]  開始代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="82219-157">Click **Install** to begin the agent installation.</span></span> <span data-ttu-id="82219-158">備份代理程式會安裝 .NET Framework 4.5 和 Windows PowerShell (若尚未安裝) 來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="82219-158">The Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not already installed) to complete the installation.</span></span>
7. <span data-ttu-id="82219-159">安裝代理程式之後，按一下 [繼續註冊]  以繼續工作流程。</span><span class="sxs-lookup"><span data-stu-id="82219-159">After the agent is installed, click **Proceed to Registration** to continue with the workflow.</span></span>
8. <span data-ttu-id="82219-160">在 [保存庫識別] 頁面中，瀏覽並選取先前下載的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="82219-160">On the Vault Identification page, browse to and select the vault credential file that you previously downloaded.</span></span>

    <span data-ttu-id="82219-161">從入口網站下載保存庫認證檔之後，其有效期只有 48 小時。</span><span class="sxs-lookup"><span data-stu-id="82219-161">The vault credential file is valid for only 48 hours after it’s downloaded from the portal.</span></span> <span data-ttu-id="82219-162">如果您在此頁面上遇到錯誤 (例如「提供的保存庫認證檔已過期」)，請登入入口網站並再次下載保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="82219-162">If you encounter an error on this page (such as “Vault credentials file provided has expired”), sign in to the portal and download the vault credential file again.</span></span>

    <span data-ttu-id="82219-163">請確定保存庫認證檔位於可透過設定應用程式存取的位置。</span><span class="sxs-lookup"><span data-stu-id="82219-163">Ensure that the vault credential file is available in a location that can be accessed by the setup application.</span></span> <span data-ttu-id="82219-164">如果您遇到存取權相關的錯誤，請將保存庫認證檔複製到同一部電腦中的暫存位置並重試作業。</span><span class="sxs-lookup"><span data-stu-id="82219-164">If you encounter access-related errors, copy the vault credential file to a temporary location on the same machine and retry the operation.</span></span>

    <span data-ttu-id="82219-165">如果您遇到保存庫認證錯誤 (例如「提供的保存庫認證無效」)，表示檔案已經損毀或沒有和復原服務關聯的最新認證。</span><span class="sxs-lookup"><span data-stu-id="82219-165">If you encounter a vault credential error such as “Invalid vault credentials provided," the file is damaged or does not have the latest credentials associated with the recovery service.</span></span> <span data-ttu-id="82219-166">從入口網站下載新的保存庫認證檔後重試作業。</span><span class="sxs-lookup"><span data-stu-id="82219-166">Retry the operation after downloading a new vault credential file from the portal.</span></span> <span data-ttu-id="82219-167">若使用者連續快速地按下 [下載保存庫認證]  選項數次，也可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="82219-167">This error can also occur if a user clicks the **Download vault credential** option several times in quick succession.</span></span> <span data-ttu-id="82219-168">在此情況下，只有最後一個保存庫認證檔有效。</span><span class="sxs-lookup"><span data-stu-id="82219-168">In this case, only the last vault credential file is valid.</span></span>
9. <span data-ttu-id="82219-169">在 [加密設定] 頁面中，您可以產生複雜密碼或提供複雜密碼 (最少 16 個字元)。</span><span class="sxs-lookup"><span data-stu-id="82219-169">On the Encryption Setting page, you can either generate a passphrase or provide a passphrase (with a minimum of 16 characters).</span></span> <span data-ttu-id="82219-170">請記得將複雜密碼存放在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="82219-170">Remember to save the passphrase in a secure location.</span></span>
10. <span data-ttu-id="82219-171">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="82219-171">Click **Finish**.</span></span> <span data-ttu-id="82219-172">[註冊伺服器精靈] 會向備份註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="82219-172">The Register Server Wizard registers the server with Backup.</span></span>

    > [!WARNING]
    > <span data-ttu-id="82219-173">如果遺失或忘記複雜密碼，Microsoft 將無法協助您復原備份資料。</span><span class="sxs-lookup"><span data-stu-id="82219-173">If you lose or forget the passphrase, Microsoft cannot help you recover the backup data.</span></span> <span data-ttu-id="82219-174">加密複雜密碼為您所擁有，Microsoft 並無法看到您所使用的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="82219-174">You own the encryption passphrase, and Microsoft does not have visibility into the passphrase that you use.</span></span> <span data-ttu-id="82219-175">請將檔案儲存在安全的位置，因為在復原作業期間將會需要該檔案。</span><span class="sxs-lookup"><span data-stu-id="82219-175">Save the file in a secure location because it will be required during a recovery operation.</span></span>
    >
    >

11. <span data-ttu-id="82219-176">設定加密金鑰之後，讓 [啟動 Microsoft Azure 復原服務代理程式] 核取方塊保持已選取狀態，然後按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="82219-176">After the encryption key is set, leave the **Launch Microsoft Azure Recovery Services Agent** check box selected, and then click **Close**.</span></span>

## <a name="complete-the-initial-backup"></a><span data-ttu-id="82219-177">完成初始備份</span><span class="sxs-lookup"><span data-stu-id="82219-177">Complete the initial backup</span></span>
<span data-ttu-id="82219-178">初始備份包括兩項重要工作：</span><span class="sxs-lookup"><span data-stu-id="82219-178">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="82219-179">建立備份排程</span><span class="sxs-lookup"><span data-stu-id="82219-179">Creating the backup schedule</span></span>
* <span data-ttu-id="82219-180">第一次備份檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="82219-180">Backing up files and folders for the first time</span></span>

<span data-ttu-id="82219-181">在備份原則完成初始備份之後，它會建立在您需要復原資料時可使用的備份點。</span><span class="sxs-lookup"><span data-stu-id="82219-181">After the backup policy completes the initial backup, it creates backup points that you can use if you need to recover the data.</span></span> <span data-ttu-id="82219-182">備份原則會依據您定義的排程執行此作業。</span><span class="sxs-lookup"><span data-stu-id="82219-182">The backup policy does this based on the schedule that you define.</span></span>

### <a name="to-schedule-the-backup"></a><span data-ttu-id="82219-183">排程備份</span><span class="sxs-lookup"><span data-stu-id="82219-183">To schedule the backup</span></span>
1. <span data-ttu-id="82219-184">開啟 Microsoft Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="82219-184">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="82219-185">(如果您在關閉註冊伺服器精靈時，讓 [啟動 Microsoft Azure 復原服務代理程式] 核取方塊保持已選取狀態，備份代理程式將會自動開啟。)您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。</span><span class="sxs-lookup"><span data-stu-id="82219-185">(It will open automatically if you left the **Launch Microsoft Azure Recovery Services Agent** check box selected when you closed the Register Server Wizard.) You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![啟動 Azure 備份代理程式](./media/backup-configure-vault-classic/snap-in-search.png)
2. <span data-ttu-id="82219-187">在備份代理程式中，按一下 [排程備份] 。</span><span class="sxs-lookup"><span data-stu-id="82219-187">In the Backup agent, click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. <span data-ttu-id="82219-189">在排程備份精靈的 [開始使用] 頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="82219-189">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="82219-190">在 [選取要備份的項目] 頁面上，按一下 [新增項目] 。</span><span class="sxs-lookup"><span data-stu-id="82219-190">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="82219-191">選取您要備份的檔案和資料夾，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="82219-191">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="82219-192">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="82219-192">Click **Next**.</span></span>
7. <span data-ttu-id="82219-193">在 [指定備份排程] 頁面上，指定[備份排程]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="82219-193">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="82219-194">您可以排程每日 (一天最多三次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="82219-194">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="82219-196">如需如何指定備份排程的相關詳細資訊，請參閱 [使用 Azure 備份來取代您的磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)一文。</span><span class="sxs-lookup"><span data-stu-id="82219-196">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="82219-197">在 [選取保留原則] 頁面上，選取 [保留原則] 做為備份複本。</span><span class="sxs-lookup"><span data-stu-id="82219-197">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="82219-198">保留原則會指定備份將儲存的期間。</span><span class="sxs-lookup"><span data-stu-id="82219-198">The retention policy specifies the duration for which the backup will be stored.</span></span> <span data-ttu-id="82219-199">除了僅針對所有備份點指定「一般原則」之外，您可以指定在進行備份時根據不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="82219-199">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="82219-200">您可以修改每日、每週、每月和每年保留原則，以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="82219-200">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="82219-201">在 [選擇初始備份類型] 頁面上，選擇初始備份類型。</span><span class="sxs-lookup"><span data-stu-id="82219-201">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="82219-202">讓 [自動透過網路] 選項保持已選取狀態，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="82219-202">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="82219-203">您可以透過網路自動備份，也可以離線備份。</span><span class="sxs-lookup"><span data-stu-id="82219-203">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="82219-204">這篇文章的其餘部分說明自動備份的程序。</span><span class="sxs-lookup"><span data-stu-id="82219-204">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="82219-205">如果您想要執行離線備份，請檢閱 [在 Azure Backup 中離線備份工作流程](backup-azure-backup-import-export.md) 一文以了解其他資訊。</span><span class="sxs-lookup"><span data-stu-id="82219-205">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="82219-206">在 [確認] 頁面上檢閱資訊，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="82219-206">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="82219-207">當精靈建立好備份排程時，請按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="82219-207">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling-optional"></a><span data-ttu-id="82219-208">啟用網路節流 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="82219-208">Enable network throttling (optional)</span></span>
<span data-ttu-id="82219-209">備份代理程式提供網路節流。</span><span class="sxs-lookup"><span data-stu-id="82219-209">The Backup agent provides network throttling.</span></span> <span data-ttu-id="82219-210">節流會控制資料傳輸期間的網路頻寬使用方式。</span><span class="sxs-lookup"><span data-stu-id="82219-210">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="82219-211">如果您需要在上班時間內備份資料，但不希望備份程序干擾其他網際網路流量，這樣的控制會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="82219-211">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="82219-212">節流適用於備份和還原活動。</span><span class="sxs-lookup"><span data-stu-id="82219-212">Throttling applies to back up and restore activities.</span></span>

<span data-ttu-id="82219-213">**啟用網路節流**</span><span class="sxs-lookup"><span data-stu-id="82219-213">**To enable network throttling**</span></span>

1. <span data-ttu-id="82219-214">在備份代理程式中，按一下 [變更屬性] 。</span><span class="sxs-lookup"><span data-stu-id="82219-214">In the Backup agent, click **Change Properties**.</span></span>

    ![變更屬性](./media/backup-configure-vault-classic/change-properties.png)
2. <span data-ttu-id="82219-216">在 [節流] 索引標籤上，選取 [啟用備份作業的網際網路頻寬使用節流功能] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="82219-216">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![網路節流](./media/backup-configure-vault-classic/throttling-dialog.png)
3. <span data-ttu-id="82219-218">在您啟用節流之後，請指定允許的頻寬進行 [工作時間] 和 [非工作時間] 期間的備份資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="82219-218">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="82219-219">頻寬值從每秒 512 KB (Kbps) 開始，並可高達每秒 1023 MB (Mbps)。</span><span class="sxs-lookup"><span data-stu-id="82219-219">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="82219-220">您也可以指定 [工作時間] 的開始和完成時間，以及一週中有哪幾天視為工作天。</span><span class="sxs-lookup"><span data-stu-id="82219-220">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="82219-221">指定之工作時間以外的時間則視為非工作時間。</span><span class="sxs-lookup"><span data-stu-id="82219-221">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="82219-222">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="82219-222">Click **OK**.</span></span>

### <a name="to-back-up-now"></a><span data-ttu-id="82219-223">立即備份</span><span class="sxs-lookup"><span data-stu-id="82219-223">To back up now</span></span>
1. <span data-ttu-id="82219-224">在備份代理程式中，按一下 [立即備份]  ，以透過網路完成初始植入。</span><span class="sxs-lookup"><span data-stu-id="82219-224">In the Backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server 立即備份](./media/backup-configure-vault-classic/backup-now.png)
2. <span data-ttu-id="82219-226">在 [確認] 頁面上，檢閱立即備份精靈將用於備份電腦的設定。</span><span class="sxs-lookup"><span data-stu-id="82219-226">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="82219-227">然後按一下 [備份] 。</span><span class="sxs-lookup"><span data-stu-id="82219-227">Then click **Back Up**.</span></span>
3. <span data-ttu-id="82219-228">按一下 [關閉]  即可關閉精靈。</span><span class="sxs-lookup"><span data-stu-id="82219-228">Click **Close** to close the wizard.</span></span> <span data-ttu-id="82219-229">如果您在備份程序完成之前關閉精靈，精靈會繼續在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="82219-229">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="82219-230">完成初始備份之後，備份主控台中會顯示 [作業已完成]  狀態。</span><span class="sxs-lookup"><span data-stu-id="82219-230">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR 已完成](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a><span data-ttu-id="82219-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82219-232">Next steps</span></span>
* <span data-ttu-id="82219-233">註冊 [免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="82219-233">Sign up for a [free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="82219-234">如需備份 VM 或其他工作負載的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="82219-234">For additional information about backing up VMs or other workloads, see:</span></span>

* [<span data-ttu-id="82219-235">備份 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="82219-235">Back up IaaS VMs</span></span>](backup-azure-vms-prepare.md)
* [<span data-ttu-id="82219-236">使用 Microsoft Azure 備份伺服器備份工作負載</span><span class="sxs-lookup"><span data-stu-id="82219-236">Back up workloads to Azure with Microsoft Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
* [<span data-ttu-id="82219-237">使用 DPM 將工作負載備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="82219-237">Back up workloads to Azure with DPM</span></span>](backup-azure-dpm-introduction.md)
