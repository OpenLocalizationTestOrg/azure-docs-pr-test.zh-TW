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
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>在 Azure Key Vault 中使用客戶管理金鑰進行儲存體服務加密

Microsoft Azure 是強式認可的 toohelping 保護，並保護資料 toomeet 您組織的安全性和相容性所做的認可。  您可以保護您的待用資料的一個方式是 toouse 儲存體服務加密 (SSE) 中，以自動將您的資料加密時寫入 toostorage，和擷取它時，會解密資料。 hello 加密和解密為自動和完全透明，並使用 256 位元[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，hello 最強的區塊的其中一個這類編碼器使用。

您可以搭配 SSE 使用 Microsoft 管理的加密金鑰，或使用自己的加密金鑰。 這篇文章會討論 hello 後者。 如需有關使用 Microsoft 管理之金鑰的詳細資訊，或有關 SSE 的一般資訊，請參閱[待用資料的儲存體服務加密](storage-service-encryption.md)。

tooprovide hello 能力 toouse 整合您自己的加密金鑰，SSE 的 Blob 儲存體與 Azure 金鑰保存庫 (AKV)。 您可以建立您自己的加密金鑰，並將其儲存在保存，或者您可以使用保存的應用程式開發介面 toogenerate 加密金鑰。 不僅沒有 AKV toomanage 可讓您控制您的金鑰，它也可讓您 tooaudit 您金鑰的使用方式。 

為什麼需要 toocreate 您自己的金鑰？ 它可讓您更大的彈性，包括 hello 能力 toocreate、 旋轉、 停用，並定義存取控制和 tooaudit hello 加密用金鑰 tooprotect 您的資料。

## <a name="sse-with-customer-managed-keys-preview"></a>使用客戶管理之金鑰的 SSE 預覽

此功能目前為預覽狀態。 toouse 這項功能，您需要 toocreate 新的儲存體帳戶。 您可以建立新金鑰保存庫與金鑰，或者可以使用現有金鑰保存庫與金鑰。 hello 儲存體帳戶和 hello 金鑰保存庫必須在 hello 相同區域中，但它們可以是不同的訂用帳戶中。

在 hello 預覽 tooparticipate 請連絡[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)。我們將提供的特殊連結 tooparticipate hello 預覽中。

toolearn 詳細資訊，請參閱 toohello[常見問題集](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)。

> [!IMPORTANT]
> 您必須註冊 hello 預覽先前 toofollowing 本文中的 hello 步驟。 沒有預覽存取，您將不會無法 tooenable hello 入口網站中的這項功能。

## <a name="getting-started"></a>開始使用
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>步驟 1：[建立新的儲存體帳戶](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>步驟 2︰啟用加密
您可以使用 hello hello 儲存體帳戶啟用 SSE [Azure 入口網站](https://portal.azure.com)。 在 hello 設定刀鋒視窗中的 hello 儲存體帳戶，尋找 hello 如下圖所示的 Blob 服務 > 一節，按一下 [加密]。

![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption/image1.png)
<br/>*為 Blob 服務啟用 SSE*

如果您想 tooprogrammatically 啟用或停用的儲存體帳戶的儲存體服務加密 hello 時，您可以使用 hello [Azure 儲存體資源提供者 REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)，hello[儲存體資源提供者用戶端程式庫適用於.NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN)， [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0)，或使用 hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli)。

在這個畫面上，如果您看 hello [使用您自己的金鑰] 核取方塊，您有尚未核准 hello 預覽。 請傳送電子郵件太[ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)和要求核准。

![顯示 [加密預覽] 的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

根據預設，SSE 將使用 Microsoft 管理的金鑰。 toouse 您自己的金鑰，請檢查 hello 方塊。 然後您可以指定的 URI，您的金鑰，或從 hello 選擇器選取金鑰和金鑰保存庫。

## <a name="step-3-select-your-key"></a>步驟 3：選取您的金鑰

![顯示 [使用您自己的金鑰加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![顯示 [透過輸入金鑰 URI 來加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

如果 hello 儲存體帳戶沒有存取 toohello 金鑰保存庫，您可以執行 hello 下列命令： 使用 Azure Powershell toogrant 存取 toohello 儲存體帳戶 toohello 需要金鑰保存庫。

![顯示金鑰保存庫存取遭拒的入口網站螢幕擷取畫面](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

您也可以移 toohello Azure 金鑰保存庫中 hello Azure 入口網站並授與存取 toohello 儲存體帳戶授與透過 hello Azure 入口網站的存取。

## <a name="step-4-copy-data-toostorage-account"></a>步驟 4： 複製資料 toostorage 帳戶
如果您想要 tootransfer 資料到新的儲存體帳戶，讓它已經加密，請參閱太[步驟 3 的快速入門中的待用資料的儲存體服務加密](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account)。

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>步驟 5: Hello 查詢 hello 狀態加密資料
tooquery hello 狀態的 hello 加密資料，請參閱太[步驟 4 的快速入門中的待用資料的儲存體服務加密](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data)。

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>待用資料的儲存體服務加密的常見問題集
**問︰我正在使用進階儲存體，是否可以使用具有客戶管理之金鑰的 SSE？**

答：是，在標準儲存體和進階儲存體上都支援搭配 Microsoft 管理與客戶管理之金鑰使用 SSE。 

**問：是否可以搭配客戶管理的金鑰 \(使用 Azure PowerShell 和 Azure CLI 啟用\) 使用 SSE 建立新儲存體帳戶？**

答：是。

**問：如果啟用使用客戶管理金鑰的 SSE，Azure 儲存體的成本會多出多少？**

答：使用 Azure Key Vault 有相關成本。 如需詳細資訊，請瀏覽 [Key Vault 定價](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。 使用 SSE 不會產生額外的費用。

**問： 是否可以撤銷存取 toohello 加密金鑰？**

答：是，您可以隨時撤銷存取權。 有幾個方式 toorevoke 存取 tooyour 索引鍵。 請參閱太[Azure 金鑰保存庫 PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0)和[Azure 金鑰保存庫 CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault)如需詳細資訊。 因為 hello 帳戶加密金鑰是無法存取 Azure 儲存體，撤銷存取權可以有效地會封鎖存取 tooall blob hello 儲存體帳戶中。

**問：是否可以在不同的區域建立儲存體帳戶和金鑰？**

答： 否，hello 儲存體帳戶和金鑰的保存庫金鑰需要 toobe 在 hello 相同的區域。 

**問： 是否可以啟用 SSE 受管理的客戶索引鍵的同時建立 hello 儲存體帳戶？**

答：否。 當您啟用 SSE 建立 hello 儲存體帳戶時，您只能使用 Microsoft 受管理的金鑰。 如果您想要 toouse 由客戶管理金鑰必須 tooupdate hello 儲存體帳戶屬性。 您可以使用 REST 或其中一個 hello 儲存體用戶端程式庫 tooprogrammatically 更新您的儲存體帳戶，或更新 hello 建立 hello 帳戶後使用 hello Azure 入口網站的儲存體帳戶屬性。

**問：使用具有客戶管理之金鑰的 SSE 時是否可以停用加密？**

答：否，使用具有客戶管理之金鑰的 SSE 時無法停用加密。 toodisable 加密，您將需要 tooswitch toousing Microsoft 受管理的金鑰。 您可以使用 hello Azure 入口網站或 PowerShell。

**問︰我建立新的儲存體帳戶時是否預設啟用 SSE？**

答： SSE 不會啟用預設值;您可以使用 Azure 入口網站 tooenable hello 它。 您可以也以程式設計方式啟用此功能使用 hello 儲存體資源提供者 REST API。 

**問︰我無法在我的儲存體帳戶上啟用加密。**

答︰這是 Resource Manager 儲存體帳戶嗎？ 不支援傳統儲存體帳戶。 也只能對新建立的資源管理員儲存體帳戶啟用使用客戶管理之金鑰的 SSE。

**問：是否只在特定區域中允許使用客戶管理之金鑰的 SSE？**

答：針對這個預覽，只能在 Blob 儲存體的特定區域中使用 SSE。 請寄電子郵件[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck 可用性和預覽的詳細資訊。 

**問： 如何連絡有人如果我有任何問題或想 tooprovide 意見反應？**

答： 請連絡[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)是否有任何問題相關 tooStorage 服務加密。 

## <a name="next-steps"></a>後續步驟

*   如需有關 hello 一組完整的安全性功能，可協助開發人員建立安全的應用程式，請參閱 hello[存放安全性指南 》](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide)。
*   如需 Azure Key Vault 的概觀資訊，請參閱[什麼是 Azure Key Vault？](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)
*   若要開始使用 Azure Key Vault，請參閱[開始使用 Azure Key Vault](../key-vault/key-vault-get-started.md)。
