---
title: "aaaCreate hello Azure 入口網站中的批次帳戶 |Microsoft 文件"
description: "了解如何 toocreate Azure Batch 帳戶在 Azure 入口網站 toorun hello hello 雲端中大規模的平行工作負載"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>以 hello Azure 入口網站建立 Batch 帳戶

> [!div class="op_single_selector"]
> * [Azure 入口網站](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
>
>

了解如何 toocreate Azure Batch 帳戶 hello [Azure 入口網站][azure_portal]，然後選擇適合您運算案例的 hello 帳戶屬性。 了解 toofind 重要的帳戶內容要存取金鑰和帳戶 Url 的位置。

如需批次帳戶和案例的背景，請參閱 hello[功能概觀](batch-api-basics.md)。



## <a name="create-a-batch-account"></a>建立批次帳戶：

使用其中一個 hello 兩個中的 hello 入口 toocreate 批次帳戶*集區配置模式*:**批次服務**模式或使用較新的 hello**使用者訂用帳戶**模式，因此需要更多組態設定。 這兩種模式的相關資訊，請參閱 hello[功能概觀](batch-api-basics.md#account)。 如需 hello 使用者訂用帳戶模式的功能，請參閱 hello[部落格文章](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/)。

## <a name="batch-service-mode"></a>Batch 服務模式



1. 登入 toohello [Azure 入口網站][azure_portal]。
2. 按一下 [新增]  >  [計算]   >  [Batch 服務]。

    ![Hello Marketplace 中的批次][marketplace_portal]
3. hello**新批次帳戶**刀鋒視窗會顯示。 請參閱下方的 hello 描述的每個刀鋒視窗中的項目。

    ![建立批次帳戶：][account_portal]

    a. **帳戶名稱**: hello 您所選擇的批次帳戶名稱內必須是唯一 hello hello 帳戶建立所在的 Azure 區域 (請參閱**位置**下方)。 hello 帳戶名稱可能只能包含小寫字元或數字，而且必須是長度為 3-24 個字元。

    b. **訂用帳戶**: hello 哪些 toocreate hello 批次帳戶的訂用帳戶。 如果您只有一個訂用帳戶，則預設會選取此項目。

    c. **集區配置模式**︰選取 **Batch 服務**。

    c. **資源群組**：為新的 Batch 帳戶選取現有的資源群組，或選擇性地建立一個新的資源群組。

    d. **位置**: hello 中哪些 toocreate hello 批次帳戶的 Azure 區域。 只支援您的訂用帳戶和資源群組 hello 區域會顯示為選項。

    e. **儲存體帳戶** (選用)：與 Batch 帳戶相關聯的一般用途 Azure 儲存體帳戶。 這是大部分 Batch 帳戶的建議作法。 如需詳細資訊，請參閱本文稍後的[連結的 Azure 儲存體帳戶](#linked-azure-storage-account)。

4. 按一下**建立**toocreate hello 帳戶。

   hello 入口網站會指出部署正在進行中。 完成時，**通知**中會出現**部署成功**通知。

## <a name="user-subscription-mode"></a>使用者訂用帳戶模式

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>允許 Azure Batch tooaccess hello 訂用帳戶 （一次性）
您第一批次中建立帳戶時使用者訂用帳戶模式，執行下列步驟 tooregister hello 訂用帳戶與批次。 （如果您先前已，略過 toohello 下一節）。

1. 登入 toohello [Azure 入口網站][azure_portal]。

2. 按一下**更服務** > **訂閱**，然後按一下您想要 hello 批次帳戶 toouse hello 訂用帳戶。

3. 在 hello**訂用帳戶**刀鋒視窗中，按一下 **存取控制 (IAM)** > **新增**。

    ![訂用帳戶存取控制][subscription_access]

4. 在 hello**新增權限**刀鋒視窗中，選取 hello**參與者**角色中，搜尋 hello 批次 API。 針對每個這些字串的搜尋，直到您找到 hello API:
    1. **MicrosoftAzureBatch**。
    2. **Microsoft Azure Batch**。 較新的 Azure AD 租用戶可以使用這個名稱。
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864**是 hello 識別碼 hello 批次 API。 

5. 一旦您找到 hello 批次 API，請選取它，然後按一下**儲存**。

    ![新增 Batch 權限][add_permission]

### <a name="create-a-key-vault"></a>建立金鑰保存庫
使用者訂用帳戶模式中，Azure 金鑰保存庫是必要的所屬 toothe 建立 hello 批次帳戶 toobe 相同資源群組。 請確定 hello 資源群組是在批次所在的區域[可用](https://azure.microsoft.com/regions/services/)和訂用帳戶支援。

1. 在 hello [Azure 入口網站][azure_portal]，按一下 **新增** > **安全性 + 身分識別** > **金鑰保存庫**.

2. 在 hello**建立金鑰保存庫**刀鋒視窗中，輸入 hello 金鑰保存庫的名稱和您想要用於您的 Batch 帳戶的 hello 區域中建立資源群組。 保留 hello 剩餘的預設值，然後按一下 **建立**。

### <a name="create-a-batch-account"></a>建立批次帳戶：

1. 在 hello [Azure 入口網站][azure_portal]，按一下 **新增** > **計算** > **批次服務**.

    ![Hello Marketplace 中的批次][marketplace_portal]
3. hello**新批次帳戶**刀鋒視窗會顯示。 請參閱下方的 hello 描述的每個刀鋒視窗中的項目。

    ![建立批次帳戶：][account_portal_byos]

    a. **帳戶名稱**: hello 您所選擇的批次帳戶名稱內必須是唯一 hello hello 帳戶建立所在的 Azure 區域 (請參閱**位置**下方)。 hello 帳戶名稱可能只能包含小寫字元或數字，而且必須是長度為 3-24 個字元。

    b. **訂用帳戶**： 如果您有多個訂閱，選取您已向 hello 批次服務的 hello 訂用帳戶。

    c. **集區配置模式**︰選取 [使用者訂用帳戶]。

    d. **金鑰保存庫**: hello 選取您為您的 Batch 帳戶 hello 前一節中建立的金鑰保存庫。 選擇性地，建立新的 Key Vault。 選取 hello 保存庫之後, 再選擇 hello 核取方塊 toogrant Azure 批次存取 toohello 金鑰保存庫。

    c. **資源群組**： 您可以在其中建立金鑰保存庫 hello 選取 hello 資源群組。

    d. **位置**: hello Azure 區域，您可以在其中建立 hello hello 批次帳戶的金鑰保存庫。

    e. **儲存體帳戶** (選用)：與 Batch 帳戶相關聯的一般用途 Azure 儲存體帳戶。 這是大部分 Batch 帳戶的建議作法。 如需詳細資訊，請參閱下面的[連結的 Azure 儲存體帳戶](#linked-azure-storage-account)。

4. 按一下**建立**toocreate hello 帳戶。

   hello 入口網站會指出部署正在進行中。 完成時，**通知**中會出現**部署成功**通知。



## <a name="view-batch-account-properties"></a>檢視 Batch 帳戶屬性
一旦建立 hello 帳戶之後，您可以開啟 hello**批次帳戶 刀鋒視窗**tooaccess 其設定和屬性。 您可以使用 hello hello 批次帳戶 刀鋒視窗的左邊的功能表存取所有帳戶設定和屬性。

![Azure 入口網站中的 Batch 帳戶刀鋒視窗][account_blade]

* **批次帳戶 URL**： 當您開發應用程式以 hello[批次 Api](batch-apis-tools.md#azure-accounts-for-batch-development)，您將需要帳戶 URL tooaccess 批次資源。 批次帳戶 URL 具有下列格式的 hello:

    `https://<account_name>.<region>.batch.azure.com`

![入口網站中的 Batch 帳戶 URL][account_url]

* **存取金鑰**（批次服務模式）： tooauthenticate 存取 tooyour 批次帳戶從您的應用程式，您將需要的帳戶存取金鑰。 (此設定在您使用 Azure Active Directory 驗證的使用者訂用帳戶模式中無法使用。)

    tooview 或重新建立您的 Batch 帳戶存取金鑰，請輸入`keys`hello 左功能表中**搜尋**hello 批次帳戶 刀鋒視窗，然後選取**金鑰**。

    ![Azure 入口網站中的 Batch 帳戶金鑰][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>連結的 Azure 儲存體帳戶

您可以選擇性地連結一般用途的 Azure 儲存體帳戶 tooyour Batch 帳戶。 hello[應用程式封裝](batch-application-packages.md)批次的功能會使用 Azure Blob 儲存體，如同 hello[批次檔慣例.NET](batch-task-output.md)程式庫。 這些選擇性功能可協助您部署的 hello 應用程式執行批次工作和它們所產生的保存 hello 資料。

我們建議建立 Batch 帳戶專用的新儲存體帳戶。

![建立一般用途的儲存體帳戶][storage_account]

> [!NOTE]
> Azure 批次目前支援僅 hello 一般用途儲存體帳戶類型。 此帳戶類型如[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的步驟 5 [建立儲存體帳戶] (../storage/common/storage-create-storage-account.md#create-a-storage-account) 所述。
>
>

> [!WARNING]
> 重新產生連結的儲存體帳戶的 hello 便捷鍵時要小心。 重新產生只能有一個儲存體帳戶金鑰，並按一下**同步金鑰**hello 上連結儲存體帳戶 刀鋒視窗。 稍候五分鐘 tooallow hello 金鑰 toopropagate toohello 程式集區中的計算節點，然後重新產生，並同步處理 hello 其他必要的索引鍵。 如果您重新產生金鑰在 hello 相同時，計算節點將不會無法 toosynchronize 任一個索引鍵，而且他們將會遺失存取 toohello 儲存體帳戶。
>
>

![重新產生儲存體帳戶金鑰][4]

## <a name="batch-service-quotas-and-limits"></a>Batch 服務配額和限制
請要注意，為您的 Azure 訂閱與其他 Azure 服務，某些[配額和限制](batch-quota-limit.md)套用 tooBatch 帳戶。 目前批次帳戶的配額會出現在 hello 帳戶中的 hello 入口網站**屬性**。

![Azure 入口網站中的 Batch 帳戶配額][quotas]



此外，許多這些配額可以增加只需使用免費的產品支援要求送出 hello Azure 入口網站中。 請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)如要求增加配額的詳細資訊。

## <a name="other-batch-account-management-options"></a>其他 Batch 帳戶管理選項
此外 toousing hello Azure 入口網站，您也可以建立及管理 hello 下列批次帳戶：

* [Batch PowerShell Cmdlet](batch-powershell-cmdlets-get-started.md)
* [Azure CLI](batch-cli-get-started.md)
* [Batch Management .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>後續步驟
* 請參閱 hello[批次功能概觀](batch-api-basics.md)toolearn 更多關於批次服務概念和功能。 hello 文章討論 hello 主要批次資源集區、 計算節點、 工作和工作，例如，並提供概觀 hello 服務的功能，可大規模的運算工作負載執行。
* 了解 hello 基本概念的開發批次啟用應用程式使用 hello[批次.NET 用戶端程式庫](batch-dotnet-get-started.md)或[Python](batch-python-tutorial.md)。 這些簡介文章會引導您完成使用 hello 批次服務 tooexecute 工作負載上多個計算節點，並包含使用 Azure 儲存體的工作負載檔案臨時區域與擷取之工作應用程式。

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "重新產生儲存體帳戶金鑰"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
