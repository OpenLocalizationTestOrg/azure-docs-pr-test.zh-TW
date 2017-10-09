---
title: "aaaCreate 外部的 Azure App Service 環境"
description: "說明如何 toocreate App Service 環境時建立的應用程式或獨立"
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
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a><span data-ttu-id="077f6-103">建立外部 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="077f6-103">Create an External App Service environment</span></span> #

<span data-ttu-id="077f6-104">Azure App Service Environment (ASE) 是將 Azure App Service 部署到客戶 Azure 虛擬網路 (VNet) 中子網路的一種部署。</span><span class="sxs-lookup"><span data-stu-id="077f6-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="077f6-105">有兩種方式 toodeploy App Service 環境 (ASE):</span><span class="sxs-lookup"><span data-stu-id="077f6-105">There are two ways toodeploy an App Service environment (ASE):</span></span>

- <span data-ttu-id="077f6-106">使用外部 IP 位址上的 VIP，通常稱為「外部 ASE」。</span><span class="sxs-lookup"><span data-stu-id="077f6-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="077f6-107">以內部 IP 位址上 hello VIP，通常稱為 ILB ASE 因為 hello 內部端點的內部負載平衡器 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="077f6-107">With hello VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span>

<span data-ttu-id="077f6-108">本文章將示範如何 toocreate 外部 ase。</span><span class="sxs-lookup"><span data-stu-id="077f6-108">This article shows you how toocreate an External ASE.</span></span> <span data-ttu-id="077f6-109">如需 hello ASE 的概觀，請參閱[簡介 toohello App Service 環境][Intro]。</span><span class="sxs-lookup"><span data-stu-id="077f6-109">For an overview of hello ASE, see [An introduction toohello App Service Environment][Intro].</span></span> <span data-ttu-id="077f6-110">如需有關如何 toocreate ILB ASE，請參閱詳細[建立並使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="077f6-110">For information on how toocreate an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="before-you-create-your-ase"></a><span data-ttu-id="077f6-111">建立 ASE 之前</span><span class="sxs-lookup"><span data-stu-id="077f6-111">Before you create your ASE</span></span> ##

<span data-ttu-id="077f6-112">建立您 ASE 之後，您無法變更 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="077f6-112">After you create your ASE, you can't change hello following:</span></span>

- <span data-ttu-id="077f6-113">位置</span><span class="sxs-lookup"><span data-stu-id="077f6-113">Location</span></span>
- <span data-ttu-id="077f6-114">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="077f6-114">Subscription</span></span>
- <span data-ttu-id="077f6-115">資源群組</span><span class="sxs-lookup"><span data-stu-id="077f6-115">Resource group</span></span>
- <span data-ttu-id="077f6-116">使用的 VNet</span><span class="sxs-lookup"><span data-stu-id="077f6-116">VNet used</span></span>
- <span data-ttu-id="077f6-117">使用的子網路</span><span class="sxs-lookup"><span data-stu-id="077f6-117">Subnet used</span></span>
- <span data-ttu-id="077f6-118">子網路大小</span><span class="sxs-lookup"><span data-stu-id="077f6-118">Subnet size</span></span>

> [!NOTE]
> <span data-ttu-id="077f6-119">當您選擇的 VNet，並指定子網路時，請確定它是夠大 tooaccommodate 未來的成長。</span><span class="sxs-lookup"><span data-stu-id="077f6-119">When you choose a VNet and specify a subnet, make sure that it's large enough tooaccommodate future growth.</span></span> <span data-ttu-id="077f6-120">我們建議使用包含 128 個位址的 `/25` 大小。</span><span class="sxs-lookup"><span data-stu-id="077f6-120">We recommend a size of `/25` with 128 addresses.</span></span>
>

## <a name="three-ways-toocreate-an-ase"></a><span data-ttu-id="077f6-121">三種方式 toocreate ase 中</span><span class="sxs-lookup"><span data-stu-id="077f6-121">Three ways toocreate an ASE</span></span> ##

<span data-ttu-id="077f6-122">有三種方式 toocreate ase 中：</span><span class="sxs-lookup"><span data-stu-id="077f6-122">There are three ways toocreate an ASE:</span></span>

- <span data-ttu-id="077f6-123">**建立 App Service 方案時**。</span><span class="sxs-lookup"><span data-stu-id="077f6-123">**While creating an App Service plan**.</span></span> <span data-ttu-id="077f6-124">這個方法會在一個步驟中建立 hello ASE 和 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="077f6-124">This method creates hello ASE and hello App Service plan in one step.</span></span>
- <span data-ttu-id="077f6-125">**作為獨立動作**。</span><span class="sxs-lookup"><span data-stu-id="077f6-125">**As a standalone action**.</span></span> <span data-ttu-id="077f6-126">這個方法會建立獨立 ASE，也就是任何項目的 ASE。</span><span class="sxs-lookup"><span data-stu-id="077f6-126">This method creates a standalone ASE, which is an ASE with nothing in it.</span></span> <span data-ttu-id="077f6-127">這個方法是更進階的程序 toocreate ase。</span><span class="sxs-lookup"><span data-stu-id="077f6-127">This method is a more advanced process toocreate an ASE.</span></span> <span data-ttu-id="077f6-128">您使用它 toocreate ase 中搭配 ILB 一起運作。</span><span class="sxs-lookup"><span data-stu-id="077f6-128">You use it toocreate an ASE with an ILB.</span></span>
- <span data-ttu-id="077f6-129">**從 Azure Resource Manager 範本**。</span><span class="sxs-lookup"><span data-stu-id="077f6-129">**From an Azure Resource Manager template**.</span></span> <span data-ttu-id="077f6-130">這個方法適用於進階使用者。</span><span class="sxs-lookup"><span data-stu-id="077f6-130">This method is for advanced users.</span></span> <span data-ttu-id="077f6-131">如需詳細資訊，請參閱[從範本建立 ASE][MakeASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="077f6-131">For more information, see [Create an ASE from a template][MakeASEfromTemplate].</span></span>

<span data-ttu-id="077f6-132">外部 ase 中都有公用 VIP，這表示所有 HTTP/HTTPS 流量 toohello 應用程式在 hello ASE 中的叫都用可存取網際網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="077f6-132">An External ASE has a public VIP, which means that all HTTP/HTTPS traffic toohello apps in hello ASE hits an internet-accessible IP address.</span></span> <span data-ttu-id="077f6-133">使用 ILB ase 中有 hello hello ASE 所使用的子網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="077f6-133">An ASE with an ILB has an IP address from hello subnet used by hello ASE.</span></span> <span data-ttu-id="077f6-134">hello ILB ASE 中裝載的應用程式不會被公開直接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="077f6-134">hello apps hosted in an ILB ASE aren't exposed directly toohello internet.</span></span>

## <a name="create-an-ase-and-an-app-service-plan-together"></a><span data-ttu-id="077f6-135">一起建立 ASE 和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="077f6-135">Create an ASE and an App Service plan together</span></span> ##

<span data-ttu-id="077f6-136">hello 應用程式服務方案是應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="077f6-136">hello App Service plan is a container of apps.</span></span> <span data-ttu-id="077f6-137">當您在 App Service 中建立應用程式時，要選擇或建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="077f6-137">When you create an app in App Service, you choose or create an App Service plan.</span></span> <span data-ttu-id="077f6-138">hello 容器模型環境保存應用程式服務方案，而且應用程式服務方案保留應用程式。</span><span class="sxs-lookup"><span data-stu-id="077f6-138">hello container model environments hold App Service plans, and App Service plans hold apps.</span></span>

<span data-ttu-id="077f6-139">toocreate ase 中建立 App Service 方案時：</span><span class="sxs-lookup"><span data-stu-id="077f6-139">toocreate an ASE while you create an App Service plan:</span></span>

1. <span data-ttu-id="077f6-140">在 hello [Azure 入口網站](https://portal.azure.com/)，選取**新增** > **Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="077f6-140">In hello [Azure portal](https://portal.azure.com/), select **New** > **Web + Mobile** > **Web App**.</span></span>

    ![建立 Web 應用程式][1]

2. <span data-ttu-id="077f6-142">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="077f6-142">Select your subscription.</span></span> <span data-ttu-id="077f6-143">hello 應用程式和 hello ASE 中建立 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="077f6-143">hello app and hello ASE are created in hello same subscriptions.</span></span>

3. <span data-ttu-id="077f6-144">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="077f6-144">Select or create a resource group.</span></span> <span data-ttu-id="077f6-145">您可以使用資源群組來管理相關的一組 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="077f6-145">With resource groups, you can manage related Azure resources as a unit.</span></span> <span data-ttu-id="077f6-146">當您為應用程式建立角色型存取控制規則時，資源群組也十分實用。</span><span class="sxs-lookup"><span data-stu-id="077f6-146">Resource groups also are useful when you establish Role-Based Access Control rules for your apps.</span></span> <span data-ttu-id="077f6-147">如需詳細資訊，請參閱 hello [Azure 資源管理員概觀][ARMOverview]。</span><span class="sxs-lookup"><span data-stu-id="077f6-147">For more information, see hello [Azure Resource Manager overview][ARMOverview].</span></span>

4. <span data-ttu-id="077f6-148">選取 hello App Service 方案，然後選取**新建**。</span><span class="sxs-lookup"><span data-stu-id="077f6-148">Select hello App Service plan, and then select **Create New**.</span></span>

    ![新增 App Service 方案][2]

5. <span data-ttu-id="077f6-150">在 hello**位置**下拉式清單中，選取 hello 區域想 toocreate hello ASE。</span><span class="sxs-lookup"><span data-stu-id="077f6-150">In hello **Location** drop-down list, select hello region where you want toocreate hello ASE.</span></span> <span data-ttu-id="077f6-151">如果您選取現有的 ASE，就不會建立新的 ASE。</span><span class="sxs-lookup"><span data-stu-id="077f6-151">If you select an existing ASE, a new ASE isn't created.</span></span> <span data-ttu-id="077f6-152">hello 您選取的 ASE 中建立 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="077f6-152">hello App Service plan is created in hello ASE that you selected.</span></span> 

6. <span data-ttu-id="077f6-153">選取**定價層**，然後選擇其中一個 hello**隔離**定價 Sku。</span><span class="sxs-lookup"><span data-stu-id="077f6-153">Select **Pricing tier**, and choose one of hello **Isolated** pricing SKUs.</span></span> <span data-ttu-id="077f6-154">如果您選擇**隔離** SKU 卡以及非 ASE 的位置，就會在該位置中建立新的 ASE。</span><span class="sxs-lookup"><span data-stu-id="077f6-154">If you choose an **Isolated** SKU card and a location that's not an ASE, a new ASE is created in that location.</span></span> <span data-ttu-id="077f6-155">toostart hello 程序 toocreate ase 中，選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="077f6-155">toostart hello process toocreate an ASE, select **Select**.</span></span> <span data-ttu-id="077f6-156">hello**隔離**SKU 不只適用於搭配 ase。</span><span class="sxs-lookup"><span data-stu-id="077f6-156">hello **Isolated** SKU is available only in conjunction with an ASE.</span></span> <span data-ttu-id="077f6-157">您也無法在 ASE 中使用**隔離**以外的其他任何定價 SKU。</span><span class="sxs-lookup"><span data-stu-id="077f6-157">You also can't use any other pricing SKU in an ASE other than **Isolated**.</span></span>

    ![定價層選取項目][3]

7. <span data-ttu-id="077f6-159">輸入您 ASE hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-159">Enter hello name for your ASE.</span></span> <span data-ttu-id="077f6-160">在您的應用程式的 hello 可定址名稱中使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-160">This name is used in hello addressable name for your apps.</span></span> <span data-ttu-id="077f6-161">如果 hello ASE hello 名稱是_appsvcenvdemo_，hello 網域名稱是*。 appsvcenvdemo.p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="077f6-161">If hello name of hello ASE is _appsvcenvdemo_, hello domain name is *.appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="077f6-162">如果您建立名為 mytestapp 的應用程式，則可定址於 mytestapp.appsvcenvdemo.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="077f6-162">If you create an app named *mytestapp*, it's addressable at mytestapp.appsvcenvdemo.p.azurewebsites.net.</span></span> <span data-ttu-id="077f6-163">您無法在 hello 名稱中使用空白字元。</span><span class="sxs-lookup"><span data-stu-id="077f6-163">You can't use white space in hello name.</span></span> <span data-ttu-id="077f6-164">如果您使用大寫字元，hello 網域名稱是 hello 總小寫版本名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-164">If you use uppercase characters, hello domain name is hello total lowercase version of that name.</span></span>

    ![新增 App Service 方案名稱][4]

8. <span data-ttu-id="077f6-166">指定 Azure 虛擬網路詳細資料。</span><span class="sxs-lookup"><span data-stu-id="077f6-166">Specify your Azure virtual networking details.</span></span> <span data-ttu-id="077f6-167">選取 [新建] 或 [選取現有]。</span><span class="sxs-lookup"><span data-stu-id="077f6-167">Select either **Create New** or **Select Existing**.</span></span> <span data-ttu-id="077f6-168">只有當您擁有 hello 所選資料區域中的 VNet 使用 hello 選項 tooselect 現有的 VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-168">hello option tooselect an existing VNet is available only if you have a VNet in hello selected region.</span></span> <span data-ttu-id="077f6-169">如果您選取**新建**，輸入 hello VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-169">If you select **Create New**, enter a name for hello VNet.</span></span> <span data-ttu-id="077f6-170">會建立具有該名稱的 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-170">A new Resource Manager VNet with that name is created.</span></span> <span data-ttu-id="077f6-171">它會使用 hello 位址空間`192.168.250.0/23`hello 所選資料區域中。</span><span class="sxs-lookup"><span data-stu-id="077f6-171">It uses hello address space `192.168.250.0/23` in hello selected region.</span></span> <span data-ttu-id="077f6-172">如果您選取 [選取現有]，您需要：</span><span class="sxs-lookup"><span data-stu-id="077f6-172">If you select **Select Existing**, you need to:</span></span>

    <span data-ttu-id="077f6-173">a.</span><span class="sxs-lookup"><span data-stu-id="077f6-173">a.</span></span> <span data-ttu-id="077f6-174">如果您有一個以上，請選取 hello VNet 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="077f6-174">Select hello VNet address block, if you have more than one.</span></span>

    <span data-ttu-id="077f6-175">b.</span><span class="sxs-lookup"><span data-stu-id="077f6-175">b.</span></span> <span data-ttu-id="077f6-176">輸入新的子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-176">Enter a new subnet name.</span></span>

    <span data-ttu-id="077f6-177">c.</span><span class="sxs-lookup"><span data-stu-id="077f6-177">c.</span></span> <span data-ttu-id="077f6-178">選取 hello hello 子網路大小。</span><span class="sxs-lookup"><span data-stu-id="077f6-178">Select hello size of hello subnet.</span></span> <span data-ttu-id="077f6-179">*請記住 tooselect 您 ASE 大小夠大 tooaccommodate 未來成長。*</span><span class="sxs-lookup"><span data-stu-id="077f6-179">*Remember tooselect a size large enough tooaccommodate future growth of your ASE.*</span></span> <span data-ttu-id="077f6-180">建議是 `/25`，具有 128 個位址，而且可以處理最大大小的 ASE。</span><span class="sxs-lookup"><span data-stu-id="077f6-180">We recommend `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="077f6-181">例如，不建議 `/28`，因為只有 16 個位址可供使用。</span><span class="sxs-lookup"><span data-stu-id="077f6-181">We don't recommend `/28`, for example, because only 16 addresses are available.</span></span> <span data-ttu-id="077f6-182">基礎結構會使用至少五個位址。</span><span class="sxs-lookup"><span data-stu-id="077f6-182">Infrastructure uses at least five addresses.</span></span> <span data-ttu-id="077f6-183">在 `/28` 子網路中，您會擁有 11 個執行個體的最大縮放比例。</span><span class="sxs-lookup"><span data-stu-id="077f6-183">In a `/28` subnet, you're left with a maximum scaling of 11 instances.</span></span>

    <span data-ttu-id="077f6-184">d.</span><span class="sxs-lookup"><span data-stu-id="077f6-184">d.</span></span> <span data-ttu-id="077f6-185">選取 hello 子網路 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="077f6-185">Select hello subnet IP range.</span></span>

9. <span data-ttu-id="077f6-186">選取**建立**toocreate hello ASE。</span><span class="sxs-lookup"><span data-stu-id="077f6-186">Select **Create** toocreate hello ASE.</span></span> <span data-ttu-id="077f6-187">Hello App Service 方案及 hello 應用程式，也會建立此程序。</span><span class="sxs-lookup"><span data-stu-id="077f6-187">This process also creates hello App Service plan and hello app.</span></span> <span data-ttu-id="077f6-188">hello ASE、 應用程式服務方案和應用程式是全部都是在 hello 相同訂用帳戶和也在 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="077f6-188">hello ASE, App Service plan, and app are all under hello same subscription and also in hello same resource group.</span></span> <span data-ttu-id="077f6-189">如果您 ASE 需要針對個別資源群組，或需要 ILB ase 中，遵循 hello 步驟 toocreate ase 中單獨使用。</span><span class="sxs-lookup"><span data-stu-id="077f6-189">If your ASE needs a separate resource group or if you need an ILB ASE, follow hello steps toocreate an ASE by itself.</span></span>

## <a name="create-an-ase-by-itself"></a><span data-ttu-id="077f6-190">由 ASE 本身建立</span><span class="sxs-lookup"><span data-stu-id="077f6-190">Create an ASE by itself</span></span> ##

<span data-ttu-id="077f6-191">如果您建立 ASE 獨立，它就不會包含任何項目。</span><span class="sxs-lookup"><span data-stu-id="077f6-191">If you create an ASE standalone, it has nothing in it.</span></span> <span data-ttu-id="077f6-192">空白 ase 中仍會產生 hello 基礎結構的每月費用。</span><span class="sxs-lookup"><span data-stu-id="077f6-192">An empty ASE still incurs a monthly charge for hello infrastructure.</span></span> <span data-ttu-id="077f6-193">請遵循這些步驟 toocreate ase 中搭配 ILB 一起運作或 toocreate ase 中在它自己的資源群組。</span><span class="sxs-lookup"><span data-stu-id="077f6-193">Follow these steps toocreate an ASE with an ILB or toocreate an ASE in its own resource group.</span></span> <span data-ttu-id="077f6-194">建立您 ASE 之後，您可以使用 hello 一般程序中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="077f6-194">After you create your ASE, you can create apps in it by using hello normal process.</span></span> <span data-ttu-id="077f6-195">選取您新 ASE 做為 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="077f6-195">Select your new ASE as hello location.</span></span>

1. <span data-ttu-id="077f6-196">搜尋 hello Azure Marketplace 中的**App Service 環境**，或選取**新增** > **Web 行動** > **應用程式服務環境**。</span><span class="sxs-lookup"><span data-stu-id="077f6-196">Search hello Azure Marketplace for **App Service Environment**, or select **New** > **Web Mobile** > **App Service Environment**.</span></span> 

2. <span data-ttu-id="077f6-197">輸入您 ASE hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-197">Enter hello name of your ASE.</span></span> <span data-ttu-id="077f6-198">這個名稱會用於建立 hello ASE 中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="077f6-198">This name is used for hello apps created in hello ASE.</span></span> <span data-ttu-id="077f6-199">如果 hello 名稱*mynewdemoase*，hello 子網域名稱是*。 mynewdemoase.p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="077f6-199">If hello name is *mynewdemoase*, hello subdomain name is *.mynewdemoase.p.azurewebsites.net*.</span></span> <span data-ttu-id="077f6-200">如果您建立名為 mytestapp 的應用程式，則可定址於 mytestapp.mynewdemoase.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="077f6-200">If you create an app named *mytestapp*, it's addressable at mytestapp.mynewdemoase.p.azurewebsites.net.</span></span> <span data-ttu-id="077f6-201">您無法在 hello 名稱中使用空白字元。</span><span class="sxs-lookup"><span data-stu-id="077f6-201">You can't use white space in hello name.</span></span> <span data-ttu-id="077f6-202">如果您使用大寫字元，hello 網域名稱是 hello 總小寫版本 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="077f6-202">If you use uppercase characters, hello domain name is hello total lowercase version of hello name.</span></span> <span data-ttu-id="077f6-203">如果您是使用 ILB，ASE 名稱就不會用於您的子網域中，但是會在 ASE 建立期間明確指定。</span><span class="sxs-lookup"><span data-stu-id="077f6-203">If you use an ILB, your ASE name isn't used in your subdomain but is instead explicitly stated during ASE creation.</span></span>

    ![ASE 命名][5]

3. <span data-ttu-id="077f6-205">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="077f6-205">Select your subscription.</span></span> <span data-ttu-id="077f6-206">此訂用帳戶也是 hello hello ASE 中的所有應用程式使用的其中一個。</span><span class="sxs-lookup"><span data-stu-id="077f6-206">This subscription is also hello one that all apps in hello ASE use.</span></span> <span data-ttu-id="077f6-207">您無法將 ASE 放在另一個訂用帳戶中的 VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-207">You can't put your ASE in a VNet that's in another subscription.</span></span>

4. <span data-ttu-id="077f6-208">選取或指定新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="077f6-208">Select or specify a new resource group.</span></span> <span data-ttu-id="077f6-209">hello 同一個用於您的 VNet 時，必須要用於您 ASE hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="077f6-209">hello resource group used for your ASE must be hello same one that's used for your VNet.</span></span> <span data-ttu-id="077f6-210">如果您選取現有的 VNet，針對您 ASE hello 資源群組的選擇是更新的 tooreflect 的 VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-210">If you select an existing VNet, hello resource group selection for your ASE is updated tooreflect that of your VNet.</span></span> <span data-ttu-id="077f6-211">*您可以建立 ase 中是不同於 hello VNet 資源群組，如果您使用資源管理員範本的資源群組。*</span><span class="sxs-lookup"><span data-stu-id="077f6-211">*You can create an ASE with a resource group that is different from hello VNet resource group if you use a Resource Manager template.*</span></span> <span data-ttu-id="077f6-212">toocreate ase 中的從範本，請參閱[從範本建立 App Service 環境][MakeASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="077f6-212">toocreate an ASE from a template, see [Create an App Service environment from a template][MakeASEfromTemplate].</span></span>

    ![資源群組選取項目][6]

5. <span data-ttu-id="077f6-214">選取您的 VNet 和位置。</span><span class="sxs-lookup"><span data-stu-id="077f6-214">Select your VNet and location.</span></span> <span data-ttu-id="077f6-215">您可以建立新的 VNet 或選取現有的 VNet：</span><span class="sxs-lookup"><span data-stu-id="077f6-215">You can create a new VNet or select an existing VNet:</span></span> 

    * <span data-ttu-id="077f6-216">如果您選取新的 VNet，就可以指定名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="077f6-216">If you select a new VNet, you can specify a name and location.</span></span> <span data-ttu-id="077f6-217">hello 新的 VNet 有 hello 位址範圍 192.168.250.0/23 和名為 default 的子網路。</span><span class="sxs-lookup"><span data-stu-id="077f6-217">hello new VNet has hello address range 192.168.250.0/23 and a subnet named default.</span></span> <span data-ttu-id="077f6-218">hello 子網路定義為 192.168.250.0/24。</span><span class="sxs-lookup"><span data-stu-id="077f6-218">hello subnet is defined as 192.168.250.0/24.</span></span> <span data-ttu-id="077f6-219">您只能選取 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-219">You can only select a Resource Manager VNet.</span></span> <span data-ttu-id="077f6-220">hello **VIP 類型**的選擇會決定是否從可以直接存取您 ASE hello 網際網路 （外部） 或如果它使用 ILB。</span><span class="sxs-lookup"><span data-stu-id="077f6-220">hello **VIP Type** selection determines if your ASE can be directly accessed from hello internet (External) or if it uses an ILB.</span></span> <span data-ttu-id="077f6-221">toolearn 進一步了解這些選項，請參閱[建立並使用 App Service 環境的內部負載平衡器][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="077f6-221">toolearn more about these options, see [Create and use an internal load balancer with an App Service environment][MakeILBASE].</span></span> 

      * <span data-ttu-id="077f6-222">如果您選取**外部**hello **VIP 類型**，您可以選取多少外部 IP 位址 hello 系統會透過 IP SSL 的用途。</span><span class="sxs-lookup"><span data-stu-id="077f6-222">If you select **External** for hello **VIP Type**, you can select how many external IP addresses hello system is created with for IP-based SSL purposes.</span></span> 
    
      * <span data-ttu-id="077f6-223">如果您選取**內部**hello **VIP 類型**，您必須指定您 ASE 使用 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="077f6-223">If you select **Internal** for hello **VIP Type**, you must specify hello domain that your ASE uses.</span></span> <span data-ttu-id="077f6-224">您可以將 ASE 部署到使用公用或私人位址範圍的 VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-224">You can deploy an ASE into a VNet that uses public or private address ranges.</span></span> <span data-ttu-id="077f6-225">toouse 公用位址範圍的 VNet，您必須事先 toocreate hello VNet。</span><span class="sxs-lookup"><span data-stu-id="077f6-225">toouse a VNet with a public address range, you need toocreate hello VNet ahead of time.</span></span> 
    
    * <span data-ttu-id="077f6-226">如果您選取現有的 VNet，請建立 hello ASE 時建立新的子網路。</span><span class="sxs-lookup"><span data-stu-id="077f6-226">If you select an existing VNet, a new subnet is created when hello ASE is created.</span></span> <span data-ttu-id="077f6-227">*您無法在 hello 入口網站中使用的預先建立的子網路。如果您是使用 Resource Manager 範本，則可以使用現有的子網路建立 ASE。*</span><span class="sxs-lookup"><span data-stu-id="077f6-227">*You can't use a pre-created subnet in hello portal. You can create an ASE with an existing subnet if you use a Resource Manager template.*</span></span> <span data-ttu-id="077f6-228">toocreate ase 中的從範本，請參閱[從範本建立 App Service 環境][MakeASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="077f6-228">toocreate an ASE from a template, see [Create an App Service Environment from a template][MakeASEfromTemplate].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="077f6-229">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="077f6-229">App Service Environment v1</span></span> ##

<span data-ttu-id="077f6-230">您仍然可以建立 hello 第一個版本的 App Service 環境 (ASEv1) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="077f6-230">You can still create instances of hello first version of App Service Environment (ASEv1).</span></span> <span data-ttu-id="077f6-231">處理時，搜尋 hello Marketplace 的 toostart 如**App Service 環境 v1**。</span><span class="sxs-lookup"><span data-stu-id="077f6-231">toostart that process, search hello Marketplace for **App Service Environment v1**.</span></span> <span data-ttu-id="077f6-232">您可以建立 hello ASE 中 hello 建立 hello 獨立 ASE 相同方式。</span><span class="sxs-lookup"><span data-stu-id="077f6-232">You create hello ASE in hello same way that you create hello standalone ASE.</span></span> <span data-ttu-id="077f6-233">完成後，您的 ASEv1 會有兩個「前端」和兩個「背景工作角色」。</span><span class="sxs-lookup"><span data-stu-id="077f6-233">When it's finished, your ASEv1 has two front ends and two workers.</span></span> <span data-ttu-id="077f6-234">與 ASEv1，您必須管理 hello 前端和背景工作。</span><span class="sxs-lookup"><span data-stu-id="077f6-234">With ASEv1, you must manage hello front ends and workers.</span></span> <span data-ttu-id="077f6-235">當您建立 App Service 方案時，它們不會自動新增。</span><span class="sxs-lookup"><span data-stu-id="077f6-235">They're not automatically added when you create your App Service plans.</span></span> <span data-ttu-id="077f6-236">hello 前端做為 hello HTTP/HTTPS 端點，並且將流量傳送 toohello 背景工作。</span><span class="sxs-lookup"><span data-stu-id="077f6-236">hello front ends act as hello HTTP/HTTPS endpoints and send traffic toohello workers.</span></span> <span data-ttu-id="077f6-237">hello 工作者是 hello 角色裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="077f6-237">hello workers are hello roles that host your apps.</span></span> <span data-ttu-id="077f6-238">建立您 ASE 之後，您可以調整 hello 前端和背景工作數量。</span><span class="sxs-lookup"><span data-stu-id="077f6-238">You can adjust hello quantity of front ends and workers after you create your ASE.</span></span> 

<span data-ttu-id="077f6-239">toolearn 深入了解 ASEv1，請參閱[簡介 toohello App Service 環境 v1][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="077f6-239">toolearn more about ASEv1, see [Introduction toohello App Service Environment v1][ASEv1Intro].</span></span> <span data-ttu-id="077f6-240">如需有關調整的詳細資訊，管理及監視 ASEv1，請參閱[如何 tooconfigure App Service 環境][ConfigureASEv1]。</span><span class="sxs-lookup"><span data-stu-id="077f6-240">For more information on scaling, managing, and monitoring ASEv1, see [How tooconfigure an App Service Environment][ConfigureASEv1].</span></span>

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
