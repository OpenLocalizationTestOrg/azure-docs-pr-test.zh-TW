---
title: "Azure AD Connect 同步：排程器 | Microsoft Docs"
description: "本主題描述 Azure AD Connect 同步處理中的 hello 內建的排程器功能。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a><span data-ttu-id="6927e-103">Azure AD Connect 同步處理：排程器</span><span class="sxs-lookup"><span data-stu-id="6927e-103">Azure AD Connect sync: Scheduler</span></span>
<span data-ttu-id="6927e-104">本主題描述 Azure AD Connect 同步處理中的 hello 內建排程器 （也稱為</span><span class="sxs-lookup"><span data-stu-id="6927e-104">This topic describes hello built-in scheduler in Azure AD Connect sync (a.k.a.</span></span> <span data-ttu-id="6927e-105">同步處理引擎) 中內建的排程器。</span><span class="sxs-lookup"><span data-stu-id="6927e-105">sync engine).</span></span>

<span data-ttu-id="6927e-106">此功能是隨組建 1.1.105.0 (於 2016 年 2 月發行) 一起導入。</span><span class="sxs-lookup"><span data-stu-id="6927e-106">This feature was introduced with build 1.1.105.0 (released February 2016).</span></span>

## <a name="overview"></a><span data-ttu-id="6927e-107">概觀</span><span class="sxs-lookup"><span data-stu-id="6927e-107">Overview</span></span>
<span data-ttu-id="6927e-108">Azure AD Connect 同步處理會使用排程器來同步處理您內部部署目錄中發生的變更。</span><span class="sxs-lookup"><span data-stu-id="6927e-108">Azure AD Connect sync synchronize changes occurring in your on-premises directory using a scheduler.</span></span> <span data-ttu-id="6927e-109">有兩個排程器程序，一個用於密碼同步處理，另一個用於物件/屬性同步處理以及維護工作。</span><span class="sxs-lookup"><span data-stu-id="6927e-109">There are two scheduler processes, one for password sync and another for object/attribute sync and maintenance tasks.</span></span> <span data-ttu-id="6927e-110">本主題涵蓋 hello 後者。</span><span class="sxs-lookup"><span data-stu-id="6927e-110">This topic covers hello latter.</span></span>

<span data-ttu-id="6927e-111">Hello 排程器的物件和屬性的外部 toohello 同步處理引擎在較早的版本。</span><span class="sxs-lookup"><span data-stu-id="6927e-111">In earlier releases, hello scheduler for objects and attributes was external toohello sync engine.</span></span> <span data-ttu-id="6927e-112">它使用 Windows 工作排程器或另一個 Windows 服務 tootrigger hello 同步處理程序。</span><span class="sxs-lookup"><span data-stu-id="6927e-112">It used Windows task scheduler or a separate Windows service tootrigger hello synchronization process.</span></span> <span data-ttu-id="6927e-113">hello 排程器是與 hello 1.1 版本內建 toohello 同步處理引擎，允許某項自訂作業。</span><span class="sxs-lookup"><span data-stu-id="6927e-113">hello scheduler is with hello 1.1 releases built-in toohello sync engine and do allow some customization.</span></span> <span data-ttu-id="6927e-114">hello 新預設同步處理頻率為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6927e-114">hello new default synchronization frequency is 30 minutes.</span></span>

<span data-ttu-id="6927e-115">hello 排程器會負責這兩個工作項目：</span><span class="sxs-lookup"><span data-stu-id="6927e-115">hello scheduler is responsible for two tasks:</span></span>

* <span data-ttu-id="6927e-116">**同步處理循環**。</span><span class="sxs-lookup"><span data-stu-id="6927e-116">**Synchronization cycle**.</span></span> <span data-ttu-id="6927e-117">hello 程序 tooimport，同步處理及匯出變更。</span><span class="sxs-lookup"><span data-stu-id="6927e-117">hello process tooimport, sync, and export changes.</span></span>
* <span data-ttu-id="6927e-118">**維護工作**。</span><span class="sxs-lookup"><span data-stu-id="6927e-118">**Maintenance tasks**.</span></span> <span data-ttu-id="6927e-119">為密碼重設和「裝置註冊服務」(DRS) 更新金鑰和憑證。</span><span class="sxs-lookup"><span data-stu-id="6927e-119">Renew keys and certificates for Password reset and Device Registration Service (DRS).</span></span> <span data-ttu-id="6927e-120">清除 hello 作業記錄檔中的舊項目。</span><span class="sxs-lookup"><span data-stu-id="6927e-120">Purge old entries in hello operations log.</span></span>

<span data-ttu-id="6927e-121">hello 排程器本身一直執行，但可以設定的 tooonly 執行一個或無這些工作。</span><span class="sxs-lookup"><span data-stu-id="6927e-121">hello scheduler itself is always running, but it can be configured tooonly run one or none of these tasks.</span></span> <span data-ttu-id="6927e-122">例如，如果您需要 toohave 您自己的同步處理循環程序，您可以停用此 hello 排程器中的工作，但仍執行的 hello 維護工作。</span><span class="sxs-lookup"><span data-stu-id="6927e-122">For example, if you need toohave your own synchronization cycle process, you can disable this task in hello scheduler but still run hello maintenance task.</span></span>

## <a name="scheduler-configuration"></a><span data-ttu-id="6927e-123">排程器組態</span><span class="sxs-lookup"><span data-stu-id="6927e-123">Scheduler configuration</span></span>
<span data-ttu-id="6927e-124">toosee 移 tooPowerShell 目前的組態設定，並執行`Get-ADSyncScheduler`。</span><span class="sxs-lookup"><span data-stu-id="6927e-124">toosee your current configuration settings, go tooPowerShell and run `Get-ADSyncScheduler`.</span></span> <span data-ttu-id="6927e-125">它會向您顯示類似以下圖片︰</span><span class="sxs-lookup"><span data-stu-id="6927e-125">It shows you something like this picture:</span></span>

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

<span data-ttu-id="6927e-127">如果您看到**hello 同步命令或指令程式不提供**當您執行這個指令程式，然後 hello PowerShell 模組未載入。</span><span class="sxs-lookup"><span data-stu-id="6927e-127">If you see **hello sync command or cmdlet is not available** when you run this cmdlet, then hello PowerShell module is not loaded.</span></span> <span data-ttu-id="6927e-128">如果您在網域控制站上，或具有較高的 PowerShell 限制層級比 hello 的預設設定的伺服器上執行 Azure AD Connect，可能會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="6927e-128">This problem could happen if you run Azure AD Connect on a domain controller or on a server with higher PowerShell restriction levels than hello default settings.</span></span> <span data-ttu-id="6927e-129">如果您看到此錯誤，然後執行`Import-Module ADSync`toomake hello cmdlet 可用。</span><span class="sxs-lookup"><span data-stu-id="6927e-129">If you see this error, then run `Import-Module ADSync` toomake hello cmdlet available.</span></span>

* <span data-ttu-id="6927e-130">**AllowedSyncCycleInterval**。</span><span class="sxs-lookup"><span data-stu-id="6927e-130">**AllowedSyncCycleInterval**.</span></span> <span data-ttu-id="6927e-131">hello 最短時間間隔允許由 Azure AD 的同步處理循環之間。</span><span class="sxs-lookup"><span data-stu-id="6927e-131">hello shortest time interval between synchronization cycles allowed by Azure AD.</span></span> <span data-ttu-id="6927e-132">同步處理頻率一旦超過此設定，即不受支援。</span><span class="sxs-lookup"><span data-stu-id="6927e-132">You cannot synchronize more frequently than this setting and still be supported.</span></span>
* <span data-ttu-id="6927e-133">**CurrentlyEffectiveSyncCycleInterval**。</span><span class="sxs-lookup"><span data-stu-id="6927e-133">**CurrentlyEffectiveSyncCycleInterval**.</span></span> <span data-ttu-id="6927e-134">hello 排程目前作用中。</span><span class="sxs-lookup"><span data-stu-id="6927e-134">hello schedule currently in effect.</span></span> <span data-ttu-id="6927e-135">它有相同的值做 CustomizedSyncInterval hello (如果設定) 如果不是比 AllowedSyncInterval 更頻繁。</span><span class="sxs-lookup"><span data-stu-id="6927e-135">It has hello same value as CustomizedSyncInterval (if set) if it is not more frequent than AllowedSyncInterval.</span></span> <span data-ttu-id="6927e-136">如果您使用 1.1.281 之前的組件且變更 CustomizedSyncCycleInterval，將會在下一個同步處理循環後才生效。</span><span class="sxs-lookup"><span data-stu-id="6927e-136">If you use a build before 1.1.281 and you change CustomizedSyncCycleInterval, this change takes effect after next synchronization cycle.</span></span> <span data-ttu-id="6927e-137">從組建 1.1.281 hello 變更會立即生效。</span><span class="sxs-lookup"><span data-stu-id="6927e-137">From build 1.1.281 hello change takes effect immediately.</span></span>
* <span data-ttu-id="6927e-138">**CustomizedSyncCycleInterval**。</span><span class="sxs-lookup"><span data-stu-id="6927e-138">**CustomizedSyncCycleInterval**.</span></span> <span data-ttu-id="6927e-139">如果您想在任何其他頻率與 hello 預設 hello 排程器 toorun 30 分鐘內，您會設定此設定。</span><span class="sxs-lookup"><span data-stu-id="6927e-139">If you want hello scheduler toorun at any other frequency than hello default 30 minutes, then you configure this setting.</span></span> <span data-ttu-id="6927e-140">在上述的 hello 圖片，hello 排程器已設定 toorun 每小時改為。</span><span class="sxs-lookup"><span data-stu-id="6927e-140">In hello picture above, hello scheduler has been set toorun every hour instead.</span></span> <span data-ttu-id="6927e-141">如果您設定此設定 tooa 值低於 AllowedSyncInterval，則會使用第二個 hello。</span><span class="sxs-lookup"><span data-stu-id="6927e-141">If you set this setting tooa value lower than AllowedSyncInterval, then hello latter is used.</span></span>
* <span data-ttu-id="6927e-142">**NextSyncCyclePolicyType**。</span><span class="sxs-lookup"><span data-stu-id="6927e-142">**NextSyncCyclePolicyType**.</span></span> <span data-ttu-id="6927e-143">Delta (差異) 或 Initial (初始)。</span><span class="sxs-lookup"><span data-stu-id="6927e-143">Either Delta or Initial.</span></span> <span data-ttu-id="6927e-144">定義是否 hello 接下來執行應該只能處理差異變更，或如果 hello 下次執行應執行完整匯入和同步處理。hello 後者也會重新處理任何新的或變更的規則。</span><span class="sxs-lookup"><span data-stu-id="6927e-144">Defines if hello next run should only process delta changes, or if hello next run should do a full import and sync. hello latter would also reprocess any new or changed rules.</span></span>
* <span data-ttu-id="6927e-145">**NextSyncCycleStartTimeInUTC**。</span><span class="sxs-lookup"><span data-stu-id="6927e-145">**NextSyncCycleStartTimeInUTC**.</span></span> <span data-ttu-id="6927e-146">下一次 hello 排程器會開始 hello 下一個同步處理循環。</span><span class="sxs-lookup"><span data-stu-id="6927e-146">Next time hello scheduler starts hello next sync cycle.</span></span>
* <span data-ttu-id="6927e-147">**PurgeRunHistoryInterval**。</span><span class="sxs-lookup"><span data-stu-id="6927e-147">**PurgeRunHistoryInterval**.</span></span> <span data-ttu-id="6927e-148">hello 應該保留記錄檔的階段作業。</span><span class="sxs-lookup"><span data-stu-id="6927e-148">hello time operation logs should be kept.</span></span> <span data-ttu-id="6927e-149">可以在 hello 同步處理服務管理員中檢閱這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6927e-149">These logs can be reviewed in hello synchronization service manager.</span></span> <span data-ttu-id="6927e-150">hello 預設值是 7 天 tookeep 這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6927e-150">hello default is tookeep these logs for 7 days.</span></span>
* <span data-ttu-id="6927e-151">**SyncCycleEnabled**。</span><span class="sxs-lookup"><span data-stu-id="6927e-151">**SyncCycleEnabled**.</span></span> <span data-ttu-id="6927e-152">指出是否 hello 排程器執行 hello 匯入、 同步處理以及匯出處理程序做為其作業的一部分。</span><span class="sxs-lookup"><span data-stu-id="6927e-152">Indicates if hello scheduler is running hello import, sync, and export processes as part of its operation.</span></span>
* <span data-ttu-id="6927e-153">**MaintenanceEnabled**。</span><span class="sxs-lookup"><span data-stu-id="6927e-153">**MaintenanceEnabled**.</span></span> <span data-ttu-id="6927e-154">顯示 hello 維護程序是否已啟用。</span><span class="sxs-lookup"><span data-stu-id="6927e-154">Shows if hello maintenance process is enabled.</span></span> <span data-ttu-id="6927e-155">它會更新 hello 憑證/索引鍵，並清除 hello 作業記錄。</span><span class="sxs-lookup"><span data-stu-id="6927e-155">It updates hello certificates/keys and purges hello operations log.</span></span>
* <span data-ttu-id="6927e-156">**StagingModeEnabled**。</span><span class="sxs-lookup"><span data-stu-id="6927e-156">**StagingModeEnabled**.</span></span> <span data-ttu-id="6927e-157">顯示是否已啟用 [預備模式](active-directory-aadconnectsync-operations.md#staging-mode) 。</span><span class="sxs-lookup"><span data-stu-id="6927e-157">Shows if [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) is enabled.</span></span> <span data-ttu-id="6927e-158">如果已啟用此設定，然後它會隱藏 hello 匯出的執行，但仍執行 匯入和同步處理。</span><span class="sxs-lookup"><span data-stu-id="6927e-158">If this setting is enabled, then it suppresses hello exports from running but still run import and synchronization.</span></span>
* <span data-ttu-id="6927e-159">**SchedulerSuspended**。</span><span class="sxs-lookup"><span data-stu-id="6927e-159">**SchedulerSuspended**.</span></span> <span data-ttu-id="6927e-160">設定連線期間升級 tootemporarily 區塊 hello 排程器無法執行。</span><span class="sxs-lookup"><span data-stu-id="6927e-160">Set by Connect during an upgrade tootemporarily block hello scheduler from running.</span></span>

<span data-ttu-id="6927e-161">您可以使用 `Set-ADSyncScheduler`變更這些設定的其中一部分。</span><span class="sxs-lookup"><span data-stu-id="6927e-161">You can change some of these settings with `Set-ADSyncScheduler`.</span></span> <span data-ttu-id="6927e-162">您可以修改 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="6927e-162">hello following parameters can be modified:</span></span>

* <span data-ttu-id="6927e-163">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="6927e-163">CustomizedSyncCycleInterval</span></span>
* <span data-ttu-id="6927e-164">NextSyncCyclePolicyType</span><span class="sxs-lookup"><span data-stu-id="6927e-164">NextSyncCyclePolicyType</span></span>
* <span data-ttu-id="6927e-165">PurgeRunHistoryInterval</span><span class="sxs-lookup"><span data-stu-id="6927e-165">PurgeRunHistoryInterval</span></span>
* <span data-ttu-id="6927e-166">SyncCycleEnabled</span><span class="sxs-lookup"><span data-stu-id="6927e-166">SyncCycleEnabled</span></span>
* <span data-ttu-id="6927e-167">MaintenanceEnabled</span><span class="sxs-lookup"><span data-stu-id="6927e-167">MaintenanceEnabled</span></span>

<span data-ttu-id="6927e-168">在先前的 Azure AD Connect 組建中，**isStagingModeEnabled** 已在 Set-ADSyncScheduler 中公開。</span><span class="sxs-lookup"><span data-stu-id="6927e-168">In earlier builds of Azure AD Connect, **isStagingModeEnabled** was exposed in Set-ADSyncScheduler.</span></span> <span data-ttu-id="6927e-169">它是**不支援**tooset 這個屬性。</span><span class="sxs-lookup"><span data-stu-id="6927e-169">It is **unsupported** tooset this property.</span></span> <span data-ttu-id="6927e-170">hello 屬性**SchedulerSuspended**應該只能由連接進行修改。</span><span class="sxs-lookup"><span data-stu-id="6927e-170">hello property **SchedulerSuspended** should only be modified by Connect.</span></span> <span data-ttu-id="6927e-171">它是**不支援**tooset 這 PowerShell 直接使用。</span><span class="sxs-lookup"><span data-stu-id="6927e-171">It is **unsupported** tooset this with PowerShell directly.</span></span>

<span data-ttu-id="6927e-172">hello 排程器設定儲存在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6927e-172">hello scheduler configuration is stored in Azure AD.</span></span> <span data-ttu-id="6927e-173">如果您有在臨時伺服器，則 hello 主要伺服器上的任何變更也會影響 hello 開發用伺服器 （除了 IsStagingModeEnabled)。</span><span class="sxs-lookup"><span data-stu-id="6927e-173">If you have a staging server, any change on hello primary server also affects hello staging server (except IsStagingModeEnabled).</span></span>

### <a name="customizedsynccycleinterval"></a><span data-ttu-id="6927e-174">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="6927e-174">CustomizedSyncCycleInterval</span></span>
<span data-ttu-id="6927e-175">語法： `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span><span class="sxs-lookup"><span data-stu-id="6927e-175">Syntax: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span></span>  
<span data-ttu-id="6927e-176">d - 天、HH - 小時、mm - 分鐘、ss - 秒</span><span class="sxs-lookup"><span data-stu-id="6927e-176">d - days, HH - hours, mm - minutes, ss - seconds</span></span>

<span data-ttu-id="6927e-177">範例： `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span><span class="sxs-lookup"><span data-stu-id="6927e-177">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span></span>  
<span data-ttu-id="6927e-178">變更 hello 排程器 toorun 每 3 個小時。</span><span class="sxs-lookup"><span data-stu-id="6927e-178">Changes hello scheduler toorun every 3 hours.</span></span>

<span data-ttu-id="6927e-179">範例： `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span><span class="sxs-lookup"><span data-stu-id="6927e-179">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span></span>  
<span data-ttu-id="6927e-180">變更每日變更 hello 排程器 toorun。</span><span class="sxs-lookup"><span data-stu-id="6927e-180">Changes change hello scheduler toorun daily.</span></span>

### <a name="disable-hello-scheduler"></a><span data-ttu-id="6927e-181">停用 hello 排程器</span><span class="sxs-lookup"><span data-stu-id="6927e-181">Disable hello scheduler</span></span>  
<span data-ttu-id="6927e-182">如果您需要 toomake 組態變更，您會想 toodisable hello 排程器。</span><span class="sxs-lookup"><span data-stu-id="6927e-182">If you need toomake configuration changes, then you want toodisable hello scheduler.</span></span> <span data-ttu-id="6927e-183">例如，當您[設定篩選](active-directory-aadconnectsync-configure-filtering.md)或[變更 toosynchronization 規則](active-directory-aadconnectsync-change-the-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="6927e-183">For example, when you [configure filtering](active-directory-aadconnectsync-configure-filtering.md) or [make changes toosynchronization rules](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="6927e-184">toodisable hello 排程器執行`Set-ADSyncScheduler -SyncCycleEnabled $false`。</span><span class="sxs-lookup"><span data-stu-id="6927e-184">toodisable hello scheduler, run `Set-ADSyncScheduler -SyncCycleEnabled $false`.</span></span>

![停用 hello 排程器](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

<span data-ttu-id="6927e-186">當您完成變更之後，不要忘記再次 tooenable hello 排程器`Set-ADSyncScheduler -SyncCycleEnabled $true`。</span><span class="sxs-lookup"><span data-stu-id="6927e-186">When you've made your changes, do not forget tooenable hello scheduler again with `Set-ADSyncScheduler -SyncCycleEnabled $true`.</span></span>

## <a name="start-hello-scheduler"></a><span data-ttu-id="6927e-187">啟動 hello 排程器</span><span class="sxs-lookup"><span data-stu-id="6927e-187">Start hello scheduler</span></span>
<span data-ttu-id="6927e-188">預設每隔 30 分鐘執行一次為 hello 排程器。</span><span class="sxs-lookup"><span data-stu-id="6927e-188">hello scheduler is by default run every 30 minutes.</span></span> <span data-ttu-id="6927e-189">在某些情況下，您可能想的 toorun hello 之間的同步處理循環排程的循環，或者您需要 toorun 不同的型別。</span><span class="sxs-lookup"><span data-stu-id="6927e-189">In some cases, you might want toorun a sync cycle in between hello scheduled cycles or you need toorun a different type.</span></span>

<span data-ttu-id="6927e-190">**差異同步處理循環**</span><span class="sxs-lookup"><span data-stu-id="6927e-190">**Delta sync cycle**</span></span>  
<span data-ttu-id="6927e-191">差異同步處理循環包含下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6927e-191">A delta sync cycle includes hello following steps:</span></span>

* <span data-ttu-id="6927e-192">在所有的連接器上執行差異匯入</span><span class="sxs-lookup"><span data-stu-id="6927e-192">Delta import on all Connectors</span></span>
* <span data-ttu-id="6927e-193">在所有的連接器上執行差異同步處理</span><span class="sxs-lookup"><span data-stu-id="6927e-193">Delta sync on all Connectors</span></span>
* <span data-ttu-id="6927e-194">在所有的連接器上執行匯出</span><span class="sxs-lookup"><span data-stu-id="6927e-194">Export on all Connectors</span></span>

<span data-ttu-id="6927e-195">這可能是您有緊急變更必須立即同步處理就是為什麼您需要 toomanually 執行循環。</span><span class="sxs-lookup"><span data-stu-id="6927e-195">It could be that you have an urgent change that must be synchronized immediately, which is why you need toomanually run a cycle.</span></span> <span data-ttu-id="6927e-196">如果您需要 toomanually 執行循環，然後從 PowerShell 執行`Start-ADSyncSyncCycle -PolicyType Delta`。</span><span class="sxs-lookup"><span data-stu-id="6927e-196">If you need toomanually run a cycle, then from PowerShell run `Start-ADSyncSyncCycle -PolicyType Delta`.</span></span>

<span data-ttu-id="6927e-197">**完整同步處理循環**</span><span class="sxs-lookup"><span data-stu-id="6927e-197">**Full sync cycle**</span></span>  
<span data-ttu-id="6927e-198">如果您做了其中一個 hello 下列組態變更，您 （也稱為需要完整同步處理週期 toorun</span><span class="sxs-lookup"><span data-stu-id="6927e-198">If you have made one of hello following configuration changes, you need toorun a full sync cycle (a.k.a.</span></span> <span data-ttu-id="6927e-199">Initial (初始))：</span><span class="sxs-lookup"><span data-stu-id="6927e-199">Initial):</span></span>

* <span data-ttu-id="6927e-200">加入多個物件或屬性 toobe 匯入從來源目錄</span><span class="sxs-lookup"><span data-stu-id="6927e-200">Added more objects or attributes toobe imported from a source directory</span></span>
* <span data-ttu-id="6927e-201">變更 toohello 同步處理規則</span><span class="sxs-lookup"><span data-stu-id="6927e-201">Made changes toohello Synchronization rules</span></span>
* <span data-ttu-id="6927e-202">變更 [篩選](active-directory-aadconnectsync-configure-filtering.md) 以納入不同數目的物件</span><span class="sxs-lookup"><span data-stu-id="6927e-202">Changed [filtering](active-directory-aadconnectsync-configure-filtering.md) so a different number of objects should be included</span></span>

<span data-ttu-id="6927e-203">如果您做了其中一個這些變更，您需要的 toorun 完整同步處理循環，所以 hello 同步處理引擎沒有 hello 機會 tooreconsolidate hello 連接器空間。</span><span class="sxs-lookup"><span data-stu-id="6927e-203">If you have made one of these changes, then you need toorun a full sync cycle so hello sync engine has hello opportunity tooreconsolidate hello connector spaces.</span></span> <span data-ttu-id="6927e-204">完整同步處理循環包含下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6927e-204">A full sync cycle includes hello following steps:</span></span>

* <span data-ttu-id="6927e-205">在所有的連接器上執行完整匯入</span><span class="sxs-lookup"><span data-stu-id="6927e-205">Full Import on all Connectors</span></span>
* <span data-ttu-id="6927e-206">在所有的連接器上執行完整同步處理</span><span class="sxs-lookup"><span data-stu-id="6927e-206">Full Sync on all Connectors</span></span>
* <span data-ttu-id="6927e-207">在所有的連接器上執行匯出</span><span class="sxs-lookup"><span data-stu-id="6927e-207">Export on all Connectors</span></span>

<span data-ttu-id="6927e-208">執行完整同步處理週期 tooinitiate`Start-ADSyncSyncCycle -PolicyType Initial`從 PowerShell 提示中。</span><span class="sxs-lookup"><span data-stu-id="6927e-208">tooinitiate a full sync cycle, run `Start-ADSyncSyncCycle -PolicyType Initial` from a PowerShell prompt.</span></span> <span data-ttu-id="6927e-209">此命令會啟動完整同步處理循環。</span><span class="sxs-lookup"><span data-stu-id="6927e-209">This command starts a full sync cycle.</span></span>

## <a name="stop-hello-scheduler"></a><span data-ttu-id="6927e-210">停止 hello 排程器</span><span class="sxs-lookup"><span data-stu-id="6927e-210">Stop hello scheduler</span></span>
<span data-ttu-id="6927e-211">如果 hello 排程器目前正在執行同步處理循環，您可能需要 toostop 它。</span><span class="sxs-lookup"><span data-stu-id="6927e-211">If hello scheduler is currently running a synchronization cycle, you might need toostop it.</span></span> <span data-ttu-id="6927e-212">例如，如果您啟動 hello 安裝精靈，您會收到這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="6927e-212">For example if you start hello installation wizard and you get this error:</span></span>

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

<span data-ttu-id="6927e-214">當同步處理循環正在執行時，您會無法進行組態變更。</span><span class="sxs-lookup"><span data-stu-id="6927e-214">When a sync cycle is running, you cannot make configuration changes.</span></span> <span data-ttu-id="6927e-215">您無法等到 hello 排程器已完成 hello 程序，但也可以停止它，因此您可以立即進行變更。</span><span class="sxs-lookup"><span data-stu-id="6927e-215">You could wait until hello scheduler has finished hello process, but you can also stop it so you can make your changes immediately.</span></span> <span data-ttu-id="6927e-216">停止目前的循環 hello 不有害，暫止的變更會和處理接下來執行。</span><span class="sxs-lookup"><span data-stu-id="6927e-216">Stopping hello current cycle is not harmful and pending changes are processed with next run.</span></span>

1. <span data-ttu-id="6927e-217">藉由告訴 hello 排程器 toostop 其目前的開始與 hello PowerShell cmdlet 的循環`Stop-ADSyncSyncCycle`。</span><span class="sxs-lookup"><span data-stu-id="6927e-217">Start by telling hello scheduler toostop its current cycle with hello PowerShell cmdlet `Stop-ADSyncSyncCycle`.</span></span>
2. <span data-ttu-id="6927e-218">如果您使用的組建之前 1.1.281，則停止 hello 排程器不會停止目前的 hello 連接器從其目前的工作。</span><span class="sxs-lookup"><span data-stu-id="6927e-218">If you use a build before 1.1.281, then stopping hello scheduler does not stop hello current Connector from its current task.</span></span> <span data-ttu-id="6927e-219">tooforce hello 連接器 toostop，採取下列動作的 hello: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span><span class="sxs-lookup"><span data-stu-id="6927e-219">tooforce hello Connector toostop, take hello following actions: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span></span>
   * <span data-ttu-id="6927e-220">啟動**同步處理服務**從 hello [開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="6927e-220">Start **Synchronization Service** from hello start menu.</span></span> <span data-ttu-id="6927e-221">跳過**連接器**，反白顯示 hello 連接器與 hello 狀態**執行**，然後選取**停止**從 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="6927e-221">Go too**Connectors**, highlight hello Connector with hello state **Running**, and select **Stop** from hello Actions.</span></span>

<span data-ttu-id="6927e-222">hello 排程器仍在作用中，並在下次有機會再次啟動。</span><span class="sxs-lookup"><span data-stu-id="6927e-222">hello scheduler is still active and starts again on next opportunity.</span></span>

## <a name="custom-scheduler"></a><span data-ttu-id="6927e-223">自訂排程器</span><span class="sxs-lookup"><span data-stu-id="6927e-223">Custom scheduler</span></span>
<span data-ttu-id="6927e-224">hello 本節中所述的 cmdlet 中才有建置[1.1.130.0](active-directory-aadconnect-version-history.md#111300)和更新版本。</span><span class="sxs-lookup"><span data-stu-id="6927e-224">hello cmdlets documented in this section are only available in build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) and later.</span></span>

<span data-ttu-id="6927e-225">如果 hello 內建的排程器無法滿足您的需求，您可以排程 hello 連接器使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6927e-225">If hello built-in scheduler does not satisfy your requirements, then you can schedule hello Connectors using PowerShell.</span></span>

### <a name="invoke-adsyncrunprofile"></a><span data-ttu-id="6927e-226">Invoke-ADSyncRunProfile</span><span class="sxs-lookup"><span data-stu-id="6927e-226">Invoke-ADSyncRunProfile</span></span>
<span data-ttu-id="6927e-227">您可使用下列方式，啟動連接器的設定檔：</span><span class="sxs-lookup"><span data-stu-id="6927e-227">You can start a profile for a Connector in this way:</span></span>

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

<span data-ttu-id="6927e-228">如 hello 名稱 toouse[連接子名稱](active-directory-aadconnectsync-service-manager-ui-connectors.md)和[執行設定檔名稱](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles)位於 hello[同步處理服務管理員 UI](active-directory-aadconnectsync-service-manager-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="6927e-228">hello names toouse for [Connector names](active-directory-aadconnectsync-service-manager-ui-connectors.md) and [Run Profile Names](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) can be found in hello [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

![叫用執行設定檔](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

<span data-ttu-id="6927e-230">hello `Invoke-ADSyncRunProfile` cmdlet 是同步，亦即它不會傳回控制項 hello 連接器完成之前完成 hello 作業成功或錯誤。</span><span class="sxs-lookup"><span data-stu-id="6927e-230">hello `Invoke-ADSyncRunProfile` cmdlet is synchronous, that is, it does not return control until hello Connector has completed hello operation, either successfully or with an error.</span></span>

<span data-ttu-id="6927e-231">當您排程的連接器時，hello 建議 tooschedule hello 順序中：</span><span class="sxs-lookup"><span data-stu-id="6927e-231">When you schedule your Connectors, hello recommendation is tooschedule them in hello following order:</span></span>

1. <span data-ttu-id="6927e-232">(完整/差異) 從內部部署目錄匯入，例如 Active Directory</span><span class="sxs-lookup"><span data-stu-id="6927e-232">(Full/Delta) Import from on-premises directories, such as Active Directory</span></span>
2. <span data-ttu-id="6927e-233">(完整/差異) 從 Azure AD 匯入</span><span class="sxs-lookup"><span data-stu-id="6927e-233">(Full/Delta) Import from Azure AD</span></span>
3. <span data-ttu-id="6927e-234">(完整/差異) 從內部部署目錄同步處理，例如 Active Directory</span><span class="sxs-lookup"><span data-stu-id="6927e-234">(Full/Delta) Synchronization from on-premises directories, such as Active Directory</span></span>
4. <span data-ttu-id="6927e-235">(完整/差異) 從 Azure AD 同步處理</span><span class="sxs-lookup"><span data-stu-id="6927e-235">(Full/Delta) Synchronization from Azure AD</span></span>
5. <span data-ttu-id="6927e-236">匯出 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="6927e-236">Export tooAzure AD</span></span>
6. <span data-ttu-id="6927e-237">匯出 tooon 內部部署目錄，例如 Active Directory</span><span class="sxs-lookup"><span data-stu-id="6927e-237">Export tooon-premises directories, such as Active Directory</span></span>

<span data-ttu-id="6927e-238">這個順序是 hello 內建的排程器執行 hello 連接器的方式。</span><span class="sxs-lookup"><span data-stu-id="6927e-238">This order is how hello built-in scheduler runs hello Connectors.</span></span>

### <a name="get-adsyncconnectorrunstatus"></a><span data-ttu-id="6927e-239">Get-ADSyncConnectorRunStatus</span><span class="sxs-lookup"><span data-stu-id="6927e-239">Get-ADSyncConnectorRunStatus</span></span>
<span data-ttu-id="6927e-240">您也可以監視 hello 同步處理引擎 toosee，如果它是忙碌或閒置。</span><span class="sxs-lookup"><span data-stu-id="6927e-240">You can also monitor hello sync engine toosee if it is busy or idle.</span></span> <span data-ttu-id="6927e-241">如果 hello 同步處理引擎會處於閒置狀態，但卻未執行連接器，此 cmdlet 會傳回空的結果。</span><span class="sxs-lookup"><span data-stu-id="6927e-241">This cmdlet returns an empty result if hello sync engine is idle and is not running a Connector.</span></span> <span data-ttu-id="6927e-242">如果執行連接器，它會傳回 hello hello 連接器名稱。</span><span class="sxs-lookup"><span data-stu-id="6927e-242">If a Connector is running, it returns hello name of hello Connector.</span></span>

```
Get-ADSyncConnectorRunStatus
```

![連接器執行狀態](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
<span data-ttu-id="6927e-244">在上面的 hello 圖片，hello 第一行是從閒置 hello 同步處理引擎的狀態。</span><span class="sxs-lookup"><span data-stu-id="6927e-244">In hello picture above, hello first line is from a state where hello sync engine is idle.</span></span> <span data-ttu-id="6927e-245">hello 從 hello Azure AD Connector 正在執行時的第二行。</span><span class="sxs-lookup"><span data-stu-id="6927e-245">hello second line from when hello Azure AD Connector is running.</span></span>

## <a name="scheduler-and-installation-wizard"></a><span data-ttu-id="6927e-246">排程器和安裝精靈</span><span class="sxs-lookup"><span data-stu-id="6927e-246">Scheduler and installation wizard</span></span>
<span data-ttu-id="6927e-247">如果您啟動 hello 安裝精靈，然後 hello 排程器已暫時暫止。</span><span class="sxs-lookup"><span data-stu-id="6927e-247">If you start hello installation wizard, then hello scheduler is temporarily suspended.</span></span> <span data-ttu-id="6927e-248">這是因為它會假設您進行組態變更，但不可套用這些設定，如果 hello 同步處理引擎正在執行。</span><span class="sxs-lookup"><span data-stu-id="6927e-248">This behavior is because it is assumed you make configuration changes and these settings cannot be applied if hello sync engine is actively running.</span></span> <span data-ttu-id="6927e-249">基於這個理由，不會讓 hello 安裝精靈開啟因為它會停止 hello 同步處理引擎從執行任何同步處理動作。</span><span class="sxs-lookup"><span data-stu-id="6927e-249">For this reason, do not leave hello installation wizard open since it stops hello sync engine from performing any synchronization actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6927e-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6927e-250">Next steps</span></span>
<span data-ttu-id="6927e-251">深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。</span><span class="sxs-lookup"><span data-stu-id="6927e-251">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="6927e-252">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="6927e-252">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
