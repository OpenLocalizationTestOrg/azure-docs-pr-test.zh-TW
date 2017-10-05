---
title: "使用 Azure App Service Environment"
description: "如何在 Azure App Service Environment 中建立、發佈及調整應用程式"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 279951d40b7780120d0b94e183f06e00ccece016
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="ab350-103">使用 App Service Environment</span><span class="sxs-lookup"><span data-stu-id="ab350-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="ab350-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ab350-104">Overview</span></span> ##

<span data-ttu-id="ab350-105">Azure App Service Environment (ASE) 是 Azure App Service 到客戶之 Azure 虛擬網路中子網路的部署。</span><span class="sxs-lookup"><span data-stu-id="ab350-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="ab350-106">其中包括：</span><span class="sxs-lookup"><span data-stu-id="ab350-106">It consists of:</span></span>

- <span data-ttu-id="ab350-107">**前端**：前端為 App Service Environment (ASE) 中 HTTP/HTTPS 終止的位置。</span><span class="sxs-lookup"><span data-stu-id="ab350-107">**Front ends**: The front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="ab350-108">**背景工作**：這些背景工作是裝載應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="ab350-108">**Workers**: The workers are the resources that host your apps.</span></span>
- <span data-ttu-id="ab350-109">**資料庫**：資料庫會保留定義環境的資訊。</span><span class="sxs-lookup"><span data-stu-id="ab350-109">**Database**: The database holds information that defines the environment.</span></span>
- <span data-ttu-id="ab350-110">**儲存體**：儲存體可用來裝載客戶發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab350-110">**Storage**: The storage is used to host the customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="ab350-111">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="ab350-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="ab350-112">在 ASEv1 中，您必須先管理資源，才可加以使用。</span><span class="sxs-lookup"><span data-stu-id="ab350-112">In ASEv1, you must manage the resources before you can use them.</span></span> <span data-ttu-id="ab350-113">若要了解如何設定及管理 ASEv1，請參閱[設定 App Service Environment v1][ConfigureASEv1]。</span><span class="sxs-lookup"><span data-stu-id="ab350-113">To learn how to configure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="ab350-114">本文的其餘部分著重於 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="ab350-114">The rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="ab350-115">您可以使用適用於應用程式存取的外部 VIP 或內部 VIP，來部署 ASE (ASEv1 和 ASEv2)。</span><span class="sxs-lookup"><span data-stu-id="ab350-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="ab350-116">使用外部 VIP 的部署常稱為外部 ASE。</span><span class="sxs-lookup"><span data-stu-id="ab350-116">The deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="ab350-117">內部版本稱為 ILB ASE，因為它是使用內部負載平衡器 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="ab350-117">The internal version is called the ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="ab350-118">若要深入了解 ILB ASE，請參閱[建立和使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="ab350-118">To learn more about the ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="ab350-119">在 ASE 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ab350-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="ab350-120">若要在 ASE 中建立 Web 應用程式，可以使用和一般建立程序相同的程序，但有幾個小差異。</span><span class="sxs-lookup"><span data-stu-id="ab350-120">To create a web app in an ASE, you use the same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="ab350-121">當您建立新的 App Service 方案時：</span><span class="sxs-lookup"><span data-stu-id="ab350-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="ab350-122">您可以挑選 ASE 作為位置，而不用挑選部署應用程式的地理位置。</span><span class="sxs-lookup"><span data-stu-id="ab350-122">Instead of choosing a geographic location in which to deploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="ab350-123">在 ASE 中建立的所有 App Service 方案必須在「隔離」定價層中。</span><span class="sxs-lookup"><span data-stu-id="ab350-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="ab350-124">如果您沒有 ASE，則可以遵循[建立 App Service Environment][MakeExternalASE] 中的指示來建立一個 ASE。</span><span class="sxs-lookup"><span data-stu-id="ab350-124">If you don't have an ASE, you can create one by following the instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="ab350-125">若要在 ASE 中建立 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="ab350-125">To create a web app in an ASE:</span></span>

1. <span data-ttu-id="ab350-126">選取 [新增] > [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ab350-126">Select **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="ab350-127">輸入 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ab350-127">Enter a name for the web app.</span></span> <span data-ttu-id="ab350-128">如果您已在 ASE 中選取 App Service 方案，則應用程式的網域名稱會反映 ASE 的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ab350-128">If you already selected an App Service plan in an ASE, the domain name for the app reflects the domain name of the ASE.</span></span>

    ![選取 Web 應用程式名稱][1]

3. <span data-ttu-id="ab350-130">選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab350-130">Select a subscription.</span></span>

4. <span data-ttu-id="ab350-131">輸入新資源群組的名稱，或選取 [使用現有] 並從下拉式清單中挑選一個。</span><span class="sxs-lookup"><span data-stu-id="ab350-131">Enter a name for a new resource group, or select **Use existing** and select one from the drop-down list.</span></span>

5. <span data-ttu-id="ab350-132">選取 ASE 中現有的 App Service 方案，或透過下列步驟建立一個新的方案：</span><span class="sxs-lookup"><span data-stu-id="ab350-132">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="ab350-133">a.</span><span class="sxs-lookup"><span data-stu-id="ab350-133">a.</span></span> <span data-ttu-id="ab350-134">選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="ab350-134">Select **Create New**.</span></span>

    <span data-ttu-id="ab350-135">b.</span><span class="sxs-lookup"><span data-stu-id="ab350-135">b.</span></span> <span data-ttu-id="ab350-136">輸入 App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="ab350-136">Enter the name for your App Service plan.</span></span>

    <span data-ttu-id="ab350-137">c.</span><span class="sxs-lookup"><span data-stu-id="ab350-137">c.</span></span> <span data-ttu-id="ab350-138">在 [位置] 下拉式清單中選取您的 ASE。</span><span class="sxs-lookup"><span data-stu-id="ab350-138">Select your ASE in the **Location** drop-down list.</span></span>

    <span data-ttu-id="ab350-139">d.</span><span class="sxs-lookup"><span data-stu-id="ab350-139">d.</span></span> <span data-ttu-id="ab350-140">選取 [隔離] 定價層。</span><span class="sxs-lookup"><span data-stu-id="ab350-140">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="ab350-141">選取 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="ab350-141">Select **Select**.</span></span>

    <span data-ttu-id="ab350-142">e.</span><span class="sxs-lookup"><span data-stu-id="ab350-142">e.</span></span> <span data-ttu-id="ab350-143">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ab350-143">Select **OK**.</span></span>
    
    ![隔離定價層][2]

6. <span data-ttu-id="ab350-145">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ab350-145">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="ab350-146">調整方式</span><span class="sxs-lookup"><span data-stu-id="ab350-146">How scale works</span></span> ##

<span data-ttu-id="ab350-147">每個 App Service 應用程式都會在 App Service 方案中執行。</span><span class="sxs-lookup"><span data-stu-id="ab350-147">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="ab350-148">容器模型是：保存 App Service 方案的環境，和保存應用程式的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ab350-148">The container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="ab350-149">當您調整應用程式時，您可調整 App Service 方案，因而調整相同方案中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab350-149">When you scale an app, you scale the App Service plan and thus scale all the apps in the same plan.</span></span>

<span data-ttu-id="ab350-150">在 ASEv2 中，當您調整 App Service 方案時，系統會自動新增所需的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ab350-150">In ASEv2, when you scale an App Service plan, the needed infrastructure is automatically added.</span></span> <span data-ttu-id="ab350-151">新增基礎結構後，調整作業會有時間延遲。</span><span class="sxs-lookup"><span data-stu-id="ab350-151">There is a time delay to scale operations while the infrastructure is added.</span></span> <span data-ttu-id="ab350-152">在 ASEv1 中，您必須先在其中新增所需的基礎結構，才能建立或相應放大 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ab350-152">In ASEv1, the needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="ab350-153">在多租用戶的 App Service 中，調整通常是立即性的，因為確實有可用的資源集區可用來支援它。</span><span class="sxs-lookup"><span data-stu-id="ab350-153">In the multitenant App Service, scaling is usually immediate because a pool of resources is readily available to support it.</span></span> <span data-ttu-id="ab350-154">ASE 中沒有這類緩衝區，並在需要時配置資源。</span><span class="sxs-lookup"><span data-stu-id="ab350-154">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="ab350-155">在 ASE 中，您可以相應增加至 100 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="ab350-155">In an ASE, you can scale up to 100 instances.</span></span> <span data-ttu-id="ab350-156">這 100 個執行個體可以全都位於單一 App Service 方案中，或分散於多個 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ab350-156">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="ab350-157">IP 位址</span><span class="sxs-lookup"><span data-stu-id="ab350-157">IP addresses</span></span> ##

<span data-ttu-id="ab350-158">App Service 能夠將專用的 IP 位址配置給應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab350-158">App Service has the ability to allocate a dedicated IP address to an app.</span></span> <span data-ttu-id="ab350-159">設定以 IP 為基礎的 SSL 之後，就可以使用這項功能，如下所述：[將現有的自訂 SSL 憑證繫結至 Azure Web Apps][ConfigureSSL]。</span><span class="sxs-lookup"><span data-stu-id="ab350-159">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate to Azure web apps][ConfigureSSL].</span></span> <span data-ttu-id="ab350-160">但是，在 ASE 中，有一個明顯的例外。</span><span class="sxs-lookup"><span data-stu-id="ab350-160">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="ab350-161">您無法新增額外的 IP 位址來供 ILB ASE 中以 IP 為基礎的 SSL 使用。</span><span class="sxs-lookup"><span data-stu-id="ab350-161">You can't add additional IP addresses to be used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="ab350-162">在 ASEv1 中，您必須先配置 IP 位址作為資源，才可以使用它們。</span><span class="sxs-lookup"><span data-stu-id="ab350-162">In ASEv1, you need to allocate the IP addresses as resources before you can use them.</span></span> <span data-ttu-id="ab350-163">在 ASEv2 中，您可以如同在多租用戶的 App Service 中一樣，從您的應用程式使用它們。</span><span class="sxs-lookup"><span data-stu-id="ab350-163">In ASEv2, you use them from your app just as you do in the multitenant App Service.</span></span> <span data-ttu-id="ab350-164">ASEv2 中一律會有一個備用位址 (最多 30 個 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="ab350-164">There is always one spare address in ASEv2 up to 30 IP addresses.</span></span> <span data-ttu-id="ab350-165">每次您使用一個位址時，就會新增另一個位址，如此一律會有立即可供使用的位址。</span><span class="sxs-lookup"><span data-stu-id="ab350-165">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="ab350-166">配置另一個 IP 位址時，需有時間延遲，以避免快速連續新增 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ab350-166">A time delay is required to allocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="ab350-167">前端調整大小</span><span class="sxs-lookup"><span data-stu-id="ab350-167">Front-end scaling</span></span> ##

<span data-ttu-id="ab350-168">在 ASEv2 中，當您相應放大 App Service 方案時，系統會自動新增背景工作來支援它們。</span><span class="sxs-lookup"><span data-stu-id="ab350-168">In ASEv2, when you scale out your App Service plans, workers are automatically added to support them.</span></span> <span data-ttu-id="ab350-169">每個 ASE 建立時都會包含兩個前端。</span><span class="sxs-lookup"><span data-stu-id="ab350-169">Every ASE is created with two front ends.</span></span> <span data-ttu-id="ab350-170">此外，您的 App Service 方案中，每 15 個執行個體會有一個前端，因此前端會依據此規則自動相應放大。</span><span class="sxs-lookup"><span data-stu-id="ab350-170">In addition, the front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="ab350-171">例如，如果您有 15 個執行個體，則會有三個前端。</span><span class="sxs-lookup"><span data-stu-id="ab350-171">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="ab350-172">如果調整至 30 個執行個體，則您會有四個前端 ，依此類推。</span><span class="sxs-lookup"><span data-stu-id="ab350-172">If you scale to 30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="ab350-173">這個前端數目應該足以適用於大部分情況。</span><span class="sxs-lookup"><span data-stu-id="ab350-173">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="ab350-174">但是，您也可用更快的速率相應放大。</span><span class="sxs-lookup"><span data-stu-id="ab350-174">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="ab350-175">您可以將前端與執行處理的比例變更至最低每五個執行個體有一個前端。</span><span class="sxs-lookup"><span data-stu-id="ab350-175">You can change the ratio to as low as one front end for every five instances.</span></span> <span data-ttu-id="ab350-176">變更比例需付費。</span><span class="sxs-lookup"><span data-stu-id="ab350-176">There is a charge for changing the ratio.</span></span> <span data-ttu-id="ab350-177">如需詳細資訊，請參閱 [Azure App Service 價格][Pricing]。</span><span class="sxs-lookup"><span data-stu-id="ab350-177">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="ab350-178">前端資源是 ASE 的 HTTP/HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="ab350-178">Front-end resources are the HTTP/HTTPS endpoint for the ASE.</span></span> <span data-ttu-id="ab350-179">依照預設前端組態，每個前端的記憶體使用量始終大約為 60%。</span><span class="sxs-lookup"><span data-stu-id="ab350-179">With the default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="ab350-180">客戶工作負載不會在前端上執行。</span><span class="sxs-lookup"><span data-stu-id="ab350-180">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="ab350-181">前端調整的關鍵因素是 CPU，其主要是由 HTTPS 流量所驅動。</span><span class="sxs-lookup"><span data-stu-id="ab350-181">The key factor for a front end with respect to scale is the CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="ab350-182">應用程式存取</span><span class="sxs-lookup"><span data-stu-id="ab350-182">App access</span></span> ##

<span data-ttu-id="ab350-183">在外部 ASE 中，您在建立應用程式時使用的網域，和多租用戶 App Service 的網域是不一樣的。</span><span class="sxs-lookup"><span data-stu-id="ab350-183">In an External ASE, the domain that's used when you create apps is different from the multitenant App Service.</span></span> <span data-ttu-id="ab350-184">它包括了 ASE 的名稱。</span><span class="sxs-lookup"><span data-stu-id="ab350-184">It includes the name of the ASE.</span></span> <span data-ttu-id="ab350-185">如需有關如何建立外部 ASE 的詳細資訊，請參閱[建立 App Service Environment][MakeExternalASE]。</span><span class="sxs-lookup"><span data-stu-id="ab350-185">For more information on how to create an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="ab350-186">外部 ASE 中的網域名稱看起來像 *.&lt;asename&gt;.p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="ab350-186">The domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="ab350-187">例如，如果您的 ASE 名為 _external-ase_，而且您在該 ASE 中裝載名為 _contoso_ 的應用程式，則下列 URL 將可連至該應用程式：</span><span class="sxs-lookup"><span data-stu-id="ab350-187">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at the following URLs:</span></span>

- <span data-ttu-id="ab350-188">contoso.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ab350-188">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="ab350-189">contoso.scm.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ab350-189">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="ab350-190">URL contoso.scm.external-ase.p.azurewebsites.net 用來存取 Kudu 主控台，或可利用 Web 部署發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab350-190">The URL contoso.scm.external-ase.p.azurewebsites.net is used to access the Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="ab350-191">如需 Kudu 主控台的詳細資訊，請參閱 [Azure App Service 的 Kudu 主控台][Kudu]。</span><span class="sxs-lookup"><span data-stu-id="ab350-191">For information on the Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="ab350-192">Kudu 主控台提供給您的 Web UI 可供偵錯、上傳檔案、編輯檔案及更多功能。</span><span class="sxs-lookup"><span data-stu-id="ab350-192">The Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="ab350-193">在 ILB ASE 中，您會在部署時決定網域。</span><span class="sxs-lookup"><span data-stu-id="ab350-193">In an ILB ASE, you determine the domain at deployment time.</span></span> <span data-ttu-id="ab350-194">如需有關如何建立 ILB ASE 的詳細資訊，請參閱[建立並使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="ab350-194">For more information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="ab350-195">如果您指定網域名稱 _ilb-ase.info_，則該 ASE 中的應用程式會在應用程式建立期間使用該網域。</span><span class="sxs-lookup"><span data-stu-id="ab350-195">If you specify the domain name _ilb-ase.info_, the apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="ab350-196">對於名為 _contoso_ 的應用程式，則 URL 會是：</span><span class="sxs-lookup"><span data-stu-id="ab350-196">For the app named _contoso_, the URLs are:</span></span>

- <span data-ttu-id="ab350-197">contoso.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="ab350-197">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="ab350-198">contoso.scm.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="ab350-198">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="ab350-199">發佈</span><span class="sxs-lookup"><span data-stu-id="ab350-199">Publishing</span></span> ##

<span data-ttu-id="ab350-200">如同多租用戶 App Service，在 ASE 中，您可以透過下列各項發佈：</span><span class="sxs-lookup"><span data-stu-id="ab350-200">As with the multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="ab350-201">Web 部署。</span><span class="sxs-lookup"><span data-stu-id="ab350-201">Web deployment.</span></span>
- <span data-ttu-id="ab350-202">FTP。</span><span class="sxs-lookup"><span data-stu-id="ab350-202">FTP.</span></span>
- <span data-ttu-id="ab350-203">持續整合。</span><span class="sxs-lookup"><span data-stu-id="ab350-203">Continuous integration.</span></span>
- <span data-ttu-id="ab350-204">在 Kudu 主控台中拖放。</span><span class="sxs-lookup"><span data-stu-id="ab350-204">Drag and drop in the Kudu console.</span></span>
- <span data-ttu-id="ab350-205">IDE，例如 Visual Studio、Eclipse 或 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="ab350-205">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="ab350-206">使用外部 ASE 時，這些發行選項的行為相同。</span><span class="sxs-lookup"><span data-stu-id="ab350-206">With an External ASE, these publishing options all behave the same.</span></span> <span data-ttu-id="ab350-207">如需詳細資訊，請參閱[在 Azure App Service 中部署][AppDeploy]。</span><span class="sxs-lookup"><span data-stu-id="ab350-207">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="ab350-208">在發佈上的主要差異和 ILB ASE 有關。</span><span class="sxs-lookup"><span data-stu-id="ab350-208">The major difference with publishing is with respect to an ILB ASE.</span></span> <span data-ttu-id="ab350-209">使用 ILB ASE 時，所有發佈端點都只能透過 ILB 取得。</span><span class="sxs-lookup"><span data-stu-id="ab350-209">With an ILB ASE, the publishing endpoints are all available only through the ILB.</span></span> <span data-ttu-id="ab350-210">ILB 位於虛擬網路的 ASE 子網路中的私人 IP。</span><span class="sxs-lookup"><span data-stu-id="ab350-210">The ILB is on a private IP in the ASE subnet in the virtual network.</span></span> <span data-ttu-id="ab350-211">如果您沒有 ILB 的網路存取權，便無法在該 ASE 上發佈任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab350-211">If you don’t have network access to the ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="ab350-212">如[建立和使用 ILB ASE][MakeILBASE] 中所述，您需要在系統中設定應用程式的 DNS。</span><span class="sxs-lookup"><span data-stu-id="ab350-212">As noted in [Create and use an ILB ASE][MakeILBASE], you need to configure DNS for the apps in the system.</span></span> <span data-ttu-id="ab350-213">其中包含 SCM 端點。</span><span class="sxs-lookup"><span data-stu-id="ab350-213">That includes the SCM endpoint.</span></span> <span data-ttu-id="ab350-214">如果未正確定義它們，就無法發佈。</span><span class="sxs-lookup"><span data-stu-id="ab350-214">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="ab350-215">您的 IDE 也需要有 ILB 的網路存取權，以便直接發佈到它。</span><span class="sxs-lookup"><span data-stu-id="ab350-215">Your IDEs also need to have network access to the ILB in order to publish directly to it.</span></span>

<span data-ttu-id="ab350-216">以網際網路為基礎的 CI 系統，例如 GitHub 和 Visual Studio Team Services，不會與 ILB ASE 搭配運作，因為發佈端點不是網際網路可存取。</span><span class="sxs-lookup"><span data-stu-id="ab350-216">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="ab350-217">相反地，您需要使用會使用提取模型的 CI 系統，例如 Dropbox。</span><span class="sxs-lookup"><span data-stu-id="ab350-217">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="ab350-218">ILB ASE 中應用程式的發佈端點會使用用來建立 ILB ASE 的網域。</span><span class="sxs-lookup"><span data-stu-id="ab350-218">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="ab350-219">您可以在應用程式的發行設定檔，以及應用程式的入口網站刀鋒視窗中看到 (在 [概觀]  >  [基本資訊]，以及 [屬性] 中)。</span><span class="sxs-lookup"><span data-stu-id="ab350-219">You can see it in the app's publishing profile and in the app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="ab350-220">價格</span><span class="sxs-lookup"><span data-stu-id="ab350-220">Pricing</span></span> ##

<span data-ttu-id="ab350-221">已建立名稱為**隔離**的價格 SKU，僅供與 ASEv2 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="ab350-221">The pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="ab350-222">ASEv2 中裝載的所有 App Service 方案都位於「隔離」定價 SKU 中。</span><span class="sxs-lookup"><span data-stu-id="ab350-222">All App Service plans that are hosted in ASEv2 are in the Isolated pricing SKU.</span></span> <span data-ttu-id="ab350-223">隔離的 App Service 方案費率會因區域而有所不同。</span><span class="sxs-lookup"><span data-stu-id="ab350-223">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="ab350-224">除了 App Service 方案的價格，ASE 本身有固定費率。</span><span class="sxs-lookup"><span data-stu-id="ab350-224">In addition to the price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="ab350-225">固定費率不會隨著您的 ASE 大小而變動，而會給每 15 個 App Service 方案執行個體 1 個額外的前端，以此預設級別費率的 ASE 基礎結構來付費。</span><span class="sxs-lookup"><span data-stu-id="ab350-225">The flat rate doesn't change with the size of your ASE and pays for the ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="ab350-226">如果每 15 個 App Service 方案執行個體 1 個前端的預設級別費率不夠快，您可以調整新增前端的比率或前端的大小。</span><span class="sxs-lookup"><span data-stu-id="ab350-226">If the default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust the ratio at which front-ends are added or the size of the front-ends.</span></span>  <span data-ttu-id="ab350-227">當您調整比率或大小時，需要為預設時未加入的前端核心付費。</span><span class="sxs-lookup"><span data-stu-id="ab350-227">When you adjust the ratio or size, you pay for the front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="ab350-228">例如，如果您將級別比率調整為 10，系統就會針對 App Service 方案中每 10 個執行個體新增一個前端。</span><span class="sxs-lookup"><span data-stu-id="ab350-228">For example, if you adjust the scale ratio to 10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="ab350-229">固定費用涵蓋每隔 15 個執行個體 1 個前端的級別費率。</span><span class="sxs-lookup"><span data-stu-id="ab350-229">The flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="ab350-230">使用 10 級別比率時，您必須支付針對 10 個 App Service 方案執行個體新增的第三個前端費用。</span><span class="sxs-lookup"><span data-stu-id="ab350-230">With a scale ratio of 10, you pay a fee for the third front end that's added for the 10 App Service plan instances.</span></span> <span data-ttu-id="ab350-231">在您達到 15 個執行個體時，不需要付費，因為它是自動新增的。</span><span class="sxs-lookup"><span data-stu-id="ab350-231">You don't need to pay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="ab350-232">如果您將前端大小調整為 2 個核心，但不調整比率，則您需支付額外核心的費用。</span><span class="sxs-lookup"><span data-stu-id="ab350-232">If you adjusted the size of the front-ends to 2 cores but do not adjust the ratio then you pay for the extra cores.</span></span>  <span data-ttu-id="ab350-233">ASE 已建立 2 個前端，所以即使低於自動調整閾值，如果大小增加到 2 個核心前端，您需支付 2 個額外核心的費用。</span><span class="sxs-lookup"><span data-stu-id="ab350-233">An ASE is created with 2 front-ends, so even below the automatic scaling threshold you would pay for 2 extra cores if you increased the size to 2 core front-ends.</span></span>

<span data-ttu-id="ab350-234">如需詳細資訊，請參閱 [Azure App Service 價格][Pricing]。</span><span class="sxs-lookup"><span data-stu-id="ab350-234">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="ab350-235">刪除 ASE</span><span class="sxs-lookup"><span data-stu-id="ab350-235">Delete an ASE</span></span> ##

<span data-ttu-id="ab350-236">若要刪除 ASE：</span><span class="sxs-lookup"><span data-stu-id="ab350-236">To delete an ASE:</span></span> 

1. <span data-ttu-id="ab350-237">請使用 [App Service Environment] 刀鋒視窗頂端的 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ab350-237">Use **Delete** at the top of the **App Service Environment** blade.</span></span> 

2. <span data-ttu-id="ab350-238">輸入 ASE 的名稱以確認您想要將它刪除。</span><span class="sxs-lookup"><span data-stu-id="ab350-238">Enter the name of your ASE to confirm that you want to delete it.</span></span> <span data-ttu-id="ab350-239">當您刪除 ASE 時，將同時刪除其中包含的所有內容。</span><span class="sxs-lookup"><span data-stu-id="ab350-239">When you delete an ASE, you delete all of the content within it as well.</span></span> 

    ![ASE 刪除][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
