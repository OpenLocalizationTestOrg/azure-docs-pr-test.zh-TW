---
title: "建立外部 Azure App Service 環境"
description: "說明如何在建立應用程式或獨立時建立 App Service 環境"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 2dfe531facbe84aac65c5f787851c015de719fee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-external-app-service-environment"></a><span data-ttu-id="12bbf-103">建立外部 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="12bbf-103">Create an External App Service environment</span></span> #

<span data-ttu-id="12bbf-104">Azure App Service Environment (ASE) 是將 Azure App Service 部署到客戶 Azure 虛擬網路 (VNet) 中子網路的一種部署。</span><span class="sxs-lookup"><span data-stu-id="12bbf-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="12bbf-105">部署 App Service Environment (ASE) 有二種方法：</span><span class="sxs-lookup"><span data-stu-id="12bbf-105">There are two ways to deploy an App Service environment (ASE):</span></span>

- <span data-ttu-id="12bbf-106">使用外部 IP 位址上的 VIP，通常稱為「外部 ASE」。</span><span class="sxs-lookup"><span data-stu-id="12bbf-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="12bbf-107">使用內部 IP 位址上的 VIP，通常稱為 ILB ASE，因為內部端點是內部負載平衡器 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="12bbf-107">With the VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span>

<span data-ttu-id="12bbf-108">本文說明如何建立外部 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-108">This article shows you how to create an External ASE.</span></span> <span data-ttu-id="12bbf-109">如需 ASE 的概述，請參閱 [App Service Environment 簡介][Intro]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-109">For an overview of the ASE, see [An introduction to the App Service Environment][Intro].</span></span> <span data-ttu-id="12bbf-110">如需有關如何建立 ILB ASE 的資訊，請參閱[建立並使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-110">For information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="before-you-create-your-ase"></a><span data-ttu-id="12bbf-111">建立 ASE 之前</span><span class="sxs-lookup"><span data-stu-id="12bbf-111">Before you create your ASE</span></span> ##

<span data-ttu-id="12bbf-112">建立 ASE 之後，您就無法變更下列項目：</span><span class="sxs-lookup"><span data-stu-id="12bbf-112">After you create your ASE, you can't change the following:</span></span>

- <span data-ttu-id="12bbf-113">位置</span><span class="sxs-lookup"><span data-stu-id="12bbf-113">Location</span></span>
- <span data-ttu-id="12bbf-114">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="12bbf-114">Subscription</span></span>
- <span data-ttu-id="12bbf-115">資源群組</span><span class="sxs-lookup"><span data-stu-id="12bbf-115">Resource group</span></span>
- <span data-ttu-id="12bbf-116">使用的 VNet</span><span class="sxs-lookup"><span data-stu-id="12bbf-116">VNet used</span></span>
- <span data-ttu-id="12bbf-117">使用的子網路</span><span class="sxs-lookup"><span data-stu-id="12bbf-117">Subnet used</span></span>
- <span data-ttu-id="12bbf-118">子網路大小</span><span class="sxs-lookup"><span data-stu-id="12bbf-118">Subnet size</span></span>

> [!NOTE]
> <span data-ttu-id="12bbf-119">選取 VNet 並指定子網路時，請確定它足夠大以容納未來的成長。</span><span class="sxs-lookup"><span data-stu-id="12bbf-119">When you choose a VNet and specify a subnet, make sure that it's large enough to accommodate future growth.</span></span> <span data-ttu-id="12bbf-120">我們建議使用包含 128 個位址的 `/25` 大小。</span><span class="sxs-lookup"><span data-stu-id="12bbf-120">We recommend a size of `/25` with 128 addresses.</span></span>
>

## <a name="three-ways-to-create-an-ase"></a><span data-ttu-id="12bbf-121">建立 ASE 有三種方式</span><span class="sxs-lookup"><span data-stu-id="12bbf-121">Three ways to create an ASE</span></span> ##

<span data-ttu-id="12bbf-122">建立 ASE 有三種方式：</span><span class="sxs-lookup"><span data-stu-id="12bbf-122">There are three ways to create an ASE:</span></span>

- <span data-ttu-id="12bbf-123">**建立 App Service 方案時**。</span><span class="sxs-lookup"><span data-stu-id="12bbf-123">**While creating an App Service plan**.</span></span> <span data-ttu-id="12bbf-124">這個方法會在一個步驟中建立 ASE 和應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="12bbf-124">This method creates the ASE and the App Service plan in one step.</span></span>
- <span data-ttu-id="12bbf-125">**作為獨立動作**。</span><span class="sxs-lookup"><span data-stu-id="12bbf-125">**As a standalone action**.</span></span> <span data-ttu-id="12bbf-126">這個方法會建立獨立 ASE，也就是任何項目的 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-126">This method creates a standalone ASE, which is an ASE with nothing in it.</span></span> <span data-ttu-id="12bbf-127">這個方法是建立 ASE 的更進階流程。</span><span class="sxs-lookup"><span data-stu-id="12bbf-127">This method is a more advanced process to create an ASE.</span></span> <span data-ttu-id="12bbf-128">您可以使用它來建立 ASE 並搭配 ILB。</span><span class="sxs-lookup"><span data-stu-id="12bbf-128">You use it to create an ASE with an ILB.</span></span>
- <span data-ttu-id="12bbf-129">**從 Azure Resource Manager 範本**。</span><span class="sxs-lookup"><span data-stu-id="12bbf-129">**From an Azure Resource Manager template**.</span></span> <span data-ttu-id="12bbf-130">這個方法適用於進階使用者。</span><span class="sxs-lookup"><span data-stu-id="12bbf-130">This method is for advanced users.</span></span> <span data-ttu-id="12bbf-131">如需詳細資訊，請參閱[從範本建立 ASE][MakeASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-131">For more information, see [Create an ASE from a template][MakeASEfromTemplate].</span></span>

<span data-ttu-id="12bbf-132">外部 ASE 具有公用 VIP，這表示 ASE 中所有對應用程式的 HTTP/HTTPS 流量都會叫用可存取網際網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="12bbf-132">An External ASE has a public VIP, which means that all HTTP/HTTPS traffic to the apps in the ASE hits an internet-accessible IP address.</span></span> <span data-ttu-id="12bbf-133">搭配 ILB 的 ASE 中有 ASE 所使用之子網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="12bbf-133">An ASE with an ILB has an IP address from the subnet used by the ASE.</span></span> <span data-ttu-id="12bbf-134">裝載於 ILB ASE 中的應用程式並非直接向網際網路公開。</span><span class="sxs-lookup"><span data-stu-id="12bbf-134">The apps hosted in an ILB ASE aren't exposed directly to the internet.</span></span>

## <a name="create-an-ase-and-an-app-service-plan-together"></a><span data-ttu-id="12bbf-135">一起建立 ASE 和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="12bbf-135">Create an ASE and an App Service plan together</span></span> ##

<span data-ttu-id="12bbf-136">App Service 方案是應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="12bbf-136">The App Service plan is a container of apps.</span></span> <span data-ttu-id="12bbf-137">當您在 App Service 中建立應用程式時，要選擇或建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="12bbf-137">When you create an app in App Service, you choose or create an App Service plan.</span></span> <span data-ttu-id="12bbf-138">容器模型環境會保存 App Service 方案，和保存應用程式的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="12bbf-138">The container model environments hold App Service plans, and App Service plans hold apps.</span></span>

<span data-ttu-id="12bbf-139">若要在建立 App Service 方案時建立 ASE：</span><span class="sxs-lookup"><span data-stu-id="12bbf-139">To create an ASE while you create an App Service plan:</span></span>

1. <span data-ttu-id="12bbf-140">在 [Azure 入口網站](https://portal.azure.com/)中，選取 [新增] > [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-140">In the [Azure portal](https://portal.azure.com/), select **New** > **Web + Mobile** > **Web App**.</span></span>

    ![建立 Web 應用程式][1]

2. <span data-ttu-id="12bbf-142">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="12bbf-142">Select your subscription.</span></span> <span data-ttu-id="12bbf-143">會在相同的訂用帳戶中建立應用程式和 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-143">The app and the ASE are created in the same subscriptions.</span></span>

3. <span data-ttu-id="12bbf-144">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="12bbf-144">Select or create a resource group.</span></span> <span data-ttu-id="12bbf-145">您可以使用資源群組來管理相關的一組 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="12bbf-145">With resource groups, you can manage related Azure resources as a unit.</span></span> <span data-ttu-id="12bbf-146">當您為應用程式建立角色型存取控制規則時，資源群組也十分實用。</span><span class="sxs-lookup"><span data-stu-id="12bbf-146">Resource groups also are useful when you establish Role-Based Access Control rules for your apps.</span></span> <span data-ttu-id="12bbf-147">如需詳細資訊，請參閱 [Azure Resource Manager 概觀][ARMOverview]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-147">For more information, see the [Azure Resource Manager overview][ARMOverview].</span></span>

4. <span data-ttu-id="12bbf-148">選取 App Service 方案，然後選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-148">Select the App Service plan, and then select **Create New**.</span></span>

    ![新增 App Service 方案][2]

5. <span data-ttu-id="12bbf-150">在 [位置] 下拉式清單中，選取您需要建立 ASE 的區域。</span><span class="sxs-lookup"><span data-stu-id="12bbf-150">In the **Location** drop-down list, select the region where you want to create the ASE.</span></span> <span data-ttu-id="12bbf-151">如果您選取現有的 ASE，就不會建立新的 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-151">If you select an existing ASE, a new ASE isn't created.</span></span> <span data-ttu-id="12bbf-152">會在您選取的 ASE 中建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="12bbf-152">The App Service plan is created in the ASE that you selected.</span></span> 

6. <span data-ttu-id="12bbf-153">選取**定價層**，然後選擇其中一個**隔離的**定價 SKU。</span><span class="sxs-lookup"><span data-stu-id="12bbf-153">Select **Pricing tier**, and choose one of the **Isolated** pricing SKUs.</span></span> <span data-ttu-id="12bbf-154">如果您選擇**隔離** SKU 卡以及非 ASE 的位置，就會在該位置中建立新的 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-154">If you choose an **Isolated** SKU card and a location that's not an ASE, a new ASE is created in that location.</span></span> <span data-ttu-id="12bbf-155">若要啟動建立 ASE 的流程，請選取 [選取]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-155">To start the process to create an ASE, select **Select**.</span></span> <span data-ttu-id="12bbf-156">**隔離** SKU 僅供與 ASE 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="12bbf-156">The **Isolated** SKU is available only in conjunction with an ASE.</span></span> <span data-ttu-id="12bbf-157">您也無法在 ASE 中使用**隔離**以外的其他任何定價 SKU。</span><span class="sxs-lookup"><span data-stu-id="12bbf-157">You also can't use any other pricing SKU in an ASE other than **Isolated**.</span></span>

    ![定價層選取項目][3]

7. <span data-ttu-id="12bbf-159">輸入 ASE 的名稱。</span><span class="sxs-lookup"><span data-stu-id="12bbf-159">Enter the name for your ASE.</span></span> <span data-ttu-id="12bbf-160">此名稱是用於應用程式的可定址名稱。</span><span class="sxs-lookup"><span data-stu-id="12bbf-160">This name is used in the addressable name for your apps.</span></span> <span data-ttu-id="12bbf-161">如果 ASE 的名稱是 _appsvcenvdemo_，則網域名稱會是 .appsvcenvdemo.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="12bbf-161">If the name of the ASE is _appsvcenvdemo_, the domain name is *.appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="12bbf-162">如果您建立名為 mytestapp 的應用程式，則可定址於 mytestapp.appsvcenvdemo.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="12bbf-162">If you create an app named *mytestapp*, it's addressable at mytestapp.appsvcenvdemo.p.azurewebsites.net.</span></span> <span data-ttu-id="12bbf-163">您無法在名稱中使用空白字元。</span><span class="sxs-lookup"><span data-stu-id="12bbf-163">You can't use white space in the name.</span></span> <span data-ttu-id="12bbf-164">如果您使用大寫字元，則網域名稱會是該名稱的全小寫版本。</span><span class="sxs-lookup"><span data-stu-id="12bbf-164">If you use uppercase characters, the domain name is the total lowercase version of that name.</span></span>

    ![新增 App Service 方案名稱][4]

8. <span data-ttu-id="12bbf-166">指定 Azure 虛擬網路詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12bbf-166">Specify your Azure virtual networking details.</span></span> <span data-ttu-id="12bbf-167">選取 [新建] 或 [選取現有]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-167">Select either **Create New** or **Select Existing**.</span></span> <span data-ttu-id="12bbf-168">僅在選取的區域擁有 VNet 時，才可以使用選取現有 VNet 的選項。</span><span class="sxs-lookup"><span data-stu-id="12bbf-168">The option to select an existing VNet is available only if you have a VNet in the selected region.</span></span> <span data-ttu-id="12bbf-169">如果您選取 [新建]，請輸入 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="12bbf-169">If you select **Create New**, enter a name for the VNet.</span></span> <span data-ttu-id="12bbf-170">會建立具有該名稱的 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="12bbf-170">A new Resource Manager VNet with that name is created.</span></span> <span data-ttu-id="12bbf-171">它會使用選取區域中的位址空間 `192.168.250.0/23`。</span><span class="sxs-lookup"><span data-stu-id="12bbf-171">It uses the address space `192.168.250.0/23` in the selected region.</span></span> <span data-ttu-id="12bbf-172">如果您選取 [選取現有]，您需要：</span><span class="sxs-lookup"><span data-stu-id="12bbf-172">If you select **Select Existing**, you need to:</span></span>

    <span data-ttu-id="12bbf-173">a.</span><span class="sxs-lookup"><span data-stu-id="12bbf-173">a.</span></span> <span data-ttu-id="12bbf-174">如果您有多個位址區塊，請選取 VNet 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="12bbf-174">Select the VNet address block, if you have more than one.</span></span>

    <span data-ttu-id="12bbf-175">b.</span><span class="sxs-lookup"><span data-stu-id="12bbf-175">b.</span></span> <span data-ttu-id="12bbf-176">輸入新的子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="12bbf-176">Enter a new subnet name.</span></span>

    <span data-ttu-id="12bbf-177">c.</span><span class="sxs-lookup"><span data-stu-id="12bbf-177">c.</span></span> <span data-ttu-id="12bbf-178">選取子網路的大小。</span><span class="sxs-lookup"><span data-stu-id="12bbf-178">Select the size of the subnet.</span></span> <span data-ttu-id="12bbf-179">請記得選取大小足以容納未來成長的 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-179">*Remember to select a size large enough to accommodate future growth of your ASE.*</span></span> <span data-ttu-id="12bbf-180">建議是 `/25`，具有 128 個位址，而且可以處理最大大小的 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-180">We recommend `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="12bbf-181">例如，不建議 `/28`，因為只有 16 個位址可供使用。</span><span class="sxs-lookup"><span data-stu-id="12bbf-181">We don't recommend `/28`, for example, because only 16 addresses are available.</span></span> <span data-ttu-id="12bbf-182">基礎結構會使用至少五個位址。</span><span class="sxs-lookup"><span data-stu-id="12bbf-182">Infrastructure uses at least five addresses.</span></span> <span data-ttu-id="12bbf-183">在 `/28` 子網路中，您會擁有 11 個執行個體的最大縮放比例。</span><span class="sxs-lookup"><span data-stu-id="12bbf-183">In a `/28` subnet, you're left with a maximum scaling of 11 instances.</span></span>

    <span data-ttu-id="12bbf-184">d.</span><span class="sxs-lookup"><span data-stu-id="12bbf-184">d.</span></span> <span data-ttu-id="12bbf-185">選取子網路 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="12bbf-185">Select the subnet IP range.</span></span>

9. <span data-ttu-id="12bbf-186">選取 [建立] 以建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-186">Select **Create** to create the ASE.</span></span> <span data-ttu-id="12bbf-187">此流程也會建立 App Service 方案和應用程式。</span><span class="sxs-lookup"><span data-stu-id="12bbf-187">This process also creates the App Service plan and the app.</span></span> <span data-ttu-id="12bbf-188">ASE、App Service 方案和應用程式會在相同的訂用帳戶底下，同時在相同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="12bbf-188">The ASE, App Service plan, and app are all under the same subscription and also in the same resource group.</span></span> <span data-ttu-id="12bbf-189">如果您的 ASE 需要個別資源群組，或如果您需要 ILB ASE，請遵循步驟讓 ASE 自行建立。</span><span class="sxs-lookup"><span data-stu-id="12bbf-189">If your ASE needs a separate resource group or if you need an ILB ASE, follow the steps to create an ASE by itself.</span></span>

## <a name="create-an-ase-by-itself"></a><span data-ttu-id="12bbf-190">由 ASE 本身建立</span><span class="sxs-lookup"><span data-stu-id="12bbf-190">Create an ASE by itself</span></span> ##

<span data-ttu-id="12bbf-191">如果您建立 ASE 獨立，它就不會包含任何項目。</span><span class="sxs-lookup"><span data-stu-id="12bbf-191">If you create an ASE standalone, it has nothing in it.</span></span> <span data-ttu-id="12bbf-192">空白 ASE 仍會產生基礎結構的每月費用。</span><span class="sxs-lookup"><span data-stu-id="12bbf-192">An empty ASE still incurs a monthly charge for the infrastructure.</span></span> <span data-ttu-id="12bbf-193">請遵循下列步驟來建立具有 ILB 的 ASE，或是在它自己的資源群組中建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-193">Follow these steps to create an ASE with an ILB or to create an ASE in its own resource group.</span></span> <span data-ttu-id="12bbf-194">建立 ASE 之後，您可以使用一般流程在其中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="12bbf-194">After you create your ASE, you can create apps in it by using the normal process.</span></span> <span data-ttu-id="12bbf-195">選取您新的 ASE 作為位置。</span><span class="sxs-lookup"><span data-stu-id="12bbf-195">Select your new ASE as the location.</span></span>

1. <span data-ttu-id="12bbf-196">搜尋 Azure Marketplace 的**App Service 環境**，或選取 [新增] > [Web 行動] > [App Service 環境]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-196">Search the Azure Marketplace for **App Service Environment**, or select **New** > **Web Mobile** > **App Service Environment**.</span></span> 

2. <span data-ttu-id="12bbf-197">輸入您的 ASE 名稱。</span><span class="sxs-lookup"><span data-stu-id="12bbf-197">Enter the name of your ASE.</span></span> <span data-ttu-id="12bbf-198">這個名稱會用於 ASE 中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="12bbf-198">This name is used for the apps created in the ASE.</span></span> <span data-ttu-id="12bbf-199">如果名稱是 mynewdemoase，子網域名稱就是 .mynewdemoase.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="12bbf-199">If the name is *mynewdemoase*, the subdomain name is *.mynewdemoase.p.azurewebsites.net*.</span></span> <span data-ttu-id="12bbf-200">如果您建立名為 mytestapp 的應用程式，則可定址於 mytestapp.mynewdemoase.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="12bbf-200">If you create an app named *mytestapp*, it's addressable at mytestapp.mynewdemoase.p.azurewebsites.net.</span></span> <span data-ttu-id="12bbf-201">您無法在名稱中使用空白字元。</span><span class="sxs-lookup"><span data-stu-id="12bbf-201">You can't use white space in the name.</span></span> <span data-ttu-id="12bbf-202">如果您使用大寫字元，則網域名稱會是該名稱的全小寫版本。</span><span class="sxs-lookup"><span data-stu-id="12bbf-202">If you use uppercase characters, the domain name is the total lowercase version of the name.</span></span> <span data-ttu-id="12bbf-203">如果您是使用 ILB，ASE 名稱就不會用於您的子網域中，但是會在 ASE 建立期間明確指定。</span><span class="sxs-lookup"><span data-stu-id="12bbf-203">If you use an ILB, your ASE name isn't used in your subdomain but is instead explicitly stated during ASE creation.</span></span>

    ![ASE 命名][5]

3. <span data-ttu-id="12bbf-205">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="12bbf-205">Select your subscription.</span></span> <span data-ttu-id="12bbf-206">此訂用帳戶也是所有應用程式在 ASE 中所使用的。</span><span class="sxs-lookup"><span data-stu-id="12bbf-206">This subscription is also the one that all apps in the ASE use.</span></span> <span data-ttu-id="12bbf-207">您無法將 ASE 放在另一個訂用帳戶中的 VNet。</span><span class="sxs-lookup"><span data-stu-id="12bbf-207">You can't put your ASE in a VNet that's in another subscription.</span></span>

4. <span data-ttu-id="12bbf-208">選取或指定新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="12bbf-208">Select or specify a new resource group.</span></span> <span data-ttu-id="12bbf-209">用於 ASE 的資源群組必須是與用於您 VNet 的相同。</span><span class="sxs-lookup"><span data-stu-id="12bbf-209">The resource group used for your ASE must be the same one that's used for your VNet.</span></span> <span data-ttu-id="12bbf-210">如果您選取現有的 VNet，您 ASE 的資源群組選取項目將會更新，以反映 VNet 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="12bbf-210">If you select an existing VNet, the resource group selection for your ASE is updated to reflect that of your VNet.</span></span> <span data-ttu-id="12bbf-211">如果您是使用 Resource Manager 範本，可以使用不同於 VNet 資源群組的資源群組來建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-211">*You can create an ASE with a resource group that is different from the VNet resource group if you use a Resource Manager template.*</span></span> <span data-ttu-id="12bbf-212">若要從範本建立 ASE，請參閱[從範本建立 App Service 環境][MakeASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-212">To create an ASE from a template, see [Create an App Service environment from a template][MakeASEfromTemplate].</span></span>

    ![資源群組選取項目][6]

5. <span data-ttu-id="12bbf-214">選取您的 VNet 和位置。</span><span class="sxs-lookup"><span data-stu-id="12bbf-214">Select your VNet and location.</span></span> <span data-ttu-id="12bbf-215">您可以建立新的 VNet 或選取現有的 VNet：</span><span class="sxs-lookup"><span data-stu-id="12bbf-215">You can create a new VNet or select an existing VNet:</span></span> 

    * <span data-ttu-id="12bbf-216">如果您選取新的 VNet，就可以指定名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="12bbf-216">If you select a new VNet, you can specify a name and location.</span></span> <span data-ttu-id="12bbf-217">新的 VNet 會有位址範圍 192.168.250.0/23，和名為 default 的子網路。</span><span class="sxs-lookup"><span data-stu-id="12bbf-217">The new VNet has the address range 192.168.250.0/23 and a subnet named default.</span></span> <span data-ttu-id="12bbf-218">子網路定義為 192.168.250.0/24。</span><span class="sxs-lookup"><span data-stu-id="12bbf-218">The subnet is defined as 192.168.250.0/24.</span></span> <span data-ttu-id="12bbf-219">您只能選取 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="12bbf-219">You can only select a Resource Manager VNet.</span></span> <span data-ttu-id="12bbf-220">[VIP 類型] 選取項目會決定您的 ASE 是否可以從網際網路 (外部) 直接存取，或者它是使用 ILB。</span><span class="sxs-lookup"><span data-stu-id="12bbf-220">The **VIP Type** selection determines if your ASE can be directly accessed from the internet (External) or if it uses an ILB.</span></span> <span data-ttu-id="12bbf-221">若要深入了解這些選項，請參閱[在 App Service 環境中建立及使用內部負載平衡器][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-221">To learn more about these options, see [Create and use an internal load balancer with an App Service environment][MakeILBASE].</span></span> 

      * <span data-ttu-id="12bbf-222">如果您針對 VIP 類型選取 [外部]，則可以選取系統針對以 IP 為主的 SSL 用途會建立幾個外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="12bbf-222">If you select **External** for the **VIP Type**, you can select how many external IP addresses the system is created with for IP-based SSL purposes.</span></span> 
    
      * <span data-ttu-id="12bbf-223">如果您針對 VIP 類型選取 [外部]，就必須指定您 ASE 使用的網域。</span><span class="sxs-lookup"><span data-stu-id="12bbf-223">If you select **Internal** for the **VIP Type**, you must specify the domain that your ASE uses.</span></span> <span data-ttu-id="12bbf-224">您可以將 ASE 部署到使用公用或私人位址範圍的 VNet。</span><span class="sxs-lookup"><span data-stu-id="12bbf-224">You can deploy an ASE into a VNet that uses public or private address ranges.</span></span> <span data-ttu-id="12bbf-225">若要搭配使用 VNet 與公用位址範圍，您必須事先建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="12bbf-225">To use a VNet with a public address range, you need to create the VNet ahead of time.</span></span> 
    
    * <span data-ttu-id="12bbf-226">如果您選取現有的 VNet，ASE 建立時就會建立新的子網路。</span><span class="sxs-lookup"><span data-stu-id="12bbf-226">If you select an existing VNet, a new subnet is created when the ASE is created.</span></span> <span data-ttu-id="12bbf-227">*您無法在入口網站中使用預先建立的子網路。如果您是使用 Resource Manager 範本，則可以使用現有的子網路建立 ASE。*</span><span class="sxs-lookup"><span data-stu-id="12bbf-227">*You can't use a pre-created subnet in the portal. You can create an ASE with an existing subnet if you use a Resource Manager template.*</span></span> <span data-ttu-id="12bbf-228">若要從範本建立 ASE，請參閱[從範本建立 App Service 環境][MakeASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-228">To create an ASE from a template, see [Create an App Service Environment from a template][MakeASEfromTemplate].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="12bbf-229">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="12bbf-229">App Service Environment v1</span></span> ##

<span data-ttu-id="12bbf-230">您仍然可以建立 App Service Environment (ASEv1) 的第一個版本執行個體。</span><span class="sxs-lookup"><span data-stu-id="12bbf-230">You can still create instances of the first version of App Service Environment (ASEv1).</span></span> <span data-ttu-id="12bbf-231">若要啟動該流程，請在 Marketplace 搜尋 **App Service Environment v1**。</span><span class="sxs-lookup"><span data-stu-id="12bbf-231">To start that process, search the Marketplace for **App Service Environment v1**.</span></span> <span data-ttu-id="12bbf-232">您要使用與建立獨立 ASE 的相同方式來建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="12bbf-232">You create the ASE in the same way that you create the standalone ASE.</span></span> <span data-ttu-id="12bbf-233">完成後，您的 ASEv1 會有兩個「前端」和兩個「背景工作角色」。</span><span class="sxs-lookup"><span data-stu-id="12bbf-233">When it's finished, your ASEv1 has two front ends and two workers.</span></span> <span data-ttu-id="12bbf-234">使用 ASEv1 時，您必須管理「前端」和「背景工作角色」。</span><span class="sxs-lookup"><span data-stu-id="12bbf-234">With ASEv1, you must manage the front ends and workers.</span></span> <span data-ttu-id="12bbf-235">當您建立 App Service 方案時，它們不會自動新增。</span><span class="sxs-lookup"><span data-stu-id="12bbf-235">They're not automatically added when you create your App Service plans.</span></span> <span data-ttu-id="12bbf-236">前端可作為 HTTP/HTTPS 端點，將流量傳送到背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="12bbf-236">The front ends act as the HTTP/HTTPS endpoints and send traffic to the workers.</span></span> <span data-ttu-id="12bbf-237">背景工作角色是裝載應用程式的角色。</span><span class="sxs-lookup"><span data-stu-id="12bbf-237">The workers are the roles that host your apps.</span></span> <span data-ttu-id="12bbf-238">建立 ASE 之後，您就可以調整「前端」和「背景工作角色」的數量。</span><span class="sxs-lookup"><span data-stu-id="12bbf-238">You can adjust the quantity of front ends and workers after you create your ASE.</span></span> 

<span data-ttu-id="12bbf-239">若要深入了解 ASEv1，請參閱 [App Service Environment v1 簡介][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-239">To learn more about ASEv1, see [Introduction to the App Service Environment v1][ASEv1Intro].</span></span> <span data-ttu-id="12bbf-240">如需更多關於調整、管理及監視 ASEv1 的資訊，請參閱[如何設定 App Service Environment][ConfigureASEv1]。</span><span class="sxs-lookup"><span data-stu-id="12bbf-240">For more information on scaling, managing, and monitoring ASEv1, see [How to configure an App Service Environment][ConfigureASEv1].</span></span>

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
