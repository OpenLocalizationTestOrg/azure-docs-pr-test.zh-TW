---
title: "Azure IoT 邊緣的實體裝置 aaaUse |Microsoft 文件"
description: "如何 toouse 德州儀器 SensorTag 裝置 toosend 資料 tooan IoT 中樞透過 IoT 邊緣閘道覆盆子 Pi 3 在裝置上執行。 使用 Azure IoT 邊緣建置 hello 閘道。"
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>使用 Azure IoT 邊緣覆盆子 Pi tooforward 裝置到雲端訊息 tooIoT 中樞

這個逐步解說中的 hello[藍芽低能源範例][ lnk-ble-samplecode]為您示範如何 toouse [Azure IoT 邊緣][ lnk-sdk]至：

* 轉送裝置到雲端遙測 tooIoT 中樞，從實體裝置。
* 將命令路由傳送從 IoT 中樞 tooa 實體裝置。

本逐步解說涵蓋下列項目：

* **架構**: hello 藍芽低能源範例架構重要資訊。
* **建置並執行**: hello 步驟需要的 toobuild 和執行的 hello 範例。

## <a name="architecture"></a>架構

hello 逐步解說將示範如何 toobuild 和覆盆子 Pi 3 上執行的 IoT 邊緣閘道執行 Raspbian Linux。 hello 閘道是建置使用 IoT 邊緣。 hello 範例會使用德州儀器 SensorTag 藍芽低能源 (B) 裝置 toocollect 溫度資料。

當您執行 hello IoT 邊緣閘道它：

* 會使用 hello 藍芽低能源 (B) 通訊協定 tooa SensorTag 裝置連線。
* 連接 tooIoT 集線器使用 hello HTTP 通訊協定。
* 將遙測轉送從 hello SensorTag 裝置 tooIoT 中樞。
* 將命令路由傳送從 IoT 中樞 toohello SensorTag 裝置。

hello 閘道包含下列 IoT 邊緣模組 hello:

* A *b 模組*從 hello 裝置和傳送指令 toohello 裝置 b 裝置 tooreceive 溫度資料的介面。
* A *b 雲端 toodevice 模組*轉譯成 hello b 指示從 IoT 中樞傳送 JSON 訊息*b 模組*。
* A*記錄器模組*記錄所有閘道訊息 tooa 本機檔案。
* 「身分識別對應模組」  ，可在 BLE 裝置 MAC 位址與 Azure IoT 中樞裝置身分識別之間進行轉譯。
* *IoT 中樞模組*，上傳遙測資料 tooan IoT 中樞，並從 IoT 中樞接收裝置命令。
* A *b 印表機模組*，解譯遙測從 hello b 裝置，並列印格式化的資料 toohello 主控台 tooenable 疑難排解和偵錯。

### <a name="how-data-flows-through-hello-gateway"></a>資料如何流經 hello 閘道

hello 遵循區塊圖將說明 hello 遙測上載資料流程管線：

![遙測上傳閘道管線](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

hello 步驟的遙測資料的項目會從 b 裝置 tooIoT 中樞如下：

1. hello b 裝置會產生溫度範例，並將它傳送 hello 閘道中的藍芽 toohello b 模組。
1. hello b 模組收到 hello 範例，並將其發佈 toohello broker 以及 hello 裝置 hello MAC 位址。
1. hello 身分識別對應模組拾取此訊息，並使用到 IoT 中樞裝置身分識別的內部資料表 tootranslate hello hello 裝置的 MAC 位址。 IoT 中樞裝置身分識別是由裝置識別碼及裝置金鑰所組成。
1. hello 身分識別對應模組發佈新訊息，其中包含 hello 溫度範例資料，hello 裝置 hello 裝置識別碼及 hello 裝置機碼的 hello MAC 位址。
1. hello IoT 中樞模組接收這個新的訊息 （hello 身分識別對應模組所產生），並將其發佈 tooIoT 中樞。
1. hello 記錄器模組會記錄所有訊息從 hello broker tooa 本機檔案。

hello 遵循區塊圖將說明 hello 裝置命令資料流程管線：

![裝置命令閘道管線](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. hello 模組會定期輪詢的 IoT 中樞 hello IoT 中樞的新命令訊息。
1. 當 hello IoT 中樞模組收到新的命令訊息時，它將其發佈 toohello broker。
1. hello 身分識別對應模組收到 hello 命令訊息，且使用的內部資料表 tootranslate hello IoT Hub 裝置識別碼 tooa 裝置 MAC 位址。 接著將發佈新訊息，其中包含 hello 訊息 hello 屬性對應中的 hello 目標裝置 hello MAC 位址。
1. hello b 雲端到裝置單元拾取此訊息，並將它轉譯成 hello b 模組 hello 適當 b 指令。 接著將發佈新訊息。
1. hello b 單元拾取此訊息，並執行 hello I/O 指令與 hello b 裝置通訊。
1. hello 記錄器模組會記錄所有訊息從 hello broker tooa 磁碟檔案。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。

> [!NOTE]
> 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。

需要 SSH 用戶端上您 tooremotely 存取 hello 命令列 hello 覆盆子 Pi 您桌面的電腦 tooenable。

- Windows 不包含 SSH 用戶端。 我們建議使用 [PuTTY](http://www.putty.org/)。
- 多數 Linux 散發套件和 Mac OS 包含 hello 命令列 SSH 公用程式。 如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。

## <a name="prepare-your-hardware"></a>準備硬體

本教學課程假設您正在使用[德州儀器 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html)裝置連線 tooa 覆盆子 Pi 3 執行 Raspbian。

### <a name="install-raspbian"></a>安裝 Raspbian

您可以使用其中一個 hello 遵循選項 tooinstall Raspbian 覆盆子 Pi 3 裝置。

* tooinstall hello 最新版本的 Raspbian，使用 hello [NOOBS] [ lnk-noobs]圖形化使用者介面。
* 手動[下載][ lnk-raspbian]和寫入 hello hello Raspbian 作業系統 tooan SD 卡的最新映像。

### <a name="sign-in-and-access-hello-terminal"></a>登入及存取 hello 終端機

您有兩個選項 tooaccess 終端機環境覆盆子 Pi 上：

* 如果您有鍵盤，監視連線的 tooyour 覆盆子 Pi，您可以使用 hello Raspbian GUI tooaccess 終端機視窗。

* 從您桌面的電腦使用 SSH 您覆盆子 pi hello 命令列存取。

#### <a name="use-a-terminal-window-in-hello-gui"></a>在 hello GUI 中的終端機視窗

Raspbian hello 預設認證是使用者名稱**pi**和密碼**覆盆子**。 您可以在 hello 工作列 hello GUI 中，啟動 hello**終端機**使用 hello 圖示看起來像監視器公用程式。

#### <a name="sign-in-with-ssh"></a>使用 SSH 登入

您可以使用 SSH 的命令列存取 tooyour 覆盆子 Pi。 hello 文章[SSH (Secure Shell)] [ lnk-pi-ssh]描述如何 tooconfigure SSH 您覆盆子 pi，以及如何從 tooconnect [Windows] [ lnk-ssh-windows]或[Linux 和 Mac OS][lnk-ssh-linux]。

以使用者名稱 **pi** 和密碼 **raspberry** 登入。

### <a name="install-bluez-537"></a>安裝 BlueZ 5.37

hello b 模組討論 toohello 藍芽硬體透過 hello BlueZ 堆疊。 正確的 hello 模組 toowork 需要 BlueZ 5.37 版本。 這些指示請確定已安裝的 BlueZ hello 正確版本。

1. 停止目前藍芽精靈 hello:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. 安裝 hello BlueZ 相依項目：

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. 從 bluez.org 下載 hello BlueZ 原始程式碼：

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. 解壓縮 hello 原始程式碼：

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. 變更目錄 toohello 新建立的資料夾：

    ```sh
    cd bluez-5.37
    ```

1. 設定建置 hello BlueZ 程式碼 toobe:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. 建置 BlueZ：

    ```sh
    make
    ```

1. 完成建置後安裝 BlueZ：

    ```sh
    sudo make install
    ```

1. 變更 systemd 服務組態，讓它所指 toohello 新藍芽精靈 hello 檔案中的藍芽`/lib/systemd/system/bluetooth.service`。 Hello 'ExecStart' 行取代成下列文字的 hello:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>啟用從覆盆子 Pi 3 裝置連線 toohello SensorTag 裝置

您必須 tooverify 您覆盆子 Pi 3 可以連接 toohello SensorTag 裝置之前執行的 hello 範例。

1. 請確定 hello`rfkill`安裝公用程式：

    ```sh
    sudo apt-get install rfkill
    ```

1. 解除封鎖 hello 覆盆子 Pi 3 上的藍芽並檢查 hello 版本號碼**5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. tooenter hello 互動式藍芽殼層，啟動 hello 藍芽服務，然後執行 hello **bluetoothctl**命令：

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. 輸入 hello 命令**開機**toopower hello 藍芽控制器。 hello 命令會傳回類似 toohello 下列輸出：

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. 在 [hello 互動式藍芽 shell] 中，輸入 hello 命令**掃描**tooscan 藍芽裝置。 hello 命令會傳回類似 toohello 下列輸出：

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. 請按下 hello 小按鈕 (綠色 LED 應閃爍的 hello) hello SensorTag 裝置可探索。 hello 覆盆子 Pi 3 應該探索 hello SensorTag 裝置：

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    在此範例中，您可以看到該 hello hello SensorTag 裝置的 MAC 位址**A0:E6:F8:B5:F6:00**。

1. 關閉掃描輸入 hello**掃描關閉**命令：

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. 使用其 MAC 位址輸入 tooyour SensorTag 裝置連接**連接\<MAC 位址\>**。 下列範例輸出的 hello 是為了清楚起見縮寫：

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > 您可以列出一次使用 hello hello 裝置 hello GATT 特性**屬性清單**命令。

1. 您現在可以中斷 hello 透過從裝置 hello**中斷**命令，並結束作業從 hello 藍芽介面使用 hello**結束**命令：

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

您現在準備好 toorun hello B IoT 邊緣範例您覆盆子 Pi 3 為基礎。

## <a name="run-hello-iot-edge-ble-sample"></a>執行 hello IoT 邊緣 b 範例

toorun hello IoT 邊緣 b 範例中，您需要 toocomplete 三項工作：

* 在您的 IoT 中樞上設定兩個範例裝置。
* 在 Raspberry Pi 3 裝置上建置 IoT Edge。
* 設定及執行 hello b 範例覆盆子 Pi 3 裝置。

Hello 撰寫本文時，在 IoT 邊緣只支援 b 模組中的閘道在 Linux 上執行。

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>在您的 IoT 中樞上設定兩個範例裝置

* [建立 IoT 中樞][ lnk-create-hub]在您 Azure 訂用帳戶，您需要集線器 toocomplete hello 名稱本逐步解說。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* 加入一個稱為**SensorTag_01** tooyour IoT 中樞並記下其識別碼和裝置的金鑰。 您可以使用 hello[裝置檔案總管或 iot 中樞總管][ lnk-explorer-tools]工具 tooadd hello 上一個步驟和 tooretrieve 中建立它的索引鍵此裝置 toohello IoT 中樞。 當您設定 hello 閘道，您可以對應此裝置 toohello SensorTag 裝置。

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>在 Raspberry Pi 3 上建置 Azure IoT Edge

安裝 Azure IoT Edge 的相依項目：

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

使用 hello 下列命令 tooclone IoT 邊緣和所有其所 tooyour 主目錄：

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

當您覆盆子 Pi 3 hello IoT 邊緣儲存機制的完整複本，您可以建置使用 hello hello 資料夾包含 hello SDK 中的下列命令：

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>設定及執行您的覆盆子 Pi 3 hello b 範例

toobootstrap 以及執行的 hello 範例，您必須設定每個參與的 IoT 邊緣模組 hello 閘道中。 這個組態是以 JSON 檔案來提供，您必須設定所有五個參與的 IoT Edge 模組。 呼叫 hello 儲存機制中沒有範例 JSON 檔案**閘道\_sample.json**您可以使用做為起點來建立您自己的組態檔的 hello。 這個檔案位於 hello **src/ble_gateway範例/** hello IoT 邊緣儲存機制的本機副本中的資料夾。

hello 下列各節說明如何 tooedit 此組態檔取得 hello b 範例，然後假設該 hello IoT 邊緣存放庫處於 hello **/home/pi/iot-edge /**上您覆盆子 Pi 3 資料夾。 如果 hello 儲存機制是在其他位置，請據以調整 hello 路徑。

#### <a name="logger-configuration"></a>記錄器組態

假設 hello 閘道儲存機制位於 hello **/home/pi/iot-edge /**資料夾中，設定 hello 記錄器模組，如下所示：

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>BLE 模組組態

hello b 裝置 hello 範例設定假設德州儀器 SensorTag 裝置。 任何標準 b 裝置週邊 GATT 應該會運作，但您可能需要 tooupdate hello GATT 特性 Id 和資料可操作。 加入 SensorTag 裝置 hello MAC 位址：

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

如果您不使用 SensorTag 裝置，檢閱您 b 裝置 toodetermine hello 文件，您是否需要 tooupdate hello GATT 特性 Id 和資料值。

#### <a name="iot-hub-module"></a>IoT 中樞模組

加入 hello 的 IoT 中樞的名稱。 hello 尾碼值通常是**azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>身分識別對應模組組態

新增您 SensorTag 裝置和 hello 裝置識別碼和金鑰的 hello hello MAC 位址**SensorTag_01**加入 tooyour IoT 中樞的裝置：

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>BLE 印表機模組組態

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>BLEC2D 模組組態

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>路由組態

hello 下列組態可確保 hello 下列 IoT 邊緣模組之間的路由：

* hello**記錄器**模組接收並記錄所有訊息。
* hello **SensorTag**模組傳送訊息 tooboth hello**對應**和**b 印表機**模組。
* hello**對應**模組傳送訊息 toohello **iot 中樞**模組 toobe 傳送 tooyour IoT 中樞。
* hello **iot 中樞**模組傳送的訊息傳回 toohello**對應**模組。
* hello**對應**模組傳送訊息 toohello **BLEC2D**模組。
* hello **BLEC2D**模組傳送的訊息傳回 toohello**感應器標記**模組。

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

toorun hello 範例傳遞 hello 路徑 toohello JSON 組態檔做為參數 toohello **b\_閘道**二進位。 hello 下列命令假設您正在使用 hello **gateway_sample.json**組態檔。 執行此命令從 hello **iot 邊緣**hello 覆盆子 Pi 上的資料夾：

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

您可能需要 toopress hello 小按鈕，hello SensorTag 裝置 toomake 上它成為可搜尋才執行 hello 範例。

當您執行 hello 範例時，您可以使用 hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)或 hello [iot 中樞總管](https://github.com/Azure/iothub-explorer)工具 toomonitor hello 訊息 hello IoT 邊緣閘道會將從 hello SensorTag 裝置轉送。 例如，使用 iot 中樞總管您就可以監視裝置到雲端訊息使用 hello 下列命令：

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>傳送雲端到裝置訊息

hello b 模組也支援從 IoT 中樞 toohello 裝置傳送命令。 您可以使用 hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)或 hello [iot 中樞總管](https://github.com/Azure/iothub-explorer)toohello b 裝置上的工具 toosend JSON 訊息 hello b 閘道模組轉送。

如果您使用 hello 德州儀器 SensorTag 裝置，您可以開啟 LED hello 紅色、 綠色 LED 或警報器從 IoT 中樞傳送命令。 您從 IoT 中樞傳送命令之前，先傳送 hello 下列兩個 JSON 訊息順序。 然後您可以傳送任何 hello 命令 tooturn hello 燈號或警報器上。

1. 重設所有 Led 和 hello 警報器 （關閉）：

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. 將 I/O 設定為「遠端」：

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

現在您可以傳送任何 hello 遵循命令 tooturn hello 號誌或警報器 hello SensorTag 裝置上：

* 開啟 hello 紅色 LED:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* 開啟 hello 綠色 LED:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* 開啟 hello 警報器：

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>後續步驟

如果您想進一步了解的 IoT 邊緣 toogain 試驗一些程式碼範例，請瀏覽 hello 下列開發人員教學課程和資源：

* [Azure IoT Edge][lnk-sdk]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
