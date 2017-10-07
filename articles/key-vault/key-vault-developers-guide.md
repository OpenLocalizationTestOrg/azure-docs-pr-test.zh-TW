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
# <a name="azure-key-vault-developers-guide"></a><span data-ttu-id="0b7e8-103">Azure 金鑰保存庫開發人員指南</span><span class="sxs-lookup"><span data-stu-id="0b7e8-103">Azure Key Vault Developer's Guide</span></span>

<span data-ttu-id="0b7e8-104">金鑰保存庫可讓您 toosecurely 存取機密資訊從應用程式中：</span><span class="sxs-lookup"><span data-stu-id="0b7e8-104">Key Vault allows you toosecurely access sensitive information from within your applications:</span></span>

- <span data-ttu-id="0b7e8-105">而不需要自行 toowrite hello 程式碼保護金鑰和密碼，而且您可以輕鬆地 toouse 它們從您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-105">Keys and secrets are protected without having toowrite hello code yourself and you are easily able toouse them from your applications.</span></span>
- <span data-ttu-id="0b7e8-106">您可以 toohave 您自己的客戶而且管理他們自己的金鑰，讓您可以專注於提供 hello 核心軟體功能。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-106">You are able toohave your customers own and manage their own keys so you can concentrate on providing hello core software features.</span></span> <span data-ttu-id="0b7e8-107">如此一來，您的應用程式將會擁有 hello 責任或潛在客戶的租用戶金鑰和密碼的責任。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-107">In this way, your applications will not own hello responsibility or potential liability for your customers’ tenant keys and secrets.</span></span>
- <span data-ttu-id="0b7e8-108">您的應用程式可以使用金鑰來簽署和加密尚未保留 hello 金鑰管理您的應用程式，讓您的方案 toobe 適合做為地理位置分散的應用程式從外部。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-108">Your application can use keys for signing and encryption yet keeps hello key management external from your application, allowing your solution toobe suitable as a geographically distributed app.</span></span>
- <span data-ttu-id="0b7e8-109">如同 hello 2016 年 9 月版的金鑰保存庫，您的應用程式現在可以使用金鑰保存庫[憑證](https://docs.microsoft.com/rest/api/keyvault/certificate-operations)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-109">As of hello September 2016 release of Key Vault, your applications can now use Key Vault [certificates](https://docs.microsoft.com/rest/api/keyvault/certificate-operations).</span></span> <span data-ttu-id="0b7e8-110">如需詳細資訊，請參閱[關於金鑰、祕密和憑證](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-110">For more information, see [About keys, secrets, and certificates](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).</span></span>

<span data-ttu-id="0b7e8-111">如需 Azure 金鑰保存庫的一般詳細資訊，請參閱 [什麼是金鑰保存庫？](key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-111">For more general information on Azure Key Vault, see [What is Key Vault](key-vault-whatis.md).</span></span>

## <a name="public-previews"></a><span data-ttu-id="0b7e8-112">公開預覽</span><span class="sxs-lookup"><span data-stu-id="0b7e8-112">Public Previews</span></span>

<span data-ttu-id="0b7e8-113">我們會定期發行新 Key Vault 功能的公開預覽。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-113">Periodically, we release a public preview of a new Key Vault feature.</span></span> <span data-ttu-id="0b7e8-114">請試試看，然後透過我們的意見反應電子郵件地址 azurekeyvault@microsoft.com，讓我們知道您的想法。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-114">Please try out these and let us know what you think via azurekeyvault@microsoft.com, our feedback email address.</span></span>

### <a name="storage-account-keys---july-10-2017"></a><span data-ttu-id="0b7e8-115">儲存體帳戶金鑰 - 2017 年 7 月 10 日</span><span class="sxs-lookup"><span data-stu-id="0b7e8-115">Storage Account Keys - July 10, 2017</span></span>

>[!NOTE]
><span data-ttu-id="0b7e8-116">此更新的 Azure 金鑰保存庫的唯一 hello**儲存體帳戶金鑰**功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-116">For this update of Azure Key Vault only hello **Storage Account Keys** feature is in preview.</span></span>

<span data-ttu-id="0b7e8-117">此預覽版包含新的 [儲存體帳戶金鑰] 功能，可透過下列介面提供：[.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/)、[REST](https://docs.microsoft.com/rest/api/keyvault/) 和 [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-117">This preview includes our new Storage Account Keys feature, available through these interfaces; [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) and [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/).</span></span> 

<span data-ttu-id="0b7e8-118">如需有關 hello 新儲存體帳戶金鑰功能的詳細資訊，請參閱[Azure 金鑰保存庫儲存體帳戶金鑰概觀](key-vault-ovw-storage-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-118">For more information on hello new Storage Account Keys feature, see [Azure Key Vault storage account keys overview](key-vault-ovw-storage-keys.md).</span></span>

## <a name="videos"></a><span data-ttu-id="0b7e8-119">影片</span><span class="sxs-lookup"><span data-stu-id="0b7e8-119">Videos</span></span>

<span data-ttu-id="0b7e8-120">這部影片示範如何 toocreate 您自己的金鑰保存庫以及如何 toouse 從 hello ' Hello 金鑰保存庫 」 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-120">This video shows you how toocreate your own key vault and how toouse it from hello 'Hello Key Vault' sample application.</span></span>

- [<span data-ttu-id="0b7e8-121">Key Vault 開發人員 - 快速入門指南</span><span class="sxs-lookup"><span data-stu-id="0b7e8-121">Key Vault developer - quick start guide</span></span>](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

<span data-ttu-id="0b7e8-122">以上影片中所提及的資源︰</span><span class="sxs-lookup"><span data-stu-id="0b7e8-122">Resources mentioned in above video:</span></span>

- [<span data-ttu-id="0b7e8-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b7e8-123">Azure PowerShell</span></span>](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [<span data-ttu-id="0b7e8-124">Azure 金鑰保存庫範例程式碼</span><span class="sxs-lookup"><span data-stu-id="0b7e8-124">Azure Key Vault Sample Code</span></span>](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a><span data-ttu-id="0b7e8-125">建立及管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0b7e8-125">Creating and Managing Key Vaults</span></span>

<span data-ttu-id="0b7e8-126">之前使用 Azure 金鑰保存庫在程式碼中，您可以建立並管理保存庫，透過 REST、 資源管理員範本、 PowerShell 或 CLI hello 下列文章中所述：</span><span class="sxs-lookup"><span data-stu-id="0b7e8-126">Before working with Azure Key Vault in your code, you can create and manage vaults through REST, Resource Manager Templates, PowerShell or CLI, as described in hello following articles:</span></span>

- [<span data-ttu-id="0b7e8-127">使用 REST 建立和管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0b7e8-127">Create and Manage Key Vaults with REST</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="0b7e8-128">使用 PowerShell 建立和管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0b7e8-128">Create and Manage Key Vaults with PowerShell</span></span>](key-vault-get-started.md)
- [<span data-ttu-id="0b7e8-129">使用 CLI 建立和管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0b7e8-129">Create and Manage Key Vaults with CLI</span></span>](key-vault-manage-with-cli2.md)
- [<span data-ttu-id="0b7e8-130">透過 Azure Resource Manager 範本建立金鑰保存庫和新增祕密</span><span class="sxs-lookup"><span data-stu-id="0b7e8-130">Create a key vault and add a secret via an Azure Resource Manager template</span></span>](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> <span data-ttu-id="0b7e8-131">涉及金鑰保存庫的作業乃透過 AAD 進行驗證，以及透過金鑰保存庫自己的存取原則 (每個保存庫有各自的定義) 進行授權。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-131">Operations against key vaults are authenticated through AAD and authorized through Key Vault’s own Access Policy, defined per vault.</span></span>

## <a name="coding-with-key-vault"></a><span data-ttu-id="0b7e8-132">撰寫金鑰保存庫的程式碼</span><span class="sxs-lookup"><span data-stu-id="0b7e8-132">Coding with Key Vault</span></span>

<span data-ttu-id="0b7e8-133">hello 程式設計人員的金鑰保存庫管理系統是由數個介面，與為 hello 基礎的其餘部分所組成。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-133">hello Key Vault management system for programmers consists of several interfaces, with REST as hello foundation.</span></span> <span data-ttu-id="0b7e8-134">Hello REST 介面，透過您金鑰保存庫的資源都可存取;金鑰、 密碼和憑證。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-134">Through hello REST interface, all of your key vaults resources are accessible; keys, secrets and certificates.</span></span> <span data-ttu-id="0b7e8-135">[Key Vault REST API 參考](https://docs.microsoft.com/rest/api/keyvault/)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-135">[Key Vault REST API Reference](https://docs.microsoft.com/rest/api/keyvault/).</span></span> 

### <a name="supported-programming-languages"></a><span data-ttu-id="0b7e8-136">支援的程式設計語言</span><span class="sxs-lookup"><span data-stu-id="0b7e8-136">Supported programming languages</span></span>

#### <a name="net"></a><span data-ttu-id="0b7e8-137">.NET</span><span class="sxs-lookup"><span data-stu-id="0b7e8-137">.NET</span></span>

- [<span data-ttu-id="0b7e8-138">Key Vault 的 .NET API 參考</span><span class="sxs-lookup"><span data-stu-id="0b7e8-138">.NET API refence for Key Vault</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

<span data-ttu-id="0b7e8-139">如需有關 hello 2.x 版的 hello.NET SDK 的詳細資訊，請參閱 hello[版本資訊](key-vault-dotnet2api-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-139">For more information on hello 2.x version of hello .NET SDK, see hello [Release notes](key-vault-dotnet2api-release-notes.md).</span></span>

#### <a name="java"></a><span data-ttu-id="0b7e8-140">Java</span><span class="sxs-lookup"><span data-stu-id="0b7e8-140">Java</span></span>

- [<span data-ttu-id="0b7e8-141">Key Vault 的 Java SDK</span><span class="sxs-lookup"><span data-stu-id="0b7e8-141">Java SDK for Key Vault</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a><span data-ttu-id="0b7e8-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="0b7e8-142">Node.js</span></span>

<span data-ttu-id="0b7e8-143">在 Node.js hello 保存庫管理 API 和 hello 保存庫的物件 API 不同。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-143">In Node.js, hello vault management API and hello vault object API are separate.</span></span> <span data-ttu-id="0b7e8-144">Key Vault 管理可建立及更新您的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-144">Key Vault Management allows creating and updating your key vault.</span></span> <span data-ttu-id="0b7e8-145">Key Vault 作業 API 適用於金鑰、密碼和憑證等保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-145">Key Vault Operations API is for working with vault objects like; keys, secrets and certificates.</span></span> 

- [<span data-ttu-id="0b7e8-146">Key Vault 管理的 Node.js API 參考</span><span class="sxs-lookup"><span data-stu-id="0b7e8-146">Node.js API reference for Key Vault Management</span></span>](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [<span data-ttu-id="0b7e8-147">Key Vault 作業的 Node.js API 參考</span><span class="sxs-lookup"><span data-stu-id="0b7e8-147">Node.js API reference for Key Vault Operations</span></span>](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a><span data-ttu-id="0b7e8-148">快速入門</span><span class="sxs-lookup"><span data-stu-id="0b7e8-148">Quick start</span></span>

- [<span data-ttu-id="0b7e8-149">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0b7e8-149">Create Key Vault</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [<span data-ttu-id="0b7e8-150">開始在 Node.js 中使用 Key Vault</span><span class="sxs-lookup"><span data-stu-id="0b7e8-150">Getting started with Key Vault in Node.js</span></span>](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a><span data-ttu-id="0b7e8-151">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="0b7e8-151">Code examples</span></span>

<span data-ttu-id="0b7e8-152">如需搭配使用金鑰保存庫和應用程式的完整範例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="0b7e8-152">For complete examples using Key Vault with your applications, see:</span></span>

- <span data-ttu-id="0b7e8-153">[Azure Key Vault 程式碼範例](http://www.microsoft.com/download/details.aspx?id=45343) - .NET 範例應用程式 HelloKeyVault 和 Azure Web 服務範例。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-153">[Azure Key Vault code samples](http://www.microsoft.com/download/details.aspx?id=45343) - .NET sample application *HelloKeyVault* and an Azure web service example.</span></span> 
- <span data-ttu-id="0b7e8-154">[使用 Azure 金鑰保存庫的 Web 應用程式](key-vault-use-from-web-application.md)-教學課程 toohelp 您學習如何 toouse Azure 金鑰保存庫在 Azure 中的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-154">[Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md) - tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> 

## <a name="how-tos"></a><span data-ttu-id="0b7e8-155">作法</span><span class="sxs-lookup"><span data-stu-id="0b7e8-155">How-tos</span></span>

<span data-ttu-id="0b7e8-156">hello 下列文章和案例提供使用 Azure 金鑰保存庫的特定工作的指引：</span><span class="sxs-lookup"><span data-stu-id="0b7e8-156">hello following articles and scenarios provide task-specific guidance for working with Azure Key Vault:</span></span>

- <span data-ttu-id="0b7e8-157">[訂用帳戶之後變更金鑰保存庫租用戶識別碼移動](key-vault-subscription-move-fix.md)-當您從租用戶 B tootenant 移動您的 Azure 訂用帳戶，您現有的金鑰保存庫都無法存取的 hello 主體 （使用者和應用程式） 租用戶 b 修正此使用本指南中。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-157">[Change key vault tenant ID after subscription move](key-vault-subscription-move-fix.md) - When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. Fix this using this guide.</span></span>
- <span data-ttu-id="0b7e8-158">[存取金鑰保存庫位於防火牆後方](key-vault-access-behind-firewall.md)-tooaccess 金鑰保存庫您金鑰保存庫用戶端應用程式需求 toobe 無法 tooaccess 多個端點的各種不同功能。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-158">[Accessing Key Vault behind firewall](key-vault-access-behind-firewall.md) - tooaccess a key vault your key vault client application needs toobe able tooaccess multiple end-points for various functionalities.</span></span>
- <span data-ttu-id="0b7e8-159">[如何 tooGenerate 和 Azure 金鑰保存庫金鑰 Transfer HSM-Protected](key-vault-hsm-protected-keys.md) -這可協助您規劃、 產生和然後再將您自己的 HSM 保護的金鑰 toouse 使用 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-159">[How tooGenerate and Transfer HSM-Protected Keys for Azure Key Vault](key-vault-hsm-protected-keys.md) - This will help you plan for, generate and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>
- <span data-ttu-id="0b7e8-160">[Toopass 如何保護 （例如密碼） 的值在部署期間](../azure-resource-manager/resource-manager-keyvault-parameter.md)-當您需要做為參數 toopass 安全的值 （例如密碼） 在部署期間，您可以儲存該值做為另一個 Azure 金鑰保存庫和參考 hello 值中的密碼資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-160">[How toopass secure values (such as passwords) during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md) - When you need toopass a secure value (like a password) as a parameter during deployment, you can store that value as a secret in an Azure Key Vault and reference hello value in other Resource Manager templates.</span></span>
- <span data-ttu-id="0b7e8-161">[如何與 SQL Server 的可延伸金鑰管理的金鑰保存庫 toouse](https://msdn.microsoft.com/library/dn198405.aspx) -hello Azure 金鑰保存庫可讓 SQL Server 和 SQL 中-a-VM tooleverage hello Azure 金鑰保存庫服務作為 Extensible Key Management (EKM) 提供者的 SQL Server Connectortooprotect 其加密金鑰的應用程式連結。透明資料加密、 備份的加密和資料行層級加密。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-161">[How toouse Key Vault for extensible key management with SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) - hello SQL Server Connector for Azure Key Vault enables SQL Server and SQL-in-a-VM tooleverage hello Azure Key Vault service as an Extensible Key Management (EKM) provider tooprotect its encryption keys for applications link; Transparent Data Encryption, Backup Encryption, and Column Level Encryption.</span></span>
- <span data-ttu-id="0b7e8-162">[如何從金鑰保存庫 toodeploy 憑證 tooVMs](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) -在 VM 中 Azure 需要憑證的執行的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-162">[How toodeploy Certificates tooVMs from Key Vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - A cloud application running in a VM on Azure needs a certificate.</span></span> <span data-ttu-id="0b7e8-163">現在應如何讓此憑證進入此 VM？</span><span class="sxs-lookup"><span data-stu-id="0b7e8-163">How do you get this certificate into this VM today?</span></span>
- <span data-ttu-id="0b7e8-164">[如何結束 tooend 與金鑰保存庫註冊 tooset 金鑰旋轉和稽核](key-vault-key-rotation-log-monitoring.md)-此逐步解說如何 tooset 金鑰輪替和使用 Azure 金鑰保存庫稽核。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-164">[How tooset up Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md) - This walks through how tooset up key rotation and auditing with Azure Key Vault.</span></span>
- <span data-ttu-id="0b7e8-165">[透過金鑰保存庫部署 Azure Web 應用程式憑證]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)提供逐步指示，以便將儲存在金鑰保存庫的憑證部署為 [App Service 憑證](https://azure.microsoft.com/blog/internals-of-app-service-certificate/)供應項目的一部分。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-165">[Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) provides step-by-step instructions for deploying certificates stored in Key Vault as part of [App Service Certificate](https://azure.microsoft.com/blog/internals-of-app-service-certificate/) offering.</span></span>
- <span data-ttu-id="0b7e8-166">[授與權限 toomany 應用程式 tooaccess 金鑰保存庫](key-vault-group-permissions-for-apps.md)金鑰保存庫的存取控制原則只支援 16 的項目。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-166">[Grant permission toomany applications tooaccess a key vault](key-vault-group-permissions-for-apps.md) Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="0b7e8-167">不過，您可以建立 Azure Active Directory 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-167">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="0b7e8-168">加入所有 hello 建立關聯的服務主體 toothis 安全性群組，然後授與存取 toothis 安全性群組 tooKey 保存庫。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-168">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>
- <span data-ttu-id="0b7e8-169">如需整合及搭配使用金鑰保存庫和 Azure 的具體工作指引，請參閱 [Ryan Jones 的金鑰保存庫 Azure Resource Manager 範本範例](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-169">For more task-specific guidance on integrating and using Key Vaults with Azure, see [Ryan Jones' Azure Resource Manager template examples for Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>
- <span data-ttu-id="0b7e8-170">[如何 toouse 金鑰保存庫虛刪除與 CLI](key-vault-soft-delete-cli.md)會引導您完成使用 hello 和金鑰保存庫和金鑰保存庫的各種物件的生命週期與啟用虛刪除。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-170">[How toouse Key Vault soft-delete with CLI](key-vault-soft-delete-cli.md) guides you through hello use and lifecycle of a key vault and various key vault objects with soft-delete enabled.</span></span>
- <span data-ttu-id="0b7e8-171">[如何 toouse 金鑰保存庫虛刪除使用 PowerShell](key-vault-soft-delete-powershell.md)會引導您完成使用 hello 和金鑰保存庫和金鑰保存庫的各種物件的生命週期與啟用虛刪除。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-171">[How toouse Key Vault soft-delete with PowerShell](key-vault-soft-delete-powershell.md) guides you through hello use and lifecycle of a key vault and various key vault objects with soft-delete enabled.</span></span>

## <a name="integrated-with-key-vault"></a><span data-ttu-id="0b7e8-172">與金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="0b7e8-172">Integrated with Key Vault</span></span>

<span data-ttu-id="0b7e8-173">這些文章是關於其他可讓我們使用及整合 Key Vault 的案例和服務。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-173">These articles are about other scenarios and services that use or integrate with Key Vault.</span></span>

- <span data-ttu-id="0b7e8-174">[Azure 磁碟加密](../security/azure-security-disk-encryption.md)利用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello OS 與 hello 資料 Linux tooprovide 磁碟區加密的功能磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-174">[Azure Disk Encryption](../security/azure-security-disk-encryption.md) leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="0b7e8-175">您控制和管理 hello 磁碟加密金鑰和秘密中您金鑰保存庫的訂用帳戶，同時確保 hello 虛擬機器磁碟中的所有資料會留在您 Azure 儲存體都加密的 Azure 金鑰保存庫 toohelp 整合 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-175">hello solution is integrated with Azure Key Vault toohelp you control and manage hello disk encryption keys and secrets in your key vault subscription, while ensuring that all data in hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>
- <span data-ttu-id="0b7e8-176">[Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)提供加密的資料會儲存在 hello 帳戶的選項。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-176">[Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) provides option for encryption of data that is stored in hello account.</span></span> <span data-ttu-id="0b7e8-177">金鑰管理，資料湖存放區會用於管理您所需的解密儲存在 hello 資料湖存放區中的任何資料的主要加密金鑰 (MEKs)，提供兩種模式。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-177">For key management, Data Lake Store provides two modes for managing your master encryption keys (MEKs), which are required for decrypting any data that is stored in hello Data Lake Store.</span></span> <span data-ttu-id="0b7e8-178">您可以讓資料湖存放區 hello MEKs 管理，或選擇使用 Azure 金鑰保存庫帳戶 hello MEKs tooretain 擁有權。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-178">You can either let Data Lake Store manage hello MEKs for you, or choose tooretain ownership of hello MEKs using your Azure Key Vault account.</span></span> <span data-ttu-id="0b7e8-179">您建立 Data Lake Store 帳戶時指定金鑰管理的 hello 的模式。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-179">You specify hello mode of key management while creating a Data Lake Store account.</span></span> 
- <span data-ttu-id="0b7e8-180">[Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) toomanager 可讓您自己的租用戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-180">[Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) allows you toomanager your own tenant key.</span></span> <span data-ttu-id="0b7e8-181">例如，而不是 Microsoft 管理租用戶金鑰 （hello 預設值），您可以管理您自己的租用戶金鑰 toocomply 套用 tooyour 組織的特定法規。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-181">For example, instead of Microsoft managing your tenant key (hello default), you can manage your own tenant key toocomply with specific regulations that apply tooyour organization.</span></span> <span data-ttu-id="0b7e8-182">管理您自己的租用戶金鑰也會參照的 tooas 整合您自己的金鑰或 BYOK。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-182">Managing your own tenant key is also referred tooas bring your own key, or BYOK.</span></span>

## <a name="key-vault-overviews-and-concepts"></a><span data-ttu-id="0b7e8-183">Key Vault 的概觀和概念</span><span class="sxs-lookup"><span data-stu-id="0b7e8-183">Key Vault overviews and concepts</span></span>

- <span data-ttu-id="0b7e8-184">[金鑰保存庫虛刪除行為](key-vault-ovw-soft-delete.md)hello 刪除是否意外或故意情況下，描述功能，可復原已刪除的物件。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-184">[Key Vault soft-delete behavior](key-vault-ovw-soft-delete.md) describes a feature that allows recovery of deleted objects, whether hello deletion was accidental or intentional.</span></span>
- <span data-ttu-id="0b7e8-185">[金鑰保存庫用戶端節流](key-vault-ovw-throttling.md)將您導向 toohello 節流的基本概念，並提供您的應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-185">[Key Vault client throttling](key-vault-ovw-throttling.md) orients you toohello basic concepts of throttling and offers an approach for your app.</span></span>
- <span data-ttu-id="0b7e8-186">[金鑰保存庫儲存體帳戶金鑰概觀](key-vault-ovw-storage-keys.md)描述 hello 金鑰保存庫整合 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-186">[Key Vault storage account keys overview](key-vault-ovw-storage-keys.md) describes hello Key Vault integration Azure Storage Accounts keys.</span></span>
- <span data-ttu-id="0b7e8-187">[金鑰保存庫安全園地](key-vault-ovw-security-worlds.md)描述 hello 地區和安全性區域之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-187">[Key Vault security worlds](key-vault-ovw-security-worlds.md) describes hello relationships between regions and security areas.</span></span>

## <a name="social"></a><span data-ttu-id="0b7e8-188">社交</span><span class="sxs-lookup"><span data-stu-id="0b7e8-188">Social</span></span>

- [<span data-ttu-id="0b7e8-189">Key Vault Blog (金鑰保存庫部落格)</span><span class="sxs-lookup"><span data-stu-id="0b7e8-189">Key Vault Blog</span></span>](http://aka.ms/kvblog)
- [<span data-ttu-id="0b7e8-190">Key Vault Forum (金鑰保存庫論壇)</span><span class="sxs-lookup"><span data-stu-id="0b7e8-190">Key Vault Forum</span></span>](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a><span data-ttu-id="0b7e8-191">支援程式庫</span><span class="sxs-lookup"><span data-stu-id="0b7e8-191">Supporting Libraries</span></span>

- <span data-ttu-id="0b7e8-192">[Microsoft Azure Key Vault 核心程式庫](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core)提供 **IKey** 和 **IKeyResolver** 介面，以從識別碼找出金鑰和使用金鑰執行作業。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-192">[Microsoft Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) provides **IKey** and **IKeyResolver** interfaces for locating keys from identifiers and performing operations with keys.</span></span>
- <span data-ttu-id="0b7e8-193">[Microsoft Azure 金鑰保存庫擴充](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions)提供 Azure 金鑰保存庫的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0b7e8-193">[Microsoft Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) provides extended capabilities for Azure Key Vault.</span></span>


