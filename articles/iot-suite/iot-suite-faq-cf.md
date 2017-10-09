---
title: "aaaAzure IoT 套件連線 factory 常見問題集 |Microsoft 文件"
description: "IoT 套件連線處理站的常見問題集"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>IoT 套件連線處理站預先設定之解決方案的常見問題集

另請參閱、 hello 一般[常見問題集](iot-suite-faq.md)IoT 套件。

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>可以在哪裡找到 hello 原始程式碼 hello 預先設定的解決方案？

hello 原始程式碼儲存在 hello 遵循 GitHub 儲存機制：

* [連線處理站預先設定的解決方案](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>什麼是 OPC UA？

2008 年推出的 OPC 統一架構 (UA) 是各平台通用的服務導向互通性標準。 OPC UA 由各種工業系統和裝置使用，例如產業 PC、PLC 和感應器。 OPC UA 會具有內建的安全性，將 hello 傳統 OPC 規格 hello 功能整合到一種可擴充架構。 它是一種標準，由 hello OPC Foundation 所驅動。 hello [OPC Foundation](http://opcfoundation.org/) not 的收益組織具有多個 440 成員。 hello hello 組織目標是 toouse OPC 規格 toofacilitate 多個廠商、 多平台、 安全和可靠的互通性透過：

* 基礎結構
* 規格
* Technology
* 處理序

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>為何沒有 Microsoft 選擇 hello 的 OPC UA 連接工廠預先設定的解決方案？

Microsoft 選擇 OPC UA 的原因是它是一種開放式、非專屬、與平台無關、業界認同且已核准的標準。 它是 Industrie 4.0 (RAMI4.0) 參考架構解決方案的必要項目，以確保一組廣泛製造程序與設備之間的互通性。 Microsoft 會看到從我們的客戶 toobuild Industrie 4.0 解決方案的需求。 OPC UA 支援可協助客戶 tooachieve 低 hello 阻礙其目標，並提供即時商務值 toothem。

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>如何新增公用 IP 位址 toohello 模擬 VM？

您有兩個選項 tooadd hello IP 位址：

* 使用 hello PowerShell 指令碼`Simulation/Factory/Add-SimulationPublicIp.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。 傳遞您的部署名稱做為參數。 對於本機部署，請使用 `<your username>ConnFactoryLocal`。 hello 指令碼會列印出 hello 的 hello VM 的 IP 位址。

* 在 hello Azure 入口網站，找出您的部署的 hello 資源群組。 除了本機部署，您指定做為方案的 hello 名稱或部署名稱已 hello 資源群組。 Hello hello 資源群組名稱是使用 hello 組建指令碼的本機部署， `<your username>ConnFactoryLocal`。 現在，加入新**公用 IP 位址**toohello 資源群組。

> [!NOTE]
> 在任一情況下，請確定您遵循 hello hello 指示安裝 hello 最新修補程式[Ubuntu 網站](https://wiki.ubuntu.com/Security/Upgrades)。 只要您的 VM 可透過公用 IP 位址存取保留的 toodate 向上 hello 安裝。

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>如何移除 hello 公用 IP 位址 toohello 模擬 VM？

您有兩個選項 tooremove hello IP 位址：

* 使用 PowerShell 指令碼的 hello Simulation/Factory/Remove-SimulationPublicIp.ps1 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。 傳遞您的部署名稱做為參數。 對於本機部署，請使用 `<your username>ConnFactoryLocal`。 hello 指令碼會列印出 hello 的 hello VM 的 IP 位址。

* 在 hello Azure 入口網站，找出您的部署的 hello 資源群組。 除了本機部署，您指定做為方案的 hello 名稱或部署名稱已 hello 資源群組。 Hello hello 資源群組名稱是使用 hello 組建指令碼的本機部署， `<your username>ConnFactoryLocal`。 立即移除 hello**公用 IP 位址**hello 資源群組中的資源。

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>我要如何登入 toohello 模擬 VM？

如果您已部署您的方案使用 hello PowerShell 指令碼登入 toohello 模擬 VM 則僅支援`build.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。

如果您部署從 www.azureiotsuite.com hello 方案，您無法登入 toohello VM。 您無法登入，因為 hello 密碼會隨機產生且無法重設。

1. 新增公用 IP 位址 toohello VM。 請參閱[如何新增公用 IP 位址 toohello 模擬 VM？](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. 建立 VM 的 SSH 工作階段 tooyour 使用 hello 的 hello VM 的 IP 位址。
1. hello username toouse 是： `docker`。
1. hello 密碼 toouse 取決於您使用 toodeploy 的 hello 版本：
    * 對於 1 年 6 月 2017年之前使用 hello build.ps1 指令碼部署的解決方案，是 hello 密碼： `Passw0rd`。
    * 對於 1 年 6 月 2017年之後使用 hello build.ps1 指令碼部署的方案，您可以在 hello 找到 hello 密碼`<name of your deployment>.config.user`檔案。 hello 密碼儲存在 hello **VmAdminPassword**設定。 hello 密碼隨機產生的部署時除非您指定使用 hello`build.ps1`指令碼參數`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>如何停止和啟動所有的 docker 處理程序在 hello 模擬 VM？

1. 登入 toohello 模擬 VM。 請參閱[我要如何登入 toohello 模擬 VM？](#how-do-i-sign-in-to-the-simulation-vm)
1. toocheck 哪些容器是作用中，執行： `docker ps`。
1. toostop 所有模擬容器中，都執行： `./stopsimulation`。
1. toostart 模擬的所有容器：
    * 匯出介面變數與 hello 名稱**IOTHUB_CONNECTIONSTRING**。 使用 hello hello 值**IotHubOwnerConnectionString** hello 中設定`<name of your deployment>.config.user`檔案。 例如：

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * 執行 `./startsimulation`。

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>如何更新 hello VM 中的 hello 模擬？

如果您變更了任何 toohello 模擬，您可以使用 hello PowerShell 指令碼`build.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)使用 hello`updatedimulation`命令。 此指令碼組建所有的 hello 模擬元件、 停止 hello VM 中的 hello 模擬、 上傳、 安裝，並啟動它們。

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>我要如何找出 hello 的 hello IoT 中樞我的方案所使用的連接字串？

如果您部署您的方案以 hello `build.ps1` hello 中的指令碼[儲存機制](https://github.com/Azure/azure-iot-connected-factory)，hello 連接字串是 hello 值**IotHubOwnerConnectionString**在 hello`<name of your deployment>.config.user`檔案。

您也可以尋找 hello 使用 hello Azure 入口網站的連接字串。 在 hello IoT 中樞資源部署的 hello 資源群組中，找出 hello 連接字串設定。

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>IoT 中樞裝置沒有 hello 連接的原廠模擬使用？

hello 的模擬自我註冊下列裝置 hello:

* proxy.beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.rio.corp.contoso
* proxy.seattle.corp.contoso
* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

使用 hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)或[iot 中樞總管](https://github.com/azure/iothub-explorer)工具，您可以檢查哪些裝置會向您的方案正在使用的 hello IoT 中樞。 toouse 這些工具，您需要 hello 連接字串 hello IoT 中樞部署中。

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>如何取得記錄資料從 hello 模擬元件？

Toolog 檔案中的 hello 模擬記錄資訊中的所有元件。 這些檔案可以在 hello VM hello 資料夾中找到`home/docker/Logs`。 tooretrieve hello 記錄檔，您可以使用 hello PowerShell 指令碼`Simulation/Factory/Get-SimulationLogs.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。

這個指令碼需要 toosign toohello VM 中。 您可能需要 tooprovide 認證 hello 登入。 請參閱[我要如何登入 toohello 模擬 VM？](#how-do-i-sign-in-to-the-simulation-vm) toofind hello 認證。

hello 指令碼加入/移除公用 IP 位址 toohello VM，如果還沒有其中一個，並將它移除。 hello 指令碼置於封存檔中的所有記錄檔，並下載 hello 封存 tooyour 開發工作站。

或者登入 toohello 透過 SSH 的 VM，並檢查 hello 記錄檔，在執行階段。

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>如何檢查資料 toohello 雲端時，是否要傳送嗨模擬？

以 hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)或 hello [iot 中樞總管](https://github.com/azure/iothub-explorer)工具，您可以檢查 hello 資料從特定裝置傳送 tooIoT 中樞。 toouse 這些工具，您需要 tooknow hello 連接字串 hello IoT 中樞部署中。 請參閱[如何找出 hello 的 hello IoT 中樞我的方案所使用的連接字串？](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

檢查傳送一個 hello 發行者裝置 hello 資料：

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

如果您不看到任何資料傳送 tooIoT 中樞時，就 hello 模擬的問題。 第一個步驟是分析中，您應該分析 hello hello 模擬元件記錄檔。 請參閱[如何取得記錄資料從 hello 模擬元件？](#how-can-i-get-log-data-from-the-simulation-components) 接下來，再試一次 toostop 和啟動 hello 模擬並如果仍然不沒有傳送任何資料，更新 hello 模擬完全。 請參閱[如何更新 hello VM 中的 hello 模擬？](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>後續步驟

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預測性維護預先設定的解決方案概觀](iot-suite-predictive-overview.md)
* [連線處理站預先設定的解決方案概觀](iot-suite-connected-factory-overview.md)
* [從 hello 接地 IoT 安全性](securing-iot-ground-up.md)
