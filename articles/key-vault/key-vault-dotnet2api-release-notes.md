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
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Azure 金鑰保存庫 .NET 2.0 - 版本資訊和移轉指南
hello 下列資訊和指導方針適用於開發人員使用 Azure 金鑰保存庫.NET / C# 程式庫。 從 toohello 2.0 版的 hello 1.0 版的 hello 轉換中的更新數目所做的就是需要您為了讓 toobenefit 從 hello 功能改進的程式碼中的移轉工作，而且這類功能新增**金鑰保存庫憑證**支援。

## <a name="key-vault-certificates"></a>Key Vault 憑證

金鑰保存庫憑證支援提供的管理您的 x509 憑證和 hello 下列行為：  

* 可讓憑證擁有者 toocreate 透過金鑰保存庫建立程序或 hello 匯入現有憑證的憑證。 這同時包含自我簽署和憑證授權單位所產生的憑證。
* 可讓金鑰保存庫憑證擁有者 tooimplement 安全儲存和管理的 X509 憑證沒有私密金鑰與互動。  
* 可讓憑證擁有者 toocreate 原則，以指示金鑰保存庫 toomanage hello 生命週期的憑證。  
* 允許認證的擁有者 tooprovide 與連絡資訊告知生命週期事件的相關到期憑證的更新。  
* 支援與所選簽發者的自動更新 - 金鑰保存庫夥伴 X509 憑證提供者/憑證授權單位。
  
  * 請注意-非建立合作關係的提供者/授權單位會也允許，但不是支援 hello 自動更新功能。

## <a name="net-support"></a>.NET 支援

* **.NET 4.0** hello 2.0 版的 hello Azure 金鑰保存庫.NET 不支援 / C# 程式庫
* **.NET core**受到 hello 2.0 版的 hello Azure 金鑰保存庫.NET / C# 程式庫

## <a name="namespaces"></a>命名空間

* hello 命名空間**模型**已從**Microsoft.Azure.KeyVault**太**Microsoft.Azure.KeyVault.Models**。
* hello **Microsoft.Azure.KeyVault.Internal**卸除命名空間。
* hello Azure SDK 的相依性命名空間變更**Hyak.Common**和**Hyak.Common.Internals**太**Microsoft.Rest**和**Microsoft.Rest.Serialization**

## <a name="type-changes"></a>類型變更

* *密碼*變更太*SecretBundle*
* *字典*變更太*IDictionary*
* *清單<T>，string []*變更太*IList<T>*
* *NextList*變更太*NextPageLink*

## <a name="return-types"></a>傳回類型

* **KeyList** 和 **SecretList** 將傳回 *IPage<T>*，而非 *ListKeysResponseMessage*
* 產生的 hello **BackupKeyAsync**會傳回*BackupKeyResult*包含*值*(備份 blob)。 之前 hello 方法就是包裝並傳回唯一的 hello 值。

## <a name="exceptions"></a>例外狀況

* *KeyVaultClientException*太變更*KeyVaultErrorException*
* 從變更 hello 服務錯誤*例外狀況。錯誤*太*例外狀況。Body.Error.Message*。
* 移除 hello 錯誤訊息，取得其他資訊**[JsonExtensionData]**。

## <a name="constructors"></a>建構函式

* 而不是接受*HttpClient*做為建構函式引數，hello 建構函式只接受*HttpClientHandler*或*DelegatingHandler []*。

## <a name="downloaded-packages"></a>下載的套件

金鑰保存庫 hello 下列用戶端上處理的相依性時已下載

### <a name="previous-package-list"></a>先前的套件清單

* package id="Hyak.Common" version="1.0.2" targetFramework="net45"
* package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"
* package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"
* package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"
* package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>目前套件清單

* package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>類別變更

* 已移除 **UnixEpoch** 類別
* **Base64UrlConverter**類別已重新命名過**Base64UrlJsonConverter**

## <a name="other-changes"></a>其他變更

* 已新增 toothis 版的 hello API KV 作業重試原則的暫時性失敗的 hello 組態的支援。

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* 傳回的 hello 作業*保存庫*，hello 傳回型別是包含保存庫屬性的類別。 hello 傳回型別是現在*保存庫*。
* *PermissionsToKeys* 和 *PermissionsToSecrets* 現在是 *Permissions.Keys* 和 *Permissions.Secrets*
* 某些 hello 傳回類型的變更將套用 toohello 控制平面以及。

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* hello 封裝太分解**Microsoft.Azure.KeyVault.Extensions**和**Microsoft.Azure.KeyVault.Cryptography** hello 密碼編譯作業。

