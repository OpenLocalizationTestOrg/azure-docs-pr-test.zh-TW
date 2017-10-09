---
title: "Service Fabric 應用程式中的 aaaManaging 密碼 |Microsoft 文件"
description: "本文說明 toosecure 密碼 Service Fabric 應用程式中的值。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>管理 Service Fabric 應用程式中的密碼
本指南會引導您管理 Service Fabric 應用程式中的機密資料的 hello 步驟。 密碼可以是任何機密資訊，例如儲存體連接字串、密碼或其他不會以純文字處理的值。

本指南會使用 Azure 金鑰保存庫 toomanage 金鑰和密碼。 不過，*使用*應用程式中的密碼是雲端 tooallow 無從驗證平台應用程式 toobe 部署的 tooa 叢集裝載任何地方。 

## <a name="overview"></a>概觀
hello 建議 toomanage 服務組態設定是透過[服務組態套件][config-package]。 組態套件會有各種版本，並可透過含有健全狀況驗證和自動復原的受管理輪流升級來進行升級。 因為它會減少 hello 的全域服務中斷的可能性，這是慣用的 tooglobal 組態。 加密的密碼也不例外。 Service Fabric 具有內建的功能，可使用憑證加密來加密或解密組態套件 Settings.xml 檔案中的值。

hello 下列圖表說明 hello Service Fabric 應用程式中的密碼管理的基本流程：

![密碼管理概觀][overview]

此流程有四個主要步驟︰

1. 取得資料編密憑證。
2. 在您的叢集安裝 hello 憑證。
3. 時部署應用程式與 hello 憑證加密密碼的值，並將它們插入服務 Settings.xml 組態檔。
4. 讀取加密值超出 Settings.xml 解密與 hello 相同的加密憑證。 

[Azure 金鑰保存庫][ key-vault-get-started]為憑證的安全儲存位置和方式 tooget 此處使用在 Azure 中的 Service Fabric 叢集上安裝憑證。 如果您並不會部署 tooAzure，您不需要 toouse 金鑰保存庫 toomanage 機密資料，Service Fabric 應用程式中。

## <a name="data-encipherment-certificate"></a>資料編密憑證
資料編密憑證只會用於服務的 Settings.xml 中組態值的加密與解密，並無法用來驗證或簽署密碼文字。 hello 憑證必須符合下列需求的 hello:

* hello 憑證必須包含私密金鑰。
* 金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。
* hello 憑證的金鑰使用方法必須包含資料編密 (10)，而且不應該包含伺服器驗證用戶端驗證。 
  
  例如，當建立自我簽署的憑證，使用 PowerShell，hello`KeyUsage`旗標必須設定得`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>在您的叢集安裝 hello 憑證
此憑證必須安裝在 hello 叢集中的每個節點上。 它會成為在執行階段 toodecrypt 值儲存在 Settings.xml 的服務。 請參閱[如何使用 Azure 資源管理員的叢集 toocreate] [ service-fabric-cluster-creation-via-arm]如需安裝指示。 

## <a name="encrypt-application-secrets"></a>加密應用程式密碼
hello Service Fabric SDK 有內建的密碼加密和解密函數。 可以在建置階段加密密碼值，然後在服務代碼中以程式設計方式解密和讀取。 

下列 PowerShell 命令的 hello 是使用的 tooencrypt 密碼。 此命令只會加密 hello 值。它會**不**簽署 hello 加密文字。 您必須使用 hello 相同安裝在您的叢集 tooproduce 加密文字的密碼值的加密憑證：

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

hello 產生的 base-64 字串包含 hello 密碼的加密文字以及已使用的 tooencrypt 的 hello 憑證的相關資訊它。  hello base 64 編碼的字串可插入 hello 與您的服務 Settings.xml 組態檔中的參數`IsEncrypted`屬性設定太`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>將應用程式密碼插入應用程式執行個體內
在理想情況下，部署 toodifferent 環境應該盡可能為自動化。 這可以藉由建置環境中執行密碼的加密，並做為參數提供 hello 加密機密資料，建立應用程式執行個體時完成。

#### <a name="use-overridable-parameters-in-settingsxml"></a>在 Settings.xml 中使用可覆寫參數
hello Settings.xml 組態檔可讓您可以在應用程式建立時提供的可覆寫參數。 使用 hello`MustOverride`屬性而不是為參數提供一個值：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

toooverride 值 Settings.xml 中, 宣告覆寫參數 ApplicationManifest.xml 中的 hello 服務：

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

現在 hello 值可以指定為*應用程式參數*時建立 hello 應用程式的執行個體。 可以使用 PowerShell 編寫指令碼 (或以 C# 撰寫) 來建立應用程式執行個體，使其在建置流程中很容易整合。

使用 PowerShell，hello 參數是提供的 toohello`New-ServiceFabricApplication`命令做為[雜湊表](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

若使用 C#，則應用程式參數在 `ApplicationDescription` 中會指定為 `NameValueCollection`：

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>解密來自服務代碼的密碼
Service Fabric 服務是 NETWORK service 預設在 Windows 上執行，並不存取 toocertificates 節點上都安裝 hello 沒有額外的設定。

使用資料加密憑證時，您會需要 toomake 確認網路服務或執行任何使用者帳戶 hello 服務都有存取 toohello 憑證的私密金鑰。 服務網狀架構就會授與存取服務的自動如果您將它設定 toodo 因此來處理。 可以藉由定義使用者及憑證的安全性原則，在 ApplicationManifest.xml 中完成此組態。 在下列範例的 hello，hello NETWORK SERVICE 帳戶是指定的讀取權限 tooa 憑證其憑證指紋所定義：

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> 複製憑證指紋時從 hello 憑證存放區嵌入式管理單元在 Windows 上，不可見的字元都會放在 hello 指紋字串 hello 開頭。 這個可見的字元可能會導致錯誤時嘗試 toolocate 憑證的指紋，所以要確定 toodelete 這個額外的字元。
> 
> 

### <a name="use-application-secrets-in-service-code"></a>在服務代碼中使用應用程式密碼
從 Settings.xml 存取組態值，設定封裝中的 hello API 允許的值具有 hello 容易解密`IsEncrypted`屬性設定太`true`。 因為加密的 hello 文字包含 hello 憑證用於加密的相關資訊，您不需要 toomanually 尋找 hello 憑證。 hello 憑證只需要 toobe hello 服務執行的 hello 節點上安裝。 只需呼叫 hello`DecryptValue()`方法 tooretrieve hello 原始祕密值：

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>後續步驟
深入了解 [以不同的安全性權限執行應用程式](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
