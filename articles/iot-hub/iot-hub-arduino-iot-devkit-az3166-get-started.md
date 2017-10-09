---
title: "aaaIoT DevKit toocloud 連接 IoT DevKit AZ3166 tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接它 IoT DevKit AZ3166 tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>連接 IoT DevKit AZ3166 tooAzure hello 雲端中的 IoT 中樞

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/)可以是使用的 toodevelop 和原型的物聯網 (IoT) 解決方案，並運用 Microsoft Azure 服務。 其包含具有豐富週邊設備與感應器的 Arduino 相容面板、開放原始碼面板封裝，以及不斷擴展的[專案目錄](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/)。

## <a name="what-you-do"></a>您要做什麼
連接[DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT 中樞您建立時，收集 hello 氣溫和溼度資料從感應器和傳送嗨資料 tooIoT 中樞。

還沒有 DevKit 嗎？ 在[這裡](https://aka.ms/iot-devkit-purchase)取得新的 DevKit。

## <a name="what-you-learn"></a>您學到什麼

* 如何 tooconnect IoT DevKit tooWireless 存取點，並準備您的開發環境。
* 如何 toocreate IoT 中樞和 MXChip IoT DevKit 如註冊裝置。
* 如何執行範例應用程式上 MXChip IoT DevKit toocollect 感應器資料。
* 如何 toosend hello 感應器資料 tooyour IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

* 使用 Micro USB 纜線的 MXChip IoT DevKit 面板。 [立即取得](https://aka.ms/iot-devkit-purchase)
* 執行 Windows 10 或 macOS 10.10+ 的電腦
* 作用中的 Azure 訂用帳戶
  * 啟動 [30 天免費試用 Microsoft Azure 帳戶](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>準備硬體

連結 hello 硬體 tooyour 電腦。

### <a name="hardware-you-need"></a>您需要的硬體

* DevKit 面板
* Micro USB 纜線

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>DevKit tooyour 電腦連線

1. 連接 USB 結束 tooyour PC
2. 連接微 USB 結束 toohello DevKit
3. hello 綠色 LED 下一步 toopower 確認連接

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>設定 WiFi

IoT 專案依賴網際網路連線。 使用下列指示 tooconfigure hello DevKit tooconnect tooWiFi hello。

### <a name="enter-ap-mode"></a>進入 AP 模式

按住按鈕 B，然後推送釋放 hello 重設 按鈕，然後按一下 發行 按鈕 b。您 DevKit 會進入 AP 模式 WiFi 的設定。 囉 」 畫面會顯示服務的 hello DevKit 設定 Identifier(SSID) hello 與 hello 設定入口網站的 IP 位址：

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>連接 tooDevKit AP

現在，使用另一個 WiFi 啟用裝置 （PC 或行動電話） tooconnect toohello DevKit SSID （hello 上方螢幕擷取畫面中反白顯示），將 hello 密碼保持空白。

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>為 DevKit 設定 WiFi

選取您想，hello DevKit tooconnect hello WiFi 網路開啟 hello PC 或行動電話瀏覽器中的 hello DevKit 螢幕上顯示的 IP 位址，然後輸入 hello 密碼。 按一下**連接**toocomplete:

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Hello 連接成功後，hello DevKit 會在幾秒鐘的時間重新開機。 如果成功，您會看到囉 」 畫面上的 hello WiFi 名稱和 IP 位址：

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
顯示 hello 相片中的 hello IP 位址可能不符合實際 hello IP 指派和 hello DevKit 螢幕上顯示。 這是正常現象 WiFi 使用 DHCP toodynamically 指派 Ip。

WiFi 設定之後，您的認證會保留該連接的 hello 裝置上，即使已拔除。 例如，如果您在家中設定 WiFi hello DevKit，然後 hello DevKit toohello office，您必須 tooreconfigure AP 模式 (開始步驟**輸入 AP 模式**) tooconnect hello DevKit tooyour office WiFi。 

## <a name="start-using-devkit"></a>開始使用 DevKit

hello DevKit 上執行的預設應用程式會檢查 hello 韌體 hello 最新版本，並顯示您的某些感應器診斷資料。

### <a name="upgrade-toohello-latest-firmware"></a>升級 toohello 最新的韌體

系統將提示同時 hello 目前和最新的韌體版本，如果沒有升級所需的 hello 螢幕上。 請遵循[升級韌體](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/)引導 tooupgrade 它。

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
這是一次性的一旦您啟動 hello DevKit 上進行開發上, 傳您的應用程式，您將有 hello 最新的韌體，隨附於您的應用程式。

### <a name="test-various-sensors"></a>測試各種感應器

按下按鈕 B tootest 感應器、 繼續按下並釋放 hello B 按鈕 toocycle 透過每個感應器。

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>準備開發環境

現在時間 tooset hello 開發環境： 工具和您 toobuild 令人驚豔的 IoT 應用程式的封裝。 您可以選擇 Windows 或 macOS 根據 tooyour 作業系統的版本。


### <a name="windows"></a>Windows

我們鼓勵您 toouse hello 安裝封裝 tooprepare hello 開發環境。 如果您遇到任何問題，您可以依照 hello[手動步驟](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/)tooget 完成工作。

#### <a name="download-latest-package"></a>下載最新的封裝

hello`.zip`您下載的檔案包含所有必要工具和所需的 DevKit 開發的封裝。

> [!div class="button"]
[下載](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> hello`.zip`檔案包含 hello 下列工具和封裝。 如果您已經有安裝某些元件時，會偵測到 hello 指令碼，並略過它們。
> * Node.js 和 Yarn: hello 安裝指令碼和自動化的工作的執行階段
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -跨平台命令列管理 Azure 資源，hello MSI 經驗包含相依的 Python 和 pip。
> * [Visual Studio Code](https://code.visualstudio.com/)：DevKit 開發的輕量型程式碼編輯器
> * [適用於 Arduino 的 Visual Studio Code 擴充功能](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino)：使用 VS Code 啟用 Arduino 開發
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): hello 副檔名 Arduino 依賴這項工具
> * DevKit 面板封裝： 工具鏈結、 程式庫和 hello DevKit 的專案
> * ST-Link 公用程式：基本公用程式與驅動程式

#### <a name="run-installation-script"></a>執行安裝指令碼

在 Windows 檔案總管 中，找出 hello`.zip`並將它解壓縮，尋找`install.cmd`，以滑鼠右鍵按一下並選取**以系統管理員身分執行** toostart。

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

在安裝期間，您會看到每個工具或封裝的 hello 進度。

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>確認 tooinstall 驅動程式

hello VS Code Arduino 擴充功能會依賴 hello Arduino IDE。 如果這是 hello 第一次安裝 hello Arduino IDE 時，您將會提示的 tooinstall 相關驅動程式：

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

會花費大約 10 分鐘 toofinish 安裝，視您的網際網路速度而定。 Hello 安裝完成之後，您應該在桌面上會看到 Visual Studio 程式碼和 Arduino IDE 快速鍵。

> [!NOTE] 
有時在您啟動 VS Code 時，系統會出現錯誤提示，指出找不到 Arduino IDE 或相關面板封裝。 關閉與程式碼，它一次啟動 IDE Arduino toosolve 和 VS 程式碼應該尋找 Arduino IDE 路徑正確。


### <a name="macos-preview"></a>macOS (預覽)

您可以依照這些步驟 tooprepare 開發環境上 macOS。

#### <a name="install-azure-cli-20"></a>安裝 Azure CLI 2.0

請遵循 hello[官方指南](https://docs.microsoft.com//cli/azure/install-azure-cli)tooinstall Azure CLI 2.0:

使用 `curl` 命令安裝 Azure CLI 2.0：

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

然後重新啟動您的命令殼層，變更 tootake 效果：

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>安裝 Arduino IDE

Visual Studio 程式碼 Arduino 延伸 hello 依賴 hello Arduino IDE。 下載並安裝 hello [macOS Arduino IDE](https://www.arduino.cc/en/Main/Software)。

#### <a name="install-visual-studio-code"></a>安裝 Visual Studio Code

下載並安裝[適用於 macOS 的 Visual Studio Code](https://code.visualstudio.com/)。 這會是 hello 建置 DevKit IoT 應用程式的主要開發工具。

####  <a name="download-latest-package"></a>下載最新的封裝

1. 安裝 Node.js。 您可以使用熱門 macOS 封裝管理員[Homebrew](https://brew.sh/)或[預先建立的安裝程式](https://nodejs.org/en/download/)tooinstall 它。

2. 下載 `.zip` 檔案，其包含使用 VS Code 開發 DevKit 所需之工作指令碼。

   > [!div class="button"]
   [下載](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   找出 hello`.zip`並將它解壓縮。 然後啟動**終端機**應用程式，並執行下列命令 tooconfigure 的 hello:

   移動已解壓縮的資料夾 tooyour macOS 使用者資料夾：
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   安裝 `npm` 封裝：
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>安裝適用於 Arduino 的 Visual Studio Code 擴充功能

Visual Studio 程式碼可讓您 tooinstall Marketplace 擴充功能直接在 hello 工具中，只要按一下 hello hello 功能表左的窗格中的擴充功能圖示，然後搜尋`Arduino`tooinstall:

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>安裝 DevKit 面板封裝

您必須使用 Visual Studio 程式碼中的 hello 面板管理員 tooadd hello DevKit 面板。

1. 使用`Cmd+Shift+P`tooinvoke 命令調色盤，然後輸入**Arduino**然後尋找並選取**Arduino： 面板管理員**。

2. 按一下**'其他 Url'**在 hello 右下方。
   ![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. 在 hello`settings.json`檔案中，於 hello 下方加入線條`USER SETTINGS`窗格並儲存。
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. 現在 hello 面板管理員中搜尋 'az3166'，安裝 hello 最新版本。
   ![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

現在您有所有必要工具的 hello macOS 為安裝的套件。


## <a name="open-project-folder"></a>開啟專案資料夾

### <a name="launch-vs-code"></a>啟動 VS Code

請確定 DevKit 未連線。 第一次啟動 VS Code 和 hello DevKit tooyour 電腦連線。 VS Code 會自動尋找它，並快顯簡介頁面：

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
有時候在您啟動 VS Code 時，系統會出現錯誤提示，指明找不到 Arduino IDE 或相關面板封裝。 關閉 VS 程式碼，它一次重新啟動 Arduino IDE toosolve 和 VS 程式碼應該尋找 Arduino IDE 路徑正確。

### <a name="open-arduino-examples-folder"></a>開啟 Arduino 範例資料夾

切換太**'Arduino 範例'**索引標籤上，瀏覽過`Examples for MXCHIP AZ3166 > AzureIoT`，然後按一下  `GetStarted`。

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

如果您遇到 tooclose hello 窗格中，tooreload 它使用`Ctrl+Shift+P`(macOS: `Cmd+Shift+P`) tooinvoke 命令調色盤，然後輸入**Arduino** toofind 選取**Arduino： 範例**。

## <a name="provision-azure-services"></a>佈建 Azure 服務

在 hello 方案視窗中，執行您的工作`Ctrl+P`(macOS: `Cmd+P`) 輸入 'task 雲端佈建':

在 hello VS Code 終端機，互動式的命令列將引導您完成佈建 hello 所需的 Azure 服務：

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>組建並上傳 Arduino 草圖

### <a name="install-required-library"></a>安裝必要的程式庫

1. 按`F1`或`Ctrl+Shift+P`(macOS: `Cmd+Shift+P`) tooinvoke 命令調色盤，然後輸入**Arduino**然後尋找並選取**Arduino： 程式庫管理員**。

2. 搜尋 `ArduinoJson` 程式庫，然後按一下 [安裝]

### <a name="build-and-upload-hello-device-code"></a>建置並上傳 hello 裝置程式碼

使用`Ctrl+P`(macOS: `Cmd+P`) toorun ' 工作的裝置上傳 '。 終端機 hello 會提示您 tooenter 組態模式。 toodo，按住按鈕，然後推播和發行 hello 重設 按鈕。 囉 」 畫面會顯示 「 設定 」。 這是擷取自 '任務雲端佈建' 步驟 tooset hello 連接字串。

然後就會開始驗證和上傳 hello Arduino 草圖：

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

hello DevKit 會重新啟動並開始執行 hello 程式碼。

## <a name="test-hello-project"></a>測試 hello 專案

在 VS 程式碼中，按一下 hello 電源插頭圖示 hello 狀態列 tooopen hello 序列的監視器上。

hello 範例應用程式時您會看到下列結果 hello 順利執行：

* hello 序列的監視器顯示 hello 以下 hello 螢幕擷取畫面中的 hello 內容相同的資訊。
* hello MXChip IoT DevKit 上的 LED 閃爍不停。

![VS Code 的最終輸出](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>問題與意見反應

您可以找到[常見問題集](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/)如果遇到問題，或是聯繫 toous hello 通道下方。

## <a name="next-steps"></a>後續步驟

已成功連接 MXChip IoT DevKit tooyour IoT 中樞，並傳送的嗨擷取感應器資料 tooyour IoT 中樞。

使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：

- [透過 iothub-explorer 管理雲端裝置傳訊](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [儲存 IoT 中樞訊息 tooAzure 資料存放區](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [使用 Power BI toovisualize 即時感應器資料從 Azure IoT 中樞](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [使用 Azure Web Apps toovisualize 即時感應器資料從 Azure IoT 中樞](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Azure Machine Learning 中使用 IoT 中樞的 hello 感應器資料的氣象預報預測](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [透過 iothub-explorer進行裝置管理](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [搭配 Logic Apps 進行遠端監視和通知](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)