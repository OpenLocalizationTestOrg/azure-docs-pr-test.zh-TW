---
title: "aaaAzure 金鑰保存庫開發人員指南"
description: "開發人員可以使用 Azure 金鑰保存庫 hello Microsoft Azure 環境內 toomanage 密碼編譯金鑰。"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Azure 金鑰保存庫開發人員指南

金鑰保存庫可讓您 toosecurely 存取機密資訊從應用程式中：

- 而不需要自行 toowrite hello 程式碼保護金鑰和密碼，而且您可以輕鬆地 toouse 它們從您的應用程式。
- 您可以 toohave 您自己的客戶而且管理他們自己的金鑰，讓您可以專注於提供 hello 核心軟體功能。 如此一來，您的應用程式將會擁有 hello 責任或潛在客戶的租用戶金鑰和密碼的責任。
- 您的應用程式可以使用金鑰來簽署和加密尚未保留 hello 金鑰管理您的應用程式，讓您的方案 toobe 適合做為地理位置分散的應用程式從外部。
- 如同 hello 2016 年 9 月版的金鑰保存庫，您的應用程式現在可以使用金鑰保存庫[憑證](https://docs.microsoft.com/rest/api/keyvault/certificate-operations)。 如需詳細資訊，請參閱[關於金鑰、祕密和憑證](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates)。

如需 Azure 金鑰保存庫的一般詳細資訊，請參閱 [什麼是金鑰保存庫？](key-vault-whatis.md)。

## <a name="public-previews"></a>公開預覽

我們會定期發行新 Key Vault 功能的公開預覽。 請試試看，然後透過我們的意見反應電子郵件地址 azurekeyvault@microsoft.com，讓我們知道您的想法。

### <a name="storage-account-keys---july-10-2017"></a>儲存體帳戶金鑰 - 2017 年 7 月 10 日

>[!NOTE]
>此更新的 Azure 金鑰保存庫的唯一 hello**儲存體帳戶金鑰**功能處於預覽狀態。

此預覽版包含新的 [儲存體帳戶金鑰] 功能，可透過下列介面提供：[.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/)、[REST](https://docs.microsoft.com/rest/api/keyvault/) 和 [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/)。 

如需有關 hello 新儲存體帳戶金鑰功能的詳細資訊，請參閱[Azure 金鑰保存庫儲存體帳戶金鑰概觀](key-vault-ovw-storage-keys.md)。

## <a name="videos"></a>影片

這部影片示範如何 toocreate 您自己的金鑰保存庫以及如何 toouse 從 hello ' Hello 金鑰保存庫 」 範例應用程式。

- [Key Vault 開發人員 - 快速入門指南](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

以上影片中所提及的資源︰

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Azure 金鑰保存庫範例程式碼](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>建立及管理金鑰保存庫

之前使用 Azure 金鑰保存庫在程式碼中，您可以建立並管理保存庫，透過 REST、 資源管理員範本、 PowerShell 或 CLI hello 下列文章中所述：

- [使用 REST 建立和管理金鑰保存庫](https://docs.microsoft.com/rest/api/keyvault/)
- [使用 PowerShell 建立和管理金鑰保存庫](key-vault-get-started.md)
- [使用 CLI 建立和管理金鑰保存庫](key-vault-manage-with-cli2.md)
- [透過 Azure Resource Manager 範本建立金鑰保存庫和新增祕密](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> 涉及金鑰保存庫的作業乃透過 AAD 進行驗證，以及透過金鑰保存庫自己的存取原則 (每個保存庫有各自的定義) 進行授權。

## <a name="coding-with-key-vault"></a>撰寫金鑰保存庫的程式碼

hello 程式設計人員的金鑰保存庫管理系統是由數個介面，與為 hello 基礎的其餘部分所組成。 Hello REST 介面，透過您金鑰保存庫的資源都可存取;金鑰、 密碼和憑證。 [Key Vault REST API 參考](https://docs.microsoft.com/rest/api/keyvault/)。 

### <a name="supported-programming-languages"></a>支援的程式設計語言

#### <a name="net"></a>.NET

- [Key Vault 的 .NET API 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

如需有關 hello 2.x 版的 hello.NET SDK 的詳細資訊，請參閱 hello[版本資訊](key-vault-dotnet2api-release-notes.md)。

#### <a name="java"></a>Java

- [Key Vault 的 Java SDK](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

在 Node.js hello 保存庫管理 API 和 hello 保存庫的物件 API 不同。 Key Vault 管理可建立及更新您的 Key Vault。 Key Vault 作業 API 適用於金鑰、密碼和憑證等保存庫物件。 

- [Key Vault 管理的 Node.js API 參考](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Key Vault 作業的 Node.js API 參考](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>快速入門

- [建立金鑰保存庫](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [開始在 Node.js 中使用 Key Vault](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>程式碼範例

如需搭配使用金鑰保存庫和應用程式的完整範例，請參閱︰

- [Azure Key Vault 程式碼範例](http://www.microsoft.com/download/details.aspx?id=45343) - .NET 範例應用程式 HelloKeyVault 和 Azure Web 服務範例。 
- [使用 Azure 金鑰保存庫的 Web 應用程式](key-vault-use-from-web-application.md)-教學課程 toohelp 您學習如何 toouse Azure 金鑰保存庫在 Azure 中的 web 應用程式。 

## <a name="how-tos"></a>作法

hello 下列文章和案例提供使用 Azure 金鑰保存庫的特定工作的指引：

- [訂用帳戶之後變更金鑰保存庫租用戶識別碼移動](key-vault-subscription-move-fix.md)-當您從租用戶 B tootenant 移動您的 Azure 訂用帳戶，您現有的金鑰保存庫都無法存取的 hello 主體 （使用者和應用程式） 租用戶 b 修正此使用本指南中。
- [存取金鑰保存庫位於防火牆後方](key-vault-access-behind-firewall.md)-tooaccess 金鑰保存庫您金鑰保存庫用戶端應用程式需求 toobe 無法 tooaccess 多個端點的各種不同功能。
- [如何 tooGenerate 和 Azure 金鑰保存庫金鑰 Transfer HSM-Protected](key-vault-hsm-protected-keys.md) -這可協助您規劃、 產生和然後再將您自己的 HSM 保護的金鑰 toouse 使用 Azure 金鑰保存庫。
- [Toopass 如何保護 （例如密碼） 的值在部署期間](../azure-resource-manager/resource-manager-keyvault-parameter.md)-當您需要做為參數 toopass 安全的值 （例如密碼） 在部署期間，您可以儲存該值做為另一個 Azure 金鑰保存庫和參考 hello 值中的密碼資源管理員範本。
- [如何與 SQL Server 的可延伸金鑰管理的金鑰保存庫 toouse](https://msdn.microsoft.com/library/dn198405.aspx) -hello Azure 金鑰保存庫可讓 SQL Server 和 SQL 中-a-VM tooleverage hello Azure 金鑰保存庫服務作為 Extensible Key Management (EKM) 提供者的 SQL Server Connectortooprotect 其加密金鑰的應用程式連結。透明資料加密、 備份的加密和資料行層級加密。
- [如何從金鑰保存庫 toodeploy 憑證 tooVMs](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) -在 VM 中 Azure 需要憑證的執行的雲端應用程式。 現在應如何讓此憑證進入此 VM？
- [如何結束 tooend 與金鑰保存庫註冊 tooset 金鑰旋轉和稽核](key-vault-key-rotation-log-monitoring.md)-此逐步解說如何 tooset 金鑰輪替和使用 Azure 金鑰保存庫稽核。
- [透過金鑰保存庫部署 Azure Web 應用程式憑證]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)提供逐步指示，以便將儲存在金鑰保存庫的憑證部署為 [App Service 憑證](https://azure.microsoft.com/blog/internals-of-app-service-certificate/)供應項目的一部分。
- [授與權限 toomany 應用程式 tooaccess 金鑰保存庫](key-vault-group-permissions-for-apps.md)金鑰保存庫的存取控制原則只支援 16 的項目。 不過，您可以建立 Azure Active Directory 安全性群組。 加入所有 hello 建立關聯的服務主體 toothis 安全性群組，然後授與存取 toothis 安全性群組 tooKey 保存庫。
- 如需整合及搭配使用金鑰保存庫和 Azure 的具體工作指引，請參閱 [Ryan Jones 的金鑰保存庫 Azure Resource Manager 範本範例](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)。
- [如何 toouse 金鑰保存庫虛刪除與 CLI](key-vault-soft-delete-cli.md)會引導您完成使用 hello 和金鑰保存庫和金鑰保存庫的各種物件的生命週期與啟用虛刪除。
- [如何 toouse 金鑰保存庫虛刪除使用 PowerShell](key-vault-soft-delete-powershell.md)會引導您完成使用 hello 和金鑰保存庫和金鑰保存庫的各種物件的生命週期與啟用虛刪除。

## <a name="integrated-with-key-vault"></a>與金鑰保存庫整合

這些文章是關於其他可讓我們使用及整合 Key Vault 的案例和服務。

- [Azure 磁碟加密](../security/azure-security-disk-encryption.md)利用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello OS 與 hello 資料 Linux tooprovide 磁碟區加密的功能磁碟。 您控制和管理 hello 磁碟加密金鑰和秘密中您金鑰保存庫的訂用帳戶，同時確保 hello 虛擬機器磁碟中的所有資料會留在您 Azure 儲存體都加密的 Azure 金鑰保存庫 toohelp 整合 hello 方案。
- [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)提供加密的資料會儲存在 hello 帳戶的選項。 金鑰管理，資料湖存放區會用於管理您所需的解密儲存在 hello 資料湖存放區中的任何資料的主要加密金鑰 (MEKs)，提供兩種模式。 您可以讓資料湖存放區 hello MEKs 管理，或選擇使用 Azure 金鑰保存庫帳戶 hello MEKs tooretain 擁有權。 您建立 Data Lake Store 帳戶時指定金鑰管理的 hello 的模式。 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) toomanager 可讓您自己的租用戶金鑰。 例如，而不是 Microsoft 管理租用戶金鑰 （hello 預設值），您可以管理您自己的租用戶金鑰 toocomply 套用 tooyour 組織的特定法規。 管理您自己的租用戶金鑰也會參照的 tooas 整合您自己的金鑰或 BYOK。

## <a name="key-vault-overviews-and-concepts"></a>Key Vault 的概觀和概念

- [金鑰保存庫虛刪除行為](key-vault-ovw-soft-delete.md)hello 刪除是否意外或故意情況下，描述功能，可復原已刪除的物件。
- [金鑰保存庫用戶端節流](key-vault-ovw-throttling.md)將您導向 toohello 節流的基本概念，並提供您的應用程式的方法。
- [金鑰保存庫儲存體帳戶金鑰概觀](key-vault-ovw-storage-keys.md)描述 hello 金鑰保存庫整合 Azure 儲存體帳戶金鑰。
- [金鑰保存庫安全園地](key-vault-ovw-security-worlds.md)描述 hello 地區和安全性區域之間的關聯性。

## <a name="social"></a>社交

- [Key Vault Blog (金鑰保存庫部落格)](http://aka.ms/kvblog)
- [Key Vault Forum (金鑰保存庫論壇)](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>支援程式庫

- [Microsoft Azure Key Vault 核心程式庫](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core)提供 **IKey** 和 **IKeyResolver** 介面，以從識別碼找出金鑰和使用金鑰執行作業。
- [Microsoft Azure 金鑰保存庫擴充](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions)提供 Azure 金鑰保存庫的擴充功能。


