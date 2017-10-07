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
# <a name="windows-universal-apps-sdk-content"></a>Windows 通用 app SDK 內容
本文件列出並描述應用程式中的 hello SDK 所部署的 hello 內容。

## <a name="hello-resources-folder"></a>hello`/Resources`資料夾
這個資料夾會包含所有需要 Mobile Engagement 的 hello 資源。 您也可以自訂它們 toofit 您的應用程式。

* `EngagementConfiguration.xml`: hello Mobile Engagement 的組態檔，這是您可以在其中自訂 Mobile Engagement 設定 （Mobile Engagement 連接字串，...報告損毀）。

### <a name="html-folder"></a>/html 資料夾
* `EngagementNotification.html`: hello `Notification` web 檢視 html 設計的應用程式內橫幅。
* `EngagementAnnouncement.html`: hello `Announcement` web 應用程式中插入式檢視的檢視 html 設計。

### <a name="images-folder"></a>/images 資料夾
* `EngagementIconNotification.png`: hello 商標圖示顯示在 hello 保留的通知，取代這個品牌圖示。
* `EngagementIconOk.png`: hello `Ok` hello 動作或驗證按鈕的 hello 觸達內容頁的圖示。
* `EngagementIconNOK.png`: hello `NOK` hello 觸達內容頁的 hello 驗證按鈕已停用時所使用的圖示。
* `EngagementIconClose.png`: hello`Close`圖示的 hello 連線到通知和 hello 的內容解除 按鈕。

### <a name="overlay-folder"></a>/overlay 資料夾
* `EngagementPageOverlay.cs`: hello 覆疊頁面負責將加入的 hello Engagement 觸達在應用程式 UI tooits 子系。

