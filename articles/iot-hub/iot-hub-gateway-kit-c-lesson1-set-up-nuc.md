---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 1 課：設定 Intel NUC | Microsoft Docs"
description: "設定 Intel NUC toowork 為 IoT 閘道之間的感應器和 Azure IoT 中樞 toocollect 感應器資訊，以傳送 tooIoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 閘道, intel nuc, nuc 電腦, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>將 Intel NUC 設定為 IoT 閘道器
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>將執行的作業

- 將 Intel NUC 設定為 IoT 閘道器。
- Hello Azure IoT 邊緣上安裝套件 hello Intel NUC。
- Hello Intel NUC tooverify hello 閘道功能上執行"hello_world 」 範例應用程式。

  > 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

在這一課，您將了解：

- 如何 tooconnect Intel NUC 與週邊設備。
- 如何在使用 Intel NUC tooinstall 和更新所需的 hello 封裝 hello 智慧套件管理員。
- 如何 toorun hello"hello_world 」 的範例應用程式 tooverify hello 閘道功能。

## <a name="what-you-need"></a>您需要什麼

- 以 hello Intel IoT 閘道軟體套件 Intel NUC 套件 DE3815TYKE (Wind 河 Linux * 7.0.0.13) 預先安裝。 [按一下這裡 toopurchase Groove IoT 商業閘道套件](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html)。
- 乙太網路連接線。
- 鍵盤。
- HDMI 或 VGA 連接線。
- 具有 HDMI 或 VGA 連接埠的螢幕。
- 選擇性︰[Texas Instruments 的感應器標籤 (CC2650STK) (英文)](http://www.ti.com/tool/cc2650stk)

![閘道器套件](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>與 hello 週邊設備連接 Intel NUC

hello 圖是 Intel NUC 會連接到各種週邊設備的範例：

1. 連接的 tooa 鍵盤。
2. VGA 纜線或 HDMI 纜線連接 tooa 監視器。
3. 有線乙太網路纜線與網路連線的 tooa。
4. 使用電源纜線連接的 tooa 電源供應器。

![Intel NUC 連接 tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>從主機電腦透過安全殼層 (SSH) 連線 toohello Intel NUC 系統

您必須使用鍵盤和 Intel NUC 裝置的監視 tooget hello IP 位址。 如果您已經知道 hello IP 位址，您可以略過前 toostep 3 這一節。

1. 開啟 hello Intel NUC 按 hello 電源按鈕，然後登入。

   hello 預設使用者名稱和密碼都`root`。

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. 藉由執行 hello 取得 hello IP 位址的 hello Intel NUC `ifconfig` hello Intel NUC 裝置上的命令。

   以下是 hello 命令輸出的範例。

   ![顯示 Intel NUC IP 的 ifconfig 輸出](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   在此範例中，hello 值後面`inet addr:`是您需要時從主機電腦連接 toohello Intel NUC hello IP 位址。

3. 使用其中一種您主機電腦 tooconnect tooIntel NUC 中的下列 SSH 用戶端 hello。

    - [PuTTY](http://www.putty.org/) 適用於 Windows。
    - hello 內建 SSH 用戶端上 Ubuntu 或 macOS。

   更有效率且更有生產力 toooperate 從主機電腦 Intel NUC 它。 您需要 hello Intel NUC IP 位址，透過將 SSH 用戶端的使用者名稱和密碼 tooconnect tooit。 以下是在 macOS 上使用 SSH 用戶端的範例。
   ![在 macOS 上執行的 SSH 用戶端](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>安裝 hello Azure IoT 邊緣套件

hello Azure IoT 邊緣套件包含 hello IoT 邊緣和其相依性的先行編譯二進位檔。 這些二進位檔是 Azure IoT 邊緣、 hello Azure IoT SDK 和 hello 對應工具。 hello 封裝也包含 「 hello_world 」 範例應用程式是使用的 toovalidate hello 閘道功能。 IoT 邊緣屬於 hello 核心 hello 閘道。 

請遵循這些步驟 tooinstall hello 封裝。

1. 藉由執行下列命令在 terminal 視窗中的 hello 新增 hello IoT 雲端儲存機制：

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > 輸入 'y'，當提示您 too'Include 此通道嗎？ '
   
   如果您收到`import read failed(-1)`錯誤，使用下列命令 tooresolve hello 問題的 hello:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   hello`rpm`命令匯入 hello rpm 索引鍵。 hello`smart channel`命令會加入 hello rpm 通道 toohello 智慧套件管理員。 執行 hello 之前`smart update`命令時，您會看到類似下面的的輸出。

   ![rpm 和 smart channel 命令的輸出](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. 執行 hello 智慧更新命令：

   ```bash
   smart update
   ```

3. 執行下列命令的 hello 安裝 hello Azure IoT 閘道套件：

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`這是 hello hello 封裝名稱。 hello`smart install`命令是使用的 tooinstall hello 封裝。

    > 如果您看到此錯誤的 hello 執行的下列命令: '公用金鑰無法使用'

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > 如果您看到此錯誤，請重新啟動 hello Intel NUC: '沒有封裝所提供的開發人員 linux util '

   安裝 hello 套件之後，Intel NUC 是準備 toofunction 閘道。

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>執行 hello Azure IoT 邊緣"hello_world 」 範例應用程式

hello 遵循範例應用程式建立從閘道`hello_world.json`檔案，並每隔 5 秒使用的 Azure IoT 邊緣架構 toolog hello world 訊息 tooa 檔案 (.log.txt) hello 基礎元件。

您可以藉由執行下列命令的 hello 執行 hello Hello World 範例：

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

可讓 hello Hello World 應用程式執行幾分鐘，然後按下 hello Enter 鍵 toostop 它。
![應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> 您可以忽略您按下 Enter 之後出現的任何「無效的引數控制代碼 (NULL)」錯誤。

您可以確認該 hello 閘道已順利執行開啟現在是 hello_world 資料夾中的 hello.log.txt 檔案![.log.txt 目錄檢視](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

開啟.log.txt 使用 hello 下列命令：

```bash
vim log.txt
```

然後，您會看到 hello.log.txt，將 JSON 格式的輸出則 hello 閘道 Hello World 模組來撰寫每隔 5 秒的 hello 記錄訊息內容。
![log.txt 目錄檢視](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。

## <a name="summary"></a>摘要

恭喜！ 您已完成將 Intel NUC 設定為閘道器。 現在您已準備 toomove toohello 下一個課程 tooset 主機電腦時，在建立 Azure IoT 中樞，並註冊您的 Azure IoT 中樞邏輯裝置。

## <a name="next-steps"></a>後續步驟
[使用 IoT 閘道 tooconnect 裝置 tooAzure IoT 中樞](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

