---
title: "aaaAzure 儲存體服務加密使用客戶管理 Azure 金鑰保存庫中的金鑰 |Microsoft 文件"
description: "Hello Azure 儲存體服務加密功能 tooencrypt 您的 Azure Blob 儲存體 hello 服務端上時使用儲存 hello 資料，並將其解密時擷取 hello 資料使用客戶管理金鑰。"
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: eb2e0ad27df40e61f9c08b9db7ca7a7568adad9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a><span data-ttu-id="8e63f-103">在 Azure Key Vault 中使用客戶管理金鑰進行儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="8e63f-103">Storage Service Encryption using customer managed keys in Azure Key Vault</span></span>

<span data-ttu-id="8e63f-104">Microsoft Azure 是認可的 toohelping 保護，並保護資料 toomeet 您組織的安全性和相容性的承諾。</span><span class="sxs-lookup"><span data-stu-id="8e63f-104">Microsoft Azure is committed toohelping you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span>  <span data-ttu-id="8e63f-105">您可以保護您的待用資料的一個方式是 toouse 儲存體服務加密 (SSE) 中，以自動將您的資料加密時寫入 toostorage，和擷取它時，會解密資料。</span><span class="sxs-lookup"><span data-stu-id="8e63f-105">One way you can protect your data at rest is toouse Storage Service Encryption (SSE), which automatically encrypts your data when writing it toostorage, and decrypts your data when retrieving it.</span></span> <span data-ttu-id="8e63f-106">hello 加密和解密自動、 完全透明，而且會使用 256 位元[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，hello 最強的區塊的其中一個這類編碼器使用。</span><span class="sxs-lookup"><span data-stu-id="8e63f-106">hello encryption and decryption is automatic, completely transparent, and uses 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of hello strongest block ciphers available.</span></span>

<span data-ttu-id="8e63f-107">您可以搭配 SSE 使用 Microsoft 管理的加密金鑰，或使用自己的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e63f-107">You can use Microsoft-managed encryption keys with SSE or you can use your own encryption keys.</span></span> <span data-ttu-id="8e63f-108">這篇文章討論 hello 後者。</span><span class="sxs-lookup"><span data-stu-id="8e63f-108">This article discusses hello latter.</span></span> <span data-ttu-id="8e63f-109">如需有關使用 Microsoft 管理之金鑰的詳細資訊，或有關 SSE 的一般資訊，請參閱[待用資料的儲存體服務加密](../storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-109">For more information about using Microsoft-managed keys, or about SSE in general, see [Storage Service Encryption for Data at Rest](../storage-service-encryption.md).</span></span>

<span data-ttu-id="8e63f-110">tooprovide hello 能力 toouse 整合您自己的加密金鑰，SSE 的 Blob 儲存體與 Azure 金鑰保存庫 (AKV)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-110">tooprovide hello ability toouse your own encryption keys, SSE for Blob storage is integrated with Azure Key Vault (AKV).</span></span> <span data-ttu-id="8e63f-111">您可以建立您自己的加密金鑰，並將其儲存在保存，或者您可以使用保存的應用程式開發介面 toogenerate 加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e63f-111">You can create your own encryption keys and store them in AKV, or you can use AKV’s APIs toogenerate encryption keys.</span></span> <span data-ttu-id="8e63f-112">不僅沒有 AKV toomanage 可讓您控制您的金鑰，它也可讓您 tooaudit 您金鑰的使用方式。</span><span class="sxs-lookup"><span data-stu-id="8e63f-112">Not only does AKV allow you toomanage and control your keys, it also enables you tooaudit your key usage.</span></span> 

<span data-ttu-id="8e63f-113">為什麼需要 toocreate 您自己的金鑰？</span><span class="sxs-lookup"><span data-stu-id="8e63f-113">Why would you want toocreate your own keys?</span></span> <span data-ttu-id="8e63f-114">它可讓您更大的彈性，讓您 toocreate、 旋轉、 停用，以及定義存取控制。</span><span class="sxs-lookup"><span data-stu-id="8e63f-114">It gives you more flexibility, allowing you toocreate, rotate, disable, and define access controls.</span></span> <span data-ttu-id="8e63f-115">它也可讓您 tooaudit hello 加密金鑰使用 tooprotect 您的資料。</span><span class="sxs-lookup"><span data-stu-id="8e63f-115">It also allows you tooaudit hello encryption keys used tooprotect your data.</span></span>

## <a name="sse-with-customer-managed-keys-preview"></a><span data-ttu-id="8e63f-116">使用客戶管理之金鑰的 SSE 預覽</span><span class="sxs-lookup"><span data-stu-id="8e63f-116">SSE with customer managed keys preview</span></span>

<span data-ttu-id="8e63f-117">此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="8e63f-117">This feature is currently in preview.</span></span> <span data-ttu-id="8e63f-118">toouse 這項功能，您需要 toocreate 新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e63f-118">toouse this feature, you need toocreate a new storage account.</span></span> <span data-ttu-id="8e63f-119">您可以建立新金鑰保存庫與金鑰，或者可以使用現有金鑰保存庫與金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e63f-119">You can either create a new key vault and key or you can use an existing key vault and key.</span></span> <span data-ttu-id="8e63f-120">hello 儲存體帳戶和 hello 金鑰保存庫必須在 hello 相同區域中，但它們可以是不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8e63f-120">hello storage account and hello key vault must be in hello same region, but they can be in different subscriptions.</span></span>

<span data-ttu-id="8e63f-121">在 hello 預覽中，請連絡 tooparticipate [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)。我們將提供的特殊連結 tooparticipate hello 預覽中。</span><span class="sxs-lookup"><span data-stu-id="8e63f-121">tooparticipate in hello preview, contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com). We will provide a special link tooparticipate in hello preview.</span></span>

<span data-ttu-id="8e63f-122">toolearn 詳細資訊，請參閱 toohello[常見問題集](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-122">toolearn more, refer toohello [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e63f-123">您必須註冊 hello 預覽先前 toofollowing 本文中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="8e63f-123">You must sign up for hello preview prior toofollowing hello steps in this article.</span></span> <span data-ttu-id="8e63f-124">沒有預覽存取，您將不會無法 tooenable hello 入口網站中的這項功能。</span><span class="sxs-lookup"><span data-stu-id="8e63f-124">Without preview access, you will not be able tooenable this feature in hello portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8e63f-125">開始使用</span><span class="sxs-lookup"><span data-stu-id="8e63f-125">Getting Started</span></span>
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="8e63f-126">步驟 1：[建立新的儲存體帳戶](../storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="8e63f-126">Step 1: [Create a new storage account](../storage-create-storage-account.md)</span></span>

## <a name="step-2-enable-encryption"></a><span data-ttu-id="8e63f-127">步驟 2︰啟用加密</span><span class="sxs-lookup"><span data-stu-id="8e63f-127">Step 2: Enable encryption</span></span>
<span data-ttu-id="8e63f-128">您可以使用 hello hello 儲存體帳戶啟用 SSE [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-128">You can enable SSE for hello storage account using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8e63f-129">在 hello 設定刀鋒視窗中的 hello 儲存體帳戶，尋找 hello Blob 服務 > 一節中 hello 以下圖，並按一下 [加密] 所示。</span><span class="sxs-lookup"><span data-stu-id="8e63f-129">On hello Settings blade for hello storage account, look for hello Blob Service section as shown in hello following figure and click Encryption.</span></span>

<span data-ttu-id="8e63f-130">![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)
</span><span class="sxs-lookup"><span data-stu-id="8e63f-130">![Portal Screenshot showing Encryption option](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)
</span></span><br/><span data-ttu-id="8e63f-131">*為 Blob 服務啟用 SSE*</span><span class="sxs-lookup"><span data-stu-id="8e63f-131">*Enable SSE for Blob Service*</span></span>

<span data-ttu-id="8e63f-132">如果您想 tooprogrammatically 啟用或停用的儲存體帳戶的儲存體服務加密 hello 時，您可以使用 hello [Azure 儲存體資源提供者 REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)，hello[儲存體資源提供者用戶端程式庫適用於.NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN)， [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0)，或使用 hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-132">If you want tooprogrammatically enable or disable hello Storage Service Encryption on a storage account, you can use hello [Azure Storage Resource Provider REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [Storage Resource Provider Client Library for .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), or hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).</span></span>

<span data-ttu-id="8e63f-133">在這個畫面上，如果您看 hello [使用您自己的金鑰] 核取方塊，您有尚未核准 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="8e63f-133">On this screen, if you can’t see hello “use your own key” checkbox, you have not been approved for hello preview.</span></span> <span data-ttu-id="8e63f-134">傳送電子郵件太[ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)和要求核准。</span><span class="sxs-lookup"><span data-stu-id="8e63f-134">Send an e-mail too[ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) and request approval.</span></span>

![顯示 [加密預覽] 的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

<span data-ttu-id="8e63f-136">根據預設，SSE 會使用 Microsoft 管理的金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e63f-136">By default, SSE uses Microsoft managed keys.</span></span> <span data-ttu-id="8e63f-137">toouse 您自己的金鑰，請檢查 hello 方塊。</span><span class="sxs-lookup"><span data-stu-id="8e63f-137">toouse your own keys, check hello box.</span></span> <span data-ttu-id="8e63f-138">然後您可以指定的 URI，您的金鑰，或從 hello 選擇器選取金鑰和金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="8e63f-138">Then you can either specify your key URI, or select a key and Key Vault from hello picker.</span></span>

## <a name="step-3-select-your-key"></a><span data-ttu-id="8e63f-139">步驟 3：選取您的金鑰</span><span class="sxs-lookup"><span data-stu-id="8e63f-139">Step 3: Select your key</span></span>

![顯示 [使用您自己的金鑰加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![顯示 [透過輸入金鑰 URI 來加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

<span data-ttu-id="8e63f-142">如果 hello 儲存體帳戶沒有存取 toohello 金鑰保存庫，您可以執行 hello 下列命令： 使用 Azure Powershell toogrant 存取 toohello 儲存體帳戶 toohello 需要金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="8e63f-142">If hello storage account does not have access toohello Key Vault, you can run hello following command using Azure Powershell toogrant access toohello storage accounts toohello required key vault.</span></span>

![顯示金鑰保存庫存取遭拒的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

<span data-ttu-id="8e63f-144">您也可以移 toohello Azure 金鑰保存庫中 hello Azure 入口網站並授與存取 toohello 儲存體帳戶授與透過 hello Azure 入口網站的存取。</span><span class="sxs-lookup"><span data-stu-id="8e63f-144">You can also grant access via hello Azure portal by going toohello Azure Key Vault in hello Azure portal and granting access toohello storage account.</span></span>

## <a name="step-4-copy-data-toostorage-account"></a><span data-ttu-id="8e63f-145">步驟 4： 複製資料 toostorage 帳戶</span><span class="sxs-lookup"><span data-stu-id="8e63f-145">Step 4: Copy data toostorage account</span></span>
<span data-ttu-id="8e63f-146">如果您想要 tootransfer 資料到新的儲存體帳戶，使它已經加密，請參閱太[步驟 3 的快速入門中的待用資料的儲存體服務加密](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-146">If you would like tootransfer data into your new storage account so that it’s encrypted, refer too[Step 3 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).</span></span>

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a><span data-ttu-id="8e63f-147">步驟 5: Hello 查詢 hello 狀態加密資料</span><span class="sxs-lookup"><span data-stu-id="8e63f-147">Step 5: Query hello status of hello encrypted data</span></span>
<span data-ttu-id="8e63f-148">hello tooquery hello 狀態加密資料，請參閱太[步驟 4 的快速入門中的待用資料的儲存體服務加密](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-148">tooquery hello status of hello encrypted data, refer too[Step 4 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="8e63f-149">待用資料的儲存體服務加密的常見問題集</span><span class="sxs-lookup"><span data-stu-id="8e63f-149">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="8e63f-150">**問︰我正在使用進階儲存體，是否可以使用具有客戶管理之金鑰的 SSE？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-150">**Q: I'm using Premium storage; can I use SSE with customer managed keys?**</span></span>

<span data-ttu-id="8e63f-151">答：是，在標準儲存體和進階儲存體上都支援搭配 Microsoft 管理與客戶管理之金鑰使用 SSE。</span><span class="sxs-lookup"><span data-stu-id="8e63f-151">A: Yes, SSE with Microsoft-managed  and customer managed keys is supported on both Standard storage and Premium storage.</span></span> 

<span data-ttu-id="8e63f-152">**問：是否可以搭配客戶管理的金鑰 \(使用 Azure PowerShell 和 Azure CLI 啟用\) 使用 SSE 建立新儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-152">**Q: Can I create new storage accounts with SSE with customer managed keys enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="8e63f-153">答：是。</span><span class="sxs-lookup"><span data-stu-id="8e63f-153">A: Yes.</span></span>

<span data-ttu-id="8e63f-154">**問：如果啟用使用客戶管理金鑰的 SSE，Azure 儲存體的成本會多出多少？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-154">**Q: How much more does Azure Storage cost if SSE with customer managed keys is enabled?**</span></span>

<span data-ttu-id="8e63f-155">答：使用 Azure Key Vault 有相關成本。</span><span class="sxs-lookup"><span data-stu-id="8e63f-155">A: There is a cost associated for using Azure Key Vault.</span></span> <span data-ttu-id="8e63f-156">如需詳細資訊，請瀏覽 [Key Vault 定價](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-156">For more details visit [Key Vault Pricing](https://azure.microsoft.com/en-us/pricing/details/key-vault/).</span></span> <span data-ttu-id="8e63f-157">使用 SSE 不會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="8e63f-157">There is no additional cost for using SSE.</span></span>

<span data-ttu-id="8e63f-158">**問： 是否可以撤銷存取 toohello 加密金鑰？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-158">**Q: Can I revoke access toohello encryption keys?**</span></span>

<span data-ttu-id="8e63f-159">答：是，您可以隨時撤銷存取權。</span><span class="sxs-lookup"><span data-stu-id="8e63f-159">A: Yes, you can revoke access at any time.</span></span> <span data-ttu-id="8e63f-160">有幾個方式 toorevoke 存取 tooyour 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8e63f-160">There are several ways toorevoke access tooyour keys.</span></span> <span data-ttu-id="8e63f-161">請參閱太[Azure 金鑰保存庫 PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0)和[Azure 金鑰保存庫 CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8e63f-161">Refer too[Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) and [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) for more details.</span></span> <span data-ttu-id="8e63f-162">因為 hello 帳戶加密金鑰是無法存取 Azure 儲存體，撤銷存取權可以有效地會封鎖存取 tooall blob hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8e63f-162">Revoking access will effectively block access tooall blobs in hello storage account as hello Account Encryption Key is inaccessible by Azure Storage.</span></span>

<span data-ttu-id="8e63f-163">**問：是否可以在不同的區域建立儲存體帳戶和金鑰？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-163">**Q: Can I create a storage account and key in different region?**</span></span>

<span data-ttu-id="8e63f-164">答： 否，hello 儲存體帳戶和金鑰的保存庫金鑰需要 toobe 在 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="8e63f-164">A: No, hello storage account and key vault/key need toobe in hello same region.</span></span> 

<span data-ttu-id="8e63f-165">**問： 是否可以啟用 SSE 受管理的客戶索引鍵的同時建立 hello 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-165">**Q: Can I enable SSE with customer managed keys while creating hello storage account?**</span></span>

<span data-ttu-id="8e63f-166">答：否。</span><span class="sxs-lookup"><span data-stu-id="8e63f-166">A: No.</span></span> <span data-ttu-id="8e63f-167">當您啟用 SSE 建立 hello 儲存體帳戶時，您只能使用 Microsoft 受管理的金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e63f-167">When you enable SSE while creating hello storage account, you can only use Microsoft managed keys.</span></span> <span data-ttu-id="8e63f-168">如果您想要 toouse 由客戶管理金鑰，您必須更新 hello 儲存體帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="8e63f-168">If you would like toouse customer managed keys, you must update hello storage account properties.</span></span> <span data-ttu-id="8e63f-169">您可以使用 REST 或其中一個 hello 儲存體用戶端程式庫 tooprogrammatically 更新您的儲存體帳戶，或更新 hello 建立 hello 帳戶後使用 hello Azure 入口網站的儲存體帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="8e63f-169">You can use REST or one of hello storage client libraries tooprogrammatically update your storage account, or update hello storage account properties using hello Azure portal after creating hello account.</span></span>

<span data-ttu-id="8e63f-170">**問：使用具有客戶管理之金鑰的 SSE 時是否可以停用加密？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-170">**Q: Can I disable encryption while using SSE with customer managed keys?**</span></span>

<span data-ttu-id="8e63f-171">答：否，使用具有客戶管理之金鑰的 SSE 時無法停用加密。</span><span class="sxs-lookup"><span data-stu-id="8e63f-171">A: No, you cannot disable encryption while using SSE with customer managed keys.</span></span> <span data-ttu-id="8e63f-172">toodisable 加密，您必須切換 toousing Microsoft 受管理的金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e63f-172">toodisable encryption, you must switch toousing Microsoft managed keys.</span></span> <span data-ttu-id="8e63f-173">您可以使用 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8e63f-173">You can do this using either hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="8e63f-174">**問︰我建立新的儲存體帳戶時是否預設啟用 SSE？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-174">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="8e63f-175">答： SSE 不會啟用預設值;您可以使用 Azure 入口網站 tooenable hello 它。</span><span class="sxs-lookup"><span data-stu-id="8e63f-175">A: SSE is not enabled by default; you can use hello Azure portal tooenable it.</span></span> <span data-ttu-id="8e63f-176">您可以也以程式設計方式啟用此功能使用 hello 儲存體資源提供者 REST API。</span><span class="sxs-lookup"><span data-stu-id="8e63f-176">You can also programmatically enable this feature using hello Storage Resource Provider REST API.</span></span> 

<span data-ttu-id="8e63f-177">**問︰我無法在我的儲存體帳戶上啟用加密。**</span><span class="sxs-lookup"><span data-stu-id="8e63f-177">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="8e63f-178">答︰這是 Resource Manager 儲存體帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="8e63f-178">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="8e63f-179">不支援傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e63f-179">Classic storage accounts are not supported.</span></span> <span data-ttu-id="8e63f-180">也只能對新建立的資源管理員儲存體帳戶啟用使用客戶管理之金鑰的 SSE。</span><span class="sxs-lookup"><span data-stu-id="8e63f-180">SSE with customer managed keys can also be enabled only on newly created Resource Manager storage accounts.</span></span>

<span data-ttu-id="8e63f-181">**問：是否只在特定區域中允許使用客戶管理之金鑰的 SSE？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-181">**Q: Is SSE with customer managed keys only permitted in specific regions?**</span></span>

<span data-ttu-id="8e63f-182">答：針對這個預覽，只能在 Blob 儲存體的特定區域中使用 SSE。</span><span class="sxs-lookup"><span data-stu-id="8e63f-182">A: SSE is available in only certain regions for Blob storage for this Preview.</span></span> <span data-ttu-id="8e63f-183">電子郵件[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck 可用性和預覽的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8e63f-183">Email [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) toocheck for availability and details on preview.</span></span> 

<span data-ttu-id="8e63f-184">**問： 如何連絡有人如果我有任何問題或想 tooprovide 意見反應？**</span><span class="sxs-lookup"><span data-stu-id="8e63f-184">**Q: How do I contact someone if I have any issues or want tooprovide feedback?**</span></span>

<span data-ttu-id="8e63f-185">答： 連絡[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)是否有任何問題相關 tooStorage 服務加密。</span><span class="sxs-lookup"><span data-stu-id="8e63f-185">A: Contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related tooStorage Service Encryption.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8e63f-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e63f-186">Next steps</span></span>

*   <span data-ttu-id="8e63f-187">如需有關 hello 一組完整的安全性功能，可協助開發人員建立安全的應用程式，請參閱 hello[存放安全性指南 》](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-187">For more information on hello comprehensive set of security capabilities that help developers build secure applications, see hello [Storage Security Guide](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).</span></span>
*   <span data-ttu-id="8e63f-188">如需 Azure Key Vault 的概觀資訊，請參閱[什麼是 Azure Key Vault？](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)</span><span class="sxs-lookup"><span data-stu-id="8e63f-188">For overview information about Azure Key Vault, see [What is Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?</span></span>
*   <span data-ttu-id="8e63f-189">若要開始使用 Azure Key Vault，請參閱[開始使用 Azure Key Vault](../../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8e63f-189">For getting started on Azure Key Vault, see [Getting Started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>
