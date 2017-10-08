---
title: "aaaAzure App Service 方案深入概觀 |Microsoft 文件"
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
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="c2df2-104">Azure App Service 方案深入概觀</span><span class="sxs-lookup"><span data-stu-id="c2df2-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="c2df2-105">應用程式服務計劃代表 hello 集合，其使用的實體資源 toohost 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="c2df2-106">App Service 方案可定義：</span><span class="sxs-lookup"><span data-stu-id="c2df2-106">App Service plans define:</span></span>

- <span data-ttu-id="c2df2-107">區域 (美國西部、美國東部等)</span><span class="sxs-lookup"><span data-stu-id="c2df2-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="c2df2-108">級別計數 (一、二、三個執行個體等)</span><span class="sxs-lookup"><span data-stu-id="c2df2-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="c2df2-109">執行個體大小 (小型、中型、大型)</span><span class="sxs-lookup"><span data-stu-id="c2df2-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="c2df2-110">SKU (免費、共用、基本、標準、進階)</span><span class="sxs-lookup"><span data-stu-id="c2df2-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="c2df2-111">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 中的 Web Apps、Mobile Apps、Function Apps (或 Functions) 全部都在 App Service 方案中執行。</span><span class="sxs-lookup"><span data-stu-id="c2df2-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="c2df2-112">應用程式在 hello 相同的地區和訂用帳戶，可以共用 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="c2df2-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="c2df2-113">所有應用程式指派 tooan **App Service 方案**共用 hello 它所定義的資源。</span><span class="sxs-lookup"><span data-stu-id="c2df2-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="c2df2-114">這可讓您在單一 App Service 方案中託管多個應用程式時，能夠節省成本。</span><span class="sxs-lookup"><span data-stu-id="c2df2-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="c2df2-115">您**App Service 方案**範圍，小從**免費**和**共用**Sku 太**基本**，**標準**，和**Premium** Sku 讓您存取 toomore 資源和沿著 hello 功能的方式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="c2df2-116">如果您的應用程式服務方案設定太**基本**SKU 或更高版本，則您可以控制 hello**大小**和調整 hello Vm 的計數。</span><span class="sxs-lookup"><span data-stu-id="c2df2-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="c2df2-117">比方說，如果您計劃設定的 toouse 兩 hello standard 服務層中的 「 小型 」 執行個體，與該方案有關聯的所有應用程式在兩個執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="c2df2-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="c2df2-118">應用程式也可以存取 toohello standard 服務層功能。</span><span class="sxs-lookup"><span data-stu-id="c2df2-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="c2df2-119">應用程式在其上執行的方案執行個體完全受管理且高度可用。</span><span class="sxs-lookup"><span data-stu-id="c2df2-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2df2-120">hello **SKU**和**標尺**的 hello 應用程式服務計劃可決定 hello 成本不 hello 數目及託管於該應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="c2df2-121">這篇文章探討 hello 主要特性，例如層和應用程式服務方案的小數位數以及它們如何進入播放時管理您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="c2df2-122">應用程式和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="c2df2-122">Apps and App Service plans</span></span>

<span data-ttu-id="c2df2-123">在任何指定時間，應用程式服務方案中的一個應用程式只能與一個應用程式服務方案產生關聯。</span><span class="sxs-lookup"><span data-stu-id="c2df2-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="c2df2-124">應用程式和方案都包含在**資源群組**中。</span><span class="sxs-lookup"><span data-stu-id="c2df2-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="c2df2-125">資源群組可做為它在每個資源的 hello 生命週期界限。</span><span class="sxs-lookup"><span data-stu-id="c2df2-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="c2df2-126">您可以使用資源群組 toomanage 應用程式所有 hello 項目放在一起。</span><span class="sxs-lookup"><span data-stu-id="c2df2-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="c2df2-127">由於單一資源群組只能有多個應用程式服務計劃，您可以配置不同的應用程式 toodifferent 實體資源。</span><span class="sxs-lookup"><span data-stu-id="c2df2-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="c2df2-128">例如，您可以將資源分隔為開發、測試和生產環境。</span><span class="sxs-lookup"><span data-stu-id="c2df2-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="c2df2-129">將生產和開發/測試的環境分開可讓您隔離資源。</span><span class="sxs-lookup"><span data-stu-id="c2df2-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="c2df2-130">如此一來，負載測試針對您的應用程式的新版本並不會競用 hello 相同您實際執行的應用程式，實際客戶服務和資源。</span><span class="sxs-lookup"><span data-stu-id="c2df2-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="c2df2-131">當您在單一資源群組中有多個方案時，您也可以定義一個跨越地理區域的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="c2df2-132">例如，在兩個區域中執行的高度可用應用程式包括至少兩個方案，每個區域一個方案，而一個應用程式則與每個方案相關聯。</span><span class="sxs-lookup"><span data-stu-id="c2df2-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="c2df2-133">在這種情況下，hello 應用程式的所有 hello 副本然後都包含在單一資源群組。</span><span class="sxs-lookup"><span data-stu-id="c2df2-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="c2df2-134">具有多個計劃和多個應用程式的資源群組可輕鬆 toomanage、 控制和檢視 hello hello 應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="c2df2-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="c2df2-135">建立 App Service 方案或使用現有的方案</span><span class="sxs-lookup"><span data-stu-id="c2df2-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="c2df2-136">在建立應用程式時，請考慮建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="c2df2-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="c2df2-137">在 hello 相反地，如果此應用程式是較大型應用程式的元件，並建立 hello 配置給該較大的應用程式的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="c2df2-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="c2df2-138">是否 hello 應用程式是完全新的應用程式或更大的一個部分，您可以選擇 toouse 現有的計劃 toohost 它或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="c2df2-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="c2df2-139">這項決定其實是容量和預期負載方面的問題。</span><span class="sxs-lookup"><span data-stu-id="c2df2-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="c2df2-140">如果有下列情況，建議將您的應用程式隔離至新的 App Service 方案中：</span><span class="sxs-lookup"><span data-stu-id="c2df2-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="c2df2-141">應用程式會耗用大量資源。</span><span class="sxs-lookup"><span data-stu-id="c2df2-141">App is resource-intensive.</span></span>
- <span data-ttu-id="c2df2-142">應用程式有不同的縮放比例 hello 從裝載於現有的方案中其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="c2df2-143">應用程式需要不同地理區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="c2df2-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="c2df2-144">這樣可讓您為應用程式配置一組新的資源，更充分掌控您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="c2df2-145">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="c2df2-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="c2df2-146">如果您有 App Service 環境，您可以檢閱 hello 文件特定 tooApp 服務環境這裡： [App Service 環境中建立 App Service 方案](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="c2df2-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="c2df2-147">從應用程式服務計劃的瀏覽經驗 hello 或做為應用程式建立的一部分，您可以建立空白的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="c2df2-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="c2df2-148">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增** > **Web + 行動**，然後選取**Web 應用程式**或其他應用程式服務應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="c2df2-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![在 hello Azure 入口網站中建立應用程式。][createWebApp]

<span data-ttu-id="c2df2-150">然後，您可以選取或建立 hello hello 新應用程式的應用程式服務計劃。</span><span class="sxs-lookup"><span data-stu-id="c2df2-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![建立 App Service 方案。][createASP]

<span data-ttu-id="c2df2-152">toocreate App Service 方案中，按一下**[+] 建立新**，型別 hello **App Service 方案**名稱，然後再選取 適當**位置**。</span><span class="sxs-lookup"><span data-stu-id="c2df2-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="c2df2-153">按一下**定價層**，然後選取適當的定價層 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="c2df2-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="c2df2-154">選取**檢視所有**tooview 多定價選項，例如**免費**和**共用**。</span><span class="sxs-lookup"><span data-stu-id="c2df2-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="c2df2-155">您已選取 hello 定價層之後，請按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2df2-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="c2df2-156">移動應用程式 tooa 不同 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="c2df2-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="c2df2-157">您可以移動應用程式 tooa 不同 App Service 方案中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c2df2-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c2df2-158">您可以計劃之間移動應用程式，只要 hello 計劃已 hello 相同的資源群組和地理區域。</span><span class="sxs-lookup"><span data-stu-id="c2df2-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="c2df2-159">toomove 的應用程式 tooanother 計劃：</span><span class="sxs-lookup"><span data-stu-id="c2df2-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="c2df2-160">瀏覽您想 toomove toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="c2df2-161">在 hello**功能表**，尋找 hello **App Service 方案**> 一節。</span><span class="sxs-lookup"><span data-stu-id="c2df2-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="c2df2-162">選取**變更應用程式服務方案**toostart hello 程序。</span><span class="sxs-lookup"><span data-stu-id="c2df2-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="c2df2-163">**變更應用程式服務方案**開啟 hello **App Service 方案**選取器。</span><span class="sxs-lookup"><span data-stu-id="c2df2-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="c2df2-164">此時，您可以挑選現有的計劃 toomove 到此應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2df2-165">hello 選取應用程式服務方案 UI 會依下列準則的 hello 進行篩選：</span><span class="sxs-lookup"><span data-stu-id="c2df2-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="c2df2-166">存在於 hello 相同資源群組</span><span class="sxs-lookup"><span data-stu-id="c2df2-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="c2df2-167">存在於 hello 相同地理區域</span><span class="sxs-lookup"><span data-stu-id="c2df2-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="c2df2-168">存在於 hello 相同網路空間</span><span class="sxs-lookup"><span data-stu-id="c2df2-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="c2df2-169">網路空間是 App Service 內的邏輯結構，會定義伺服器資源的群組。</span><span class="sxs-lookup"><span data-stu-id="c2df2-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="c2df2-170">地理區域 （例如美國西部） 包含許多網路空間中使用應用程式服務的訂單 tooallocate 客戶。</span><span class="sxs-lookup"><span data-stu-id="c2df2-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="c2df2-171">目前應用程式服務的資源不能 toobe 網路空間之間移動。</span><span class="sxs-lookup"><span data-stu-id="c2df2-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![App Service 方案選取器。][change]

<span data-ttu-id="c2df2-173">每個方案都有其專屬定價層。</span><span class="sxs-lookup"><span data-stu-id="c2df2-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="c2df2-174">例如，將站台從免費層 tooa 標準層，可讓指派 tooit toouse hello 功能和資源 hello 標準層的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="c2df2-175">複製應用程式 tooa 不同 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="c2df2-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="c2df2-176">如果您想 toomove hello 應用程式 tooa 不同的區域，一種替代方法是應用程式複製。</span><span class="sxs-lookup"><span data-stu-id="c2df2-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="c2df2-177">複製會在任何區域中的新或現有 App Service 方案中產生您應用程式的複本。</span><span class="sxs-lookup"><span data-stu-id="c2df2-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="c2df2-178">您可以找到**複製應用程式**在 hello**開發工具**hello 功能表區段。</span><span class="sxs-lookup"><span data-stu-id="c2df2-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2df2-179">複製具有某些限制，若要深入了解，請閱讀 [使用 Azure 入口網站的 Azure App Service 應用程式複製](../app-service-web/app-service-web-app-cloning-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c2df2-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="c2df2-180">調整 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="c2df2-180">Scale an App Service plan</span></span>

<span data-ttu-id="c2df2-181">有三種方式 tooscale 計劃：</span><span class="sxs-lookup"><span data-stu-id="c2df2-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="c2df2-182">**變更 hello 計劃的定價層**。</span><span class="sxs-lookup"><span data-stu-id="c2df2-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="c2df2-183">Hello 基本層中的計畫可以是轉換後的 tooStandard 和所有應用程式指派 tooit toouse hello hello 標準層功能。</span><span class="sxs-lookup"><span data-stu-id="c2df2-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="c2df2-184">**變更 hello 計劃的執行個體大小**。</span><span class="sxs-lookup"><span data-stu-id="c2df2-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="c2df2-185">例如，hello 使用小型執行個體的基本層中的計畫可以是已變更的 toouse 大型執行個體。</span><span class="sxs-lookup"><span data-stu-id="c2df2-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="c2df2-186">現在與該方案相關聯之所有應用程式可以使用 hello 額外的記憶體和 CPU 資源，hello 較大的執行個體大小優惠。</span><span class="sxs-lookup"><span data-stu-id="c2df2-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="c2df2-187">**變更 hello 計劃的執行個體計數**。</span><span class="sxs-lookup"><span data-stu-id="c2df2-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="c2df2-188">比方說，向外延展 toothree 執行個體的標準方案可以調整的 too10 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c2df2-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="c2df2-189">高階計劃可以向外延展 too20 執行個體 (主體 tooavailability)。</span><span class="sxs-lookup"><span data-stu-id="c2df2-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="c2df2-190">現在與該方案相關聯之所有應用程式可以使用 hello 額外的記憶體和 CPU 資源，hello 較大的執行個體計數優惠。</span><span class="sxs-lookup"><span data-stu-id="c2df2-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="c2df2-191">您可以變更定價層和執行個體的大小，依序按一下 hello hello**向上延展**hello 應用程式或 hello 應用程式服務方案設定下的項目。</span><span class="sxs-lookup"><span data-stu-id="c2df2-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="c2df2-192">變更會套用 toohello App Service 方案，並會影響它所主控的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![設定值 tooscale 備份應用程式。][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="c2df2-194">App Service 方案清除</span><span class="sxs-lookup"><span data-stu-id="c2df2-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2df2-195">**應用程式服務計劃**具有沒有相關聯的應用程式 toothem，仍會產生費用，因為它們繼續 tooreserve hello 計算容量。</span><span class="sxs-lookup"><span data-stu-id="c2df2-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="c2df2-196">tooavoid 未預期的費用，刪除 hello 裝載應用程式服務計劃中的最後一個應用程式時，hello 產生空白的應用程式服務計劃也會一併刪除。</span><span class="sxs-lookup"><span data-stu-id="c2df2-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="c2df2-197">摘要</span><span class="sxs-lookup"><span data-stu-id="c2df2-197">Summary</span></span>

<span data-ttu-id="c2df2-198">應用程式服務方案代表可跨應用程式共用的一組特性和功能。</span><span class="sxs-lookup"><span data-stu-id="c2df2-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="c2df2-199">應用程式服務計劃提供 hello 彈性 tooallocate 特定應用程式 tooa 組的資源，並進一步最佳化 Azure 資源使用率。</span><span class="sxs-lookup"><span data-stu-id="c2df2-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="c2df2-200">如此一來，如果您想 toosave 金錢在測試環境中，您可以共用一個計劃跨多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2df2-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="c2df2-201">透過延展到多個區域和方案，也可以最大化生產環境的輸送量。</span><span class="sxs-lookup"><span data-stu-id="c2df2-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c2df2-202">變更的項目</span><span class="sxs-lookup"><span data-stu-id="c2df2-202">What's changed</span></span>

- <span data-ttu-id="c2df2-203">從網站 tooApp 服務指南 toohello 變更，請參閱： [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c2df2-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
