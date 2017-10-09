---
title: "Connect Raspberry Pi (C) tooAzure IoT-疑難排解 |Microsoft 文件"
description: "疑難排解 hello 覆盆子 Pi Node.js 體驗的頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 問題, 物聯網問題"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>疑難排解
## <a name="hardware-issues"></a>硬體問題
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>hello 應用程式也會執行，但 hello LED 閃爍不
此問題，一律為相關的 toohardware 電路連線。 使用下列步驟 tooidentify 問題 hello:

1. 請檢查您已選擇正確的 hello **GPIO**在面板。 hello 兩個連接埠應**GPIO GND (Pin 6)**和**GPIO 04 (Pin 7)**。
2. 請檢查您的 LED hello 極性正確。 hello 長腳應該指出 hello**正數**，anode pin。
3. 使用 hello **3.3V 釘選**和**GND Pin**覆盆子 Pi 3 為基礎。 Pi 視為 hello DC 電源。 請檢查該 hello LED 可正常運作。

![LED 規格](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>其他硬體問題
如需解決常見的問題，在覆盆子 Pi 3 上的資訊，請參閱 hello[正式的疑難排解頁面](http://elinux.org/R-Pi_Troubleshooting)。

## <a name="nodejs-package-issues"></a>Node.js 套件問題
### <a name="no-response-during-gulp-tasks"></a>gulp 工作期間沒有回應
如果您遇到中執行的 gulp 工作的問題，您可以加入 hello`--verbose`偵錯的選項。 透過使用 Ctrl + C，嘗試使用 tooterminate 目前 gulp 工作，然後執行下列命令，在主控台視窗 toosee 偵錯訊息中的 hello。 您可能會在主控台輸出中看到詳細的錯誤訊息。

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>裝置探索問題
如需協助疑難排解常見問題 hello`devdisco`命令，檢查 hello[讀我檔案](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)。

### <a name="npm-issues"></a>npm 問題
嘗試使用下列命令的 hello tooupdate npm 封裝：

```bash
npm install -g npm
```

如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started)。

## <a name="remote-debugging"></a>遠端偵錯
### <a name="run-hello-sample-application-in-debug-mode"></a>偵錯模式執行 hello 範例應用程式
```bash
gulp run --debug
```

Hello 偵錯引擎就緒時，您應該會看到```Debugger listening on port 5858```hello 主控台輸出中。

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>設定 Visual Studio Code tooconnect toohello 遠端裝置
1. 開啟 hello**偵錯**hello 左側面板。
2. 按一下綠色的 hello**開始偵錯**(F5) 按鈕。 Visual Studio Code 會開啟 launch.json 檔案。
3. 更新內容之後的 hello hello launch.json 檔案。 取代`[device hostname or IP address]`hello 實際裝置 IP 位址或主機名稱。

> [!NOTE]
> toolearn 深入了解 hello Visual Studio 偵錯，請參閱太[偵錯 Visual Studio 程式碼](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes)。


```json
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
            "remoteRoot": null
        }
    ]
}
```

![遠端偵錯組態](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>附加 toohello 遠端應用程式
按一下綠色的 hello**開始偵錯**偵錯 (F5) 按鈕 toostart。

讀取[VS 程式碼中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 更多關於 hello 偵錯工具。

![遠端偵錯互動](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure CLI 問題
hello Azure 命令列介面 (Azure CLI) 是預覽版。 tooseek 解決方案，您可以使用 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)。

如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。

疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。

## <a name="python-installation-issues"></a>Python 安裝問題
### <a name="legacy-installation-issues-macos"></a>舊版安裝問題 (macOS)
安裝 pip 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。 之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。 從先前的安裝某些 pip 封裝所建立的根，會導致 hello 權限錯誤。 hello 方案是 tooremove 由根安裝這些套件。 使用下列步驟 toocomplete hello 這項工作：

1. 請移至：/usr/local/lib/python2.7/site-packages
2. 列出根目錄建立的套件：`ls -l | grep root`
3. 從步驟 2 解除安裝套件：`sudo rm -rf {package name}`
4. 重新安裝 Python。

## <a name="azure-iot-hub-issues"></a>Azure IoT 中樞問題
如果您已成功佈建您的 Azure IoT 中樞與 Azure CLI 需要工具 toomanage hello 裝置 tooyour IoT 中樞連線，請再試一次 hello 下列工具。

### <a name="device-explorer"></a>裝置總管
hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)工具 Windows 本機電腦上執行，並連接在 Azure 中的 tooyour IoT 中樞。 它會與 hello 下列通訊[IoT 中樞端點](iot-hub-devguide.md):


* *裝置身分識別管理*tooprovision 和管理裝置與 IoT 中樞註冊。
* *接收裝置到雲端*讓您監視從您的裝置 tooyour IoT 中樞傳送的訊息。
* *傳送雲端到裝置*讓您可以傳送訊息 tooyour 裝置從 IoT 中樞。

設定您的 IoT 中樞連接字串，此工具 toouse 內所有其功能。

### <a name="iothub-explorer"></a>iothub-explorer
[iot 中樞總管](https://github.com/Azure/iothub-explorer)toomanage 裝置是範例多平台 CLI 工具。 您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置訊息。

tooinstall hello 最新版本 （發行前版本） 的 hello iot 中樞總管工具，執行下列命令，命令列環境中的 hello:

```bash
npm install -g iothub-explorer@latest
```

您可以使用下列命令 tooget 所有相關的其他說明 hello iot 中樞總管命令和其參數的 hello:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure 入口網站
完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。 您也可以 toouse hello [Azure 入口網站](../azure-portal-overview.md)toohelp 佈建、 管理和偵錯您的 Azure 資源。

## <a name="azure-storage-issues"></a>Azure 儲存體問題
[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com)是獨立應用程式，microsoft 可讓您 toowork Windows、 macOS 和 Linux 的 Azure 儲存體資料。 使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。 您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。

