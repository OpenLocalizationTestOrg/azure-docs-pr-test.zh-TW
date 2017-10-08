---
title: "Azure IoT 套件 aaaCustomize 連接工廠 |Microsoft 文件"
description: "Hello toocustomize hello 行為連接處理站的方式描述預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>自訂 hello 從 OPC UA 伺服器所連接的原廠方案顯示資料

## <a name="introduction"></a>簡介

hello 連接的工廠方案彙總，並顯示 hello OPC UA 伺服器已連線的 toohello 方案的資料。 您可以瀏覽並傳送命令 toohello OPC UA 方案中的伺服器。 如需有關 OPC UA 的詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。

Hello 方案中的彙總資料的範例包括 hello 整體設備效率 (OEE) 和關鍵效能指標 (Kpi)，您可以在 hello factory、 線條與站台層級的 hello 儀表板中檢視。 hello 下列螢幕擷取畫面顯示 hello OEE 和 KPI 值 hello**組件**站，在**生產線 1**，在 hello**慕尼黑**factory:

![Hello 方案中的 OEE 和 KPI 值的範例][img-oee-kpi]

hello 方案可讓您 tooview 的詳細資訊，從特定資料的項目從 hello OPC UA 伺服器，稱為*電台*。 hello 下列螢幕擷取畫面顯示繪圖 hello 的製造的項目，從特定站台的數字：

![製造項目數的繪圖][img-manufactured-items]

如果您按一下某個 hello 圖形，您可以瀏覽 hello 資料進一步使用時間序列 Insights (TSI):

![使用 Time Series Insights 探索資料][img-tsi]

本文章說明：

- Hello 資料的方式進行可用 toohello 各種檢視 hello 方案中。
- 您可以自訂 hello 方式 hello 方案的方式顯示 hello 資料。

## <a name="data-sources"></a>資料來源

hello 連接的工廠方案顯示 hello OPC UA 伺服器已連線的 toohello 方案的資料。 hello 預設安裝包含數個執行的處理站模擬的 OPC UA 伺服器。 您可以新增您自己的 OPC UA 伺服器，[透過閘道連線][ lnk-connect-cf] tooyour 方案。

您可以瀏覽的已連接的 OPC UA 伺服器可以傳送 tooyour 方案 hello 儀表板中的 hello 資料項目：

1. 瀏覽 toohello**選取 OPC UA 伺服器**檢視：

    ![瀏覽 toohello 選取 OPC UA 伺服器檢視][img-select-server]

1. 選取伺服器，然後按一下 [Connect (連線)]。 按一下**繼續**hello 安全性警告出現時。

    > [!NOTE]
    > 這個警告只出現一次，每個伺服器，而且會建立 hello 方案儀表板與 hello 伺服器之間的信任關係。

1. 您現在即可以瀏覽 hello 資料項目 hello 伺服器可以傳送 toohello 方案。 傳送 toohello 方案的項目具有綠色的核取記號：

    ![發行的項目][img-published]

1. 如果您是*管理員*hello 在解決方案中，您可以選擇 toopublish 資料的項目 toomake hello 提供連接出廠解決方案。 身為管理員，您也可以變更 hello 值項目，並呼叫 hello OPC UA 伺服器中的方法。

## <a name="map-hello-data"></a>Hello 資料對應

hello 連接工廠方案對應，而彙總 hello 已發佈資料項目 hello OPC UA 伺服器 toohello 從各種檢視 hello 方案中。 hello 連接的工廠方案 tooyour Azure 帳戶時部署您佈建 hello 方案。 Hello 處理站的連線的 Visual Studio 方案中的 JSON 檔案會儲存此對應資訊。 您可以檢視和修改這個 hello 連線 factory Visual Studio 方案中的 JSON 組態檔。 您進行變更之後，您可以重新部署 hello 方案。

您可以使用 hello 設定檔：

- 編輯 hello 現有模擬處理站、 生產線條，以及站台。
- 從實際的 OPC UA 伺服器 toohello 方案連接的資料對應。

tooclone 副本 hello 連線 factory Visual Studio 方案，使用 hello 下列 git 命令：

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

hello 檔案**ContosoTopologyDescription.json**定義 hello hello OPC UA 伺服器資料從對應 hello 連接的工廠方案儀表板中的項目 toohello 檢視。 您可以找到這個組態檔中 hello **Contoso\Topology**資料夾中 hello **WebApp** hello Visual Studio 方案中的專案。

hello hello JSON 檔案的內容會組織成原廠生產線上及站台節點的階層。 此階層定義 hello 連接的工廠儀表板中的 hello 導覽階層。 Hello 階層之每個節點的值會決定顯示 hello 儀表板中的 hello 資訊。 例如，hello JSON 檔案包含 hello hello 慕尼黑 factory 的值：

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

hello 名稱、 描述和位置會出現在這個檢視表 hello 儀表板中：

![慕尼黑 hello 儀表板中的資料][img-munich]

每個工廠、生產線和工作站都有一個映像屬性。 您可以在 hello 找到這些 JPEG 檔案**Content\img**資料夾中 hello **WebApp**專案。 這些映像檔會顯示 hello 連接的工廠儀表板中。

每個站台包含數個定義 hello 從 hello OPC UA 對應資料項目的詳細的屬性。 Hello 下列各節將描述這些屬性：

### <a name="opcuri"></a>OpcUri

hello **OpcUri**值為 hello OPC UA 應用程式 URI 可唯一識別 hello OPC UA 伺服器。 例如，hello **OpcUri** hello 慕尼黑生產行 1 上的組件站看起來像 hello 下列值： **urn: scada2194:ua:munich:productionline0:assemblystation**。

您可以在 hello 方案儀表板中檢視 hello hello 連接 OPC UA 伺服器的 Uri:

![檢視 OPC UA 伺服器 URI][img-server-uris]

### <a name="simulation"></a>模擬

hello 資訊在 hello**模擬**節點是特定 toohello OPC UA 模擬執行 hello 的預設佈建的 OPC UA 伺服器。 它不會使用在實際的 OPC UA 伺服器上。

### <a name="kpi1-and-kpi2"></a>Kpi1 和 Kpi2

這些節點會描述如何從 hello 站的資料造成 toohello 兩個 KPI 值 hello 儀表板中。 在預設部署中，這些 KPI 值是每小時的單位及每小時的 kWh。 hello 方案計算 KPI 值層級 hello 的站台，並加以彙總在 hello 生產線和 factory 層級。

每個 KPI 都有最小值、最大值和目標值。 每個 KPI 值也可以定義警示 hello 連接工廠方案 tooperform 動作。 hello 下列程式碼片段顯示 hello 組件站台的 hello KPI 定義生產線上慕尼黑中為 1:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

hello 下列螢幕擷取畫面顯示 hello KPI 資料 hello 儀表板中。

![Hello 儀表板中的 KPI 資訊][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

hello **OpcNodes**節點識別 hello hello OPC UA 伺服器從已發佈的資料項目，並指定如何 tooprocess 該資料。

hello **NodeId**值識別 hello hello OPC UA 伺服器從特定的 OPC UA NodeID。 hello 生產線慕尼黑中為 1 的 hello 組件站中的第一個節點的值**ns = 2; 我 = 385**。 A **NodeId**值會指定從 hello OPC UA 伺服器與 hello hello 資料項目 tooread **SymbolicName** hello 儀表板中的使用者易記名稱 toouse 提供該資料。

Hello 下表中摘要說明每個節點相關聯的其他值：

| 值 | 說明 |
| ----- | ----------- |
| 相關性  | 此資料提供給 hello KPI 和 OEE 值。 |
| OpCode     | Hello 資料彙總方式。 |
| Units      | hello 單位 toouse hello 儀表板中。  |
| 可見    | Toodisplay 這中是否有值 hello 儀表板。 部分值使用於計算中而不會顯示。  |
| 最大值    | hello 最大值，會觸發警示 hello 儀表板中。 |
| MaximumAlertActions | 在回應 tooan 警示動作 tootake。 例如，傳送命令 tooa 站台。 |
| ConstValue | 使用於計算的常數值。 |

## <a name="deploy-hello-changes"></a>部署 hello 變更

當您完成之後變更 toohello **ContosoTopologyDescription.json**檔案中，您就必須重新部署 hello 連接工廠方案 tooyour Azure 帳戶。

hello **azure-iot-連線-原廠**儲存機制包括**build.ps1** PowerShell 指令碼，您可以使用 toorebuild 並部署 hello 方案。

## <a name="next-steps"></a>後續步驟

深入了解 hello 連接工廠預先設定方案的下列文章閱讀 hello:

* [連線處理站預先設定的解決方案逐步解說][lnk-rm-walkthrough]
* [為連線處理站部署閘道][lnk-connect-cf]
* [Hello azureiotsuite.com 網站的權限][lnk-permissions]
* [連線的處理站常見問題](iot-suite-faq-cf.md)
* [常見問題集][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md