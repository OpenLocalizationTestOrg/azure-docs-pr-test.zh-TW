---
title: "StorSimple Manager 服務儀表板 | Microsoft Docs"
description: "描述 StorSimple Manager 服務儀表板，以及如何使用它來監視 StorSimple 解決方案的健全狀況。"
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
ms.openlocfilehash: 596431b7279b753ca4da838eb028cdde2022ce02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-dashboard"></a><span data-ttu-id="e417c-103">使用 StorSimple Manager 服務儀表板</span><span class="sxs-lookup"><span data-stu-id="e417c-103">Use the StorSimple Manager service dashboard</span></span>
## <a name="overview"></a><span data-ttu-id="e417c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e417c-104">Overview</span></span>
<span data-ttu-id="e417c-105">StorSimple Manager 服務儀表板頁面提供連線至 StorSimple Manager 服務的所有裝置的摘要檢視，並強調顯示需要系統管理員注意的裝置。</span><span class="sxs-lookup"><span data-stu-id="e417c-105">The StorSimple Manager service dashboard page provides a summary view of all the devices that are connected to the StorSimple Manager service, highlighting those that need a system administrator's attention.</span></span> <span data-ttu-id="e417c-106">本教學課程介紹儀表板頁面、說明儀表板內容和功能，並說明您可以從這個頁面執行的工作。</span><span class="sxs-lookup"><span data-stu-id="e417c-106">This tutorial introduces the dashboard page, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![服務儀表板](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

<span data-ttu-id="e417c-108">StorSimple Manager 服務儀表板會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e417c-108">The StorSimple Manager service dashboard displays the following information:</span></span>

* <span data-ttu-id="e417c-109">在 **圖表** 區域中，您可以查看裝置的相關度量圖表。</span><span class="sxs-lookup"><span data-stu-id="e417c-109">In the **chart** area, you can see the relevant metrics chart for your devices.</span></span> <span data-ttu-id="e417c-110">您可以檢視所有裝置上使用的主要儲存體 (本機釘選與分層式)，以及經過一段時間裝置已耗用的雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="e417c-110">You can view the primary storage (locally pinned and tiered) used across all the devices, as well as the cloud storage consumed by devices over a period of time.</span></span> <span data-ttu-id="e417c-111">使用圖表右上角的控制項，指定 1 週、1 個月、3 個月或 1 年的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e417c-111">Use the controls in the top-right corner of the chart to specify a 1-week, 1-month, 3-month, or 1-year time scale.</span></span>
* <span data-ttu-id="e417c-112">[ **使用量概觀** ] 相對於所有裝置可用的總儲存體，顯示所有裝置已佈建和使用的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="e417c-112">The **usage overview** shows the primary storage that is provisioned and consumed by all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="e417c-113">[已佈建] 是指已準備和配置來使用的儲存體數量，而 [已使用] 是指向連接至裝置的啟動器所可看的磁碟區用量。</span><span class="sxs-lookup"><span data-stu-id="e417c-113">**Provisioned** refers to the amount of storage that is prepared and allocated for use, while **Used** refers to usage of volumes as viewed by the initiators that are connected to the devices.</span></span>
* <span data-ttu-id="e417c-114">[ **警示** ] 區域提供所有裝置上的所有作用中警示的快照集，依警示嚴重性分組。</span><span class="sxs-lookup"><span data-stu-id="e417c-114">The **alerts** area provides a snapshot of all the active alerts across all the devices, grouped by alert severity.</span></span> <span data-ttu-id="e417c-115">按一下嚴重性層級會開啟 [ **警示** ] 頁面，只顯示那些警示。</span><span class="sxs-lookup"><span data-stu-id="e417c-115">Clicking the severity level opens the **Alerts** page, scoped to show those alerts.</span></span> <span data-ttu-id="e417c-116">在 [ **警示** ] 頁面上，您可以按一下個別警示來檢視該警示的其他詳細資料，包括任何建議的動作。</span><span class="sxs-lookup"><span data-stu-id="e417c-116">On the **Alerts** page, you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="e417c-117">如果已解決問題，您也可以清除警示。</span><span class="sxs-lookup"><span data-stu-id="e417c-117">You can also clear the alert if the issue has been resolved.</span></span>
* <span data-ttu-id="e417c-118">[ **作業** ] 區域提供連線到服務的所有裝置上的最近工作的快照集。</span><span class="sxs-lookup"><span data-stu-id="e417c-118">The **jobs** area provides a snapshot of recent jobs across all devices that are connected to your service.</span></span> <span data-ttu-id="e417c-119">您可以利用連結查看目前正在進行的作業、過去 24 小時失敗的作業，或排定在接下來 24 小時內執行的作業。</span><span class="sxs-lookup"><span data-stu-id="e417c-119">There are links that you can use to look at jobs that are currently in progress, those that failed in the last 24 hours, or those that are scheduled to run in the next 24 hours.</span></span>
* <span data-ttu-id="e417c-120">[ **快速概覽** ] 區域提供有用的資訊，例如服務狀態、連接到服務的裝置數目、服務的位置，以及與服務相關聯的訂用帳戶的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e417c-120">The **quick glance** area provides useful information such as service status, number of devices connected to the service, location of the service, and details of the subscription that is associated with the service.</span></span> <span data-ttu-id="e417c-121">另外還有作業記錄檔的連結。</span><span class="sxs-lookup"><span data-stu-id="e417c-121">There is also a link to the operations log.</span></span> <span data-ttu-id="e417c-122">按一下連結即可查看所有已完成的 StorSimple Manager 服務作業的清單。</span><span class="sxs-lookup"><span data-stu-id="e417c-122">Click the link to see a list of all completed StorSimple Manager service operations.</span></span>

<span data-ttu-id="e417c-123">您可以使用 StorSimple Manager 服務儀表板頁面來起始下列工作：</span><span class="sxs-lookup"><span data-stu-id="e417c-123">You can use the StorSimple Manager service dashboard page to initiate the following tasks:</span></span>

* <span data-ttu-id="e417c-124">檢視或重新產生服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="e417c-124">View or regenerate the service registration key.</span></span>
* <span data-ttu-id="e417c-125">變更服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e417c-125">Change the service data encryption key.</span></span>
* <span data-ttu-id="e417c-126">檢視作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e417c-126">View the operation logs.</span></span>

## <a name="view-or-regenerate-the-service-registration-key"></a><span data-ttu-id="e417c-127">檢視或重新產生服務註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="e417c-127">View or regenerate the service registration key</span></span>
<span data-ttu-id="e417c-128">服務註冊金鑰用於向 StorSimple Manager 服務註冊 Microsoft Azure StorSimple 裝置，之後裝置就會出現在Azure 傳統入口網站中，讓您採取進一步的管理動作。</span><span class="sxs-lookup"><span data-stu-id="e417c-128">The service registration key is used to register a Microsoft Azure StorSimple device with the StorSimple Manager service, so that the device appears in the Azure classic portal for further management actions.</span></span> <span data-ttu-id="e417c-129">金鑰是在第一個裝置上建立，然後與其餘裝置共用。</span><span class="sxs-lookup"><span data-stu-id="e417c-129">The key is created on the first device and shared with the rest of your devices.</span></span>

<span data-ttu-id="e417c-130">按一下 [註冊金鑰]\(在頁面底部) 會開啟 [服務註冊金鑰] 對話方塊，您可以在此處將目前的服務註冊金鑰複製到剪貼簿，或重新產生服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="e417c-130">Clicking **Registration Key** (at the bottom of the page) opens the **Service Registration Key** dialog box, where you can either copy the current service registration key to the clipboard or regenerate the service registration key.</span></span>

<span data-ttu-id="e417c-131">重新產生金鑰並不會影響先前註冊的裝置：只會影響重新產生金鑰之後，才向服務註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="e417c-131">Regenerating the key does not affect previously registered devices: it affects only the devices that are registered with the service after the key is regenerated.</span></span>

<span data-ttu-id="e417c-132">如需有關檢視和產生服務註冊金鑰的詳細資訊，請移至 [取得服務註冊金鑰](storsimple-manage-service.md#get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="e417c-132">For more information about viewing and generating the service registration key, go to [Get the service registration key](storsimple-manage-service.md#get-the-service-registration-key).</span></span>

## <a name="change-the-service-data-encryption-key"></a><span data-ttu-id="e417c-133">變更服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="e417c-133">Change the service data encryption key</span></span>
<span data-ttu-id="e417c-134">服務資料加密金鑰用來加密從 StorSimple Manager 服務傳送至 StorSimple 裝置的機密客戶資料，例如儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="e417c-134">Service data encryption keys are used to encrypt confidential customer data, such as storage account credentials, that are sent from your StorSimple Manager service to the StorSimple device.</span></span> <span data-ttu-id="e417c-135">如果您的 IT 組織在存放裝置上有金鑰輪替原則，則您必須定期變更這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="e417c-135">You will need to change these keys periodically if your IT organization has a key rotation policy on the storage devices.</span></span> <span data-ttu-id="e417c-136">根據 StorSimple Manager 服務是管理單一裝置或多個裝置而定，金鑰變更程序可能稍有不同。</span><span class="sxs-lookup"><span data-stu-id="e417c-136">The key change process can be slightly different depending on whether there is a single device or multiple devices managed by the StorSimple Manager service.</span></span>

<span data-ttu-id="e417c-137">變更服務資料加密金鑰分成 3 個步驟：</span><span class="sxs-lookup"><span data-stu-id="e417c-137">Changing the service data encryption key is a 3-step process:</span></span>

1. <span data-ttu-id="e417c-138">使用 Azure 傳統入口網站，授權裝置來變更服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e417c-138">Using the Azure classic portal, authorize a device to change the service data encryption key.</span></span>
2. <span data-ttu-id="e417c-139">使用 Windows PowerShell for StorSimple，起始服務資料加密金鑰變更。</span><span class="sxs-lookup"><span data-stu-id="e417c-139">Using Windows PowerShell for StorSimple, initiate the service data encryption key change.</span></span>
3. <span data-ttu-id="e417c-140">如果您有一個以上的 StorSimple 裝置，請在其他裝置上更新服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e417c-140">If you have more than one StorSimple device, update the service data encryption key on the other devices.</span></span>

<span data-ttu-id="e417c-141">下列步驟將說明服務資料加密金鑰的變換程序。</span><span class="sxs-lookup"><span data-stu-id="e417c-141">The following steps describe the rollover process for the service data encryption key.</span></span>

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-the-operations-logs"></a><span data-ttu-id="e417c-142">檢視作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="e417c-142">View the operations logs</span></span>
<span data-ttu-id="e417c-143">您可以在儀表板的 [ **快速概覽** ] 窗格中按一下可用的作業記錄檔連結，以檢視作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e417c-143">You can view the operation logs by clicking the operation logs link available in the **quick glance** pane of the dashboard.</span></span> <span data-ttu-id="e417c-144">這樣會移至管理服務頁面，讓您篩選並查看 StorSimple Manager 服務特定的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e417c-144">This will take you to the management services page, where you can filter and see the logs specific to your StorSimple Manager service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e417c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e417c-145">Next steps</span></span>
* <span data-ttu-id="e417c-146">了解如何 [進行 StorSimple 裝置的疑難排解](storsimple-troubleshoot-operational-device.md)。</span><span class="sxs-lookup"><span data-stu-id="e417c-146">Learn how to [troubleshoot a StorSimple device](storsimple-troubleshoot-operational-device.md).</span></span>
* <span data-ttu-id="e417c-147">深入了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="e417c-147">Learn more about how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

