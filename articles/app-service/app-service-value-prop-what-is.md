---
title: "適用於 web、 mobile 和應用程式開發介面應用程式的應用程式服務 aaaAzure |Microsoft 文件"
description: "了解 Azure App Service 如何協助您開發、部署和管理 Web 和行動應用程式。"
keywords: "App Service, Azure App Service, App Service 成本, 級別, 可調整, 應用程式部署, Azure 應用程式部署, paas, 平台即服務, 網站, web, azure 行動"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a><span data-ttu-id="002cf-104">什麼是 Azure App Service？</span><span class="sxs-lookup"><span data-stu-id="002cf-104">What is Azure App Service?</span></span>
<span data-ttu-id="002cf-105"> 是 Microsoft Azure 的 [平台即服務](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) 供應項目。</span><span class="sxs-lookup"><span data-stu-id="002cf-105">*App Service* is a [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) offering of Microsoft Azure.</span></span> <span data-ttu-id="002cf-106">建立適用任何平台或裝置的 Web 與行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-106">Create web and mobile apps for any platform or device.</span></span> <span data-ttu-id="002cf-107">整合您的應用程式與 SaaS 解決方案、與內部部署應用程式連接，並使您的商務程序自動化。</span><span class="sxs-lookup"><span data-stu-id="002cf-107">Integrate your apps with SaaS solutions, connect with on-premises applications, and automate your business processes.</span></span> <span data-ttu-id="002cf-108">Azure 會使用您選擇的共用 VM 資源或專用 VM，在完全受管理的虛擬機器 (VM) 上執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-108">Azure runs your apps on fully managed virtual machines (VMs), with your choice of shared VM resources or dedicated VMs.</span></span>

<span data-ttu-id="002cf-109">應用程式服務包括 hello web 和行動我們先前分別以傳遞 Azure 網站和 Azure 行動服務的功能。</span><span class="sxs-lookup"><span data-stu-id="002cf-109">App Service includes hello web and mobile capabilities that we previously delivered separately as Azure Websites and Azure Mobile Services.</span></span> <span data-ttu-id="002cf-110">此外，它也包含可用來自動執行商務程序及裝載雲端 API 的新功能。</span><span class="sxs-lookup"><span data-stu-id="002cf-110">It also includes new capabilities for automating business processes and hosting cloud APIs.</span></span> <span data-ttu-id="002cf-111">App Service 是單一的整合式服務，可讓您將各種元件 (網站、行動應用程式後端、RESTful API 和商務程序) 撰寫成單一解決方案。</span><span class="sxs-lookup"><span data-stu-id="002cf-111">As a single integrated service, App Service lets you compose various components -- websites, mobile app back ends, RESTful APIs, and business processes -- into a single solution.</span></span>

<span data-ttu-id="002cf-112">hello 下列 4 分鐘影片提供的簡短說明的應用程式服務與 tooearlier Azure 的相關供應項目，並在其最新消息。</span><span class="sxs-lookup"><span data-stu-id="002cf-112">hello following 4-minute video provides a brief explanation of how App Service relates tooearlier Azure offerings and what's new in it.</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a><span data-ttu-id="002cf-113">為何要使用 App Service？</span><span class="sxs-lookup"><span data-stu-id="002cf-113">Why use App Service?</span></span>
<span data-ttu-id="002cf-114">以下是 App Service 的一些重要功能和能力︰</span><span class="sxs-lookup"><span data-stu-id="002cf-114">Here are some key features and capabilities of App Service:</span></span>

* <span data-ttu-id="002cf-115">**多種語言和架構** - App Service有 ASP.NET、Node.js、Java、PHP 和 Python 的頂級支援。</span><span class="sxs-lookup"><span data-stu-id="002cf-115">**Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python.</span></span> <span data-ttu-id="002cf-116">您也可以在 App Service VM 上執行 [Windows PowerShell 和其他指令碼或可執行檔](../app-service-web/web-sites-create-web-jobs.md) 。</span><span class="sxs-lookup"><span data-stu-id="002cf-116">You can also run [Windows PowerShell and other scripts or executables](../app-service-web/web-sites-create-web-jobs.md) on App Service VMs.</span></span>
* <span data-ttu-id="002cf-117">**DevOps 最佳化** - 使用 Visual Studio Team Services、GitHub 或 BitBucket 設定 [持續整合和部署](../app-service-web/app-service-continuous-deployment.md) 。</span><span class="sxs-lookup"><span data-stu-id="002cf-117">**DevOps optimization** - Set up [continuous integration and deployment](../app-service-web/app-service-continuous-deployment.md) with Visual Studio Team Services, GitHub, or BitBucket.</span></span> <span data-ttu-id="002cf-118">透過 [測試和預備環境](../app-service-web/web-sites-staged-publishing.md)升級更新。</span><span class="sxs-lookup"><span data-stu-id="002cf-118">Promote updates through [test and staging environments](../app-service-web/web-sites-staged-publishing.md).</span></span> <span data-ttu-id="002cf-119">執行 [A/B 測試](../app-service-web/app-service-web-test-in-production-get-start.md)。</span><span class="sxs-lookup"><span data-stu-id="002cf-119">Perform [A/B testing](../app-service-web/app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="002cf-120">管理您的應用程式，App Service 中使用[Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello[跨平台命令列介面 (CLI)](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="002cf-120">Manage your apps in App Service by using [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="002cf-121">**具高可用性的全域調整** - 以手動或自動方式相應[增加](../app-service-web/web-sites-scale.md)或[放大](../monitoring-and-diagnostics/insights-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="002cf-121">**Global scale with high availability** - Scale [up](../app-service-web/web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically.</span></span> <span data-ttu-id="002cf-122">裝載任何位置在 Microsoft 的全域資料中心基礎結構，應用程式和應用程式服務的 hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/)承諾高可用性。</span><span class="sxs-lookup"><span data-stu-id="002cf-122">Host your apps anywhere in Microsoft's global datacenter infrastructure, and hello App Service [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promises high availability.</span></span>
* <span data-ttu-id="002cf-123">**Connections tooSaaS 平台和內部部署資料**-選擇超過 50[連接器](../connectors/apis-list.md)企業系統 （例如 SAP、 Siebel 和 Oracle），如 SaaS 服務 （例如 Salesforce 和 Office 365） 和網際網路服務 （例如 Facebook 和 Twitter）。</span><span class="sxs-lookup"><span data-stu-id="002cf-123">**Connections tooSaaS platforms and on-premises data** - Choose from more than 50 [connectors](../connectors/apis-list.md) for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services (such as Facebook and Twitter).</span></span> <span data-ttu-id="002cf-124">使用[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和 [Azure 虛擬網路](../app-service-web/web-sites-integrate-with-vnet.md)存取內部部署資料。</span><span class="sxs-lookup"><span data-stu-id="002cf-124">Access on-premises data using [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Azure Virtual Networks](../app-service-web/web-sites-integrate-with-vnet.md).</span></span>
* <span data-ttu-id="002cf-125">**安全性和法規遵循** - App Service 為 [ISO、SOC 和 PCI 相容](https://www.microsoft.com/TrustCenter/)。</span><span class="sxs-lookup"><span data-stu-id="002cf-125">**Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.microsoft.com/TrustCenter/).</span></span>
* <span data-ttu-id="002cf-126">**應用程式範本**-從延伸 hello 中的範本清單中選擇[Azure Marketplace](https://azure.microsoft.com/marketplace/) ，可讓您使用精靈 tooinstall 熱門開放原始碼軟體，例如 WordPress、 Joomla 和 Drupal。</span><span class="sxs-lookup"><span data-stu-id="002cf-126">**Application templates** - Choose from an extensive list of templates in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) that let you use a wizard tooinstall popular open-source software such as WordPress, Joomla, and Drupal.</span></span>
* <span data-ttu-id="002cf-127">**Visual Studio 整合**-Visual Studio 中的專用的工具簡化 hello 工作建立、 部署和偵錯。</span><span class="sxs-lookup"><span data-stu-id="002cf-127">**Visual Studio integration** - Dedicated tools in Visual Studio streamline hello work of creating, deploying, and debugging.</span></span>

## <a name="app-types-in-app-service"></a><span data-ttu-id="002cf-128">App Service 中的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="002cf-128">App types in App Service</span></span>
<span data-ttu-id="002cf-129">應用程式服務提供數個*應用程式類型*，每個都是預定的 toohost 特定的工作負載：</span><span class="sxs-lookup"><span data-stu-id="002cf-129">App Service offers several *app types*, each of which is intended toohost a specific workload:</span></span>

* <span data-ttu-id="002cf-130">[Web Apps](../app-service-web/app-service-web-overview.md) - 用於裝載網站和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-130">[**Web Apps**](../app-service-web/app-service-web-overview.md) - For hosting websites and web applications.</span></span>
* <span data-ttu-id="002cf-131">[Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) - 用於裝載行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="002cf-131">[**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md) For hosting mobile app back ends.</span></span>
* <span data-ttu-id="002cf-132">[**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) - 用於裝載 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="002cf-132">[**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) - For hosting RESTful APIs.</span></span>
* <span data-ttu-id="002cf-133">[**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) - 用於自動化商務程序和跨雲端整合系統和資料，而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="002cf-133">[**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) - For automating business processes and integrating systems and data across clouds without writing code.</span></span>

<span data-ttu-id="002cf-134">hello word*應用程式*這裡是指 toohello 裝載資源專用的 toorunning 工作負載。</span><span class="sxs-lookup"><span data-stu-id="002cf-134">hello word *app* here refers toohello hosting resources dedicated toorunning a workload.</span></span> <span data-ttu-id="002cf-135">取得做為範例的 「 web 應用程式 」，您很可能是因為 hello 計算資源和應用程式程式碼一起傳遞功能 tooa 瀏覽器慣用 toothinking web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-135">Taking “web app” as an example, you’re probably accustomed toothinking of a web app as both hello compute resources and application code that together deliver functionality tooa browser.</span></span> <span data-ttu-id="002cf-136">App Service 中，但*web 應用程式*為 hello Azure 提供裝載應用程式程式碼的計算資源。</span><span class="sxs-lookup"><span data-stu-id="002cf-136">But in App Service a *web app* is hello compute resources that Azure provides for hosting your application code.</span></span> 

<span data-ttu-id="002cf-137">您的應用程式可能是由多個各種不同的 App Service 應用程式所組成。</span><span class="sxs-lookup"><span data-stu-id="002cf-137">Your application may be composed of multiple App Service apps of different kinds.</span></span> <span data-ttu-id="002cf-138">例如，如果您的應用程式包含 Web 前端和RESTful API 後端，您可以︰</span><span class="sxs-lookup"><span data-stu-id="002cf-138">For example If your application is composed of a web front end and a RESTful API back end you could:</span></span>

- <span data-ttu-id="002cf-139">部署 （前端和應用程式開發介面） tooa 單一 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="002cf-139">Deploy both (front end and api) tooa single web app</span></span>  
- <span data-ttu-id="002cf-140">部署 web 應用程式前端的程式碼 tooa 和 tooan API 應用程式後端程式碼。</span><span class="sxs-lookup"><span data-stu-id="002cf-140">Deploy your front-end code tooa web app and your back-end code tooan API app.</span></span> 



## <a name="app-service-plans"></a><span data-ttu-id="002cf-141">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="002cf-141">App Service plans</span></span>
<span data-ttu-id="002cf-142">[應用程式服務計劃](azure-web-sites-web-hosting-plans-in-depth-overview.md)代表 hello 集合，其使用的實體資源 toohost 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-142">[App Service plans](azure-web-sites-web-hosting-plans-in-depth-overview.md) represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="002cf-143">App Service 方案可定義：</span><span class="sxs-lookup"><span data-stu-id="002cf-143">App Service plans define:</span></span>

- <span data-ttu-id="002cf-144">**區域** (美國西部、美國東部等)</span><span class="sxs-lookup"><span data-stu-id="002cf-144">**Region** (West US, East US, etc.)</span></span>
- <span data-ttu-id="002cf-145">**級別計數** (一、二、三個執行個體等)</span><span class="sxs-lookup"><span data-stu-id="002cf-145">**Scale count** (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="002cf-146">**執行個體大小** (小型、中型、大型)</span><span class="sxs-lookup"><span data-stu-id="002cf-146">**Instance size** (Small, Medium, Large)</span></span>
- <span data-ttu-id="002cf-147">**SKU** (免費、共用、基本、標準、進階)</span><span class="sxs-lookup"><span data-stu-id="002cf-147">**SKU** (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="002cf-148">所有應用程式指派 tooan **App Service 方案**共用 hello 它允許您 toosave 成本裝載多個應用程式時所定義的資源。</span><span class="sxs-lookup"><span data-stu-id="002cf-148">All applications assigned tooan **App Service plan** share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>

<span data-ttu-id="002cf-149">您**App Service 方案**範圍，小從**免費**和**共用**Sku 太**基本**，**標準**，和**Premium** Sku 讓您存取 toomore 資源和沿著 hello 功能的方式。</span><span class="sxs-lookup"><span data-stu-id="002cf-149">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span> <span data-ttu-id="002cf-150">一旦您 App Service 方案太設定**基本**或更高版本您也可以控制 hello**大小**和調整 hello Vm 的計數。</span><span class="sxs-lookup"><span data-stu-id="002cf-150">Once your App Service Plan is set too**Basic** or higher you can also control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="002cf-151">hello **SKU**和**標尺**的 hello 應用程式服務計劃可決定 hello 成本不 hello 數目及託管於該應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-151">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span> 

<span data-ttu-id="002cf-152">如果您需要更多的延展性和網路隔離，則可在 [App Service 環境](../app-service-web/app-service-app-service-environment-intro.md)中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="002cf-152">If you need more scalability and network isolation, you can run your apps in an [App Service Environment](../app-service-web/app-service-app-service-environment-intro.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="002cf-153">定價</span><span class="sxs-lookup"><span data-stu-id="002cf-153">Pricing</span></span>
<span data-ttu-id="002cf-154">如需 App Service 費用的詳細資訊，請參閱 [App Service 價格](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="002cf-154">For information about how much App Service costs, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

## <a name="test-drive-app-service"></a><span data-ttu-id="002cf-155">試驗 App Service</span><span class="sxs-lookup"><span data-stu-id="002cf-155">Test-drive App Service</span></span>
<span data-ttu-id="002cf-156">[建立範例 Web 應用程式、行動應用程式或邏輯應用程式](https://azure.microsoft.com/try/app-service/)，並試用一小時，無需信用卡，也無需簽定合約，一切都非常簡單。</span><span class="sxs-lookup"><span data-stu-id="002cf-156">[Create a sample web app, mobile app, or logic app](https://azure.microsoft.com/try/app-service/) and play with it for one hour, with no credit card required, no commitments, no hassles.</span></span>

<span data-ttu-id="002cf-157">或申請 [免費 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)，並試試我們的其中一個入門教學課程︰</span><span class="sxs-lookup"><span data-stu-id="002cf-157">Or open a [free Azure account](https://azure.microsoft.com/pricing/free-trial/), and try one of our getting-started tutorials:</span></span>

* [<span data-ttu-id="002cf-158">教學課程︰建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="002cf-158">Tutorial: Create a web app</span></span>](../app-service-web/app-service-web-get-started.md)
* [<span data-ttu-id="002cf-159">教學課程︰建立行動應用程式</span><span class="sxs-lookup"><span data-stu-id="002cf-159">Tutorial: Create a mobile app</span></span>](../app-service-mobile/app-service-mobile-android-get-started.md)
* [<span data-ttu-id="002cf-160">教學課程︰建立 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="002cf-160">Tutorial: Create an API app</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)
* [<span data-ttu-id="002cf-161">教學課程︰建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="002cf-161">Tutorial: Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

