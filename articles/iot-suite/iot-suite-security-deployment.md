---
title: "aaaSecure 物聯網部署 |Microsoft 文件"
description: "此發行項詳細資料時，如何 toosecure IoT 部署"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 95c23341-16b0-4954-b3f2-d2e82ab7b367
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: befba8f2009279c2217dcd3496d529139134ec01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-iot-deployment"></a>保護您的 IoT 部署
這篇文章會提供 hello 下一個層級的詳細資料，來保護 hello Azure IoT 為基礎的物聯網 (IoT) 基礎結構。 它會連結 tooimplementation 設定及部署每個元件的層級詳細資料。 另外也會提供各種競爭方法之間的比較和選擇。

保護 hello Azure IoT 部署可分為下列三個安全性區域的 hello:

* **裝置安全性**： 保護 hello IoT 裝置部署在 hello wild 時。
* **連線安全性**： 確保 hello IoT 裝置與 IoT 中樞之間傳輸的所有資料是機密和竄改。
* **雲端安全性**： 提供的方法 toosecure 資料，而它通過，並儲存在 hello 雲端。

![三個安全性區域][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>保護裝置佈建和驗證
hello Azure IoT 套件 hello 下列兩種方法來保護 IoT 裝置：

* 藉由提供每個裝置，可供 hello 裝置 toocommunicate hello IoT 中樞與唯一識別索引鍵 （安全性權杖）。
* 使用裝置上[X.509 憑證][ lnk-x509]和表示 tooauthenticate hello 裝置 toohello IoT 中樞與私密金鑰。 這種驗證方法可確保該 hello hello 裝置上不知道私密金鑰外 hello 裝置在任何時候，提供較高的安全性等級。

hello 安全性權杖的方法會提供每個呼叫 hello 裝置 tooIoT 集線器所建立的關聯 hello 對稱金鑰 tooeach 呼叫的驗證。 X.509 為基礎的驗證 hello TLS 連線建立過程 hello 實體層允許 IoT 裝置的驗證。 hello 安全性權杖為基礎的方法可以用沒有 hello X.509 驗證這是較不安全的模式。 hello hello 兩個方法之間的選擇主要取決於如何安全 hello 的裝置必須驗證 toobe 和安全存放裝置 hello 裝置上的可用性 (toostore hello 私用金鑰安全地)。

## <a name="iot-hub-security-tokens"></a>IoT 中樞安全性權杖
IoT 中樞將會使用安全性權杖 tooauthenticate 裝置與服務 tooavoid 傳送 hello 網路上的索引鍵。 此外，安全性權杖有時效性和範圍的限制。 Azure IoT SDK 能在不需要任何特殊組態的情況下自動產生權杖。 不過，某些情況下，需要 hello 使用者 toogenerate，並直接使用安全性權杖。 這些包括 hello hello MQTT、 AMQP 或 HTTP 介面，直接使用或 hello hello 語彙基元服務模式實作。

Hello 結構的 hello 安全性權杖和其使用方式的更多詳細資料位於 hello 下列文章：

* [安全性權杖結構][lnk-security-tokens]
* [將 SAS 權杖當做裝置][lnk-sas-tokens]

每個 IoT 中樞[身分識別登錄][ lnk-identity-registry]可以使用的 toocreate hello 服務，如，其中包含執行中雲端到裝置訊息和 tooallow 存取 toohello 佇列中的每一裝置資源面對裝置的端點。 hello IoT 中樞身分識別登錄機提供安全地儲存裝置的身分識別與安全性金鑰的解決方案。 新增一或多個裝置身分識別 tooan 允許清單或封鎖清單，啟用裝置存取的完整控制權。 hello 下列文章提供更多詳細資料 hello 結構 hello 身分識別登錄和支援的作業。

[IoT 中樞支援 MQTT、AMQP 和 HTTP][lnk-protocols] 之類的通訊協定。 每個這些通訊協定以不同的方式使用 hello IoT 裝置 tooIoT 中樞從安全性權杖：

* AMQP: SASL 純文字和 AMQP 宣告式安全性 ({policyName}@sas.root。 {iothubName} IoT 中樞層級語彙基元; hello 案例{deviceId} 發生裝置範圍語彙基元)。
* MQTT: Hello {ClientId}，{IoThubhostname} 為連接的封包使用 {deviceId} / {deviceId} 中 hello **Username**欄位和 SAS 權杖中 hello**密碼**欄位。
* HTTP: Hello 授權要求標頭中是有效的語彙基元。

IoT 中樞身分識別登錄可以是使用的 tooconfigure 每一裝置的安全性認證和存取控制。 但是，如果 IoT 解決方案已經大幅投資[自訂裝置身分識別登錄及/或驗證配置][lnk-custom-auth]，則可藉由建立權杖服務，將現有基礎結構與 IoT 中樞整合。

### <a name="x509-certificate-based-device-authentication"></a>X.509 憑證型裝置驗證
hello 使用[裝置為基礎的 X.509 憑證][ lnk-protocols]和其相關聯的私人和公用金鑰組 hello 實體層級允許額外的驗證。 hello 私密金鑰 hello 裝置安全地儲存，並不是外部 hello 裝置可探索。 hello X.509 憑證包含 hello 裝置，例如裝置識別碼的相關資訊以及其他組織的詳細資料。 Hello 憑證的簽章是使用 hello 私密金鑰所產生。

高層級裝置佈建流程：

* 建立關聯的識別項 tooa 實體裝置 – 裝置身分識別及/或裝置製造或 commissioning 期間的 X.509 憑證相關聯的 toohello 裝置。
* 在 IoT 中樞-裝置身分識別和相關聯的裝置資訊 hello IoT 中樞身分識別登錄中建立對應的識別項目。
* 在 IoT 中樞身分識別登錄中安全地儲存 X.509 憑證指紋。

### <a name="root-certificate-on-device"></a>裝置上的根憑證
建立 IoT 中樞與安全 TLS 連線，時 hello IoT 裝置會驗證使用屬於 hello 裝置 SDK 的根憑證的 IoT 中樞。 若是 hello C client SDK hello 憑證位於 hello 資料夾下"\\c\\憑證"hello hello 儲存機制根目錄下。 雖然這些根憑證是長效的，但它們仍會過期或遭到撤銷。 如果沒有任何方法，更新 hello 裝置上的 hello 憑證 hello 的裝置可能無法再 toosubsequently 連接 toohello IoT 中樞 （或任何其他雲端服務）。 一旦部署 hello IoT 裝置具有表示 tooupdate hello 根憑證會有效地降低此風險。

## <a name="securing-hello-connection"></a>保護 hello 連線
Hello IoT 裝置與 IoT 中樞之間的網際網路連線是使用 hello 傳輸層安全性 (TLS) 標準來保護。 Azure IoT 支援 [TLS 1.2][lnk-tls12]、TLS 1.1 和 TLS 1.0 (依此順序)。 針對 TLS 1.0 的支援僅為提供回溯相容性。 因為它提供 hello 大部分的安全性建議 toouse TLS 1.2。

Azure IoT 套件支援的加密套件，遵循這個順序的 hello。

| 加密套件 | 長度 |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (相等於 7680 位元 RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (相等於 3072 位元 RSA) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (相等於 7680 位元 RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (相等於 3072 位元 RSA) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>保護 hello 雲端
Azure IoT 中樞允許針對每個安全性金鑰定義[存取控制原則][lnk-protocols]。 它會使用下列的 IoT 中樞端點的權限 toogrant 存取 tooeach 組 hello。 權限限制 hello 存取 tooan IoT 中樞根據功能。

* **RegistryRead**。 授與讀取存取 toohello 身分識別登錄。 如需詳細資訊，請參閱[身分識別登錄][lnk-identity-registry]。
* **RegistryReadWrite**。 授與讀取和寫入存取 toohello 身分識別登錄。 如需詳細資訊，請參閱[身分識別登錄][lnk-identity-registry]。
* **ServiceConnect**。 授與存取 toocloud 面對服務的通訊和監視端點。 例如，它會授與權限 tooback 端雲端服務 tooreceive 裝置到雲端訊息、 將雲端到裝置訊息傳送和擷取 hello 對應傳遞通知。
* **DeviceConnect**。 授與存取 toodevice 向端點。 例如，它會授與權限 toosend 裝置到雲端訊息並接收雲端到裝置訊息。 裝置會使用此權限。

有兩種方式 tooobtain **DeviceConnect**與 IoT 中樞與的權限[安全性語彙基元][lnk-sas-tokens]： 使用裝置識別的索引鍵或共用的存取金鑰。 此外，它是重要的 toonote 裝置可以存取的所有功能所設計，具有前置詞端點上公開`/devices/{deviceId}`。

[服務元件只會產生安全性權杖][ lnk-service-tokens]使用共用存取原則授與 hello 適當的權限。

Azure IoT 中樞及其他服務，這可能屬於 hello 方案允許使用者使用 hello Azure Active Directory 的管理。

由 Azure IoT 中樞內嵌的資料可供各種不同服務使用，例如 Azure 串流分析和 Azure Blob 儲存體。 這些服務允許管理存取。 在下面深入了解這些服務和可用選項：

* [Azure Cosmos DB][lnk-docdb]： 管理裝置 hello 的中繼資料的半結構化資料的可擴充、 完全編製索引的資料庫服務您佈建，例如屬性、 組態和安全性內容。 Cosmos DB 提供高效能且高輸送量的處理、無從驗證結構描述的資料索引編製，以及豐富的 SQL 查詢介面。
* [Azure Stream Analytics][lnk-asa]： 即時資料流處理，可讓您 toorapidly hello 雲端中開發和部署低成本的分析解決方案 toouncover 即時見解，並從裝置感應器基礎結構，以及應用程式。 從此完全受管理服務的 hello 資料可以調整 tooany 磁碟區，但仍然達到高輸送量、 低延遲、 和恢復功能。
* [Azure 應用程式服務][lnk-appservices]： 雲端平台 toobuild 強大 web 和行動裝置應用程式連接的任何位置; toodata hello 雲端或內部部署中。 建置吸引客戶參與的 iOS、Android 和 Windows 版行動應用程式。 整合您的軟體為服務 (SaaS) 和企業應用程式的全新連線 toodozens 的雲端服務和企業應用程式。 您最愛的語言和 IDE 中的程式碼 （.NET、 Node.js、 PHP、 Python 或 Java） toobuild web 應用程式和應用程式開發介面比以前更快。
* [邏輯應用程式][lnk-logicapps]: hello Logic Apps 功能的 Azure 應用程式服務可協助整合 IoT 解決方案 tooyour 現有的業務系統和自動化工作流程處理序。 邏輯應用程式可讓開發人員 toodesign 工作流程的觸發程序從開始，然後再執行一系列的步驟-規則和使用功能強大的連接器 toointegrate 與您的商務程序的動作。 邏輯應用程式提供的方塊外連線 tooa vast 的生態系統 SaaS，雲端為基礎，並在內部部署應用程式。
* [Azure blob 儲存體][lnk-blob]： 您的裝置傳送 toohello 雲端的 hello 資料的可靠且經濟的雲端儲存體。

## <a name="conclusion"></a>結論
本文提供使用 Azure IoT 設計和部署 IoT 基礎結構的實作層級詳細資料概觀。 設定每個元件 toobe 安全是金鑰保護 hello 整體 IoT 基礎結構。 Azure IoT 中可用的 hello 設計選項提供某種程度的彈性和選擇。不過，每個選項可能會有安全性隱憂。 建議您透過風險/成本評估謹慎評估每個選擇。

## <a name="see-also"></a>另請參閱
您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預先設定的預防性維護解決方案概觀][lnk-predictive-overview]
* [IoT 套件的常見問題集][lnk-faq]

您可以閱讀 IoT 中樞中的安全性[控制存取 tooIoT 中樞][ lnk-devguide-security] hello IoT 中樞開發人員指南 》 中。


[img-overview]: media/iot-suite-security-deployment/overview.png

[lnk-security-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
