---
title: "開始使用 Azure 中的自動調整規模的 aaaGet |Microsoft 文件"
description: "深入了解如何 tooscale 您在 Azure 中的資源。"
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>開始在 Azure 中自動調整規模
本文說明如何 tooset 您 hello Microsoft Azure 入口網站中資源的自動調整規模設定。

只有 toovirtual 機器擴展集、 雲端服務、 Azure App Service 方案和應用程式服務環境，適用於 azure 監視的自動調整規模。 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>探索您的訂用帳戶中的 hello 自動調整規模設定
您可以探索所有自動調整會針對適用的 Azure 監視中的 hello 資源。 使用下列逐步解說的步驟 hello:

1. 開啟 hello [Azure 入口網站。][1]
2. 按一下 hello 左窗格中的 hello Azure 監視器圖示。
  ![開啟 Azure 監視器][2]
3. 按一下**自動調整規模**tooview 所有 hello 資源的自動調整規模都是適用的資源，以及其目前的自動調整狀態。
  ![探索 Azure 監視器中的自動調整規模][3]

您可以使用 hello 向特定的資源群組、 特定的資源類型或特定的資源中的 hello 清單 tooselect 資源的最上層 tooscope hello 篩選 窗格。

每個資源，您會發現 hello 目前執行個體計數和 hello 自動調整狀態。 hello 自動調整狀態可以是：

- **未設定**︰您尚未針對此資源啟用自動調整規模。
- **已啟用**：您已針對此資源啟用自動調整規模。
- **已停用**：您已針對此資源停用自動調整規模。

## <a name="create-your-first-autoscale-setting"></a>建立您的第一個自動調整規模設定

我們現在，請透過簡單的逐步解說 toocreate 第一次的自動調整規模設定。

1. 開啟 hello**自動調整規模**刀鋒視窗中 Azure 監視器，然後選取您想要 tooscale 的資源。 （hello 下列步驟使用 web 應用程式相關聯的應用程式服務計劃。 您可以[在 5 分鐘內，將您的第一個 ASP.NET Web 應用程式建立在 Azure 中][4])
2. 請注意 hello 目前執行個體計數為 1。 按一下 [啟用自動調整規模]。
  ![適用於新 Web 應用程式的調整規模設定][5]
3. 提供設定，hello 標尺的名稱，然後按**新增規則**。 請注意 hello 右側的 [內容] 窗格為開啟的 hello 調整規則選項。 根據預設，這會設定您的執行個體計數 1，如果 hello hello 資源的 CPU 百分比超過 70%的 hello 選項 tooscale。 將其保留為預設值，然後按一下 [新增]。
  ![建立 Web 應用程式的調整規模設定][6]
4. 您現在已建立第一個調整規模規則。 請注意 UX 建議最佳作法，並指出該 hello"建議 toohave 規則中的至少一個小數位數。" toodo 因此：
  
    a. 按一下 [新增規則]。 

    b. 設定**運算子**太**小於**。

    c. 設定**閾值**太**20**。

    d. 設定**作業**太**減少計數所依據**。

   您現在應該會有一個調整規模設定，其會根據 CPU 使用量進行相應放大/相應縮小。
   ![根據 CPU 調整規模][8]
5. 按一下 [儲存] 。

恭喜！ 現在您已成功建立 web 應用程式根據 CPU 使用量您第一個小數位數設定 tooautoscale。

> [!NOTE] 
> hello 相同的步驟都適用 tooget 開始使用的虛擬機器擴展集或雲端服務角色。

## <a name="other-considerations"></a>其他考量
### <a name="scale-based-on-a-schedule"></a>根據排程進行調整
此外 tooscale 根據 CPU，您可以設定您的標尺不同的 hello 一週的特定幾天。

1. 按一下 [新增調整規模的條件]。
2. 設定模式和 hello 規則 hello 小數位數是 hello 相同當做 hello 預設條件。
3. 選取**重複特定幾天**hello 排程。
4. 選取 hello 天和 hello 開始/結束時間應套用 hello 小數位數的條件。

![根據排程調整規模的條件][9]
### <a name="scale-differently-on-specific-dates"></a>在特定日期以不同方式調整規模
此外 tooscale 根據 CPU，您可以設定您的標尺以不同方式的特定日期。

1. 按一下 [新增調整規模的條件]。
2. 設定模式和 hello 規則 hello 小數位數是 hello 相同當做 hello 預設條件。
3. 選取**指定開始/結束日期**hello 排程。
4. 選取 hello 開始/結束日期和 hello 開始/結束時間應套用 hello 小數位數的條件。

![根據日期調整規模的條件][10]

### <a name="view-hello-scale-history-of-your-resource"></a>檢視您資源的 hello 標尺歷程記錄
每當您的資源縮放向上或向下，事件會記錄在 hello 活動記錄檔。 您可以檢視 hello 標尺記錄之資源的 hello 過去 24 小時內切換 toohello**執行歷程記錄** 索引標籤。

![執行記錄][11]

如果您想 tooview hello 完成延展歷程記錄 (如向上 too90 天)，請選取**按一下這裡 toosee 更多詳細資料**。 hello 活動記錄檔會開啟，預先選取您的資源和類別目錄的自動調整規模。

### <a name="view-hello-scale-definition-of-your-resource"></a>檢視您資源的 hello 小數位數定義
自動調整規模是 Azure Resource Manager 的資源。 您可以在 JSON 中檢視 hello 小數位數的定義，藉由切換 toohello **JSON**  索引標籤。

![調整規模定義][12]

您可以視需要直接在 JSON 中進行變更。 變更將在儲存後生效。

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>停用自動調整規模並手動調整執行個體規模
可能會有時間，當您想 toodisable 目前的調整規模設定並手動調整您的資源。

按一下 hello**停用自動調整規模**hello 頂端的按鈕。
![停用自動調整規模][13]

> [!NOTE] 
> 此選項會停用您的設定。 不過，您可以取得 tooit 之後重新啟用自動調整規模。 

您現在可以設定您想 tooscale toomanually 的執行個體的 hello 數目。

![設定手動調整規模][14]

您可以按一下傳回 tooAutoscale**啟用自動調整規模**然後**儲存**。

## <a name="next-steps"></a>後續步驟
- [建立活動記錄警示 toomonitor 訂用帳戶上的所有自動調整引擎作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [建立活動記錄警示 toomonitor 訂用帳戶所有失敗的自動調整標尺輸入/向外作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

