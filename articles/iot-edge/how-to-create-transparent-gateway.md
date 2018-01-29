---
title: "使用 Azure IoT Edge 建立透明閘道裝置 | Microsoft Docs"
description: "使用 Azure IoT Edge 建立可以處理多個裝置資訊的透明閘道裝置"
services: iot-edge
keywords: 
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 12/04/2017
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: 25f4cea1908a0f9bdf387ddfed5f29e6d19bdd20
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2017
---
# <a name="create-an-iot-edge-device-that-acts-as-a-transparent-gateway---preview"></a>建立做為透明閘道的 IoT Edge 裝置 - 預覽

本文會詳細說明如何使用 IoT Edge 裝置做為透明閘道。 本文接下來的「IoT Edge 閘道」一詞是指做為透明閘道的 IoT Edge 裝置。 如需詳細資訊，請參閱[如何使用 IoT Edge 裝置作為閘道][lnk-edge-as-gateway]，其中提供概念性的概觀。 

>[!NOTE]
>目前狀況：
> * 如果閘道與 IoT 中樞中斷連線，則下游裝置無法透過閘道進行驗證。
> * IoT Edge 裝置無法連線到 IoT Edge 閘道。

## <a name="understand-the-azure-iot-device-sdk"></a>了解 Azure IoT 裝置 SDK


安裝在所有 IoT Edge 裝置中的 Edge 中樞會將下列基本項目公開給下游裝置：

* 裝置到雲端及雲端到裝置訊息
* 直接方法
* 裝置對應項作業

目前下游裝置如果透過 IoT Edge 閘道連線時，無法使用檔案上傳功能。

當您使用 Azure IoT 裝置 SDK 將裝置連線到 IoT Edge 閘道 時，您需要：

* 使用引用閘道裝置主機名稱的連接字串來設定下游裝置；以及
* 確定下游裝置信任用來接受閘道裝置連線的憑證。

當您使用控制指令碼來安裝 Azure IoT Edg 執行階段時，用於 Edge 中樞的憑證會隨即建立，如同您在教學課程＜在 [Windows][lnk-tutorial1-win] 和 [Linux][lnk-tutorial1-lin] 上的模擬裝置中安裝 IoT Edge＞中所執行的動作。 Edge 中樞會使用此憑證來接受連入的 TLS 連線，而且連線至閘道裝置時，必須被下游裝置所信任。

您可以建立任何憑證基礎結構，來啟用裝置閘道拓撲所需的信任。 在本文中，我們假設您會使用相同的憑證安裝程式，在 IoT 中樞中啟用 [X.509 CA 安全性][ lnk-iothub-x509]，其中包含與特定 IoT 中樞相關聯的 X.509 CA 憑證 (*IoT 中樞擁有者 CA*)，以及安裝在 IoT Edge 裝置且使用此 CA 簽署的一系列憑證。

>[!IMPORTANT]
>目前，IoT Edge 裝置和下游裝置只能使用 [SAS 權杖][lnk-iothub-tokens] 向 IoT 中樞進行驗證。 憑證將只能用來驗證分葉和閘道裝置之間的 TLS 連線。

我們的設定會使用 **IoT 中樞擁有者 CA** 作為：
* IoT Edge 執行階段在所有 IoT Edge 裝置上的安裝簽署憑證，以及
* 安裝在下游裝置的公開金鑰憑證。

這將產生可讓所有裝置將任何 IoT Edge 裝置作為閘道使用的解決方案，前提是要連線至相同的 IoT 中樞。

## <a name="create-the-certificates-for-test-scenarios"></a>建立測試案例的憑證

您可以使用[管理 CA 憑證範例][lnk-ca-scripts]中所述的 Powershell 和 Bash 指令碼範例，產生自我簽署的 **IoT 中樞擁有者 CA** 和用其簽署的裝置憑證。

>[!IMPORTANT]
>此範例僅供測試用。 如需實際案例，請參閱[保護您的 IoT 部署][lnk-iothub-secure-deployment]，以取得 Azure IoT 指導方針，了解如何保護您的 IoT 解決方案，並據以佈建您的憑證。


1. 從 GitHub 複製 [適用於 C 的 Microsoft Azure IoT SDK 和程式庫]：

   ```
   git clone -b modules-preview https://github.com/Azure/azure-iot-sdk-c.git 
   ```

2. 若要安裝憑證的指令碼，請依照[管理 CA 憑證範例][lnk-ca-scripts]中的＜步驟 1 - 初始設定＞操作。 
3. 若要產生 **IoT 中樞擁有者 CA**，請依照＜步驟 2 - 建立憑證鏈結＞操作。 下游裝置會使用此檔案來驗證連線。
4. 若要產生閘道裝置的憑證，請使用 Bash 或 PowerShell 指令：

### <a name="bash"></a>Bash

建立新的裝置憑證：

   ```
   ./certGen.sh create_edge_device_certificate myGateway
   ```

這會建立新檔案：.\certs\new-edge-device.* 包含公開金鑰和 PFX，而.\private\new-edge-device.key.pem 包含裝置的私密金鑰。
 
在 `certs` 目錄中執行以下命令，以取得裝置公開金鑰的完整鏈結：

   ```
   cat ./new-edge-device.cert.pem ./azure-iot-test-only.intermediate.cert.pem ./azure-iot-test-only.root.ca.cert.pem > ./new-edge-device-full-chain.cert.pem
   ```

### <a name="powershell"></a>Powershell

建立新的裝置憑證： 
   ```
   New-CACertsEdgeDevice myGateway
   ```

這會建立新的 myEdgeDevice* 檔案，其中包含此憑證的公開金鑰、私密金鑰和 PFX。 

簽署過程中若出現輸入密碼的提示，請輸入 "1234"。

## <a name="configure-a-gateway-device"></a>設定閘道裝置

若要將您的 IoT Edge 裝置設定為閘道，您只需要設定為使用上一節中建立的裝置憑證。

我們從上述的範例指令碼中假設下列檔案名稱：

| 輸出 | Bash 指令碼 | PowerShell |
| ------ | ----------- | ---------- |
| 裝置憑證 | `certs/new-edge-device.cert.pem` | `certs/new-edge-device.cert.pem` |
| 裝置私密金鑰 | `private/new-edge-device.cert.pem` | `private/new-edge-device.cert.pem` |
| 裝置憑證鏈結 | `certs/new-edge-device-full-chain.cert.pem` | `certs/new-edge-device-full-chain.cert.pem` |
| IoT 中樞擁有者 CA | `certs/azure-iot-test-only.root.ca.cert.pem` | `RootCA.pem` |

將裝置和憑證資訊提供給 IoT Edge 執行階段。 
 
在 Linux 中，使用 Bash 輸出：

   ```
   sudo iotedgectl setup --connection-string {device connection string}
        --edge-hostname {gateway hostname, e.g. mygateway.contoso.com}
        --device-ca-cert-file {full path}/certs/new-edge-device.cert.pem
        --device-ca-chain-cert-file {full path}/certs/new-edge-device-full-chain.cert.pem
        --device-ca-private-key-file {full path}/private/new-edge-device.key.pem
        --owner-ca-cert-file {full path}/certs/azure-iot-test-only.root.ca.cert.pem
   ```

在 Windows 中，使用 PowerShell 輸出：

   ```
   iotedgectl setup --connection-string {device connection string}
        --edge-hostname {gateway hostname, e.g. mygateway.contoso.com}
        --device-ca-cert-file {full path}/certs/new-edge-device.cert.pem
        --device-ca-chain-cert-file {full path}/certs/new-edge-device-full-chain.cert.pem
        --device-ca-private-key-file {full path}/private/new-edge-device.key.pem
        --owner-ca-cert-file {full path}/RootCA.pem
   ```

依預設，範例指令碼不會對裝置私密金鑰設定複雜密碼。 如果您想設定複雜密碼，請新增下列參數：

   ```
   --device-ca-passphrase {passphrase}
   ```

指令碼會提示您為 Edge 代理程式憑證設定複雜密碼。 執行此命令之後，請重新啟動 IoT Edge 執行階段：

   ```
   iotedgectl restart
   ```

## <a name="configure-a-downstream-device"></a>設定下游裝置

下游裝置可以是任何使用 [Azure IoT 裝置 SDK][lnk-devicesdk] 的應用程式，例如[使用 .NET 將您的裝置連線至 IoT 中樞][lnk-iothub-getstarted]中所述的其中一個。

首先，下游裝置應用程式必須信任 **IoT 中樞擁有者 CA** 憑證，才能驗證連線到閘道裝置的 TLS 連線。 通常有兩種方式可執行此步驟：在作業系統層級，或在 (適用於特定語言) 應用程式層級。

例如，針對 .NET 應用程式，您可以新增下列程式碼片段，來信任 `certPath` 路徑中所儲存的憑證 (PEM 格式)。 視您使用的指令碼版本而定，路徑會參照 `certs/azure-iot-test-only.root.ca.cert.pem` (Bash) 或 `RootCA.pem` (Powershell)。

   ```
   using System.Security.Cryptography.X509Certificates;
   
   ...

   X509Store store = new X509Store(StoreName.Root, StoreLocation.CurrentUser);
   store.Open(OpenFlags.ReadWrite);
   store.Add(new X509Certificate2(X509Certificate2.CreateFromCertFile(certPath)));
   store.Close();
   ```

在作業系統層級執行此步驟不同於在 Windows 之間及 Linux 散發套件之間執行。

第二個步驟是使用連接字串 (引用閘道裝置的主機名稱) 初始化 IoT 中樞裝置 SDK。
這會透過將 `GatewayHostName` 屬性附加至您裝置的連接字串來完成。 例如，以下是裝置的裝置連接字串範例，我們在其中附加 `GatewayHostName` 屬性：

   ```
   HostName=yourHub.azure-devices-int.net;DeviceId=yourDevice;SharedAccessKey=2BUaYca45uBS/O1AsawsuQslH4GX+SPkrytydWNdFxc=;GatewayHostName=mygateway.contoso.com
   ```

這兩個步驟可讓您的裝置應用程式連線至閘道裝置。

## <a name="next-steps"></a>後續步驟
[了解開發 IoT Edge 模組的需求和工具][lnk-module-dev]。

[lnk-devicesdk]: ../iot-hub/iot-hub-devguide-sdks.md
[lnk-tutorial1-win]: tutorial-simulate-device-windows.md
[lnk-tutorial1-lin]: tutorial-simulate-device-linux.md
[lnk-edge-as-gateway]: ./iot-edge-as-gateway.md
[lnk-module-dev]: module-development.md
[lnk-iothub-getstarted]: ../iot-hub/iot-hub-csharp-csharp-getstarted.md
[lnk-iothub-x509]: ../iot-hub/iot-hub-x509ca-overview.md
[lnk-iothub-secure-deployment]: ../iot-hub/iot-hub-security-deployment.md
[lnk-iothub-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-tokens 
[lnk-iothub-throttles-quotas]: ../iot-hub/iot-hub-devguide-quotas-throttling.md
[lnk-iothub-devicetwins]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-iothub-c2d]: ../iot-hub/iot-hub-devguide-messages-c2d.md
[lnk-ca-scripts]: https://github.com/Azure/azure-iot-sdk-c/blob/modules-preview/tools/CACertificates/CACertificateOverview.md
[lnk-modbus-module]: https://github.com/Azure/iot-edge-modbus