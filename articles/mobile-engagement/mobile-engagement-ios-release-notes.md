---
title: "aaaAzure Mobile Engagement iOS SDK 版本資訊 |Microsoft 文件"
description: "Azure Mobile Engagement iOS SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Azure Mobile Engagement iOS SDK 版本資訊

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* 修正在背景清除徽章。
* 修正在 XCode 9 上關於 API 未在主要佇列呼叫的警告。
* 修正觸達輪詢中的記憶體流失。
* 停止支援 iOS 6.X。 從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 7。

## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* 改善在背景中的記錄傳送。

## <a name="400-09122016"></a>4.0.0 (09/12/2016)
* iOS 10 裝置上有固定的通知不會採取動作。
* 取代 XCode 7。

## <a name="324-06302016"></a>3.2.4 (06/30/2016)
* 修正技術記錄和其他記錄之間的彙總。

## <a name="323-06072016"></a>3.2.3 (06/07/2016)
* 其中傳送意見反應閘道並未回報 hello 背景應用程式時的固定的 hello bug。
* 最佳化的技術的記錄檔傳送 hello。

## <a name="322-04072016"></a>3.2.2 (04/07/2016)
* 在 HTTP 要求取消，而有時導致 toocrash 修正的 bug。

## <a name="321-12112015"></a>3.2.1 (12/11/2015)
* 深層連結的通知所觸發的新應用程式執行個體時，固定的 hello 延遲

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* 它可以搭配 hello SDK toomake 中啟用 Bitcode **Xcode 7**。
* 已修正的 bug 相關 tooin 應用程式通知。
* 進行 hello 應用程式內通知發生電力偏低與其他這類案例更可靠。
* 移除第三方程式庫所產生的額外主控台記錄檔。

## <a name="310-08262015"></a>3.1.0 (2015/08/26)
* 搭配協力廠商程式庫修正 iOS 9 相容性錯誤。 當傳送投票結果、應用程式資訊或是額外的資料時會造成當機。

## <a name="300-06192015"></a>3.0.0 (2015/06/19)
* Mobile Engagement 使用無聲推播通知。
* 停止支援 iOS 4.X。 從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 6。

## <a name="220-05212015"></a>2.2.0 (05/21/2015)
* 裝置 hello Mobile Engagement 裝置識別碼 < iOS 6 現在會根據在安裝期間所產生的 GUID。

## <a name="210-04242015"></a>2.1.0 (2015/04/24)
* 新增 Swift 相容性。
* 按一下通知，當 hello 現在是 URL 之後，執行的動作右邊 hello 應用程式開啟。
* 在 SDK 封裝中加入缺少的標頭檔案。
* 停用 hello Mobile Engagement 當機報告時，請修正的問題。

## <a name="200-02172015"></a>2.0.0 (2015/02/17)
* Azure Mobile Engagement 的最初發行版本
* 以連接字串組態取代 appId/sdkKey 組態。
* 移除應用程式開發介面 toosend 和任意 XMPP 訊息接收任意 XMPP 實體。
* 移除應用程式開發介面 toosend 和接收裝置之間的訊息。
* 增強安全性。
* 已移除 SmartAd 追蹤。
