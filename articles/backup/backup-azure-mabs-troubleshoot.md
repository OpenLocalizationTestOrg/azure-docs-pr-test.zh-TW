---
title: "針對 Azure 備份伺服器進行疑難排解 | Microsoft Docs"
description: "針對安裝、註冊 Azure 備份伺服器以及備份和還原應用程式工作負載進行疑難排解"
services: backup
documentationcenter: 
author: pvrk
manager: shreeshd
editor: 
ms.assetid: 2d73c349-0fc8-4ca8-afd8-8c9029cb8524
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pullabhk;markgal;
ms.openlocfilehash: 5672bb1e17dac4ae0aaa67f936676d6c2fc5ef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-backup-server"></a><span data-ttu-id="eacd2-103">針對 Azure 備份伺服器進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="eacd2-103">Troubleshoot Azure Backup Server</span></span>

<span data-ttu-id="eacd2-104">您可以針對使用 Azure 備份伺服器搭配下表列出的資訊時所發生的錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="eacd2-104">You can troubleshoot errors encountered while using Azure Backup Server with information listed in the following table.</span></span>


## <a name="installation-issues"></a><span data-ttu-id="eacd2-105">安裝問題</span><span class="sxs-lookup"><span data-stu-id="eacd2-105">Installation issues</span></span>

| <span data-ttu-id="eacd2-106">作業</span><span class="sxs-lookup"><span data-stu-id="eacd2-106">Operation</span></span> | <span data-ttu-id="eacd2-107">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-107">Error details</span></span> | <span data-ttu-id="eacd2-108">因應措施</span><span class="sxs-lookup"><span data-stu-id="eacd2-108">Workaround</span></span> |
|-----------|---------------|------------|
|<span data-ttu-id="eacd2-109">安裝</span><span class="sxs-lookup"><span data-stu-id="eacd2-109">Installation</span></span> | <span data-ttu-id="eacd2-110">安裝程式無法更新登錄中繼資料。</span><span class="sxs-lookup"><span data-stu-id="eacd2-110">Setup could not update registry metadata.</span></span> <span data-ttu-id="eacd2-111">此更新失敗會導致儲存體過度耗用。</span><span class="sxs-lookup"><span data-stu-id="eacd2-111">This update failure could lead to over usage of storage consumption.</span></span> <span data-ttu-id="eacd2-112">若要避免此問題，請更新 ReFS Trimming 登錄項目。</span><span class="sxs-lookup"><span data-stu-id="eacd2-112">To avoid this please update the ReFS Trimming registry entry.</span></span> | <span data-ttu-id="eacd2-113">調整登錄機碼 SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim。</span><span class="sxs-lookup"><span data-stu-id="eacd2-113">Adjust the registry key, SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim.</span></span> <span data-ttu-id="eacd2-114">將 Dword 值設為 1。</span><span class="sxs-lookup"><span data-stu-id="eacd2-114">Set the value Dword to 1.</span></span> |
|<span data-ttu-id="eacd2-115">安裝</span><span class="sxs-lookup"><span data-stu-id="eacd2-115">Installation</span></span> | <span data-ttu-id="eacd2-116">安裝程式無法更新登錄中繼資料。</span><span class="sxs-lookup"><span data-stu-id="eacd2-116">Setup could not update registry metadata.</span></span> <span data-ttu-id="eacd2-117">此更新失敗會導致儲存體過度耗用。</span><span class="sxs-lookup"><span data-stu-id="eacd2-117">This update failure could lead to over usage of storage consumption.</span></span> <span data-ttu-id="eacd2-118">若要避免此問題，請更新 Volume SnapOptimization 登錄項目。</span><span class="sxs-lookup"><span data-stu-id="eacd2-118">To avoid this please update the Volume SnapOptimization registry entry.</span></span> | <span data-ttu-id="eacd2-119">使用空白字串值建立登錄機碼 SOFTWARE\Microsoft Data Protection Manager\Configuration\VolSnapOptimization\WriteIds。</span><span class="sxs-lookup"><span data-stu-id="eacd2-119">Create the registry key, SOFTWARE\Microsoft Data Protection Manager\Configuration\VolSnapOptimization\WriteIds, with an empty string value.</span></span> |

## <a name="registration-and-agent-related-issues"></a><span data-ttu-id="eacd2-120">註冊與代理程式相關問題</span><span class="sxs-lookup"><span data-stu-id="eacd2-120">Registration and Agent related issues</span></span>
| <span data-ttu-id="eacd2-121">作業</span><span class="sxs-lookup"><span data-stu-id="eacd2-121">Operation</span></span> | <span data-ttu-id="eacd2-122">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-122">Error details</span></span> | <span data-ttu-id="eacd2-123">因應措施</span><span class="sxs-lookup"><span data-stu-id="eacd2-123">Workaround</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eacd2-124">註冊至保存庫</span><span class="sxs-lookup"><span data-stu-id="eacd2-124">Registering to a vault</span></span> | <span data-ttu-id="eacd2-125">提供的保存庫認證無效。</span><span class="sxs-lookup"><span data-stu-id="eacd2-125">Invalid vault credentials provided.</span></span> <span data-ttu-id="eacd2-126">檔案可能損毀或沒有復原服務所關聯的最新認證</span><span class="sxs-lookup"><span data-stu-id="eacd2-126">The file is either corrupted or does not have the latest credentials associated with recovery service</span></span> | <span data-ttu-id="eacd2-127">若要修正此錯誤：</span><span class="sxs-lookup"><span data-stu-id="eacd2-127">To fix this error:</span></span> <ol><li> <span data-ttu-id="eacd2-128">從保存庫下載最新的認證檔案，然後再試一次</span><span class="sxs-lookup"><span data-stu-id="eacd2-128">Download the latest credentials file from the vault and try again</span></span> <br><span data-ttu-id="eacd2-129">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-129">(OR)</span></span></li> <li> <span data-ttu-id="eacd2-130">如果上述動作沒有用，請嘗試將認證下載至不同的本機目錄，或建立新的保存庫</span><span class="sxs-lookup"><span data-stu-id="eacd2-130">If the above action didn't work, try downloading the credentials to a different local directory or create a new vault</span></span> <br><span data-ttu-id="eacd2-131">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-131">(OR)</span></span></li> <li> <span data-ttu-id="eacd2-132">如[這個部落格](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/)所述嘗試更新日期和時間設定</span><span class="sxs-lookup"><span data-stu-id="eacd2-132">Try updating the date and time settings as stated in [this blog](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/)</span></span> <br><span data-ttu-id="eacd2-133">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-133">(OR)</span></span></li> <li> <span data-ttu-id="eacd2-134">檢查 c:\windows\temp 是否有超過 65000 個檔案。</span><span class="sxs-lookup"><span data-stu-id="eacd2-134">Check whether c:\windows\temp has more than 65000 files.</span></span> <span data-ttu-id="eacd2-135">將過時檔案移至另一個位置，或刪除暫存資料夾中的項目</span><span class="sxs-lookup"><span data-stu-id="eacd2-135">Move stale files to another location or delete the items in the Temp folder</span></span> <br><span data-ttu-id="eacd2-136">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-136">(OR)</span></span></li> <li> <span data-ttu-id="eacd2-137">檢查憑證的狀態</span><span class="sxs-lookup"><span data-stu-id="eacd2-137">Check the status of certificates</span></span> <br> <span data-ttu-id="eacd2-138">a.</span><span class="sxs-lookup"><span data-stu-id="eacd2-138">a.</span></span> <span data-ttu-id="eacd2-139">開啟 [管理電腦憑證] \(在控制台中)</span><span class="sxs-lookup"><span data-stu-id="eacd2-139">Open "Manage Computer Certificates" (in the Control Panel)</span></span> <br> <span data-ttu-id="eacd2-140">b.</span><span class="sxs-lookup"><span data-stu-id="eacd2-140">b.</span></span> <span data-ttu-id="eacd2-141">展開 [個人] 節點和它的子節點 [憑證]</span><span class="sxs-lookup"><span data-stu-id="eacd2-141">Expand the "Personal" node and its child node "Certificates"</span></span> <br> <span data-ttu-id="eacd2-142">c.</span><span class="sxs-lookup"><span data-stu-id="eacd2-142">c.</span></span>  <span data-ttu-id="eacd2-143">移除 [Windows Azure 工具] 憑證</span><span class="sxs-lookup"><span data-stu-id="eacd2-143">Remove the certificate "Windows Azure Tools"</span></span> <br> <span data-ttu-id="eacd2-144">d.</span><span class="sxs-lookup"><span data-stu-id="eacd2-144">d.</span></span> <span data-ttu-id="eacd2-145">在 Azure 備份用戶端中重試註冊</span><span class="sxs-lookup"><span data-stu-id="eacd2-145">Retry the registration in the Azure Backup client</span></span> <br> <span data-ttu-id="eacd2-146">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-146">(OR)</span></span> </li> <li> <span data-ttu-id="eacd2-147">檢查是否已備有任何群組原則</span><span class="sxs-lookup"><span data-stu-id="eacd2-147">Check whether any Group policy is in place</span></span> </li></ol> |
| <span data-ttu-id="eacd2-148">將代理程式推送至受保護的伺服器</span><span class="sxs-lookup"><span data-stu-id="eacd2-148">Pushing agent(s) to protected servers</span></span> | <span data-ttu-id="eacd2-149">代理程式作業因為 \<ServerName> 上的 DPM 代理程式協調員服務發生通訊錯誤而失敗</span><span class="sxs-lookup"><span data-stu-id="eacd2-149">The agent operation failed because of a communication error with the DPM Agent Coordinator service on \<ServerName></span></span> | <span data-ttu-id="eacd2-150">**如果產品所示的建議動作沒有用**，</span><span class="sxs-lookup"><span data-stu-id="eacd2-150">**If the recommended action shown in the product doesn't work**,</span></span> <ol><li> <span data-ttu-id="eacd2-151">如果您要連結來自不受信任網域的電腦，請遵循[這些](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx)步驟</span><span class="sxs-lookup"><span data-stu-id="eacd2-151">If you are attaching a computer from an untrusted domain, follow [these](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx) steps</span></span> <br> <span data-ttu-id="eacd2-152">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-152">(OR)</span></span> </li><li> <span data-ttu-id="eacd2-153">如果您要連結來自受信任網域的電腦，請使用[這個部落格](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/)中概述的步驟進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="eacd2-153">If you are attaching a computer from a trusted domain, troubleshoot using the steps outlined in [this blog](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/)</span></span> <br><span data-ttu-id="eacd2-154">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-154">(OR)</span></span></li><li> <span data-ttu-id="eacd2-155">嘗試停用防毒來作為疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="eacd2-155">Try disabling Antivirus as a troubleshooting step.</span></span> <span data-ttu-id="eacd2-156">如果這能解決問題，請修改 [這篇文章] (https://technet.microsoft.com/library/hh757911.aspx) 中建議的防毒設定</span><span class="sxs-lookup"><span data-stu-id="eacd2-156">If it resolves the issue, modify the Antivirus settings as suggested in [this article] (https://technet.microsoft.com/library/hh757911.aspx)</span></span></li></ol> |
| <span data-ttu-id="eacd2-157">將代理程式推送至受保護的伺服器</span><span class="sxs-lookup"><span data-stu-id="eacd2-157">Pushing agent(s) to protected servers</span></span> | <span data-ttu-id="eacd2-158">為伺服器指定的認證無效</span><span class="sxs-lookup"><span data-stu-id="eacd2-158">The credentials specified for server are invalid</span></span> | <span data-ttu-id="eacd2-159">**如果產品所示的建議動作沒有用**，</span><span class="sxs-lookup"><span data-stu-id="eacd2-159">**If the recommended action shown in the product doesn't work**,</span></span> <br> <span data-ttu-id="eacd2-160">嘗試手動將保護代理程式安裝在[這篇文章](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)所指定的生產伺服器上</span><span class="sxs-lookup"><span data-stu-id="eacd2-160">try to install the protection agent manually on the production server as specified in [this article](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)</span></span>|
| <span data-ttu-id="eacd2-161">Azure 備份代理程式無法連線到 Azure 備份服務 (ID：100050)</span><span class="sxs-lookup"><span data-stu-id="eacd2-161">Azure Backup Agent was unable to connect to the Azure Backup service (ID: 100050)</span></span> | <span data-ttu-id="eacd2-162">Azure 備份代理程式無法連線到 Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="eacd2-162">The Azure Backup Agent was unable to connect to the Azure Backup service.</span></span> | <span data-ttu-id="eacd2-163">**如果產品所示的建議動作沒有用**，</span><span class="sxs-lookup"><span data-stu-id="eacd2-163">**If the recommended action shown in the product doesn't work**,</span></span> <br><span data-ttu-id="eacd2-164">1.從提升權限的提示字元中執行下列命令︰psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"。這會開啟 IE 視窗。</span><span class="sxs-lookup"><span data-stu-id="eacd2-164">1. Run following command from elevated prompt, psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe" It will open internet explorer window.</span></span> <br/> <span data-ttu-id="eacd2-165">2.移至 [工具]-> [網際網路選項]-> [連線]-> [區域網路設定]。</span><span class="sxs-lookup"><span data-stu-id="eacd2-165">2. Go to Tools -> Internet Options -> Connections -> LAN settings.</span></span> <br/> <span data-ttu-id="eacd2-166">3.確認系統帳戶的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="eacd2-166">3. Verify proxy settings for System account.</span></span> <span data-ttu-id="eacd2-167">設定 Proxy IP 和連接埠。</span><span class="sxs-lookup"><span data-stu-id="eacd2-167">Set Proxy IP and port.</span></span> <br/> <span data-ttu-id="eacd2-168">4.關閉 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="eacd2-168">4. Close Internet Explorer.</span></span>|
| <span data-ttu-id="eacd2-169">Azure 備份代理程式安裝失敗</span><span class="sxs-lookup"><span data-stu-id="eacd2-169">Azure Backup Agent installation failed</span></span> | <span data-ttu-id="eacd2-170">Microsoft Azure 復原服務安裝失敗。</span><span class="sxs-lookup"><span data-stu-id="eacd2-170">The Microsoft Azure Recovery Services installation failed.</span></span> <span data-ttu-id="eacd2-171">Microsoft Azure 復原服務安裝作業對系統所做的所有變更都已復原。</span><span class="sxs-lookup"><span data-stu-id="eacd2-171">All changes made by the Microsoft Azure Recovery Services installation to the system were rolled back.</span></span> <span data-ttu-id="eacd2-172">(ID：4024)</span><span class="sxs-lookup"><span data-stu-id="eacd2-172">(ID: 4024)</span></span> | <span data-ttu-id="eacd2-173">手動安裝 Azure 代理程式</span><span class="sxs-lookup"><span data-stu-id="eacd2-173">Manually install Azure Agent</span></span>


## <a name="configuring-protection-group"></a><span data-ttu-id="eacd2-174">設定保護群組</span><span class="sxs-lookup"><span data-stu-id="eacd2-174">Configuring protection group</span></span>
| <span data-ttu-id="eacd2-175">作業</span><span class="sxs-lookup"><span data-stu-id="eacd2-175">Operation</span></span> | <span data-ttu-id="eacd2-176">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-176">Error details</span></span> | <span data-ttu-id="eacd2-177">因應措施</span><span class="sxs-lookup"><span data-stu-id="eacd2-177">Workaround</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eacd2-178">設定保護群組</span><span class="sxs-lookup"><span data-stu-id="eacd2-178">Configuring Protection groups</span></span> | <span data-ttu-id="eacd2-179">DPM 無法列舉受保護電腦 (受保護的電腦名稱) 上的應用程式元件</span><span class="sxs-lookup"><span data-stu-id="eacd2-179">DPM could not enumerate application component  on protected computer (Protected computer Name)</span></span> | <span data-ttu-id="eacd2-180">在相關的資料來源/元件層級按一下設定保護群組 UI 畫面上的 [重新整理]</span><span class="sxs-lookup"><span data-stu-id="eacd2-180">Click 'Refresh' on the configure protection group UI screen at the relevant datasource/component level</span></span> |
| <span data-ttu-id="eacd2-181">設定保護群組</span><span class="sxs-lookup"><span data-stu-id="eacd2-181">Configuring Protection groups</span></span> | <span data-ttu-id="eacd2-182">無法設定保護</span><span class="sxs-lookup"><span data-stu-id="eacd2-182">Unable to configure protection</span></span> | <span data-ttu-id="eacd2-183">如果受保護的伺服器是 SQL Server，請檢查是否以將 sysadmin 角色權限提供給[這篇文章](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)中所述之受保護電腦上的系統帳戶 (NTAuthority\System)</span><span class="sxs-lookup"><span data-stu-id="eacd2-183">If the protected server is a SQL server, please check whether sysadmin role permissions have been provided to the system account (NTAuthority\System) on the protected computer as stated in [this article](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)</span></span>
| <span data-ttu-id="eacd2-184">設定保護群組</span><span class="sxs-lookup"><span data-stu-id="eacd2-184">Configuring Protection groups</span></span> | <span data-ttu-id="eacd2-185">此保護群組在儲存體集區中沒有足夠的可用空間</span><span class="sxs-lookup"><span data-stu-id="eacd2-185">There is insufficient free space in the storage pool for this protection group</span></span> | <span data-ttu-id="eacd2-186">新增至儲存體集區的磁碟[不應包含磁碟分割](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx)。</span><span class="sxs-lookup"><span data-stu-id="eacd2-186">The disks which are added to the storage pool [should not contain a partition](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx).</span></span> <span data-ttu-id="eacd2-187">刪除磁碟上的任何現有磁碟區，然後將它新增到儲存體集區</span><span class="sxs-lookup"><span data-stu-id="eacd2-187">Delete any existing volumes on the disks and then add it to the storage pool</span></span>|
| <span data-ttu-id="eacd2-188">原則變更</span><span class="sxs-lookup"><span data-stu-id="eacd2-188">Policy change</span></span> |<span data-ttu-id="eacd2-189">無法修改備份原則。</span><span class="sxs-lookup"><span data-stu-id="eacd2-189">The backup policy could not be modified.</span></span> <span data-ttu-id="eacd2-190">錯誤：由於發生內部服務錯誤 [0x29834]，導致目前的作業失敗。</span><span class="sxs-lookup"><span data-stu-id="eacd2-190">Error: The current operation failed due to an internal service error [0x29834].</span></span> <span data-ttu-id="eacd2-191">請稍後再重試操作。</span><span class="sxs-lookup"><span data-stu-id="eacd2-191">Please retry the operation after sometime.</span></span> <span data-ttu-id="eacd2-192">如果問題持續發生， 請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="eacd2-192">If the issue persists, please contact Microsoft support.</span></span> |<span data-ttu-id="eacd2-193">**原因：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-193">**Cause:**</span></span><br/><span data-ttu-id="eacd2-194">當安全性設定已啟用，而您嘗試將保留範圍縮減至低於上面指定的最小值，且您使用不受支援的版本 (低於 MAB 2.0.9052 版和 Azure 備份伺服器更新 1) 時，就會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="eacd2-194">This error comes when security settings are enabled, you try to reduce retention range below the minimum values specified above and you are on unsupported  version (below MAB version 2.0.9052 and Azure Backup server update 1).</span></span> <br/><span data-ttu-id="eacd2-195">**建議的動作：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-195">**Recommended Action:**</span></span><br/> <span data-ttu-id="eacd2-196">在此情況下，您應該將保留期限設定為高於指定的最小保留期限 (若是每日則 7 天、若是每週則 4 週、若是每月則 3 個月，若是每年則 1 年)，以繼續進行與原則有關的更新。</span><span class="sxs-lookup"><span data-stu-id="eacd2-196">In this case, you should set retention period above the minimum retention period specified (seven days for daily, four weeks for weekly, three weeks for monthly or one year for yearly) to proceed with policy related udpates.</span></span> <span data-ttu-id="eacd2-197">(選擇性) 較好的方法是更新備份代理程式和 Azure 備份伺服器，以利用所有安全性更新。</span><span class="sxs-lookup"><span data-stu-id="eacd2-197">Optionally, preferred approach would be to update backup agent and Azure Backup Server to leverage all the security updates.</span></span> |

## <a name="backup"></a><span data-ttu-id="eacd2-198">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-198">Backup</span></span>
| <span data-ttu-id="eacd2-199">作業</span><span class="sxs-lookup"><span data-stu-id="eacd2-199">Operation</span></span> | <span data-ttu-id="eacd2-200">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-200">Error details</span></span> | <span data-ttu-id="eacd2-201">因應措施</span><span class="sxs-lookup"><span data-stu-id="eacd2-201">Workaround</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eacd2-202">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-202">Backup</span></span> | <span data-ttu-id="eacd2-203">複本不一致</span><span class="sxs-lookup"><span data-stu-id="eacd2-203">Replica is inconsistent</span></span> | <span data-ttu-id="eacd2-204">您可以在[這裡](https://technet.microsoft.com/library/cc161593.aspx)找到更多關於複本不一致原因和相關建議的詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-204">You can find more details about the causes of replica inconsistency and relevant suggestions [here](https://technet.microsoft.com/library/cc161593.aspx)</span></span> <br> <ol><li> <span data-ttu-id="eacd2-205">如果是系統狀態/BMR 備份，請檢查受保護伺服器上是否已安裝 Windows Server Backup</span><span class="sxs-lookup"><span data-stu-id="eacd2-205">In case of System State/BMR backup, please check whether Windows Server Backup is installed or not on Protected Server</span></span> </li><li> <span data-ttu-id="eacd2-206">檢查 DPM/MABS 伺服器上 DPM 儲存體集區的空間相關問題，並視需要配置儲存體</span><span class="sxs-lookup"><span data-stu-id="eacd2-206">Check for Space related issues on DPM storage pool on the DPM/MABS server and allocate storage as required</span></span> </li><li> <span data-ttu-id="eacd2-207">檢查受保護伺服器上的磁碟區陰影複製服務狀態。</span><span class="sxs-lookup"><span data-stu-id="eacd2-207">Check the state of the Volume shadow copy service on the protected server.</span></span> <span data-ttu-id="eacd2-208">如果它是停用狀態，請將它設定為手動啟動，並在伺服器上啟動服務。</span><span class="sxs-lookup"><span data-stu-id="eacd2-208">If it is in disabled state set it to start manually and start the service on the server.</span></span> <span data-ttu-id="eacd2-209">然後返回 DPM/MABS 主控台，並開始一致性檢查作業的同步處理。</span><span class="sxs-lookup"><span data-stu-id="eacd2-209">Then go back to the DPM/MABS console and start the sync with consistency check job.</span></span></li></ol>|
| <span data-ttu-id="eacd2-210">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-210">Backup</span></span> | <span data-ttu-id="eacd2-211">執行作業時發生非預期的錯誤，裝置未就緒</span><span class="sxs-lookup"><span data-stu-id="eacd2-211">An unexpected error occurred while the job was running, The device is not ready</span></span> | <span data-ttu-id="eacd2-212">**如果產品所示的建議動作沒有用**，</span><span class="sxs-lookup"><span data-stu-id="eacd2-212">**If the recommended action shown in the product doesn't work**,</span></span> <br> <ol><li><span data-ttu-id="eacd2-213">針對保護群組中的項目，將陰影複製儲存空間設定為無限，並執行一致性檢查</span><span class="sxs-lookup"><span data-stu-id="eacd2-213">Set the Shadow Copy Storage space to unlimited on the Items in the protection group and run the consistency check</span></span> <br></li> <span data-ttu-id="eacd2-214">(或)</span><span class="sxs-lookup"><span data-stu-id="eacd2-214">(OR)</span></span> <li><span data-ttu-id="eacd2-215">嘗試刪除現有保護群組，並建立多個新的保護群組，每個保護群組中各有一個個別項目</span><span class="sxs-lookup"><span data-stu-id="eacd2-215">Try deleting the existing Protection group and create multiple new ones – one with each individual item in it</span></span></li></ol> |
| <span data-ttu-id="eacd2-216">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-216">Backup</span></span> | <span data-ttu-id="eacd2-217">如果您只要備份系統狀態，請確認受保護的電腦上是否有足夠的可用空間可儲存系統狀態備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-217">If you are backing up only System State, verify if there is enough free space on the protected computer to store the System State backup</span></span> | <ol><li><span data-ttu-id="eacd2-218">確認受保護的電腦上已安裝 WSB</span><span class="sxs-lookup"><span data-stu-id="eacd2-218">Verify that the WSB on the protected machine is installed</span></span></li><li><span data-ttu-id="eacd2-219">確認受保護的電腦上有足夠空間可存放系統狀態︰最簡單的執行方法是移到受保護的電腦上、開啟 WSB、逐一點選選取項目，然後選取 BMR。</span><span class="sxs-lookup"><span data-stu-id="eacd2-219">Verify that enough space is present on the protected computer for the system state: The easiest way to do this is to go to the protected computer, open WSB and click through the selections and select BMR.</span></span> <span data-ttu-id="eacd2-220">然後，UI 會告訴您這需要多少空間。</span><span class="sxs-lookup"><span data-stu-id="eacd2-220">The UI will then tell you how much space is required for this.</span></span> <span data-ttu-id="eacd2-221">開啟 WSB -> 本機備份 -> 備份排程 -> 選取備份設定 -> 完整伺服器 (大小會顯示出來)。</span><span class="sxs-lookup"><span data-stu-id="eacd2-221">Open WSB -> Local backup -> Backup schedule -> Select Backup Configuration -> Full server (size is displayed).</span></span> <span data-ttu-id="eacd2-222">使用此大小進行驗證。</span><span class="sxs-lookup"><span data-stu-id="eacd2-222">Use this size for verification.</span></span></li></ol>
| <span data-ttu-id="eacd2-223">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-223">Backup</span></span> | <span data-ttu-id="eacd2-224">線上復原點建立失敗</span><span class="sxs-lookup"><span data-stu-id="eacd2-224">Online recovery point creation failed</span></span> | <span data-ttu-id="eacd2-225">如果錯誤訊息指出「Windows Azure Backup Agent 無法建立所選磁碟區的快照集」，請嘗試增加複本和復原點磁碟區中的空間。</span><span class="sxs-lookup"><span data-stu-id="eacd2-225">If the error message says "Windows Azure Backup Agent was unable to create a snapshot of the selected volume", please try increasing the space in replica and recovery point volume.</span></span>
| <span data-ttu-id="eacd2-226">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-226">Backup</span></span> | <span data-ttu-id="eacd2-227">線上復原點建立失敗</span><span class="sxs-lookup"><span data-stu-id="eacd2-227">Online recovery point creation failed</span></span> | <span data-ttu-id="eacd2-228">如果錯誤訊息顯示「Windows Azure 備份代理程式無法連線到 OBEngine 服務」，請確認 OBEngine 存在於電腦上的執行中服務清單。</span><span class="sxs-lookup"><span data-stu-id="eacd2-228">If the error message says "The Windows Azure Backup Agent cannot connect to the OBEngine service", verify that the OBEngine exists in the list of running services on the computer.</span></span> <span data-ttu-id="eacd2-229">如果 OBEngine 服務不在執行中，請使用 "net start OBEngine" 命令來啟動 OBEngine 服務。</span><span class="sxs-lookup"><span data-stu-id="eacd2-229">If the OBEngine service is not running use the "net start OBEngine" command to start the OBEngine service.</span></span>
| <span data-ttu-id="eacd2-230">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-230">Backup</span></span> | <span data-ttu-id="eacd2-231">線上復原點建立失敗</span><span class="sxs-lookup"><span data-stu-id="eacd2-231">Online recovery point creation failed</span></span> | <span data-ttu-id="eacd2-232">如果錯誤訊息指出「未設定此伺服器的加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="eacd2-232">If the error message says "The encryption passphrase for this server is not set.</span></span> <span data-ttu-id="eacd2-233">請設定加密複雜密碼」，請嘗試設定加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="eacd2-233">Please configure an encryption passphrase" try configuring an encryption passphrase.</span></span> <span data-ttu-id="eacd2-234">如果作業失敗，</span><span class="sxs-lookup"><span data-stu-id="eacd2-234">If it fails,</span></span> <br> <ol><li><span data-ttu-id="eacd2-235">請檢查暫存位置是否存在。</span><span class="sxs-lookup"><span data-stu-id="eacd2-235">check whether the scratch location exists or not.</span></span> <span data-ttu-id="eacd2-236">名稱為 “ScratchLocation” 之登錄 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config 中所提到的位置應該要存在。</span><span class="sxs-lookup"><span data-stu-id="eacd2-236">The location mentioned in the registry HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config with name “ScratchLocation” should exist.</span></span></li><li> <span data-ttu-id="eacd2-237">如果暫存位置存在，請嘗試使用舊的複雜密碼重新註冊。</span><span class="sxs-lookup"><span data-stu-id="eacd2-237">If the scratch location exists, try re-registering using the old passphrase.</span></span> <span data-ttu-id="eacd2-238">**每當您設定加密複雜密碼時，請將它儲存在安全的位置**</span><span class="sxs-lookup"><span data-stu-id="eacd2-238">**Whenever you configure an encryption passphrase, please save it in a secure location**</span></span></li><ol>
| <span data-ttu-id="eacd2-239">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-239">Backup</span></span> | <span data-ttu-id="eacd2-240">BMR 的備份失敗</span><span class="sxs-lookup"><span data-stu-id="eacd2-240">Backup failure for BMR</span></span> | <span data-ttu-id="eacd2-241">如果 BMR 大小很大，請將一些應用程式檔案移到作業系統磁碟機後再重試</span><span class="sxs-lookup"><span data-stu-id="eacd2-241">If BMR size is huge, retry after moving some application files to OS drive</span></span> |
| <span data-ttu-id="eacd2-242">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-242">Backup</span></span> | <span data-ttu-id="eacd2-243">存取檔案/共用資料夾時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="eacd2-243">Error while accessing files/shared folders</span></span> | <span data-ttu-id="eacd2-244">請嘗試依[這裡](https://technet.microsoft.com/library/hh757911.aspx)的建議修改防毒設定</span><span class="sxs-lookup"><span data-stu-id="eacd2-244">Try modifying the antivirus settings as suggested [here](https://technet.microsoft.com/library/hh757911.aspx)</span></span>|
| <span data-ttu-id="eacd2-245">備份</span><span class="sxs-lookup"><span data-stu-id="eacd2-245">Backup</span></span> | <span data-ttu-id="eacd2-246">VMware VM 的線上復原點建立作業失敗。</span><span class="sxs-lookup"><span data-stu-id="eacd2-246">Online recovery point creation jobs for VMware VM fails.</span></span> <span data-ttu-id="eacd2-247">DPM 在嘗試取得變更追蹤資訊時，VMware 發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="eacd2-247">DPM encountered error from VMware while trying to get ChangeTracking information.</span></span> <span data-ttu-id="eacd2-248">ErrorCode - FileFaultFault (ID 33621 )</span><span class="sxs-lookup"><span data-stu-id="eacd2-248">ErrorCode - FileFaultFault (ID 33621 )</span></span> |  <span data-ttu-id="eacd2-249">1.針對受影響的 VM，在 VMWare 上重設 ctk</span><span class="sxs-lookup"><span data-stu-id="eacd2-249">1. Reset the ctk on VMWare, for the affected VMs</span></span> <br/> <span data-ttu-id="eacd2-250">檢查獨立磁碟不在 VMWare 上</span><span class="sxs-lookup"><span data-stu-id="eacd2-250">Check that Independent disk is not in place on VMWare</span></span> <br/> <span data-ttu-id="eacd2-251">停止保護受影響的 VM，然後使用 [重新整理] 按鈕重新保護</span><span class="sxs-lookup"><span data-stu-id="eacd2-251">Stop protection for the affected VMs and re-protect with Refresh button</span></span> <br/> <span data-ttu-id="eacd2-252">對受影響的 VM 執行 CC</span><span class="sxs-lookup"><span data-stu-id="eacd2-252">Run a CC for the affected VMs</span></span>|


## <a name="change-passphrase"></a><span data-ttu-id="eacd2-253">變更複雜密碼</span><span class="sxs-lookup"><span data-stu-id="eacd2-253">Change Passphrase</span></span>
| <span data-ttu-id="eacd2-254">作業</span><span class="sxs-lookup"><span data-stu-id="eacd2-254">Operation</span></span> | <span data-ttu-id="eacd2-255">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-255">Error details</span></span> | <span data-ttu-id="eacd2-256">因應措施</span><span class="sxs-lookup"><span data-stu-id="eacd2-256">Workaround</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eacd2-257">變更複雜密碼</span><span class="sxs-lookup"><span data-stu-id="eacd2-257">Change Passphrase</span></span> |<span data-ttu-id="eacd2-258">輸入的安全性 PIN 碼不正確。</span><span class="sxs-lookup"><span data-stu-id="eacd2-258">Security PIN entered is incorrect.</span></span> <span data-ttu-id="eacd2-259">請提供正確的安全性 PIN 碼以完成此作業。</span><span class="sxs-lookup"><span data-stu-id="eacd2-259">Provide the correct Security PIN to complete this operation.</span></span> |<span data-ttu-id="eacd2-260">**原因：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-260">**Cause:**</span></span><br/> <span data-ttu-id="eacd2-261">當您在執行重要作業 (例如變更複雜密碼) 時輸入無效或已到期的安全性 PIN 碼時，就會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="eacd2-261">This error comes when you enter invalid or expired Security PIN while performing critical operation (like change passphrase).</span></span> <br/><span data-ttu-id="eacd2-262">**建議的動作：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-262">**Recommended Action:**</span></span><br/> <span data-ttu-id="eacd2-263">若要完成作業，您必須輸入有效的安全性 PIN 碼。</span><span class="sxs-lookup"><span data-stu-id="eacd2-263">To complete the operation, you must enter valid Security PIN.</span></span> <span data-ttu-id="eacd2-264">若要取得 PIN 碼，請登入 Azure 入口網站，並瀏覽至 [復原服務保存庫] > [設定] > [屬性] > [產生安全性 PIN 碼]。</span><span class="sxs-lookup"><span data-stu-id="eacd2-264">To get the PIN, log in to Azure portal and navigate to Recovery Services vault > Settings > Properties > Generate Security PIN.</span></span> <span data-ttu-id="eacd2-265">請使用這個 PIN 碼來變更複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="eacd2-265">Use this PIN to change passphrase.</span></span> |
| <span data-ttu-id="eacd2-266">變更複雜密碼</span><span class="sxs-lookup"><span data-stu-id="eacd2-266">Change Passphrase</span></span> |<span data-ttu-id="eacd2-267">作業失敗。</span><span class="sxs-lookup"><span data-stu-id="eacd2-267">Operation failed.</span></span> <span data-ttu-id="eacd2-268">識別碼：120002</span><span class="sxs-lookup"><span data-stu-id="eacd2-268">ID: 120002</span></span> |<span data-ttu-id="eacd2-269">**原因：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-269">**Cause:**</span></span><br/><span data-ttu-id="eacd2-270">當安全性設定已啟用，而您嘗試變更複雜密碼，且您使用不受支援的版本時，就會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="eacd2-270">This error comes when security settings are enabled, you try to change passphrase and you are on unsupported version.</span></span><br/><span data-ttu-id="eacd2-271">**建議的動作：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-271">**Recommended Action:**</span></span><br/> <span data-ttu-id="eacd2-272">若要變更複雜密碼，您必須先將備份代理程式至少更新為最低版本 2.0.9052，並將 Azure 備份伺服器至少更新為更新 1，然後輸入有效的安全性 PIN 碼。</span><span class="sxs-lookup"><span data-stu-id="eacd2-272">To change passphrase, you must first update backup agent to minimum version minimum 2.0.9052 and Azure Backup server to minimum update 1, then enter valid Security PIN.</span></span> <span data-ttu-id="eacd2-273">若要取得 PIN 碼，請登入 Azure 入口網站，並瀏覽至 [復原服務保存庫] > [設定] > [屬性] > [產生安全性 PIN 碼]。</span><span class="sxs-lookup"><span data-stu-id="eacd2-273">To get the PIN, log in to Azure portal and navigate to Recovery Services vault > Settings > Properties > Generate Security PIN.</span></span> <span data-ttu-id="eacd2-274">請使用這個 PIN 碼來變更複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="eacd2-274">Use this PIN to change passphrase.</span></span> |


## <a name="configure-email-notifications"></a><span data-ttu-id="eacd2-275">設定電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="eacd2-275">Configure email notifications</span></span>
| <span data-ttu-id="eacd2-276">作業</span><span class="sxs-lookup"><span data-stu-id="eacd2-276">Operation</span></span> | <span data-ttu-id="eacd2-277">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="eacd2-277">Error details</span></span> | <span data-ttu-id="eacd2-278">因應措施</span><span class="sxs-lookup"><span data-stu-id="eacd2-278">Workaround</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eacd2-279">嘗試使用 Office365 帳戶設定電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="eacd2-279">Trying to set up email notifications using Office365 account.</span></span> | <span data-ttu-id="eacd2-280">取得錯誤 ID：2013</span><span class="sxs-lookup"><span data-stu-id="eacd2-280">getting Error ID: 2013</span></span>| <span data-ttu-id="eacd2-281">**原因：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-281">**Cause:**</span></span><br/> <span data-ttu-id="eacd2-282">嘗試使用 Office 365 帳戶</span><span class="sxs-lookup"><span data-stu-id="eacd2-282">Trying to use Office 365 account</span></span> <br/> <span data-ttu-id="eacd2-283">**建議的動作：**</span><span class="sxs-lookup"><span data-stu-id="eacd2-283">**Recommended Action:**</span></span><br/> <span data-ttu-id="eacd2-284">所要確保的第一件事就是已 Exchange 上設定 DPM 伺服器的「允許接收連接器上的匿名轉送」。</span><span class="sxs-lookup"><span data-stu-id="eacd2-284">The first thing to ensure is that “Allow Anonymous Relay on a Receive Connector” for your DPM server is setup on Exchange.</span></span> <span data-ttu-id="eacd2-285">以下是如何進行此設定的連結：http://technet.microsoft.com/en-us/library/bb232021.aspx</span><span class="sxs-lookup"><span data-stu-id="eacd2-285">Here is a link on how to configure this: http://technet.microsoft.com/en-us/library/bb232021.aspx</span></span> <br/> <span data-ttu-id="eacd2-286">如果您無法使用內部 SMTP 轉送，而需要使用 Office 365 伺服器進行設定，您可以將 IIS 設定為其轉送。</span><span class="sxs-lookup"><span data-stu-id="eacd2-286">If you can't use an internal SMTP relay and need to set up using your Office 365 server, you can set up IIS to be a relay for this.</span></span> <br/> <span data-ttu-id="eacd2-287">您必須將 DPM 伺服器設定為能使用 IIS 將 SMTP 轉送至 O365 (https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx)，才能設定 IIS 來轉送至 O365</span><span class="sxs-lookup"><span data-stu-id="eacd2-287">You will need to configure the DPM server to be able to relay the SMTP to O365 using IIS https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx to setup IIS to relay to O365</span></span> <br/> <span data-ttu-id="eacd2-288">重要事項：在步驟 3->g->ii，務必使用 user@domain.com 格式，而非 domain\user 格式</span><span class="sxs-lookup"><span data-stu-id="eacd2-288">Important note:  On step 3->g->ii, be sure to use user@domain.com format and NOT domain\user</span></span> <br/> <span data-ttu-id="eacd2-289">指示 DPM 使用本機伺服器名稱作為 SMTP 伺服器、連接埠 587，以及應送出電子郵件的使用者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="eacd2-289">Point DPM to use the local servername as SMTP server, port 587 and then the user email that the emails should come from.</span></span> <br/> <span data-ttu-id="eacd2-290">DPM SMTP 設定頁面上的使用者名稱和密碼，應該是網域 DPM 所在的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="eacd2-290">The username and password on the DPM SMTP setup page should be a domain account in the domain DPM is on.</span></span> <br/> <span data-ttu-id="eacd2-291">注意：變更 SMTP 伺服器位址時，對新設定進行變更，關閉 [設定] 方塊，然後重新開啟來確定其反映新的值。</span><span class="sxs-lookup"><span data-stu-id="eacd2-291">NOTE:  When changing the SMTP server address, make the change to new settings, close the settings box and then reopen to be sure it reflects the new value.</span></span>  <span data-ttu-id="eacd2-292">只有變更和測試不一定會採用新的設定，因此以這種方式測試是最佳做法。</span><span class="sxs-lookup"><span data-stu-id="eacd2-292">Simply changing and testing will not always take the new settings so testing this way is best practice.</span></span> <br/> <span data-ttu-id="eacd2-293">在此程序期間，您可藉由關閉 DPM 主控台並編輯下列登錄機碼，隨時清除這些設定︰</span><span class="sxs-lookup"><span data-stu-id="eacd2-293">At any time during this process, you can clear these settings out by closing DPM console and editing the following registry keys:</span></span><br/> <span data-ttu-id="eacd2-294">HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\\</span><span class="sxs-lookup"><span data-stu-id="eacd2-294">HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\\</span></span> <br/> <span data-ttu-id="eacd2-295">刪除 SMTPPassword 和 SMTPUserName 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="eacd2-295">Delete SMTPPassword and SMTPUserName keys.</span></span> <br/> <span data-ttu-id="eacd2-296">再次啟動時，您可以在 UI 中將它們加回。</span><span class="sxs-lookup"><span data-stu-id="eacd2-296">You can add them back in the UI when you launch it again.</span></span>