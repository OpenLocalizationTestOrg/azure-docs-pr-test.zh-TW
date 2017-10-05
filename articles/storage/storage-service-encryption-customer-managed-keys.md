---
title: "在 Azure Key Vault 中使用客戶管理的金鑰進行 Azure 儲存體服務加密 | Microsoft 文件"
description: "使用 Azure 儲存體服務加密功能，在儲存資料時於服務端加密您的 Azure Blob 儲存體，並在擷取資料時使用客戶管理的金鑰將它解密。"
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
ms.openlocfilehash: b596cf1a98a9c6f42c3bbee9cc27608549e2b5ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a><span data-ttu-id="55ff9-103">在 Azure Key Vault 中使用客戶管理金鑰進行儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="55ff9-103">Storage Service Encryption using customer managed keys in Azure Key Vault</span></span>

<span data-ttu-id="55ff9-104">Microsoft Azure 堅定承諾協助您保護資料安全，以符合組織安全性和合規性承諾。</span><span class="sxs-lookup"><span data-stu-id="55ff9-104">Microsoft Azure is strongly committed to helping you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span>  <span data-ttu-id="55ff9-105">您可以透過一種方式保護待用資料，那就是使用「儲存服務加密」(SSE)，它會在將資料寫入到儲存體時自動加密資料，並在擷取時解密資料。</span><span class="sxs-lookup"><span data-stu-id="55ff9-105">One way you can protect your data at rest is to use Storage Service Encryption (SSE), which automatically encrypts your data when writing it to storage, and decrypts your data when retrieving it.</span></span> <span data-ttu-id="55ff9-106">加密與解密是自動進行的，過程完全透明，並且使用 256 位元 [AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) \(英文\)，這是目前可用最強大的區塊編碼器之一。</span><span class="sxs-lookup"><span data-stu-id="55ff9-106">The encryption and decryption is automatic and completely transparent and uses 256-bit [AES encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), one of the strongest block ciphers available.</span></span>

<span data-ttu-id="55ff9-107">您可以搭配 SSE 使用 Microsoft 管理的加密金鑰，或使用自己的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-107">You can use Microsoft-managed encryption keys with SSE or you can use your own encryption keys.</span></span> <span data-ttu-id="55ff9-108">此文章將會討論後者。</span><span class="sxs-lookup"><span data-stu-id="55ff9-108">This article will talk about the latter.</span></span> <span data-ttu-id="55ff9-109">如需有關使用 Microsoft 管理之金鑰的詳細資訊，或有關 SSE 的一般資訊，請參閱[待用資料的儲存體服務加密](storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-109">For more information about using Microsoft-managed keys, or about SSE in general, please see [Storage Service Encryption for Data at Rest](storage-service-encryption.md).</span></span>

<span data-ttu-id="55ff9-110">為了提供使用自己的加密金鑰之能力，Blob 儲存體的 SSE 已與 Azure Key Vault (AKV) 整合。</span><span class="sxs-lookup"><span data-stu-id="55ff9-110">To provide the ability to use your own encryption keys, SSE for Blob storage is integrated with Azure Key Vault (AKV).</span></span> <span data-ttu-id="55ff9-111">您可以建立自己的加密金鑰，並將其儲存在 AKV 中，或者可以使用 AKV 的 API 來產生加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-111">You can create your own encryption keys and store them in AKV, or you can use AKV’s APIs to generate encryption keys.</span></span> <span data-ttu-id="55ff9-112">AKV 不僅允許您管理及控制金鑰，也可以讓您稽核金鑰的使用狀況。</span><span class="sxs-lookup"><span data-stu-id="55ff9-112">Not only does AKV allow you to manage and control your keys, it also enables you to audit your key usage.</span></span> 

<span data-ttu-id="55ff9-113">為什麼要建立您自己的金鑰？</span><span class="sxs-lookup"><span data-stu-id="55ff9-113">Why would you want to create your own keys?</span></span> <span data-ttu-id="55ff9-114">這樣可以賦予您更大的彈性，包括建立、輪替、停用及定義存取控制的能力，還可以稽核用於保護資料的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-114">It gives you more flexibility, including the ability to create, rotate, disable, and define access controls, and to audit the encryption keys used to protect your data.</span></span>

## <a name="sse-with-customer-managed-keys-preview"></a><span data-ttu-id="55ff9-115">使用客戶管理之金鑰的 SSE 預覽</span><span class="sxs-lookup"><span data-stu-id="55ff9-115">SSE with customer managed keys preview</span></span>

<span data-ttu-id="55ff9-116">此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="55ff9-116">This feature is currently in preview.</span></span> <span data-ttu-id="55ff9-117">若要使用此功能，您需要建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55ff9-117">To use this feature, you need to create a new storage account.</span></span> <span data-ttu-id="55ff9-118">您可以建立新金鑰保存庫與金鑰，或者可以使用現有金鑰保存庫與金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-118">You can either create a new key vault and key or you can use an existing key vault and key.</span></span> <span data-ttu-id="55ff9-119">儲存體帳戶與金鑰保存庫必須位於相同區域，但可位於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="55ff9-119">The storage account and the key vault must be in the same region, but they can be in different subscriptions.</span></span>

<span data-ttu-id="55ff9-120">若要參與預覽，請連絡 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-120">To participate in the preview please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com).</span></span> <span data-ttu-id="55ff9-121">我們將提供參與預覽的特殊連結。</span><span class="sxs-lookup"><span data-stu-id="55ff9-121">We will provide a special link to participate in the preview.</span></span>

<span data-ttu-id="55ff9-122">若要深入了解，請參閱[常見問題集](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-122">To learn more, please refer to the [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55ff9-123">您必須註冊預覽，才能繼續此文章中的後續步驟。</span><span class="sxs-lookup"><span data-stu-id="55ff9-123">You must sign up for the preview prior to following the steps in this article.</span></span> <span data-ttu-id="55ff9-124">若無預覽存取權，您將無法在入口網站中啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="55ff9-124">Without preview access, you will not be able to enable this feature in the portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="55ff9-125">開始使用</span><span class="sxs-lookup"><span data-stu-id="55ff9-125">Getting Started</span></span>
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a><span data-ttu-id="55ff9-126">步驟 1：[建立新的儲存體帳戶](storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="55ff9-126">Step 1: [Create a new storage account](storage-create-storage-account.md)</span></span>

## <a name="step-2-enable-encryption"></a><span data-ttu-id="55ff9-127">步驟 2︰啟用加密</span><span class="sxs-lookup"><span data-stu-id="55ff9-127">Step 2: Enable encryption</span></span>
<span data-ttu-id="55ff9-128">您可以使用 [Azure 入口網站](https://portal.azure.com)來啟用儲存體帳戶的 SSE。</span><span class="sxs-lookup"><span data-stu-id="55ff9-128">You can enable SSE for the storage account using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="55ff9-129">在儲存體帳戶的 [設定] 刀鋒視窗上，尋找如下圖所示的 [Blob 服務] 區段，並按一下 [加密]。</span><span class="sxs-lookup"><span data-stu-id="55ff9-129">On the Settings blade for the storage account, look for the Blob Service section as shown in figure below and click Encryption.</span></span>

<span data-ttu-id="55ff9-130">![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption/image1.png)
</span><span class="sxs-lookup"><span data-stu-id="55ff9-130">![Portal Screenshot showing Encryption option](./media/storage-service-encryption/image1.png)
</span></span><br/><span data-ttu-id="55ff9-131">*為 Blob 服務啟用 SSE*</span><span class="sxs-lookup"><span data-stu-id="55ff9-131">*Enable SSE for Blob Service*</span></span>

<span data-ttu-id="55ff9-132">如果您想要以程式設計方式啟用或停用儲存體帳戶上的儲存體服務加密，您可以使用 [Azure 儲存體資源提供者 REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)、[適用於 .NET 的儲存體資源提供者用戶端程式庫](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN)、[Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0) 或 [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-132">If you want to programmatically enable or disable the Storage Service Encryption on a storage account, you can use the [Azure Storage Resource Provider REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), the [Storage Resource Provider Client Library for .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), or the [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).</span></span>

<span data-ttu-id="55ff9-133">在這個畫面上，如果沒有看到 [使用您自己的金鑰] 核取方塊，即表示您尚未獲准預覽。</span><span class="sxs-lookup"><span data-stu-id="55ff9-133">On this screen, if you can’t see the “use your own key” checkbox, you have not been approved for the preview.</span></span> <span data-ttu-id="55ff9-134">請傳送電子郵件至 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) 並要求核准。</span><span class="sxs-lookup"><span data-stu-id="55ff9-134">Please send an e-mail to [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) and request approval.</span></span>

![顯示 [加密預覽] 的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

<span data-ttu-id="55ff9-136">根據預設，SSE 將使用 Microsoft 管理的金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-136">By default, SSE will use Microsoft managed keys.</span></span> <span data-ttu-id="55ff9-137">若要使用您自己的金鑰，請選取該方塊。</span><span class="sxs-lookup"><span data-stu-id="55ff9-137">To use your own keys, check the box.</span></span> <span data-ttu-id="55ff9-138">然後您可以指定金鑰 URI，或從選擇器中選取金鑰和 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="55ff9-138">Then you can either specify your key URI, or select a key and Key Vault from the picker.</span></span>

## <a name="step-3-select-your-key"></a><span data-ttu-id="55ff9-139">步驟 3：選取您的金鑰</span><span class="sxs-lookup"><span data-stu-id="55ff9-139">Step 3: Select your key</span></span>

![顯示 [使用您自己的金鑰加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![顯示 [透過輸入金鑰 URI 來加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

<span data-ttu-id="55ff9-142">如果儲存體帳戶沒有 Key Vault 的存取權，您可以使用 Azure Powershell 執行下列命令，授與儲存體帳戶對於所需金鑰保存庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="55ff9-142">If the storage account does not have access to the Key Vault, you can run the following command using Azure Powershell to grant access to the storage accounts to the required key vault.</span></span>

![顯示金鑰保存庫存取遭拒的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

<span data-ttu-id="55ff9-144">您也可以移至 Azure 入口網站中的 Azure Key Vault，並將存取權授與儲存體帳戶，以透過 Azure 入口網站授與存取權。</span><span class="sxs-lookup"><span data-stu-id="55ff9-144">You can also grant access via the Azure portal by going to the Azure Key Vault in the Azure portal and granting access to the storage account.</span></span>

## <a name="step-4-copy-data-to-storage-account"></a><span data-ttu-id="55ff9-145">步驟 4︰將資料複製到儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="55ff9-145">Step 4: Copy data to storage account</span></span>
<span data-ttu-id="55ff9-146">如果您想要將資料傳輸至新的儲存體帳戶，以對其進行加密，請參閱[待用資料的儲存體服務加密快速入門步驟 3](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-146">If you would like to transfer data into your new storage account so that it’s encrypted, please refer to [Step 3 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).</span></span>

## <a name="step-5-query-the-status-of-the-encrypted-data"></a><span data-ttu-id="55ff9-147">步驟 5︰查詢加密資料的狀態</span><span class="sxs-lookup"><span data-stu-id="55ff9-147">Step 5: Query the status of the encrypted data</span></span>
<span data-ttu-id="55ff9-148">若要查詢加密資料的狀態，請參閱[待用資料的儲存體服務加密快速入門步驟 4](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-148">To query the status of the encrypted data please refer to [Step 4 of Getting Started in Storage Service Encryption for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).</span></span>

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a><span data-ttu-id="55ff9-149">待用資料的儲存體服務加密的常見問題集</span><span class="sxs-lookup"><span data-stu-id="55ff9-149">Frequently asked questions about Storage Service Encryption for Data at Rest</span></span>
<span data-ttu-id="55ff9-150">**問︰我正在使用進階儲存體，是否可以使用具有客戶管理之金鑰的 SSE？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-150">**Q: I'm using Premium storage; can I use SSE with customer managed keys?**</span></span>

<span data-ttu-id="55ff9-151">答：是，在標準儲存體和進階儲存體上都支援搭配 Microsoft 管理與客戶管理之金鑰使用 SSE。</span><span class="sxs-lookup"><span data-stu-id="55ff9-151">A: Yes, SSE with Microsoft-managed  and customer managed keys is supported on both Standard storage and Premium storage.</span></span> 

<span data-ttu-id="55ff9-152">**問：是否可以搭配客戶管理的金鑰 \(使用 Azure PowerShell 和 Azure CLI 啟用\) 使用 SSE 建立新儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-152">**Q: Can I create new storage accounts with SSE with customer managed keys enabled using Azure PowerShell and Azure CLI?**</span></span>

<span data-ttu-id="55ff9-153">答：是。</span><span class="sxs-lookup"><span data-stu-id="55ff9-153">A: Yes.</span></span>

<span data-ttu-id="55ff9-154">**問：如果啟用使用客戶管理金鑰的 SSE，Azure 儲存體的成本會多出多少？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-154">**Q: How much more does Azure Storage cost if SSE with customer managed keys is enabled?**</span></span>

<span data-ttu-id="55ff9-155">答：使用 Azure Key Vault 有相關成本。</span><span class="sxs-lookup"><span data-stu-id="55ff9-155">A: There is a cost associated for using Azure Key Vault.</span></span> <span data-ttu-id="55ff9-156">如需詳細資訊，請瀏覽 [Key Vault 定價](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-156">For more details visit [Key Vault Pricing](https://azure.microsoft.com/en-us/pricing/details/key-vault/).</span></span> <span data-ttu-id="55ff9-157">使用 SSE 不會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="55ff9-157">There is no additional cost for using SSE.</span></span>

<span data-ttu-id="55ff9-158">**問︰是否可以撤銷加密金鑰的存取權？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-158">**Q: Can I revoke access to the encryption keys?**</span></span>

<span data-ttu-id="55ff9-159">答：是，您可以隨時撤銷存取權。</span><span class="sxs-lookup"><span data-stu-id="55ff9-159">A: Yes, you can revoke access at any time.</span></span> <span data-ttu-id="55ff9-160">有幾種方法可以撤銷對金鑰的存取權。</span><span class="sxs-lookup"><span data-stu-id="55ff9-160">There are several ways to revoke access to your keys.</span></span> <span data-ttu-id="55ff9-161">如需詳細資訊，請參閱 [Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) \(英文\) 與 [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-161">Please refer to [Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) and [Azure Key Vault CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) for more details.</span></span> <span data-ttu-id="55ff9-162">撤銷存取權將有效封鎖對儲存體帳戶中所有 Blob 的存取權，因為 Azure 儲存體將無法存取帳戶加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-162">Revoking access will effectively block access to all blobs in the storage account as the Account Encryption Key is inaccessible by Azure Storage.</span></span>

<span data-ttu-id="55ff9-163">**問：是否可以在不同的區域建立儲存體帳戶和金鑰？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-163">**Q: Can I create a storage account and key in different region?**</span></span>

<span data-ttu-id="55ff9-164">答：否，儲存體帳戶和金鑰保存庫/金鑰必須位於相同區域中。</span><span class="sxs-lookup"><span data-stu-id="55ff9-164">A: No, the storage account and key vault/key need to be in the same region.</span></span> 

<span data-ttu-id="55ff9-165">**問：建立儲存體帳戶時是否可以啟用使用客戶管理之金鑰的 SSE？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-165">**Q: Can I enable SSE with customer managed keys while creating the storage account?**</span></span>

<span data-ttu-id="55ff9-166">答：否。</span><span class="sxs-lookup"><span data-stu-id="55ff9-166">A: No.</span></span> <span data-ttu-id="55ff9-167">如果您在建立儲存體帳戶時啟用 SSE，便只能使用 Microsoft 管理的金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-167">When you enable SSE while creating the storage account, you can only use Microsoft managed keys.</span></span> <span data-ttu-id="55ff9-168">如果您想要使用客戶管理的金鑰，將需要更新儲存體帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="55ff9-168">If you would like to use customer managed keys you will need to update the storage account properties.</span></span> <span data-ttu-id="55ff9-169">您可以使用 REST 或其中一個儲存體用戶端程式庫來以程式設計方式更新儲存體帳戶，或在建立帳戶之後使用 Azure 入口網站更新儲存體帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="55ff9-169">You can use REST or one of the storage client libraries to programmatically update your storage account, or update the storage account properties using the Azure Portal after creating the account.</span></span>

<span data-ttu-id="55ff9-170">**問：使用具有客戶管理之金鑰的 SSE 時是否可以停用加密？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-170">**Q: Can I disable encryption while using SSE with customer managed keys?**</span></span>

<span data-ttu-id="55ff9-171">答：否，使用具有客戶管理之金鑰的 SSE 時無法停用加密。</span><span class="sxs-lookup"><span data-stu-id="55ff9-171">A: No, you cannot disable encryption while using SSE with customer managed keys.</span></span> <span data-ttu-id="55ff9-172">若要停用加密，您將必須改為使用 Microsoft 管理的金鑰。</span><span class="sxs-lookup"><span data-stu-id="55ff9-172">To disable encryption, you will need to switch to using Microsoft managed keys.</span></span> <span data-ttu-id="55ff9-173">您可以使用 Azure 入口網站或 PowerShell 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="55ff9-173">You can do this using either the Azure portal or PowerShell.</span></span>

<span data-ttu-id="55ff9-174">**問︰我建立新的儲存體帳戶時是否預設啟用 SSE？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-174">**Q: Is SSE enabled by default when I create a new storage account?**</span></span>

<span data-ttu-id="55ff9-175">答：預設未啟用 SSE；您可以使用 Azure 入口網站來啟用它。</span><span class="sxs-lookup"><span data-stu-id="55ff9-175">A: SSE is not enabled by default; you can use the Azure portal to enable it.</span></span> <span data-ttu-id="55ff9-176">您也能以程式設計方式，使用儲存體資源提供者 REST API 來啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="55ff9-176">You can also programmatically enable this feature using the Storage Resource Provider REST API.</span></span> 

<span data-ttu-id="55ff9-177">**問︰我無法在我的儲存體帳戶上啟用加密。**</span><span class="sxs-lookup"><span data-stu-id="55ff9-177">**Q: I can't enable encryption on my storage account.**</span></span>

<span data-ttu-id="55ff9-178">答︰這是 Resource Manager 儲存體帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="55ff9-178">A: Is it a Resource Manager storage account?</span></span> <span data-ttu-id="55ff9-179">不支援傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55ff9-179">Classic storage accounts are not supported.</span></span> <span data-ttu-id="55ff9-180">也只能對新建立的資源管理員儲存體帳戶啟用使用客戶管理之金鑰的 SSE。</span><span class="sxs-lookup"><span data-stu-id="55ff9-180">SSE with customer managed keys can also be enabled only on newly created Resource Manager storage accounts.</span></span>

<span data-ttu-id="55ff9-181">**問：是否只在特定區域中允許使用客戶管理之金鑰的 SSE？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-181">**Q: Is SSE with customer managed keys only permitted in specific regions?**</span></span>

<span data-ttu-id="55ff9-182">答：針對這個預覽，只能在 Blob 儲存體的特定區域中使用 SSE。</span><span class="sxs-lookup"><span data-stu-id="55ff9-182">A: SSE is available in only certain regions for Blob storage for this Preview.</span></span> <span data-ttu-id="55ff9-183">請寄電子郵件至 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com)，查詢預覽的可用性與詳細資料。</span><span class="sxs-lookup"><span data-stu-id="55ff9-183">Please email [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) to check for availability and details on preview.</span></span> 

<span data-ttu-id="55ff9-184">**問︰如果我有任何問題或想要提供意見反應，要如何連絡相關人員？**</span><span class="sxs-lookup"><span data-stu-id="55ff9-184">**Q: How do I contact someone if I have any issues or want to provide feedback?**</span></span>

<span data-ttu-id="55ff9-185">答︰如果有儲存體服務加密的相關問題，請連絡 [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) 。</span><span class="sxs-lookup"><span data-stu-id="55ff9-185">A: Please contact [ssediscussions@microsoft.com](mailto:ssediscussions@microsoft.com) for any issues related to Storage Service Encryption.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="55ff9-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55ff9-186">Next steps</span></span>

*   <span data-ttu-id="55ff9-187">如需協助開發人員建置安全應用程式之全方位安全功能的詳細資訊，請參閱[儲存體安全性指南](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-187">For more information on the comprehensive set of security capabilities that help developers build secure applications, please see the [Storage Security Guide](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).</span></span>
*   <span data-ttu-id="55ff9-188">如需 Azure Key Vault 的概觀資訊，請參閱[什麼是 Azure Key Vault？](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)</span><span class="sxs-lookup"><span data-stu-id="55ff9-188">For overview information about Azure Key Vault, see [What is Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?</span></span>
*   <span data-ttu-id="55ff9-189">若要開始使用 Azure Key Vault，請參閱[開始使用 Azure Key Vault](../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="55ff9-189">For getting started on Azure Key Vault, see [Getting Started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
