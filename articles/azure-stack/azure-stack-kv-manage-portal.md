---
title: "使用 PowerShell 的 Azure 堆疊中的金鑰保存庫 aaaManage |Microsoft 文件"
description: "深入了解如何使用 PowerShell 的 Azure 堆疊中的金鑰保存庫 toomanage。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a><span data-ttu-id="1121d-103">管理 Azure 堆疊使用 hello 入口網站中的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="1121d-103">Manage Key Vault in Azure Stack using hello portal</span></span>

<span data-ttu-id="1121d-104">您可以使用 hello Azure 堆疊入口網站來管理 Azure 堆疊中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="1121d-104">You can manage Key Vault in Azure Stack by using hello Azure Stack portal.</span></span> <span data-ttu-id="1121d-105">這篇文章可協助您取得啟動的 toocreate 並管理 Azure 堆疊中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="1121d-105">This article helps you get started toocreate and manage Key Vault in Azure Stack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1121d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="1121d-106">Prerequisites</span></span>  

* <span data-ttu-id="1121d-107">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="1121d-107">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="1121d-108">使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="1121d-108">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
 
## <a name="create-a-key-vault"></a><span data-ttu-id="1121d-109">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="1121d-109">Create a key vault</span></span> 

1. <span data-ttu-id="1121d-110">登入 toohello 使用者入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="1121d-110">Sign in toohello user portal(https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="1121d-111">從 hello 儀表板中，按一下 **新增 > 安全性 + 身分識別 > 金鑰保存庫**。</span><span class="sxs-lookup"><span data-stu-id="1121d-111">From hello dashboard, click **New > Security + Identity > Key Vault**.</span></span>  

    ![KV 畫面](media/azure-stack-kv-manage-portal/image1.png)  

3. <span data-ttu-id="1121d-113">在 hello**建立金鑰保存庫**刀鋒視窗中，指派**名稱**您保存庫。</span><span class="sxs-lookup"><span data-stu-id="1121d-113">On hello **Create Key Vault** blade, assign a **Name** for your vault.</span></span> <span data-ttu-id="1121d-114">保存庫名稱只能包含英數字元、 hello 特殊字元連字號 （-），而且不應該以開頭數字。</span><span class="sxs-lookup"><span data-stu-id="1121d-114">Vault name can contain only alphanumeric characters, hello special character hyphen (-), and it shouldn’t start with a number.</span></span>  

4. <span data-ttu-id="1121d-115">選擇**訂用帳戶**從 hello 可用訂閱清單。</span><span class="sxs-lookup"><span data-stu-id="1121d-115">Choose a **Subscription** from hello list of available subscriptions.</span></span> <span data-ttu-id="1121d-116">提供 hello 金鑰保存庫服務的所有訂用帳戶會顯示在 [hello] 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="1121d-116">All subscriptions that offer hello Key Vault service are displayed in hello drop-down.</span></span>  

5. <span data-ttu-id="1121d-117">選取現有的 [資源群組] 或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="1121d-117">Select an existing **Resource Group** or create a new one.</span></span>  

6. <span data-ttu-id="1121d-118">選取 hello**定價層**。</span><span class="sxs-lookup"><span data-stu-id="1121d-118">Select hello **Pricing tier**.</span></span>  
    >[!NOTE]
    > <span data-ttu-id="1121d-119">Azure Stack 開發套件中的金鑰保存庫僅支援**標準**SKU。</span><span class="sxs-lookup"><span data-stu-id="1121d-119">Key vaults in Azure Stack Development Kit support **Standard** SKU only.</span></span>

7. <span data-ttu-id="1121d-120">選取現有的 [存取原則] 或建立新原則。</span><span class="sxs-lookup"><span data-stu-id="1121d-120">Choose an existing **Access policies** or create a new one.</span></span> <span data-ttu-id="1121d-121">存取原則可讓您 toogrant 使用者、 應用程式或安全性權限群組 tooperform 作業與此保存庫。</span><span class="sxs-lookup"><span data-stu-id="1121d-121">Access policy allows you toogrant permissions for a user, application, or a security group tooperform operations with this vault.</span></span>  

8. <span data-ttu-id="1121d-122">（選擇性） 選擇**進階存取權原則**tooenable hello 功能，例如存取 tooVirtual 機器進行部署，存取 tooResource 管理員針對範本部署，以及存取 tooAzure 磁碟加密磁碟區加密。</span><span class="sxs-lookup"><span data-stu-id="1121d-122">Optionally, choose an **Advanced access policy** tooenable hello features like access tooVirtual Machines for deployment, access tooResource Manager for template deployment and access tooAzure Disk Encryption for volume encryption.</span></span> 
  
9.  <span data-ttu-id="1121d-123">設定 hello，完成後，按一下 **確定**然後**建立**。</span><span class="sxs-lookup"><span data-stu-id="1121d-123">After configuring hello settings, click **OK** and then **Create**.</span></span> <span data-ttu-id="1121d-124">這樣會啟動 hello 金鑰保存庫部署。</span><span class="sxs-lookup"><span data-stu-id="1121d-124">This starts hello key vault deployment.</span></span> 

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="1121d-125">管理金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="1121d-125">Manage keys and secrets</span></span>

<span data-ttu-id="1121d-126">建立保存庫之後，請使用下列步驟 toocreate hello，以及管理金鑰和秘密 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="1121d-126">After you create a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

## <a name="create-a-key"></a><span data-ttu-id="1121d-127">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="1121d-127">Create a key</span></span>

1. <span data-ttu-id="1121d-128">登入 toohello 使用者入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="1121d-128">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="1121d-129">從 hello 儀表板中，按一下 **所有資源**> 您先前建立的選取 hello 金鑰保存庫 > 按一下 hello**金鑰**磚。</span><span class="sxs-lookup"><span data-stu-id="1121d-129">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Keys** tile.</span></span>  

3. <span data-ttu-id="1121d-130">從 hello**金鑰**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="1121d-130">From hello **Keys** blade, click **Add**.</span></span> 

4. <span data-ttu-id="1121d-131">在 hello**建立金鑰**刀鋒視窗中，表單 hello 清單**選項**，選擇 hello 方法您想 toouse toocreate 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1121d-131">On hello **Create a key** blade, form hello list of **Options**, choose hello method that you want toouse toocreate a key.</span></span> <span data-ttu-id="1121d-132">您可以 [產生] 新的金鑰、[上傳] 現有金鑰，或是 [還原備份] 金鑰。</span><span class="sxs-lookup"><span data-stu-id="1121d-132">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span></span>  

5. <span data-ttu-id="1121d-133">在 [名稱] 中輸入金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="1121d-133">Enter a **Name** for your key.</span></span> <span data-ttu-id="1121d-134">hello 索引鍵名稱只能包含英數字元和 hello 特殊字元連字號 （-）。</span><span class="sxs-lookup"><span data-stu-id="1121d-134">hello key name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="1121d-135">(選用) 為金鑰設定 [設定啟用日期] 和 [設定到期日期]。</span><span class="sxs-lookup"><span data-stu-id="1121d-135">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span></span>  

7. <span data-ttu-id="1121d-136">按一下**建立**toostart hello 部署。</span><span class="sxs-lookup"><span data-stu-id="1121d-136">Click **Create** toostart hello deployment.</span></span>  

<span data-ttu-id="1121d-137">已成功建立 hello 金鑰之後，可以選取從 hello**金鑰**刀鋒視窗和檢視或修改其屬性。</span><span class="sxs-lookup"><span data-stu-id="1121d-137">After hello key is successfully created, you can select it from hello **Keys** blade and view or modify its properties.</span></span> <span data-ttu-id="1121d-138">hello properties 區段包含 hello**金鑰識別碼**，外部應用程式可以存取此機碼的 URI。</span><span class="sxs-lookup"><span data-stu-id="1121d-138">hello properties section contains hello **Key Identifier**, a URI by which external applications can access this key.</span></span> <span data-ttu-id="1121d-139">此機碼 toolimit 作業下設定設定**允許的作業**。</span><span class="sxs-lookup"><span data-stu-id="1121d-139">toolimit operations on this key, configure settings under **Permitted operations**.</span></span>

![URI 金鑰](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a><span data-ttu-id="1121d-141">建立祕密</span><span class="sxs-lookup"><span data-stu-id="1121d-141">Create a secret</span></span> 

1. <span data-ttu-id="1121d-142">登入 toohello 使用者入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="1121d-142">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  
2. <span data-ttu-id="1121d-143">從 hello 儀表板中，按一下 **所有資源**> 您先前建立的選取 hello 金鑰保存庫 > 按一下 hello**密碼**磚。</span><span class="sxs-lookup"><span data-stu-id="1121d-143">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Secrets** tile.</span></span>  

3. <span data-ttu-id="1121d-144">從 hello**密碼**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="1121d-144">From hello **Secrets** blade, click **Add**.</span></span>  

4. <span data-ttu-id="1121d-145">在 hello**建立密碼**刀鋒視窗中的，從 hello 清單**上傳選項**，選擇要依據的 toocreate 選項的密碼。</span><span class="sxs-lookup"><span data-stu-id="1121d-145">On hello **Create a secret** blade, from hello list of **Upload options**, choose an option by which you want toocreate a secret.</span></span> <span data-ttu-id="1121d-146">您可以建立密碼**手動**hello 密碼的輸入值，或上傳**憑證**從本機電腦。</span><span class="sxs-lookup"><span data-stu-id="1121d-146">You can create a secret **Manually** by entering a value for hello secret, or by uploading a **Certificate** from your local machine.</span></span>  

5. <span data-ttu-id="1121d-147">輸入**名稱**的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="1121d-147">Enter a **Name** for hello secret.</span></span> <span data-ttu-id="1121d-148">hello 秘密名稱只能包含英數字元和 hello 特殊字元連字號 （-）。</span><span class="sxs-lookup"><span data-stu-id="1121d-148">hello secret name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="1121d-149">（選擇性） 指定 hello**內容類型**，以及設定值**設定啟用日期**和**設定到期日**hello 密碼的值。</span><span class="sxs-lookup"><span data-stu-id="1121d-149">Optionally, specify hello **Content type**, and configure values for **Set activation date** and **Set expiration date** values for hello secret.</span></span>  

7. <span data-ttu-id="1121d-150">按一下 建立 toostart hello 部署。</span><span class="sxs-lookup"><span data-stu-id="1121d-150">Click Create toostart hello deployment.</span></span>  

<span data-ttu-id="1121d-151">已成功建立 hello 密碼之後，可以選取從 hello**密碼**刀鋒視窗和檢視或修改其屬性。</span><span class="sxs-lookup"><span data-stu-id="1121d-151">After hello secret is successfully created, you can select it from hello **Secrets** blade and view or modify its properties.</span></span> <span data-ttu-id="1121d-152">hello properties 區段包含**密碼識別碼**，外部應用程式可以存取此密碼的 URI。</span><span class="sxs-lookup"><span data-stu-id="1121d-152">hello properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span></span> 

![URI 祕密](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a><span data-ttu-id="1121d-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1121d-154">Next Steps</span></span>
* [<span data-ttu-id="1121d-155">擷取儲存在金鑰保存庫中的 hello 密碼來部署 VM</span><span class="sxs-lookup"><span data-stu-id="1121d-155">Deploy a VM by retrieving hello password stored in a key vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="1121d-156">使用存放在金鑰保存庫中的憑證來部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1121d-156">Deploy a VM with certificate stored in a key vault</span></span>](azure-stack-kv-push-secret-into-vm.md)     


