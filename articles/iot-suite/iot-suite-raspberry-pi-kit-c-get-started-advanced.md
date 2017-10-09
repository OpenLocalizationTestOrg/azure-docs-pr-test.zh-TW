---
title: "aaaConnect 覆盆子 Pi tooAzure IoT 套件使用 C toosupport 韌體更新 |Microsoft 文件"
description: "使用 hello 覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件 hello 和 Azure IoT 套件。 使用 C tooconnect 遠端監視解決方案程式覆盆子 Pi toohello、 感應器從傳送遙測 toohello 雲端，並執行遠端軔體更新。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>連接遠端監視解決方案程式覆盆子 Pi 3 toohello 並啟用遠端韌體更新使用 C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

本教學課程會示範如何 toouse hello 至覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件：

* 開發氣溫和溼度的讀取器可與 hello 雲端通訊。
* 啟用及執行遠端韌體更新 tooupdate hello 用戶端應用程式上 hello 覆盆子 Pi。

hello 教學課程使用：

* Raspbian OS、 hello C 程式設計語言和為 C tooimplement 範例裝置 hello Microsoft Azure IoT SDK。
* hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。

## <a name="overview"></a>概觀

在本教學課程中，您完成下列步驟的 hello:

* 部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。 這個步驟會自動部署並設定多個 Azure 服務。
* 設定您的電腦與 hello 與您的裝置與感應器 toocommunicate 遠端監視解決方案。
* 更新 hello 範例裝置的程式碼 tooconnect toohello 遠端監視解決方案，並傳送嗨方案儀表板，您可以檢視的遙測。
* 使用 hello 範例裝置的程式碼 tooupdate hello 用戶端應用程式。

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。 hello 部署會反映實際的企業架構。 當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。 如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。 減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>下載及設定 hello 範例

現在，您可以下載並設定覆盆子 pi hello 遠端監視用戶端應用程式。

### <a name="clone-hello-repositories"></a>複製 hello 儲存機制

如果還沒有這麼做，複製 hello 所需執行的儲存機制 hello 您 pi 下列命令：

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>更新 hello 裝置連接字串

開啟 hello 範例組態檔中 hello **nano**編輯器使用下列命令的 hello:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Hello 預留位置值 hello 裝置識別碼和 IoT 中樞資訊來取代您建立並儲存在本教學課程中的 hello 開頭。

當您完成之後時，hello hello deviceinfo 檔內容看起來應該像下列範例中的 hello:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

儲存您的變更 (**Ctrl-O**， **Enter**) 和結束 hello 編輯器 (**Ctrl X**)。

## <a name="build-hello-sample"></a>建立 hello 範例

如果您尚未這樣做，執行命令在終止後 hello 覆盆子 Pi hello hello hello Microsoft Azure IoT 裝置 SDK 的必要條件套件安裝 c:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

您現在可以在 hello 覆盆子 Pi 建置 hello 範例方案：

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

您現在可以在 hello 覆盆子 Pi 執行 hello 範例程式。 輸入 hello 命令：

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

hello 下列範例輸出是您 hello 覆盆子 Pi hello 命令提示字元下，請參閱 hello 輸出的範例：

![Raspberry Pi 應用程式的輸出][img-raspberry-output]

按**CTRL-C** tooexit hello 程式在任何時間。

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. 在 hello 方案儀表板中，按一下 **裝置**toovisit hello**裝置**頁面。 選取在 hello 覆盆子 Pi**裝置清單**。 然後選擇 [方法]：

    ![在儀表板中列出裝置][img-list-devices]

1. 在 hello**叫用方法**頁面上，選擇**InitiateFirmwareUpdate**在 hello**方法**下拉式清單。

1. 在 hello **FWPackageURI**欄位中，輸入**https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**。 這個封存檔案包含 hello hello 韌體版本 2.0 實作。

1. 選擇 [InvokeMethod]。 hello hello 覆盆子 Pi 上的應用程式傳送的通知後 toohello 方案儀表板。 接著它會啟動 hello 韌體更新程序下載新版 hello 韌體 hello:

    ![顯示方法歷程記錄][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>觀察 hello 韌體更新程序

您可以在 hello 裝置上執行，觀察 hello 韌體更新程序及檢視 hello 回報 hello 方案儀表板中的屬性：

1. 您可以檢視 hello 覆盆子 Pi hello 正在進行中的 hello 更新程序：

    ![顯示更新進度][img-update-progress]

    > [!NOTE]
    > hello 遠端監視應用程式會重新啟動以無訊息模式，hello 更新完成時。 使用 hello 命令`ps -ef`tooverify 它正在執行。 如果您想 tooterminate hello 程序，使用 hello`kill`命令與 hello 處理序識別碼。

1. Hello 方案入口網站中的 hello 裝置所報告，您可以檢視 hello 韌體更新，hello 狀態。 hello 下列螢幕擷取畫面顯示 hello 狀態和持續時間的 hello 更新程序，以及 hello 新的韌體版本每個階段：

    ![顯示作業狀態][img-job-status]

    如果您瀏覽後 toohello 儀表板，您可以確認 hello 裝置仍在傳送 hello 韌體更新之後的遙測。

> [!WARNING]
> 如果您離開 hello 遠端監視您的 Azure 帳戶中執行的解決方案，您所要支付 hello 次執行。 減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。 使用完畢時，請從您的 Azure 帳戶刪除 hello 預先設定的解決方案。

## <a name="next-steps"></a>後續步驟

請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md