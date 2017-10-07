---
title: "在 Microsoft Azure 中的度量的 aaaOverview |Microsoft 文件"
description: "了解如何監視 toocustomize 圖表顯示在 Azure 中。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure 中的計量概觀
所有 Azure 服務，來追蹤 toomonitor hello 健全狀況、 效能、 可用性和使用方式，您的服務可讓您的關鍵計量。 您可以在 hello Azure 入口網站中檢視這些度量資訊，而且您也可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello 組完整的度量以程式設計的方式。

某些服務，您可能需要的任何度量 tooturn toosee 順序中的診斷。 對於其他人使用，例如虛擬機器，您會收到一組基本度量，但需要 tooenable hello 完整集頻率高的度量。 請參閱[啟用監視和診斷](insights-how-to-use-diagnostics.md)toolearn 更多。

## <a name="using-monitoring-charts"></a>使用監視圖表
您可以將任何 hello 計量圖表需要將任何您選擇的時間週期內。

1. 在 [hello [Azure 入口網站](https://portal.azure.com/)，按一下**瀏覽**，然後資源您感興趣監視。
2. hello**監視**章節包含的每個 Azure 資源 hello 最重要的指標。 例如，Web 應用程式具有**要求和錯誤**，而虛擬機器則具有 **CPU 百分比**和**磁碟讀取和寫入**：![監視透鏡](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. 按一下任何圖上，會顯示您 hello**度量**刀鋒視窗。 Hello 刀鋒視窗中，此外 toohello 圖形是顯示 hello 度量 （例如平均值、 最小和最大，您所選擇的 hello 時間範圍內） 的彙總的資料表。 請在下方是 hello hello 資源的警示規則。
    ![計量刀鋒視窗](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. toocustomize hello 行出現之後，按一下 hello**編輯**hello 圖表上的按鈕，或 hello**編輯圖表**hello 計量刀鋒伺服器上的命令。
5. Hello 編輯查詢] 刀鋒視窗中，您可以執行三件事：
   
   * 變更 hello 時間範圍
   * 切換 hello 外觀之間列和行
   * 選擇不同的計量 ![編輯查詢](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. 變更 hello 時間範圍非常簡單，只要選取不同的範圍 (例如**過去一小時**)，然後按一下**儲存**在 hello hello 刀鋒視窗的底部。 您也可以選擇**自訂**，可讓您 toochoose 任何時段透過 hello 過去 2 週。 例如，您可以看到 hello 整個兩週，或只昨天 1 小時內。 輸入 hello 文字方塊 tooenter 中不同的小時。
    ![自訂時間範圍](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. 以下 hello 時間範圍，您將會選擇任意數目的度量 tooshow hello 圖表上。
8. 當您按一下 [儲存] 時，系統便會儲存為該特定資源所做的變更。 例如，如果您有兩個虛擬機器，而且您變更其中一個圖表，它不會影響其他 hello。

## <a name="creating-side-by-side-charts"></a>建立並排圖表
與 hello hello 入口網站中功能強大的自訂，您可以新增您想要的許多圖表。

1. 在 [hello **...**功能表頂端的 hello 刀鋒視窗中按一下 hello**新增磚**:  
    ![新增功能表](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. 然後，您可以選取 [選取圖表從 hello**圖庫**螢幕 hello 右側：![組件庫](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. 如果您沒有看到您想要的 hello 度量，您可以新增的其中一個 hello 預先設定的度量，和**編輯**hello 您需要的圖表 tooshow hello 度量。

## <a name="monitoring-usage-quotas"></a>監視使用量配額
大部分的計量會顯示某一段時間的趨勢，但是某些特定資料 (如使用量配額) 則會是包含臨界值的時間點資訊。

您也可以看到 hello 刀鋒視窗中有配額的資源使用量配額：

![使用量](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

像度量，您可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello 整組使用量配額以程式設計的方式。

## <a name="next-steps"></a>後續步驟
* [接收警示通知](insights-receive-alert-notifications.md) 。
* [啟用監視和診斷](insights-how-to-use-diagnostics.md)toocollect 詳細高頻率度量，您的服務。
* [自動調整執行個體計數](insights-how-to-scale.md)toomake 確定您的服務可用，並能繼續回應。
* [監視應用程式效能](../application-insights/app-insights-azure-web-apps.md)如果您想 toounderstand 完全如何您的程式碼執行 hello 雲端中。
* 使用[Application Insights for JavaScript 應用程式及網頁](../application-insights/app-insights-web-track-usage.md)tooget 用戶端分析有關 hello 瀏覽器瀏覽網頁。
* [監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。

