---
title: "監視 Resource Manager 部署的虛擬機器備份 | Microsoft Docs"
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
ms.openlocfilehash: b9dc3f52e5fc275bc56b9964f2115833f2dde42e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a><span data-ttu-id="11a60-104">監視 Azure 虛擬機器備份的警示</span><span class="sxs-lookup"><span data-stu-id="11a60-104">Monitor alerts for Azure virtual machine backups</span></span>
<span data-ttu-id="11a60-105">警示是來自已達到或超過事件閾值之服務的回應。</span><span class="sxs-lookup"><span data-stu-id="11a60-105">Alerts are responses from the service that an event threshold has been met or surpassed.</span></span> <span data-ttu-id="11a60-106">了解何時出現問題，可能對於維持低商務成本很重要。</span><span class="sxs-lookup"><span data-stu-id="11a60-106">Knowing when problems start can be critical to keeping business costs down.</span></span> <span data-ttu-id="11a60-107">警示通常不會依照排程發生，因此在警示發生之後盡早得知將會有所幫助。</span><span class="sxs-lookup"><span data-stu-id="11a60-107">Alerts typically do not occur on a schedule, and so it is helpful to know as soon as possible after alerts occur.</span></span> <span data-ttu-id="11a60-108">例如，當備份或還原作業失敗時，警示會在失敗後五分鐘內發生。</span><span class="sxs-lookup"><span data-stu-id="11a60-108">For example, when a backup or restore job fails, an alert occurs within five minutes of the failure.</span></span> <span data-ttu-id="11a60-109">在保存庫儀表板中，[備份警示] 圖格會顯示嚴重和警告層級的事件。</span><span class="sxs-lookup"><span data-stu-id="11a60-109">In the vault dashboard, the Backup Alerts tile displays Critical and Warning-level events.</span></span> <span data-ttu-id="11a60-110">在 [備份警示] 設定中，您可以檢視所有事件。</span><span class="sxs-lookup"><span data-stu-id="11a60-110">In the Backup Alerts settings, you can view all events.</span></span> <span data-ttu-id="11a60-111">但是，如果在您處理不同問題時發生警示，您該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="11a60-111">But what do you do if an alert occurs when you are working on a separate issue?</span></span> <span data-ttu-id="11a60-112">如果您不知道何時發生警示，可能會有點不便，或可能危及資料。</span><span class="sxs-lookup"><span data-stu-id="11a60-112">If you don't know when the alert happens, it could be a minor inconvenience, or it could compromise data.</span></span> <span data-ttu-id="11a60-113">若要確定正確的人員會留意警示 (當它發生時)，請設定服務以透過電子郵件傳送警示通知。</span><span class="sxs-lookup"><span data-stu-id="11a60-113">To make sure the correct people are aware of an alert - when it occurs, configure the service to send alert notifications via email.</span></span> <span data-ttu-id="11a60-114">如需設定電子郵件通知的詳細資訊，請參閱 [設定通知](backup-azure-monitor-vms.md#configure-notifications)。</span><span class="sxs-lookup"><span data-stu-id="11a60-114">For details on setting up email notifications, see [Configure notifications](backup-azure-monitor-vms.md#configure-notifications).</span></span>

## <a name="how-do-i-find-information-about-the-alerts"></a><span data-ttu-id="11a60-115">如何找到警示的相關資訊？</span><span class="sxs-lookup"><span data-stu-id="11a60-115">How do I find information about the alerts?</span></span>
<span data-ttu-id="11a60-116">若要檢視擲回警示的事件相關資訊，您必須開啟 [備份警示] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-116">To view information about the event that threw an alert, you must open the Backup Alerts blade.</span></span> <span data-ttu-id="11a60-117">開啟 [備份警示] 刀鋒視窗的方法有兩種︰從保存庫儀表板中的 [備份警示] 圖格，或從 [警示和事件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-117">There are two ways to open the Backup Alerts blade: either from the Backup Alerts tile in the vault dashboard, or from the Alerts and Events blade.</span></span>

<span data-ttu-id="11a60-118">若要從 [備份警示] 圖格開啟 [備份警示] 刀鋒視窗︰</span><span class="sxs-lookup"><span data-stu-id="11a60-118">To open the Backup Alerts blade from Backup Alerts tile:</span></span>

* <span data-ttu-id="11a60-119">在保存庫儀表板的 [備份警示] 圖格上，按一下 [嚴重] 或 [警告] 以檢視該嚴重性層級的作業事件。</span><span class="sxs-lookup"><span data-stu-id="11a60-119">On the **Backup Alerts** tile on the vault dashboard, click **Critical** or **Warning** to view the operational events for that severity level.</span></span>

    ![備份警示圖格](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

<span data-ttu-id="11a60-121">若要從 [警示和事件] 刀鋒視窗開啟 [備份警示] 刀鋒視窗︰</span><span class="sxs-lookup"><span data-stu-id="11a60-121">To open the Backup Alerts blade from the Alerts and Events blade:</span></span>

1. <span data-ttu-id="11a60-122">在保存庫儀表板中，按一下 [所有設定] 。</span><span class="sxs-lookup"><span data-stu-id="11a60-122">From the vault dashboard, click **All Settings**.</span></span> <span data-ttu-id="11a60-123">![所有設定按鈕](./media/backup-azure-monitor-vms/all-settings-button.png)</span><span class="sxs-lookup"><span data-stu-id="11a60-123">![All Settings button](./media/backup-azure-monitor-vms/all-settings-button.png)</span></span>
2. <span data-ttu-id="11a60-124">在 [設定] 刀鋒視窗上，按一下 [警示和事件]。</span><span class="sxs-lookup"><span data-stu-id="11a60-124">On the **Settings** blade, click **Alerts and Events**.</span></span> <span data-ttu-id="11a60-125">![警示和事件按鈕](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span><span class="sxs-lookup"><span data-stu-id="11a60-125">![Alerts and Events button](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span></span>
3. <span data-ttu-id="11a60-126">在 [警示與事件] 刀鋒視窗上，按一下 [備份警示]。</span><span class="sxs-lookup"><span data-stu-id="11a60-126">On the **Alerts and Events** blade, click **Backup Alerts**.</span></span> <span data-ttu-id="11a60-127">![備份警示按鈕](./media/backup-azure-monitor-vms/backup-alerts.png)</span><span class="sxs-lookup"><span data-stu-id="11a60-127">![Backup Alerts button](./media/backup-azure-monitor-vms/backup-alerts.png)</span></span>

    <span data-ttu-id="11a60-128">[備份警示]  刀鋒視窗會開啟並顯示篩選後的警示。</span><span class="sxs-lookup"><span data-stu-id="11a60-128">The **Backup Alerts** blade opens and displays the filtered alerts.</span></span>

    ![備份警示圖格](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. <span data-ttu-id="11a60-130">若要檢視特定警示的詳細資訊，請從事件清單中按一下警示，以開啟其 [詳細資料]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-130">To view detailed information about a particular alert, from the list of events, click the alert to open its **Details** blade.</span></span>

    ![事件詳細資料](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    <span data-ttu-id="11a60-132">若要自訂清單中顯示的屬性，請參閱 [檢視其他事件屬性](backup-azure-monitor-vms.md#view-additional-event-attributes)</span><span class="sxs-lookup"><span data-stu-id="11a60-132">To customize the attributes displayed in the list, see [View additional event attributes](backup-azure-monitor-vms.md#view-additional-event-attributes)</span></span>

## <a name="configure-notifications"></a><span data-ttu-id="11a60-133">設定通知</span><span class="sxs-lookup"><span data-stu-id="11a60-133">Configure notifications</span></span>
 <span data-ttu-id="11a60-134">您可以設定服務以針對過去一小時發生的警示，或在特定類型的事件發生時，傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="11a60-134">You can configure the service to send email notifications for the alerts that occurred over the past hour, or when particular types of events occur.</span></span>

<span data-ttu-id="11a60-135">設定警示的電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="11a60-135">To set up email notifications for alerts</span></span>

1. <span data-ttu-id="11a60-136">在 [備份警示] 功能表上，按一下 [設定通知] </span><span class="sxs-lookup"><span data-stu-id="11a60-136">On the Backup Alerts menu, click **Configure notifications**</span></span>

    ![備份警示功能表](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    <span data-ttu-id="11a60-138">[設定通知] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="11a60-138">The Configure notifications blade opens.</span></span>

    ![設定通知刀鋒視窗](./media/backup-azure-monitor-vms/configure-notifications.png)
2. <span data-ttu-id="11a60-140">在 [設定通知] 刀鋒視窗上，針對 [電子郵件通知]，按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="11a60-140">On the Configure notifications blade, for Email notifications, click **On**.</span></span>

    <span data-ttu-id="11a60-141">[收件者] 和 [嚴重性] 對話方塊旁邊有星號，因為該資訊是必要的。</span><span class="sxs-lookup"><span data-stu-id="11a60-141">The Recipients and Severity dialogs have a star next to them because that information is required.</span></span> <span data-ttu-id="11a60-142">提供至少一個電子郵件地址，然後選取至少一個嚴重性。</span><span class="sxs-lookup"><span data-stu-id="11a60-142">Provide at least one email address, and select at least one Severity.</span></span>
3. <span data-ttu-id="11a60-143">在 [收件者 (電子郵件)]  對話方塊中，輸入接收通知者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="11a60-143">In the **Recipients (Email)** dialog, type the email addresses for who receive the notifications.</span></span> <span data-ttu-id="11a60-144">使用格式︰username@domainname.com。用分號分 (;) 分隔多個電子郵件位址。</span><span class="sxs-lookup"><span data-stu-id="11a60-144">Use the format: username@domainname.com. Separate multiple email addresses with a semicolon (;).</span></span>
4. <span data-ttu-id="11a60-145">在 [通知] 區域中，選擇 [每個警示] 以在指定的警示發生時傳送通知，或選擇 [每小時摘要] 以傳送過去一小時的摘要。</span><span class="sxs-lookup"><span data-stu-id="11a60-145">In the **Notify** area, choose **Per Alert** to send notification when the specified alert occurs, or **Hourly Digest** to send a summary for the past hour.</span></span>
5. <span data-ttu-id="11a60-146">在 [嚴重性]  對話方塊中，選擇您要觸發電子郵件通知的一或多個層級。</span><span class="sxs-lookup"><span data-stu-id="11a60-146">In the **Severity** dialog, choose one or more levels that you want to trigger email notification.</span></span>
6. <span data-ttu-id="11a60-147">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="11a60-147">Click **Save**.</span></span>

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a><span data-ttu-id="11a60-148">有哪些警示類型可供 Azure IaaS VM 備份使用？</span><span class="sxs-lookup"><span data-stu-id="11a60-148">What alert types are available for Azure IaaS VM backup?</span></span>
   | <span data-ttu-id="11a60-149">警示層級</span><span class="sxs-lookup"><span data-stu-id="11a60-149">Alert Level</span></span> | <span data-ttu-id="11a60-150">傳送的警示</span><span class="sxs-lookup"><span data-stu-id="11a60-150">Alerts sent</span></span> |
   | --- | --- |
   | <span data-ttu-id="11a60-151">重要</span><span class="sxs-lookup"><span data-stu-id="11a60-151">Critical</span></span> |<span data-ttu-id="11a60-152">備份失敗、復原失敗</span><span class="sxs-lookup"><span data-stu-id="11a60-152">Backup failure, recovery failure</span></span> |
   | <span data-ttu-id="11a60-153">警告</span><span class="sxs-lookup"><span data-stu-id="11a60-153">Warning</span></span> |<span data-ttu-id="11a60-154">None</span><span class="sxs-lookup"><span data-stu-id="11a60-154">None</span></span> |
   | <span data-ttu-id="11a60-155">資訊</span><span class="sxs-lookup"><span data-stu-id="11a60-155">Informational</span></span> |<span data-ttu-id="11a60-156">None</span><span class="sxs-lookup"><span data-stu-id="11a60-156">None</span></span> |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a><span data-ttu-id="11a60-157">會有即使已設定通知卻不寄送電子郵件的情況嗎？</span><span class="sxs-lookup"><span data-stu-id="11a60-157">Are there situations where email isn't sent even if notifications are configured?</span></span>
<span data-ttu-id="11a60-158">即使已正確設定通知，仍會有不寄送警示的情況。</span><span class="sxs-lookup"><span data-stu-id="11a60-158">There are situations where an alert is not sent, even though the notifications have been properly configured.</span></span> <span data-ttu-id="11a60-159">在下列情況下將不會寄送電子郵件通知，以避免警示雜訊︰</span><span class="sxs-lookup"><span data-stu-id="11a60-159">In the following situations email notifications are not sent to avoid alert noise:</span></span>

* <span data-ttu-id="11a60-160">如果通知設定為 [每小時摘要]，而且在一小時內引發警示並加以解決，</span><span class="sxs-lookup"><span data-stu-id="11a60-160">If notifications are configured to Hourly Digest, and an alert is raised and resolved within the hour.</span></span>
* <span data-ttu-id="11a60-161">作業便會取消。</span><span class="sxs-lookup"><span data-stu-id="11a60-161">The job is canceled.</span></span>
* <span data-ttu-id="11a60-162">備份作業會觸發然後失敗，且另一個備份作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="11a60-162">A backup job is triggered and then fails, and another backup job is in progress.</span></span>
* <span data-ttu-id="11a60-163">啟用 Resource Manager 功能之 VM 的排程備份作業會啟動，但 VM 將不再存在。</span><span class="sxs-lookup"><span data-stu-id="11a60-163">A scheduled backup job for a Resource Manager-enabled VM starts, but the VM no longer exists.</span></span>

## <a name="customize-your-view-of-events"></a><span data-ttu-id="11a60-164">自訂事件的檢視</span><span class="sxs-lookup"><span data-stu-id="11a60-164">Customize your view of events</span></span>
<span data-ttu-id="11a60-165">[稽核記錄檔]  設定隨附一組預先定義的篩選器和資料行，以顯示作業事件資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-165">The **Audit logs** setting comes with a pre-defined set of filters and columns showing operational event information.</span></span> <span data-ttu-id="11a60-166">您可以自訂檢視，因此當 [事件]  刀鋒視窗開啟時，它會顯示您所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-166">You can customize the view so that when the **Events** blade opens, it shows you the information you want.</span></span>

1. <span data-ttu-id="11a60-167">在[保存庫儀表板](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)中，瀏覽並按一下 [稽核記錄檔]，以開啟 [事件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-167">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span></span>

    ![稽核記錄檔](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="11a60-169">開啟的 [事件]  刀鋒視窗會顯示針對目前保存庫而篩選的作業事件。</span><span class="sxs-lookup"><span data-stu-id="11a60-169">The **Events** blade opens to the operational events filtered just for the current vault.</span></span>

    ![稽核記錄檔篩選器](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    <span data-ttu-id="11a60-171">此刀鋒視窗會顯示過去一週發生的嚴重、錯誤、警告和資訊事件清單。</span><span class="sxs-lookup"><span data-stu-id="11a60-171">The blade shows the list of Critical, Error, Warning, and Informational events that occurred in the past week.</span></span> <span data-ttu-id="11a60-172">時間範圍是在 [篩選] 中設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="11a60-172">The time span is a default value set in the **Filter**.</span></span> <span data-ttu-id="11a60-173">[事件]  刀鋒視窗也會顯示橫條圖來追蹤事件發生的時間。</span><span class="sxs-lookup"><span data-stu-id="11a60-173">The **Events** blade also shows a bar chart tracking when the events occurred.</span></span> <span data-ttu-id="11a60-174">如果您不想看到橫條圖，請在 [事件] 功能表中按一下 [隱藏圖表] 以關閉圖表。</span><span class="sxs-lookup"><span data-stu-id="11a60-174">If you don't want to see the bar chart, in the **Events** menu, click **Hide chart** to toggle off the chart.</span></span> <span data-ttu-id="11a60-175">[事件] 的預設檢視會顯示 [作業]、[層級]、[狀態]、[資源] 和 [時間] 資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-175">The default view of Events shows Operation, Level, Status, Resource, and Time information.</span></span> <span data-ttu-id="11a60-176">如需公開其他事件屬性的相關資訊，請參閱 [展開事件資訊](backup-azure-monitor-vms.md#view-additional-event-attributes)一節。</span><span class="sxs-lookup"><span data-stu-id="11a60-176">For information about exposing additional Event attributes, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>
2. <span data-ttu-id="11a60-177">如需作業事件的其他資訊，請在 [作業]  資料行中，按一下作業事件以開啟其刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-177">For additional information on an operational event, in the **Operation** column, click an operational event to open its blade.</span></span> <span data-ttu-id="11a60-178">此刀鋒視窗包含事件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-178">The blade contains detailed information about the events.</span></span> <span data-ttu-id="11a60-179">事件會依其相互關聯識別碼以及在時間範圍內發生的事件清單分組。</span><span class="sxs-lookup"><span data-stu-id="11a60-179">Events are grouped by their correlation ID and a list of the events that occurred in the Time span.</span></span>

    ![Operation Details](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. <span data-ttu-id="11a60-181">若要檢視特定事件的詳細資訊，請從事件清單中按一下事件，以開啟其 [詳細資料]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-181">To view detailed information about a particular event, from the list of events, click the event to open its **Details** blade.</span></span>

    ![事件詳細資料](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    <span data-ttu-id="11a60-183">事件層級資訊隨著資訊越多而越詳細。</span><span class="sxs-lookup"><span data-stu-id="11a60-183">The Event-level information is as detailed as the information gets.</span></span> <span data-ttu-id="11a60-184">如果您想查看有關每個事件的這麼多資訊，而且想要將這麼多詳細資料加入至 [事件]  刀鋒視窗，請參閱 [展開事件資訊](backup-azure-monitor-vms.md#view-additional-event-attributes)一節。</span><span class="sxs-lookup"><span data-stu-id="11a60-184">If you prefer seeing this much information about each event, and would like to add this much detail to the **Events** blade, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>

## <a name="customize-the-event-filter"></a><span data-ttu-id="11a60-185">自訂事件篩選器</span><span class="sxs-lookup"><span data-stu-id="11a60-185">Customize the event filter</span></span>
<span data-ttu-id="11a60-186">使用 [篩選]  進行調整，或選擇特定刀鋒視窗中顯示的資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-186">Use the **Filter** to adjust or choose the information that appears in a particular blade.</span></span> <span data-ttu-id="11a60-187">若要篩選事件資訊︰</span><span class="sxs-lookup"><span data-stu-id="11a60-187">To filter the event information:</span></span>

1. <span data-ttu-id="11a60-188">在[保存庫儀表板](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)中，瀏覽並按一下 [稽核記錄檔]，以開啟 [事件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-188">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span></span>

    ![稽核記錄檔](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="11a60-190">開啟的 [事件]  刀鋒視窗會顯示針對目前保存庫而篩選的作業事件。</span><span class="sxs-lookup"><span data-stu-id="11a60-190">The **Events** blade opens to the operational events filtered just for the current vault.</span></span>

    ![稽核記錄檔篩選器](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. <span data-ttu-id="11a60-192">在 [事件] 功能表上，按一下 [篩選] 以開啟該刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="11a60-192">On the **Events** menu, click **Filter** to open that blade.</span></span>

    ![開放篩選刀鋒視窗](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. <span data-ttu-id="11a60-194">在 [篩選] 刀鋒視窗上，調整 [層級]、[時間範圍] 和 [呼叫者] 篩選器。</span><span class="sxs-lookup"><span data-stu-id="11a60-194">On the **Filter** blade, adjust the **Level**, **Time span**, and **Caller** filters.</span></span> <span data-ttu-id="11a60-195">其他篩選器已設定為提供復原服務保存庫的目前資訊，所以無法使用。</span><span class="sxs-lookup"><span data-stu-id="11a60-195">The other filters are not available since they were set to provide the current information for the Recovery Services vault.</span></span>

    ![稽核記錄檔查詢詳細資料](./media/backup-azure-monitor-vms/filter-blade.png)

    <span data-ttu-id="11a60-197">您可以指定事件的 **層級** ︰嚴重、錯誤、警告或資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-197">You can specify the **Level** of event: Critical, Error, Warning, or Informational.</span></span> <span data-ttu-id="11a60-198">您可以選擇任何事件層級組合，但必須選取至少一個層級。</span><span class="sxs-lookup"><span data-stu-id="11a60-198">You can choose any combination of event Levels, but you must have at least one Level selected.</span></span> <span data-ttu-id="11a60-199">開啟或關閉層級。</span><span class="sxs-lookup"><span data-stu-id="11a60-199">Toggle the Level on or off.</span></span> <span data-ttu-id="11a60-200">[時間範圍]  篩選器可讓您指定時間長度來擷取事件。</span><span class="sxs-lookup"><span data-stu-id="11a60-200">The **Time span** filter allows you to specify the length of time for capturing events.</span></span> <span data-ttu-id="11a60-201">如果您使用自訂的時間範圍，您可以設定開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="11a60-201">If you use a custom Time span, you can set the start and end times.</span></span>
4. <span data-ttu-id="11a60-202">當您準備好使用篩選器來查詢作業記錄時，請按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="11a60-202">Once you are ready to query the operations logs using your filter, click **Update**.</span></span> <span data-ttu-id="11a60-203">結果會顯示在 [事件]  刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="11a60-203">The results display in the **Events** blade.</span></span>

    ![Operation Details](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a><span data-ttu-id="11a60-205">檢視其他事件屬性</span><span class="sxs-lookup"><span data-stu-id="11a60-205">View additional event attributes</span></span>
<span data-ttu-id="11a60-206">使用 [資料行] 按鈕，您可以讓其他事件屬性出現在 [事件] 刀鋒視窗上的清單中。</span><span class="sxs-lookup"><span data-stu-id="11a60-206">Using the **Columns** button, you can enable additional event attributes to appear in the list on the **Events** blade.</span></span> <span data-ttu-id="11a60-207">事件的預設清單會顯示 [作業]、[層級]、[狀態]、[資源] 和 [時間] 資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-207">The default list of events displays information for Operation, Level, Status, Resource, and Time.</span></span> <span data-ttu-id="11a60-208">若要啟用其他屬性︰</span><span class="sxs-lookup"><span data-stu-id="11a60-208">To enable additional attributes:</span></span>

1. <span data-ttu-id="11a60-209">在 [事件] 刀鋒視窗上，按一下 [資料行]。</span><span class="sxs-lookup"><span data-stu-id="11a60-209">On the **Events** blade, click **Columns**.</span></span>

    ![開啟資料行](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    <span data-ttu-id="11a60-211">[選擇資料行]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="11a60-211">The **Choose columns** blade opens.</span></span>

    ![資料行刀鋒視窗](./media/backup-azure-monitor-vms/columns-blade.png)
2. <span data-ttu-id="11a60-213">若要選取屬性，請按一下核取方塊。</span><span class="sxs-lookup"><span data-stu-id="11a60-213">To select the attribute, click the checkbox.</span></span> <span data-ttu-id="11a60-214">屬性核取方塊可進行開啟和關閉切換。</span><span class="sxs-lookup"><span data-stu-id="11a60-214">The attribute checkbox toggles on and off.</span></span>
3. <span data-ttu-id="11a60-215">按一下 [重設] 以在 [事件] 刀鋒視窗中重設屬性清單。</span><span class="sxs-lookup"><span data-stu-id="11a60-215">Click **Reset** to reset the list of attributes in the **Events** blade.</span></span> <span data-ttu-id="11a60-216">從清單中新增或移除屬性之後，使用 [重設]  來檢視新的事件屬性清單。</span><span class="sxs-lookup"><span data-stu-id="11a60-216">After adding or removing attributes from the list, use **Reset** to view the new list of Event attributes.</span></span>
4. <span data-ttu-id="11a60-217">按一下 [更新]  以更新事件屬性的資料。</span><span class="sxs-lookup"><span data-stu-id="11a60-217">Click **Update** to update the data in the Event attributes.</span></span> <span data-ttu-id="11a60-218">下表提供每個屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="11a60-218">The following table provides information about each attribute.</span></span>

| <span data-ttu-id="11a60-219">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="11a60-219">Column name</span></span> | <span data-ttu-id="11a60-220">說明</span><span class="sxs-lookup"><span data-stu-id="11a60-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11a60-221">作業</span><span class="sxs-lookup"><span data-stu-id="11a60-221">Operation</span></span> |<span data-ttu-id="11a60-222">作業的名稱</span><span class="sxs-lookup"><span data-stu-id="11a60-222">The name of the operation</span></span> |
| <span data-ttu-id="11a60-223">層級</span><span class="sxs-lookup"><span data-stu-id="11a60-223">Level</span></span> |<span data-ttu-id="11a60-224">作業的層級，其值可以是︰資訊、警告、錯誤或嚴重</span><span class="sxs-lookup"><span data-stu-id="11a60-224">The level of the operation, values can be: Informational, Warning, Error, or Critical</span></span> |
| <span data-ttu-id="11a60-225">狀態</span><span class="sxs-lookup"><span data-stu-id="11a60-225">Status</span></span> |<span data-ttu-id="11a60-226">作業的描述性狀態</span><span class="sxs-lookup"><span data-stu-id="11a60-226">Descriptive state of the operation</span></span> |
| <span data-ttu-id="11a60-227">資源</span><span class="sxs-lookup"><span data-stu-id="11a60-227">Resource</span></span> |<span data-ttu-id="11a60-228">可識別資源的 URI；也稱為資源識別碼</span><span class="sxs-lookup"><span data-stu-id="11a60-228">URL that identifies the resource; also known as the resource ID</span></span> |
| <span data-ttu-id="11a60-229">時間</span><span class="sxs-lookup"><span data-stu-id="11a60-229">Time</span></span> |<span data-ttu-id="11a60-230">事件發生時的時間 (從目前時間開始測量)</span><span class="sxs-lookup"><span data-stu-id="11a60-230">Time, measured from the current time, when the event occurred</span></span> |
| <span data-ttu-id="11a60-231">呼叫者</span><span class="sxs-lookup"><span data-stu-id="11a60-231">Caller</span></span> |<span data-ttu-id="11a60-232">何者或何物呼叫或觸發事件；可以是系統或使用者</span><span class="sxs-lookup"><span data-stu-id="11a60-232">Who or what called or triggered the event; can be the system, or a user</span></span> |
| <span data-ttu-id="11a60-233">Timestamp</span><span class="sxs-lookup"><span data-stu-id="11a60-233">Timestamp</span></span> |<span data-ttu-id="11a60-234">觸發事件時的時間</span><span class="sxs-lookup"><span data-stu-id="11a60-234">The time when the event was triggered</span></span> |
| <span data-ttu-id="11a60-235">資源群組</span><span class="sxs-lookup"><span data-stu-id="11a60-235">Resource Group</span></span> |<span data-ttu-id="11a60-236">相關聯的資源群組</span><span class="sxs-lookup"><span data-stu-id="11a60-236">The associated resource group</span></span> |
| <span data-ttu-id="11a60-237">資源類型</span><span class="sxs-lookup"><span data-stu-id="11a60-237">Resource Type</span></span> |<span data-ttu-id="11a60-238">Resource Manager 所使用的內部資源類型</span><span class="sxs-lookup"><span data-stu-id="11a60-238">The internal resource type used by Resource Manager</span></span> |
| <span data-ttu-id="11a60-239">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="11a60-239">Subscription ID</span></span> |<span data-ttu-id="11a60-240">相關聯的訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="11a60-240">The associated subscription ID</span></span> |
| <span data-ttu-id="11a60-241">類別</span><span class="sxs-lookup"><span data-stu-id="11a60-241">Category</span></span> |<span data-ttu-id="11a60-242">事件的類別</span><span class="sxs-lookup"><span data-stu-id="11a60-242">Category of the event</span></span> |
| <span data-ttu-id="11a60-243">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="11a60-243">Correlation ID</span></span> |<span data-ttu-id="11a60-244">相關事件的通用識別碼</span><span class="sxs-lookup"><span data-stu-id="11a60-244">Common ID for related events</span></span> |

## <a name="use-powershell-to-customize-alerts"></a><span data-ttu-id="11a60-245">使用 PowerShell 自訂警示</span><span class="sxs-lookup"><span data-stu-id="11a60-245">Use PowerShell to customize alerts</span></span>
<span data-ttu-id="11a60-246">您可以在入口網站取得作業的自訂警示通知。</span><span class="sxs-lookup"><span data-stu-id="11a60-246">You can get custom alert notifications for the jobs in the portal.</span></span> <span data-ttu-id="11a60-247">若要取得這些作業，請在作業記錄事件中定義以 PowerShell 為基礎的警示規則。</span><span class="sxs-lookup"><span data-stu-id="11a60-247">To get these jobs, define PowerShell-based alert rules on the operational logs events.</span></span> <span data-ttu-id="11a60-248">使用 PowerShell 1.3.0 版或更新版本 。</span><span class="sxs-lookup"><span data-stu-id="11a60-248">Use *PowerShell version 1.3.0 or later*.</span></span>

<span data-ttu-id="11a60-249">若要定義自訂通知以警示備份失敗，請使用如同下列指令碼的命令：</span><span class="sxs-lookup"><span data-stu-id="11a60-249">To define a custom notification to alert for backup failures, use a command like the following script:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="11a60-250">**ResourceId** ︰您可以從稽核記錄檔中取得 ResourceId。</span><span class="sxs-lookup"><span data-stu-id="11a60-250">**ResourceId** : You can get ResourceId from the Audit logs.</span></span> <span data-ttu-id="11a60-251">ResourceId 是作業記錄檔的 [資源] 資料行中提供的 URL。</span><span class="sxs-lookup"><span data-stu-id="11a60-251">The ResourceId is a URL provided in the Resource column of the Operation logs.</span></span>

<span data-ttu-id="11a60-252">**OperationName**：OperationName 的格式為 "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*"，其中 *EventName* 可以是：</span><span class="sxs-lookup"><span data-stu-id="11a60-252">**OperationName** : OperationName is in the format "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" where *EventName* can be:</span></span><br/>

* <span data-ttu-id="11a60-253">註冊</span><span class="sxs-lookup"><span data-stu-id="11a60-253">Register</span></span> <br/>
* <span data-ttu-id="11a60-254">Unregister </span><span class="sxs-lookup"><span data-stu-id="11a60-254">Unregister</span></span> <br/>
* <span data-ttu-id="11a60-255">ConfigureProtection </span><span class="sxs-lookup"><span data-stu-id="11a60-255">ConfigureProtection</span></span> <br/>
* <span data-ttu-id="11a60-256">Backup </span><span class="sxs-lookup"><span data-stu-id="11a60-256">Backup</span></span> <br/>
* <span data-ttu-id="11a60-257">Restore </span><span class="sxs-lookup"><span data-stu-id="11a60-257">Restore</span></span> <br/>
* <span data-ttu-id="11a60-258">StopProtection </span><span class="sxs-lookup"><span data-stu-id="11a60-258">StopProtection</span></span> <br/>
* <span data-ttu-id="11a60-259">DeleteBackupData </span><span class="sxs-lookup"><span data-stu-id="11a60-259">DeleteBackupData</span></span> <br/>
* <span data-ttu-id="11a60-260">CreateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="11a60-260">CreateProtectionPolicy</span></span> <br/>
* <span data-ttu-id="11a60-261">DeleteProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="11a60-261">DeleteProtectionPolicy</span></span> <br/>
* <span data-ttu-id="11a60-262">UpdateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="11a60-262">UpdateProtectionPolicy</span></span> <br/>

<span data-ttu-id="11a60-263">**Status** ：支援的值為 [已開始]、[成功] 或 [失敗]。</span><span class="sxs-lookup"><span data-stu-id="11a60-263">**Status** : Supported values are Started, Succeeded, or Failed.</span></span>

<span data-ttu-id="11a60-264">**ResourceGroup** ︰這是資源所屬的資源群組。</span><span class="sxs-lookup"><span data-stu-id="11a60-264">**ResourceGroup** : This is the Resource Group to which the resource belongs.</span></span> <span data-ttu-id="11a60-265">您可以將 [資源群組] 資料行加入至產生的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="11a60-265">You can add the Resource Group column to the generated logs.</span></span> <span data-ttu-id="11a60-266">資源群組是其中一個可用的事件資訊類型。</span><span class="sxs-lookup"><span data-stu-id="11a60-266">Resource Group is one of the available types of event information.</span></span>

<span data-ttu-id="11a60-267">**Name** ：警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="11a60-267">**Name** : Name of the Alert Rule.</span></span>

<span data-ttu-id="11a60-268">**CustomEmail** ：指定您要傳送警示通知的自訂電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="11a60-268">**CustomEmail** : Specify the custom email address to which you want to send an alert notification</span></span>

<span data-ttu-id="11a60-269">**SendToServiceOwners** ：此選項會將警示通知傳送給訂用帳戶的所有系統管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="11a60-269">**SendToServiceOwners** : This option sends alert notifications to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="11a60-270">它可以用於 **New-AzureRmAlertRuleEmail** Cmdlet 中</span><span class="sxs-lookup"><span data-stu-id="11a60-270">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="11a60-271">警示的限制</span><span class="sxs-lookup"><span data-stu-id="11a60-271">Limitations on Alerts</span></span>
<span data-ttu-id="11a60-272">以事件為基礎的警示受到下列限制：</span><span class="sxs-lookup"><span data-stu-id="11a60-272">Event-based alerts are subject to the following limitations:</span></span>

1. <span data-ttu-id="11a60-273">在復原服務保存庫中的所有虛擬機器上觸發警示。</span><span class="sxs-lookup"><span data-stu-id="11a60-273">Alerts are triggered on all virtual machines in the Recovery Services vault.</span></span> <span data-ttu-id="11a60-274">您無法針對復原服務保存庫中的部份虛擬機器自訂警示。</span><span class="sxs-lookup"><span data-stu-id="11a60-274">You cannot customize the alert for a subset of virtual machines in a Recovery Services vault.</span></span>
2. <span data-ttu-id="11a60-275">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="11a60-275">This feature is in Preview.</span></span> [<span data-ttu-id="11a60-276">深入了解</span><span class="sxs-lookup"><span data-stu-id="11a60-276">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="11a60-277">"alerts-noreply@mail.windowsazure.com" 會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="11a60-277">Alerts are sent from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="11a60-278">目前您無法修改電子郵件寄件者。</span><span class="sxs-lookup"><span data-stu-id="11a60-278">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11a60-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11a60-279">Next steps</span></span>
<span data-ttu-id="11a60-280">事件記錄檔會啟用備份作業的絕佳事後剖析和稽核支援。</span><span class="sxs-lookup"><span data-stu-id="11a60-280">Event logs enable great post-mortem and audit support for the backup operations.</span></span> <span data-ttu-id="11a60-281">系統會記錄下列作業：</span><span class="sxs-lookup"><span data-stu-id="11a60-281">The following operations are logged:</span></span>

* <span data-ttu-id="11a60-282">Register </span><span class="sxs-lookup"><span data-stu-id="11a60-282">Register</span></span>
* <span data-ttu-id="11a60-283">Unregister </span><span class="sxs-lookup"><span data-stu-id="11a60-283">Unregister</span></span>
* <span data-ttu-id="11a60-284">設定保護</span><span class="sxs-lookup"><span data-stu-id="11a60-284">Configure protection</span></span>
* <span data-ttu-id="11a60-285">備份 (排程和隨選備份兩者)</span><span class="sxs-lookup"><span data-stu-id="11a60-285">Backup (Both scheduled as well as on-demand backup)</span></span>
* <span data-ttu-id="11a60-286">Restore </span><span class="sxs-lookup"><span data-stu-id="11a60-286">Restore</span></span>
* <span data-ttu-id="11a60-287">停止保護</span><span class="sxs-lookup"><span data-stu-id="11a60-287">Stop protection</span></span>
* <span data-ttu-id="11a60-288">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="11a60-288">Delete backup data</span></span>
* <span data-ttu-id="11a60-289">Add policy</span><span class="sxs-lookup"><span data-stu-id="11a60-289">Add policy</span></span>
* <span data-ttu-id="11a60-290">刪除原則</span><span class="sxs-lookup"><span data-stu-id="11a60-290">Delete policy</span></span>
* <span data-ttu-id="11a60-291">更新原則</span><span class="sxs-lookup"><span data-stu-id="11a60-291">Update policy</span></span>
* <span data-ttu-id="11a60-292">取消工作</span><span class="sxs-lookup"><span data-stu-id="11a60-292">Cancel job</span></span>

<span data-ttu-id="11a60-293">如需各項 Azure 服務的事件、作業和稽核記錄檔的廣泛說明，請參閱[檢視事件和稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)一文。</span><span class="sxs-lookup"><span data-stu-id="11a60-293">For a broad explanation of events, operations, and audit logs across the Azure services, see the article, [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span></span>

<span data-ttu-id="11a60-294">如需從復原點重新建立虛擬機器的詳細資訊，請參閱 [還原 Azure VM](backup-azure-restore-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="11a60-294">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="11a60-295">如需保護虛擬機器的詳細資訊，請參閱 [搶先目睹︰將 VM 備份至復原服務保存庫](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="11a60-295">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="11a60-296">深入了解 [管理 Azure 虛擬機器備份](backup-azure-manage-vms.md)一文中 VM 備份的管理工作。</span><span class="sxs-lookup"><span data-stu-id="11a60-296">Learn about the management tasks for VM backups in the article, [Manage Azure virtual machine backups](backup-azure-manage-vms.md).</span></span>
