---
title: "連接您的 Azure IoT 套件 aaaDeploy factory 閘道 |Microsoft 文件"
description: "如何 toodeploy 閘道在 Windows 或 Linux tooenable 連線 toohello 連接工廠預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>部署 Windows 或 Linux 上閘道連線的 hello factory 預先設定的解決方案

hello 軟體所需的閘道連線的 hello factory 預先設定的解決方案 toodeploy 有兩個元件：

* hello *OPC Proxy*建立連線 tooIoT 中樞。 hello *OPC Proxy*然後等候來自 hello 的命令和控制訊息的整合 hello 連線的 factory 方案入口網站中執行的 OPC 瀏覽器。
* hello *OPC 發行者*連接 tooexisting 內部 OPC UA 伺服器和從中 tooIoT 中樞轉送遙測訊息。

這兩個元件都是開放程式碼，且以 GitHub 上的來源與 Docker 容器的方式提供：

| GitHub | DockerHub |
| ------ | --------- |
| [OPC 發行者][lnk-publisher-github] | [OPC 發行者][lnk-publisher-docker] |
| [OPC Proxy][lnk-proxy-github] | [OPC Proxy][lnk-proxy-docker] |

沒有公開 IP 位址或 hello 閘道防火牆中的漏洞所需的其中一個元件。 hello OPC Proxy 和 OPC 發行者使用只有輸出連接埠 443、 5671、 和 8883。

hello 本文章中的步驟示範的閘道器上使用 Docker toodeploy [Windows](#windows-deployment)或[Linux](#linux-deployment)。 hello 閘道啟用連線 toohello 連接工廠預先設定的解決方案。

> [!NOTE]
> 執行 hello Docker 容器中的 hello 閘道軟體[Azure IoT 邊緣]。

## <a name="windows-deployment"></a>Windows 部署

> [!NOTE]
> 如果您還沒有閘道裝置，Microsoft 建議您從我們的合作夥伴購買商業閘道。 請瀏覽 hello [Azure IoT 裝置類別目錄]取得一份 hello 與相容的閘道裝置連線 factory 方案。 請遵循隨附 hello 裝置 tooset hello 閘道組成的 hello 指示。 或者，使用下列的其中一個您現有的閘道設定的指示 toomanually hello。

### <a name="install-docker"></a>安裝 Docker

在 Windows 閘道裝置上安裝 [Docker for Windows]。 在 Windows Docker 安裝期間選取的磁碟機上使用 Docker 您主機機器 tooshare。 下列螢幕擷取畫面顯示共用 hello D 磁碟機，Windows 系統上的 hello:

![安裝 Docker][img-install-docker]

然後建立一個稱為資料夾**docker** hello hello 根目錄中共用磁碟機。
您也可以執行此步驟之後從 hello 安裝 docker**設定**功能表。

### <a name="configure-hello-gateway"></a>Hello 閘道設定

1. 您需要 hello **iothubowner**您的 Azure IoT 套件的連接字串連接工廠部署 toocomplete hello 閘道部署。 在 hello [Azure 入口網站]，瀏覽的 tooyour 部署 hello 連接工廠方案時，建立 IoT 中樞 hello 資源群組中。 按一下**共用存取原則**tooaccess hello **iothubowner**連接字串：

    ![Hello IoT 中樞連接字串中尋找][img-hub-connection]

    複製 hello**連接字串-主索引鍵**值。

1. 藉由執行 hello 兩個閘道模組，設定您的 IoT 中樞 hello 閘道**一旦**從命令提示字元，使用：

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;** 是 hello 名稱 toogive tooyour OPC UA 發行者 hello 格式**發行者。&lt;完整的網域名稱&gt;**。 例如，如果您處理站的網路呼叫**myfactorynetwork.com**，hello **ApplicationName**值是**publisher.myfactorynetwork.com**。
    * **&lt;IoTHubOwnerConnectionString&gt;** 為 hello **iothubowner** hello 先前步驟中複製的連接字串。 這個連接字串只能用在此步驟中，您不需要在 hello 下列步驟：

    您使用 hello 對應 d:\\docker 資料夾 (hello`-v`引數) 更新 toopersist hello hello 閘道模組使用的兩個 X.509 憑證。

### <a name="run-hello-gateway"></a>執行 hello 閘道

1. 使用下列命令的 hello hello 閘道來重新啟動：

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. 基於安全性理由，hello 兩個 X.509 憑證保存在 d: hello\\docker 資料夾包含 hello 私密金鑰。 限制存取 toothis 資料夾 toohello 認證 (通常**管理員**) 使用 toorun hello Docker 容器。 以滑鼠右鍵按一下 hello d:\\docker 資料夾中，選擇**屬性**，然後**安全性**，然後**編輯**。 賦予 **Administrators** 完全控制，並移除其他人︰

    ![授與權限 tooDocker 共用][img-docker-share]

1. 驗證網路連線。 從命令提示字元中，輸入 hello 命令`ping publisher.<your fully qualified domain name>`tooping 您的閘道。 如果無法連線到 hello 目的地，新增 hello IP 位址和閘道 toohello hosts 檔案在閘道上的名稱。 hello 主機檔案位於 hello **Windows\\System32\\驅動程式\\等**資料夾。

1. 接下來，請嘗試使用執行 hello 閘道上的本機 OPC UA 用戶端 tooconnect toohello 「 發行者 」。 hello OPC UA 端點 URL 為`opc.tcp://publisher.<your fully qualified domain name>:62222`。 如果您沒有 OPC UA 用戶端，則可以下載並使用[開放原始碼的 OPC UA 用戶端]。

1. 當您已成功完成這些本機測試時，瀏覽 toohello**自己 OPC UA 伺服器連接**hello 連接的工廠方案入口網站頁面中。 輸入 hello 發行者端點 URL (`tcp://publisher.<your fully qualified domain name>:62222`) 按一下**連接**。 您會收到憑證警告，然後按一下 [Proceed (繼續)]。 接下來您收到錯誤的 hello 發行者不信任 hello UA Web 用戶端。 tooresolve 這個錯誤，複製 hello **UA Web 用戶端**憑證從 hello **d:\\docker\\拒絕憑證\\憑證**資料夾 toohello **D:\\docker\\UA 應用程式\\憑證**hello 閘道上的資料夾。 您不需要 toorestart 的 hello 閘道。 重複此步驟。 您現在可以從 hello 雲端連線 toohello 閘道，而且您會準備 tooadd OPC UA 伺服器 toohello 方案。

### <a name="add-your-opc-ua-servers"></a>新增 OPC UA 伺服器

1. 瀏覽 toohello**自己 OPC UA 伺服器連接**hello 連接的工廠方案入口網站頁面中。 請遵循相同的 hello 前面一節 tooestablish 步驟之間的信任 hello 連線的 factory 入口網站和 hello OPC UA 伺服器 hello。 此步驟會建立相互信任的 hello hello 憑證 factory 入口網站和 hello OPC UA 伺服器連線，並建立連線。

1. 瀏覽 hello UA OPC OPC UA 伺服器節點樹狀結構、 以滑鼠右鍵按一下 hello OPC 節點，並選取**發行**。 發行 toowork 這種方式，如 hello OPC UA 伺服器且 hello 「 發行者 」 必須在 hello 相同的網路。 換句話說，如果 hello 完整網域名稱的 hello 發行者是**publisher.mydomain.com** hello hello OPC UA 伺服器必須，例如，完整的網域名稱，然後**myopcuaserver.mydomain.com**.如果您的設定不同，您可以手動新增節點 toohello publishesnodes.json 檔案位於 hello **d:\\docker**資料夾。 hello publishesnodes.json 檔案會自動產生 hello 上第一次成功發佈的 OPC 節點。

1. 遙測現在順著 hello 閘道裝置。 您可以在 hello 檢視 hello 遙測**Factory 位置**hello 連線的 factory 入口網站下的檢視**新的處理站**。

## <a name="linux-deployment"></a>Linux 部署

> [!NOTE]
> 如果您還沒有閘道裝置，Microsoft 建議您從我們的合作夥伴購買商業閘道。 請瀏覽 hello [Azure IoT 裝置類別目錄]取得一份 hello 與相容的閘道裝置連線 factory 方案。 請遵循隨附 hello 裝置 tooset hello 閘道組成的 hello 指示。 或者，使用下列的其中一個您現有的閘道設定的指示 toomanually hello。

在 Linux 閘道裝置上[安裝 Docker]。

### <a name="configure-hello-gateway"></a>Hello 閘道設定

1. 您需要 hello **iothubowner**您的 Azure IoT 套件的連接字串連接工廠部署 toocomplete hello 閘道部署。 在 hello [Azure 入口網站]，瀏覽的 tooyour 部署 hello 連接工廠方案時，建立 IoT 中樞 hello 資源群組中。 按一下**共用存取原則**tooaccess hello **iothubowner**連接字串：

    ![Hello IoT 中樞連接字串中尋找][img-hub-connection]

    複製 hello**連接字串-主索引鍵**值。

1. 藉由執行 hello 兩個閘道模組，設定您的 IoT 中樞 hello 閘道**一旦**從與殼層：

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  hello hello OPC UA 應用程式 hello 閘道建立 hello 格式名稱**發行者。&lt;完整的網域名稱&gt;**。 例如，**publisher.microsoft.com**。
    * **&lt;IoTHubOwnerConnectionString&gt;** 為 hello **iothubowner** hello 先前步驟中複製的連接字串。 這個連接字串只能用在此步驟中，您不需要在 hello 下列步驟：

    使用 hello **/ 共用**資料夾 (hello`-v`引數) 更新 toopersist hello hello 閘道模組使用的兩個 X.509 憑證。

### <a name="run-hello-gateway"></a>執行 hello 閘道

1. 使用下列命令的 hello hello 閘道來重新啟動：

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. 基於安全性理由，hello 兩個 X.509 憑證保存在 hello **/ 共用**資料夾包含 hello 私密金鑰。 限制存取 toothis 資料夾 toohello 認證使用 toorun hello Docker 容器。 tooset hello 權限**根**只能使用 hello`chmod`殼層 hello 資料夾上的命令。

1. 驗證網路連線。 從殼層中，輸入 hello 命令`ping publisher.<your fully qualified domain name>`tooping 您的閘道。 如果無法連線到 hello 目的地，新增 hello IP 位址和閘道 tooyour hosts 檔案在閘道上的名稱。 hello 主機檔案位於 hello **/等等**資料夾。

1. 接下來，請嘗試使用執行 hello 閘道上的本機 OPC UA 用戶端 tooconnect toohello 「 發行者 」。 hello OPC UA 端點 URL 為`opc.tcp://publisher.<your fully qualified domain name>:62222`。 如果您沒有 OPC UA 用戶端，則可以下載並使用[開放原始碼的 OPC UA 用戶端]。

1. 當您已成功完成這些本機測試時，瀏覽 toohello**自己 OPC UA 伺服器連接**hello 連接的工廠方案入口網站頁面中。 輸入 hello 發行者端點 URL (`tcp://publisher.<your fully qualified domain name>:62222`) 按一下**連接**。 您會收到憑證警告，然後按一下 [Proceed (繼續)]。 接下來您收到錯誤的 hello 發行者不信任 hello UA Web 用戶端。 tooresolve 這個錯誤，複製 hello **UA Web 用戶端**憑證從 hello **/共用/已拒絕憑證/憑證**資料夾 toohello **/shared/UA 應用程式/憑證**hello 閘道上的資料夾。 您不需要 toorestart 的 hello 閘道。 重複此步驟。 您現在可以從 hello 雲端連線 toohello 閘道，而且您會準備 tooadd OPC UA 伺服器 toohello 方案。

### <a name="add-your-opc-ua-servers"></a>新增 OPC UA 伺服器

1. 瀏覽 toohello**自己 OPC UA 伺服器連接**hello 連接的工廠方案入口網站頁面中。 請遵循相同的 hello 前面一節 tooestablish 步驟之間的信任 hello 連線的 factory 入口網站和 hello OPC UA 伺服器 hello。 此步驟會建立相互信任的 hello hello 憑證 factory 入口網站和 hello OPC UA 伺服器連線，並建立連線。

1. 瀏覽 hello UA OPC OPC UA 伺服器節點樹狀結構、 以滑鼠右鍵按一下 hello OPC 節點，並選取**發行**。 發行 toowork 這種方式，如 hello OPC UA 伺服器且 hello 「 發行者 」 必須在 hello 相同的網路。 換句話說，如果 hello 完整網域名稱的 hello 發行者是**publisher.mydomain.com** hello hello OPC UA 伺服器必須，例如，完整的網域名稱，然後**myopcuaserver.mydomain.com**.如果您的設定不同，您可以手動新增節點 toohello publishesnodes.json 檔案位於 hello **/ 共用**資料夾。 hello publishesnodes.json 會自動產生 hello 上第一次成功發佈的 OPC 節點。

1. 遙測現在順著 hello 閘道裝置。 您可以在 hello 檢視 hello 遙測**Factory 位置**hello 連線的 factory 入口網站下的檢視**新的處理站**。

## <a name="next-steps"></a>後續步驟

進一步了解 hello 連線 factory 的 hello 架構 toolearn 預先設定的方案，請參閱[連接的工廠預先設定方案的逐步解說][lnk-walkthrough]。

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker for Windows]: https://www.docker.com/docker-windows
[Azure IoT 裝置類別目錄]: https://catalog.azureiotsuite.com/?q=opc
[Azure 入口網站]: http://portal.azure.com/
[開放原始碼的 OPC UA 用戶端]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[安裝 Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT 邊緣]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy