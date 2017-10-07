---
title: "設定 Windows 伺服器或工作站 tooAzure （傳統模型） aaaBack |Microsoft 文件"
description: "備份 Windows 伺服器或用戶端 tooa 備份保存庫在 Azure 中。 通過基本概念，來保護檔案和資料夾 tooa 備份保存庫使用 hello Azure Backup agent。"
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
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a><span data-ttu-id="bfbee-105">備份使用 hello 傳統入口網站的 Windows 伺服器或工作站 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bfbee-105">Back up a Windows server or workstation tooAzure using hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfbee-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="bfbee-106">Classic portal</span></span>](backup-configure-vault-classic.md)
> * [<span data-ttu-id="bfbee-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bfbee-107">Azure portal</span></span>](backup-configure-vault.md)
>
>

<span data-ttu-id="bfbee-108">本文涵蓋 hello 程序，您需要 toofollow tooprepare 您的環境，並將 Windows 伺服器 （或工作站） tooAzure 備份。</span><span class="sxs-lookup"><span data-stu-id="bfbee-108">This article covers hello procedures that you need toofollow tooprepare your environment and back up a Windows server (or workstation) tooAzure.</span></span> <span data-ttu-id="bfbee-109">它還涵蓋部署備份解決方案的考量。</span><span class="sxs-lookup"><span data-stu-id="bfbee-109">It also covers considerations for deploying your backup solution.</span></span> <span data-ttu-id="bfbee-110">如果您想要在第一次嘗試 hello Azure 備份，這篇文章快速引導您 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="bfbee-110">If you're interested in trying Azure Backup for hello first time, this article quickly walks you through hello process.</span></span>

<span data-ttu-id="bfbee-111">Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。</span><span class="sxs-lookup"><span data-stu-id="bfbee-111">Azure has two different deployment models for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="bfbee-112">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="bfbee-112">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="bfbee-113">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="bfbee-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="bfbee-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="bfbee-114">Before you start</span></span>
<span data-ttu-id="bfbee-115">伺服器或用戶端 tooAzure tooback，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbee-115">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="bfbee-116">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="bfbee-116">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-backup-vault"></a><span data-ttu-id="bfbee-117">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="bfbee-117">Create a backup vault</span></span>
<span data-ttu-id="bfbee-118">tooback 檔案及資料夾從伺服器或用戶端，您需要 toocreate hello toostore hello 資料所在的地理區域的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-118">tooback up files and folders from a server or client, you need toocreate a backup vault in hello geographic region where you want toostore hello data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfbee-119">從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-119">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="bfbee-120">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-120">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="bfbee-121">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="bfbee-121">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="bfbee-122">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-122">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="bfbee-123">**2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-123">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="bfbee-124">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="bfbee-124">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="bfbee-125">任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-125">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="bfbee-126">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="bfbee-126">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="bfbee-127">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="bfbee-127">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>


## <a name="download-hello-vault-credential-file"></a><span data-ttu-id="bfbee-128">下載 hello 保存庫認證檔案</span><span class="sxs-lookup"><span data-stu-id="bfbee-128">Download hello vault credential file</span></span>
<span data-ttu-id="bfbee-129">必須先驗證用戶端向備份保存庫可以備份資料 tooAzure toobe hello 在內部部署的機器。</span><span class="sxs-lookup"><span data-stu-id="bfbee-129">hello on-premises machine needs toobe authenticated with a backup vault before it can back up data tooAzure.</span></span> <span data-ttu-id="bfbee-130">hello 驗證透過來達成*保存庫認證*。</span><span class="sxs-lookup"><span data-stu-id="bfbee-130">hello authentication is achieved through *vault credentials*.</span></span> <span data-ttu-id="bfbee-131">透過從 hello 傳統入口網站的安全通道會下載 hello 保存庫認證檔案。</span><span class="sxs-lookup"><span data-stu-id="bfbee-131">hello vault credential file is downloaded through a secure channel from hello classic portal.</span></span> <span data-ttu-id="bfbee-132">hello 憑證私密金鑰不會保存在 hello 入口網站或 hello 服務中。</span><span class="sxs-lookup"><span data-stu-id="bfbee-132">hello certificate private key does not persist in hello portal or hello service.</span></span>

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a><span data-ttu-id="bfbee-133">toodownload hello 保存庫認證檔案 tooa 本機電腦</span><span class="sxs-lookup"><span data-stu-id="bfbee-133">toodownload hello vault credential file tooa local machine</span></span>
1. <span data-ttu-id="bfbee-134">在 hello 左側瀏覽窗格中，按一下 **復原服務**，然後選取您所建立的 hello 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-134">In hello left navigation pane, click **Recovery Services**, and then select hello backup vault that you created.</span></span>

    ![IR 已完成](./media/backup-configure-vault-classic/rs-left-nav.png)
2. <span data-ttu-id="bfbee-136">在 hello 快速入門 頁面上，按一下 **下載保存庫認證**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-136">On hello Quick Start page, click **Download vault credentials**.</span></span>

   <span data-ttu-id="bfbee-137">hello 傳統入口網站會使用組合的 hello 保存庫名稱和 hello 目前的日期，以產生保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="bfbee-137">hello classic portal generates a vault credential by using a combination of hello vault name and hello current date.</span></span> <span data-ttu-id="bfbee-138">hello 保存庫認證檔案 hello 註冊工作流程期間只會使用，且 48 小時後到期。</span><span class="sxs-lookup"><span data-stu-id="bfbee-138">hello vault credentials file is used only during hello registration workflow and expires after 48 hours.</span></span>

   <span data-ttu-id="bfbee-139">hello 保存庫認證檔案可以從 hello 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="bfbee-139">hello vault credential file can be downloaded from hello portal.</span></span>
3. <span data-ttu-id="bfbee-140">按一下**儲存**toodownload hello 保存庫認證檔案 toohello 下載 資料夾的 hello 本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="bfbee-140">Click **Save** toodownload hello vault credential file toohello Downloads folder of hello local account.</span></span> <span data-ttu-id="bfbee-141">您也可以選取**存**從 hello**儲存**功能表 toospecify hello 保存庫認證檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="bfbee-141">You can also select **Save As** from hello **Save** menu toospecify a location for hello vault credential file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bfbee-142">請確定 hello 保存庫認證檔案會儲存在可從您的電腦存取的位置。</span><span class="sxs-lookup"><span data-stu-id="bfbee-142">Make sure hello vault credential file is saved in a location that can be accessed from your machine.</span></span> <span data-ttu-id="bfbee-143">如果它儲存在檔案共用或伺服器訊息區塊，確認您擁有 hello 權限 tooaccess 它。</span><span class="sxs-lookup"><span data-stu-id="bfbee-143">If it is stored in a file share or server message block, verify that you have hello permissions tooaccess it.</span></span>
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a><span data-ttu-id="bfbee-144">下載、 安裝及註冊 hello 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="bfbee-144">Download, install, and register hello Backup agent</span></span>
<span data-ttu-id="bfbee-145">您建立備份保存庫 hello 和下載 hello 保存庫認證檔案之後，代理程式必須安裝在每一部 Windows 電腦上。</span><span class="sxs-lookup"><span data-stu-id="bfbee-145">After you create hello backup vault and download hello vault credential file, an agent must be installed on each of your Windows machines.</span></span>

### <a name="toodownload-install-and-register-hello-agent"></a><span data-ttu-id="bfbee-146">toodownload，安裝及註冊 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="bfbee-146">toodownload, install, and register hello agent</span></span>
1. <span data-ttu-id="bfbee-147">按一下**復原服務**，然後選取您想要與伺服器 tooregister hello 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="bfbee-147">Click **Recovery Services**, and then select hello backup vault that you want tooregister with a server.</span></span>
2. <span data-ttu-id="bfbee-148">在 hello 快速入門] 頁面上，按一下 [hello 代理程式**代理程式適用於 Windows Server 或 System Center Data Protection Manager 或 Windows 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-148">On hello Quick Start page, click hello agent **Agent for Windows Server or System Center Data Protection Manager or Windows client**.</span></span> <span data-ttu-id="bfbee-149">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bfbee-149">Then click **Save**.</span></span>

    ![儲存代理程式](./media/backup-configure-vault-classic/agent.png)
3. <span data-ttu-id="bfbee-151">Hello MARSagentinstaller.exe 檔案下載之後，請按一下**執行**(或按兩下**MARSAgentInstaller.exe**從 hello 儲存位置)。</span><span class="sxs-lookup"><span data-stu-id="bfbee-151">After hello MARSagentinstaller.exe file has downloaded, click **Run** (or double-click **MARSAgentInstaller.exe** from hello saved location).</span></span>
4. <span data-ttu-id="bfbee-152">選擇 hello 安裝資料夾，以及所需的 hello 代理程式，快取資料夾，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-152">Choose hello installation folder and cache folder that are required for hello agent, and then click **Next**.</span></span> <span data-ttu-id="bfbee-153">您指定的 hello 快取位置必須有可用空間等於 tooat hello 備份資料的最少 5%。</span><span class="sxs-lookup"><span data-stu-id="bfbee-153">hello cache location you specify must have free space equal tooat least 5 percent of hello backup data.</span></span>
5. <span data-ttu-id="bfbee-154">您可以繼續 tooconnect toohello 網際網路透過 hello 預設 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="bfbee-154">You can continue tooconnect toohello Internet through hello default proxy settings.</span></span>             <span data-ttu-id="bfbee-155">如果您使用 proxy 伺服器 tooconnect toohello 網際網路，hello Proxy 組態 頁面上，選取 hello**使用自訂 proxy 設定**核取方塊，，，然後輸入 hello proxy 伺服器的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bfbee-155">If you use a proxy server tooconnect toohello Internet, on hello Proxy Configuration page, select hello **Use custom proxy settings** check box, and then enter hello proxy server details.</span></span> <span data-ttu-id="bfbee-156">如果您使用驗證的 proxy 時，輸入 hello 使用者名稱和密碼的詳細資訊，，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-156">If you use an authenticated proxy, enter hello user name and password details, and then click **Next**.</span></span>
6. <span data-ttu-id="bfbee-157">按一下**安裝**toobegin hello 代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="bfbee-157">Click **Install** toobegin hello agent installation.</span></span> <span data-ttu-id="bfbee-158">hello 備份代理程式安裝.NET Framework 4.5 和 Windows PowerShell （如果尚未安裝） toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="bfbee-158">hello Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not already installed) toocomplete hello installation.</span></span>
7. <span data-ttu-id="bfbee-159">Hello 代理程式安裝之後，請按一下**繼續 tooRegistration** toocontinue 與 hello 的工作流程。</span><span class="sxs-lookup"><span data-stu-id="bfbee-159">After hello agent is installed, click **Proceed tooRegistration** toocontinue with hello workflow.</span></span>
8. <span data-ttu-id="bfbee-160">在 hello 保存庫識別 頁面上，瀏覽 tooand 選取 hello 保存庫認證檔案，您先前下載。</span><span class="sxs-lookup"><span data-stu-id="bfbee-160">On hello Vault Identification page, browse tooand select hello vault credential file that you previously downloaded.</span></span>

    <span data-ttu-id="bfbee-161">hello 保存庫認證檔案無效只 48 個小時之後從 hello 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="bfbee-161">hello vault credential file is valid for only 48 hours after it’s downloaded from hello portal.</span></span> <span data-ttu-id="bfbee-162">如果您遇到錯誤，在此頁面 （例如 「 保存庫認證檔案，提供已過期 」），登入 toohello 入口網站，並再次下載 hello 保存庫認證檔案。</span><span class="sxs-lookup"><span data-stu-id="bfbee-162">If you encounter an error on this page (such as “Vault credentials file provided has expired”), sign in toohello portal and download hello vault credential file again.</span></span>

    <span data-ttu-id="bfbee-163">確定該 hello 保存庫認證檔案可用在 hello 安裝應用程式可以存取的位置。</span><span class="sxs-lookup"><span data-stu-id="bfbee-163">Ensure that hello vault credential file is available in a location that can be accessed by hello setup application.</span></span> <span data-ttu-id="bfbee-164">如果您遇到與存取相關的錯誤，將複製 hello 保存庫認證檔 tooa 暫存位置的相同電腦，然後重試 hello 作業 hello。</span><span class="sxs-lookup"><span data-stu-id="bfbee-164">If you encounter access-related errors, copy hello vault credential file tooa temporary location on hello same machine and retry hello operation.</span></span>

    <span data-ttu-id="bfbee-165">如果您遇到的保存庫認證錯誤，例如 「 無效的保存庫認證提供 」，hello 檔案已損毀，或沒有不 hello 與 hello 復原服務相關聯的最新認證。</span><span class="sxs-lookup"><span data-stu-id="bfbee-165">If you encounter a vault credential error such as “Invalid vault credentials provided," hello file is damaged or does not have hello latest credentials associated with hello recovery service.</span></span> <span data-ttu-id="bfbee-166">Hello 作業之後從 hello 入口網站下載新的保存庫認證檔案重試一次。</span><span class="sxs-lookup"><span data-stu-id="bfbee-166">Retry hello operation after downloading a new vault credential file from hello portal.</span></span> <span data-ttu-id="bfbee-167">如果使用者按一下 hello，也會發生此錯誤**下載保存庫認證**中快速且連續數次的選項。</span><span class="sxs-lookup"><span data-stu-id="bfbee-167">This error can also occur if a user clicks hello **Download vault credential** option several times in quick succession.</span></span> <span data-ttu-id="bfbee-168">在此情況下，只有 hello 最後一個保存庫認證檔案無效。</span><span class="sxs-lookup"><span data-stu-id="bfbee-168">In this case, only hello last vault credential file is valid.</span></span>
9. <span data-ttu-id="bfbee-169">在 hello 加密設定 頁面上，您可以產生複雜密碼，或提供複雜密碼 （至最少 16 個字元）。</span><span class="sxs-lookup"><span data-stu-id="bfbee-169">On hello Encryption Setting page, you can either generate a passphrase or provide a passphrase (with a minimum of 16 characters).</span></span> <span data-ttu-id="bfbee-170">請記住 toosave hello 複雜密碼，在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="bfbee-170">Remember toosave hello passphrase in a secure location.</span></span>
10. <span data-ttu-id="bfbee-171">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="bfbee-171">Click **Finish**.</span></span> <span data-ttu-id="bfbee-172">hello 註冊伺服器精靈 」 會登錄 hello 伺服器備份。</span><span class="sxs-lookup"><span data-stu-id="bfbee-172">hello Register Server Wizard registers hello server with Backup.</span></span>

    > [!WARNING]
    > <span data-ttu-id="bfbee-173">如果您遺失或忘記 hello 複雜密碼時，Microsoft 無法協助您復原 hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="bfbee-173">If you lose or forget hello passphrase, Microsoft cannot help you recover hello backup data.</span></span> <span data-ttu-id="bfbee-174">您擁有 hello 加密複雜密碼，而 Microsoft 並沒有您所使用的 hello 複雜密碼的可視性。</span><span class="sxs-lookup"><span data-stu-id="bfbee-174">You own hello encryption passphrase, and Microsoft does not have visibility into hello passphrase that you use.</span></span> <span data-ttu-id="bfbee-175">因為它會在需要復原作業期間，請將 hello 檔案儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="bfbee-175">Save hello file in a secure location because it will be required during a recovery operation.</span></span>
    >
    >

11. <span data-ttu-id="bfbee-176">設定 hello 加密金鑰之後，保留 hello**啟動 Microsoft Azure Recovery Services Agent**核取方塊，然後**關閉**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-176">After hello encryption key is set, leave hello **Launch Microsoft Azure Recovery Services Agent** check box selected, and then click **Close**.</span></span>

## <a name="complete-hello-initial-backup"></a><span data-ttu-id="bfbee-177">完整的 hello 初始備份</span><span class="sxs-lookup"><span data-stu-id="bfbee-177">Complete hello initial backup</span></span>
<span data-ttu-id="bfbee-178">hello 初始備份包含兩個主要工作：</span><span class="sxs-lookup"><span data-stu-id="bfbee-178">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="bfbee-179">正在建立 hello 備份排程</span><span class="sxs-lookup"><span data-stu-id="bfbee-179">Creating hello backup schedule</span></span>
* <span data-ttu-id="bfbee-180">備份檔案和資料夾進行 hello 第一次</span><span class="sxs-lookup"><span data-stu-id="bfbee-180">Backing up files and folders for hello first time</span></span>

<span data-ttu-id="bfbee-181">Hello 備份原則完成 hello 初始備份之後，它會建立您需要 toorecover hello 資料時，您可使用的備份點。</span><span class="sxs-lookup"><span data-stu-id="bfbee-181">After hello backup policy completes hello initial backup, it creates backup points that you can use if you need toorecover hello data.</span></span> <span data-ttu-id="bfbee-182">hello 備份原則會根據您定義的 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="bfbee-182">hello backup policy does this based on hello schedule that you define.</span></span>

### <a name="tooschedule-hello-backup"></a><span data-ttu-id="bfbee-183">tooschedule hello 備份</span><span class="sxs-lookup"><span data-stu-id="bfbee-183">tooschedule hello backup</span></span>
1. <span data-ttu-id="bfbee-184">開啟 hello Microsoft Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="bfbee-184">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="bfbee-185">(它會開啟自動保留 hello**啟動 Microsoft Azure Recovery Services Agent**關閉 hello 註冊伺服器精靈時選取核取方塊。)您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。</span><span class="sxs-lookup"><span data-stu-id="bfbee-185">(It will open automatically if you left hello **Launch Microsoft Azure Recovery Services Agent** check box selected when you closed hello Register Server Wizard.) You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![啟動 hello Azure 備份代理程式](./media/backup-configure-vault-classic/snap-in-search.png)
2. <span data-ttu-id="bfbee-187">在 hello 備份代理程式，按一下 **排程備份**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-187">In hello Backup agent, click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. <span data-ttu-id="bfbee-189">在 [hello 上開始使用 hello 排程備份精靈] 頁面中，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-189">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="bfbee-190">在 hello 選取項目 tooBackup 頁面上，按一下 **新增的項目**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-190">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="bfbee-191">選取 hello 檔案和資料夾，您想 tooback、，然後按一下**好**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-191">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="bfbee-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bfbee-192">Click **Next**.</span></span>
7. <span data-ttu-id="bfbee-193">在 hello**指定備份排程**頁面上，指定 hello**備份排程**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-193">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="bfbee-194">您可以排程每日 (一天最多三次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="bfbee-194">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="bfbee-196">如需有關如何 toospecify hello 備份排程的詳細資訊，請參閱 hello 文章[使用 Azure Backup tooreplace 磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="bfbee-196">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="bfbee-197">在 hello**選取保留原則**頁面上，選取 hello**保留原則**為 hello 備份副本。</span><span class="sxs-lookup"><span data-stu-id="bfbee-197">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="bfbee-198">hello 保留原則會指定儲存 hello 備份 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="bfbee-198">hello retention policy specifies hello duration for which hello backup will be stored.</span></span> <span data-ttu-id="bfbee-199">而不是只指定 「 一般原則 」 的所有備份的點，您可以指定不同的保留原則根據 hello 備份發生時。</span><span class="sxs-lookup"><span data-stu-id="bfbee-199">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="bfbee-200">您可以修改 hello 每日、 每週、 每月和每年保留原則 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="bfbee-200">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="bfbee-201">在 [hello 選擇初始備份類型] 頁面上，選擇 hello 初始備份類型。</span><span class="sxs-lookup"><span data-stu-id="bfbee-201">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="bfbee-202">保留 hello 選項**自動透過網路 hello**選取，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-202">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="bfbee-203">您可以備份自動 hello 網路上或您可以離線備份。</span><span class="sxs-lookup"><span data-stu-id="bfbee-203">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="bfbee-204">hello 本文其餘部分說明 hello 程序會自動備份。</span><span class="sxs-lookup"><span data-stu-id="bfbee-204">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="bfbee-205">如果您偏好 toodo 離線備份，請檢閱 hello 文件[Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bfbee-205">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="bfbee-206">在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-206">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="bfbee-207">Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-207">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling-optional"></a><span data-ttu-id="bfbee-208">啟用網路節流 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="bfbee-208">Enable network throttling (optional)</span></span>
<span data-ttu-id="bfbee-209">hello 備份代理程式會提供網路節流設定。</span><span class="sxs-lookup"><span data-stu-id="bfbee-209">hello Backup agent provides network throttling.</span></span> <span data-ttu-id="bfbee-210">節流會控制資料傳輸期間的網路頻寬使用方式。</span><span class="sxs-lookup"><span data-stu-id="bfbee-210">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="bfbee-211">如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="bfbee-211">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="bfbee-212">節流設定會套用 tooback 和還原活動。</span><span class="sxs-lookup"><span data-stu-id="bfbee-212">Throttling applies tooback up and restore activities.</span></span>

<span data-ttu-id="bfbee-213">**tooenable 網路節流設定**</span><span class="sxs-lookup"><span data-stu-id="bfbee-213">**tooenable network throttling**</span></span>

1. <span data-ttu-id="bfbee-214">在 hello 備份代理程式，按一下 **變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-214">In hello Backup agent, click **Change Properties**.</span></span>

    ![變更屬性](./media/backup-configure-vault-classic/change-properties.png)
2. <span data-ttu-id="bfbee-216">在 hello**節流**索引標籤，選取 hello**啟用網際網路頻寬使用節流設定的備份操作**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="bfbee-216">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![網路節流](./media/backup-configure-vault-classic/throttling-dialog.png)
3. <span data-ttu-id="bfbee-218">啟用節流設定後，指定允許的頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。</span><span class="sxs-lookup"><span data-stu-id="bfbee-218">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="bfbee-219">hello 頻寬值開始每秒 (Kbps) 為 512 kb，最高 too1，023 mb / 秒 (MBps)。</span><span class="sxs-lookup"><span data-stu-id="bfbee-219">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="bfbee-220">也可以指定 hello 開始和完成**上班**，和 hello 一週的哪幾天都視為的工作日。</span><span class="sxs-lookup"><span data-stu-id="bfbee-220">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="bfbee-221">指定之工作時間以外的時間則視為非工作時間。</span><span class="sxs-lookup"><span data-stu-id="bfbee-221">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="bfbee-222">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bfbee-222">Click **OK**.</span></span>

### <a name="tooback-up-now"></a><span data-ttu-id="bfbee-223">現在向上 tooback</span><span class="sxs-lookup"><span data-stu-id="bfbee-223">tooback up now</span></span>
1. <span data-ttu-id="bfbee-224">在 hello 備份代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="bfbee-224">In hello Backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server 立即備份](./media/backup-configure-vault-classic/backup-now.png)
2. <span data-ttu-id="bfbee-226">在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。</span><span class="sxs-lookup"><span data-stu-id="bfbee-226">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="bfbee-227">然後按一下 [備份] 。</span><span class="sxs-lookup"><span data-stu-id="bfbee-227">Then click **Back Up**.</span></span>
3. <span data-ttu-id="bfbee-228">按一下**關閉**tooclose hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="bfbee-228">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="bfbee-229">如果 hello 備份程序完成之前，您可以這樣做，hello 精靈會繼續 toorun hello 背景。</span><span class="sxs-lookup"><span data-stu-id="bfbee-229">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="bfbee-230">Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。</span><span class="sxs-lookup"><span data-stu-id="bfbee-230">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR 已完成](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a><span data-ttu-id="bfbee-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bfbee-232">Next steps</span></span>
* <span data-ttu-id="bfbee-233">註冊 [免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="bfbee-233">Sign up for a [free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="bfbee-234">如需備份 VM 或其他工作負載的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="bfbee-234">For additional information about backing up VMs or other workloads, see:</span></span>

* [<span data-ttu-id="bfbee-235">備份 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="bfbee-235">Back up IaaS VMs</span></span>](backup-azure-vms-prepare.md)
* [<span data-ttu-id="bfbee-236">備份工作負載 tooAzure 與 Microsoft Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="bfbee-236">Back up workloads tooAzure with Microsoft Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
* [<span data-ttu-id="bfbee-237">備份與 DPM 工作負載 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bfbee-237">Back up workloads tooAzure with DPM</span></span>](backup-azure-dpm-introduction.md)
