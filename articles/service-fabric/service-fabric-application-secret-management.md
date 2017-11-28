---
title: "管理 Service Fabric 應用程式中的祕密 | Microsoft Docs"
description: "本文說明如何保護在 Service Fabric 應用程式中的密碼值。"
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
ms.openlocfilehash: d71924cda8bb3bffbe221946d80dba150359e38e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="86718-103">管理 Service Fabric 應用程式中的密碼</span><span class="sxs-lookup"><span data-stu-id="86718-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="86718-104">本指南將逐步引導您完成管理 Service Fabric 應用程式中密碼的步驟。</span><span class="sxs-lookup"><span data-stu-id="86718-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="86718-105">密碼可以是任何機密資訊，例如儲存體連接字串、密碼或其他不會以純文字處理的值。</span><span class="sxs-lookup"><span data-stu-id="86718-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="86718-106">本指南使用 Azure 金鑰保存庫來管理金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="86718-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="86718-107">不過，應用程式中的密碼「使用」  是由平台驗證，讓應用程式可部署至裝載在任何位置的叢集。</span><span class="sxs-lookup"><span data-stu-id="86718-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="86718-108">概觀</span><span class="sxs-lookup"><span data-stu-id="86718-108">Overview</span></span>
<span data-ttu-id="86718-109">建議透過[服務組態套件][config-package]來管理服務組態設定。</span><span class="sxs-lookup"><span data-stu-id="86718-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="86718-110">組態套件會有各種版本，並可透過含有健全狀況驗證和自動復原的受管理輪流升級來進行升級。</span><span class="sxs-lookup"><span data-stu-id="86718-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="86718-111">這是慣用的全域組態，因為可以減少全域服務中斷的機會。</span><span class="sxs-lookup"><span data-stu-id="86718-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="86718-112">加密的密碼也不例外。</span><span class="sxs-lookup"><span data-stu-id="86718-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="86718-113">Service Fabric 具有內建的功能，可使用憑證加密來加密或解密組態套件 Settings.xml 檔案中的值。</span><span class="sxs-lookup"><span data-stu-id="86718-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="86718-114">下圖說明 Service Fabric 應用程式中密碼管理的基本流程︰</span><span class="sxs-lookup"><span data-stu-id="86718-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![密碼管理概觀][overview]

<span data-ttu-id="86718-116">此流程有四個主要步驟︰</span><span class="sxs-lookup"><span data-stu-id="86718-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="86718-117">取得資料編密憑證。</span><span class="sxs-lookup"><span data-stu-id="86718-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="86718-118">在叢集中安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="86718-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="86718-119">在部署應用程式時以憑證來加密密碼的值，並將其插入服務的 Settings.xml 組態檔。</span><span class="sxs-lookup"><span data-stu-id="86718-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="86718-120">藉由以相同的編密憑證進行解密，從 Settings.xml 讀取加密的值。</span><span class="sxs-lookup"><span data-stu-id="86718-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="86718-121">[Azure Key Vault][key-vault-get-started] 在此是當做憑證的安全儲存位置，以及讓憑證安裝在 Azure 中的 Service Fabric 叢集上的方法。</span><span class="sxs-lookup"><span data-stu-id="86718-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="86718-122">如果您沒有要部署至 Azure，您不需要使用金鑰保存庫管理 Service Fabric 應用程式中的密碼。</span><span class="sxs-lookup"><span data-stu-id="86718-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="86718-123">資料編密憑證</span><span class="sxs-lookup"><span data-stu-id="86718-123">Data encipherment certificate</span></span>
<span data-ttu-id="86718-124">資料編密憑證只會用於服務的 Settings.xml 中組態值的加密與解密，並無法用來驗證或簽署密碼文字。</span><span class="sxs-lookup"><span data-stu-id="86718-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="86718-125">憑證必須符合下列要求：</span><span class="sxs-lookup"><span data-stu-id="86718-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="86718-126">憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="86718-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="86718-127">憑證必須是為了進行金鑰交換而建立，且可匯出成個人資訊交換檔 (.pfx)。</span><span class="sxs-lookup"><span data-stu-id="86718-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="86718-128">憑證的金鑰使用法必須包含資料編密 (10)，而且不應該包含伺服器驗證或用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="86718-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="86718-129">例如，當使用 PowerShell 建立自我簽署的憑證時，`KeyUsage` 旗標必須設定為 `DataEncipherment`：</span><span class="sxs-lookup"><span data-stu-id="86718-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="86718-130">在叢集中安裝憑證</span><span class="sxs-lookup"><span data-stu-id="86718-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="86718-131">此憑證必須安裝在叢集中的每個節點上。</span><span class="sxs-lookup"><span data-stu-id="86718-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="86718-132">它會用在執行階段來解密服務的 Settings.xml 中儲存的值。</span><span class="sxs-lookup"><span data-stu-id="86718-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="86718-133">請參閱[如何使用 Azure Resource Manager][service-fabric-cluster-creation-via-arm] 建立叢集的安裝指示。</span><span class="sxs-lookup"><span data-stu-id="86718-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="86718-134">加密應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="86718-134">Encrypt application secrets</span></span>
<span data-ttu-id="86718-135">Service Fabric SDK 有內建密碼加密和解密函式。</span><span class="sxs-lookup"><span data-stu-id="86718-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="86718-136">可以在建置階段加密密碼值，然後在服務代碼中以程式設計方式解密和讀取。</span><span class="sxs-lookup"><span data-stu-id="86718-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="86718-137">下列 PowerShell 命令會用來加密密碼。</span><span class="sxs-lookup"><span data-stu-id="86718-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="86718-138">此命令只會將值加密；並**不會**簽署密碼文字。</span><span class="sxs-lookup"><span data-stu-id="86718-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="86718-139">您必須使用安裝在叢集中相同的編密憑證，以產生密碼值的加密文字︰</span><span class="sxs-lookup"><span data-stu-id="86718-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="86718-140">產生的 Base-64 字串同時包含密碼的加密文字，以及用來對其加密的憑證相關資訊。</span><span class="sxs-lookup"><span data-stu-id="86718-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="86718-141">當 `IsEncrypted` 屬性設為 `true` 時，Base-64 編碼的字串可插入到服務的 Settings.xml 組態檔中的參數內：</span><span class="sxs-lookup"><span data-stu-id="86718-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="86718-142">將應用程式密碼插入應用程式執行個體內</span><span class="sxs-lookup"><span data-stu-id="86718-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="86718-143">在理想情況下，部署至不同的環境應儘可能自動化。</span><span class="sxs-lookup"><span data-stu-id="86718-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="86718-144">這可以藉由在建置環境中執行密碼加密，並在建立應用程式執行個體時提供加密的密碼做為參數來實現。</span><span class="sxs-lookup"><span data-stu-id="86718-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="86718-145">在 Settings.xml 中使用可覆寫參數</span><span class="sxs-lookup"><span data-stu-id="86718-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="86718-146">Settings.xml 組態檔允許可以在應用程式建立時提供的可覆寫參數。</span><span class="sxs-lookup"><span data-stu-id="86718-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="86718-147">使用 `MustOverride` 屬性而非提供參數的值︰</span><span class="sxs-lookup"><span data-stu-id="86718-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="86718-148">若要覆寫 Settings.xml 中的值，請宣告 ApplicationManifest.xml 中服務的覆寫參數︰</span><span class="sxs-lookup"><span data-stu-id="86718-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="86718-149">現在可以在建立應用程式執行個體時，將值指定為「應用程式參數」  。</span><span class="sxs-lookup"><span data-stu-id="86718-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="86718-150">可以使用 PowerShell 編寫指令碼 (或以 C# 撰寫) 來建立應用程式執行個體，使其在建置流程中很容易整合。</span><span class="sxs-lookup"><span data-stu-id="86718-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="86718-151">若使用 PowerShell，則參數會提供給 `New-ServiceFabricApplication` 命令當做 [雜湊表](https://technet.microsoft.com/library/ee692803.aspx)：</span><span class="sxs-lookup"><span data-stu-id="86718-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="86718-152">若使用 C#，則應用程式參數在 `ApplicationDescription` 中會指定為 `NameValueCollection`：</span><span class="sxs-lookup"><span data-stu-id="86718-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="86718-153">解密來自服務代碼的密碼</span><span class="sxs-lookup"><span data-stu-id="86718-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="86718-154">Service Fabric 中的服務在「網路服務」下依預設是在 Windows 上執行，而且若沒有額外設定，則沒有安裝在節點上憑證的存取權。</span><span class="sxs-lookup"><span data-stu-id="86718-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="86718-155">使用資料編密憑證時，您必須確定「網路服務」或服務在其下執行的任何使用者帳戶，可以存取憑證的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="86718-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="86718-156">若您如此設定，Service Fabric 會自動處理授與服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="86718-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="86718-157">可以藉由定義使用者及憑證的安全性原則，在 ApplicationManifest.xml 中完成此組態。</span><span class="sxs-lookup"><span data-stu-id="86718-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="86718-158">在下列範例中，已授與「網路服務」帳戶由其憑證指紋所定義的憑證讀取權限︰</span><span class="sxs-lookup"><span data-stu-id="86718-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="86718-159">當從 Windows 上的憑證存放區嵌入式管理單元中複製憑證指紋時，在憑證指紋字串的開頭會放置不可見的字元。</span><span class="sxs-lookup"><span data-stu-id="86718-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="86718-160">嘗試按憑證指紋尋找憑證時，這個不可見的字元可能會導致錯誤，因此請務必刪除這個額外的字元。</span><span class="sxs-lookup"><span data-stu-id="86718-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="86718-161">在服務代碼中使用應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="86718-161">Use application secrets in service code</span></span>
<span data-ttu-id="86718-162">存取來自組態套件中 Settings.xml 組態值的 API，可輕鬆解密將 `IsEncrypted` 屬性設為 `true` 的值。</span><span class="sxs-lookup"><span data-stu-id="86718-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="86718-163">由於加密的文字包含用於加密的憑證相關資訊，因此您不需要手動尋找憑證。</span><span class="sxs-lookup"><span data-stu-id="86718-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="86718-164">只需要在執行服務的節點上安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="86718-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="86718-165">只要呼叫 `DecryptValue()` 方法來擷取原始的密碼值︰</span><span class="sxs-lookup"><span data-stu-id="86718-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="86718-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86718-166">Next Steps</span></span>
<span data-ttu-id="86718-167">深入了解 [以不同的安全性權限執行應用程式](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="86718-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
