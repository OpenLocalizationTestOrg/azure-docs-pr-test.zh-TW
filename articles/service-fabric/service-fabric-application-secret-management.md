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
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="45303-103">管理 Service Fabric 應用程式中的密碼</span><span class="sxs-lookup"><span data-stu-id="45303-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="45303-104">本指南會引導您管理 Service Fabric 應用程式中的機密資料的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="45303-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="45303-105">密碼可以是任何機密資訊，例如儲存體連接字串、密碼或其他不會以純文字處理的值。</span><span class="sxs-lookup"><span data-stu-id="45303-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="45303-106">本指南會使用 Azure 金鑰保存庫 toomanage 金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="45303-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="45303-107">不過，*使用*應用程式中的密碼是雲端 tooallow 無從驗證平台應用程式 toobe 部署的 tooa 叢集裝載任何地方。</span><span class="sxs-lookup"><span data-stu-id="45303-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="45303-108">概觀</span><span class="sxs-lookup"><span data-stu-id="45303-108">Overview</span></span>
<span data-ttu-id="45303-109">hello 建議 toomanage 服務組態設定是透過[服務組態套件][config-package]。</span><span class="sxs-lookup"><span data-stu-id="45303-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="45303-110">組態套件會有各種版本，並可透過含有健全狀況驗證和自動復原的受管理輪流升級來進行升級。</span><span class="sxs-lookup"><span data-stu-id="45303-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="45303-111">因為它會減少 hello 的全域服務中斷的可能性，這是慣用的 tooglobal 組態。</span><span class="sxs-lookup"><span data-stu-id="45303-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="45303-112">加密的密碼也不例外。</span><span class="sxs-lookup"><span data-stu-id="45303-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="45303-113">Service Fabric 具有內建的功能，可使用憑證加密來加密或解密組態套件 Settings.xml 檔案中的值。</span><span class="sxs-lookup"><span data-stu-id="45303-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="45303-114">hello 下列圖表說明 hello Service Fabric 應用程式中的密碼管理的基本流程：</span><span class="sxs-lookup"><span data-stu-id="45303-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![密碼管理概觀][overview]

<span data-ttu-id="45303-116">此流程有四個主要步驟︰</span><span class="sxs-lookup"><span data-stu-id="45303-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="45303-117">取得資料編密憑證。</span><span class="sxs-lookup"><span data-stu-id="45303-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="45303-118">在您的叢集安裝 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="45303-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="45303-119">時部署應用程式與 hello 憑證加密密碼的值，並將它們插入服務 Settings.xml 組態檔。</span><span class="sxs-lookup"><span data-stu-id="45303-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="45303-120">讀取加密值超出 Settings.xml 解密與 hello 相同的加密憑證。</span><span class="sxs-lookup"><span data-stu-id="45303-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="45303-121">[Azure 金鑰保存庫][ key-vault-get-started]為憑證的安全儲存位置和方式 tooget 此處使用在 Azure 中的 Service Fabric 叢集上安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="45303-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="45303-122">如果您並不會部署 tooAzure，您不需要 toouse 金鑰保存庫 toomanage 機密資料，Service Fabric 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="45303-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="45303-123">資料編密憑證</span><span class="sxs-lookup"><span data-stu-id="45303-123">Data encipherment certificate</span></span>
<span data-ttu-id="45303-124">資料編密憑證只會用於服務的 Settings.xml 中組態值的加密與解密，並無法用來驗證或簽署密碼文字。</span><span class="sxs-lookup"><span data-stu-id="45303-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="45303-125">hello 憑證必須符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="45303-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="45303-126">hello 憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="45303-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="45303-127">金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="45303-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="45303-128">hello 憑證的金鑰使用方法必須包含資料編密 (10)，而且不應該包含伺服器驗證用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="45303-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="45303-129">例如，當建立自我簽署的憑證，使用 PowerShell，hello`KeyUsage`旗標必須設定得`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="45303-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="45303-130">在您的叢集安裝 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="45303-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="45303-131">此憑證必須安裝在 hello 叢集中的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="45303-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="45303-132">它會成為在執行階段 toodecrypt 值儲存在 Settings.xml 的服務。</span><span class="sxs-lookup"><span data-stu-id="45303-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="45303-133">請參閱[如何使用 Azure 資源管理員的叢集 toocreate] [ service-fabric-cluster-creation-via-arm]如需安裝指示。</span><span class="sxs-lookup"><span data-stu-id="45303-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="45303-134">加密應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="45303-134">Encrypt application secrets</span></span>
<span data-ttu-id="45303-135">hello Service Fabric SDK 有內建的密碼加密和解密函數。</span><span class="sxs-lookup"><span data-stu-id="45303-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="45303-136">可以在建置階段加密密碼值，然後在服務代碼中以程式設計方式解密和讀取。</span><span class="sxs-lookup"><span data-stu-id="45303-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="45303-137">下列 PowerShell 命令的 hello 是使用的 tooencrypt 密碼。</span><span class="sxs-lookup"><span data-stu-id="45303-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="45303-138">此命令只會加密 hello 值。它會**不**簽署 hello 加密文字。</span><span class="sxs-lookup"><span data-stu-id="45303-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="45303-139">您必須使用 hello 相同安裝在您的叢集 tooproduce 加密文字的密碼值的加密憑證：</span><span class="sxs-lookup"><span data-stu-id="45303-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="45303-140">hello 產生的 base-64 字串包含 hello 密碼的加密文字以及已使用的 tooencrypt 的 hello 憑證的相關資訊它。</span><span class="sxs-lookup"><span data-stu-id="45303-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="45303-141">hello base 64 編碼的字串可插入 hello 與您的服務 Settings.xml 組態檔中的參數`IsEncrypted`屬性設定太`true`:</span><span class="sxs-lookup"><span data-stu-id="45303-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="45303-142">將應用程式密碼插入應用程式執行個體內</span><span class="sxs-lookup"><span data-stu-id="45303-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="45303-143">在理想情況下，部署 toodifferent 環境應該盡可能為自動化。</span><span class="sxs-lookup"><span data-stu-id="45303-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="45303-144">這可以藉由建置環境中執行密碼的加密，並做為參數提供 hello 加密機密資料，建立應用程式執行個體時完成。</span><span class="sxs-lookup"><span data-stu-id="45303-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="45303-145">在 Settings.xml 中使用可覆寫參數</span><span class="sxs-lookup"><span data-stu-id="45303-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="45303-146">hello Settings.xml 組態檔可讓您可以在應用程式建立時提供的可覆寫參數。</span><span class="sxs-lookup"><span data-stu-id="45303-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="45303-147">使用 hello`MustOverride`屬性而不是為參數提供一個值：</span><span class="sxs-lookup"><span data-stu-id="45303-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="45303-148">toooverride 值 Settings.xml 中, 宣告覆寫參數 ApplicationManifest.xml 中的 hello 服務：</span><span class="sxs-lookup"><span data-stu-id="45303-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="45303-149">現在 hello 值可以指定為*應用程式參數*時建立 hello 應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="45303-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="45303-150">可以使用 PowerShell 編寫指令碼 (或以 C# 撰寫) 來建立應用程式執行個體，使其在建置流程中很容易整合。</span><span class="sxs-lookup"><span data-stu-id="45303-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="45303-151">使用 PowerShell，hello 參數是提供的 toohello`New-ServiceFabricApplication`命令做為[雜湊表](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="45303-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="45303-152">若使用 C#，則應用程式參數在 `ApplicationDescription` 中會指定為 `NameValueCollection`：</span><span class="sxs-lookup"><span data-stu-id="45303-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="45303-153">解密來自服務代碼的密碼</span><span class="sxs-lookup"><span data-stu-id="45303-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="45303-154">Service Fabric 服務是 NETWORK service 預設在 Windows 上執行，並不存取 toocertificates 節點上都安裝 hello 沒有額外的設定。</span><span class="sxs-lookup"><span data-stu-id="45303-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="45303-155">使用資料加密憑證時，您會需要 toomake 確認網路服務或執行任何使用者帳戶 hello 服務都有存取 toohello 憑證的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="45303-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="45303-156">服務網狀架構就會授與存取服務的自動如果您將它設定 toodo 因此來處理。</span><span class="sxs-lookup"><span data-stu-id="45303-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="45303-157">可以藉由定義使用者及憑證的安全性原則，在 ApplicationManifest.xml 中完成此組態。</span><span class="sxs-lookup"><span data-stu-id="45303-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="45303-158">在下列範例的 hello，hello NETWORK SERVICE 帳戶是指定的讀取權限 tooa 憑證其憑證指紋所定義：</span><span class="sxs-lookup"><span data-stu-id="45303-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="45303-159">複製憑證指紋時從 hello 憑證存放區嵌入式管理單元在 Windows 上，不可見的字元都會放在 hello 指紋字串 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="45303-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="45303-160">這個可見的字元可能會導致錯誤時嘗試 toolocate 憑證的指紋，所以要確定 toodelete 這個額外的字元。</span><span class="sxs-lookup"><span data-stu-id="45303-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="45303-161">在服務代碼中使用應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="45303-161">Use application secrets in service code</span></span>
<span data-ttu-id="45303-162">從 Settings.xml 存取組態值，設定封裝中的 hello API 允許的值具有 hello 容易解密`IsEncrypted`屬性設定太`true`。</span><span class="sxs-lookup"><span data-stu-id="45303-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="45303-163">因為加密的 hello 文字包含 hello 憑證用於加密的相關資訊，您不需要 toomanually 尋找 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="45303-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="45303-164">hello 憑證只需要 toobe hello 服務執行的 hello 節點上安裝。</span><span class="sxs-lookup"><span data-stu-id="45303-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="45303-165">只需呼叫 hello`DecryptValue()`方法 tooretrieve hello 原始祕密值：</span><span class="sxs-lookup"><span data-stu-id="45303-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="45303-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45303-166">Next Steps</span></span>
<span data-ttu-id="45303-167">深入了解 [以不同的安全性權限執行應用程式](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="45303-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
