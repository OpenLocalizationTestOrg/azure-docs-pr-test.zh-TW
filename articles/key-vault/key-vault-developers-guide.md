---
title: "Azure 金鑰保存庫開發人員指南"
description: "開發人員可以使用 Azure 金鑰保存庫來管理 Microsoft Azure 環境中的密碼編譯金鑰。"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: fec4769c0bd571edea84dd2f766bb907d8819be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-developers-guide"></a><span data-ttu-id="af42e-103">Azure 金鑰保存庫開發人員指南</span><span class="sxs-lookup"><span data-stu-id="af42e-103">Azure Key Vault Developer's Guide</span></span>

<span data-ttu-id="af42e-104">Key Vault 可讓您從應用程式內安全地存取機密資訊︰</span><span class="sxs-lookup"><span data-stu-id="af42e-104">Key Vault allows you to securely access sensitive information from within your applications:</span></span>

- <span data-ttu-id="af42e-105">不需要自行撰寫程式碼即可保護金鑰和密碼，而且也能輕易地從應用程式加以使用。</span><span class="sxs-lookup"><span data-stu-id="af42e-105">Keys and secrets are protected without having to write the code yourself and you are easily able to use them from your applications.</span></span>
- <span data-ttu-id="af42e-106">可以讓客戶擁有及管理他們自己的金鑰，因此您可以致力於提供核心軟體功能。</span><span class="sxs-lookup"><span data-stu-id="af42e-106">You are able to have your customers own and manage their own keys so you can concentrate on providing the core software features.</span></span> <span data-ttu-id="af42e-107">透過這種方式，您的應用程式將不需要對客戶的租用戶金鑰和密碼負起責任或潛在責任。</span><span class="sxs-lookup"><span data-stu-id="af42e-107">In this way, your applications will not own the responsibility or potential liability for your customers’ tenant keys and secrets.</span></span>
- <span data-ttu-id="af42e-108">您的應用程式能使用金鑰進行簽署和加密，同時也能在應用程式外部管理金鑰，讓您的解決方案適用於位於不同地點的應用程式。</span><span class="sxs-lookup"><span data-stu-id="af42e-108">Your application can use keys for signing and encryption yet keeps the key management external from your application, allowing your solution to be suitable as a geographically distributed app.</span></span>
- <span data-ttu-id="af42e-109">自 2016 年 9 月起推出的 Key Vault，您的應用程式現在可以使用 Key Vault [憑證](https://docs.microsoft.com/rest/api/keyvault/certificate-operations)。</span><span class="sxs-lookup"><span data-stu-id="af42e-109">As of the September 2016 release of Key Vault, your applications can now use Key Vault [certificates](https://docs.microsoft.com/rest/api/keyvault/certificate-operations).</span></span> <span data-ttu-id="af42e-110">如需詳細資訊，請參閱[關於金鑰、祕密和憑證](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates)。</span><span class="sxs-lookup"><span data-stu-id="af42e-110">For more information, see [About keys, secrets, and certificates](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).</span></span>

<span data-ttu-id="af42e-111">如需 Azure 金鑰保存庫的一般詳細資訊，請參閱 [什麼是金鑰保存庫？](key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="af42e-111">For more general information on Azure Key Vault, see [What is Key Vault](key-vault-whatis.md).</span></span>

## <a name="public-previews"></a><span data-ttu-id="af42e-112">公開預覽</span><span class="sxs-lookup"><span data-stu-id="af42e-112">Public Previews</span></span>

<span data-ttu-id="af42e-113">我們會定期發行新 Key Vault 功能的公開預覽。</span><span class="sxs-lookup"><span data-stu-id="af42e-113">Periodically, we release a public preview of a new Key Vault feature.</span></span> <span data-ttu-id="af42e-114">請試試看，然後透過我們的意見反應電子郵件地址 azurekeyvault@microsoft.com，讓我們知道您的想法。</span><span class="sxs-lookup"><span data-stu-id="af42e-114">Please try out these and let us know what you think via azurekeyvault@microsoft.com, our feedback email address.</span></span>

### <a name="storage-account-keys---july-10-2017"></a><span data-ttu-id="af42e-115">儲存體帳戶金鑰 - 2017 年 7 月 10 日</span><span class="sxs-lookup"><span data-stu-id="af42e-115">Storage Account Keys - July 10, 2017</span></span>

>[!NOTE]
><span data-ttu-id="af42e-116">在此 Azure Key Vault 更新中，只有 [儲存體帳戶金鑰] 功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="af42e-116">For this update of Azure Key Vault only the **Storage Account Keys** feature is in preview.</span></span>

<span data-ttu-id="af42e-117">此預覽版包含新的 [儲存體帳戶金鑰] 功能，可透過下列介面提供：[.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/)、[REST](https://docs.microsoft.com/rest/api/keyvault/) 和 [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/)。</span><span class="sxs-lookup"><span data-stu-id="af42e-117">This preview includes our new Storage Account Keys feature, available through these interfaces; [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) and [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/).</span></span> 

<span data-ttu-id="af42e-118">如需新 [儲存體帳戶金鑰] 功能的詳細資訊，請參閱 [Azure Key Vault 儲存體帳戶金鑰概觀](key-vault-ovw-storage-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="af42e-118">For more information on the new Storage Account Keys feature, see [Azure Key Vault storage account keys overview](key-vault-ovw-storage-keys.md).</span></span>

## <a name="videos"></a><span data-ttu-id="af42e-119">影片</span><span class="sxs-lookup"><span data-stu-id="af42e-119">Videos</span></span>

<span data-ttu-id="af42e-120">此影片示範如何建立專屬金鑰保存庫以及如何從 'Hello Key Vault' 範例應用程式使用它。</span><span class="sxs-lookup"><span data-stu-id="af42e-120">This video shows you how to create your own key vault and how to use it from the 'Hello Key Vault' sample application.</span></span>

- [<span data-ttu-id="af42e-121">Key Vault 開發人員 - 快速入門指南</span><span class="sxs-lookup"><span data-stu-id="af42e-121">Key Vault developer - quick start guide</span></span>](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

<span data-ttu-id="af42e-122">以上影片中所提及的資源︰</span><span class="sxs-lookup"><span data-stu-id="af42e-122">Resources mentioned in above video:</span></span>

- [<span data-ttu-id="af42e-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="af42e-123">Azure PowerShell</span></span>](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [<span data-ttu-id="af42e-124">Azure 金鑰保存庫範例程式碼</span><span class="sxs-lookup"><span data-stu-id="af42e-124">Azure Key Vault Sample Code</span></span>](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a><span data-ttu-id="af42e-125">建立及管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="af42e-125">Creating and Managing Key Vaults</span></span>

<span data-ttu-id="af42e-126">在程式碼中使用 Azure 金鑰保存庫之前，您可以透過 REST、資源管理員範本、PowerShell 或 CLI 來建立及管理保存庫，如以下文章所述︰</span><span class="sxs-lookup"><span data-stu-id="af42e-126">Before working with Azure Key Vault in your code, you can create and manage vaults through REST, Resource Manager Templates, PowerShell or CLI, as described in the following articles:</span></span>

- [<span data-ttu-id="af42e-127">使用 REST 建立和管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="af42e-127">Create and Manage Key Vaults with REST</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="af42e-128">使用 PowerShell 建立和管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="af42e-128">Create and Manage Key Vaults with PowerShell</span></span>](key-vault-get-started.md)
- [<span data-ttu-id="af42e-129">使用 CLI 建立和管理金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="af42e-129">Create and Manage Key Vaults with CLI</span></span>](key-vault-manage-with-cli2.md)
- [<span data-ttu-id="af42e-130">透過 Azure Resource Manager 範本建立金鑰保存庫和新增祕密</span><span class="sxs-lookup"><span data-stu-id="af42e-130">Create a key vault and add a secret via an Azure Resource Manager template</span></span>](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> <span data-ttu-id="af42e-131">涉及金鑰保存庫的作業乃透過 AAD 進行驗證，以及透過金鑰保存庫自己的存取原則 (每個保存庫有各自的定義) 進行授權。</span><span class="sxs-lookup"><span data-stu-id="af42e-131">Operations against key vaults are authenticated through AAD and authorized through Key Vault’s own Access Policy, defined per vault.</span></span>

## <a name="coding-with-key-vault"></a><span data-ttu-id="af42e-132">撰寫金鑰保存庫的程式碼</span><span class="sxs-lookup"><span data-stu-id="af42e-132">Coding with Key Vault</span></span>

<span data-ttu-id="af42e-133">程式設計人員的 Key Vault 管理系統由幾個介面組成，並以 REST 作為基礎。</span><span class="sxs-lookup"><span data-stu-id="af42e-133">The Key Vault management system for programmers consists of several interfaces, with REST as the foundation.</span></span> <span data-ttu-id="af42e-134">透過 REST 介面，可存取所有 Key Vault 資源；包括金鑰、密碼和憑證。</span><span class="sxs-lookup"><span data-stu-id="af42e-134">Through the REST interface, all of your key vaults resources are accessible; keys, secrets and certificates.</span></span> <span data-ttu-id="af42e-135">[Key Vault REST API 參考](https://docs.microsoft.com/rest/api/keyvault/)。</span><span class="sxs-lookup"><span data-stu-id="af42e-135">[Key Vault REST API Reference](https://docs.microsoft.com/rest/api/keyvault/).</span></span> 

### <a name="supported-programming-languages"></a><span data-ttu-id="af42e-136">支援的程式設計語言</span><span class="sxs-lookup"><span data-stu-id="af42e-136">Supported programming languages</span></span>

#### <a name="net"></a><span data-ttu-id="af42e-137">.NET</span><span class="sxs-lookup"><span data-stu-id="af42e-137">.NET</span></span>

- [<span data-ttu-id="af42e-138">Key Vault 的 .NET API 參考</span><span class="sxs-lookup"><span data-stu-id="af42e-138">.NET API refence for Key Vault</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

<span data-ttu-id="af42e-139">如需 .NET SDK 2.x 版的詳細資訊，請參閱[版本資訊](key-vault-dotnet2api-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="af42e-139">For more information on the 2.x version of the .NET SDK, see the [Release notes](key-vault-dotnet2api-release-notes.md).</span></span>

#### <a name="java"></a><span data-ttu-id="af42e-140">Java</span><span class="sxs-lookup"><span data-stu-id="af42e-140">Java</span></span>

- [<span data-ttu-id="af42e-141">Key Vault 的 Java SDK</span><span class="sxs-lookup"><span data-stu-id="af42e-141">Java SDK for Key Vault</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a><span data-ttu-id="af42e-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="af42e-142">Node.js</span></span>

<span data-ttu-id="af42e-143">在 Node.js 中，保存庫管理 API 和保存庫物件 API 會分開。</span><span class="sxs-lookup"><span data-stu-id="af42e-143">In Node.js, the vault management API and the vault object API are separate.</span></span> <span data-ttu-id="af42e-144">Key Vault 管理可建立及更新您的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="af42e-144">Key Vault Management allows creating and updating your key vault.</span></span> <span data-ttu-id="af42e-145">Key Vault 作業 API 適用於金鑰、密碼和憑證等保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="af42e-145">Key Vault Operations API is for working with vault objects like; keys, secrets and certificates.</span></span> 

- [<span data-ttu-id="af42e-146">Key Vault 管理的 Node.js API 參考</span><span class="sxs-lookup"><span data-stu-id="af42e-146">Node.js API reference for Key Vault Management</span></span>](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [<span data-ttu-id="af42e-147">Key Vault 作業的 Node.js API 參考</span><span class="sxs-lookup"><span data-stu-id="af42e-147">Node.js API reference for Key Vault Operations</span></span>](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a><span data-ttu-id="af42e-148">快速入門</span><span class="sxs-lookup"><span data-stu-id="af42e-148">Quick start</span></span>

- [<span data-ttu-id="af42e-149">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="af42e-149">Create Key Vault</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [<span data-ttu-id="af42e-150">開始在 Node.js 中使用 Key Vault</span><span class="sxs-lookup"><span data-stu-id="af42e-150">Getting started with Key Vault in Node.js</span></span>](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a><span data-ttu-id="af42e-151">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="af42e-151">Code examples</span></span>

<span data-ttu-id="af42e-152">如需搭配使用金鑰保存庫和應用程式的完整範例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="af42e-152">For complete examples using Key Vault with your applications, see:</span></span>

- <span data-ttu-id="af42e-153">[Azure Key Vault 程式碼範例](http://www.microsoft.com/download/details.aspx?id=45343) - .NET 範例應用程式 HelloKeyVault 和 Azure Web 服務範例。</span><span class="sxs-lookup"><span data-stu-id="af42e-153">[Azure Key Vault code samples](http://www.microsoft.com/download/details.aspx?id=45343) - .NET sample application *HelloKeyVault* and an Azure web service example.</span></span> 
- <span data-ttu-id="af42e-154">[從 Web 應用程式使用 Azure Key Vault ](key-vault-use-from-web-application.md) - 此教學課程可幫助您了解如何從 Azure 中的 Web 應用程式使用 Azure Key Vault。</span><span class="sxs-lookup"><span data-stu-id="af42e-154">[Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md) - tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> 

## <a name="how-tos"></a><span data-ttu-id="af42e-155">作法</span><span class="sxs-lookup"><span data-stu-id="af42e-155">How-tos</span></span>

<span data-ttu-id="af42e-156">下列文章和案例提供使用 Azure Key Vault 的工作特定指引：</span><span class="sxs-lookup"><span data-stu-id="af42e-156">The following articles and scenarios provide task-specific guidance for working with Azure Key Vault:</span></span>

- <span data-ttu-id="af42e-157">[訂用帳戶動作之後變更金鑰保存庫租用戶識別碼](key-vault-subscription-move-fix.md) - 當您將 Azure 訂用帳戶從租用戶 A 移動至租用戶 B 時，租用戶 B 中的實體 (使用者和應用程式) 將無法存取您現有的金鑰保存庫。請利用本指南來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="af42e-157">[Change key vault tenant ID after subscription move](key-vault-subscription-move-fix.md) - When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. Fix this using this guide.</span></span>
- <span data-ttu-id="af42e-158">[存取防火牆後面的金鑰保存庫](key-vault-access-behind-firewall.md)若要存取金鑰保存庫，您的金鑰保存庫用戶端應用程式必須能夠存取多個端點，才能使用各種功能。</span><span class="sxs-lookup"><span data-stu-id="af42e-158">[Accessing Key Vault behind firewall](key-vault-access-behind-firewall.md) - To access a key vault your key vault client application needs to be able to access multiple end-points for various functionalities.</span></span>
- <span data-ttu-id="af42e-159">[如何為 Azure 金鑰保存庫產生並傳輸受 HSM 保護的金鑰](key-vault-hsm-protected-keys.md) - 這將協助您規劃、產生並傳輸專屬受 HSM 保護的金鑰，以搭配 Azure 金鑰保存庫使用。</span><span class="sxs-lookup"><span data-stu-id="af42e-159">[How to Generate and Transfer HSM-Protected Keys for Azure Key Vault](key-vault-hsm-protected-keys.md) - This will help you plan for, generate and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>
- <span data-ttu-id="af42e-160">[如何在部署期間傳遞安全值 (例如密碼)](../azure-resource-manager/resource-manager-keyvault-parameter.md) - 當您需要在部署期間傳遞安全值 (例如密碼) 作為參數時，可以將該值儲存為 Azure 金鑰保存庫中的密碼，並在其他資源管理員範本中參考該值。</span><span class="sxs-lookup"><span data-stu-id="af42e-160">[How to pass secure values (such as passwords) during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md) - When you need to pass a secure value (like a password) as a parameter during deployment, you can store that value as a secret in an Azure Key Vault and reference the value in other Resource Manager templates.</span></span>
- <span data-ttu-id="af42e-161">[如何搭配使用金鑰保存庫與 SQL Server 進行可延伸金鑰管理](https://msdn.microsoft.com/library/dn198405.aspx) - 適用於 Azure 金鑰保存庫的 SQL Server 連接器會啟用 SQL Server 和 SQL-in-a-VM，利用 Azure 金鑰保存庫服務作為可延伸金鑰管理 (EKM) 提供者來保護其針對應用程式連結的加密金鑰；透明資料加密、備份加密和資料行層級加密。</span><span class="sxs-lookup"><span data-stu-id="af42e-161">[How to use Key Vault for extensible key management with SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) - The SQL Server Connector for Azure Key Vault enables SQL Server and SQL-in-a-VM to leverage the Azure Key Vault service as an Extensible Key Management (EKM) provider to protect its encryption keys for applications link; Transparent Data Encryption, Backup Encryption, and Column Level Encryption.</span></span>
- <span data-ttu-id="af42e-162">[如何將憑證從金鑰保存庫部署至 VM](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - 在 Azure 上的 VM 中執行的雲端應用程式需要憑證。</span><span class="sxs-lookup"><span data-stu-id="af42e-162">[How to deploy Certificates to VMs from Key Vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - A cloud application running in a VM on Azure needs a certificate.</span></span> <span data-ttu-id="af42e-163">現在應如何讓此憑證進入此 VM？</span><span class="sxs-lookup"><span data-stu-id="af42e-163">How do you get this certificate into this VM today?</span></span>
- <span data-ttu-id="af42e-164">[如何使用端對端金鑰輪替和稽核設定金鑰保存庫](key-vault-key-rotation-log-monitoring.md) - 引導您逐步完成使用 Azure Key Vault 設定金鑰輪替和稽核的步驟。</span><span class="sxs-lookup"><span data-stu-id="af42e-164">[How to set up Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md) - This walks through how to set up key rotation and auditing with Azure Key Vault.</span></span>
- <span data-ttu-id="af42e-165">[透過金鑰保存庫部署 Azure Web 應用程式憑證]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)提供逐步指示，以便將儲存在金鑰保存庫的憑證部署為 [App Service 憑證](https://azure.microsoft.com/blog/internals-of-app-service-certificate/)供應項目的一部分。</span><span class="sxs-lookup"><span data-stu-id="af42e-165">[Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) provides step-by-step instructions for deploying certificates stored in Key Vault as part of [App Service Certificate](https://azure.microsoft.com/blog/internals-of-app-service-certificate/) offering.</span></span>
- <span data-ttu-id="af42e-166">[對許多應用程式授與金鑰保存庫的存取權限](key-vault-group-permissions-for-apps.md) 金鑰保存庫存取控制原則只支援 16 個項目。</span><span class="sxs-lookup"><span data-stu-id="af42e-166">[Grant permission to many applications to access a key vault](key-vault-group-permissions-for-apps.md) Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="af42e-167">不過，您可以建立 Azure Active Directory 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="af42e-167">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="af42e-168">將所有相關聯的服務主體新增至這個安全性群組，然後對 Key Vault 授與此安全性群組的存取權。</span><span class="sxs-lookup"><span data-stu-id="af42e-168">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>
- <span data-ttu-id="af42e-169">如需整合及搭配使用金鑰保存庫和 Azure 的具體工作指引，請參閱 [Ryan Jones 的金鑰保存庫 Azure Resource Manager 範本範例](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples)。</span><span class="sxs-lookup"><span data-stu-id="af42e-169">For more task-specific guidance on integrating and using Key Vaults with Azure, see [Ryan Jones' Azure Resource Manager template examples for Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>
- <span data-ttu-id="af42e-170">[如何以 CLI 使用金鑰保存庫虛刪除](key-vault-soft-delete-cli.md)引導您完成金鑰保存庫和各種金鑰保存庫物件的使用和生命週期，並啟用虛刪除。</span><span class="sxs-lookup"><span data-stu-id="af42e-170">[How to use Key Vault soft-delete with CLI](key-vault-soft-delete-cli.md) guides you through the use and lifecycle of a key vault and various key vault objects with soft-delete enabled.</span></span>
- <span data-ttu-id="af42e-171">[如何以 Powershell 使用金鑰保存庫虛刪除](key-vault-soft-delete-powershell.md)引導您完成金鑰保存庫和各種金鑰保存庫物件的使用和生命週期，並啟用虛刪除。</span><span class="sxs-lookup"><span data-stu-id="af42e-171">[How to use Key Vault soft-delete with PowerShell](key-vault-soft-delete-powershell.md) guides you through the use and lifecycle of a key vault and various key vault objects with soft-delete enabled.</span></span>

## <a name="integrated-with-key-vault"></a><span data-ttu-id="af42e-172">與金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="af42e-172">Integrated with Key Vault</span></span>

<span data-ttu-id="af42e-173">這些文章是關於其他可讓我們使用及整合 Key Vault 的案例和服務。</span><span class="sxs-lookup"><span data-stu-id="af42e-173">These articles are about other scenarios and services that use or integrate with Key Vault.</span></span>

- <span data-ttu-id="af42e-174">[Azure 磁碟加密](../security/azure-security-disk-encryption.md)利用 Windows 的業界標準 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 功能和 Linux 的 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 功能，為 OS 和資料磁碟提供磁碟區加密。</span><span class="sxs-lookup"><span data-stu-id="af42e-174">[Azure Disk Encryption](../security/azure-security-disk-encryption.md) leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="af42e-175">此解決方案與 Azure 金鑰保存庫整合，可幫助您控制和管理您的金鑰保存庫訂用帳戶中的磁碟加密金鑰和密碼，同時確保虛擬機器磁碟中的所有資料會在您的 Azure 儲存體中輕鬆加密。</span><span class="sxs-lookup"><span data-stu-id="af42e-175">The solution is integrated with Azure Key Vault to help you control and manage the disk encryption keys and secrets in your key vault subscription, while ensuring that all data in the virtual machine disks are encrypted at rest in your Azure storage.</span></span>
- <span data-ttu-id="af42e-176">[Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) 會為帳戶中儲存的資料提供加密選項。</span><span class="sxs-lookup"><span data-stu-id="af42e-176">[Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) provides option for encryption of data that is stored in the account.</span></span> <span data-ttu-id="af42e-177">金鑰管理，如 Data Lake Store 會提供兩種模式用於管理您的主要加密金鑰 (MEK)，它是解密 Data Lake Store 中儲存任何資料所需。</span><span class="sxs-lookup"><span data-stu-id="af42e-177">For key management, Data Lake Store provides two modes for managing your master encryption keys (MEKs), which are required for decrypting any data that is stored in the Data Lake Store.</span></span> <span data-ttu-id="af42e-178">您可以讓 Data Lake Store 管理 MEK，或使用 Azure 金鑰保存庫帳戶，選擇保留 MEK 的擁有權。</span><span class="sxs-lookup"><span data-stu-id="af42e-178">You can either let Data Lake Store manage the MEKs for you, or choose to retain ownership of the MEKs using your Azure Key Vault account.</span></span> <span data-ttu-id="af42e-179">您會在建立 Data Lake Store 帳戶時指定金鑰管理的模式。</span><span class="sxs-lookup"><span data-stu-id="af42e-179">You specify the mode of key management while creating a Data Lake Store account.</span></span> 
- <span data-ttu-id="af42e-180">[Azure 資訊保護](/information-protection/plan-design/plan-implement-tenant-key)可讓您管理自己的租用戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="af42e-180">[Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) allows you to manager your own tenant key.</span></span> <span data-ttu-id="af42e-181">例如，您可以管理自己的租用戶金鑰，以符合適用於貴組織的特定規範，而不需 Microsoft 管理您的租用戶金鑰 (預設值)。</span><span class="sxs-lookup"><span data-stu-id="af42e-181">For example, instead of Microsoft managing your tenant key (the default), you can manage your own tenant key to comply with specific regulations that apply to your organization.</span></span> <span data-ttu-id="af42e-182">管理自己的租用戶金鑰也稱為「自備金鑰」或 BYOK。</span><span class="sxs-lookup"><span data-stu-id="af42e-182">Managing your own tenant key is also referred to as bring your own key, or BYOK.</span></span>

## <a name="key-vault-overviews-and-concepts"></a><span data-ttu-id="af42e-183">Key Vault 的概觀和概念</span><span class="sxs-lookup"><span data-stu-id="af42e-183">Key Vault overviews and concepts</span></span>

- <span data-ttu-id="af42e-184">[Key Vault 虛刪除行為](key-vault-ovw-soft-delete.md)描述一項功能，該功能可復原已刪除的物件，無論是無意或有意刪除的。</span><span class="sxs-lookup"><span data-stu-id="af42e-184">[Key Vault soft-delete behavior](key-vault-ovw-soft-delete.md) describes a feature that allows recovery of deleted objects, whether the deletion was accidental or intentional.</span></span>
- <span data-ttu-id="af42e-185">[Key Vault 用戶端節流](key-vault-ovw-throttling.md)可讓您了解節流的基本概念，並提供適用於您應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="af42e-185">[Key Vault client throttling](key-vault-ovw-throttling.md) orients you to the basic concepts of throttling and offers an approach for your app.</span></span>
- <span data-ttu-id="af42e-186">[Key Vault 儲存體帳戶金鑰概觀](key-vault-ovw-storage-keys.md)描述 Key Vault 與 Azure 儲存體帳戶金鑰的整合。</span><span class="sxs-lookup"><span data-stu-id="af42e-186">[Key Vault storage account keys overview](key-vault-ovw-storage-keys.md) describes the Key Vault integration Azure Storage Accounts keys.</span></span>
- <span data-ttu-id="af42e-187">[Key Vault 安全世界](key-vault-ovw-security-worlds.md)描述地區和安全區域之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="af42e-187">[Key Vault security worlds](key-vault-ovw-security-worlds.md) describes the relationships between regions and security areas.</span></span>

## <a name="social"></a><span data-ttu-id="af42e-188">社交</span><span class="sxs-lookup"><span data-stu-id="af42e-188">Social</span></span>

- [<span data-ttu-id="af42e-189">Key Vault Blog (金鑰保存庫部落格)</span><span class="sxs-lookup"><span data-stu-id="af42e-189">Key Vault Blog</span></span>](http://aka.ms/kvblog)
- [<span data-ttu-id="af42e-190">Key Vault Forum (金鑰保存庫論壇)</span><span class="sxs-lookup"><span data-stu-id="af42e-190">Key Vault Forum</span></span>](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a><span data-ttu-id="af42e-191">支援程式庫</span><span class="sxs-lookup"><span data-stu-id="af42e-191">Supporting Libraries</span></span>

- <span data-ttu-id="af42e-192">[Microsoft Azure Key Vault 核心程式庫](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core)提供 **IKey** 和 **IKeyResolver** 介面，以從識別碼找出金鑰和使用金鑰執行作業。</span><span class="sxs-lookup"><span data-stu-id="af42e-192">[Microsoft Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) provides **IKey** and **IKeyResolver** interfaces for locating keys from identifiers and performing operations with keys.</span></span>
- <span data-ttu-id="af42e-193">[Microsoft Azure 金鑰保存庫擴充](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions)提供 Azure 金鑰保存庫的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="af42e-193">[Microsoft Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) provides extended capabilities for Azure Key Vault.</span></span>


