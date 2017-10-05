---
title: "Application Insights 的發行註解 | Microsoft Docs"
description: "在 Application Insights 中對計量瀏覽器新增部署或建置標記。"
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
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Application Insights 中度量圖表上的註解
[計量瀏覽器](app-insights-metrics-explorer.md)圖表上的註解會顯示您在哪裡部署了新的組建，或是其他重要事件。 註解可讓您輕鬆查看變更是否對應用程式的效能有任何影響。 [Visual Studio Team Services 建置系統](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs)可以自動建立這些註解。 您也可以[從 PowerShell 建立註解](#create-annotations-from-powershell)來標幟您想要的任何事件。

![註解範例，其會顯示與伺服器回應時間的相互關聯](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>與 VSTS 組建搭配的發行註解

發行註解是 Visual Studio Team Services 的雲端型組建和發行服務的功能。 

### <a name="install-the-annotations-extension-one-time"></a>安裝註解擴充功能 (一次)
若要能夠建立發行註解，必須安裝 Visual Studio Marketplace 中許多可用 Team Service 擴充功能的其中一個。

1. 登入您的 [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) 專案。
2. 在 Visual Studio Marketplace 中， [取得發行註解擴充功能](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)，並將其加入至 Team Services 帳戶。

![在 Team Services 網頁右上角開啟 Marketplace。 選取 [Visual Team Services]，然後在 [組建和發行] 下選擇 [查看更多]。](./media/app-insights-annotations/10.png)

您只需要為 Visual Studio Team Services 帳戶執行一次。 現在就能為帳戶中的任何專案設定發行註解。 

### <a name="configure-release-annotations"></a>設定發行註解

您必須為每個 VSTS 發行範本取得個別的 API 金鑰。

1. 登入 [Microsoft Azure 入口網站](https://portal.azure.com)，然後開啟監視您應用程式的 Application Insights 資源。 (或如果您尚未建立該資源，請[立即建立一個](app-insights-overview.md))。
2. 開啟 [API 存取]、[Application Insights 識別碼]。
   
    ![在 portal.azure.com 中，開啟您的 Application Insights 資源然後選擇 [設定]。 開啟 [API 存取]。 複製應用程式識別碼](./media/app-insights-annotations/20.png)

4. 在另一個瀏覽器視窗中，開啟 (或建立) 可從 Visual Studio Team Services 管理部署的發行範本。 
   
    新增工作，然後從功能表中選取 Application Insights 發行註解工作。
   
    將您從 [API 存取] 刀鋒視窗複製的應用程式識別碼  貼上。
   
    ![在 Visual Studio Team Services 中，開啟 [發行]，選取一項發行定義，然後選擇 [編輯]。 按一下 [新增工作] 然後選取 [Application Insights 發行註解]。 貼上 Application Insights 識別碼。](./media/app-insights-annotations/30.png)
4. 將 [APIKey] 欄位設定為變數 `$(ApiKey)`。

5. 回到 Azure 視窗，建立新的「API 金鑰」並複製它。
   
    ![在 [Azure] 視窗的 [API 存取] 刀鋒視窗中，按一下 [建立 API 金鑰]。 提供註解，檢查 [寫入註解]，然後按一下 [產生金鑰]。 複製新的金鑰。](./media/app-insights-annotations/40.png)

6. 開啟發行範本的 [設定] 索引標籤。
   
    建立 `ApiKey`的變數定義。
   
    將您的 API 金鑰貼上至 ApiKey 變數定義。
   
    ![在 [Team Services] 視窗中，選取 [設定] 索引標籤然後按一下 [新增變數]。 設定 ApiKey 的名稱，並在 [值] 中，貼上剛才產生的金鑰，然後按一下鎖定圖示。](./media/app-insights-annotations/50.png)
7. 最後，儲存  發行定義。


## <a name="view-annotations"></a>檢視註解
現在，每當您使用發行範本來部署新的發行，就會將註解傳送至 Application Insights。 註解將會出現在計量瀏覽器的圖表上。

按一下任一註解標記即可開啟版本的詳細資料，包括要求者、來源控制分支、版本定義、環境等。

![按一下任一版本註解標記。](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>從 PowerShell 建立自訂註解
您也可以從任何您喜歡的處理程序建立註解 (不使用 VS Team System)。 


1. 建立一個[來自 GitHub 的 Powershell 指令碼](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)的本機複本。

2. 從 [API 存取] 刀鋒視窗中取得「應用程式識別碼」並建立 API 金鑰。

3. 依下列方式呼叫指令碼：

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

修改指令碼很簡單，例如，修改成建立過去的註解。

## <a name="next-steps"></a>後續步驟

* [建立工作項目](app-insights-diagnostic-search.md#create-work-item)
* [使用 PowerShell 進行自動化](app-insights-powershell.md)
