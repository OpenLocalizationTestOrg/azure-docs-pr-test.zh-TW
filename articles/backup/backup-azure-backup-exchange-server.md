---
title: "使用 System Center 2012 R2 DPM 備份的 Exchange server tooAzure 向上 aaaBack |Microsoft 文件"
description: "深入了解如何設定 Exchange server tooAzure tooback 備份使用 System Center 2012 R2 DPM"
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
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="2d69d-103">備份 Exchange server tooAzure 使用 System Center 2012 R2 DPM 備份</span><span class="sxs-lookup"><span data-stu-id="2d69d-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="2d69d-104">本文章說明如何設定 Microsoft Exchange server 的 System Center 2012 R2 Data Protection Manager (DPM) 伺服器 tooback tooconfigure 太 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="2d69d-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="2d69d-105">更新</span><span class="sxs-lookup"><span data-stu-id="2d69d-105">Updates</span></span>
<span data-ttu-id="2d69d-106">toosuccessfully 暫存器 hello DPM 伺服器使用 Azure Backup，您必須安裝 hello 最新更新彙總套件 hello Azure Backup Agent 的 System Center 2012 R2 DPM 和 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="2d69d-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="2d69d-107">收到 hello hello 最新的更新彙總[Microsoft 目錄](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager)。</span><span class="sxs-lookup"><span data-stu-id="2d69d-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="2d69d-108">這篇文章中的 hello 範例，版本 2.0.8719.0 hello Azure Backup Agent 已安裝，且 System Center 2012 R2 DPM 上安裝更新彙總套件 6。</span><span class="sxs-lookup"><span data-stu-id="2d69d-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2d69d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d69d-109">Prerequisites</span></span>
<span data-ttu-id="2d69d-110">在繼續之前，請確定所有 hello[必要條件](backup-azure-dpm-introduction.md#prerequisites)tooprotect 工作負載已符合使用 Microsoft Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="2d69d-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="2d69d-111">這些必要條件 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="2d69d-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="2d69d-112">已建立 hello Azure 站台上的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="2d69d-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="2d69d-113">已下載的 toohello DPM 伺服器代理程式和保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="2d69d-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="2d69d-114">hello DPM 伺服器上安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="2d69d-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="2d69d-115">hello 保存庫認證是使用的 tooregister hello DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2d69d-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="2d69d-116">如果您要保護 Exchange 2016，請升級 tooDPM 2012 R2 UR9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="2d69d-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="2d69d-117">DPM 保護代理程式</span><span class="sxs-lookup"><span data-stu-id="2d69d-117">DPM protection agent</span></span>
<span data-ttu-id="2d69d-118">tooinstall hello DPM 保護代理程式在 hello Exchange 伺服器上，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2d69d-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="2d69d-119">請確定已正確設定 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="2d69d-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="2d69d-120">請參閱[設定 hello 代理程式的防火牆例外](https://technet.microsoft.com/library/Hh758204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2d69d-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="2d69d-121">Hello Exchange 伺服器上安裝 hello 代理程式，依序按一下**管理 > 代理程式 > 安裝**DPM 系統管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="2d69d-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="2d69d-122">請參閱[hello DPM 保護代理程式安裝](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396)如需詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="2d69d-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="2d69d-123">建立 hello Exchange 伺服器的保護群組</span><span class="sxs-lookup"><span data-stu-id="2d69d-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="2d69d-124">在 hello DPM 系統管理員主控台中，按一下 **保護**，然後按一下**新增**上 hello 工具功能區 tooopen hello**建立新保護群組**精靈。</span><span class="sxs-lookup"><span data-stu-id="2d69d-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="2d69d-125">在 hello ** 褖畫惎**hello 精靈按一下畫面**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="2d69d-126">在 hello**選取保護群組類型**畫面上，選取**伺服器**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="2d69d-127">您想 tooprotect 並按一下選取的 hello Exchange 伺服器資料庫**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2d69d-128">如果您要保護 Exchange 2013，請檢查 hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2d69d-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="2d69d-129">在下列範例的 hello，會選取 hello Exchange 2010 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d69d-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![選擇群組成員](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="2d69d-131">選取 hello 資料保護方式。</span><span class="sxs-lookup"><span data-stu-id="2d69d-131">Select hello data protection method.</span></span>

    <span data-ttu-id="2d69d-132">名稱 hello 保護群組，然後再選取這兩個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="2d69d-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="2d69d-133">我想要使用磁碟進行短期保護。</span><span class="sxs-lookup"><span data-stu-id="2d69d-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="2d69d-134">我想要線上保護。</span><span class="sxs-lookup"><span data-stu-id="2d69d-134">I want online protection.</span></span>
6. <span data-ttu-id="2d69d-135">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2d69d-135">Click **Next**.</span></span>
7. <span data-ttu-id="2d69d-136">選取 hello**執行 Eseutil toocheck 資料完整性**如果您想 toocheck hello 完整性 hello Exchange Server 資料庫的選項。</span><span class="sxs-lookup"><span data-stu-id="2d69d-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="2d69d-137">選取此選項之後，備份一致性檢查會執行上的 hello DPM 伺服器 tooavoid hello I/O 流量所產生的執行 hello **eseutil** hello Exchange 伺服器上的命令。</span><span class="sxs-lookup"><span data-stu-id="2d69d-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2d69d-138">toouse 選取此選項，您必須複製 hello Ese.dll 和 Eseutil.exe 檔案 toohello hello DPM 伺服器上的 C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin 目錄。</span><span class="sxs-lookup"><span data-stu-id="2d69d-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="2d69d-139">否則，會觸發 hello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="2d69d-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="2d69d-140">![eseutil 錯誤](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="2d69d-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="2d69d-141">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2d69d-141">Click **Next**.</span></span>
9. <span data-ttu-id="2d69d-142">選取 hello 資料庫**複製備份**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2d69d-143">如果您未對資料庫的至少一個 DAG 複本選取「完整備份」，則不會截斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2d69d-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="2d69d-144">設定目標 hello**短期備份**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="2d69d-145">檢閱 hello 可用磁碟空間，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="2d69d-146">選取 hello 時間在哪一個 hello DPM 伺服器將會建立 hello 初始複寫，並按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="2d69d-147">選取 hello 一致性檢查選項，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="2d69d-148">選擇您想要向上 tooAzure，tooback，然後按一下 hello 資料庫**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="2d69d-149">例如：</span><span class="sxs-lookup"><span data-stu-id="2d69d-149">For example:</span></span>

    ![指定線上保護資料](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="2d69d-151">定義 hello 排程**Azure Backup**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="2d69d-152">例如：</span><span class="sxs-lookup"><span data-stu-id="2d69d-152">For example:</span></span>

    ![指定線上備份排程](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="2d69d-154">請注意，線上復原點是以快速完整復原點為基礎。</span><span class="sxs-lookup"><span data-stu-id="2d69d-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="2d69d-155">因此，您必須排程 hello 線上復原點之後所指定的 hello 的 hello 時間表達完整的復原點。</span><span class="sxs-lookup"><span data-stu-id="2d69d-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="2d69d-156">設定保留原則 hello **Azure Backup**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="2d69d-157">選擇線上複寫選項並按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2d69d-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="2d69d-158">如果您有大型的資料庫時，可能需要很長的時間 hello 初始備份 toobe hello 網路上建立。</span><span class="sxs-lookup"><span data-stu-id="2d69d-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="2d69d-159">tooavoid 此問題，您可以建立離線備份。</span><span class="sxs-lookup"><span data-stu-id="2d69d-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![指定線上保留期原則](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="2d69d-161">確認 hello 設定，然後按一下**建立群組**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="2d69d-162">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="2d69d-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="2d69d-163">Hello Exchange 資料庫復原</span><span class="sxs-lookup"><span data-stu-id="2d69d-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="2d69d-164">toorecover Exchange 資料庫，按一下**復原**hello DPM 系統管理員主控台中。</span><span class="sxs-lookup"><span data-stu-id="2d69d-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="2d69d-165">找出您想 toorecover hello Exchange 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d69d-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="2d69d-166">選取 線上復原點從 hello*復原時間*下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="2d69d-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="2d69d-167">按一下**復原**toostart hello**復原精靈**。</span><span class="sxs-lookup"><span data-stu-id="2d69d-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="2d69d-168">線上復原點有五種復原類型：</span><span class="sxs-lookup"><span data-stu-id="2d69d-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="2d69d-169">**復原 toooriginal Exchange Server 位置：** hello 資料將會復原的 toohello 原始 Exchange server。</span><span class="sxs-lookup"><span data-stu-id="2d69d-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="2d69d-170">**復原 Exchange Server 上的 tooanother 資料庫：** hello 資料將會復原的 tooanother 另一部 Exchange 伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d69d-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="2d69d-171">**復原 tooa 復原資料庫：** hello 資料將會復原的 tooan Exchange 復原資料庫 (RDB)。</span><span class="sxs-lookup"><span data-stu-id="2d69d-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="2d69d-172">**複製 tooa 網路資料夾：** hello 資料將會復原的 tooa 網路資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d69d-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="2d69d-173">**複製 tootape:**如果您有任何磁帶媒體櫃或獨立磁帶機，將會附加，且設定在 hello DPM 伺服器，hello 復原點複製 tooa 可用磁帶。</span><span class="sxs-lookup"><span data-stu-id="2d69d-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![選擇線上複寫](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="2d69d-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d69d-175">Next steps</span></span>
* [<span data-ttu-id="2d69d-176">Azure 備份常見問題集</span><span class="sxs-lookup"><span data-stu-id="2d69d-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
