---
title: "模擬裝置與 Azure IoT 閘道 - 第 1 課：設定 NUC | Microsoft Docs"
description: "設定 Intel NUC toowork 為 IoT 閘道之間的感應器和 Azure IoT 中樞 toocollect 感應器資訊，以傳送 tooIoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "iot 閘道, intel nuc, nuc 電腦, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>將 Intel NUC 設定為 IoT 閘道器

## <a name="what-you-will-do"></a>將執行的作業

- 將 Intel NUC 設定為 IoT 閘道器。
- Intel NUC 上安裝 hello Azure IoT 邊緣套件。
- 在 Intel NUC tooverify hello 閘道功能上執行"hello_world 」 範例應用程式。
如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

在這一課，您將了解：

- 如何 tooconnect Intel NUC 與週邊設備。
- 如何在使用 Intel NUC tooinstall 和更新所需的 hello 封裝 hello 智慧套件管理員。
- 如何 toorun hello"hello_world 」 的範例應用程式 tooverify hello 閘道功能。

## <a name="what-you-need"></a>您需要什麼

- 以 hello Intel IoT 閘道軟體套件 Intel NUC 套件 DE3815TYKE (Wind 河 Linux * 7.0.0.13) 預先安裝。
- 乙太網路連接線。
- 鍵盤。
- HDMI 或 VGA 連接線。
- 具有 HDMI 或 VGA 連接埠的螢幕。

![閘道器套件](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>與 hello 週邊設備連接 Intel NUC

hello 圖是 Intel NUC 會連接到各種週邊設備的範例：

1. 連接的 tooa 鍵盤。
2. 連接 toohello 監視器 VGA 纜線或 HDMI 纜線。
3. 透過乙太網路纜線有線網路連線的 tooa。
4. 使用電源纜線連接的 toohello 電源供應器。

![Intel NUC 連接 tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>從主機電腦透過安全殼層 (SSH) 連線 toohello Intel NUC 系統

您需要在這裡鍵盤與監視器 tooget hello IP NUC 裝置位址。 如果您已經知道 hello IP 位址，您可以略過 toostep 3 這一節。

1. 開啟 Intel NUC 按 hello 系統中的 hello 電源按鈕和記錄檔。

   hello 預設使用者名稱和密碼都`root`。

2. 藉由執行 hello 取得 NUC hello IP 位址`ifconfig`命令。 Hello NUC 裝置上執行此步驟。

   以下是 hello 命令輸出的範例。

   ![ifconfig 輸出顯示 NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   在此範例中，hello 值後面`inet addr:`是您計劃從主機電腦 tooIntel NUC 遠端 tooconnect 時，您需要的 hello IP 位址。

3. 使用其中一種您主機機器 tooconnect tooIntel NUC 中的下列 SSH 用戶端 hello。

   - [PuTTY](http://www.putty.org/) 適用於 Windows。
   - hello 內建 SSH 用戶端上 Ubuntu 或 macOS。

   它是更有效率且更有生產力 toooperate Intel NUC 上的從主機電腦。 您需要 hello hello IP 位址、 使用者名稱和密碼 tooconnect hello NUC 透過 SSH 用戶端。 以下是範例使用 SSH 用戶端 hello macOS 上。
   ![在 macOS 上執行的 SSH 用戶端](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>安裝 hello Azure IoT 邊緣套件

hello Azure IoT 邊緣封裝包含的 hello SDK hello 預先編譯的二進位檔和其相依性。 這些二進位檔是 Azure IoT 邊緣、 hello Azure IoT SDK 和 hello 對應工具。 hello 封裝也包含 「 hello_world 」 範例應用程式所使用的 toovalidate hello 閘道功能。 IoT 邊緣屬於 hello 核心 hello 閘道。 tooinstall hello 封裝，請遵循下列步驟：

1. 加入 hello IoT 雲端儲存機制，藉由執行下列命令在 terminal 視窗中的 hello:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   hello`rpm`命令匯入 hello rpm 索引鍵。 hello`smart channel`命令會加入 hello rpm 通道 toohello 智慧套件管理員。 執行 hello 之前`smart update`命令，您會看到類似的輸出如下。

   ![rpm 和 smart channel 命令的輸出](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. 藉由執行下列命令的 hello 安裝 hello 封裝：

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`這是 hello hello 封裝名稱。 hello`smart install`命令是使用的 tooinstall hello 封裝。

   安裝 hello 套件之後，Intel NUC 會是預期的 toowork 作為閘道。

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>執行 hello Azure IoT 邊緣"hello_world 」 範例應用程式

跳過`azureiotgatewaysdk/samples`和執行 hello 範例 」 hello_world 」 範例應用程式。 此範例應用程式建立閘道從 hello`hello_world.json`檔案，並使用 hello 的 hello Azure IoT 邊緣架構 toolog hello world 訊息 tooa 檔案的基本元件每隔 5 秒。

您可以藉由執行下列命令的 hello 執行 hello 範例 」 hello_world 」 範例應用程式：

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

hello 範例應用程式會產生 hello 以下輸出如果 hello 閘道功能正常運作：

![應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。

## <a name="summary"></a>摘要

恭喜！ 您已完成將 Intel NUC 設定為閘道器。 現在您已準備 toomove toohello 下一個課程 tooset 主機電腦時，在建立 Azure IoT 中樞，並註冊您的 Azure IoT 中樞邏輯裝置。

## <a name="next-steps"></a>後續步驟
[準備好您的主機電腦和 Azure IoT 中樞](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
