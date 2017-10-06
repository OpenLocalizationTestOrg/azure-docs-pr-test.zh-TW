---
title: "一種載具，健全狀況和驅動 aaaPower BI 儀表板習慣-Azure |Microsoft 文件"
description: "一種載具，健全狀況使用 Cortana 智慧 toogain 即時和預測 insights hello 功能和驅動習慣。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>車輛遙測分析方案範本 Power BI 儀表板安裝指示
這**功能表**連結 toohello 章節，在這個腳本中的。 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

hello Vehicle 遙測分析解決方案示範汽車經銷商、 汽車的製造商和保險的公司可以利用 Cortana 智慧 toogain 即時和預測一種載具，健全狀況和洞察開車 hello 功能習慣 toodrive 改進 hello 區域中的客戶體驗，R&d 與行銷活動。 本文件包含逐步指示如何設定 hello Power BI 報表和儀表板一旦 hello 方案會部署您的訂用帳戶中。 

## <a name="prerequisites"></a>必要條件
1. 部署 hello[遙測分析](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)方案  
2. [安裝 Microsoft Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331)
3. [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。 如果您沒有 Azure 訂用帳戶，請立即取得免費的 Azure 訂用帳戶
4. Microsoft Power BI 帳戶

## <a name="cortana-intelligence-suite-components"></a>Cortana Intelligence Suite 元件
Hello Vehicle 遙測分析解決方案範本的一部分，hello 遵循 Cortana 智慧服務會部署在您的訂用帳戶。

* 事件中樞可將數百萬計的車輛遙測事件擷取至 Azure。
* **串流分析** 」可取得關於車輛健全狀態的即時情資，同時以長期儲存的方式保存這些資料，供日後進行更豐富廣泛的批次分析之用。
* **機器學習**以便進行異常偵測即時和批次處理 toogain 預測的深入資訊。
* **HDInsight**運用 tootransform 大規模的資料
* **Data Factory**處理協調流程排程、 資源管理和監視 hello 批次處理管線。

**Power BI** 為此解決方案提供具備即時資料與預測性分析視覺效果等豐富功能的儀表板。 

hello 解決方案會使用兩個不同的資料來源：**模擬 vehicle 訊號和診斷的資料集**和**vehicle 目錄**。

此方案包含車輛遠程資訊服務模擬器。 它會發出診斷資訊，並告知對應 toohello 狀態 hello vehicle 和推動模式特定時點的時間。 

hello Vehicle 目錄是參考資料集包含 VIN toomodel 對應

## <a name="power-bi-dashboard-preparation"></a>Power BI 儀表板準備
### <a name="setup-power-bi-real-time-dashboard"></a>設定 Power BI 即時儀表板

**啟動 hello 即時儀表板應用程式**hello 部署完成後，您應該遵循 hello 手動操作說明

* 下載即時儀表板應用程式 RealtimeDashboardApp.zip，並將它解壓縮。
*  在 hello 解壓縮資料夾中，開啟 應用程式組態檔 'RealtimeDashboardApp.exe.config'，取代 appSettings Eventhub、 Blob 儲存體和 ML 服務使用的連線 hello 值在 hello 手動操作的指示，和儲存您的變更。
* 執行應用程式 RealtimeDashboardApp.exe。 登入視窗會快顯，提供有效的 power Bi 認證，然後按一下 hello**接受** 按鈕。 然後 toorun 會啟動 hello 應用程式。

   ![登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI 儀表板權限](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* 登入 tooPowerBI 網站，並建立即時儀表板。

現在，您準備好 tooconfigure hello Power BI 儀表板具有豐富視覺效果 toogain 即時而且預測的洞察能力 vehicle 健全狀況和驅動習慣。 它會採用約 45 分鐘內 tooan 小時 toocreate 所有 hello 報告，並設定 hello 儀表板。 

### <a name="configure-power-bi-reports"></a>設定 Power BI 報告
hello 即時報表和 hello 儀表板花費 30-45 分鐘 toocomplete。 瀏覽過[http://powerbi.com](http://powerbi.com)與登入。

![登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Power BI 中會產生新的資料集。 按一下 hello **ConnectedCarsRealtime**資料集。

![選取連接的汽車即時資料集](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

儲存 hello 空白報表使用**Ctrl + s**。

![儲存空白報告](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

提供報告名稱「車輛遙測分析即時 - 報告」 。

![提供報告名稱](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>即時報告
此解決方案有三份即時報告：

1. 行駛中的車輛
2. 需要維修的車輛
3. 車輛健全狀況統計資料

您可以選擇 tooconfigure 所有三個即時報表 hello 或在任何階段後停止，然後繼續進行的設定 hello 批次報表 toohello 下一節。 我們建議您所有的 toocreate hello 三報告 toovisualize hello 完整 insights 的 hello 方案 hello 即時路徑。  

### <a name="1-vehicles-in-operation"></a>1.行駛中的車輛
按兩下**第 1 頁**並將它重新命名過"車輛作業中的"  
    ![Connected Cars - 行駛中的車輛](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

從 [欄位] 中選取 **vin** 欄位，然後選擇「卡片」做為視覺效果類型。  

建立的卡片視覺效果如下圖所示。  
    ![Connected Cars - 選取 vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

按一下 hello 的空白區域 tooadd 新的視覺效果。  

從欄位中選取 **City** 和 **vin**。 變更視覺效果太**「 對應 」**。 將 **vin** 拖曳到值區域。 拖曳**縣 （市)**欄位太**圖例**區域。   
    ![Connected Cars - 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

選取**格式**> 一節**視覺效果**，按一下 **標題**並變更 hello**文字**太**"車輛中依城市的作業 」**。  
    ![Connected Cars - 行駛中的車輛 (依城市)](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

最終的視覺效果如下圖所示。    
    ![Connected Cars - 最終視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

按一下 hello 的空白區域 tooadd 新的視覺效果。  

選取**縣 （市)**和**vin**，視覺效果類型變更太**群組直條圖**。 確定 **City** 欄位在 [軸] 區域，而 **vin** 在 [值] 區域  

依 [vin 的計數]   
    ![Connected Cars - vin 的計數](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

變更圖表**標題**太**」 作業依城市中的車輛"**  

按一下 hello**格式**區段，然後選取 **資料色彩**，按一下 hello **「 On 」**太**全部顯示**  
    ![Connected Cars - 顯示所有資料色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

變更個別的城市 hello 色彩，色彩圖示即可。  
    ![Connected Cars - 變更色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

按一下 hello 的空白區域 tooadd 新的視覺效果。  

從 [視覺效果] 中選取「群組直條圖」視覺效果，將 **city** 欄位拖曳到 [軸] 區域、將 **Model** 拖曳到 [圖例] 區域、將 **vin** 拖曳到 [值] 區域。  
    ![Connected Cars - 群組直條圖](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Connected Cars - 轉譯](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

重新排列此頁面上的所有視覺效果，如下圖所示。  
    ![Connected Cars -視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

您已成功設定 hello"車輛作業中的"即時報表。 您可以繼續 toocreate hello 下一步，即時報表或在此停止，以及設定 hello 儀表板。 

### <a name="2-vehicles-requiring-maintenance"></a>2.需要維修的車輛
按一下![新增](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png)tooadd 新的報表，將它重新命名過**「 車輛需要維護 」**

![Connected Cars - 需要維修的車輛](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

選取**vin**欄位和視覺效果類型變更太**卡**。  
    ![Connected Cars - Vin 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

我們有 hello 資料集中名為"MaintenanceLabel"的欄位。 此欄位的值可以是 “0” 或 “1”。 它會設定由佈建為方案的一部分，而且與 hello 即時路徑整合 hello Azure 機器學習模型。 hello 值"1"表示一種載具，需要維護。 

tooadd**頁面層級**顯示需要維護的車輛資料篩選條件： 

1. 拖曳 hello **"MaintenanceLabel"**欄位到**頁面層級篩選**。  
   ![Connected Cars - 頁面層級篩選](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. 按一下 MaintenanceLabel 頁面層級篩選底部出現的 [基本篩選]  功能表。  
   ![Connected Cars - 基本篩選](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. 設定其篩選值太**"1"**    
   ![Connected Cars - 篩選值](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

按一下 hello 的空白區域 tooadd 新的視覺效果。  

從 [視覺效果] 中選取「群組直條圖」  
![Connected Cars - Vind 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Connected Cars - 群組直條圖](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

拖曳欄位**模型**到**軸**區域中， **Vin**太**值**區域。 然後，依 [vin 的計數] 排序視覺效果。  變更圖表**標題**太**"車輛模型需要維護 」**  

將 **vin** 欄位拖曳到 [視覺效果] 索引標籤的 [欄位] ![欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) 區段上出現的 [色彩飽和度]  
![Connected Cars - 色彩飽和度](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

從 [格式] 區段變更視覺效果中的 [資料色彩]  
將最小值色彩變更為：**F2C812**  
將最大值色彩變更為：**FF6300**  
![Connected Cars - 色彩變更](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Connected Cars - 新的視覺效果色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

按一下 hello 的空白區域 tooadd 新的視覺效果。  

從 [視覺效果] 中選取「群組直條圖」，將 **vin** 欄位拖曳到 [值] 區域，將 **City** 欄位拖曳到 [軸] 區域。 依 [vin 的計數] 排序圖表。 變更圖表**標題**太**"車輛需要維護縣 （市） 」**   
![Connected Cars - 需要維修的車輛 (依城市)](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

按一下 hello 的空白區域 tooadd 新的視覺效果。  

選取**多列卡片**視覺效果，從視覺效果拖曳**模型**和**vin**到 hello**欄位**區域。  
![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

重新整理所有 hello 視覺效果，hello 最終報表看都起來如下：  
![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

您已成功設定 hello"車輛需要 Maintenance"即時報表。 您可以繼續 toocreate hello 下一步，即時報表或在此停止，以及設定 hello 儀表板。 

### <a name="3-vehicles-health-statistics"></a>3.車輛健全狀況統計資料
按一下![新增](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png)tooadd 新報表、 將它重新命名過**"車輛健全狀況統計資料 」**  

選取**量測計**視覺效果從視覺效果，然後將拖曳 hello**速度**欄位到**值、 最小值，最大值**區域。  
![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

變更 hello 預設彙總的**速度**中**值區域**太**平均** 

變更 hello 預設彙總的**速度**中**最小值 區域**太**最小值**

變更 hello 預設彙總的**速度**中**最大值區**太**上限**

![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

重新命名 hello**量測計標題**太**「 平均速度 」** 

![Connected Cars - 量測計](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

按一下 hello 的空白區域 tooadd 新的視覺效果。  

同樣地加入「平均機油」、「平均油量」和「平均引擎溫度」的**量測計**。  

變更 hello 預設彙總的每個量測計中依照上述步驟中的欄位**「 平均速度 」**量測計。

![Connected Cars - 量測計](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

按一下 hello 的空白區域 tooadd 新的視覺效果。

選取**折線與群組直條圖**從視覺效果，然後將拖曳**縣 （市)**欄位到**共用軸**，拖曳**速度**， **tirepressure 和 engineoil 欄位**到**資料行值**區域中，變更其彙總類型太**平均**。 

拖曳 hello **engineTemperature**欄位到**行值**區域中，也變更 hello 彙總類型**平均**。 

![Connected Cars -視覺效果欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

變更 hello 圖表**標題**太**「 平均速度、 tire 不足的壓力，引擎石油和引擎溫度 」**。  

![Connected Cars -視覺效果欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

按一下 hello 的空白區域 tooadd 新的視覺效果。

選取**矩形式樹狀結構圖**視覺效果，從視覺效果拖曳 hello**模型**欄位到 hello**群組**區域中，然後拖曳 hello 欄位**MaintenanceProbability**到 hello**值**區域。

變更 hello 圖表**標題**太**"Vehicle 模型需要維護 >**。

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

按一下 hello 的空白區域 tooadd 新的視覺效果。

選取**100%堆疊橫條圖**從 視覺效果中，拖曳 hello**縣 （市)**欄位到 hello**軸**區域中，然後拖曳 hello **MaintenanceProbability**， **RecallProbability** hello 將欄位**值**區域。

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

按一下**格式**，選取**資料色彩**，並設定 hello **MaintenanceProbability**色彩 toohello 值**"F2C80F"**。

變更 hello**標題**hello 的圖表太**"機率的一種載具，維護及回收由 City"**。

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

按一下 hello 的空白區域 tooadd 新的視覺效果。

選取**區域圖**從視覺效果的視覺效果，從拖曳 hello**模型**欄位到 hello**軸**區域中，然後拖曳 hello **engineOil，tirepressure，速度和 MaintenanceProbability** hello 將欄位**值**區域。 變更其彙總類型太**「 平均數 」**。 

![Connected Cars - 變更彙總類型](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

變更 hello 圖表 hello 標題太**「 平均引擎石油，tire 不足的壓力、 速度以及維護機率模型 」**。

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

按一下 hello 的空白區域 tooadd 新的視覺效果：

1. 從 [視覺效果] 中選取「散佈圖」  視覺效果。
2. 拖曳 hello**模型**欄位到 hello**詳細資料**和**圖例**區域。
3. 拖曳 hello**燃料**欄位到 hello **x 軸**區域中，也變更 hello 彙總**平均**。
4. 拖曳**engineTemparature**到**y 軸區域**，也變更 hello 彙總**平均**
5. 拖曳 hello **vin**欄位到 hello**大小**區域。

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

變更 hello 圖表**標題**太**"燃料的平均值，模型的引擎溫度"**。

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

hello 最終報表看起來類似，如下所示。

![Connected Cars - 最終報告](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>從 hello 報表 toohello 即時儀表板釘選視覺效果
建立空白的儀表板上 hello 加號圖示的 下一步 tooDashboards 即可。 您可以將它命名為「車輛遙測分析儀表板」

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

從報表 toohello 儀表板上方的 hello hello 釘選視覺效果。 

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

hello 儀表板應該看起來像這樣當所有三個報表都是建立的 hello 和 hello 對應的視覺效果釘選的 toohello 儀表板。 如果您沒有建立 hello 的所有報表，您的儀表板看起來可能不同。 

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

恭喜！ 您已成功建立 hello 即時儀表板。 當您繼續 tooexecute CarEventGenerator.exe 和 RealtimeDashboardApp.exe，您應該看到 hello 儀表板上的即時更新。 它應該採取下列步驟大約 10 個 too15 分鐘 toocomplete hello。

## <a name="setup-power-bi-batch-processing-dashboard"></a>設定 Power BI 批次處理儀表板
> [!NOTE]
> 它需要約兩小時的時間 （從 hello 部署的 hello 成功完成） hello 結束 tooend 批次處理管線 toofinish 執行並處理過去年度產生的資料。 因此等候 hello 處理 toofinish hello 接下來的步驟繼續執行。 
> 
> 

**下載 hello Power BI 設計工具檔案**

* 建立預先設定的 Power BI 設計工具的檔案是包含在 hello 部署手動操作說明
* 尋找 2. 安裝程式 PowerBI 批次處理儀表板，您可以下載此呼叫的批次處理儀表板的 hello PowerBI 範本**ConnectedCarsPbiReport.pbix**。
* 儲存在本機

**設定 Power BI 報告**

* 開啟 hello 設計工具檔案 '**ConnectedCarsPbiReport.pbix**' 使用 Power BI Desktop。 如果您沒有已有，安裝 hello 從 Power BI Desktop [Power BI Desktop 安裝](http://www.microsoft.com/download/details.aspx?id=45331)。 
* 按一下 hello**編輯查詢**。

![編輯 Power BI 查詢](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* 按兩下 hello**來源**。

![設定 Power BI 來源](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* 收到 hello 部署的一部分佈建的 hello Azure SQL server 更新伺服器的連接字串。  查詢 底下的 hello 手動操作說明 

    4. Azure SQL Database
    
    * 伺服器︰somethingsrv.database.windows.net
    * 資料庫︰connectedcar
    * 使用者名稱︰使用者名稱
    * 密碼︰ 您可以從 Azure 入口網站管理您的 SQL 伺服器密碼

* 將 [資料庫]  保留為 *connectedcar*。

![設定 Power BI 資料庫](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* 按一下 [確定] 。
* 您會看到**Windows 認證**預設選取索引標籤，變更太**資料庫認證**上的 **資料庫**右邊索引標籤。
* 提供 hello **Username**和**密碼**其部署安裝期間指定您 Azure SQL database。

![提供資料庫認證](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* 按一下 [連接] 
* 針對每個 hello 三個剩餘查詢出現在右窗格中，重複上述步驟 hello，然後更新 hello 資料來源連接的詳細資料。
* 按一下 [關閉並載入] 。 Power BI Desktop 檔案的資料集是已連線的 tooSQL Azure 資料庫的資料表。
* **關閉** Power BI Desktop 檔案。

![關閉 Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* 按一下**儲存**按鈕 toosave hello 變更。 

您現在已設定對應 toohello 批次處理路徑 hello 方案中的所有 hello 報表。 

## <a name="upload-toopowerbicom"></a>上傳太*powerbi.com*
1. 瀏覽 toohello http://powerbi.com 以及登入 Power BI web 入口網站。
2. 按一下 [取得資料]   
3. 上傳 hello Power BI Desktop 檔案。  
4. tooupload，按一下 **取得資料-> 檔案-> 本機檔案**  
5. 瀏覽 toohello **"**ConnectedCarsPbiReport.pbix**"**  
6. 一旦上傳 hello 檔案時，會巡覽後 tooyour Power BI 工作空間。  

將會為您建立資料集、報告和空白儀表板。  

釘選圖呼叫 tooa 新儀表板**Vehicle 遙測分析儀表板**中**Power BI**。 按一下上面建立 hello 空白儀表板，然後瀏覽 toohello**報表**區段中，按一下 hello 新上傳報表。  

![車輛遙測 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**請注意 hello 報表有六個頁面：**  
第 1 頁︰車輛密度  
第 2 頁︰即時車輛健全狀況  
第 3 頁︰危險駕駛的車輛   
第 4 頁︰召回的車輛  
第 5 頁︰省油的車輛  
第 6 頁︰Contoso 標誌  

![連接的車輛 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**從第 3 頁**，釘選 hello 下列：  

1. VIN 的計數  
   ![連接的車輛 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. 危險駕駛的車輛 (依車型) – 瀑布圖   
   ![車輛遙測 - 釘選圖表 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**從第 5 頁**，釘選 hello 下列： 

1. vin 的計數    
   ![車輛遙測 - 釘選圖表 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. 省油的車輛 (依車型)：群組直條圖   
   ![車輛遙測 - 釘選圖表 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**從第 4 頁**，釘選 hello 下列：  

1. vin 的計數  
   ![車輛遙測 - 釘選圖表 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. 召回的車輛 (依城市、車型)：樹狀圖   
   ![車輛遙測 - 釘選圖表 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**從第 6 頁**，釘選 hello 下列：  

1. Contoso Motors 標誌   
   ![車輛遙測 - 釘選圖表 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**組織 hello 儀表板**  

1. 瀏覽 toohello 儀表板
2. 將滑鼠停留在每個圖表，並將它會根據 hello 命名重新命名圖的 hello 完整儀表板中提供。 也會移動 hello 圖表周圍 toolook 像 hello 儀表板下方。  
   ![車輛遙測 - 組織儀表板 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![車輛遙測 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. 如果您已建立所有 hello 報告這份文件中所述，hello 最後完成的儀表板看起來應該像 hello 遵循圖。 

![車輛遙測 - 組織儀表板 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

恭喜！ 您已成功建立 hello 報告和 hello 儀表板 toogain 即時、 預測及批次的洞察能力 vehicle 健全狀況和驅動習慣。  
