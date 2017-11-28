---
title: "aaaHow tooretain 常數 Azure 雲端服務的虛擬 IP 位址 |Microsoft 文件"
description: "了解如何 tooensure hello 虛擬 IP 位址 (VIP) 的 Azure 雲端服務，並不會變更。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a><span data-ttu-id="5ed4f-103">保持 Azure 雲端服務的固定虛擬 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ed4f-103">Retain a constant virtual IP address for an Azure cloud service</span></span>
<span data-ttu-id="5ed4f-104">當您更新雲端服務裝載於 Azure 時，您可能需要 tooensure hello 虛擬 IP 位址 (VIP) hello 服務不會變更。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-104">When you update a cloud service that's hosted in Azure, you might need tooensure that hello virtual IP address (VIP) of hello service doesn't change.</span></span> <span data-ttu-id="5ed4f-105">許多網域管理服務使用 hello 網域名稱系統 (DNS) 註冊網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-105">Many domain management services use hello Domain Name System (DNS) for registering domain names.</span></span> <span data-ttu-id="5ed4f-106">DNS 只有 hello VIP 會維持為 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-106">DNS works only if hello VIP remains hello same.</span></span> <span data-ttu-id="5ed4f-107">您可以使用 hello**發行精靈**hello VIP 的雲端服務不會變更時的 Azure Tools tooensure 您更新它。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-107">You can use hello **Publish Wizard** in Azure Tools tooensure that hello VIP of your cloud service doesn’t change when you update it.</span></span> <span data-ttu-id="5ed4f-108">如需有關如何 toouse DNS 網域管理雲端服務，請參閱[設定 Azure 雲端服務的自訂網域名稱](cloud-services/cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-108">For more information about how toouse DNS domain management for cloud services, see [Configuring a custom domain name for an Azure cloud service](cloud-services/cloud-services-custom-domain-name.md).</span></span>

## <a name="publish-a-cloud-service-without-changing-its-vip"></a><span data-ttu-id="5ed4f-109">發佈雲端服務而不變更其 VIP</span><span class="sxs-lookup"><span data-stu-id="5ed4f-109">Publish a cloud service without changing its VIP</span></span>
<span data-ttu-id="5ed4f-110">當您第一次將它部署在特定的環境中，例如 hello 實際執行環境的 tooAzure 配置 hello VIP 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-110">hello VIP of a cloud service is allocated when you first deploy it tooAzure in a particular environment, such as hello production environment.</span></span> <span data-ttu-id="5ed4f-111">只有明確刪除 hello 部署或隱含地刪除 hello 部署的 hello 部署的 hello VIP 變更的更新程序。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-111">hello VIP changes only if you delete hello deployment explicitly or hello deployment is implicitly deleted by hello deployment update process.</span></span> <span data-ttu-id="5ed4f-112">tooretain hello VIP，您必須刪除您的部署，您必須先確定 Visual Studio 並不會自動刪除您的部署。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-112">tooretain hello VIP, you must not delete your deployment, and you must make sure that Visual Studio doesn’t delete your deployment automatically.</span></span> 

<span data-ttu-id="5ed4f-113">您可以指定部署設定中 hello**發行精靈**，可支援多種部署選項。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-113">You can specify deployment settings in hello **Publish Wizard**, which supports several deployment options.</span></span> <span data-ttu-id="5ed4f-114">您可以指定全新部署或更新部署，後者可以是累加或同時的。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-114">You can specify a fresh deployment or an update deployment, which can be incremental or simultaneous.</span></span> <span data-ttu-id="5ed4f-115">這兩種更新部署保留 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-115">Both kinds of update deployment retain hello VIP.</span></span> <span data-ttu-id="5ed4f-116">如需這些不同類型部署的定義，請參閱 [發佈 Azure 應用程式精靈](vs-azure-tools-publish-azure-application-wizard.md)。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-116">For definitions of these different types of deployment, see [Publish Azure Application Wizard](vs-azure-tools-publish-azure-application-wizard.md).</span></span> <span data-ttu-id="5ed4f-117">此外，您可以控制是否要在發生錯誤時，刪除 hello 先前部署的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-117">In addition, you can control whether hello previous deployment of a cloud service is deleted if an error occurs.</span></span> <span data-ttu-id="5ed4f-118">如果您未正確設定該選項，hello VIP 可能會意外變更。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-118">If you don't set that option correctly, hello VIP might change unexpectedly.</span></span>

## <a name="update-a-cloud-service-without-changing-its-vip"></a><span data-ttu-id="5ed4f-119">更新雲端服務而不變更其 VIP</span><span class="sxs-lookup"><span data-stu-id="5ed4f-119">Update a cloud service without changing its VIP</span></span>
1. <span data-ttu-id="5ed4f-120">在 Visual Studio 中建立或開啟 Azure 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-120">Create or open an Azure cloud service project in Visual Studio.</span></span> 

2. <span data-ttu-id="5ed4f-121">在**方案總管 中**，以滑鼠右鍵按一下 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-121">In **Solution Explorer**, right-click hello project.</span></span> <span data-ttu-id="5ed4f-122">Hello 捷徑功能表上，選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-122">On hello shortcut menu, select **Publish**.</span></span>

    ![Publish menu](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. <span data-ttu-id="5ed4f-124">在 hello**發行 Azure 應用程式**對話方塊中，選取 hello Azure 訂用帳戶 toowhich 想 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-124">In hello **Publish Azure Application** dialog box, select hello Azure subscription toowhich you want toodeploy.</span></span> <span data-ttu-id="5ed4f-125">視需要登入，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-125">Sign in if necessary, and select **Next**.</span></span>

    ![發佈 Azure 應用程式登入頁面](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. <span data-ttu-id="5ed4f-127">在 hello**一般設定**索引標籤上，確認您要部署，hello hello 雲端服務 toowhich hello 名稱**環境**，hello**組建組態**，和 hello**服務組態**都正確。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-127">On hello **Common Settings** tab, verify that hello name of hello cloud service toowhich you’re deploying, hello **Environment**, hello **Build configuration**, and hello **Service configuration** are all correct.</span></span>

    ![發佈 Azure 應用程式一般設定索引標籤](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. <span data-ttu-id="5ed4f-129">在 hello**進階設定**索引標籤上，確認該 hello**部署標籤**和 hello**儲存體帳戶**正確無誤。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-129">On hello **Advanced Settings** tab, verify that hello **Deployment label** and hello **Storage account** are correct.</span></span> <span data-ttu-id="5ed4f-130">請確認該 hello**失敗時刪除部署**核取方塊已清除，並確認該 hello**部署更新**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-130">Verify that hello **Delete deployment on failure** check box is cleared, and verify that hello **Deployment update** check box is selected.</span></span> <span data-ttu-id="5ed4f-131">透過清除 hello**失敗時刪除部署**您核取方塊，確保 VIP 部署期間發生錯誤時不會遺失。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-131">By clearing hello **Delete deployment on failure** check box, you ensure that your VIP isn't lost if an error occurs during deployment.</span></span> <span data-ttu-id="5ed4f-132">藉由選取 hello**部署更新**核取方塊，確定您的部署不會遭到刪除，並重新發行應用程式時，無法遺失 VIP。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-132">By selecting hello **Deployment update** check box, you ensure that your deployment isn't deleted and your VIP isn't lost when you republish your application.</span></span> 

    ![發佈 Azure 應用程式進階設定索引標籤](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. <span data-ttu-id="5ed4f-134">指定要如何更新 hello 角色 toobe toofurther 中，選取**設定**下一步太**部署更新**。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-134">toofurther specify how you want hello roles toobe updated, select **Settings** next too**Deployment update**.</span></span> <span data-ttu-id="5ed4f-135">選取 [累加式更新] 或 [同時更新]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-135">Select either **Incremental update** or **Simultaneous update**, and select **OK**.</span></span> <span data-ttu-id="5ed4f-136">選擇**累加式更新**tooupdate 應用程式的每個執行個體，因此，hello 應用程式仍可使用。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-136">Choose **Incremental update** tooupdate each instance of your application, one after another, so that hello application is always available.</span></span> <span data-ttu-id="5ed4f-137">選擇**同時更新**tooupdate hello 在應用程式的所有執行個體相同的時間。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-137">Choose **Simultaneous update** tooupdate all instances of your application at hello same time.</span></span> <span data-ttu-id="5ed4f-138">同時更新較為快速，但您的服務可能無法使用 hello 更新程序期間。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-138">Simultaneous updating is faster, but your service might not be available during hello update process.</span></span> <span data-ttu-id="5ed4f-139">完成後，選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-139">When you are finished, select **Next**.</span></span>

    ![發佈 Azure 應用程式部署設定頁面](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. <span data-ttu-id="5ed4f-141">在 [hello**發行 Azure 應用程式**對話方塊中，選取**下一步]**直到 hello**摘要**頁面隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-141">In hello **Publish Azure Application** dialog box, select **Next** until hello **Summary** page is displayed.</span></span> <span data-ttu-id="5ed4f-142">確認您的設定，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="5ed4f-142">Verify your settings, and then select **Publish**.</span></span>
   
    ![發佈 Azure 應用程式摘要頁面](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a><span data-ttu-id="5ed4f-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ed4f-144">Next steps</span></span>
- [<span data-ttu-id="5ed4f-145">使用 hello Visual Studio 發行 Azure 應用程式精靈</span><span class="sxs-lookup"><span data-stu-id="5ed4f-145">Using hello Visual Studio Publish Azure Application Wizard</span></span>](vs-azure-tools-publish-azure-application-wizard.md)

