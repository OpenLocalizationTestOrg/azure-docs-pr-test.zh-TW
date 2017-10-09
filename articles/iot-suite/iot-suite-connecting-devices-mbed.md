---
title: "一部裝置上 mbed 使用 C aaaConnect |Microsoft 文件"
description: "描述如何 tooconnect 裝置 toohello Azure IoT 套件預先設定的遠端使用撰寫 C mbed 裝置上執行的應用程式的監視解決方案。"
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>連接您的裝置 toohello 遠端監視預先設定的解決方案 (mbed)

## <a name="scenario-overview"></a>案例概觀
在此案例中，您會建立傳送嗨遵循遙測 toohello 遠端監視的裝置[預先設定的解決方案][lnk-what-are-preconfig-solutions]:

* 外部溫度
* 內部溫度
* 溼度

為了簡單起見，hello hello 裝置上的程式碼會產生範例值，但我們鼓勵您 tooextend hello 範例實際感應器 tooyour 裝置連接和傳送實際的遙測。

hello 裝置也是可以 toorespond toomethods hello 方案儀表板從叫用，且想要設定 hello 方案儀表板中的屬性值。

toocomplete 本教學課程中，您需要使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。

## <a name="before-you-start"></a>開始之前
在您為裝置撰寫任何程式碼之前，您必須先佈建遠端監視預先設定解決方案，並在該解決方案中佈建新的自訂裝置。

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>佈建遠端監視預先設定解決方案
您在本教學課程中建立的 hello 裝置傳送嗨資料 tooan 執行個體[遠端監視][ lnk-remote-monitoring]預先設定的解決方案。 如果您沒有已佈建 hello 遠端監視您的 Azure 帳戶中預先設定的解決方案，使用下列步驟的 hello:

1. 在 hello <https://www.azureiotsuite.com/>頁面上，按一下 **+**  toocreate 方案。
2. 按一下**選取**上 hello**遠端監視**面板 toocreate 您的方案。
3. 在 hello**建立遠端監視解決方案**頁面上，輸入**方案名稱**您選擇的選取 hello**區域**toodeploy，再選取 hello Azure訂用帳戶 toowant toouse。 按一下 [建立解決方案] 。
4. 等待直到 hello 佈建程序完成。

> [!WARNING]
> 預先設定的 hello 解決方案會使用可計費的 Azure 服務。 請務必 tooremove hello 預先設定的方案，從您的訂用帳戶，當您在與其 tooavoid 任何不必要的費用。 您可以完整移除預先設定的方案從您的訂用帳戶瀏覽 hello <https://www.azureiotsuite.com/>頁面。
> 
> 

Hello 佈建 hello 遠端監視解決方案的程序完成時，請按一下**啟動**tooopen hello 方案儀表板在您的瀏覽器中。

![解決方案儀表板][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>佈建您的裝置 hello 遠端監視解決方案中
> [!NOTE]
> 如果您已經在解決方案中佈建裝置，則可以略過此步驟。 當您建立 hello 用戶端應用程式時，您會需要 tooknow hello 裝置認證。
> 
> 

提供裝置 tooconnect toohello 預先設定的解決方案，它必須將自己識別 tooIoT 集線器使用有效的認證。 您可以擷取 hello 裝置認證從 hello 方案儀表板。 您稍後在本教學課程中，用戶端應用程式包含 hello 裝置認證。

tooadd 裝置 tooyour 遠端監視解決方案，下列的完整 hello hello 方案儀表板中的步驟：

1. 在 hello 左下角的 hello 儀表板，按一下 **新增裝置**。
   
   ![新增裝置][1]
2. 在 hello**自訂裝置** 面板中，按一下 **新增**。
   
   ![新增自訂裝置][2]
3. 選擇 [讓我定義自己的裝置識別碼]。 輸入裝置識別碼，例如**mydevice**，按一下 **檢查識別碼**tooverify 還未在使用中，該名稱，然後按一下**建立**tooprovision hello 裝置。
   
   ![新增裝置識別碼][3]
4. 請注意 hello 裝置認證 （裝置識別碼、 IoT 中樞的主機名稱、 和裝置金鑰）。 用戶端應用程式需要這些值 tooconnect toohello 遠端監視解決方案。 然後按一下 [完成]。
   
    ![檢視裝置認證][4]
5. Hello hello 方案儀表板中的裝置清單中選取您的裝置。 然後，在 hello**裝置詳細資料**] 面板中，按一下 [**啟用裝置**。 您的裝置 hello 狀態現在是**執行**。 hello 遠端監視解決方案現在可以從您的裝置接收遙測，並叫用 hello 裝置上的方法。

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>建置並執行 hello C 範例方案

hello 下列指示描述連接 hello 步驟[mbed 啟用 Freescale FRDM K64F] [ lnk-mbed-home]裝置 toohello 遠端監視解決方案。

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Hello mbed 裝置 tooyour 網路和桌面的電腦連接

1. Hello mbed 裝置 tooyour 網路使用乙太網路纜線連線。 這個步驟是必要的因為 hello 範例應用程式需要網際網路存取。

1. 請參閱[入門 mbed] [ lnk-mbed-getstarted] tooconnect mbed 裝置 tooyour 桌面電腦。

1. 如果您桌面的電腦執行 Windows，請參閱[PC 組態][ lnk-mbed-pcconnect] tooconfigure 序列連接埠存取 tooyour mbed 裝置。

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>建立 mbed 專案並匯入 hello 範例程式碼

請遵循這些步驟 tooadd 某些範例程式碼 tooan mbed 專案。 您匯入 hello 遠端監視入門專案，然後變更 hello 專案 toouse hello MQTT 通訊協定，而不是 hello AMQP 通訊協定。 目前，您需要 toouse hello MQTT 通訊協定 toouse hello 裝置管理功能的 IoT 中樞。

1. 在 網頁瀏覽器，移 toohello mbed.org[開發人員網站](https://developer.mbed.org/)。 如果您尚未註冊，您會看到選項 toocreate （它是免費） 帳戶。 否則，請使用您的帳戶認證登入。 然後按一下 **編譯器**hello 右上角的 hello 頁面。 此動作可讓您 toohello*工作區*介面。

1. 請確定 hello 您所使用的硬體平台會出現在 hello 右上角的 [hello] 視窗中，或按一下 hello 圖示 hello 右下角 tooselect 在您的硬體平台。

1. 按一下**匯入**hello 主功能表上。 然後按一下 **按這裡從 URL tooimport**。
   
    ![啟動匯入 toombed 工作區][6]

1. 在 hello 快顯視窗中，輸入 hello 範例程式碼 https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ hello 連結，然後按一下 **匯入**。
   
    ![匯入範例程式碼 toombed 工作區][7]

1. 您可以在 hello mbed 編譯器視窗中看到，匯入這個專案也會匯入的各種程式庫。 部分提供且由 hello Azure IoT 團隊負責維護 ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/)， [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/)， [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/)， [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/))，而其他則 hello mbed 媒體櫃類別目錄中所適用的協力廠商程式庫。
   
    ![檢視 mbed 專案][8]

1. 在 hello**程式工作區**，以滑鼠右鍵按一下 hello **iot 中樞\_amqp\_傳輸**程式庫，按一下**刪除**，然後按一下 **確定**tooconfirm。

1. 在 hello**程式工作區**，以滑鼠右鍵按一下 hello **azure\_amqp\_c**程式庫，按一下 **刪除**，然後按一下 **確定** tooconfirm。

1. 以滑鼠右鍵按一下 hello **remote_monitoring** hello 中的專案**程式工作區**，選取**匯入程式庫**，然後選取**From URL**。
   
    ![啟動程式庫匯入 toombed 工作區][6]

1. 在 hello 快顯視窗中，輸入 hello MQTT 傳輸程式庫 https://developer.mbed.org/users/AzureIoTClient/code/iothub hello 連結\_mqtt\_傳輸 / 然後按一下 **匯入**。
   
    ![匯入程式庫 toombed 工作區][12]

1. Hello 重複上一個步驟 tooadd hello MQTT 從程式庫 https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /。

1. 您的工作區現在看起來像下列 hello:

    ![檢視 mbed 工作區][13]

1. 遠端開啟 hello\_monitoring\remote_monitoring.c 檔案和取代現有的 hello`#include`陳述式，以下列程式碼的 hello:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. 刪除所有剩餘 hello 遠端中的程式碼的 hello\_monitoring\remote\_monitoring.c 檔案。

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>建置並執行 hello 範例

新增程式碼 tooinvoke hello**遠端\_監視\_執行**函式，然後建置並執行 hello 裝置應用程式。

1. 新增**主要**函式與下列程式碼結尾 hello hello 遠端\_monitoring.c 檔案 tooinvoke hello**遠端\_監視\_執行**函式：
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. 按一下**編譯**toobuild hello 程式。 您可以安全地忽略任何警告，，但如果 hello 建置會產生錯誤，修正後再繼續。

1. 如果 hello 建置成功，hello mbed 編譯器網站會產生 hello 專案名稱的.bin 檔案，並會下載 tooyour 本機電腦。 複製 hello.bin 檔案 toohello 裝置。 儲存 hello.bin 檔案 toohello 裝置會導致 hello 裝置 toorestart 並執行 hello.bin 檔案中包含的 hello 程式。 您可以手動重新啟動 hello 程式隨時按下上 hello mbed 裝置 hello 重設按鈕。

1. 使用 SSH 用戶端應用程式，例如 PuTTY toohello 裝置連線。 您可以判斷您的裝置會使用透過檢查 Windows 裝置管理員中的 hello 序列連接埠。
   
    ![][11]

1. 在 PuTTY，按一下 hello**序列**連接類型。 hello 裝置通常會 9600 傳輸連接中，因此輸入 hello 9600**速度**方塊。 然後按一下 [開啟] 。

1. hello 程式開始執行。 如果 hello 程式沒有自動啟動您的連接時，可能會發生 tooreset hello 面板 （按 CTRL + Break 或按 hello 面板的 [重設] 按鈕）。
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
