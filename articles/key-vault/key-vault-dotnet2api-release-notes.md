---
title: "aaaKey 保存庫.NET 2.x 應用程式開發介面版本資訊 |Microsoft 文件"
description: ".NET 開發人員使用此 API toocode for Azure Key Vault"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="39708-103">Azure 金鑰保存庫 .NET 2.0 - 版本資訊和移轉指南</span><span class="sxs-lookup"><span data-stu-id="39708-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="39708-104">hello 下列資訊和指導方針適用於開發人員使用 Azure 金鑰保存庫.NET / C# 程式庫。</span><span class="sxs-lookup"><span data-stu-id="39708-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="39708-105">從 toohello 2.0 版的 hello 1.0 版的 hello 轉換中的更新數目所做的就是需要您為了讓 toobenefit 從 hello 功能改進的程式碼中的移轉工作，而且這類功能新增**金鑰保存庫憑證**支援。</span><span class="sxs-lookup"><span data-stu-id="39708-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="39708-106">Key Vault 憑證</span><span class="sxs-lookup"><span data-stu-id="39708-106">Key Vault certificates</span></span>

<span data-ttu-id="39708-107">金鑰保存庫憑證支援提供的管理您的 x509 憑證和 hello 下列行為：</span><span class="sxs-lookup"><span data-stu-id="39708-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="39708-108">可讓憑證擁有者 toocreate 透過金鑰保存庫建立程序或 hello 匯入現有憑證的憑證。</span><span class="sxs-lookup"><span data-stu-id="39708-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="39708-109">這同時包含自我簽署和憑證授權單位所產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="39708-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="39708-110">可讓金鑰保存庫憑證擁有者 tooimplement 安全儲存和管理的 X509 憑證沒有私密金鑰與互動。</span><span class="sxs-lookup"><span data-stu-id="39708-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="39708-111">可讓憑證擁有者 toocreate 原則，以指示金鑰保存庫 toomanage hello 生命週期的憑證。</span><span class="sxs-lookup"><span data-stu-id="39708-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="39708-112">允許認證的擁有者 tooprovide 與連絡資訊告知生命週期事件的相關到期憑證的更新。</span><span class="sxs-lookup"><span data-stu-id="39708-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="39708-113">支援與所選簽發者的自動更新 - 金鑰保存庫夥伴 X509 憑證提供者/憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="39708-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="39708-114">請注意-非建立合作關係的提供者/授權單位會也允許，但不是支援 hello 自動更新功能。</span><span class="sxs-lookup"><span data-stu-id="39708-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="39708-115">.NET 支援</span><span class="sxs-lookup"><span data-stu-id="39708-115">.NET support</span></span>

* <span data-ttu-id="39708-116">**.NET 4.0** hello 2.0 版的 hello Azure 金鑰保存庫.NET 不支援 / C# 程式庫</span><span class="sxs-lookup"><span data-stu-id="39708-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="39708-117">**.NET core**受到 hello 2.0 版的 hello Azure 金鑰保存庫.NET / C# 程式庫</span><span class="sxs-lookup"><span data-stu-id="39708-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="39708-118">命名空間</span><span class="sxs-lookup"><span data-stu-id="39708-118">Namespaces</span></span>

* <span data-ttu-id="39708-119">hello 命名空間**模型**已從**Microsoft.Azure.KeyVault**太**Microsoft.Azure.KeyVault.Models**。</span><span class="sxs-lookup"><span data-stu-id="39708-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="39708-120">hello **Microsoft.Azure.KeyVault.Internal**卸除命名空間。</span><span class="sxs-lookup"><span data-stu-id="39708-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="39708-121">hello Azure SDK 的相依性命名空間變更**Hyak.Common**和**Hyak.Common.Internals**太**Microsoft.Rest**和**Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="39708-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="39708-122">類型變更</span><span class="sxs-lookup"><span data-stu-id="39708-122">Type changes</span></span>

* <span data-ttu-id="39708-123">*密碼*變更太*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="39708-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="39708-124">*字典*變更太*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="39708-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="39708-125">*清單<T>，string []*變更太*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="39708-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="39708-126">*NextList*變更太*NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="39708-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="39708-127">傳回類型</span><span class="sxs-lookup"><span data-stu-id="39708-127">Return types</span></span>

* <span data-ttu-id="39708-128">**KeyList** 和 **SecretList** 將傳回 *IPage<T>*，而非 *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="39708-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="39708-129">產生的 hello **BackupKeyAsync**會傳回*BackupKeyResult*包含*值*(備份 blob)。</span><span class="sxs-lookup"><span data-stu-id="39708-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="39708-130">之前 hello 方法就是包裝並傳回唯一的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="39708-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="39708-131">例外狀況</span><span class="sxs-lookup"><span data-stu-id="39708-131">Exceptions</span></span>

* <span data-ttu-id="39708-132">*KeyVaultClientException*太變更*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="39708-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="39708-133">從變更 hello 服務錯誤*例外狀況。錯誤*太*例外狀況。Body.Error.Message*。</span><span class="sxs-lookup"><span data-stu-id="39708-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="39708-134">移除 hello 錯誤訊息，取得其他資訊**[JsonExtensionData]**。</span><span class="sxs-lookup"><span data-stu-id="39708-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="39708-135">建構函式</span><span class="sxs-lookup"><span data-stu-id="39708-135">Constructors</span></span>

* <span data-ttu-id="39708-136">而不是接受*HttpClient*做為建構函式引數，hello 建構函式只接受*HttpClientHandler*或*DelegatingHandler []*。</span><span class="sxs-lookup"><span data-stu-id="39708-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="39708-137">下載的套件</span><span class="sxs-lookup"><span data-stu-id="39708-137">Downloaded packages</span></span>

<span data-ttu-id="39708-138">金鑰保存庫 hello 下列用戶端上處理的相依性時已下載</span><span class="sxs-lookup"><span data-stu-id="39708-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="39708-139">先前的套件清單</span><span class="sxs-lookup"><span data-stu-id="39708-139">Previous package list</span></span>

* <span data-ttu-id="39708-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="39708-148">目前套件清單</span><span class="sxs-lookup"><span data-stu-id="39708-148">Current package list</span></span>

* <span data-ttu-id="39708-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="39708-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="39708-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="39708-152">類別變更</span><span class="sxs-lookup"><span data-stu-id="39708-152">Class changes</span></span>

* <span data-ttu-id="39708-153">已移除 **UnixEpoch** 類別</span><span class="sxs-lookup"><span data-stu-id="39708-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="39708-154">**Base64UrlConverter**類別已重新命名過**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="39708-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="39708-155">其他變更</span><span class="sxs-lookup"><span data-stu-id="39708-155">Other changes</span></span>

* <span data-ttu-id="39708-156">已新增 toothis 版的 hello API KV 作業重試原則的暫時性失敗的 hello 組態的支援。</span><span class="sxs-lookup"><span data-stu-id="39708-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="39708-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="39708-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="39708-158">傳回的 hello 作業*保存庫*，hello 傳回型別是包含保存庫屬性的類別。</span><span class="sxs-lookup"><span data-stu-id="39708-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="39708-159">hello 傳回型別是現在*保存庫*。</span><span class="sxs-lookup"><span data-stu-id="39708-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="39708-160">*PermissionsToKeys* 和 *PermissionsToSecrets* 現在是 *Permissions.Keys* 和 *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="39708-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="39708-161">某些 hello 傳回類型的變更將套用 toohello 控制平面以及。</span><span class="sxs-lookup"><span data-stu-id="39708-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="39708-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="39708-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="39708-163">hello 封裝太分解**Microsoft.Azure.KeyVault.Extensions**和**Microsoft.Azure.KeyVault.Cryptography** hello 密碼編譯作業。</span><span class="sxs-lookup"><span data-stu-id="39708-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

