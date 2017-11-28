---
title: "aaaWindows 通用應用程式 SDK 的內容"
description: "了解的 hello Windows 通用應用程式 SDK 的 hello 內容適用於 Azure Mobile Engagement"
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
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="7f7d5-103">Windows 通用 app SDK 內容</span><span class="sxs-lookup"><span data-stu-id="7f7d5-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="7f7d5-104">本文件列出並描述應用程式中的 hello SDK 所部署的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="7f7d5-105">hello`/Resources`資料夾</span><span class="sxs-lookup"><span data-stu-id="7f7d5-105">hello `/Resources` folder</span></span>
<span data-ttu-id="7f7d5-106">這個資料夾會包含所有需要 Mobile Engagement 的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="7f7d5-107">您也可以自訂它們 toofit 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="7f7d5-108">`EngagementConfiguration.xml`: hello Mobile Engagement 的組態檔，這是您可以在其中自訂 Mobile Engagement 設定 （Mobile Engagement 連接字串，...報告損毀）。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="7f7d5-109">/html 資料夾</span><span class="sxs-lookup"><span data-stu-id="7f7d5-109">/html folder</span></span>
* <span data-ttu-id="7f7d5-110">`EngagementNotification.html`: hello `Notification` web 檢視 html 設計的應用程式內橫幅。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="7f7d5-111">`EngagementAnnouncement.html`: hello `Announcement` web 應用程式中插入式檢視的檢視 html 設計。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="7f7d5-112">/images 資料夾</span><span class="sxs-lookup"><span data-stu-id="7f7d5-112">/images folder</span></span>
* <span data-ttu-id="7f7d5-113">`EngagementIconNotification.png`: hello 商標圖示顯示在 hello 保留的通知，取代這個品牌圖示。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="7f7d5-114">`EngagementIconOk.png`: hello `Ok` hello 動作或驗證按鈕的 hello 觸達內容頁的圖示。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="7f7d5-115">`EngagementIconNOK.png`: hello `NOK` hello 觸達內容頁的 hello 驗證按鈕已停用時所使用的圖示。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="7f7d5-116">`EngagementIconClose.png`: hello`Close`圖示的 hello 連線到通知和 hello 的內容解除 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="7f7d5-117">/overlay 資料夾</span><span class="sxs-lookup"><span data-stu-id="7f7d5-117">/overlay folder</span></span>
* <span data-ttu-id="7f7d5-118">`EngagementPageOverlay.cs`: hello 覆疊頁面負責將加入的 hello Engagement 觸達在應用程式 UI tooits 子系。</span><span class="sxs-lookup"><span data-stu-id="7f7d5-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>

