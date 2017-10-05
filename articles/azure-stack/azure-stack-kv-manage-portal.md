---
title: "使用 PowerShell 管理 Azure Stack 中的金鑰保存庫 | Microsoft Docs"
description: "了解如何使用 PowerShell 管理 Azure Stack 中的金鑰保存庫。"
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
ms.openlocfilehash: 6e70fd8a053a97a4bc4a66ea44d7e92cdec93afb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-key-vault-in-azure-stack-using-the-portal"></a><span data-ttu-id="f3749-103">使用入口網站管理 Azure Stack 中的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f3749-103">Manage Key Vault in Azure Stack using the portal</span></span>

<span data-ttu-id="f3749-104">您可以使用 Azure Stack 入口網站管理 Azure Stack 中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f3749-104">You can manage Key Vault in Azure Stack by using the Azure Stack portal.</span></span> <span data-ttu-id="f3749-105">此文章可協助您開始建立和管理 Azure Stack 中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f3749-105">This article helps you get started to create and manage Key Vault in Azure Stack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f3749-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f3749-106">Prerequisites</span></span>  

* <span data-ttu-id="f3749-107">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="f3749-107">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="f3749-108">使用者必須[訂閱產品](azure-stack-subscribe-plan-provision-vm.md)，且其包含「金鑰保存庫」服務。</span><span class="sxs-lookup"><span data-stu-id="f3749-108">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
 
## <a name="create-a-key-vault"></a><span data-ttu-id="f3749-109">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f3749-109">Create a key vault</span></span> 

1. <span data-ttu-id="f3749-110">登入使用者入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="f3749-110">Sign in to the user portal(https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="f3749-111">從儀表板按一下 [新增] > [安全性 + 身分識別] > [金鑰保存庫]。</span><span class="sxs-lookup"><span data-stu-id="f3749-111">From the dashboard, click **New > Security + Identity > Key Vault**.</span></span>  

    ![KV 畫面](media/azure-stack-kv-manage-portal/image1.png)  

3. <span data-ttu-id="f3749-113">在 [建立金鑰保存庫] 刀鋒視窗上，為您的保存庫指派 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="f3749-113">On the **Create Key Vault** blade, assign a **Name** for your vault.</span></span> <span data-ttu-id="f3749-114">保存庫名稱只能包含英數字元、特殊字元連字號 (-)，而且不應該以數字開頭。</span><span class="sxs-lookup"><span data-stu-id="f3749-114">Vault name can contain only alphanumeric characters, the special character hyphen (-), and it shouldn’t start with a number.</span></span>  

4. <span data-ttu-id="f3749-115">從可用的訂用帳戶清單中選擇 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f3749-115">Choose a **Subscription** from the list of available subscriptions.</span></span> <span data-ttu-id="f3749-116">所有提供「金鑰保存庫」服務的訂用帳戶皆會顯示在下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="f3749-116">All subscriptions that offer the Key Vault service are displayed in the drop-down.</span></span>  

5. <span data-ttu-id="f3749-117">選取現有的 [資源群組] 或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="f3749-117">Select an existing **Resource Group** or create a new one.</span></span>  

6. <span data-ttu-id="f3749-118">選取 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="f3749-118">Select the **Pricing tier**.</span></span>  
    >[!NOTE]
    > <span data-ttu-id="f3749-119">Azure Stack 開發套件中的金鑰保存庫僅支援**標準**SKU。</span><span class="sxs-lookup"><span data-stu-id="f3749-119">Key vaults in Azure Stack Development Kit support **Standard** SKU only.</span></span>

7. <span data-ttu-id="f3749-120">選取現有的 [存取原則] 或建立新原則。</span><span class="sxs-lookup"><span data-stu-id="f3749-120">Choose an existing **Access policies** or create a new one.</span></span> <span data-ttu-id="f3749-121">存取原則可讓您授與使用者、應用程式或安全性群組權限，來執行此保存庫的作業。</span><span class="sxs-lookup"><span data-stu-id="f3749-121">Access policy allows you to grant permissions for a user, application, or a security group to perform operations with this vault.</span></span>  

8. <span data-ttu-id="f3749-122">(選用) 選擇 [進階存取原則] 來啟用功能，像是存取虛擬機器進行部署、存取 Resource Manager 進行範本部署，以及存取 Azure 磁碟加密進行磁碟區加密。</span><span class="sxs-lookup"><span data-stu-id="f3749-122">Optionally, choose an **Advanced access policy** to enable the features like access to Virtual Machines for deployment, access to Resource Manager for template deployment and access to Azure Disk Encryption for volume encryption.</span></span> 
  
9.  <span data-ttu-id="f3749-123">完成設定後，請按一下 [確定]，然後 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f3749-123">After configuring the settings, click **OK** and then **Create**.</span></span> <span data-ttu-id="f3749-124">如此一來，就將會啟動金鑰保存庫部署。</span><span class="sxs-lookup"><span data-stu-id="f3749-124">This starts the key vault deployment.</span></span> 

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="f3749-125">管理金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="f3749-125">Manage keys and secrets</span></span>

<span data-ttu-id="f3749-126">在您建立保存庫之後，請使用下列逐步執行來建立並管理保存庫內的金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="f3749-126">After you create a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

## <a name="create-a-key"></a><span data-ttu-id="f3749-127">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="f3749-127">Create a key</span></span>

1. <span data-ttu-id="f3749-128">請登入使用者入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="f3749-128">Sign in to the user portal (https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="f3749-129">從儀表板中，按一下 [所有資源] > 選取您稍早建立的金鑰保存庫 > 按一下 [金鑰] 磚。</span><span class="sxs-lookup"><span data-stu-id="f3749-129">From the dashboard, click **All resources** > select the key vault that you created earlier> click the **Keys** tile.</span></span>  

3. <span data-ttu-id="f3749-130">從 [金鑰] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f3749-130">From the **Keys** blade, click **Add**.</span></span> 

4. <span data-ttu-id="f3749-131">在 [建立金鑰] 刀鋒視窗中，從 [選項] 清單選擇您要用來建立金鑰的方法。</span><span class="sxs-lookup"><span data-stu-id="f3749-131">On the **Create a key** blade, form the list of **Options**, choose the method that you want to use to create a key.</span></span> <span data-ttu-id="f3749-132">您可以 [產生] 新的金鑰、[上傳] 現有金鑰，或是 [還原備份] 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f3749-132">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span></span>  

5. <span data-ttu-id="f3749-133">在 [名稱] 中輸入金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3749-133">Enter a **Name** for your key.</span></span> <span data-ttu-id="f3749-134">金鑰名稱只能包含英數字元和特殊字元連字號 (-)。</span><span class="sxs-lookup"><span data-stu-id="f3749-134">The key name can contain only alphanumeric characters and the special character hyphen (-).</span></span>  

6. <span data-ttu-id="f3749-135">(選用) 為金鑰設定 [設定啟用日期] 和 [設定到期日期]。</span><span class="sxs-lookup"><span data-stu-id="f3749-135">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span></span>  

7. <span data-ttu-id="f3749-136">按一下 [建立] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="f3749-136">Click **Create** to start the deployment.</span></span>  

<span data-ttu-id="f3749-137">成功建立金鑰之後，您可以從 [金鑰] 刀鋒視窗選取該金鑰，並檢視或修改其屬性。</span><span class="sxs-lookup"><span data-stu-id="f3749-137">After the key is successfully created, you can select it from the **Keys** blade and view or modify its properties.</span></span> <span data-ttu-id="f3749-138">屬性區段包含**金鑰識別碼**，其為外部應用程式可以存取此金鑰的 URI。</span><span class="sxs-lookup"><span data-stu-id="f3749-138">The properties section contains the **Key Identifier**, a URI by which external applications can access this key.</span></span> <span data-ttu-id="f3749-139">若要限制此金鑰的作業，請設定 [允許的作業] 下的設定。</span><span class="sxs-lookup"><span data-stu-id="f3749-139">To limit operations on this key, configure settings under **Permitted operations**.</span></span>

![URI 金鑰](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a><span data-ttu-id="f3749-141">建立祕密</span><span class="sxs-lookup"><span data-stu-id="f3749-141">Create a secret</span></span> 

1. <span data-ttu-id="f3749-142">請登入使用者入口網站 (https://portal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="f3749-142">Sign in to the user portal (https://portal.local.azurestack.external).</span></span>  
2. <span data-ttu-id="f3749-143">從儀表板中，按一下 [所有資源] > 選取您稍早建立的金鑰保存庫 > 按一下 [祕密] 磚。</span><span class="sxs-lookup"><span data-stu-id="f3749-143">From the dashboard, click **All resources** > select the key vault that you created earlier> click the **Secrets** tile.</span></span>  

3. <span data-ttu-id="f3749-144">從 [祕密] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f3749-144">From the **Secrets** blade, click **Add**.</span></span>  

4. <span data-ttu-id="f3749-145">在 [建立祕密] 刀鋒視窗中，從[上傳選項] 的清單選擇您想要建立祕密的選項。</span><span class="sxs-lookup"><span data-stu-id="f3749-145">On the **Create a secret** blade, from the list of **Upload options**, choose an option by which you want to create a secret.</span></span> <span data-ttu-id="f3749-146">您可以透過輸入值來**手動**建立祕密，或是透過本機上傳**憑證**。</span><span class="sxs-lookup"><span data-stu-id="f3749-146">You can create a secret **Manually** by entering a value for the secret, or by uploading a **Certificate** from your local machine.</span></span>  

5. <span data-ttu-id="f3749-147">輸入祕密的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="f3749-147">Enter a **Name** for the secret.</span></span> <span data-ttu-id="f3749-148">祕密名稱只能包含英數字元和特殊字元連字號 (-)。</span><span class="sxs-lookup"><span data-stu-id="f3749-148">The secret name can contain only alphanumeric characters and the special character hyphen (-).</span></span>  

6. <span data-ttu-id="f3749-149">(選用) 指定 [內容型別]、為 [設定啟用日期] 設定值，以及為祕密 [設定到期日期]設定值。</span><span class="sxs-lookup"><span data-stu-id="f3749-149">Optionally, specify the **Content type**, and configure values for **Set activation date** and **Set expiration date** values for the secret.</span></span>  

7. <span data-ttu-id="f3749-150">按一下 [建立] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="f3749-150">Click Create to start the deployment.</span></span>  

<span data-ttu-id="f3749-151">成功建立祕密之後，您可以從 [祕密] 刀鋒視窗選取該祕密，並檢視或修改其屬性。</span><span class="sxs-lookup"><span data-stu-id="f3749-151">After the secret is successfully created, you can select it from the **Secrets** blade and view or modify its properties.</span></span> <span data-ttu-id="f3749-152">屬性區段包含**祕密識別碼**，其為外部應用程式可以存取此祕密的 URI。</span><span class="sxs-lookup"><span data-stu-id="f3749-152">The properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span></span> 

![URI 祕密](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a><span data-ttu-id="f3749-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3749-154">Next Steps</span></span>
* [<span data-ttu-id="f3749-155">擷取存放在金鑰保存庫中的密碼來部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f3749-155">Deploy a VM by retrieving the password stored in a key vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="f3749-156">使用存放在金鑰保存庫中的憑證來部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f3749-156">Deploy a VM with certificate stored in a key vault</span></span>](azure-stack-kv-push-secret-into-vm.md)     


