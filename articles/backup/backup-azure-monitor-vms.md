---
title: "aaaMonitor 資源管理員部署虛擬機器備份 |Microsoft 文件"
description: "監視 Resource Manager 部署的虛擬機器備份中的事件和警示。 根據警示傳送電子郵件。"
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a><span data-ttu-id="07ee0-104">監視 Azure 虛擬機器備份的警示</span><span class="sxs-lookup"><span data-stu-id="07ee0-104">Monitor alerts for Azure virtual machine backups</span></span>
<span data-ttu-id="07ee0-105">警示是事件閾值已達到或超過 hello 服務的回應。</span><span class="sxs-lookup"><span data-stu-id="07ee0-105">Alerts are responses from hello service that an event threshold has been met or surpassed.</span></span> <span data-ttu-id="07ee0-106">了解當問題開始可以重大 tookeeping 的商務成本。</span><span class="sxs-lookup"><span data-stu-id="07ee0-106">Knowing when problems start can be critical tookeeping business costs down.</span></span> <span data-ttu-id="07ee0-107">警示通常不會發生排程，並因此，很有幫助 tooknow 儘速之後便會產生警示。</span><span class="sxs-lookup"><span data-stu-id="07ee0-107">Alerts typically do not occur on a schedule, and so it is helpful tooknow as soon as possible after alerts occur.</span></span> <span data-ttu-id="07ee0-108">例如，當備份或還原作業失敗時，發生 hello 失敗的五分鐘內的警示。</span><span class="sxs-lookup"><span data-stu-id="07ee0-108">For example, when a backup or restore job fails, an alert occurs within five minutes of hello failure.</span></span> <span data-ttu-id="07ee0-109">Hello 保存庫儀表板中 hello 備份警示磚會顯示重大和警告層級的事件。</span><span class="sxs-lookup"><span data-stu-id="07ee0-109">In hello vault dashboard, hello Backup Alerts tile displays Critical and Warning-level events.</span></span> <span data-ttu-id="07ee0-110">在 hello 備份警示設定中，您可以檢視所有事件。</span><span class="sxs-lookup"><span data-stu-id="07ee0-110">In hello Backup Alerts settings, you can view all events.</span></span> <span data-ttu-id="07ee0-111">但是，如果在您處理不同問題時發生警示，您該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="07ee0-111">But what do you do if an alert occurs when you are working on a separate issue?</span></span> <span data-ttu-id="07ee0-112">如果您不知道 hello 警示時，它可能是次要的不便，或它可能會危及資料。</span><span class="sxs-lookup"><span data-stu-id="07ee0-112">If you don't know when hello alert happens, it could be a minor inconvenience, or it could compromise data.</span></span> <span data-ttu-id="07ee0-113">toomake 確定 hello 正確人員了解警示-它發生時，設定透過電子郵件的 hello 服務 toosend 警示通知。</span><span class="sxs-lookup"><span data-stu-id="07ee0-113">toomake sure hello correct people are aware of an alert - when it occurs, configure hello service toosend alert notifications via email.</span></span> <span data-ttu-id="07ee0-114">如需設定電子郵件通知的詳細資訊，請參閱 [設定通知](backup-azure-monitor-vms.md#configure-notifications)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-114">For details on setting up email notifications, see [Configure notifications](backup-azure-monitor-vms.md#configure-notifications).</span></span>

## <a name="how-do-i-find-information-about-hello-alerts"></a><span data-ttu-id="07ee0-115">如何找到 hello 警示的詳細資訊？</span><span class="sxs-lookup"><span data-stu-id="07ee0-115">How do I find information about hello alerts?</span></span>
<span data-ttu-id="07ee0-116">tooview 資訊有關 hello 擲回警示的事件，您必須開啟 hello 備份警示刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-116">tooview information about hello event that threw an alert, you must open hello Backup Alerts blade.</span></span> <span data-ttu-id="07ee0-117">有兩種方式 tooopen hello 備份警示刀鋒伺服器： 從備份警示磚 hello 保存庫儀表板中的 hello 或 hello 警示與事件刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-117">There are two ways tooopen hello Backup Alerts blade: either from hello Backup Alerts tile in hello vault dashboard, or from hello Alerts and Events blade.</span></span>

<span data-ttu-id="07ee0-118">tooopen hello 備份警示刀鋒視窗，從備份警示磚：</span><span class="sxs-lookup"><span data-stu-id="07ee0-118">tooopen hello Backup Alerts blade from Backup Alerts tile:</span></span>

* <span data-ttu-id="07ee0-119">在 hello**備份警示**hello 保存庫儀表板磚上，按一下 **重大**或**警告**tooview hello 操作該嚴重性層級的事件。</span><span class="sxs-lookup"><span data-stu-id="07ee0-119">On hello **Backup Alerts** tile on hello vault dashboard, click **Critical** or **Warning** tooview hello operational events for that severity level.</span></span>

    ![備份警示圖格](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

<span data-ttu-id="07ee0-121">tooopen hello 備份警示刀鋒視窗中的 hello 警示與事件刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="07ee0-121">tooopen hello Backup Alerts blade from hello Alerts and Events blade:</span></span>

1. <span data-ttu-id="07ee0-122">從 hello 保存庫儀表板中，按一下 **所有設定**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-122">From hello vault dashboard, click **All Settings**.</span></span> <span data-ttu-id="07ee0-123">![所有設定按鈕](./media/backup-azure-monitor-vms/all-settings-button.png)</span><span class="sxs-lookup"><span data-stu-id="07ee0-123">![All Settings button](./media/backup-azure-monitor-vms/all-settings-button.png)</span></span>
2. <span data-ttu-id="07ee0-124">在 hello**設定**刀鋒視窗中，按一下 **警示與事件**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-124">On hello **Settings** blade, click **Alerts and Events**.</span></span> <span data-ttu-id="07ee0-125">![警示和事件按鈕](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span><span class="sxs-lookup"><span data-stu-id="07ee0-125">![Alerts and Events button](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span></span>
3. <span data-ttu-id="07ee0-126">在 hello**警示與事件**刀鋒視窗中，按一下 **備份警示**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-126">On hello **Alerts and Events** blade, click **Backup Alerts**.</span></span> <span data-ttu-id="07ee0-127">![備份警示按鈕](./media/backup-azure-monitor-vms/backup-alerts.png)</span><span class="sxs-lookup"><span data-stu-id="07ee0-127">![Backup Alerts button](./media/backup-azure-monitor-vms/backup-alerts.png)</span></span>

    <span data-ttu-id="07ee0-128">hello**備份警示**刀鋒視窗會開啟並顯示 hello 篩選的警示。</span><span class="sxs-lookup"><span data-stu-id="07ee0-128">hello **Backup Alerts** blade opens and displays hello filtered alerts.</span></span>

    ![備份警示圖格](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. <span data-ttu-id="07ee0-130">tooview 詳細的資訊有關特定警示，從 hello 清單中的事件，按一下 hello 警示 tooopen 其**詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-130">tooview detailed information about a particular alert, from hello list of events, click hello alert tooopen its **Details** blade.</span></span>

    ![事件詳細資料](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    <span data-ttu-id="07ee0-132">toocustomize hello 屬性顯示在 [hello] 清單中，請參閱[檢視其他事件屬性](backup-azure-monitor-vms.md#view-additional-event-attributes)</span><span class="sxs-lookup"><span data-stu-id="07ee0-132">toocustomize hello attributes displayed in hello list, see [View additional event attributes](backup-azure-monitor-vms.md#view-additional-event-attributes)</span></span>

## <a name="configure-notifications"></a><span data-ttu-id="07ee0-133">設定通知</span><span class="sxs-lookup"><span data-stu-id="07ee0-133">Configure notifications</span></span>
 <span data-ttu-id="07ee0-134">您可以設定 hello 服務 toosend 透過 hello 過去一小時，或發生特定類型的事件時所發生的 hello 警示的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="07ee0-134">You can configure hello service toosend email notifications for hello alerts that occurred over hello past hour, or when particular types of events occur.</span></span>

<span data-ttu-id="07ee0-135">tooset 警示的電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="07ee0-135">tooset up email notifications for alerts</span></span>

1. <span data-ttu-id="07ee0-136">Hello 備份警示功能表上，按一下**設定通知**</span><span class="sxs-lookup"><span data-stu-id="07ee0-136">On hello Backup Alerts menu, click **Configure notifications**</span></span>

    ![備份警示功能表](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    <span data-ttu-id="07ee0-138">hello 通知設定 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="07ee0-138">hello Configure notifications blade opens.</span></span>

    ![設定通知刀鋒視窗](./media/backup-azure-monitor-vms/configure-notifications.png)
2. <span data-ttu-id="07ee0-140">在 hello 電子郵件通知，設定通知刀鋒視窗上按一下**上**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-140">On hello Configure notifications blade, for Email notifications, click **On**.</span></span>

    <span data-ttu-id="07ee0-141">hello 收件者和嚴重性對話方塊具有星號的下一個 toothem，因為該資訊是必要的。</span><span class="sxs-lookup"><span data-stu-id="07ee0-141">hello Recipients and Severity dialogs have a star next toothem because that information is required.</span></span> <span data-ttu-id="07ee0-142">提供至少一個電子郵件地址，然後選取至少一個嚴重性。</span><span class="sxs-lookup"><span data-stu-id="07ee0-142">Provide at least one email address, and select at least one Severity.</span></span>
3. <span data-ttu-id="07ee0-143">在 [hello**收件者 （電子郵件）** ] 對話方塊中，型別 hello 電子郵件地址收到 hello 通知的人員。</span><span class="sxs-lookup"><span data-stu-id="07ee0-143">In hello **Recipients (Email)** dialog, type hello email addresses for who receive hello notifications.</span></span> <span data-ttu-id="07ee0-144">使用 hello 格式： username@domainname.com。用分號分 (;) 分隔多個電子郵件位址。</span><span class="sxs-lookup"><span data-stu-id="07ee0-144">Use hello format: username@domainname.com. Separate multiple email addresses with a semicolon (;).</span></span>
4. <span data-ttu-id="07ee0-145">在 hello**通知**區域中，選擇**每個警示**toosend 通知時 hello 指定警示時，或**每小時摘要**toosend hello 過去一小時的摘要。</span><span class="sxs-lookup"><span data-stu-id="07ee0-145">In hello **Notify** area, choose **Per Alert** toosend notification when hello specified alert occurs, or **Hourly Digest** toosend a summary for hello past hour.</span></span>
5. <span data-ttu-id="07ee0-146">在 [hello**嚴重性**] 對話方塊中，選擇您想 tootrigger 的一或多個層級電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="07ee0-146">In hello **Severity** dialog, choose one or more levels that you want tootrigger email notification.</span></span>
6. <span data-ttu-id="07ee0-147">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="07ee0-147">Click **Save**.</span></span>

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a><span data-ttu-id="07ee0-148">有哪些警示類型可供 Azure IaaS VM 備份使用？</span><span class="sxs-lookup"><span data-stu-id="07ee0-148">What alert types are available for Azure IaaS VM backup?</span></span>
   | <span data-ttu-id="07ee0-149">警示層級</span><span class="sxs-lookup"><span data-stu-id="07ee0-149">Alert Level</span></span> | <span data-ttu-id="07ee0-150">傳送的警示</span><span class="sxs-lookup"><span data-stu-id="07ee0-150">Alerts sent</span></span> |
   | --- | --- |
   | <span data-ttu-id="07ee0-151">重要</span><span class="sxs-lookup"><span data-stu-id="07ee0-151">Critical</span></span> |<span data-ttu-id="07ee0-152">備份失敗、復原失敗</span><span class="sxs-lookup"><span data-stu-id="07ee0-152">Backup failure, recovery failure</span></span> |
   | <span data-ttu-id="07ee0-153">警告</span><span class="sxs-lookup"><span data-stu-id="07ee0-153">Warning</span></span> |<span data-ttu-id="07ee0-154">None</span><span class="sxs-lookup"><span data-stu-id="07ee0-154">None</span></span> |
   | <span data-ttu-id="07ee0-155">資訊</span><span class="sxs-lookup"><span data-stu-id="07ee0-155">Informational</span></span> |<span data-ttu-id="07ee0-156">None</span><span class="sxs-lookup"><span data-stu-id="07ee0-156">None</span></span> |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a><span data-ttu-id="07ee0-157">會有即使已設定通知卻不寄送電子郵件的情況嗎？</span><span class="sxs-lookup"><span data-stu-id="07ee0-157">Are there situations where email isn't sent even if notifications are configured?</span></span>
<span data-ttu-id="07ee0-158">有情況下，不會傳送警示，即使已正確設定 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="07ee0-158">There are situations where an alert is not sent, even though hello notifications have been properly configured.</span></span> <span data-ttu-id="07ee0-159">Hello 在下列情況下電子郵件不會傳送通知 tooavoid 警示的干擾：</span><span class="sxs-lookup"><span data-stu-id="07ee0-159">In hello following situations email notifications are not sent tooavoid alert noise:</span></span>

* <span data-ttu-id="07ee0-160">如果通知設定的 tooHourly 摘要，而且會引發和解決的警示 hello 一小時內。</span><span class="sxs-lookup"><span data-stu-id="07ee0-160">If notifications are configured tooHourly Digest, and an alert is raised and resolved within hello hour.</span></span>
* <span data-ttu-id="07ee0-161">hello 作業已取消。</span><span class="sxs-lookup"><span data-stu-id="07ee0-161">hello job is canceled.</span></span>
* <span data-ttu-id="07ee0-162">備份作業會觸發然後失敗，且另一個備份作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="07ee0-162">A backup job is triggered and then fails, and another backup job is in progress.</span></span>
* <span data-ttu-id="07ee0-163">啟用資源管理員的 VM 的排定備份工作會啟動，但 hello VM 不存在。</span><span class="sxs-lookup"><span data-stu-id="07ee0-163">A scheduled backup job for a Resource Manager-enabled VM starts, but hello VM no longer exists.</span></span>

## <a name="customize-your-view-of-events"></a><span data-ttu-id="07ee0-164">自訂事件的檢視</span><span class="sxs-lookup"><span data-stu-id="07ee0-164">Customize your view of events</span></span>
<span data-ttu-id="07ee0-165">hello**稽核記錄檔**設定隨附一組預先定義的篩選和資料行顯示操作事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-165">hello **Audit logs** setting comes with a pre-defined set of filters and columns showing operational event information.</span></span> <span data-ttu-id="07ee0-166">您可以自訂 hello 檢視，讓當 hello**事件**刀鋒視窗中開啟時，它會顯示您 hello 您想要的資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-166">You can customize hello view so that when hello **Events** blade opens, it shows you hello information you want.</span></span>

1. <span data-ttu-id="07ee0-167">在 hello[保存庫儀表板](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)，瀏覽 tooand 按一下**稽核記錄檔**tooopen hello**事件**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-167">In hello [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse tooand click **Audit Logs** tooopen hello **Events** blade.</span></span>

    ![稽核記錄檔](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="07ee0-169">hello**事件**刀鋒視窗會開啟 toohello 操作事件篩選，只供 hello 目前保存庫。</span><span class="sxs-lookup"><span data-stu-id="07ee0-169">hello **Events** blade opens toohello operational events filtered just for hello current vault.</span></span>

    ![稽核記錄檔篩選器](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    <span data-ttu-id="07ee0-171">hello 刀鋒視窗中顯示 hello 嚴重、 錯誤、 警告和參考發生的事件中清單 hello 過去一週。</span><span class="sxs-lookup"><span data-stu-id="07ee0-171">hello blade shows hello list of Critical, Error, Warning, and Informational events that occurred in hello past week.</span></span> <span data-ttu-id="07ee0-172">hello 時間範圍是預設值設定在 hello**篩選**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-172">hello time span is a default value set in hello **Filter**.</span></span> <span data-ttu-id="07ee0-173">hello**事件**刀鋒視窗也會顯示橫條圖 hello 事件發生時加以追蹤。</span><span class="sxs-lookup"><span data-stu-id="07ee0-173">hello **Events** blade also shows a bar chart tracking when hello events occurred.</span></span> <span data-ttu-id="07ee0-174">如果您不想 toosee hello 橫條圖中的，在 hello**事件**功能表上，按一下 **隱藏圖表**tootoggle 關閉 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="07ee0-174">If you don't want toosee hello bar chart, in hello **Events** menu, click **Hide chart** tootoggle off hello chart.</span></span> <span data-ttu-id="07ee0-175">hello 預設檢視的事件會顯示作業、 層級、 狀態、 資源和時間資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-175">hello default view of Events shows Operation, Level, Status, Resource, and Time information.</span></span> <span data-ttu-id="07ee0-176">公開其他事件屬性的相關資訊，請參閱 hello 區段[展開事件資訊](backup-azure-monitor-vms.md#view-additional-event-attributes)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-176">For information about exposing additional Event attributes, see hello section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>
2. <span data-ttu-id="07ee0-177">如需有關作業的事件，在 hello**作業**資料行中，按一下 操作事件 tooopen 其刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-177">For additional information on an operational event, in hello **Operation** column, click an operational event tooopen its blade.</span></span> <span data-ttu-id="07ee0-178">hello 刀鋒視窗會包含有關 hello 事件的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-178">hello blade contains detailed information about hello events.</span></span> <span data-ttu-id="07ee0-179">事件會依其相互關聯識別碼和一份 hello hello 時間範圍中發生的事件分組。</span><span class="sxs-lookup"><span data-stu-id="07ee0-179">Events are grouped by their correlation ID and a list of hello events that occurred in hello Time span.</span></span>

    ![Operation Details](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. <span data-ttu-id="07ee0-181">tooview 詳細的資訊關於特定事件，從 hello 清單中的事件，按一下 hello 事件 tooopen 其**詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-181">tooview detailed information about a particular event, from hello list of events, click hello event tooopen its **Details** blade.</span></span>

    ![事件詳細資料](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    <span data-ttu-id="07ee0-183">hello 事件層級資訊是詳細 hello 資訊取得。</span><span class="sxs-lookup"><span data-stu-id="07ee0-183">hello Event-level information is as detailed as hello information gets.</span></span> <span data-ttu-id="07ee0-184">如果您想看到這麼多資訊每個事件，並希望 tooadd 這更詳細說明 toohello**事件**刀鋒視窗中，請參閱 hello 節[展開事件資訊](backup-azure-monitor-vms.md#view-additional-event-attributes)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-184">If you prefer seeing this much information about each event, and would like tooadd this much detail toohello **Events** blade, see hello section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>

## <a name="customize-hello-event-filter"></a><span data-ttu-id="07ee0-185">自訂 hello 事件篩選器</span><span class="sxs-lookup"><span data-stu-id="07ee0-185">Customize hello event filter</span></span>
<span data-ttu-id="07ee0-186">使用 hello**篩選**tooadjust 或選擇特定刀鋒視窗中顯示的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-186">Use hello **Filter** tooadjust or choose hello information that appears in a particular blade.</span></span> <span data-ttu-id="07ee0-187">toofilter hello 事件資訊：</span><span class="sxs-lookup"><span data-stu-id="07ee0-187">toofilter hello event information:</span></span>

1. <span data-ttu-id="07ee0-188">在 hello[保存庫儀表板](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)，瀏覽 tooand 按一下**稽核記錄檔**tooopen hello**事件**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-188">In hello [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse tooand click **Audit Logs** tooopen hello **Events** blade.</span></span>

    ![稽核記錄檔](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="07ee0-190">hello**事件**刀鋒視窗會開啟 toohello 操作事件篩選，只供 hello 目前保存庫。</span><span class="sxs-lookup"><span data-stu-id="07ee0-190">hello **Events** blade opens toohello operational events filtered just for hello current vault.</span></span>

    ![稽核記錄檔篩選器](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. <span data-ttu-id="07ee0-192">在 hello**事件**功能表上，按一下 **篩選**tooopen 該刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-192">On hello **Events** menu, click **Filter** tooopen that blade.</span></span>

    ![開放篩選刀鋒視窗](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. <span data-ttu-id="07ee0-194">在 hello**篩選**刀鋒視窗中，調整 hello**層級**，**時間範圍**，和**呼叫端**篩選。</span><span class="sxs-lookup"><span data-stu-id="07ee0-194">On hello **Filter** blade, adjust hello **Level**, **Time span**, and **Caller** filters.</span></span> <span data-ttu-id="07ee0-195">hello 其他篩選器沒有因為 hello 復原服務保存庫的已設定 tooprovide hello 目前資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-195">hello other filters are not available since they were set tooprovide hello current information for hello Recovery Services vault.</span></span>

    ![稽核記錄檔查詢詳細資料](./media/backup-azure-monitor-vms/filter-blade.png)

    <span data-ttu-id="07ee0-197">您可以指定 hello**層級**的事件： 嚴重、 錯誤、 警告還是資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-197">You can specify hello **Level** of event: Critical, Error, Warning, or Informational.</span></span> <span data-ttu-id="07ee0-198">您可以選擇任何事件層級組合，但必須選取至少一個層級。</span><span class="sxs-lookup"><span data-stu-id="07ee0-198">You can choose any combination of event Levels, but you must have at least one Level selected.</span></span> <span data-ttu-id="07ee0-199">開啟或關閉切換 hello 層級。</span><span class="sxs-lookup"><span data-stu-id="07ee0-199">Toggle hello Level on or off.</span></span> <span data-ttu-id="07ee0-200">hello**時間範圍**篩選可讓您 toospecify hello 擷取事件的時間長度。</span><span class="sxs-lookup"><span data-stu-id="07ee0-200">hello **Time span** filter allows you toospecify hello length of time for capturing events.</span></span> <span data-ttu-id="07ee0-201">如果您使用自訂的時間範圍，您可以設定 hello 的開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="07ee0-201">If you use a custom Time span, you can set hello start and end times.</span></span>
4. <span data-ttu-id="07ee0-202">當您準備好 tooquery hello 作業記錄檔使用篩選器，請按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-202">Once you are ready tooquery hello operations logs using your filter, click **Update**.</span></span> <span data-ttu-id="07ee0-203">hello 結果都會顯示在 hello**事件**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-203">hello results display in hello **Events** blade.</span></span>

    ![Operation Details](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a><span data-ttu-id="07ee0-205">檢視其他事件屬性</span><span class="sxs-lookup"><span data-stu-id="07ee0-205">View additional event attributes</span></span>
<span data-ttu-id="07ee0-206">使用 hello**資料行** 按鈕，您可以啟用在 hello 的 hello 清單中的其他事件屬性 tooappear**事件**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-206">Using hello **Columns** button, you can enable additional event attributes tooappear in hello list on hello **Events** blade.</span></span> <span data-ttu-id="07ee0-207">hello 預設清單的事件顯示作業、 層級、 狀態、 資源和時間的資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-207">hello default list of events displays information for Operation, Level, Status, Resource, and Time.</span></span> <span data-ttu-id="07ee0-208">tooenable 額外屬性：</span><span class="sxs-lookup"><span data-stu-id="07ee0-208">tooenable additional attributes:</span></span>

1. <span data-ttu-id="07ee0-209">在 hello**事件**刀鋒視窗中，按一下 **資料行**。</span><span class="sxs-lookup"><span data-stu-id="07ee0-209">On hello **Events** blade, click **Columns**.</span></span>

    ![開啟資料行](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    <span data-ttu-id="07ee0-211">hello**選擇資料行**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="07ee0-211">hello **Choose columns** blade opens.</span></span>

    ![資料行刀鋒視窗](./media/backup-azure-monitor-vms/columns-blade.png)
2. <span data-ttu-id="07ee0-213">tooselect hello 屬性，請按一下 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-213">tooselect hello attribute, click hello checkbox.</span></span> <span data-ttu-id="07ee0-214">hello 屬性核取方塊切換開啟 / 關閉。</span><span class="sxs-lookup"><span data-stu-id="07ee0-214">hello attribute checkbox toggles on and off.</span></span>
3. <span data-ttu-id="07ee0-215">按一下**重設**tooreset hello 份屬性清單中 hello**事件**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07ee0-215">Click **Reset** tooreset hello list of attributes in hello **Events** blade.</span></span> <span data-ttu-id="07ee0-216">在之後新增或移除屬性 hello 清單中，使用**重設**tooview hello 新的事件屬性清單。</span><span class="sxs-lookup"><span data-stu-id="07ee0-216">After adding or removing attributes from hello list, use **Reset** tooview hello new list of Event attributes.</span></span>
4. <span data-ttu-id="07ee0-217">按一下**更新**tooupdate hello hello 事件屬性的資料。</span><span class="sxs-lookup"><span data-stu-id="07ee0-217">Click **Update** tooupdate hello data in hello Event attributes.</span></span> <span data-ttu-id="07ee0-218">hello 下表提供每個屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="07ee0-218">hello following table provides information about each attribute.</span></span>

| <span data-ttu-id="07ee0-219">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="07ee0-219">Column name</span></span> | <span data-ttu-id="07ee0-220">說明</span><span class="sxs-lookup"><span data-stu-id="07ee0-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07ee0-221">作業</span><span class="sxs-lookup"><span data-stu-id="07ee0-221">Operation</span></span> |<span data-ttu-id="07ee0-222">hello hello 作業名稱</span><span class="sxs-lookup"><span data-stu-id="07ee0-222">hello name of hello operation</span></span> |
| <span data-ttu-id="07ee0-223">Level</span><span class="sxs-lookup"><span data-stu-id="07ee0-223">Level</span></span> |<span data-ttu-id="07ee0-224">hello 層級 hello 作業的值可以是： 參考、 警告、 錯誤或嚴重</span><span class="sxs-lookup"><span data-stu-id="07ee0-224">hello level of hello operation, values can be: Informational, Warning, Error, or Critical</span></span> |
| <span data-ttu-id="07ee0-225">狀態</span><span class="sxs-lookup"><span data-stu-id="07ee0-225">Status</span></span> |<span data-ttu-id="07ee0-226">描述作業狀態的 hello</span><span class="sxs-lookup"><span data-stu-id="07ee0-226">Descriptive state of hello operation</span></span> |
| <span data-ttu-id="07ee0-227">資源</span><span class="sxs-lookup"><span data-stu-id="07ee0-227">Resource</span></span> |<span data-ttu-id="07ee0-228">URL 識別 hello 資源;也稱為 hello 資源識別碼</span><span class="sxs-lookup"><span data-stu-id="07ee0-228">URL that identifies hello resource; also known as hello resource ID</span></span> |
| <span data-ttu-id="07ee0-229">時間</span><span class="sxs-lookup"><span data-stu-id="07ee0-229">Time</span></span> |<span data-ttu-id="07ee0-230">測量從 hello hello 事件發生的目前時間的時間</span><span class="sxs-lookup"><span data-stu-id="07ee0-230">Time, measured from hello current time, when hello event occurred</span></span> |
| <span data-ttu-id="07ee0-231">呼叫者</span><span class="sxs-lookup"><span data-stu-id="07ee0-231">Caller</span></span> |<span data-ttu-id="07ee0-232">人員或所呼叫或觸發 hello 事件;可以是 hello 系統或使用者</span><span class="sxs-lookup"><span data-stu-id="07ee0-232">Who or what called or triggered hello event; can be hello system, or a user</span></span> |
| <span data-ttu-id="07ee0-233">Timestamp</span><span class="sxs-lookup"><span data-stu-id="07ee0-233">Timestamp</span></span> |<span data-ttu-id="07ee0-234">hello 事件所觸發的 hello 時間</span><span class="sxs-lookup"><span data-stu-id="07ee0-234">hello time when hello event was triggered</span></span> |
| <span data-ttu-id="07ee0-235">資源群組</span><span class="sxs-lookup"><span data-stu-id="07ee0-235">Resource Group</span></span> |<span data-ttu-id="07ee0-236">hello 相關聯的資源群組</span><span class="sxs-lookup"><span data-stu-id="07ee0-236">hello associated resource group</span></span> |
| <span data-ttu-id="07ee0-237">資源類型</span><span class="sxs-lookup"><span data-stu-id="07ee0-237">Resource Type</span></span> |<span data-ttu-id="07ee0-238">使用資源管理員的 hello 內部資源類型</span><span class="sxs-lookup"><span data-stu-id="07ee0-238">hello internal resource type used by Resource Manager</span></span> |
| <span data-ttu-id="07ee0-239">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="07ee0-239">Subscription ID</span></span> |<span data-ttu-id="07ee0-240">hello 相關聯的訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="07ee0-240">hello associated subscription ID</span></span> |
| <span data-ttu-id="07ee0-241">類別</span><span class="sxs-lookup"><span data-stu-id="07ee0-241">Category</span></span> |<span data-ttu-id="07ee0-242">Hello 事件的類別目錄</span><span class="sxs-lookup"><span data-stu-id="07ee0-242">Category of hello event</span></span> |
| <span data-ttu-id="07ee0-243">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="07ee0-243">Correlation ID</span></span> |<span data-ttu-id="07ee0-244">相關事件的通用識別碼</span><span class="sxs-lookup"><span data-stu-id="07ee0-244">Common ID for related events</span></span> |

## <a name="use-powershell-toocustomize-alerts"></a><span data-ttu-id="07ee0-245">使用 PowerShell toocustomize 警示</span><span class="sxs-lookup"><span data-stu-id="07ee0-245">Use PowerShell toocustomize alerts</span></span>
<span data-ttu-id="07ee0-246">您可以在 hello 入口網站取得 hello 工作的自訂警示通知。</span><span class="sxs-lookup"><span data-stu-id="07ee0-246">You can get custom alert notifications for hello jobs in hello portal.</span></span> <span data-ttu-id="07ee0-247">這些作業，tooget 定義 PowerShell 為基礎的警示規則上操作的 hello 記錄的事件。</span><span class="sxs-lookup"><span data-stu-id="07ee0-247">tooget these jobs, define PowerShell-based alert rules on hello operational logs events.</span></span> <span data-ttu-id="07ee0-248">使用 PowerShell 1.3.0 版或更新版本 。</span><span class="sxs-lookup"><span data-stu-id="07ee0-248">Use *PowerShell version 1.3.0 or later*.</span></span>

<span data-ttu-id="07ee0-249">toodefine 自訂通知 tooalert 備份失敗，使用下列指令碼的 hello 類似的命令：</span><span class="sxs-lookup"><span data-stu-id="07ee0-249">toodefine a custom notification tooalert for backup failures, use a command like hello following script:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="07ee0-250">**ResourceId** ： 您可以取得 ResourceId hello 從稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="07ee0-250">**ResourceId** : You can get ResourceId from hello Audit logs.</span></span> <span data-ttu-id="07ee0-251">hello ResourceId 是 hello 資源 欄中的 hello 作業記錄檔中提供的 URL。</span><span class="sxs-lookup"><span data-stu-id="07ee0-251">hello ResourceId is a URL provided in hello Resource column of hello Operation logs.</span></span>

<span data-ttu-id="07ee0-252">**OperationName** : OperationName 的 hello 格式"Microsoft.RecoveryServices/recoveryServicesVault/*EventName*"其中*EventName*可以是：</span><span class="sxs-lookup"><span data-stu-id="07ee0-252">**OperationName** : OperationName is in hello format "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" where *EventName* can be:</span></span><br/>

* <span data-ttu-id="07ee0-253">註冊</span><span class="sxs-lookup"><span data-stu-id="07ee0-253">Register</span></span> <br/>
* <span data-ttu-id="07ee0-254">Unregister </span><span class="sxs-lookup"><span data-stu-id="07ee0-254">Unregister</span></span> <br/>
* <span data-ttu-id="07ee0-255">ConfigureProtection </span><span class="sxs-lookup"><span data-stu-id="07ee0-255">ConfigureProtection</span></span> <br/>
* <span data-ttu-id="07ee0-256">Backup </span><span class="sxs-lookup"><span data-stu-id="07ee0-256">Backup</span></span> <br/>
* <span data-ttu-id="07ee0-257">Restore </span><span class="sxs-lookup"><span data-stu-id="07ee0-257">Restore</span></span> <br/>
* <span data-ttu-id="07ee0-258">StopProtection </span><span class="sxs-lookup"><span data-stu-id="07ee0-258">StopProtection</span></span> <br/>
* <span data-ttu-id="07ee0-259">DeleteBackupData </span><span class="sxs-lookup"><span data-stu-id="07ee0-259">DeleteBackupData</span></span> <br/>
* <span data-ttu-id="07ee0-260">CreateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="07ee0-260">CreateProtectionPolicy</span></span> <br/>
* <span data-ttu-id="07ee0-261">DeleteProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="07ee0-261">DeleteProtectionPolicy</span></span> <br/>
* <span data-ttu-id="07ee0-262">UpdateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="07ee0-262">UpdateProtectionPolicy</span></span> <br/>

<span data-ttu-id="07ee0-263">**Status** ：支援的值為 [已開始]、[成功] 或 [失敗]。</span><span class="sxs-lookup"><span data-stu-id="07ee0-263">**Status** : Supported values are Started, Succeeded, or Failed.</span></span>

<span data-ttu-id="07ee0-264">**ResourceGroup** ： 這是 hello toowhich hello 資源所屬的資源群組。</span><span class="sxs-lookup"><span data-stu-id="07ee0-264">**ResourceGroup** : This is hello Resource Group toowhich hello resource belongs.</span></span> <span data-ttu-id="07ee0-265">您可以加入 hello 資源群組資料行 toohello 產生記錄檔。</span><span class="sxs-lookup"><span data-stu-id="07ee0-265">You can add hello Resource Group column toohello generated logs.</span></span> <span data-ttu-id="07ee0-266">資源群組是其中一個 hello 可用的事件資訊的類型。</span><span class="sxs-lookup"><span data-stu-id="07ee0-266">Resource Group is one of hello available types of event information.</span></span>

<span data-ttu-id="07ee0-267">**名稱**: hello 警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="07ee0-267">**Name** : Name of hello Alert Rule.</span></span>

<span data-ttu-id="07ee0-268">**CustomEmail** ： 指定您要警示的通知 toosend hello 自訂電子郵件地址 toowhich</span><span class="sxs-lookup"><span data-stu-id="07ee0-268">**CustomEmail** : Specify hello custom email address toowhich you want toosend an alert notification</span></span>

<span data-ttu-id="07ee0-269">**SendToServiceOwners** ： 這個選項會傳送警示通知 tooall 系統管理員和共同管理員的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07ee0-269">**SendToServiceOwners** : This option sends alert notifications tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="07ee0-270">它可以用於 **New-AzureRmAlertRuleEmail** Cmdlet 中</span><span class="sxs-lookup"><span data-stu-id="07ee0-270">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="07ee0-271">警示的限制</span><span class="sxs-lookup"><span data-stu-id="07ee0-271">Limitations on Alerts</span></span>
<span data-ttu-id="07ee0-272">以事件為基礎的警示是主體 toohello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="07ee0-272">Event-based alerts are subject toohello following limitations:</span></span>

1. <span data-ttu-id="07ee0-273">Hello 復原服務保存庫中的所有虛擬機器上便會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="07ee0-273">Alerts are triggered on all virtual machines in hello Recovery Services vault.</span></span> <span data-ttu-id="07ee0-274">您無法自訂 hello 警示復原服務保存庫中的虛擬機器的子集。</span><span class="sxs-lookup"><span data-stu-id="07ee0-274">You cannot customize hello alert for a subset of virtual machines in a Recovery Services vault.</span></span>
2. <span data-ttu-id="07ee0-275">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="07ee0-275">This feature is in Preview.</span></span> [<span data-ttu-id="07ee0-276">深入了解</span><span class="sxs-lookup"><span data-stu-id="07ee0-276">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="07ee0-277">"alerts-noreply@mail.windowsazure.com" 會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="07ee0-277">Alerts are sent from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="07ee0-278">目前您無法修改 hello 電子郵件寄件者。</span><span class="sxs-lookup"><span data-stu-id="07ee0-278">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07ee0-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07ee0-279">Next steps</span></span>
<span data-ttu-id="07ee0-280">事件記錄檔啟用絕佳事後和稽核 hello 備份作業的支援。</span><span class="sxs-lookup"><span data-stu-id="07ee0-280">Event logs enable great post-mortem and audit support for hello backup operations.</span></span> <span data-ttu-id="07ee0-281">記錄 hello 下列作業：</span><span class="sxs-lookup"><span data-stu-id="07ee0-281">hello following operations are logged:</span></span>

* <span data-ttu-id="07ee0-282">註冊</span><span class="sxs-lookup"><span data-stu-id="07ee0-282">Register</span></span>
* <span data-ttu-id="07ee0-283">Unregister </span><span class="sxs-lookup"><span data-stu-id="07ee0-283">Unregister</span></span>
* <span data-ttu-id="07ee0-284">設定保護</span><span class="sxs-lookup"><span data-stu-id="07ee0-284">Configure protection</span></span>
* <span data-ttu-id="07ee0-285">備份 (排程和隨選備份兩者)</span><span class="sxs-lookup"><span data-stu-id="07ee0-285">Backup (Both scheduled as well as on-demand backup)</span></span>
* <span data-ttu-id="07ee0-286">Restore </span><span class="sxs-lookup"><span data-stu-id="07ee0-286">Restore</span></span>
* <span data-ttu-id="07ee0-287">停止保護</span><span class="sxs-lookup"><span data-stu-id="07ee0-287">Stop protection</span></span>
* <span data-ttu-id="07ee0-288">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="07ee0-288">Delete backup data</span></span>
* <span data-ttu-id="07ee0-289">Add policy</span><span class="sxs-lookup"><span data-stu-id="07ee0-289">Add policy</span></span>
* <span data-ttu-id="07ee0-290">刪除原則</span><span class="sxs-lookup"><span data-stu-id="07ee0-290">Delete policy</span></span>
* <span data-ttu-id="07ee0-291">更新原則</span><span class="sxs-lookup"><span data-stu-id="07ee0-291">Update policy</span></span>
* <span data-ttu-id="07ee0-292">取消工作</span><span class="sxs-lookup"><span data-stu-id="07ee0-292">Cancel job</span></span>

<span data-ttu-id="07ee0-293">如需事件、 作業和跨 hello 的稽核記錄檔的廣泛說明 Azure 服務，請參閱 hello 文章[檢視的事件，並稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-293">For a broad explanation of events, operations, and audit logs across hello Azure services, see hello article, [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span></span>

<span data-ttu-id="07ee0-294">如需從復原點重新建立虛擬機器的詳細資訊，請參閱 [還原 Azure VM](backup-azure-restore-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-294">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="07ee0-295">如果您需要保護虛擬機器的詳細資訊，請參閱[第一印象： 備份復原服務保存庫的 Vm tooa](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-295">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="07ee0-296">深入了解 hello hello 文章中的 VM 備份的管理工作[管理 Azure 虛擬機器備份](backup-azure-manage-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="07ee0-296">Learn about hello management tasks for VM backups in hello article, [Manage Azure virtual machine backups](backup-azure-manage-vms.md).</span></span>
