---
title: "aaaStorSimple 管理員服務儀表板 |Microsoft 文件"
description: "描述 hello StorSimple Manager 服務儀表板，並說明如何 toouse 它讓 StorSimple 方案 toomonitor hello 健全狀況。"
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a><span data-ttu-id="3cd9c-103">使用 hello StorSimple Manager 服務儀表板</span><span class="sxs-lookup"><span data-stu-id="3cd9c-103">Use hello StorSimple Manager service dashboard</span></span>
## <a name="overview"></a><span data-ttu-id="3cd9c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3cd9c-104">Overview</span></span>
<span data-ttu-id="3cd9c-105">hello StorSimple Manager 服務儀表板頁面會提供所有 hello 的裝置連線的 toohello StorSimple Manager 服務，反白顯示那些需要系統管理員注意的摘要檢視。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-105">hello StorSimple Manager service dashboard page provides a summary view of all hello devices that are connected toohello StorSimple Manager service, highlighting those that need a system administrator's attention.</span></span> <span data-ttu-id="3cd9c-106">本教學課程介紹 hello 儀表板頁面、 說明 hello 儀表板的內容，以及函式，並說明您可以從這個頁面上執行的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-106">This tutorial introduces hello dashboard page, explains hello dashboard content and function, and describes hello tasks that you can perform from this page.</span></span>

![服務儀表板](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

<span data-ttu-id="3cd9c-108">hello StorSimple Manager 服務儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="3cd9c-108">hello StorSimple Manager service dashboard displays hello following information:</span></span>

* <span data-ttu-id="3cd9c-109">在 hello**圖表**區域中，您可以看到您的裝置 hello 相關度量圖表。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-109">In hello **chart** area, you can see hello relevant metrics chart for your devices.</span></span> <span data-ttu-id="3cd9c-110">您可以檢視 hello 主要儲存體 （本機釘選或階層） 跨所有 hello 裝置，以及以 hello 給裝置使用的一段時間的雲端儲存體使用。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-110">You can view hello primary storage (locally pinned and tiered) used across all hello devices, as well as hello cloud storage consumed by devices over a period of time.</span></span> <span data-ttu-id="3cd9c-111">在 hello 右上角的 hello 圖表 toospecify 1 週、 1 個月、 3 個月或 1 年的時間刻度使用 hello 控制項。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-111">Use hello controls in hello top-right corner of hello chart toospecify a 1-week, 1-month, 3-month, or 1-year time scale.</span></span>
* <span data-ttu-id="3cd9c-112">hello**使用量概觀**顯示 hello 佈建並供所有裝置上的所有裝置相對 toohello 可用總儲存體的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-112">hello **usage overview** shows hello primary storage that is provisioned and consumed by all devices relative toohello total storage available across all devices.</span></span> <span data-ttu-id="3cd9c-113">**佈建**是指已備妥並配置供使用，而儲存體的 toohello 數量**用於**檢視 hello 啟動器連接的 toohello 裝置是指 toousage 的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-113">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, while **Used** refers toousage of volumes as viewed by hello initiators that are connected toohello devices.</span></span>
* <span data-ttu-id="3cd9c-114">hello**警示**區域提供所有 hello 作用中警示的快照集上，依警示嚴重性分組的所有 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-114">hello **alerts** area provides a snapshot of all hello active alerts across all hello devices, grouped by alert severity.</span></span> <span data-ttu-id="3cd9c-115">按一下 hello 嚴重性層級開啟 hello**警示**頁面上，已設定領域的 tooshow 這些警示。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-115">Clicking hello severity level opens hello **Alerts** page, scoped tooshow those alerts.</span></span> <span data-ttu-id="3cd9c-116">在 [hello**警示**] 頁面上，您可以按一下個別警示 tooview 詳細有關該警示，包括任何建議的動作。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-116">On hello **Alerts** page, you can click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="3cd9c-117">如果 hello 問題已經解決，您也可以清除 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-117">You can also clear hello alert if hello issue has been resolved.</span></span>
* <span data-ttu-id="3cd9c-118">hello**作業**區域會提供連接的所有裝置上最近工作的快照 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-118">hello **jobs** area provides a snapshot of recent jobs across all devices that are connected tooyour service.</span></span> <span data-ttu-id="3cd9c-119">您可以在作業正在進行中，這些失敗 hello 過去 24 小時，使用 toolook 連結或的排程在 hello toorun 未來 24 小時內。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-119">There are links that you can use toolook at jobs that are currently in progress, those that failed in hello last 24 hours, or those that are scheduled toorun in hello next 24 hours.</span></span>
* <span data-ttu-id="3cd9c-120">hello**快速概覽**區域會提供實用資訊，例如服務狀態、 裝置連線的 toohello 服務、 hello 服務位置與 hello 服務相關聯的 hello 訂用帳戶的詳細資料的數目。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-120">hello **quick glance** area provides useful information such as service status, number of devices connected toohello service, location of hello service, and details of hello subscription that is associated with hello service.</span></span> <span data-ttu-id="3cd9c-121">另外還有連結 toohello 作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-121">There is also a link toohello operations log.</span></span> <span data-ttu-id="3cd9c-122">按一下 hello 連結 toosee 所有已完成的 StorSimple Manager 服務作業的清單。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-122">Click hello link toosee a list of all completed StorSimple Manager service operations.</span></span>

<span data-ttu-id="3cd9c-123">您可以使用 hello StorSimple Manager 服務儀表板頁面 tooinitiate hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="3cd9c-123">You can use hello StorSimple Manager service dashboard page tooinitiate hello following tasks:</span></span>

* <span data-ttu-id="3cd9c-124">檢視或重新產生 hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-124">View or regenerate hello service registration key.</span></span>
* <span data-ttu-id="3cd9c-125">變更 hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-125">Change hello service data encryption key.</span></span>
* <span data-ttu-id="3cd9c-126">檢視 hello 作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-126">View hello operation logs.</span></span>

## <a name="view-or-regenerate-hello-service-registration-key"></a><span data-ttu-id="3cd9c-127">檢視或重新產生 hello 服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="3cd9c-127">View or regenerate hello service registration key</span></span>
<span data-ttu-id="3cd9c-128">hello 服務註冊金鑰是使用的 tooregister hello StorSimple Manager 服務，Microsoft Azure StorSimple 裝置，因此 hello 裝置會出現在 hello Azure 傳統入口網站，供進一步的管理動作。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-128">hello service registration key is used tooregister a Microsoft Azure StorSimple device with hello StorSimple Manager service, so that hello device appears in hello Azure classic portal for further management actions.</span></span> <span data-ttu-id="3cd9c-129">hello 金鑰 hello 第一個裝置上建立並與您的裝置 hello 其他部分共用。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-129">hello key is created on hello first device and shared with hello rest of your devices.</span></span>

<span data-ttu-id="3cd9c-130">按一下**登錄機碼**（位於 hello hello 頁面底部） 開啟 hello**服務註冊金鑰**對話方塊中，您可以在其中一個複本 hello 目前服務註冊金鑰 toohello 剪貼簿或重新產生 hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-130">Clicking **Registration Key** (at hello bottom of hello page) opens hello **Service Registration Key** dialog box, where you can either copy hello current service registration key toohello clipboard or regenerate hello service registration key.</span></span>

<span data-ttu-id="3cd9c-131">重新產生 hello 金鑰不會影響先前已註冊的裝置： 它會影響只有 hello 後重新產生金鑰 hello 與 hello 服務註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-131">Regenerating hello key does not affect previously registered devices: it affects only hello devices that are registered with hello service after hello key is regenerated.</span></span>

<span data-ttu-id="3cd9c-132">如需有關檢視和太產生 hello 服務註冊金鑰，請前往[Get hello 服務註冊金鑰](storsimple-manage-service.md#get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-132">For more information about viewing and generating hello service registration key, go too[Get hello service registration key](storsimple-manage-service.md#get-the-service-registration-key).</span></span>

## <a name="change-hello-service-data-encryption-key"></a><span data-ttu-id="3cd9c-133">變更 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="3cd9c-133">Change hello service data encryption key</span></span>
<span data-ttu-id="3cd9c-134">服務資料加密金鑰是使用的 tooencrypt 客戶機密資料，例如從 StorSimple Manager 服務 toohello StorSimple 裝置傳送的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-134">Service data encryption keys are used tooencrypt confidential customer data, such as storage account credentials, that are sent from your StorSimple Manager service toohello StorSimple device.</span></span> <span data-ttu-id="3cd9c-135">您將需要 toochange 這些機碼定期如果您的 IT 組織具有 hello 存放裝置金鑰輪動原則。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-135">You will need toochange these keys periodically if your IT organization has a key rotation policy on hello storage devices.</span></span> <span data-ttu-id="3cd9c-136">hello 金鑰變更程序可能會稍有不同，視沒有單一裝置或多個 hello StorSimple Manager 服務所管理的裝置。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-136">hello key change process can be slightly different depending on whether there is a single device or multiple devices managed by hello StorSimple Manager service.</span></span>

<span data-ttu-id="3cd9c-137">變更 hello 服務資料加密金鑰是 3 個步驟程序：</span><span class="sxs-lookup"><span data-stu-id="3cd9c-137">Changing hello service data encryption key is a 3-step process:</span></span>

1. <span data-ttu-id="3cd9c-138">使用 hello Azure 傳統入口網站，授權裝置 toochange hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-138">Using hello Azure classic portal, authorize a device toochange hello service data encryption key.</span></span>
2. <span data-ttu-id="3cd9c-139">使用 Windows PowerShell for StorSimple，起始 hello 服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-139">Using Windows PowerShell for StorSimple, initiate hello service data encryption key change.</span></span>
3. <span data-ttu-id="3cd9c-140">如果您有多個 StorSimple 裝置，更新其他裝置上 hello hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-140">If you have more than one StorSimple device, update hello service data encryption key on hello other devices.</span></span>

<span data-ttu-id="3cd9c-141">hello 下列步驟描述 hello hello 服務資料加密金鑰變換程序。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-141">hello following steps describe hello rollover process for hello service data encryption key.</span></span>

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a><span data-ttu-id="3cd9c-142">檢視 hello 作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="3cd9c-142">View hello operations logs</span></span>
<span data-ttu-id="3cd9c-143">您可以按一下 hello hello 中可用的作業記錄連結，以檢視 hello 作業記錄**快速概覽**hello 儀表板的窗格。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-143">You can view hello operation logs by clicking hello operation logs link available in hello **quick glance** pane of hello dashboard.</span></span> <span data-ttu-id="3cd9c-144">這會帶您 toohello 管理服務 頁面上，您可以在此篩選，並查看 hello 記錄特定 tooyour StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-144">This will take you toohello management services page, where you can filter and see hello logs specific tooyour StorSimple Manager service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cd9c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3cd9c-145">Next steps</span></span>
* <span data-ttu-id="3cd9c-146">了解如何太[StorSimple 裝置排解](storsimple-troubleshoot-operational-device.md)。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-146">Learn how too[troubleshoot a StorSimple device](storsimple-troubleshoot-operational-device.md).</span></span>
* <span data-ttu-id="3cd9c-147">深入了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="3cd9c-147">Learn more about how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

