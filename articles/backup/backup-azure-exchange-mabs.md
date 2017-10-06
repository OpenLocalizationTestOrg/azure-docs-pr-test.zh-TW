---
title: "使用 Azure 備份伺服器備份的 Exchange server tooAzure 向上 aaaBack |Microsoft 文件"
description: "深入了解如何設定 Exchange server tooAzure tooback 備份使用 Azure 備份伺服器"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="0403a-103">備份 Exchange server tooAzure 使用 Azure 備份伺服器備份</span><span class="sxs-lookup"><span data-stu-id="0403a-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="0403a-104">本文說明如何設定 Microsoft Exchange server tooAzure tooconfigure Microsoft Azure 備份伺服器 (MABS) tooback。</span><span class="sxs-lookup"><span data-stu-id="0403a-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="0403a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="0403a-105">Prerequisites</span></span>
<span data-ttu-id="0403a-106">繼續之前，請確定已[安裝並備妥](backup-azure-microsoft-azure-backup.md) Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="0403a-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="0403a-107">MABS 保護代理程式</span><span class="sxs-lookup"><span data-stu-id="0403a-107">MABS protection agent</span></span>
<span data-ttu-id="0403a-108">tooinstall hello MABS 保護代理程式在 hello Exchange 伺服器上，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0403a-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="0403a-109">請確定已正確設定 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="0403a-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="0403a-110">請參閱[設定 hello 代理程式的防火牆例外](https://technet.microsoft.com/library/Hh758204.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0403a-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="0403a-111">Hello Exchange 伺服器上安裝 hello 代理程式，依序按一下**管理 > 代理程式 > 安裝**MABS 系統管理員主控台中。</span><span class="sxs-lookup"><span data-stu-id="0403a-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="0403a-112">請參閱[hello MABS 保護代理程式安裝](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396)如需詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="0403a-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="0403a-113">建立 hello Exchange 伺服器的保護群組</span><span class="sxs-lookup"><span data-stu-id="0403a-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="0403a-114">在 hello MABS 系統管理員主控台中，按一下 **保護**，然後按一下**新增**上 hello 工具功能區 tooopen hello**建立新保護群組**精靈。</span><span class="sxs-lookup"><span data-stu-id="0403a-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="0403a-115">在 hello ** 褖畫惎**hello 精靈按一下畫面**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="0403a-116">在 hello**選取保護群組類型**畫面上，選取**伺服器**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="0403a-117">您想 tooprotect 並按一下選取的 hello Exchange 伺服器資料庫**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0403a-118">如果您要保護 Exchange 2013，請檢查 hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0403a-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="0403a-119">在下列範例的 hello，會選取 hello Exchange 2010 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0403a-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![選擇群組成員](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="0403a-121">選取 hello 資料保護方式。</span><span class="sxs-lookup"><span data-stu-id="0403a-121">Select hello data protection method.</span></span>

    <span data-ttu-id="0403a-122">名稱 hello 保護群組，然後再選取這兩個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="0403a-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="0403a-123">我想要使用磁碟進行短期保護。</span><span class="sxs-lookup"><span data-stu-id="0403a-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="0403a-124">我想要線上保護。</span><span class="sxs-lookup"><span data-stu-id="0403a-124">I want online protection.</span></span>
6. <span data-ttu-id="0403a-125">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0403a-125">Click **Next**.</span></span>
7. <span data-ttu-id="0403a-126">選取 hello**執行 Eseutil toocheck 資料完整性**如果您想 toocheck hello 完整性 hello Exchange Server 資料庫的選項。</span><span class="sxs-lookup"><span data-stu-id="0403a-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="0403a-127">選取此選項之後，備份一致性檢查將會執行所產生的執行 hello MABS tooavoid hello I/O 流量**eseutil** hello Exchange 伺服器上的命令。</span><span class="sxs-lookup"><span data-stu-id="0403a-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0403a-128">toouse 選取此選項，您必須複製 hello Ese.dll 和 Eseutil.exe 檔案 toohello hello MAB 伺服器上的 C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin 目錄。</span><span class="sxs-lookup"><span data-stu-id="0403a-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="0403a-129">否則，會觸發 hello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0403a-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="0403a-130">![eseutil 錯誤](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="0403a-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="0403a-131">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0403a-131">Click **Next**.</span></span>
9. <span data-ttu-id="0403a-132">選取 hello 資料庫**複製備份**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0403a-133">如果您未對資料庫的至少一個 DAG 複本選取「完整備份」，則不會截斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0403a-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="0403a-134">設定目標 hello**短期備份**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="0403a-135">檢閱 hello 可用磁碟空間，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="0403a-136">選取 hello 時間在哪一個 hello MAB 伺服器將會建立 hello 初始複寫，並按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="0403a-137">選取 hello 一致性檢查選項，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="0403a-138">選擇您想要向上 tooAzure，tooback，然後按一下 hello 資料庫**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="0403a-139">例如：</span><span class="sxs-lookup"><span data-stu-id="0403a-139">For example:</span></span>

    ![指定線上保護資料](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="0403a-141">定義 hello 排程**Azure Backup**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="0403a-142">例如：</span><span class="sxs-lookup"><span data-stu-id="0403a-142">For example:</span></span>

    ![指定線上備份排程](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="0403a-144">請注意，線上復原點是以快速完整復原點為基礎。</span><span class="sxs-lookup"><span data-stu-id="0403a-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="0403a-145">因此，您必須排程 hello 線上復原點之後所指定的 hello 的 hello 時間表達完整的復原點。</span><span class="sxs-lookup"><span data-stu-id="0403a-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="0403a-146">設定保留原則 hello **Azure Backup**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0403a-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="0403a-147">選擇線上複寫選項並按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0403a-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="0403a-148">如果您有大型的資料庫時，可能需要很長的時間 hello 初始備份 toobe hello 網路上建立。</span><span class="sxs-lookup"><span data-stu-id="0403a-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="0403a-149">tooavoid 此問題，您可以建立離線備份。</span><span class="sxs-lookup"><span data-stu-id="0403a-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![指定線上保留期原則](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="0403a-151">確認 hello 設定，然後按一下**建立群組**。</span><span class="sxs-lookup"><span data-stu-id="0403a-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="0403a-152">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="0403a-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="0403a-153">Hello Exchange 資料庫復原</span><span class="sxs-lookup"><span data-stu-id="0403a-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="0403a-154">toorecover Exchange 資料庫，按一下**復原**hello MABS 系統管理員主控台中。</span><span class="sxs-lookup"><span data-stu-id="0403a-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="0403a-155">找出您想 toorecover hello Exchange 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0403a-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="0403a-156">選取 線上復原點從 hello*復原時間*下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="0403a-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="0403a-157">按一下**復原**toostart hello**復原精靈**。</span><span class="sxs-lookup"><span data-stu-id="0403a-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="0403a-158">線上復原點有五種復原類型：</span><span class="sxs-lookup"><span data-stu-id="0403a-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="0403a-159">**復原 toooriginal Exchange Server 位置：** hello 資料將會復原的 toohello 原始 Exchange server。</span><span class="sxs-lookup"><span data-stu-id="0403a-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="0403a-160">**復原 Exchange Server 上的 tooanother 資料庫：** hello 資料將會復原的 tooanother 另一部 Exchange 伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0403a-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="0403a-161">**復原 tooa 復原資料庫：** hello 資料將會復原的 tooan Exchange 復原資料庫 (RDB)。</span><span class="sxs-lookup"><span data-stu-id="0403a-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="0403a-162">**複製 tooa 網路資料夾：** hello 資料將會復原的 tooa 網路資料夾。</span><span class="sxs-lookup"><span data-stu-id="0403a-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="0403a-163">**複製 tootape:**如果您有任何磁帶媒體櫃或獨立磁帶機，將會附加，且設定在 MABS，hello 復原點複製 tooa 可用磁帶。</span><span class="sxs-lookup"><span data-stu-id="0403a-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![選擇線上複寫](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="0403a-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0403a-165">Next steps</span></span>
* [<span data-ttu-id="0403a-166">Azure 備份常見問題集</span><span class="sxs-lookup"><span data-stu-id="0403a-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
