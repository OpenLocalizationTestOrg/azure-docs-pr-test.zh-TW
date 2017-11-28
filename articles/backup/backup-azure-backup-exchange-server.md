---
title: "使用 System Center 2012 R2 DPM 將 Exchange Server 備份至 Azure 備份 | Microsoft Docs"
description: "了解如何使用 System Center 2012 R2 DPM 將 Exchange Server 備份至 Azure 備份"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="13253-103">使用 System Center 2012 R2 DPM 將 Exchange Server 備份至 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="13253-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="13253-104">本文說明如何設定 System Center 2012 R2 Data Protection Manager (DPM) 伺服器，以將 Microsoft Exchange Server 備份至 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="13253-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="13253-105">更新</span><span class="sxs-lookup"><span data-stu-id="13253-105">Updates</span></span>
<span data-ttu-id="13253-106">若要在 Azure 備份中成功註冊 DPM 伺服器，您必須安裝 System Center 2012 R2 DPM 的最新更新彙總套件和 Azure 備份代理程式的最新版本。</span><span class="sxs-lookup"><span data-stu-id="13253-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="13253-107">從 [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager)取得最新的更新彙總套件。</span><span class="sxs-lookup"><span data-stu-id="13253-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="13253-108">對於本文中的範例，會安裝 Azure 備份代理程式的 2.0.8719.0 版，而更新彙總套件 6 會安裝於 System Center 2012 R2 DPM。</span><span class="sxs-lookup"><span data-stu-id="13253-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="13253-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="13253-109">Prerequisites</span></span>
<span data-ttu-id="13253-110">繼續之前，請確定符合使用 Microsoft Azure 備份保護工作負載的所有 [必要條件](backup-azure-dpm-introduction.md#prerequisites) 。</span><span class="sxs-lookup"><span data-stu-id="13253-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="13253-111">這些先決條件包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="13253-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="13253-112">已在 Azure 網站上建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="13253-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="13253-113">代理程式和保存庫認證已下載至 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="13253-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="13253-114">代理程式已安裝於 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="13253-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="13253-115">保存庫認證已用來註冊 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="13253-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="13253-116">如果您要保護 Exchange 2016，請升級為 DPM 2012 R2 UR9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="13253-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="13253-117">DPM 保護代理程式</span><span class="sxs-lookup"><span data-stu-id="13253-117">DPM protection agent</span></span>
<span data-ttu-id="13253-118">若要在 Exchange Server 上安裝 DPM 保護代理程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="13253-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="13253-119">請確定已正確設定防火牆。</span><span class="sxs-lookup"><span data-stu-id="13253-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="13253-120">請參閱 [設定代理程式的防火牆例外狀況](https://technet.microsoft.com/library/Hh758204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="13253-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="13253-121">按一下 DPM 系統管理員主控台中的 [管理] > [代理程式] > [安裝]，在 Exchange Server 上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="13253-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="13253-122">如需詳細步驟，請參閱 [安裝 DPM 保護代理程式](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) 。</span><span class="sxs-lookup"><span data-stu-id="13253-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="13253-123">建立 Exchange Server 的保護群組</span><span class="sxs-lookup"><span data-stu-id="13253-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="13253-124">在 DPM 系統管理員主控台中，按一下 [保護]，然後按一下工具功能區上的 [新增]，以開啟 [建立新保護群組] 精靈。</span><span class="sxs-lookup"><span data-stu-id="13253-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="13253-125">在精靈的 [歡迎使用] 畫面上按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="13253-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="13253-126">在 [選取保護群組類型] 畫面上，選取 [伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="13253-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="13253-127">選取您想要保護的 Exchange Server 資料庫，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13253-128">如果您要保護 Exchange 2013，請檢查 [Exchange 2013 先決條件](https://technet.microsoft.com/library/dn751029.aspx)。</span><span class="sxs-lookup"><span data-stu-id="13253-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="13253-129">下例中選取了Exchange 2010 資料庫。</span><span class="sxs-lookup"><span data-stu-id="13253-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![選擇群組成員](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="13253-131">選取資料保護方式。</span><span class="sxs-lookup"><span data-stu-id="13253-131">Select the data protection method.</span></span>

    <span data-ttu-id="13253-132">替保護群組命名，然後選取下列兩個選項：</span><span class="sxs-lookup"><span data-stu-id="13253-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="13253-133">我想要使用磁碟進行短期保護。</span><span class="sxs-lookup"><span data-stu-id="13253-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="13253-134">我想要線上保護。</span><span class="sxs-lookup"><span data-stu-id="13253-134">I want online protection.</span></span>
6. <span data-ttu-id="13253-135">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-135">Click **Next**.</span></span>
7. <span data-ttu-id="13253-136">如果您想要檢查 Exchange Server 資料庫的完整性，請選取 [執行 Eseutil 以檢查資料完整性]  選項。</span><span class="sxs-lookup"><span data-stu-id="13253-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="13253-137">選取此選項之後，將會在 DPM 伺服器上執行備份一致性檢查，以避免在 Exchange Server 上執行 **eseutil** 命令所產生的 I/O 流量。</span><span class="sxs-lookup"><span data-stu-id="13253-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13253-138">若要使用此選項，您必須將 Ese.dll 和 Eseutil.exe 檔案複製到 DPM 伺服器上的 C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin 目錄。</span><span class="sxs-lookup"><span data-stu-id="13253-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="13253-139">否則會觸發下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="13253-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="13253-140">![eseutil 錯誤](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="13253-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="13253-141">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-141">Click **Next**.</span></span>
9. <span data-ttu-id="13253-142">選取用於 [複製備份] 的資料庫，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="13253-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="13253-143">如果您未對資料庫的至少一個 DAG 複本選取「完整備份」，則不會截斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13253-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="13253-144">設定 [短期備份] 的目標，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="13253-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="13253-145">檢閱可用的磁碟空間，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="13253-146">選取 DPM 伺服器將建立初始複寫的時間，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="13253-147">選取一致性檢查選項，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="13253-148">選擇您要備份至 Azure 資料庫，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="13253-149">例如：</span><span class="sxs-lookup"><span data-stu-id="13253-149">For example:</span></span>

    ![指定線上保護資料](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="13253-151">定義 [Azure 備份] 的排程，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="13253-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="13253-152">例如：</span><span class="sxs-lookup"><span data-stu-id="13253-152">For example:</span></span>

    ![指定線上備份排程](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="13253-154">請注意，線上復原點是以快速完整復原點為基礎。</span><span class="sxs-lookup"><span data-stu-id="13253-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="13253-155">因此，您必須將線上復原點排程在針對快速完整復原點指定的時間之後。</span><span class="sxs-lookup"><span data-stu-id="13253-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="13253-156">設定 [Azure 備份] 的保留原則，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="13253-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="13253-157">選擇線上複寫選項並按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="13253-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="13253-158">如果您有大型資料庫，則透過網路建立初始備份所需的時間很長。</span><span class="sxs-lookup"><span data-stu-id="13253-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="13253-159">若要避免這個問題，您可以建立離線備份。</span><span class="sxs-lookup"><span data-stu-id="13253-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![指定線上保留期原則](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="13253-161">確認設定，然後按一下 [建立群組] 。</span><span class="sxs-lookup"><span data-stu-id="13253-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="13253-162">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="13253-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="13253-163">復原 Exchange 資料庫</span><span class="sxs-lookup"><span data-stu-id="13253-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="13253-164">若要復原 Exchange 資料庫，請按一下 DPM 系統管理員主控台中的 [復原]  。</span><span class="sxs-lookup"><span data-stu-id="13253-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="13253-165">找出您要復原的 Exchange 資料庫。</span><span class="sxs-lookup"><span data-stu-id="13253-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="13253-166">從「復原時間」  下拉式清單選取線上復原點。</span><span class="sxs-lookup"><span data-stu-id="13253-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="13253-167">按一下 [復原] 啟動 [復原精靈]。</span><span class="sxs-lookup"><span data-stu-id="13253-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="13253-168">線上復原點有五種復原類型：</span><span class="sxs-lookup"><span data-stu-id="13253-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="13253-169">**復原到原始 Exchange Server 位置：** 資料將會還原到原始 Exchange Server。</span><span class="sxs-lookup"><span data-stu-id="13253-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="13253-170">**復原到 Exchange Server 上的其他資料庫：** 資料將會還原到其他 Exchange Server 上的其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="13253-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="13253-171">**復原到復原資料庫：** 資料將會復原到 Exchange 復原資料庫 (RDB)。</span><span class="sxs-lookup"><span data-stu-id="13253-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="13253-172">**複製到網路資料夾：** 資料將會還原到網路資料夾。</span><span class="sxs-lookup"><span data-stu-id="13253-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="13253-173">**複製到磁帶：** 如果您有磁帶媒體櫃或獨立磁帶機連接並設定於 DPM 伺服器，則復原點將會複製到可用的磁帶。</span><span class="sxs-lookup"><span data-stu-id="13253-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![選擇線上複寫](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="13253-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13253-175">Next steps</span></span>
* [<span data-ttu-id="13253-176">Azure 備份常見問題集</span><span class="sxs-lookup"><span data-stu-id="13253-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
