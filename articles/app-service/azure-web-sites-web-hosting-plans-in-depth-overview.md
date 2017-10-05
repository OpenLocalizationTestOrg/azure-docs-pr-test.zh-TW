---
title: "Azure App Service 方案深入概觀 | Microsoft Docs"
description: "了解 Azure App Service 之應用程式服務方案的運作方式，以及在管理經驗上帶來的效益。"
keywords: "App Service, Azure App Service, 級別, 可調整, App Service方案, App Service 成本"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="da4ba-104">Azure App Service 方案深入概觀</span><span class="sxs-lookup"><span data-stu-id="da4ba-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="da4ba-105">App Service 方案代表用來裝載應用程式的實體資源集合。</span><span class="sxs-lookup"><span data-stu-id="da4ba-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="da4ba-106">App Service 方案可定義：</span><span class="sxs-lookup"><span data-stu-id="da4ba-106">App Service plans define:</span></span>

- <span data-ttu-id="da4ba-107">區域 (美國西部、美國東部等)</span><span class="sxs-lookup"><span data-stu-id="da4ba-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="da4ba-108">級別計數 (一、二、三個執行個體等)</span><span class="sxs-lookup"><span data-stu-id="da4ba-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="da4ba-109">執行個體大小 (小型、中型、大型)</span><span class="sxs-lookup"><span data-stu-id="da4ba-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="da4ba-110">SKU (免費、共用、基本、標準、進階)</span><span class="sxs-lookup"><span data-stu-id="da4ba-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="da4ba-111">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 中的 Web Apps、Mobile Apps、Function Apps (或 Functions) 全部都在 App Service 方案中執行。</span><span class="sxs-lookup"><span data-stu-id="da4ba-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="da4ba-112">相同訂用帳戶及區域中的應用程式可以共用 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="da4ba-113">所有指派給 **App Service 方案**的應用程式都會共用其所定義的資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="da4ba-114">這可讓您在單一 App Service 方案中託管多個應用程式時，能夠節省成本。</span><span class="sxs-lookup"><span data-stu-id="da4ba-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="da4ba-115">**App Service 方案**可以從 [免費] 和 [共用] SKU 調整為 [基本]、[標準] 和 [進階] SKU，以便存取更多資源和功能。</span><span class="sxs-lookup"><span data-stu-id="da4ba-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="da4ba-116">如果 App Service 方案設為 [基本] 或更高的 SKU，則您可以控制 VM 的**大小**和級別計數。</span><span class="sxs-lookup"><span data-stu-id="da4ba-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="da4ba-117">比方說，如果您的方案設定為使用標準服務層中的兩個「小型」執行個體，則與該方案相關聯的所有應用程式會在兩個執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="da4ba-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="da4ba-118">應用程式也可以存取標準服務層功能。</span><span class="sxs-lookup"><span data-stu-id="da4ba-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="da4ba-119">應用程式在其上執行的方案執行個體完全受管理且高度可用。</span><span class="sxs-lookup"><span data-stu-id="da4ba-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da4ba-120">App Service 方案的 **SKU** 和**級別**可決定成本，而不是其中裝載的應用程式數目。</span><span class="sxs-lookup"><span data-stu-id="da4ba-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="da4ba-121">本文探討重要的特性，例如 App Service 方案的層級與規模，以及這些特性如何在管理您的應用程式時發揮效用。</span><span class="sxs-lookup"><span data-stu-id="da4ba-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="da4ba-122">應用程式和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="da4ba-122">Apps and App Service plans</span></span>

<span data-ttu-id="da4ba-123">在任何指定時間，應用程式服務方案中的一個應用程式只能與一個應用程式服務方案產生關聯。</span><span class="sxs-lookup"><span data-stu-id="da4ba-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="da4ba-124">應用程式和方案都包含在**資源群組**中。</span><span class="sxs-lookup"><span data-stu-id="da4ba-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="da4ba-125">資源群組可做為其內各項資源的生命週期界限。</span><span class="sxs-lookup"><span data-stu-id="da4ba-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="da4ba-126">您可以使用資源群組集中管理應用程式的一切層面。</span><span class="sxs-lookup"><span data-stu-id="da4ba-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="da4ba-127">單一資源群組可擁有多個 App Service 方案，因此您可以將不同的應用程式配置到不同的實際資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="da4ba-128">例如，您可以將資源分隔為開發、測試和生產環境。</span><span class="sxs-lookup"><span data-stu-id="da4ba-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="da4ba-129">將生產和開發/測試的環境分開可讓您隔離資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="da4ba-130">如此一來，對您應用程式的新版本進行負載測試就不會與您的生產應用程式競爭相同的資源，生產應用程式是為真實的客戶提供服務。</span><span class="sxs-lookup"><span data-stu-id="da4ba-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="da4ba-131">當您在單一資源群組中有多個方案時，您也可以定義一個跨越地理區域的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="da4ba-132">例如，在兩個區域中執行的高度可用應用程式包括至少兩個方案，每個區域一個方案，而一個應用程式則與每個方案相關聯。</span><span class="sxs-lookup"><span data-stu-id="da4ba-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="da4ba-133">在這種情況下，應用程式的所有複本都在單一資源群組內。</span><span class="sxs-lookup"><span data-stu-id="da4ba-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="da4ba-134">將多個方案和多個應用程式放在一個資源群組中，可輕鬆管理、控制和檢視應用程式的健康情況。</span><span class="sxs-lookup"><span data-stu-id="da4ba-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="da4ba-135">建立 App Service 方案或使用現有的方案</span><span class="sxs-lookup"><span data-stu-id="da4ba-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="da4ba-136">在建立應用程式時，請考慮建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="da4ba-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="da4ba-137">另一方面，如果此應用程式是較大應用程式的元件，請在配置給該較大應用程式的資源群組內建立此應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="da4ba-138">不論應用程式是全新的應用程式，還是較大應用程式的一部分，您都可以選擇使用現有的方案來裝載它，或建立新的方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="da4ba-139">這項決定其實是容量和預期負載方面的問題。</span><span class="sxs-lookup"><span data-stu-id="da4ba-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="da4ba-140">如果有下列情況，建議將您的應用程式隔離至新的 App Service 方案中：</span><span class="sxs-lookup"><span data-stu-id="da4ba-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="da4ba-141">應用程式會耗用大量資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-141">App is resource-intensive.</span></span>
- <span data-ttu-id="da4ba-142">應用程式的縮放係數不同於現有方案中裝載的其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="da4ba-143">應用程式需要不同地理區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="da4ba-144">這樣可讓您為應用程式配置一組新的資源，更充分掌控您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="da4ba-145">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="da4ba-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="da4ba-146">如果您有 App Service 環境，您可以檢閱這裡的 App Service 環境相關文件︰[在 App Service 環境中建立 App Service 方案](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="da4ba-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="da4ba-147">您可以從 App Service 方案瀏覽體驗或在應用程式建立期間，建立空白的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="da4ba-148">在 [Azure 入口網站](https://portal.azure.com)中，按一下 **[新增]** > **[Web + 行動]**，然後選取 **[Web 應用程式]** 或其他 App Service 應用程式種類。</span><span class="sxs-lookup"><span data-stu-id="da4ba-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![在 Azure 入口網站中建立應用程式。][createWebApp]

<span data-ttu-id="da4ba-150">接著，您可以選取或建立新應用程式的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-150">You can then select or create the App Service plan for the new app.</span></span>

 ![建立 App Service 方案。][createASP]

<span data-ttu-id="da4ba-152">若要建立 App Service 方案，請按一下 [[+] 建立新的]，輸入 [App Service 方案] 名稱，然後選取適當 [位置]。</span><span class="sxs-lookup"><span data-stu-id="da4ba-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="da4ba-153">按一下 [定價層] ，然後為服務選取適當的定價層。</span><span class="sxs-lookup"><span data-stu-id="da4ba-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="da4ba-154">選取 [檢視全部] 以檢視其他價格選項，例如 [免費] 和 [共用]。</span><span class="sxs-lookup"><span data-stu-id="da4ba-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="da4ba-155">選取定價層後，請按一下 [選取]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="da4ba-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="da4ba-156">將應用程式移到不同的應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="da4ba-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="da4ba-157">您可以在 [Azure 入口網站](https://portal.azure.com)中將應用程式移至不同的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="da4ba-158">只要方案都位於相同的資源群組與地理區域中，您就可以在這些方案之間移動應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="da4ba-159">若要將應用程式移到另一個方案︰</span><span class="sxs-lookup"><span data-stu-id="da4ba-159">To move an app to another plan:</span></span>

- <span data-ttu-id="da4ba-160">瀏覽至您想要移動的應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="da4ba-161">在 [功能表] 中，尋找 [App Service 方案]區段。</span><span class="sxs-lookup"><span data-stu-id="da4ba-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="da4ba-162">選取 [變更 App Service 方案]，以啟動程序。</span><span class="sxs-lookup"><span data-stu-id="da4ba-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="da4ba-163">[變更 App Service 方案] 會開啟 [App Service 方案] 選取器。</span><span class="sxs-lookup"><span data-stu-id="da4ba-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="da4ba-164">此時，您可以挑選要將此應用程式移往的現有方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da4ba-165">選取的 App Service 方案 UI 會依下列準則進行篩選：</span><span class="sxs-lookup"><span data-stu-id="da4ba-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="da4ba-166">存在相同的資源群組內</span><span class="sxs-lookup"><span data-stu-id="da4ba-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="da4ba-167">存在相同的地理區域內</span><span class="sxs-lookup"><span data-stu-id="da4ba-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="da4ba-168">存在相同的網路空間內</span><span class="sxs-lookup"><span data-stu-id="da4ba-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="da4ba-169">網路空間是 App Service 內的邏輯結構，會定義伺服器資源的群組。</span><span class="sxs-lookup"><span data-stu-id="da4ba-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="da4ba-170">地理區域 (例如美國西部) 包含許多網路空間，可配置使用 App Service 的客戶。</span><span class="sxs-lookup"><span data-stu-id="da4ba-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="da4ba-171">目前，App Service 資源無法在網路空間之間移動。</span><span class="sxs-lookup"><span data-stu-id="da4ba-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![App Service 方案選取器。][change]

<span data-ttu-id="da4ba-173">每個方案都有其專屬定價層。</span><span class="sxs-lookup"><span data-stu-id="da4ba-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="da4ba-174">比方說，如果將網站從免費層移至標準層，則所有指派給它的應用程式可以使用標準層的所有功能和資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="da4ba-175">將應用程式移到不同的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="da4ba-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="da4ba-176">如果您想要將應用程式移至不同的區域，有一個替代方法是複製應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="da4ba-177">複製會在任何區域中的新或現有 App Service 方案中產生您應用程式的複本。</span><span class="sxs-lookup"><span data-stu-id="da4ba-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="da4ba-178">您可以在功能表的 [開發工具] 區段中找到 [複製應用程式]。</span><span class="sxs-lookup"><span data-stu-id="da4ba-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da4ba-179">複製具有某些限制，若要深入了解，請閱讀 [使用 Azure 入口網站的 Azure App Service 應用程式複製](../app-service-web/app-service-web-app-cloning-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="da4ba-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="da4ba-180">調整 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="da4ba-180">Scale an App Service plan</span></span>

<span data-ttu-id="da4ba-181">有三種方式可以調整方案：</span><span class="sxs-lookup"><span data-stu-id="da4ba-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="da4ba-182">**變更方案的定價層**。</span><span class="sxs-lookup"><span data-stu-id="da4ba-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="da4ba-183">基本層的方案可以轉換成「標準」，所有指派給它的應用程式將使用標準層的功能。</span><span class="sxs-lookup"><span data-stu-id="da4ba-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="da4ba-184">**變更方案的執行個體大小**。</span><span class="sxs-lookup"><span data-stu-id="da4ba-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="da4ba-185">例如，基本層中使用小型執行個體的方案可以變更為使用大型執行個體。</span><span class="sxs-lookup"><span data-stu-id="da4ba-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="da4ba-186">與該方案相關聯的所有應用程式現在都可以使用較大執行個體大小所提供的額外記憶體和 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="da4ba-187">**變更方案的執行個體計數**。</span><span class="sxs-lookup"><span data-stu-id="da4ba-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="da4ba-188">例如，已相應放大為 3 個執行個體的標準方案可調整為 10 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="da4ba-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="da4ba-189">進階方案可以相應放大為 20 個執行個體 (視實際情況而定)。</span><span class="sxs-lookup"><span data-stu-id="da4ba-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="da4ba-190">與該方案相關聯的所有應用程式現在都可以使用較大執行個體計數所提供的額外記憶體和 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="da4ba-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="da4ba-191">您可以按一下應用程式或 App Service 方案設定下方的 [相應增加]  項目，來變更定價層和執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="da4ba-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="da4ba-192">變更會套用到 App Service 方案，並影響它裝載的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="da4ba-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![設定值以相應增加應用程式。][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="da4ba-194">App Service 方案清除</span><span class="sxs-lookup"><span data-stu-id="da4ba-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da4ba-195">沒有相關聯應用程式的 **App Service 方案**仍會產生費用，因為它們會繼續保留計算容量。</span><span class="sxs-lookup"><span data-stu-id="da4ba-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="da4ba-196">為了避免非預期的費用，刪除 App Service 方案中裝載的最後一個應用程式時，也會刪除產生的空白 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="da4ba-197">摘要</span><span class="sxs-lookup"><span data-stu-id="da4ba-197">Summary</span></span>

<span data-ttu-id="da4ba-198">應用程式服務方案代表可跨應用程式共用的一組特性和功能。</span><span class="sxs-lookup"><span data-stu-id="da4ba-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="da4ba-199">App Service 方案可讓您將特定應用程式彈性地配置給一組資源，並進一步最佳化 Azure 資源使用率。</span><span class="sxs-lookup"><span data-stu-id="da4ba-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="da4ba-200">如此一來，如果您想要節省測試環境的成本，則可以跨多個應用程式共用方案。</span><span class="sxs-lookup"><span data-stu-id="da4ba-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="da4ba-201">透過延展到多個區域和方案，也可以最大化生產環境的輸送量。</span><span class="sxs-lookup"><span data-stu-id="da4ba-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="da4ba-202">變更的項目</span><span class="sxs-lookup"><span data-stu-id="da4ba-202">What's changed</span></span>

- <span data-ttu-id="da4ba-203">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="da4ba-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
