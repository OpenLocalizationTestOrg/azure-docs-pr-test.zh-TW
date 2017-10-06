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
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="d28e9-103">以 hello Azure 入口網站建立 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="d28e9-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d28e9-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d28e9-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="d28e9-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="d28e9-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="d28e9-106">了解如何 toocreate Azure Batch 帳戶 hello [Azure 入口網站][azure_portal]，然後選擇適合您運算案例的 hello 帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="d28e9-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="d28e9-107">了解 toofind 重要的帳戶內容要存取金鑰和帳戶 Url 的位置。</span><span class="sxs-lookup"><span data-stu-id="d28e9-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="d28e9-108">如需批次帳戶和案例的背景，請參閱 hello[功能概觀](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="d28e9-109">建立批次帳戶：</span><span class="sxs-lookup"><span data-stu-id="d28e9-109">Create a Batch account</span></span>

<span data-ttu-id="d28e9-110">使用其中一個 hello 兩個中的 hello 入口 toocreate 批次帳戶*集區配置模式*:**批次服務**模式或使用較新的 hello**使用者訂用帳戶**模式，因此需要更多組態設定。</span><span class="sxs-lookup"><span data-stu-id="d28e9-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="d28e9-111">這兩種模式的相關資訊，請參閱 hello[功能概觀](batch-api-basics.md#account)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="d28e9-112">如需 hello 使用者訂用帳戶模式的功能，請參閱 hello[部落格文章](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="d28e9-113">Batch 服務模式</span><span class="sxs-lookup"><span data-stu-id="d28e9-113">Batch service mode</span></span>



1. <span data-ttu-id="d28e9-114">登入 toohello [Azure 入口網站][azure_portal]。</span><span class="sxs-lookup"><span data-stu-id="d28e9-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="d28e9-115">按一下 [新增]  >  [計算]   >  [Batch 服務]。</span><span class="sxs-lookup"><span data-stu-id="d28e9-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Hello Marketplace 中的批次][marketplace_portal]
3. <span data-ttu-id="d28e9-117">hello**新批次帳戶**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="d28e9-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="d28e9-118">請參閱下方的 hello 描述的每個刀鋒視窗中的項目。</span><span class="sxs-lookup"><span data-stu-id="d28e9-118">See hello descriptions below of each blade element.</span></span>

    ![建立批次帳戶：][account_portal]

    <span data-ttu-id="d28e9-120">a.</span><span class="sxs-lookup"><span data-stu-id="d28e9-120">a.</span></span> <span data-ttu-id="d28e9-121">**帳戶名稱**: hello 您所選擇的批次帳戶名稱內必須是唯一 hello hello 帳戶建立所在的 Azure 區域 (請參閱**位置**下方)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="d28e9-122">hello 帳戶名稱可能只能包含小寫字元或數字，而且必須是長度為 3-24 個字元。</span><span class="sxs-lookup"><span data-stu-id="d28e9-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="d28e9-123">b.</span><span class="sxs-lookup"><span data-stu-id="d28e9-123">b.</span></span> <span data-ttu-id="d28e9-124">**訂用帳戶**: hello 哪些 toocreate hello 批次帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="d28e9-125">如果您只有一個訂用帳戶，則預設會選取此項目。</span><span class="sxs-lookup"><span data-stu-id="d28e9-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="d28e9-126">c.</span><span class="sxs-lookup"><span data-stu-id="d28e9-126">c.</span></span> <span data-ttu-id="d28e9-127">**集區配置模式**︰選取 **Batch 服務**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="d28e9-128">c.</span><span class="sxs-lookup"><span data-stu-id="d28e9-128">c.</span></span> <span data-ttu-id="d28e9-129">**資源群組**：為新的 Batch 帳戶選取現有的資源群組，或選擇性地建立一個新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d28e9-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="d28e9-130">d.</span><span class="sxs-lookup"><span data-stu-id="d28e9-130">d.</span></span> <span data-ttu-id="d28e9-131">**位置**: hello 中哪些 toocreate hello 批次帳戶的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="d28e9-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="d28e9-132">只支援您的訂用帳戶和資源群組 hello 區域會顯示為選項。</span><span class="sxs-lookup"><span data-stu-id="d28e9-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="d28e9-133">e.</span><span class="sxs-lookup"><span data-stu-id="d28e9-133">e.</span></span> <span data-ttu-id="d28e9-134">**儲存體帳戶** (選用)：與 Batch 帳戶相關聯的一般用途 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="d28e9-135">這是大部分 Batch 帳戶的建議作法。</span><span class="sxs-lookup"><span data-stu-id="d28e9-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="d28e9-136">如需詳細資訊，請參閱本文稍後的[連結的 Azure 儲存體帳戶](#linked-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="d28e9-137">按一下**建立**toocreate hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="d28e9-138">hello 入口網站會指出部署正在進行中。</span><span class="sxs-lookup"><span data-stu-id="d28e9-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="d28e9-139">完成時，**通知**中會出現**部署成功**通知。</span><span class="sxs-lookup"><span data-stu-id="d28e9-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="d28e9-140">使用者訂用帳戶模式</span><span class="sxs-lookup"><span data-stu-id="d28e9-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="d28e9-141">允許 Azure Batch tooaccess hello 訂用帳戶 （一次性）</span><span class="sxs-lookup"><span data-stu-id="d28e9-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="d28e9-142">您第一批次中建立帳戶時使用者訂用帳戶模式，執行下列步驟 tooregister hello 訂用帳戶與批次。</span><span class="sxs-lookup"><span data-stu-id="d28e9-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="d28e9-143">（如果您先前已，略過 toohello 下一節）。</span><span class="sxs-lookup"><span data-stu-id="d28e9-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="d28e9-144">登入 toohello [Azure 入口網站][azure_portal]。</span><span class="sxs-lookup"><span data-stu-id="d28e9-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="d28e9-145">按一下**更服務** > **訂閱**，然後按一下您想要 hello 批次帳戶 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="d28e9-146">在 hello**訂用帳戶**刀鋒視窗中，按一下 **存取控制 (IAM)** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![訂用帳戶存取控制][subscription_access]

4. <span data-ttu-id="d28e9-148">在 hello**新增權限**刀鋒視窗中，選取 hello**參與者**角色中，搜尋 hello 批次 API。</span><span class="sxs-lookup"><span data-stu-id="d28e9-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="d28e9-149">針對每個這些字串的搜尋，直到您找到 hello API:</span><span class="sxs-lookup"><span data-stu-id="d28e9-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="d28e9-150">**MicrosoftAzureBatch**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="d28e9-151">**Microsoft Azure Batch**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="d28e9-152">較新的 Azure AD 租用戶可以使用這個名稱。</span><span class="sxs-lookup"><span data-stu-id="d28e9-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="d28e9-153">**ddbf3205-c6bd-46ae-8127-60eb93363864**是 hello 識別碼 hello 批次 API。</span><span class="sxs-lookup"><span data-stu-id="d28e9-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="d28e9-154">一旦您找到 hello 批次 API，請選取它，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![新增 Batch 權限][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="d28e9-156">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="d28e9-156">Create a key vault</span></span>
<span data-ttu-id="d28e9-157">使用者訂用帳戶模式中，Azure 金鑰保存庫是必要的所屬 toothe 建立 hello 批次帳戶 toobe 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="d28e9-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="d28e9-158">請確定 hello 資源群組是在批次所在的區域[可用](https://azure.microsoft.com/regions/services/)和訂用帳戶支援。</span><span class="sxs-lookup"><span data-stu-id="d28e9-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="d28e9-159">在 hello [Azure 入口網站][azure_portal]，按一下 **新增** > **安全性 + 身分識別** > **金鑰保存庫**.</span><span class="sxs-lookup"><span data-stu-id="d28e9-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="d28e9-160">在 hello**建立金鑰保存庫**刀鋒視窗中，輸入 hello 金鑰保存庫的名稱和您想要用於您的 Batch 帳戶的 hello 區域中建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="d28e9-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="d28e9-161">保留 hello 剩餘的預設值，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="d28e9-162">建立批次帳戶：</span><span class="sxs-lookup"><span data-stu-id="d28e9-162">Create a Batch account</span></span>

1. <span data-ttu-id="d28e9-163">在 hello [Azure 入口網站][azure_portal]，按一下 **新增** > **計算** > **批次服務**.</span><span class="sxs-lookup"><span data-stu-id="d28e9-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Hello Marketplace 中的批次][marketplace_portal]
3. <span data-ttu-id="d28e9-165">hello**新批次帳戶**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="d28e9-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="d28e9-166">請參閱下方的 hello 描述的每個刀鋒視窗中的項目。</span><span class="sxs-lookup"><span data-stu-id="d28e9-166">See hello descriptions below of each blade element.</span></span>

    ![建立批次帳戶：][account_portal_byos]

    <span data-ttu-id="d28e9-168">a.</span><span class="sxs-lookup"><span data-stu-id="d28e9-168">a.</span></span> <span data-ttu-id="d28e9-169">**帳戶名稱**: hello 您所選擇的批次帳戶名稱內必須是唯一 hello hello 帳戶建立所在的 Azure 區域 (請參閱**位置**下方)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="d28e9-170">hello 帳戶名稱可能只能包含小寫字元或數字，而且必須是長度為 3-24 個字元。</span><span class="sxs-lookup"><span data-stu-id="d28e9-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="d28e9-171">b.</span><span class="sxs-lookup"><span data-stu-id="d28e9-171">b.</span></span> <span data-ttu-id="d28e9-172">**訂用帳戶**： 如果您有多個訂閱，選取您已向 hello 批次服務的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="d28e9-173">c.</span><span class="sxs-lookup"><span data-stu-id="d28e9-173">c.</span></span> <span data-ttu-id="d28e9-174">**集區配置模式**︰選取 [使用者訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="d28e9-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="d28e9-175">d.</span><span class="sxs-lookup"><span data-stu-id="d28e9-175">d.</span></span> <span data-ttu-id="d28e9-176">**金鑰保存庫**: hello 選取您為您的 Batch 帳戶 hello 前一節中建立的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d28e9-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="d28e9-177">選擇性地，建立新的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="d28e9-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="d28e9-178">選取 hello 保存庫之後, 再選擇 hello 核取方塊 toogrant Azure 批次存取 toohello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d28e9-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="d28e9-179">c.</span><span class="sxs-lookup"><span data-stu-id="d28e9-179">c.</span></span> <span data-ttu-id="d28e9-180">**資源群組**： 您可以在其中建立金鑰保存庫 hello 選取 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d28e9-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="d28e9-181">d.</span><span class="sxs-lookup"><span data-stu-id="d28e9-181">d.</span></span> <span data-ttu-id="d28e9-182">**位置**: hello Azure 區域，您可以在其中建立 hello hello 批次帳戶的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d28e9-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="d28e9-183">e.</span><span class="sxs-lookup"><span data-stu-id="d28e9-183">e.</span></span> <span data-ttu-id="d28e9-184">**儲存體帳戶** (選用)：與 Batch 帳戶相關聯的一般用途 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="d28e9-185">這是大部分 Batch 帳戶的建議作法。</span><span class="sxs-lookup"><span data-stu-id="d28e9-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="d28e9-186">如需詳細資訊，請參閱下面的[連結的 Azure 儲存體帳戶](#linked-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="d28e9-187">按一下**建立**toocreate hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="d28e9-188">hello 入口網站會指出部署正在進行中。</span><span class="sxs-lookup"><span data-stu-id="d28e9-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="d28e9-189">完成時，**通知**中會出現**部署成功**通知。</span><span class="sxs-lookup"><span data-stu-id="d28e9-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="d28e9-190">檢視 Batch 帳戶屬性</span><span class="sxs-lookup"><span data-stu-id="d28e9-190">View Batch account properties</span></span>
<span data-ttu-id="d28e9-191">一旦建立 hello 帳戶之後，您可以開啟 hello**批次帳戶 刀鋒視窗**tooaccess 其設定和屬性。</span><span class="sxs-lookup"><span data-stu-id="d28e9-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="d28e9-192">您可以使用 hello hello 批次帳戶 刀鋒視窗的左邊的功能表存取所有帳戶設定和屬性。</span><span class="sxs-lookup"><span data-stu-id="d28e9-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Azure 入口網站中的 Batch 帳戶刀鋒視窗][account_blade]

* <span data-ttu-id="d28e9-194">**批次帳戶 URL**： 當您開發應用程式以 hello[批次 Api](batch-apis-tools.md#azure-accounts-for-batch-development)，您將需要帳戶 URL tooaccess 批次資源。</span><span class="sxs-lookup"><span data-stu-id="d28e9-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="d28e9-195">批次帳戶 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d28e9-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![入口網站中的 Batch 帳戶 URL][account_url]

* <span data-ttu-id="d28e9-197">**存取金鑰**（批次服務模式）： tooauthenticate 存取 tooyour 批次帳戶從您的應用程式，您將需要的帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d28e9-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="d28e9-198">(此設定在您使用 Azure Active Directory 驗證的使用者訂用帳戶模式中無法使用。)</span><span class="sxs-lookup"><span data-stu-id="d28e9-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="d28e9-199">tooview 或重新建立您的 Batch 帳戶存取金鑰，請輸入`keys`hello 左功能表中**搜尋**hello 批次帳戶 刀鋒視窗，然後選取**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Azure 入口網站中的 Batch 帳戶金鑰][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="d28e9-201">連結的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d28e9-201">Linked Azure Storage account</span></span>

<span data-ttu-id="d28e9-202">您可以選擇性地連結一般用途的 Azure 儲存體帳戶 tooyour Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="d28e9-203">hello[應用程式封裝](batch-application-packages.md)批次的功能會使用 Azure Blob 儲存體，如同 hello[批次檔慣例.NET](batch-task-output.md)程式庫。</span><span class="sxs-lookup"><span data-stu-id="d28e9-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="d28e9-204">這些選擇性功能可協助您部署的 hello 應用程式執行批次工作和它們所產生的保存 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d28e9-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="d28e9-205">我們建議建立 Batch 帳戶專用的新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![建立一般用途的儲存體帳戶][storage_account]

> [!NOTE]
> <span data-ttu-id="d28e9-207">Azure 批次目前支援僅 hello 一般用途儲存體帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="d28e9-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="d28e9-208">此帳戶類型如[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的步驟 5 [建立儲存體帳戶] (../storage/common/storage-create-storage-account.md#create-a-storage-account) 所述。</span><span class="sxs-lookup"><span data-stu-id="d28e9-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="d28e9-209">重新產生連結的儲存體帳戶的 hello 便捷鍵時要小心。</span><span class="sxs-lookup"><span data-stu-id="d28e9-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="d28e9-210">重新產生只能有一個儲存體帳戶金鑰，並按一下**同步金鑰**hello 上連結儲存體帳戶 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d28e9-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="d28e9-211">稍候五分鐘 tooallow hello 金鑰 toopropagate toohello 程式集區中的計算節點，然後重新產生，並同步處理 hello 其他必要的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d28e9-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="d28e9-212">如果您重新產生金鑰在 hello 相同時，計算節點將不會無法 toosynchronize 任一個索引鍵，而且他們將會遺失存取 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="d28e9-213">![重新產生儲存體帳戶金鑰][4]</span><span class="sxs-lookup"><span data-stu-id="d28e9-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="d28e9-214">Batch 服務配額和限制</span><span class="sxs-lookup"><span data-stu-id="d28e9-214">Batch service quotas and limits</span></span>
<span data-ttu-id="d28e9-215">請要注意，為您的 Azure 訂閱與其他 Azure 服務，某些[配額和限制](batch-quota-limit.md)套用 tooBatch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d28e9-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="d28e9-216">目前批次帳戶的配額會出現在 hello 帳戶中的 hello 入口網站**屬性**。</span><span class="sxs-lookup"><span data-stu-id="d28e9-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Azure 入口網站中的 Batch 帳戶配額][quotas]



<span data-ttu-id="d28e9-218">此外，許多這些配額可以增加只需使用免費的產品支援要求送出 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d28e9-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="d28e9-219">請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)如要求增加配額的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d28e9-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="d28e9-220">其他 Batch 帳戶管理選項</span><span class="sxs-lookup"><span data-stu-id="d28e9-220">Other Batch account management options</span></span>
<span data-ttu-id="d28e9-221">此外 toousing hello Azure 入口網站，您也可以建立及管理 hello 下列批次帳戶：</span><span class="sxs-lookup"><span data-stu-id="d28e9-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="d28e9-222">Batch PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="d28e9-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="d28e9-223">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d28e9-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="d28e9-224">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="d28e9-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="d28e9-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d28e9-225">Next steps</span></span>
* <span data-ttu-id="d28e9-226">請參閱 hello[批次功能概觀](batch-api-basics.md)toolearn 更多關於批次服務概念和功能。</span><span class="sxs-lookup"><span data-stu-id="d28e9-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="d28e9-227">hello 文章討論 hello 主要批次資源集區、 計算節點、 工作和工作，例如，並提供概觀 hello 服務的功能，可大規模的運算工作負載執行。</span><span class="sxs-lookup"><span data-stu-id="d28e9-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="d28e9-228">了解 hello 基本概念的開發批次啟用應用程式使用 hello[批次.NET 用戶端程式庫](batch-dotnet-get-started.md)或[Python](batch-python-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d28e9-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="d28e9-229">這些簡介文章會引導您完成使用 hello 批次服務 tooexecute 工作負載上多個計算節點，並包含使用 Azure 儲存體的工作負載檔案臨時區域與擷取之工作應用程式。</span><span class="sxs-lookup"><span data-stu-id="d28e9-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

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
