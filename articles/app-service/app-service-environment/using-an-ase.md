---
title: "aaaUse Azure App Service 環境"
description: "如何發佈 toocreate，，和在 Azure App Service 環境調整應用程式"
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
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="ce23a-103">使用 App Service Environment</span><span class="sxs-lookup"><span data-stu-id="ce23a-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="ce23a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ce23a-104">Overview</span></span> ##

<span data-ttu-id="ce23a-105">Azure App Service Environment (ASE) 是 Azure App Service 到客戶之 Azure 虛擬網路中子網路的部署。</span><span class="sxs-lookup"><span data-stu-id="ce23a-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="ce23a-106">其中包括：</span><span class="sxs-lookup"><span data-stu-id="ce23a-106">It consists of:</span></span>

- <span data-ttu-id="ce23a-107">**前端結束**: hello 前端是 HTTP/HTTPS 終止的 App Service 環境 (ASE) 中的位置。</span><span class="sxs-lookup"><span data-stu-id="ce23a-107">**Front ends**: hello front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="ce23a-108">**工作者**: hello 背景工作可以裝載應用程式的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="ce23a-108">**Workers**: hello workers are hello resources that host your apps.</span></span>
- <span data-ttu-id="ce23a-109">**資料庫**: hello 資料庫會保留定義 hello 環境的資訊。</span><span class="sxs-lookup"><span data-stu-id="ce23a-109">**Database**: hello database holds information that defines hello environment.</span></span>
- <span data-ttu-id="ce23a-110">**儲存體**: hello 儲存體就是使用的 toohost hello 客戶發行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce23a-110">**Storage**: hello storage is used toohost hello customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="ce23a-111">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="ce23a-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="ce23a-112">中 ASEv1，您必須管理 hello 資源，才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="ce23a-112">In ASEv1, you must manage hello resources before you can use them.</span></span> <span data-ttu-id="ce23a-113">toolearn 如何 tooconfigure 和管理 ASEv1，請參閱[設定 App Service 環境 v1][ConfigureASEv1]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-113">toolearn how tooconfigure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="ce23a-114">hello 本文其餘部分著重於 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="ce23a-114">hello rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="ce23a-115">您可以使用適用於應用程式存取的外部 VIP 或內部 VIP，來部署 ASE (ASEv1 和 ASEv2)。</span><span class="sxs-lookup"><span data-stu-id="ce23a-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="ce23a-116">hello 與外部 VIP 的部署通常稱為外部 ase。</span><span class="sxs-lookup"><span data-stu-id="ce23a-116">hello deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="ce23a-117">因為它會使用內部負載平衡器 (ILB)，會呼叫 hello ILB ASE hello 內部版本。</span><span class="sxs-lookup"><span data-stu-id="ce23a-117">hello internal version is called hello ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="ce23a-118">請參閱深入了解 hello ILB ASE toolearn[建立並使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-118">toolearn more about hello ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="ce23a-119">在 ASE 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ce23a-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="ce23a-120">toocreate 在 ase 中的 web 應用程式，您使用的 hello 相同的處理序，做為您建立時就一般來說，但有一些小差異。</span><span class="sxs-lookup"><span data-stu-id="ce23a-120">toocreate a web app in an ASE, you use hello same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="ce23a-121">當您建立新的 App Service 方案時：</span><span class="sxs-lookup"><span data-stu-id="ce23a-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="ce23a-122">而不是選擇的地理位置在哪一個 toodeploy 您的應用程式，您可以選擇 ase 中做為位置。</span><span class="sxs-lookup"><span data-stu-id="ce23a-122">Instead of choosing a geographic location in which toodeploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="ce23a-123">在 ASE 中建立的所有 App Service 方案必須在「隔離」定價層中。</span><span class="sxs-lookup"><span data-stu-id="ce23a-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="ce23a-124">如果您沒有 ase 中，您可以建立一個遵照中的 hello[建立 App Service 環境][MakeExternalASE]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-124">If you don't have an ASE, you can create one by following hello instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="ce23a-125">toocreate web 應用程式在 ase 中：</span><span class="sxs-lookup"><span data-stu-id="ce23a-125">toocreate a web app in an ASE:</span></span>

1. <span data-ttu-id="ce23a-126">選取 [新增] > [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-126">Select **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="ce23a-127">輸入 hello web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ce23a-127">Enter a name for hello web app.</span></span> <span data-ttu-id="ce23a-128">如果您已經在 ase 中選取的應用程式服務計劃，hello hello 應用程式的網域名稱會反映 hello ASE hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ce23a-128">If you already selected an App Service plan in an ASE, hello domain name for hello app reflects hello domain name of hello ASE.</span></span>

    ![選取 Web 應用程式名稱][1]

3. <span data-ttu-id="ce23a-130">選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce23a-130">Select a subscription.</span></span>

4. <span data-ttu-id="ce23a-131">輸入新的資源群組的名稱，或選取**使用現有**和從 hello 下拉式清單中選取一個。</span><span class="sxs-lookup"><span data-stu-id="ce23a-131">Enter a name for a new resource group, or select **Use existing** and select one from hello drop-down list.</span></span>

5. <span data-ttu-id="ce23a-132">選取 ASE 中現有的 App Service 方案，或透過下列步驟建立一個新的方案：</span><span class="sxs-lookup"><span data-stu-id="ce23a-132">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="ce23a-133">a.</span><span class="sxs-lookup"><span data-stu-id="ce23a-133">a.</span></span> <span data-ttu-id="ce23a-134">選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-134">Select **Create New**.</span></span>

    <span data-ttu-id="ce23a-135">b.</span><span class="sxs-lookup"><span data-stu-id="ce23a-135">b.</span></span> <span data-ttu-id="ce23a-136">輸入您 App Service 方案的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ce23a-136">Enter hello name for your App Service plan.</span></span>

    <span data-ttu-id="ce23a-137">c.</span><span class="sxs-lookup"><span data-stu-id="ce23a-137">c.</span></span> <span data-ttu-id="ce23a-138">選取您 ASE 中 hello**位置**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ce23a-138">Select your ASE in hello **Location** drop-down list.</span></span>

    <span data-ttu-id="ce23a-139">d.</span><span class="sxs-lookup"><span data-stu-id="ce23a-139">d.</span></span> <span data-ttu-id="ce23a-140">選取 [隔離] 定價層。</span><span class="sxs-lookup"><span data-stu-id="ce23a-140">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="ce23a-141">選取 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="ce23a-141">Select **Select**.</span></span>

    <span data-ttu-id="ce23a-142">e.</span><span class="sxs-lookup"><span data-stu-id="ce23a-142">e.</span></span> <span data-ttu-id="ce23a-143">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ce23a-143">Select **OK**.</span></span>
    
    ![隔離定價層][2]

6. <span data-ttu-id="ce23a-145">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-145">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="ce23a-146">調整方式</span><span class="sxs-lookup"><span data-stu-id="ce23a-146">How scale works</span></span> ##

<span data-ttu-id="ce23a-147">每個 App Service 應用程式都會在 App Service 方案中執行。</span><span class="sxs-lookup"><span data-stu-id="ce23a-147">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="ce23a-148">hello 容器模型是環境保存應用程式服務方案和應用程式服務方案保留應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce23a-148">hello container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="ce23a-149">當您調整應用程式時，您和調整其規模 hello 應用程式服務計劃因此縮放 hello hello 的所有應用程式相同的計劃。</span><span class="sxs-lookup"><span data-stu-id="ce23a-149">When you scale an app, you scale hello App Service plan and thus scale all hello apps in hello same plan.</span></span>

<span data-ttu-id="ce23a-150">在 ASEv2，當您調整 App Service 方案，也會自動加入 hello 所需的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ce23a-150">In ASEv2, when you scale an App Service plan, hello needed infrastructure is automatically added.</span></span> <span data-ttu-id="ce23a-151">沒有時間延遲 tooscale 作業時就會加入 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ce23a-151">There is a time delay tooscale operations while hello infrastructure is added.</span></span> <span data-ttu-id="ce23a-152">ASEv1，hello 所需的基礎結構必須加入您才能建立或擴充您的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="ce23a-152">In ASEv1, hello needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="ce23a-153">在 hello 多租用戶應用程式服務，縮放比例是立即通常因為資源集區是隨時可用 toosupport 它。</span><span class="sxs-lookup"><span data-stu-id="ce23a-153">In hello multitenant App Service, scaling is usually immediate because a pool of resources is readily available toosupport it.</span></span> <span data-ttu-id="ce23a-154">ASE 中沒有這類緩衝區，並在需要時配置資源。</span><span class="sxs-lookup"><span data-stu-id="ce23a-154">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="ce23a-155">在 ase 中，您可以調整 too100 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ce23a-155">In an ASE, you can scale up too100 instances.</span></span> <span data-ttu-id="ce23a-156">這 100 個執行個體可以全都位於單一 App Service 方案中，或分散於多個 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ce23a-156">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="ce23a-157">IP 位址</span><span class="sxs-lookup"><span data-stu-id="ce23a-157">IP addresses</span></span> ##

<span data-ttu-id="ce23a-158">App Service 必須 hello 能力 tooallocate 專用的 IP 位址 tooan 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce23a-158">App Service has hello ability tooallocate a dedicated IP address tooan app.</span></span> <span data-ttu-id="ce23a-159">這項功能可設定以 IP 為主的 SSL 之後, 中所述[繫結現有自訂 SSL 憑證 tooAzure web 應用程式][ConfigureSSL]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-159">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate tooAzure web apps][ConfigureSSL].</span></span> <span data-ttu-id="ce23a-160">但是，在 ASE 中，有一個明顯的例外。</span><span class="sxs-lookup"><span data-stu-id="ce23a-160">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="ce23a-161">您無法加入其他 IP 位址 toobe 用於 ILB ASE 以 IP 為主的 SSL。</span><span class="sxs-lookup"><span data-stu-id="ce23a-161">You can't add additional IP addresses toobe used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="ce23a-162">在 ASEv1，您需要 tooallocate hello IP 位址做為資源才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="ce23a-162">In ASEv1, you need tooallocate hello IP addresses as resources before you can use them.</span></span> <span data-ttu-id="ce23a-163">ASEv2，在您使用它們從您的應用程式就像您一樣 hello 多租用戶應用程式服務中。</span><span class="sxs-lookup"><span data-stu-id="ce23a-163">In ASEv2, you use them from your app just as you do in hello multitenant App Service.</span></span> <span data-ttu-id="ce23a-164">一定會有一個備用位址 ASEv2 中向上 too30 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ce23a-164">There is always one spare address in ASEv2 up too30 IP addresses.</span></span> <span data-ttu-id="ce23a-165">每次您使用一個位址時，就會新增另一個位址，如此一律會有立即可供使用的位址。</span><span class="sxs-lookup"><span data-stu-id="ce23a-165">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="ce23a-166">需要的時間延遲是 tooallocate 另一個 IP 位址，不會新增 IP 位址快速連續。</span><span class="sxs-lookup"><span data-stu-id="ce23a-166">A time delay is required tooallocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="ce23a-167">前端調整大小</span><span class="sxs-lookup"><span data-stu-id="ce23a-167">Front-end scaling</span></span> ##

<span data-ttu-id="ce23a-168">在 ASEv2，當您擴充您的應用程式服務計劃，背景工作會自動加入 toosupport 它們。</span><span class="sxs-lookup"><span data-stu-id="ce23a-168">In ASEv2, when you scale out your App Service plans, workers are automatically added toosupport them.</span></span> <span data-ttu-id="ce23a-169">每個 ASE 建立時都會包含兩個前端。</span><span class="sxs-lookup"><span data-stu-id="ce23a-169">Every ASE is created with two front ends.</span></span> <span data-ttu-id="ce23a-170">此外，hello 前端自動向外延展速率為每隔 15 的執行個體的一個前端應用程式服務方案中。</span><span class="sxs-lookup"><span data-stu-id="ce23a-170">In addition, hello front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="ce23a-171">例如，如果您有 15 個執行個體，則會有三個前端。</span><span class="sxs-lookup"><span data-stu-id="ce23a-171">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="ce23a-172">如果縮放 too30 執行個體時，您會有四個最上層結束，以此類推。</span><span class="sxs-lookup"><span data-stu-id="ce23a-172">If you scale too30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="ce23a-173">這個前端數目應該足以適用於大部分情況。</span><span class="sxs-lookup"><span data-stu-id="ce23a-173">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="ce23a-174">但是，您也可用更快的速率相應放大。</span><span class="sxs-lookup"><span data-stu-id="ce23a-174">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="ce23a-175">您可以變更為每五個執行個體的一個前端低 tooas hello 比率。</span><span class="sxs-lookup"><span data-stu-id="ce23a-175">You can change hello ratio tooas low as one front end for every five instances.</span></span> <span data-ttu-id="ce23a-176">沒有變更 hello 比例收取費用。</span><span class="sxs-lookup"><span data-stu-id="ce23a-176">There is a charge for changing hello ratio.</span></span> <span data-ttu-id="ce23a-177">如需詳細資訊，請參閱 [Azure App Service 價格][Pricing]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-177">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="ce23a-178">前端資源是 hello ASE hello HTTP/HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="ce23a-178">Front-end resources are hello HTTP/HTTPS endpoint for hello ASE.</span></span> <span data-ttu-id="ce23a-179">Hello 預設前端組態，每個前端記憶體使用量持續約為 60%。</span><span class="sxs-lookup"><span data-stu-id="ce23a-179">With hello default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="ce23a-180">客戶工作負載不會在前端上執行。</span><span class="sxs-lookup"><span data-stu-id="ce23a-180">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="ce23a-181">hello 前端與尊重 tooscale 的關鍵因素是 hello CPU 驅動主要是由 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="ce23a-181">hello key factor for a front end with respect tooscale is hello CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="ce23a-182">應用程式存取</span><span class="sxs-lookup"><span data-stu-id="ce23a-182">App access</span></span> ##

<span data-ttu-id="ce23a-183">在外部 ase 中，建立應用程式時所使用的 hello 網域與不同 hello 多租用戶應用程式服務的。</span><span class="sxs-lookup"><span data-stu-id="ce23a-183">In an External ASE, hello domain that's used when you create apps is different from hello multitenant App Service.</span></span> <span data-ttu-id="ce23a-184">它包括 hello ASE hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ce23a-184">It includes hello name of hello ASE.</span></span> <span data-ttu-id="ce23a-185">如需有關如何 toocreate 外部 ase 中，請參閱[建立 App Service 環境][MakeExternalASE]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-185">For more information on how toocreate an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="ce23a-186">hello 網域名稱，在外部 ase 中看起來像*。&lt;asename&gt;。 p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="ce23a-186">hello domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="ce23a-187">例如，如果您 ASE 名為_外部 ase_和裝載應用程式呼叫_contoso_該 ASE 中，在您連線到它在 hello 下列 Url:</span><span class="sxs-lookup"><span data-stu-id="ce23a-187">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at hello following URLs:</span></span>

- <span data-ttu-id="ce23a-188">contoso.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ce23a-188">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="ce23a-189">contoso.scm.external-ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ce23a-189">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="ce23a-190">hello URL contoso.scm.external ase.p.azurewebsites.net 使用的 tooaccess hello Kudu 主控台或使用 web 應用程式部署發行。</span><span class="sxs-lookup"><span data-stu-id="ce23a-190">hello URL contoso.scm.external-ase.p.azurewebsites.net is used tooaccess hello Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="ce23a-191">Hello Kudu 主控台上的資訊，請參閱[Azure App Service 的 Kudu 主控台][Kudu]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-191">For information on hello Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="ce23a-192">hello Kudu 主控台可讓您 web UI 的偵錯、 上傳檔案、 編輯檔案，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="ce23a-192">hello Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="ce23a-193">在 ILB ase 中，您會在部署期間判斷 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="ce23a-193">In an ILB ASE, you determine hello domain at deployment time.</span></span> <span data-ttu-id="ce23a-194">如需有關如何 toocreate ILB ASE，請參閱[建立並使用 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-194">For more information on how toocreate an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="ce23a-195">如果您指定 hello 網域名稱_ilb ase.info_，hello 應用程式，ASE 應用程式建立期間可以使用該網域。</span><span class="sxs-lookup"><span data-stu-id="ce23a-195">If you specify hello domain name _ilb-ase.info_, hello apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="ce23a-196">Hello 應用程式名為_contoso_，hello url:</span><span class="sxs-lookup"><span data-stu-id="ce23a-196">For hello app named _contoso_, hello URLs are:</span></span>

- <span data-ttu-id="ce23a-197">contoso.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="ce23a-197">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="ce23a-198">contoso.scm.ilb-ase.info</span><span class="sxs-lookup"><span data-stu-id="ce23a-198">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="ce23a-199">發佈</span><span class="sxs-lookup"><span data-stu-id="ce23a-199">Publishing</span></span> ##

<span data-ttu-id="ce23a-200">如同 hello 多租用戶應用程式服務，在 ase 中您可以將發行使用：</span><span class="sxs-lookup"><span data-stu-id="ce23a-200">As with hello multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="ce23a-201">Web 部署。</span><span class="sxs-lookup"><span data-stu-id="ce23a-201">Web deployment.</span></span>
- <span data-ttu-id="ce23a-202">FTP。</span><span class="sxs-lookup"><span data-stu-id="ce23a-202">FTP.</span></span>
- <span data-ttu-id="ce23a-203">持續整合。</span><span class="sxs-lookup"><span data-stu-id="ce23a-203">Continuous integration.</span></span>
- <span data-ttu-id="ce23a-204">拖放在 hello Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="ce23a-204">Drag and drop in hello Kudu console.</span></span>
- <span data-ttu-id="ce23a-205">IDE，例如 Visual Studio、Eclipse 或 IntelliJ IDEA。</span><span class="sxs-lookup"><span data-stu-id="ce23a-205">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="ce23a-206">與外部 ase 中，這些行為的發行選項 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="ce23a-206">With an External ASE, these publishing options all behave hello same.</span></span> <span data-ttu-id="ce23a-207">如需詳細資訊，請參閱[在 Azure App Service 中部署][AppDeploy]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-207">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="ce23a-208">hello 與發行的主要差異是尊重 tooan ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="ce23a-208">hello major difference with publishing is with respect tooan ILB ASE.</span></span> <span data-ttu-id="ce23a-209">ILB ase 中，與 hello 發行端點則是只能透過 hello ILB 所有可用項目。</span><span class="sxs-lookup"><span data-stu-id="ce23a-209">With an ILB ASE, hello publishing endpoints are all available only through hello ILB.</span></span> <span data-ttu-id="ce23a-210">hello ILB 會位於 hello 虛擬網路中的 hello ASE 子網路中的私人 IP。</span><span class="sxs-lookup"><span data-stu-id="ce23a-210">hello ILB is on a private IP in hello ASE subnet in hello virtual network.</span></span> <span data-ttu-id="ce23a-211">如果您沒有網路存取 toohello ILB，您無法發行該 ASE 上的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce23a-211">If you don’t have network access toohello ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="ce23a-212">如中所述[建立並使用 ILB ASE][MakeILBASE]，hello 應用程式需要 tooconfigure DNS hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="ce23a-212">As noted in [Create and use an ILB ASE][MakeILBASE], you need tooconfigure DNS for hello apps in hello system.</span></span> <span data-ttu-id="ce23a-213">其中包含 hello SCM 端點。</span><span class="sxs-lookup"><span data-stu-id="ce23a-213">That includes hello SCM endpoint.</span></span> <span data-ttu-id="ce23a-214">如果未正確定義它們，就無法發佈。</span><span class="sxs-lookup"><span data-stu-id="ce23a-214">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="ce23a-215">您的 Ide 也需要 toohave 網路存取 toohello ILB 順序 toopublish 中的直接 tooit。</span><span class="sxs-lookup"><span data-stu-id="ce23a-215">Your IDEs also need toohave network access toohello ILB in order toopublish directly tooit.</span></span>

<span data-ttu-id="ce23a-216">以網際網路為基礎 CI 系統，例如 GitHub 和 Visual Studio Team Services，不使用 ILB ASE 因為 hello 發行端點不是可存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="ce23a-216">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="ce23a-217">相反地，您需要 toouse 使用提取模型，例如 Dropbox 的 CI 系統。</span><span class="sxs-lookup"><span data-stu-id="ce23a-217">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="ce23a-218">hello ILB ASE 中的應用程式的發行端點會使用 ILB ASE 建立與該 hello hello 網域。</span><span class="sxs-lookup"><span data-stu-id="ce23a-218">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="ce23a-219">您可以在 hello 應用程式發行設定檔和 hello 應用程式的入口網站的刀鋒視窗中看到它 (在**概觀** > **Essentials**同時也位於**屬性**)。</span><span class="sxs-lookup"><span data-stu-id="ce23a-219">You can see it in hello app's publishing profile and in hello app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="ce23a-220">價格</span><span class="sxs-lookup"><span data-stu-id="ce23a-220">Pricing</span></span> ##

<span data-ttu-id="ce23a-221">定價 SKU 呼叫 hello**隔離**建立 ASEv2 只能搭配使用。</span><span class="sxs-lookup"><span data-stu-id="ce23a-221">hello pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="ce23a-222">所有裝載於 ASEv2 的應用程式服務計劃已 hello 定價 SKU 的隔離。</span><span class="sxs-lookup"><span data-stu-id="ce23a-222">All App Service plans that are hosted in ASEv2 are in hello Isolated pricing SKU.</span></span> <span data-ttu-id="ce23a-223">隔離的 App Service 方案費率會因區域而有所不同。</span><span class="sxs-lookup"><span data-stu-id="ce23a-223">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="ce23a-224">此外 toohello 價格為您的應用程式服務計劃，ASE 本身一般速率。</span><span class="sxs-lookup"><span data-stu-id="ce23a-224">In addition toohello price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="ce23a-225">hello 一般速率不會變更您 ASE hello 大小及支付 hello ASE 基礎結構在調整率 1 其他預設值的前端每隔 15 的 App Service 方案執行個體。</span><span class="sxs-lookup"><span data-stu-id="ce23a-225">hello flat rate doesn't change with hello size of your ASE and pays for hello ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="ce23a-226">如果 hello 預設小數位數率 1 前端每隔 15 的 App Service 方案執行個體不是速度不夠快，您可以調整 hello 比率前端加入或是 hello hello 前端的大小。</span><span class="sxs-lookup"><span data-stu-id="ce23a-226">If hello default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust hello ratio at which front-ends are added or hello size of hello front-ends.</span></span>  <span data-ttu-id="ce23a-227">當您調整 hello 比例或大小時，您需支付不會加入預設的 hello 前端核心。</span><span class="sxs-lookup"><span data-stu-id="ce23a-227">When you adjust hello ratio or size, you pay for hello front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="ce23a-228">例如，如果您調整 hello 小數位數的比率 too10，前端會加入每 10 個執行個體的 App Service 方案中。</span><span class="sxs-lookup"><span data-stu-id="ce23a-228">For example, if you adjust hello scale ratio too10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="ce23a-229">hello 一般費用涵蓋一個前端每隔 15 的執行個體的小數位數速率。</span><span class="sxs-lookup"><span data-stu-id="ce23a-229">hello flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="ce23a-230">小數位數的比率較 10，您需支付費用 hello 第三個前端加入 hello 10 App Service 方案執行個體。</span><span class="sxs-lookup"><span data-stu-id="ce23a-230">With a scale ratio of 10, you pay a fee for hello third front end that's added for hello 10 App Service plan instances.</span></span> <span data-ttu-id="ce23a-231">您無須 toopay，當您到達 15 的執行個體，因為它已自動加入。</span><span class="sxs-lookup"><span data-stu-id="ce23a-231">You don't need toopay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="ce23a-232">如果您已調整的 hello 前端 too2 核心 hello 大小，但不是會調整 hello 比率則您需支付 hello 額外的核心。</span><span class="sxs-lookup"><span data-stu-id="ce23a-232">If you adjusted hello size of hello front-ends too2 cores but do not adjust hello ratio then you pay for hello extra cores.</span></span>  <span data-ttu-id="ce23a-233">2 前端，所以即使 hello 自動調整臨界值以下您願意支付額外的 2 核心如果增加 hello 大小 too2 核心前端建立 ase。</span><span class="sxs-lookup"><span data-stu-id="ce23a-233">An ASE is created with 2 front-ends, so even below hello automatic scaling threshold you would pay for 2 extra cores if you increased hello size too2 core front-ends.</span></span>

<span data-ttu-id="ce23a-234">如需詳細資訊，請參閱 [Azure App Service 價格][Pricing]。</span><span class="sxs-lookup"><span data-stu-id="ce23a-234">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="ce23a-235">刪除 ASE</span><span class="sxs-lookup"><span data-stu-id="ce23a-235">Delete an ASE</span></span> ##

<span data-ttu-id="ce23a-236">toodelete ase 中：</span><span class="sxs-lookup"><span data-stu-id="ce23a-236">toodelete an ASE:</span></span> 

1. <span data-ttu-id="ce23a-237">使用**刪除**頂端的 hello hello **App Service 環境**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ce23a-237">Use **Delete** at hello top of hello **App Service Environment** blade.</span></span> 

2. <span data-ttu-id="ce23a-238">輸入您想 toodelete 您 ASE tooconfirm hello 名稱它。</span><span class="sxs-lookup"><span data-stu-id="ce23a-238">Enter hello name of your ASE tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="ce23a-239">當您刪除 ase 中時，會刪除所有的 hello 內容以及。</span><span class="sxs-lookup"><span data-stu-id="ce23a-239">When you delete an ASE, you delete all of hello content within it as well.</span></span> 

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
