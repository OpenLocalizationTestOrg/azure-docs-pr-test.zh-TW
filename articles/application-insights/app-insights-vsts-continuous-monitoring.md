---
title: "使用 VSTS 和 Azure Application Insights 連續監視您的 DevOps 發行管線 | Microsoft Docs"
description: "提供指示說明如何快速設定使用 Application Insights 來連續監視"
services: application-insights
keywords: 
author: mrbullwinkle
ms.author: mbullwin
ms.date: 11/13/2017
ms.service: application-insights
ms.topic: article
manager: carmonm
ms.openlocfilehash: 5bfbdd0033f966422a84071a694845627827f016
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="add-continuous-monitoring-to-your-release-pipeline"></a>將連續監視新增至您的發行管線

Visual Studio Team Services (VSTS) 與 Azure Application Insights 整合，可以在整個軟體開發生命週期連續監視 DevOps 發行管線。 

VSTS 現在支援連續監視，發行管線可以從 Application Insights 和其他 Azure 資源納入監視資料。 偵測到 Application Insights 警示時，可以維持閘道部署或者復原，直到解決警示為止。 如果通過所有檢查，部署可以從測試一路自動進行到生產，而不需要手動介入。 

## <a name="configure-continuous-monitoring"></a>設定連續監視

1. 選取現有的 VSTS 專案。

2. 將滑鼠停留在 [組建與版本]> 選取 [版本] > 按一下 **加號**  >  [建立發行定義]> 搜尋**監視** > **Azure App Service 部署與連續監視**。

   ![新增 VSTS 發行定義](.\media\app-insights-continuous-monitoring\001.png)

3. 按一下 [套用]。

4. 在紅色驚嘆號旁選取藍色文字以**檢視環境工作**。

   ![檢視環境工作](.\media\app-insights-continuous-monitoring\002.png)

   將會出現設定方塊，請使用下表來填寫輸入欄位。

    | 參數        | 值 |
   | ------------- |:-----|
   | **環境名稱**      | 名稱，描述發行定義環境 |
   | **Azure 訂用帳戶** | 下拉式清單會填入連結到 VSTS 帳戶的任何 Azure 訂用帳戶|
   | **App Service 名稱** | 根據其他選項而定，此欄位可能需要手動輸入新值 |
   | **資源群組**    | 下拉式清單會填入可用的資源群組 |
   | **Application Insights 資源名稱** | 下拉式清單會填入所有 Application Insights 資源，這些資源對應至先前選取的資源群組。

5. 選取 [設定 Application Insights 警示]

6. 如需預設警示規則，選取 [儲存] > 輸入描述性註解 > 按一下 [確定]

## <a name="modify-alert-rules"></a>修改警示規則

1. 若要修改預先定義的警示設定，請按一下 [警示規則] 右邊具有**省略符號...** 的方塊。

   (現成四個警示規則會出現：可用性、失敗要求、伺服器回應時間、伺服器例外狀況。)

2. 按一下 [可用性] 旁邊的下拉式清單符號。

3. 修改可用性**閾值**以符合您的服務等級需求。

   ![修改警示](.\media\app-insights-continuous-monitoring\003.png)

4. 選取 [確定]  >  [儲存] > 輸入描述性註解 > 按一下 [確定]。

## <a name="add-deployment-conditions"></a>新增部署條件

1. 按一下 [管線] > 選取 [部署前的條件] 或 [部署後的條件] 符號，取決於需要連續監視閘道的階段。

   ![部署前的條件](.\media\app-insights-continuous-monitoring\004.png)

2. 將 [閘道] 設定為 [啟用]  >  **核准閘道** > 按一下 [新增]。

3. 選取 [Azure 監視器] (此選項可讓您存取 Azure 監視器和 Application Insights 兩者的警示)

    ![Azure 監視器](.\media\app-insights-continuous-monitoring\005.png)

4. 輸入**閘道逾時**值。

5. 輸入**取樣間隔**。

## <a name="deployment-gate-status-logs"></a>部署閘道狀態記錄

一旦您新增部署閘道，Application Insights 中超過您先前定義閾值的警示，會防止您從不想要的版本提升來部署。 一旦解決警示，部署就會自動繼續進行。

若要觀察此行為，請選取 [版本] > 以滑鼠右鍵按一下版本名稱以**開啟** > **記錄**。

![記錄檔](.\media\app-insights-continuous-monitoring\006.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 VSTS 建置和版本，請嘗試這些[快速入門](https://docs.microsoft.com/vsts/build-release/)。
