---
title: "新的 Azure Application Insights 資源 aaaCreate |Microsoft 文件"
description: "針對新的即時應用程式手動設定 Application Insights 監視。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>建立 Application Insights 資源
Azure Application Insights 會在 Microsoft Azure「資源」中顯示您應用程式的相關資料。 建立新的資源屬於因此[新的應用程式設定 Application Insights toomonitor][start]。 在許多情況下，建立資源即可自動 hello IDE。 但在某些情況下，您手動建立資源-toohave 進行開發和生產環境的個別資源，例如建置應用程式。

建立 hello 資源之後，您會取得其檢測金鑰，並使用該 tooconfigure hello SDK hello 應用程式中。 hello 資源的索引鍵連結 hello 遙測 toohello 資源。

## <a name="sign-up-toomicrosoft-azure"></a>註冊 Azure tooMicrosoft
如果您還沒有 [Microsoft 帳戶，請立即申請](http://live.com)。 (如果您使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，就會有 Microsoft 帳戶)。

您也需要訂用帳戶太[Microsoft Azure](http://azure.com)。 如果您的小組或組織有 Azure 訂用帳戶，hello 擁有者可以將您加入 tooit，使用您的 Windows Live id。 您只需針對使用的項目付費。 hello 基本計劃可讓您免費的實驗使用數量。

當您有存取 tooa 訂用帳戶時，登入在 tooApplication Insights [http://portal.azure.com](https://portal.azure.com)，並使用您的 Live ID toologin。

## <a name="create-an-application-insights-resource"></a>建立 Application Insights 資源
在 hello [portal.azure.com](https://portal.azure.com)，加入 Application Insights 資源：

![按一下 新增，然後按一下Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **應用程式類型**會影響您在 hello 概觀刀鋒視窗，然後 hello 中可用的屬性上看到[度量總管][metrics]。 如果沒有看到您的應用程式類型，請選擇 [一般]。
* **訂用帳戶** 是您在 Azure 中的付款帳戶。
* **資源群組** 可讓您輕鬆管理屬性，例如存取控制。 如果您已經建立其他 Azure 資源，您可以選擇 tooput 這個新的資源中 hello 相同的群組。
* **位置** 是我們保留您資料的地方。
* **Pin toodashboard**可以在 Azure 首頁上放置快速存取磚以取得您的資源。 建議使用。

建立您的應用程式後，會開啟新的刀鋒視窗。 此刀鋒視窗是您會在其中看到應用程式的效能和使用情況資料的位置。 

tooget 後 tooit 下次您登入 tooAzure，尋找您的應用程式快速入門圖格上 hello 開始面板 （主畫面）。 或按一下瀏覽 toofind 它。

## <a name="copy-hello-instrumentation-key"></a>複製 hello 檢測金鑰
hello 檢測金鑰會識別您所建立的 hello 資源。 您需要 toogive toohello SDK。

![按一下 Essentials，請按一下 hello 檢測金鑰 CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>安裝應用程式中的 hello SDK
安裝應用程式中的 hello Application Insights SDK。 此步驟中有很大取決於您的應用程式的 hello 類型。 

使用 hello 檢測金鑰 tooconfigure [hello 您安裝應用程式中的 SDK][start]。

hello SDK 包含標準不需要您 toowrite 任何程式碼傳送遙測的模組。 tootrack 使用者動作或診斷問題的詳細資料，[使用 hello API] [ api] toosend 您自己的遙測。

## <a name="monitor"></a>查看遙測資料
關閉 hello 快速啟動刀鋒視窗 tooreturn tooyour 應用程式 刀鋒視窗中 hello Azure 入口網站。

按一下 hello 搜尋磚 toosee[診斷搜尋][diagnostic]、 hello 第一個事件的出現位置。 

如果您預期有更多資料，請在幾秒之後按一下 [重新整理]。

## <a name="creating-a-resource-automatically"></a>自動建立資源
您可以撰寫[PowerShell 指令碼](app-insights-powershell.md)toocreate 資源自動。

## <a name="next-steps"></a>後續步驟
* [建立儀表板](app-insights-dashboards.md)
* [診斷搜尋](app-insights-diagnostic-search.md)
* [探索度量](app-insights-metrics-explorer.md)
* [撰寫分析查詢](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

