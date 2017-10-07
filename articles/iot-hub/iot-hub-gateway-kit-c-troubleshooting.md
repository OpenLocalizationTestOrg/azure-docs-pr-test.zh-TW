---
title: "SensorTag 裝置與 Azure IoT 閘道 - 疑難排解 | Microsoft Docs"
description: "Intel NUC 閘道器的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 問題, 物聯網問題"
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>疑難排解

## <a name="hardware-issues"></a>硬體問題

### <a name="ti-sensortag-cannot-be-connected"></a>無法連線至 TI SensorTag

tootroubleshoot SensorTag 連線問題，使用 hello [SensorTag 應用程式](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide)。

### <a name="have-an-issue-with-intel-nuc"></a>Intel NUC 有問題

tootroubleshoot 開機問題，請參閱太[疑難排解 Intel NUC 否開機問題](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html)。

tootroubleshoot 作業系統問題，請參閱太[Intel NUC 上的作業系統問題的疑難排解](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html)。

tootroubleshoot 其他問題，請參閱太[閃爍的代碼和發出嗶聲代碼 Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html)。

## <a name="nodejs-package-issues"></a>Node.js 套件問題

### <a name="no-response-during-gulp-tasks"></a>gulp 工作期間沒有回應

如果您遇到中執行的 gulp 工作的問題，您可以加入 hello`--verbose`偵錯的選項。 嘗試使用目前 gulp 工作 tooterminate `Ctrl + C`，然後執行的 hello 遵從在主控台視窗 toosee 偵錯訊息中的命令。 您可能會在主控台輸出中看到詳細的錯誤訊息。

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>裝置探索問題

如需協助疑難排解常見問題 hello`discover-sensortag`命令，檢查 hello [wiki 頁面](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl)。

### <a name="npm-issues"></a>npm 問題

嘗試執行下列命令的 hello tooupdate npm 封裝：

```bash
npm install -g npm
```

如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started)。

## <a name="remote-debugging"></a>遠端偵錯
> 下面的指示是用於針對本教學課程中使用的 node.js 指令碼偵錯。
### <a name="run-hello-sample-application-in-debug-mode"></a>偵錯模式執行 hello 範例應用程式

藉由執行下列命令的 hello 偵錯模式執行 hello 範例應用程式：

```bash
gulp run --debug
```

Hello 偵錯引擎就緒時，您應該會看到`Debugger listening on port 5858`hello 主控台輸出中。

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>設定 Visual Studio Code tooconnect toohello 遠端裝置

1. 開啟 hello**偵錯**hello 左側面板。
2. 按一下綠色的 hello**開始偵錯**(F5) 按鈕。 Visual Studio Code 會開啟 `launch.json` 檔案。
3. 更新 hello`launch.json`以 hello 內容之後的檔案。 取代`[device hostname or IP address]`hello 實際裝置 IP 位址或主機名稱。

   ``` json
   {
     "version": "0.2.0",
     "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![遠端偵錯組態](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>附加 toohello 遠端應用程式

按一下綠色的 hello**開始偵錯**偵錯 (F5) 按鈕 toostart。

讀取[VS 程式碼中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 更多關於 hello 偵錯工具。

![偵錯 BLE 範例](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Azure CLI 問題

hello Azure 命令列介面 (Azure CLI) 是預覽版。 tooseek 解決方案，您可以使用 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)。

如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。

疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。

如果您符合 「 找不到滿足 hello 需求的版本 」，請執行的 hello 下列的命令 tooupgrade pip toolastest 版本。

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python 安裝問題

### <a name="legacy-installation-issues-macos"></a>舊版安裝問題 (macOS)

安裝 pip 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。 之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。 從先前的安裝某些 pip 封裝所建立的根，會導致 hello 權限錯誤。 hello 方案是 tooremove 由根安裝這些套件。 使用下列步驟 toocomplete hello 這項工作：

1. 跳過`/usr/local/lib/python2.7/site-packages`
2. 列出根目錄建立的套件：`ls -l | grep root`
3. 從步驟 2 解除安裝套件：`sudo rm -rf {package name}`
4. 重新安裝 Python。

## <a name="azure-iot-hub-issues"></a>Azure IoT 中樞問題

如果您已成功佈建您的 Azure IoT 中樞與 hello Azure CLI 需要工具 toomanage hello 裝置 tooyour IoT 中樞連線，請再試一次 hello 下列工具。

### <a name="device-explorer"></a>裝置總管

[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)Windows 本機電腦上執行並連接在 Azure 中的 tooyour IoT 中樞。 它會與 hello 下列通訊[IoT 中樞端點](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- 裝置身分識別管理 tooprovision 和管理裝置與 IoT 中樞註冊。
- 接收裝置到雲端，所以您可以監視從您的裝置 tooyour IoT 中樞傳送的訊息。
- 傳送雲端到裝置，因此您可以傳送訊息 tooyour 裝置從 IoT 中樞。

設定您的 IoT 中樞連接字串，此工具 toouse 內所有其功能。

### <a name="iothub-explorer"></a>iothub-explorer

[iot 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具 toomanage 裝置用戶端。 您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置命令。

tooinstall hello 最新 （發行前版本） 版本的 hello iot 中樞總管工具，執行下列命令的 hello:

```bash
npm install -g iothub-explorer@latest
```

tooget 所有相關的其他說明 hello iot 中樞總管命令和它們的參數，請執行下列命令的 hello:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>hello Azure 入口網站

完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。 您也可以 toouse hello [Azure 入口網站](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/)toohelp 佈建、 管理和偵錯您的 Azure 資源。

## <a name="azure-storage-issues"></a>Azure 儲存體問題

[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com/)是獨立應用程式，microsoft 可讓您 toowork Windows、 macOS 和 Linux 的 Azure 儲存體資料。 使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。 您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。
