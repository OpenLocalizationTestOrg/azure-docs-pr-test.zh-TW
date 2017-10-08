---
title: "Azure IoT 中樞安全性 aaaUnderstand |Microsoft 文件"
description: "開發人員指南-toocontrol 存取 tooIoT 中樞裝置應用程式和後端應用程式的方式。 包含安全性權杖和 X.509 憑證支援的相關資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>控制存取 tooIoT 中樞

本文說明 hello 選項來保護您的 IoT 中樞。 IoT 中樞用*權限*toogrant 存取 tooeach IoT 中心端點。 權限限制根據功能 hello 存取 tooan IoT 中樞。

本文章說明：

* 您可以授與 tooa 裝置或後端應用程式 tooaccess IoT 中樞 hello 不同權限。
* hello 驗證程序和 hello token，它會使用 tooverify 權限。
* 如何 tooscope 認證 toolimit 存取 toospecific 資源。
* IoT 中樞支援 X.509 憑證。
* 使用現有的裝置身分識別登錄或驗證結構描述的自訂裝置驗證機制。

### <a name="when-toouse"></a>當 toouse

您必須具備適當的權限 tooaccess hello IoT 中樞端點。 例如，裝置必須包括包含安全性認證，以及傳送 tooIoT 中樞的每個訊息的權杖。

## <a name="access-control-and-permissions"></a>存取控制及權限

您可以授與[權限](#iot-hub-permissions)hello 遵循方法中：

* **IoT 中樞層級的共用存取原則**。 共用存取原則可以授與上面所列[權限](#iot-hub-permissions)的任意組合。 您可以定義原則中 hello [Azure 入口網站][lnk-management-portal]，或以程式設計方式利用 hello [IoT 中樞資源提供者 REST Api][lnk-resource-provider-apis]。 新建立的 IoT 中樞有下列預設原則的 hello:

  * **iothubowner**︰具備所有權限的原則。
  * **service**︰具備 **ServiceConnect** 權限的原則。
  * **device**︰具備 **DeviceConnect** 權限的原則。
  * **registryRead**︰具備 **RegistryRead** 權限的原則。
  * **registryReadWrite**︰具備 **RegistryRead** 和 RegistryWrite 權限的原則。
  * **各裝置的安全性認證**。 每個 IoT 中樞都包含[身分識別登錄][lnk-identity-registry]。 對於這個身分識別登錄中的每個裝置，您可以設定授與的安全性認證**DeviceConnect**權限範圍 toohello 對應裝置的端點。

例如，在典型的 IoT 解決方案中︰

* hello 裝置管理元件會使用 hello *registryReadWrite*原則。
* hello 事件處理器元件會使用 hello*服務*原則。
* hello 裝置執行階段商務邏輯元件會使用 hello*服務*原則。
* 個別裝置使用 hello IoT 中樞的身分識別登錄中儲存的認證進行連接。

> [!NOTE]
> 如需詳細資訊，請參閱[權限](#iot-hub-permissions)。

## <a name="authentication"></a>驗證

Azure IoT 中樞中，會授與存取 tooendpoints 針對 hello 共用存取原則和身分識別登錄安全性認證的權杖進行驗證。

安全性認證，例如對稱金鑰，就不會傳送 hello 線上。

> [!NOTE]
> hello Azure IoT 中樞資源提供者透過保護您 Azure 訂用帳戶，因為所有的提供者在 hello [Azure Resource Manager][lnk-azure-resource-manager]。

如需有關如何 tooconstruct 和使用的安全性權杖，請參閱[IoT 中樞安全性語彙基元][lnk-sas-tokens]。

### <a name="protocol-specifics"></a>通訊協定詳細規格

每個支援的通訊協定 (例如 MQTT、AMQP 及 HTTP) 會以不同的方式傳輸權杖。

Hello 連線封包時使用 MQTT，有 hello deviceId 如下 hello ClientId、 {iothubhostname} / {deviceId} hello 使用者名稱欄位和 SAS 權杖在 hello 密碼 欄位中。 {iothubhostname} 應該 hello hello IoT 中樞 (例如，devices.net contoso.azure) 的完整 CName。

使用 [AMQP][lnk-amqp] 時，IoT 中樞支援 [SASL PLAIN][lnk-sasl-plain] 和 [AMQP 宣告式安全性][lnk-cbs]。

如果您使用 AMQP 宣告為基礎的安全性、 hello 標準指定如何 tootransmit 這些語彙基元。

如 SASL 純 hello **username**可以是：

* `{policyName}@sas.root.{iothubName}`，如果使用 IoT 中樞層級權杖。
* `{deviceId}@sas.{iothubname}`，如果使用裝置範圍權杖。

在這兩種情況下，hello 密碼欄位包含 hello 語彙基元，如下所示[IoT 中樞安全性語彙基元][lnk-sas-tokens]。

HTTP 實作驗證有效的語彙基元併入 hello**授權**要求標頭。

#### <a name="example"></a>範例

使用者名稱 (DeviceId 區分大小寫)︰ `iothubname.azure-devices.net/DeviceId`

密碼 (產生 SAS 權杖，以 hello[裝置總管][ lnk-device-explorer]工具):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> hello [Azure IoT Sdk] [ lnk-sdks]連接 toohello 服務時，自動產生語彙基元。 在某些情況下，hello Azure IoT Sdk 不支援所有的 hello 通訊協定或 hello 的所有驗證方法。

### <a name="special-considerations-for-sasl-plain"></a>SASL PLAIN 的特殊考量

當使用 AMQP SASL 純，連線 tooan IoT 中樞的用戶端可以使用單一語彙基元為每個 TCP 連線。 Hello 權杖過期時，hello TCP 連線從 hello 服務中斷連線再觸發重新連線。 此行為，雖然後端應用程式中，不會有問題會造成損害裝置應用程式中的 hello 下列原因：

* 閘道器通常會代表許多裝置連線。 當使用 SASL 純，它們有 toocreate 不同的 TCP 連接的每個裝置連接 tooan IoT 中樞。 這種情況下大幅增加 hello 電源和網路功能的資源耗用量，而且增加每個裝置連接的 hello 延遲。
* 有限資源的裝置會受到負面影響資源 tooreconnect hello 增加使用每個權杖到期之後。

## <a name="scope-iot-hub-level-credentials"></a>設定 IoT 中樞層級認證的範圍

使用受限制的資源 URI 建立權杖，可以設定 IoT 中樞層級安全性原則的範圍。 例如，從裝置 hello 端點 toosend 裝置到雲端訊息是**/devices/ {deviceId} / 訊息/事件**。 您也可以使用具有的 IoT 中樞層級的共用的存取原則**DeviceConnect**權限 toosign 語彙基元是其 resourceURI **/devices/ {deviceId}**。 這種方法建立的權杖，才可使用 toosend 訊息代表裝置**deviceId**。

這項機制是類似 toohello[事件中心發行者原則][lnk-event-hubs-publisher-policy]，並可讓您 tooimplement 自訂驗證方法。

## <a name="security-tokens"></a>安全性權杖

IoT 中樞使用的安全性語彙基元 tooauthenticate 裝置，而且服務 tooavoid 傳送 hello 網路上的索引鍵。 此外，安全性權杖有時效性和範圍的限制。 [Azure IoT SDK][lnk-sdks] 能在不需要任何特殊組態的情況下自動產生權杖。 某些情況下需要您 toogenerate 作業，並直接使用安全性權杖。 這類案例包括：

* hello MQTT、 AMQP 或 HTTP 介面的 hello 直接使用。
* hello hello 語彙基元服務模式，實作中所述[自訂裝置驗證][lnk-custom-auth]。

IoT 中樞也可讓裝置 tooauthenticate 與 IoT 中樞使用[X.509 憑證][lnk-x509]。

### <a name="security-token-structure"></a>安全性權杖結構

您使用的安全性語彙基元 toogrant 時間界限存取 toodevices 和服務 toospecific 功能 IoT 中樞。 tooget 授權 tooconnect tooIoT 集線器、 裝置和服務必須傳送以共用的存取或對稱金鑰簽章的安全性權杖。 這些金鑰存放在與 hello 身分識別登錄中的裝置識別身分。

共用的存取金鑰授與存取 tooall hello 功能 hello 共用存取原則權限相關聯簽署權杖。 裝置識別身分的對稱金鑰只會授與 hello 簽署權杖**DeviceConnect** hello 的權限相關聯的裝置識別身分。

hello 安全性權杖具有下列格式的 hello:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

以下是 hello 預期值：

| 值 | 說明 |
| --- | --- |
| {signature} |Hello 表單的 hmac-sha256 簽章字串： `{URL-encoded-resourceURI} + "\n" + expiry`。 **重要**: hello 金鑰從 base64 解碼，並做為索引鍵 tooperform hello hmac-sha256 計算。 |
| {resourceURI} |URI 的前置詞 （依區段） 可以使用這個語彙基元開頭的 hello IoT 中樞 （沒有任何通訊協定） 的主機名稱來存取的 hello 端點。 例如， `myHub.azure-devices.net/devices/device1` |
| {expiry} |UTF8 字串 hello epoch 00:00:00 UTC 在 1 年 1 月 1970年起的秒數。 |
| {URL-encoded-resourceURI} |較低的大小寫 URL 編碼的 hello 小寫資源 URI |
| {policyName} |這個語彙基元所參考的 hello 共用存取原則 toowhich hello 名稱。 若 hello 語彙基元是指 toodevice 登錄的認證。 |

**請注意，前置詞**: hello URI 前置詞計算的區段，而不是由字元。 例如，`/a/b` 是 `/a/b/c` 的前置詞，而不是 `/a/bc` 的前置詞。

hello 下列 Node.js 的程式碼片段示範函式呼叫**generateSasToken**計算 hello hello 輸入中的語彙基元`resourceUri, signingKey, policyName, expiresInMins`。 hello 下一節中詳細說明如何 tooinitialize hello 不同的輸入 hello 不同語彙基元的使用案例。

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

比較結果為 hello 安全性語彙基元是相等的 Python 程式碼 toogenerate:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> IoT 中樞機器上驗證 hello hello 權杖的有效時間，因為 hello 漂移 hello 產生 hello 語彙基元的 hello 電腦時鐘必須是最小。

### <a name="use-sas-tokens-in-a-device-app"></a>在裝置應用程式中使用 SAS 權杖

有兩種方式 tooobtain **DeviceConnect**與 IoT 中樞與安全性權杖的權限： 使用[hello 身分識別登錄中的對稱式裝置金鑰](#use-a-symmetric-key-in-the-identity-registry)，或使用[的共用的存取金鑰](#use-a-shared-access-policy).

請記住，所有可從裝置存取的功能，在設計上會於前置詞為 `/devices/{deviceId}`的端點公開。

> [!IMPORTANT]
> hello IoT 中樞會驗證特定裝置的唯一方法使用 hello 裝置身分識別對稱金鑰。 萬一共用的存取原則是使用的 tooaccess 裝置功能，當 hello 方案必須考慮 hello 元件發出 hello 做為受信任的子元件的安全性權杖。

hello 面對裝置的端點是 （不管 hello 通訊協定）：

| 端點 | 功能 |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |傳送裝置到雲端的訊息。 |
| `{iot hub host name}/devices/{deviceId}/devicebound` |接收雲端到裝置的訊息。 |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>在 hello 身分識別登錄中使用對稱金鑰

當使用裝置身分識別對稱金鑰 toogenerate 語彙基元，hello policyName (`skn`) 省略 hello 語彙基元的元素。

例如，語彙基元建立的 tooaccess 裝置的所有功能應擁有都 hello 下列參數：

* 資源 URI： `{IoT hub name}.azure-devices.net/devices/{device id}`、
* 簽署金鑰： hello 任何對稱金鑰`{device id}`身分識別，
* 無原則名稱、
* 任何到期時間。

會使用 hello 前面 Node.js 函式的範例：

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

hello 結果，這會授與存取 tooall device1 的功能，會是：

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> 它是可能 toogenerate SAS 權杖使用 hello.NET[裝置總管][ lnk-device-explorer]工具或 hello 跨平台，節點基礎[iot 中樞總管][ lnk-iothub-explorer]命令列公用程式。

### <a name="use-a-shared-access-policy"></a>使用共用存取原則

當您建立語彙基元從共用的存取原則時，設定 hello`skn`欄位 toohello hello 原則名稱。 此原則必須授與 hello **DeviceConnect**權限。

hello 兩個主要案例使用共用的存取原則 tooaccess 裝置功能包括：

* [雲端通訊協定閘道][lnk-endpoints]、
* [權杖服務][ lnk-custom-auth]用 tooimplement 自訂驗證配置。

因為 hello 共用的存取原則可以可能授與存取 tooconnect 為任何裝置，建立安全性權杖時，它會是重要的 toouse hello 正確的資源 URI。 這項設定，請務必特別有 tooscope hello 語彙基元 tooa 特定裝置使用 hello 資源 URI 中的權杖服務。 這點與通訊協定閘道的關聯性比較薄弱，因為它們已經在為所有裝置調節流量。

例如，權杖的服務使用 hello 預先建立共用存取原則**裝置**就會建立包含下列參數的 hello 的語彙基元：

* 資源 URI： `{IoT hub name}.azure-devices.net/devices/{device id}`、
* 簽署金鑰： hello 的 hello 金鑰的其中之一`device`原則，
* 原則名稱： `device`、
* 任何到期時間。

會使用 hello 前面 Node.js 函式的範例：

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

hello 結果，這會授與存取 tooall device1 的功能，會是：

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

通訊協定閘道無法使用相同語彙基元的只要設定的所有裝置都 hello 資源 URI 太都 hello`myhub.azure-devices.net/devices`。

### <a name="use-security-tokens-from-service-components"></a>使用來自服務元件的安全性權杖

服務元件只會產生使用共用的存取原則授與 hello 適當的權限，如先前所述的安全性權杖。

以下是 hello hello 端點上公開的服務功能：

| 端點 | 功能 |
| --- | --- |
| `{iot hub host name}/devices` |建立、更新、擷取及刪除裝置身分識別。 |
| `{iot hub host name}/messages/events` |接收裝置到雲端的訊息。 |
| `{iot hub host name}/servicebound/feedback` |接收雲端到裝置之訊息的意見反應。 |
| `{iot hub host name}/devicebound` |傳送雲端到裝置的訊息。 |

例如，產生使用 hello 預先建立的服務共用存取原則**registryRead**就會建立包含下列參數的 hello 的語彙基元：

* 資源 URI： `{IoT hub name}.azure-devices.net/devices`、
* 簽署金鑰： hello 的 hello 金鑰的其中之一`registryRead`原則，
* 原則名稱： `registryRead`、
* 任何到期時間。

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

hello 結果，會授與存取 tooread 所有的裝置識別身分，也會是：

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>支援的 X.509 憑證

您可以使用任何 X.509 憑證 tooauthenticate 裝置與 IoT 中樞。 憑證包含：

* **現有的 X.509 憑證**。 裝置可能已經有與其關聯的 X.509 憑證。 hello 裝置可以使用此憑證 tooauthenticate 與 IoT 中樞。
* **自我產生及自我簽署的 X-509 憑證**。 裝置製造商或內部部署器都可以產生這些憑證，並存放在 hello 裝置 hello 相對應的私密金鑰 （和憑證）。 您可以使用 [OpenSSL][lnk-openssl] 和 [Windows SelfSignedCertificate][lnk-selfsigned] 公用程式之類的工具來達到此目的。
* **CA 簽署的 X.509 憑證**。 tooidentify 裝置並驗證與 IoT 中樞，您可以使用產生和簽署的憑證授權單位 (CA) 的 X.509 憑證。 IoT 中樞只會驗證呈現該 hello 指紋符合 hello 設定憑證指紋。 Iot 中樞不會驗證 hello 憑證鏈結。

裝置可以使用 X.509 憑證或安全性權杖來進行驗證，但不可同時使用兩者。

### <a name="register-an-x509-certificate-for-a-device"></a>註冊裝置的 X.509 憑證

hello [Azure IoT 服務 SDK，C#] [ lnk-service-sdk] (版本 1.0.8+) 支援註冊的裝置，會使用 X.509 憑證進行驗證。 其他 API (例如匯入/匯出裝置) 也支援 X.509 憑證。

### <a name="c-support"></a>C\# 支援

hello **RegistryManager**類別會提供程式設計的方式 tooregister 裝置。 特別是，hello **AddDeviceAsync**和**UpdateDeviceAsync** tooregister 可讓您方法，並更新 hello IoT 中樞身分識別登錄中的裝置。 這兩種方法都會採用 **Device** 執行個體做為輸入。 hello**裝置**類別包含**驗證**屬性，可讓您 toospecify 主要和次要 X.509 憑證指紋。 hello 指紋表示 （使用二進位 DER 編碼方式儲存） 的 hello X.509 憑證的 sha-1 雜湊。 您必須指定主憑證指紋或次要的憑證指紋或兩者的 hello 選項。 主要和次要指紋是支援的 toohandle 憑證變換的情況。

> [!NOTE]
> IoT 中樞不需要或儲存 hello 的整個 X.509 憑證，而只 hello 憑證指紋。

以下是範例 C\#程式碼片段 tooregister 使用 X.509 憑證的裝置：

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>在執行階段作業期間使用 X.509 憑證

hello[適用於.NET 的 Azure IoT 裝置 SDK] [ lnk-client-sdk] (版本 1.0.11+) 支援 hello 使用 X.509 憑證。

### <a name="c-support"></a>C\# 支援

hello 類別**DeviceAuthenticationWithX509Certificate**支援 hello 建立**DeviceClient**執行個體使用 X.509 憑證。 hello X.509 憑證必須包含 hello 私密金鑰的 hello （也稱為 PKCS #12） 的 PFX 格式。

以下是範例程式碼片段：

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>自訂裝置驗證

您可以使用 hello IoT 中樞[身分識別登錄][ lnk-identity-registry] tooconfigure 每一裝置的安全性認證和存取控制使用[語彙基元][ lnk-sas-tokens]. 如果您的 IoT 解決方案已有自訂身分識別登錄及/或驗證配置，請考慮建立*token service 的*toointegrate 這項基礎結構與 IoT 中樞。 如此一來，您可以在解決方案中使用其他 IoT 功能。

權杖服務是自訂雲端服務。 它會使用 IoT 中樞*共用存取原則*與**DeviceConnect**權限 toocreate*裝置範圍*語彙基元。 這些語彙基元可讓裝置 tooconnect tooyour IoT 中樞。

![Hello 語彙基元服務模式中的步驟][img-tokenservice]

Hello hello 語彙基元服務模式的主要步驟如下：

1. 為您的 IoT 中樞建立具備 **DeviceConnect** 權限的 IoT 中樞共用存取原則。 您可以建立此原則在 hello [Azure 入口網站][ lnk-management-portal]或以程式設計的方式。 hello 語彙基元服務會使用它會建立此原則 toosign hello 語彙基元。
1. 當裝置需要 tooaccess IoT 中樞時，它會從您的權杖服務要求已簽署的權杖。 hello 裝置可以驗證您自訂身分識別登錄/驗證配置 toodetermine hello 裝置身分識別的 hello 語彙基元服務會使用 toocreate hello 語彙基元。
1. hello 權杖服務傳回的權杖。 hello 語彙基元由使用`/devices/{deviceId}`為`resourceURI`，與`deviceId`為 hello 裝置驗證。 hello 語彙基元服務會使用 hello 共用的存取原則 tooconstruct hello token。
1. hello 裝置會使用直接與 hello IoT 中樞 hello 語彙基元。

> [!NOTE]
> 您可以使用 hello.NET 類別[SharedAccessSignatureBuilder] [ lnk-dotnet-sas]或 hello Java 類別[IotHubServiceSasToken] [ lnk-java-sas] toocreate 語彙基元在權杖的服務中。

hello 語彙基元服務可以視需要設定 hello 權杖到期。 Hello 權杖過期時，hello IoT 中樞伺服器 hello 裝置連線。 然後，hello 裝置必須從 hello 語彙基元服務要求新權杖。 較短的到期時間會增加 hello 負載 hello 裝置和 hello 語彙基元服務。

裝置 tooconnect tooyour 中樞，還是必須將它 toohello IoT 中樞身分識別登錄 — 即使 hello 裝置使用的語彙基元和沒有裝置金鑰 tooconnect。 因此，您可以繼續 toouse 每一裝置的存取控制，啟用或停用裝置身分識別中 hello[身分識別登錄][lnk-identity-registry]。 這種方式可降低 hello 風險使用 token 搭配長時間的到期時間。

### <a name="comparison-with-a-custom-gateway"></a>和自訂閘道器的比較

hello 語彙基元服務模式是 hello 建議的方式 tooimplement IoT 中樞的自訂身分識別登錄/驗證配置。 因為 IoT 中心會繼續 toohandle 建議使用此模式，大部分的 hello 方案流量。 不過，如果使用 hello 通訊協定因此密不可分 hello 自訂驗證配置，您可能需要*自訂閘道*tooprocess 所有 hello 流量。 使用[傳輸層安全性 (TLS) 和預先共用金鑰 (PSK)][lnk-tls-psk] 是這類案例的範例之一。 如需詳細資訊，請參閱 hello[通訊協定閘道][ lnk-protocols]主題。

## <a name="reference-topics"></a>參考主題：

hello 下列參考主題提供您有關控制存取 tooyour IoT 中樞的詳細資訊。

## <a name="iot-hub-permissions"></a>IoT 中樞權限

hello 下表列出您可以使用 toocontrol 存取 tooyour IoT 中樞的 hello 權限。

| 權限 | 注意事項 |
| --- | --- |
| **RegistryRead** |授與讀取存取 toohello 身分識別登錄。 如需詳細資訊，請參閱[身分識別登錄][lnk-identity-registry]。 <br/>後端雲端服務會使用此權限。 |
| **RegistryReadWrite** |授與讀取和寫入存取 toohello 身分識別登錄。 如需詳細資訊，請參閱[身分識別登錄][lnk-identity-registry]。 <br/>後端雲端服務會使用此權限。 |
| **ServiceConnect** |授與存取 toocloud 面對服務的通訊和監視端點。 <br/>授與權限 tooreceive 裝置到雲端訊息傳送雲端到裝置訊息，以及擷取 hello 對應傳遞通知。 <br/>授與權限 tooretrieve 傳遞通知檔案上傳。 <br/>授與權限 tooaccess 裝置雙 tooupdate 標記和所需的屬性，擷取報告的屬性，並執行查詢。 <br/>後端雲端服務會使用此權限。 |
| **DeviceConnect** |授與存取 toodevice 向端點。 <br/>授與權限 toosend 裝置到雲端訊息和接收雲端到裝置訊息。 <br/>授與權限 tooperform 檔案上傳的裝置。 <br/>授與權限 tooreceive 裝置所需的兩個屬性通知和更新裝置 twin 報告的屬性。 <br/>授與權限 tooperform 檔案上傳。 <br/>裝置會使用此權限。 |

## <a name="additional-reference-material"></a>其他參考資料

Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：

* [IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。
* [節流和配額][ lnk-quotas]描述 hello 配額和節流套用 toohello IoT 中心服務的行為。
* [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。
* [IoT 中樞的查詢語言][ lnk-query]描述 hello 查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。
* [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。

## <a name="next-steps"></a>後續步驟

現在您已經學會如何 toocontrol 存取 IoT 中樞時，您可能想要遵循 IoT 中樞開發人員指南主題 hello:

* [使用裝置雙 toosynchronize 狀態和組態][lnk-devguide-device-twins]
* [在裝置上叫用直接方法][lnk-devguide-directmethods]
* [排程多個裝置上的作業][lnk-devguide-jobs]

如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程的 hello:

* [開始使用 Azure IoT 中樞][lnk-getstarted-tutorial]
* [Toosend 雲端到裝置與 IoT 中樞的訊息][lnk-c2d-tutorial]
* [如何 tooprocess IoT 中樞裝置到雲端訊息][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
