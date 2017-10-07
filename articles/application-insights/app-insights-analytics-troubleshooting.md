---
title: "在 Azure Application Insights 中分析 aaaTroubleshoot |Microsoft 文件"
description: "有關於 Application Insights 分析的問題嗎？ 從這裡開始。 "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>疑難排解 Application Insights 中的分析
有關於 [Application Insights 分析](app-insights-analytics.md)的問題嗎？ 從這裡開始。 分析是 Azure Application Insights hello 功能強大的搜尋工具。

## <a name="limits"></a>限制
* 目前，查詢結果會以有限的 toojust 超過一週的過去的資料。
* 我們測試的瀏覽器︰最新版本的 Chrome、Edge 及 Internet Explorer。

## <a name="known-incompatible-browser-extensions"></a>已知不相容的瀏覽器擴充功能
* Ghostery

停用 hello 擴充功能，或使用不同的瀏覽器。

## <a name="e-a"></a> 「未預期的錯誤」
![[未預期的錯誤] 畫面](./media/app-insights-analytics-troubleshooting/010.png)

在入口網站執行階段期間發生的內部錯誤 – 未處理的例外狀況。

* 清除 hello 瀏覽器的快取。 

## <a name="e-b"></a>403...請再試一次 tooreload
![403...請再試一次 tooreload](./media/app-insights-analytics-troubleshooting/020.png)

發生驗證相關的錯誤 (在驗證期間或存取權杖產生期間)。 hello 入口網站可能沒有太復原，而不變更瀏覽器設定的方法。

* 確認[啟用第三方 cookie](#cookies) hello 瀏覽器中。 

## <a name="authentication"></a>403 ... 確認安全性區域
![403 ... 確認安全性區域](./media/app-insights-analytics-troubleshooting/030.png)

發生驗證相關的錯誤 (在驗證期間或存取權杖產生期間)。 hello 入口網站可能沒有太復原，而不變更瀏覽器設定的方法。

1. 確認[啟用第三方 cookie](#cookies) hello 瀏覽器中。 
2. 是否使用最愛、 書籤或儲存的連結 tooopen hello Analytics 入口網站？ 您登入您儲存 hello 連結時，使用不同的認證嗎？
3. 嘗試使用 InPrivate/incognito 瀏覽器視窗 (關閉所有這類視窗之後)。 您將有 tooprovide 您的認證。 
4. 開啟另一個 （一般） 的瀏覽器視窗，並移過[Azure](https://portal.azure.com)。 登出。然後開啟您的連結，並使用 hello 正確的認證登入。
5. Edge 和 Internet Explorer 的使用者也會在不支援信任的區域設定時收到此錯誤。
   
    同時確認[Analytics 入口網站](https://analytics.applicationinsights.io)和[Azure Active Directory 網站](https://portal.azure.com)hello 中相同的安全性區域：
   
   * 在 Internet Explorer 中，開啟 [網際網路選項]、[安全性]、[信任的網站]、[網站]：
     
     ![網際網路選項 對話方塊，新增站台 tooTrusted 站台](./media/app-insights-analytics-troubleshooting/033.png)
     
     在 hello 網站清單中，如果包含了任何 hello 下列 Url，請確定該 hello 其他人也會包含：
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ...找不到資源
![404 ... 找不到資源](./media/app-insights-analytics-troubleshooting/040.png)

應用程式資源已從 Application Insights 中刪除，且不再提供。 如果您儲存 hello URL toohello 分析 頁面上，也可能會發生。

## <a name="e-e"></a>403 ...沒有授權
![403 ... 未獲授權](./media/app-insights-analytics-troubleshooting/050.png)

您沒有權限 tooopen 此應用程式在分析中。

* 您從別處取得 hello 連結？ 請確定您是在 hello toomake 要求他們[讀者或參與者的這個資源群組](app-insights-resources-roles-access-control.md)。
* 您沒有儲存 hello 連結使用不同的認證嗎？ 開啟 hello [Azure 入口網站](https://portal.azure.com)、 登出，然後再次嘗試此連結，提供 hello 正確的認證。

## <a name="html-storage"></a>403 ...HTML5 儲存體
我們的入口網站會使用 HTML5 localStorage 和 sessionStorage。

* Chrome︰設定、隱私權、內容設定。
* Internet Explorer︰網際網路選項、進階索引標籤、安全性、啟用 DOM 儲存

![403...再試一次 tooenable HTML5 儲存體](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ...找不到訂用帳戶
![404 ...找不到訂用帳戶](./media/app-insights-analytics-troubleshooting/070.png)

hello URL 無效。 

* 開啟中的 hello 應用程式資源[Application Insights 入口網站](https://portal.azure.com)。 然後使用 hello 分析按鈕。

## <a name="e-h"></a>404 ... 頁面不存在
![404 ...頁面不存在](./media/app-insights-analytics-troubleshooting/080.png)

hello URL 無效。

* 開啟中的 hello 應用程式資源[Application Insights 入口網站](https://portal.azure.com)。 然後使用 hello 分析按鈕。

## <a name="cookies"></a>啟用協力廠商 cookie
  請參閱[如何 toodisable 協力廠商 cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers)，但請注意，我們需要**啟用**它們。


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

