---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 4 課： 疑難排解 |Microsoft 文件"
description: "Intel Edison Node.js 經驗的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 疑難排解"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>疑難排解
## <a name="hardware-issues"></a>硬體問題
如需解決 Intel Edison 中常見的問題資訊，請參閱 hello[正式的疑難排解頁面](https://software.intel.com/en-us/node/637974)。

## <a name="nodejs-package-issues"></a>Node.js 套件問題
### <a name="no-response-during-gulp-tasks"></a>gulp 工作期間沒有回應
如果您遇到執行 gulp 工作的問題，您可以新增 hello`--verbose`偵錯的選項。 嘗試使用目前 gulp 工作 tooterminate `Ctrl + C`，然後執行的 hello 遵從在主控台視窗 toosee 偵錯訊息中的命令。 您可能會在主控台輸出中看到詳細的錯誤訊息。 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>NPM 問題
請嘗試 tooupdate NPM 封裝以 hello 下列命令：

```bash
npm install -g npm
```

如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制][sample-repository]。

## <a name="remote-debugging"></a>遠端偵錯

### <a name="run-hello-sample-application-in-debug-mode"></a>偵錯模式執行 hello 範例應用程式

```bash
gulp run --debug
```

Hello 偵錯引擎準備就緒之後，您應該能夠 toosee ```Debugger listening on port 5858``` hello 主控台輸出。

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>設定 VS Code tooconnect toohello 遠端裝置

開啟 hello**偵錯**從 hello 左側面板。

按一下綠色的 hello**開始偵錯**(F5) 按鈕。 這樣會開啟 VS Code **launch.json**檔案，這需要 tooupdate。

更新 hello **launch.json**檔案以 hello 下列內容，取代`[device hostname or IP address]`hello 實際裝置 IP 位址或主機名稱。  

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

![遠端偵錯組態](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>附加 toohello 遠端應用程式

按一下綠色的 hello**開始偵錯**(F5) 按鈕並享受偵錯。

您可以閱讀[VS 程式碼中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 更多關於 hello 偵錯工具。

![遠端偵錯互動](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure-CLI 問題
hello Azure 命令列介面 (Azure CLI) 是預覽版。 尋找方案中 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)tooseek 解決方案。 當命令無法運作正常，再試一次 tooupgrade Azure cli toolatest 版本。

如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。

疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。

如果您符合 「 找不到滿足 hello 需求的版本 」，請執行的 hello 下列的命令 tooupgrade pip toolastest 版本。

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python 安裝問題
### <a name="legacy-installation-issues-macos"></a>舊版安裝問題 (macOS)
安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。 之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。 某些**pip**從先前的安裝封裝所建立的根，會導致 hello 權限錯誤。 hello 方案是 tooremove 由根安裝這些套件。 使用下列步驟 toocomplete hello 這項工作：

1. 請移至：/usr/local/lib/python2.7/site-packages
2. 列出根目錄建立的套件：`ls -l | grep root`
3. 從步驟 2 解除安裝套件：`sudo rm -rf {package name}`
4. 重新安裝 Python。

## <a name="azure-iot-hub-issues"></a>Azure IoT 中樞問題
如果您已成功佈建您的 Azure IoT 中樞與`azure-cli`，而且您需要連線 tooyour IoT 中樞，遵循工具再試一次 hello 工具 toomanage hello 裝置：

### <a name="device-explorer"></a>裝置總管
[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)Windows 本機電腦上執行並連接在 Azure 中的 tooyour IoT 中樞。 它會與 hello 下列通訊[IoT 中樞端點](iot-hub-devguide.md):

- _裝置身分識別管理_tooprovision 和管理裝置與 IoT 中樞註冊。
- _接收裝置到雲端_讓您監視從您的裝置 tooyour IoT 中樞傳送的訊息。
- _傳送雲端到裝置_讓您可以傳送訊息 tooyour 裝置從 IoT 中樞。

設定您`IoT hub connection string`這個工具 toouse 內所有其功能。

### <a name="iot-hub-explorer"></a>IoT 中樞總管
[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具 toomanage 裝置用戶端。 您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置命令。

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
[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com)是獨立的應用程式，您可以使用與 toowork microsoft [Azure 儲存體](https://azure.microsoft.com/en-us/services/storage/)Windows、 macOS 和 Linux 上的資料。 使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。 您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。

## <a name="next-steps"></a>後續步驟
此頁面只會包含 hello Intel Edison 套件的最常見的問題。 您也可以保留下註解 tooreport 問題，取得進一步的疑難排解。

請返回太[Intel Edison (Node.js) 快速入門](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started