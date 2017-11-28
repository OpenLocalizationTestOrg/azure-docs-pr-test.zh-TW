---
title: "金鑰保存庫 .NET 2.x API 版本資訊 | Microsoft Docs"
description: ".NET 開發人員會使用這個 API 來編寫 Azure 金鑰保存庫的程式碼"
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
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="f6762-103">Azure 金鑰保存庫 .NET 2.0 - 版本資訊和移轉指南</span><span class="sxs-lookup"><span data-stu-id="f6762-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="f6762-104">下列資訊和指引適用於使用 Azure Key Vault .NET/C# 程式庫的開發人員。</span><span class="sxs-lookup"><span data-stu-id="f6762-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="f6762-105">從 1.0 版轉換為 2.0 版時，進行的數個更新需要程式碼中的移轉工作，您才能受益於功能改進和功能新增 (例如 **Key Vault 憑證**支援)。</span><span class="sxs-lookup"><span data-stu-id="f6762-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="f6762-106">Key Vault 憑證</span><span class="sxs-lookup"><span data-stu-id="f6762-106">Key Vault certificates</span></span>

<span data-ttu-id="f6762-107">金鑰保存庫憑證支援提供管理 x509 憑證和下列行為︰</span><span class="sxs-lookup"><span data-stu-id="f6762-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="f6762-108">允許憑證擁有者透過金鑰保存庫建立程序或匯入現有憑證來建立憑證。</span><span class="sxs-lookup"><span data-stu-id="f6762-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="f6762-109">這同時包含自我簽署和憑證授權單位所產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="f6762-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="f6762-110">允許金鑰保存庫憑證擁有者實作 X509 憑證的安全儲存和管理，而不需要與私密金鑰資料互動。</span><span class="sxs-lookup"><span data-stu-id="f6762-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="f6762-111">允許憑證擁有者建立原則，以指示金鑰保存庫管理憑證的生命週期。</span><span class="sxs-lookup"><span data-stu-id="f6762-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="f6762-112">允許憑證擁有者提供有關憑證到期和更新生命週期事件的通知的連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="f6762-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="f6762-113">支援與所選簽發者的自動更新 - 金鑰保存庫夥伴 X509 憑證提供者/憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="f6762-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="f6762-114">請注意 - 也允許無合作關係的提供者/授權單位，但不支援自動更新功能。</span><span class="sxs-lookup"><span data-stu-id="f6762-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="f6762-115">.NET 支援</span><span class="sxs-lookup"><span data-stu-id="f6762-115">.NET support</span></span>

* <span data-ttu-id="f6762-116">Azure 金鑰保存庫 .NET/C# 程式庫 2.0 版不支援 **.NET 4.0**</span><span class="sxs-lookup"><span data-stu-id="f6762-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="f6762-117">Azure 金鑰保存庫 .NET/C# 程式庫 2.0 版支援 **.NET Core**</span><span class="sxs-lookup"><span data-stu-id="f6762-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="f6762-118">命名空間</span><span class="sxs-lookup"><span data-stu-id="f6762-118">Namespaces</span></span>

* <span data-ttu-id="f6762-119">**模型**的命名空間會從 **Microsoft.Azure.KeyVault** 變更為 **Microsoft.Azure.KeyVault.Models**。</span><span class="sxs-lookup"><span data-stu-id="f6762-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="f6762-120">卸除 **Microsoft.Azure.KeyVault.Internal** 命名空間。</span><span class="sxs-lookup"><span data-stu-id="f6762-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="f6762-121">Azure SDK 相依性命名空間會從 **Hyak.Common** 和 **Hyak.Common.Internals** 變更為 **Microsoft.Rest** 和 **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="f6762-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="f6762-122">類型變更</span><span class="sxs-lookup"><span data-stu-id="f6762-122">Type changes</span></span>

* <span data-ttu-id="f6762-123">*Secret* 已變更為 *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="f6762-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="f6762-124">*Dictionary* 已變更為 *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="f6762-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="f6762-125">*List<T>, string []* 已變更為 *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="f6762-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="f6762-126">*NextList* 已變更為 *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="f6762-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="f6762-127">傳回類型</span><span class="sxs-lookup"><span data-stu-id="f6762-127">Return types</span></span>

* <span data-ttu-id="f6762-128">**KeyList** 和 **SecretList** 將傳回 *IPage<T>*，而非 *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="f6762-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="f6762-129">產生的 **BackupKeyAsync** 將會傳回 *BackupKeyResult*，其包含 *Value* (備份 Blob)。</span><span class="sxs-lookup"><span data-stu-id="f6762-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="f6762-130">包裝方法之前，只會傳回值。</span><span class="sxs-lookup"><span data-stu-id="f6762-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="f6762-131">例外狀況</span><span class="sxs-lookup"><span data-stu-id="f6762-131">Exceptions</span></span>

* <span data-ttu-id="f6762-132">*KeyVaultClientException* 變更為 *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="f6762-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="f6762-133">服務錯誤會從 *exception.Error* 變更為 *exception.Body.Error.Message*。</span><span class="sxs-lookup"><span data-stu-id="f6762-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="f6762-134">已移除 **[JsonExtensionData]** 的錯誤訊息中的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="f6762-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="f6762-135">建構函式</span><span class="sxs-lookup"><span data-stu-id="f6762-135">Constructors</span></span>

* <span data-ttu-id="f6762-136">建構函式只會接受 *HttpClientHandler* 或 *DelegatingHandler[]*，而不是接受 *HttpClient* 做為建構函式引數。</span><span class="sxs-lookup"><span data-stu-id="f6762-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="f6762-137">下載的套件</span><span class="sxs-lookup"><span data-stu-id="f6762-137">Downloaded packages</span></span>

<span data-ttu-id="f6762-138">用戶端正在處理與金鑰保存庫的相依性時，會下載下列項目：</span><span class="sxs-lookup"><span data-stu-id="f6762-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="f6762-139">先前的套件清單</span><span class="sxs-lookup"><span data-stu-id="f6762-139">Previous package list</span></span>

* <span data-ttu-id="f6762-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="f6762-148">目前套件清單</span><span class="sxs-lookup"><span data-stu-id="f6762-148">Current package list</span></span>

* <span data-ttu-id="f6762-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="f6762-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="f6762-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="f6762-152">類別變更</span><span class="sxs-lookup"><span data-stu-id="f6762-152">Class changes</span></span>

* <span data-ttu-id="f6762-153">已移除 **UnixEpoch** 類別</span><span class="sxs-lookup"><span data-stu-id="f6762-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="f6762-154">**Base64UrlConverter** 類別已重新命名為 **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="f6762-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="f6762-155">其他變更</span><span class="sxs-lookup"><span data-stu-id="f6762-155">Other changes</span></span>

* <span data-ttu-id="f6762-156">這個版本的 API 已新增暫時性失敗的 KV 作業重試原則組態支援。</span><span class="sxs-lookup"><span data-stu-id="f6762-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="f6762-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="f6762-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="f6762-158">針對傳回 *vault* 的作業，傳回類型是包含 Vault 屬性的類別。</span><span class="sxs-lookup"><span data-stu-id="f6762-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="f6762-159">傳回類型現在是 *Vault*。</span><span class="sxs-lookup"><span data-stu-id="f6762-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="f6762-160">*PermissionsToKeys* 和 *PermissionsToSecrets* 現在是 *Permissions.Keys* 和 *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="f6762-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="f6762-161">部分傳回類型變更也會套用至控制平面。</span><span class="sxs-lookup"><span data-stu-id="f6762-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="f6762-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="f6762-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="f6762-163">套件最多分成 **Microsoft.Azure.KeyVault.Extensions** 和 **Microsoft.Azure.KeyVault.Cryptography** 來進行密碼編譯作業。</span><span class="sxs-lookup"><span data-stu-id="f6762-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

