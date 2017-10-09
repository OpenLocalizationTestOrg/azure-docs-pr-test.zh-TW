---
title: "aaaAzure IoT 套件和 Logic Apps |Microsoft 文件"
description: "教學課程，說明如何 toohook 組成商務程序的 Logic Apps tooAzure IoT 套件。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>教學課程： 連接邏輯應用程式 tooyour Azure IoT 套件遠端監視預先設定的解決方案
hello [Microsoft Azure IoT 套件][ lnk-internetofthings]遠端監視預先設定的解決方案是很好的方法 tooget 快速地開始使用演化的 IoT 解決方案的端對端功能集。 本教學課程會引導您如何 tooadd 邏輯應用程式 tooyour Microsoft Azure IoT 套件遠端監視預先設定的解決方案。 這些步驟將示範如何連接 tooa 商務程序可以採取進一步的 IoT 解決方案。

*如果您想要尋求遠端監視 tooprovision 如何預先設定方案的逐步解說，請參閱[教學課程： 開始使用 hello 預先設定的 IoT 解決方案][lnk-getstarted]。*

在開始本教學課程之前，您應該：

* 佈建 hello 遠端監視您的 Azure 訂用帳戶中預先設定的解決方案。
* 建立 SendGrid 帳戶 tooenable toosend 商務程序會觸發一封電子郵件。 您可以在 [SendGrid](https://sendgrid.com/) 按一下 [免費試用]，註冊免費試用帳戶。 您註冊免費試用帳戶之後，您需要 toocreate [API 金鑰](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html)SendGrid 授與權限 toosend 郵件中。 您稍後在 hello 教學課程需要此 API 金鑰。

toocomplete 本教學課程中，您需要在 hello 預先設定的方案後端中的 Visual Studio 2015 或 Visual Studio 2017 toomodify hello 動作。

假設您已提供遠端監視預先設定的方案中，瀏覽 toohello 資源群組，為該方案在 hello [Azure 入口網站][lnk-azureportal]。 hello 資源群組都有名稱為 hello 方案名稱相同的 hello 選擇佈建遠端監視解決方案時。 在 hello 資源群組中，您可以看到所有 hello 佈都建您的解決方案，除了 hello Azure Active Directory 應用程式，您可以在 hello Azure 傳統入口網站中找到的 Azure 資源。 hello 下列螢幕擷取畫面顯示範例**資源群組**刀鋒視窗中的遠端監視預先設定的方案：

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin，設定以 hello hello 邏輯應用程式 toouse 預先設定的解決方案。

## <a name="set-up-hello-logic-app"></a>設定 hello 邏輯應用程式
1. 按一下**新增**在資源群組] 刀鋒視窗，在 [hello Azure 入口網站中的 hello 頂端。
2. 搜尋 邏輯應用程式，選取它，然後按一下建立。
3. 填寫 hello**名稱**和使用 hello 相同**訂用帳戶**和**資源群組**您佈建遠端監視解決方案時使用。 按一下 [建立] 。
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. 部署完成時，您可以查看資源 hello 邏輯應用程式會列出資源群組中。
5. 按一下 hello 邏輯應用程式 toonavigate toohello 邏輯應用程式刀鋒視窗中，選取 hello**空白邏輯應用程式**範本 tooopen hello**邏輯應用程式設計師**。
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. 選取 [要求]。 這個動作會指定以內送 HTTP 要求加上特定 JSON 格式化承載做為觸發程序。
7. 貼上下列程式碼到 hello 要求本文 JSON 結構描述的 hello:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > 您儲存 hello 邏輯應用程式，但首先您必須將動作之後，您可以複製 hello hello HTTP post 的 URL。
   > 
   > 
8. 按一下手動觸發程序下的 [+ 新增步驟]。 然後按一下 [加入動作] 。
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. 搜尋 [SendGrid - 傳送電子郵件]  並按一下它。
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. 輸入 hello 連接的名稱，例如**SendGridConnection**，輸入 hello **SendGrid API 金鑰**當您設定您的 SendGrid 帳戶，然後按一下您建立**建立**。
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. 新增電子郵件地址與您自己的 tooboth hello**從**和**至**欄位。 新增**遠端監視警示 [DeviceId]** toohello**主旨**欄位。 在 hello**電子郵件內文**欄位中，加入**裝置 [DeviceId] 已報告 [measurementName] 與 [measuredValue] 值。** 您可以加入**[DeviceId]**， **[measurementName]**，和**[measuredValue]**即可 hello**您可以將資料從先前的步驟**> 一節。
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. 按一下**儲存**hello 上方功能表中。
13. 按一下 hello**要求**觸發程序，複製 hello **Http Post toothis URL**值。 稍後在本教學課程中需要此 URL。

> [!NOTE]
> Logic Apps 可讓您 toorun[許多不同類型的動作][ lnk-logic-apps-actions]包括在 Office 365 中的動作。 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>設定 hello EventProcessor Web 工作
在本節中，您可以連接您預先設定的解決方案 toohello 您所建立的邏輯應用程式。 toocomplete 這個工作中，您新增 hello URL tootrigger hello 邏輯應用程式 toohello 動作裝置感應器值超過閾值時所引發。

1. 使用 git 用戶端 tooclone hello 最新版本的 hello [azure iot-遠端-監視 github 儲存機制][lnk-rmgithub]。 例如：
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. 在 Visual Studio 中，開啟 hello **RemoteMonitoring.sln**從 hello 的 hello 儲存機制的本機複本。
3. 開啟 hello **ActionRepository.cs**檔案在 hello**基礎結構\\儲存機制**資料夾。
4. 更新 hello **actionIds**字典以 hello **Http Post toothis URL**您記下從應用程式邏輯，如下所示：
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. 儲存在方案中的 hello 變更並結束 Visual Studio。

## <a name="deploy-from-hello-command-line"></a>從 hello 命令列部署
在本節中，您要部署您的 hello 遠端監視解決方案 tooreplace hello 版本目前在 Azure 中執行的更新的版本。

1. 下列 hello[開發人員安裝][ lnk-devsetup]指示 tooset 部署環境。
2. 在本機，toodeploy 遵循 hello[本機部署][ lnk-localdeploy]指示。
3. toodeploy toohello 雲端並更新您現有的雲端部署，請遵循 hello[雲端部署][ lnk-clouddeploy]指示。 您可以使用原始部署的 hello 名稱做為 hello 部署名稱。 例如，如果呼叫 hello 原始部署**demologicapp**，使用下列命令的 hello:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   當 hello 建置指令碼執行時，務必 toouse hello 相同 Azure 帳戶、 訂用帳戶、 地區和您佈建 hello 方案時所使用的 Active Directory 執行個體。

## <a name="see-your-logic-app-in-action"></a>了解邏輯應用程式的實際運作
hello 遠端監視預先設定的解決方案都有兩個規則時，設定預設您佈建的方案。 這兩個規則都位於 hello **SampleDevice001**裝置：

* 溫度 > 38.00
* 溼度 > 48.00

hello 溫度規則會觸發 hello**引發警示**動作和 hello 溼度規則會觸發 hello **SendMessage**動作。 假設您使用 hello 相同的 URL，這兩個動作 hello **ActionRepository**類別，邏輯應用程式觸發程序，針對任何一項規則。 這兩個規則使用 SendGrid toosend 電子郵件 toohello**至**hello 警示的詳細資料的位址。

> [!NOTE]
> hello 邏輯應用程式會繼續 tootrigger，每次達到 hello 門檻。 tooavoid 不必要的電子郵件，您可以將停用 hello 規則在您的方案入口網站或停用 hello 邏輯應用程式在 hello [Azure 入口網站][lnk-azureportal]。
> 
> 

此外 tooreceiving 電子郵件，您也可以查看在 hello 入口網站中的 hello 邏輯應用程式執行時：

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>後續步驟
既然您已使用邏輯應用程式 tooconnect 預先設定的 hello 方案 tooa 商務程序，您可以深入了解自訂 hello 預先設定的解決方案 hello 選項：

* [使用動態遙測以 hello 遠端監視預先設定的解決方案][lnk-dynamic]
* [裝置資訊的中繼資料中 hello 遠端監視預先設定的解決方案][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
