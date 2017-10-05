---
title: "Windows 通用 app SDK 內容"
description: "了解適用於 Azure Mobile Engagement 的 Windows 通用 app SDK 的內容"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="a057f-103">Windows 通用 app SDK 內容</span><span class="sxs-lookup"><span data-stu-id="a057f-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="a057f-104">本文件列出及說明 SDK 在應用程式中部署的內容。</span><span class="sxs-lookup"><span data-stu-id="a057f-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="a057f-105">`/Resources` 資料夾</span><span class="sxs-lookup"><span data-stu-id="a057f-105">The `/Resources` folder</span></span>
<span data-ttu-id="a057f-106">此資料夾包含 Mobile Engagement 需要的所有資源。</span><span class="sxs-lookup"><span data-stu-id="a057f-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="a057f-107">您也可以自訂它們，以符合您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a057f-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="a057f-108">`EngagementConfiguration.xml` ：Mobile Engagement 的組態檔，您可以在此自訂 Mobile Engagement 的設定 (Mobile Engagement 連接字串、報告當機...)。</span><span class="sxs-lookup"><span data-stu-id="a057f-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="a057f-109">/html 資料夾</span><span class="sxs-lookup"><span data-stu-id="a057f-109">/html folder</span></span>
* <span data-ttu-id="a057f-110">`EngagementNotification.html`：應用程式內橫幅的 `Notification` Web 檢視 HTML 設計。</span><span class="sxs-lookup"><span data-stu-id="a057f-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="a057f-111">`EngagementAnnouncement.html`：應用程式內橫幅的 `Announcement` Web 檢視 HTML 設計。</span><span class="sxs-lookup"><span data-stu-id="a057f-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="a057f-112">/images 資料夾</span><span class="sxs-lookup"><span data-stu-id="a057f-112">/images folder</span></span>
* <span data-ttu-id="a057f-113">`EngagementIconNotification.png`：顯示在通知左側的品牌圖示，由您的品牌圖示取代此圖示。</span><span class="sxs-lookup"><span data-stu-id="a057f-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="a057f-114">`EngagementIconOk.png`：動作或驗證按鈕之 Reach 內容頁面的 `Ok` 圖示。</span><span class="sxs-lookup"><span data-stu-id="a057f-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="a057f-115">`EngagementIconNOK.png`：Reach 內容頁面之驗證按鈕停用時的 `NOK` 圖示。</span><span class="sxs-lookup"><span data-stu-id="a057f-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="a057f-116">`EngagementIconClose.png`：隱藏按鈕之 Reach 通知和內容的 `Close` 圖示。</span><span class="sxs-lookup"><span data-stu-id="a057f-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="a057f-117">/overlay 資料夾</span><span class="sxs-lookup"><span data-stu-id="a057f-117">/overlay folder</span></span>
* <span data-ttu-id="a057f-118">`EngagementPageOverlay.cs` ：負責將 Engagement Reach 應用程式內 UI 加入子系的重疊頁面。</span><span class="sxs-lookup"><span data-stu-id="a057f-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

