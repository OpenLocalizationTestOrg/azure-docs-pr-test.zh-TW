---
title: "Application Insights aaaRelease 註釋 |Microsoft 文件"
description: "新增部署或建置 tooyour 度量總管圖表 Application Insights 中的標記。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Application Insights 中度量圖表上的註解
[計量瀏覽器](app-insights-metrics-explorer.md)圖表上的註解會顯示您在哪裡部署了新的組建，或是其他重要事件。 這個選項讓您輕鬆 toosee 是否變更沒有任何作用，對您的應用程式效能。 它們可以自動建立 hello[建置系統，Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs)。 您也可以建立註解 tooflag 您喜歡的任何事件[建立它們從 PowerShell](#create-annotations-from-powershell)。

![註解範例，其會顯示與伺服器回應時間的相互關聯](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>與 VSTS 組建搭配的發行註解

版本註解是 hello 以雲端為基礎建置的功能和版本的 Visual Studio Team Services 的服務。 

### <a name="install-hello-annotations-extension-one-time"></a>安裝 hello 註解延伸模組 （一次）
toobe 無法 toocreate 版本註解，您將需要一個 tooinstall hello 的許多小組服務延伸模組用於 hello Visual Studio Marketplace。

1. 登入 tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online)專案。
2. 在 Visual Studio Marketplace， [hello 的版本註解延伸](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)，並將它加入 tooyour Team Services 帳戶。

![在 Team Services 網頁右上角開啟 Marketplace。 選取 [Visual Team Services]，然後在 [組建和發行] 下選擇 [查看更多]。](./media/app-insights-annotations/10.png)

您只需要 toodo 這一次為您的 Visual Studio Team Services 帳戶。 現在就能為帳戶中的任何專案設定發行註解。 

### <a name="configure-release-annotations"></a>設定發行註解

您為每個 VSTS 發行範本需要 tooget 的個別 API 金鑰。

1. 登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)並開啟 hello 監視您的應用程式的 Application Insights 資源。 (或如果您尚未建立該資源，請[立即建立一個](app-insights-overview.md))。
2. 開啟 [API 存取]、[Application Insights 識別碼]。
   
    ![在 portal.azure.com 中，開啟您的 Application Insights 資源然後選擇 [設定]。 開啟 [API 存取]。 複製應用程式識別碼 hello](./media/app-insights-annotations/20.png)

4. 在另一個瀏覽器視窗中，開啟 （或建立） 從 Visual Studio Team Services 中管理您的部署的 hello 發行範本。 
   
    將工作，並從 hello 功能表選取 hello 應用程式 Insights 版本註解工作。
   
    貼上 hello**應用程式識別碼**從 hello API 存取 刀鋒視窗中複製。
   
    ![在 Visual Studio Team Services 中，開啟 [發行]，選取一項發行定義，然後選擇 [編輯]。 按一下 [新增工作] 然後選取 [Application Insights 發行註解]。 貼上 hello 應用程式 Insights 識別碼。](./media/app-insights-annotations/30.png)
4. 設定 hello **APIKey**欄位 tooa 變數`$(ApiKey)`。

5. 回到 hello Azure 的視窗，建立新的 API 金鑰，需要一份。
   
    ![在 hello hello Azure 視窗中的應用程式開發介面存取刀鋒視窗中，按一下 建立 API 金鑰。 提供註解，檢查 [寫入註解]，然後按一下 [產生金鑰]。 複製 hello 新索引鍵。](./media/app-insights-annotations/40.png)

6. 開啟 hello hello 發行範本的 [設定] 索引標籤。
   
    建立 `ApiKey`的變數定義。
   
    貼上您的 API 金鑰 toohello ApiKey 變數定義。
   
    ![Hello Team Services 在視窗中，請選取 hello 組態] 索引標籤，然後按一下 [加入變數。 設定 hello 名稱 tooApiKey 並到 hello 值，貼上您剛才產生的 hello 金鑰，然後按一下 hello 鎖定圖示。](./media/app-insights-annotations/50.png)
7. 最後，**儲存**hello 發行定義。


## <a name="view-annotations"></a>檢視註解
現在，當您使用 hello 發行範本 toodeploy 新版本，註解將會傳送 tooApplication 深入資訊。 hello 註解會顯示在計量瀏覽器中的圖表。

按一下任何註解標記 tooopen 詳細 hello 版本中，包括要求者、 原始檔控制分支、 發行定義、 環境、 等等。

![按一下任一版本註解標記。](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>從 PowerShell 建立自訂註解
您也可以從任何您喜歡的處理程序建立註解 (不使用 VS Team System)。 


1. 建立的本機副本 hello [Powershell 指令碼從 GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)。

2. 取得 hello 應用程式識別碼，並建立 API 金鑰從 hello API 存取 刀鋒視窗。

3. 呼叫 hello 指令碼，就像這樣：

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

它是簡單 toomodify hello 指令碼，例如 hello 過去 toocreate 註解。

## <a name="next-steps"></a>後續步驟

* [建立工作項目](app-insights-diagnostic-search.md#create-work-item)
* [使用 PowerShell 進行自動化](app-insights-powershell.md)
