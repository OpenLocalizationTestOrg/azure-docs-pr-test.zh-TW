---
title: "Web Apps 概觀 | Microsoft Docs"
description: "了解 Azure App Service 如何協助您開發和裝載 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3db15e9dcdd510481f4982198da5ac950f2c7e4f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="web-apps-overview"></a><span data-ttu-id="44230-103">Web 應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="44230-103">Web Apps overview</span></span>
<span data-ttu-id="44230-104"> 是受到完整管理的計算平台，非常適合用來裝載網站和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="44230-104">*App Service Web Apps* is a fully managed compute platform that is optimized for hosting websites and web applications.</span></span> <span data-ttu-id="44230-105">Microsoft Azure 的這個 [平台即服務](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) 產品可讓您專注於商務邏輯，而讓 Azure 負責處理用來執行及調整應用程式的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="44230-105">This [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) offering of Microsoft Azure lets you focus on your business logic while Azure takes care of the infrastructure to run and scale your apps.</span></span>

<span data-ttu-id="44230-106">下列的 5 分鐘影片將介紹 Azure App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="44230-106">The following 5-minute video introduces Azure App Service Web Apps.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a><span data-ttu-id="44230-107">什麼是 App Service 中的 Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="44230-107">What is a web app in App Service?</span></span>
<span data-ttu-id="44230-108">在 App Service 中，「Web 應用程式」  是 Azure 提供用來裝載網站或 Web 應用程式的計算資源。</span><span class="sxs-lookup"><span data-stu-id="44230-108">In App Service, a *web app* is the compute resources that Azure provides for hosting a website or web application.</span></span>  

<span data-ttu-id="44230-109">計算資源可能位於共用或專用的虛擬機器 (VM)，一切視您選擇的定價層而定。</span><span class="sxs-lookup"><span data-stu-id="44230-109">The compute resources may be on shared or dedicated virtual machines (VMs), depending on the pricing tier that you choose.</span></span> <span data-ttu-id="44230-110">應用程式的程式碼會在與其他客戶隔離開來的受管理 VM 中執行。</span><span class="sxs-lookup"><span data-stu-id="44230-110">Your application code runs in a managed VM that is isolated from other customers.</span></span>

<span data-ttu-id="44230-111">程式碼可以使用 [Azure App Service](../app-service/app-service-value-prop-what-is.md)所支援的任何語言或架構，例如 ASP.NET、Node.js、Java、PHP 或 Python。</span><span class="sxs-lookup"><span data-stu-id="44230-111">Your code can be in any language or framework that is supported by [Azure App Service](../app-service/app-service-value-prop-what-is.md), such as ASP.NET, Node.js, Java, PHP, or Python.</span></span> <span data-ttu-id="44230-112">您也可以在 Web 應用程式中，執行使用 [PowerShell 和其他指令碼語言](web-sites-create-web-jobs.md#acceptablefiles) 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="44230-112">You can also run scripts that use [PowerShell and other scripting languages](web-sites-create-web-jobs.md#acceptablefiles) in a web app.</span></span>

<span data-ttu-id="44230-113">如需可使用 Web Apps 的典型應用程式案例的範例，請參閱 [Web 應用程式案例](https://azure.microsoft.com/documentation/scenarios/web-app/)和 [Azure App Service、雲端服務、虛擬機器及 Service Fabric 的比較](choose-web-site-cloud-service-vm.md#scenarios)的**案例和建議**一節。</span><span class="sxs-lookup"><span data-stu-id="44230-113">For examples of typical application scenarios that you can use Web Apps for, see [Web app scenarios](https://azure.microsoft.com/documentation/scenarios/web-app/) and the **Scenarios and recommendations** section of [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md#scenarios).</span></span>

## <a name="why-use-web-apps"></a><span data-ttu-id="44230-114">為何要使用 Web Apps？</span><span class="sxs-lookup"><span data-stu-id="44230-114">Why use Web Apps?</span></span>
<span data-ttu-id="44230-115">以下是 App Service 適用於 Web Apps 的一些主要功能︰</span><span class="sxs-lookup"><span data-stu-id="44230-115">Here are some key features of App Service that apply to Web Apps:</span></span>

* <span data-ttu-id="44230-116">**多種語言和架構** - App Service有 ASP.NET、Node.js、Java、PHP 和 Python 的頂級支援。</span><span class="sxs-lookup"><span data-stu-id="44230-116">**Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python.</span></span> <span data-ttu-id="44230-117">您也可以在 App Service VM 上執行 [PowerShell 和其他指令碼或可執行檔](web-sites-create-web-jobs.md) 。</span><span class="sxs-lookup"><span data-stu-id="44230-117">You can also run [PowerShell and other scripts or executables](web-sites-create-web-jobs.md) on App Service VMs.</span></span>
* <span data-ttu-id="44230-118">**DevOps 最佳化** - 使用 Visual Studio Team Services、GitHub 或 BitBucket 設定 [持續整合和部署](app-service-continuous-deployment.md) 。</span><span class="sxs-lookup"><span data-stu-id="44230-118">**DevOps optimization** - Set up [continuous integration and deployment](app-service-continuous-deployment.md) with Visual Studio Team Services, GitHub, or BitBucket.</span></span> <span data-ttu-id="44230-119">透過 [測試和預備環境](web-sites-staged-publishing.md)升級更新。</span><span class="sxs-lookup"><span data-stu-id="44230-119">Promote updates through [test and staging environments](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="44230-120">執行 [A/B 測試](app-service-web-test-in-production-get-start.md)。</span><span class="sxs-lookup"><span data-stu-id="44230-120">Perform [A/B testing](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="44230-121">使用 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 或[跨平台命令列介面 (CLI)](../cli-install-nodejs.md)，在 App Service 中管理您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="44230-121">Manage your apps in App Service by using [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="44230-122">**具高可用性的全域調整** - 以手動或自動方式相應[增加](web-sites-scale.md)或[放大](../monitoring-and-diagnostics/insights-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="44230-122">**Global scale with high availability** - Scale [up](web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically.</span></span> <span data-ttu-id="44230-123">在 Microsoft 的通用資料中心基礎結構中隨處裝載您的應用程式，而 App Service [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) 會承諾高可用性。</span><span class="sxs-lookup"><span data-stu-id="44230-123">Host your apps anywhere in Microsoft's global datacenter infrastructure, and the App Service [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promises high availability.</span></span>
* <span data-ttu-id="44230-124">**SaaS 平台和內部部署資料的連線** - 有超過 50 種適用於企業系統 (例如 SAP、Siebel 和 Oracle)、SaaS 服務 (例如 Salesforce 和 Office 365)，以及網際網路服務 (例如 Facebook 和 Twitter) 的 [連接器](../connectors/apis-list.md) 可供選擇。</span><span class="sxs-lookup"><span data-stu-id="44230-124">**Connections to SaaS platforms and on-premises data** - Choose from more than 50 [connectors](../connectors/apis-list.md) for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services (such as Facebook and Twitter).</span></span> <span data-ttu-id="44230-125">使用[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和 [Azure 虛擬網路](web-sites-integrate-with-vnet.md)存取內部部署資料。</span><span class="sxs-lookup"><span data-stu-id="44230-125">Access on-premises data using [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Azure Virtual Networks](web-sites-integrate-with-vnet.md).</span></span>
* <span data-ttu-id="44230-126">**安全性和法規遵循** - App Service 為 [ISO、SOC 和 PCI 相容](https://www.microsoft.com/TrustCenter/)。</span><span class="sxs-lookup"><span data-stu-id="44230-126">**Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.microsoft.com/TrustCenter/).</span></span>
* <span data-ttu-id="44230-127">**應用程式範本** - 從 [Azure Marketplace](https://azure.microsoft.com/marketplace/) 中的廣泛應用程式範本清單中進行選擇，以便使用精靈來安裝受歡迎的開放原始碼軟體，例如 WordPress、Joomla 和 Drupal。</span><span class="sxs-lookup"><span data-stu-id="44230-127">**Application templates** - Choose from an extensive list of application templates in the [Azure Marketplace](https://azure.microsoft.com/marketplace/) that let you use a wizard to install popular open-source software such as WordPress, Joomla, and Drupal.</span></span>
* <span data-ttu-id="44230-128">**Visual Studio 整合** - Visual Studio 中的專用工具可簡化建立、部署和偵錯的工作。</span><span class="sxs-lookup"><span data-stu-id="44230-128">**Visual Studio integration** - Dedicated tools in Visual Studio streamline the work of creating, deploying, and debugging.</span></span>

<span data-ttu-id="44230-129">此外，Web 應用程式可以利用 [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (例如 CORS 支援) 和 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (例如推播通知) 所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="44230-129">In addition, a web app can take advantage of features offered by [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (such as CORS support) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (such as push notifications).</span></span> <span data-ttu-id="44230-130">如需 App Service 中的應用程式類型詳細資訊，請參閱 [Azure App Service 概觀](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="44230-130">For more information about app types in App Service, see [Azure App Service overview](../app-service/app-service-value-prop-what-is.md).</span></span>

<span data-ttu-id="44230-131">除了 App Service 中的 Web Apps，Azure 還提供可用來裝載網站和 Web 應用程式的其他服務。</span><span class="sxs-lookup"><span data-stu-id="44230-131">Besides Web Apps in App Service, Azure offers other services that can be used for hosting websites and web applications.</span></span> <span data-ttu-id="44230-132">大部分的情況下，Web Apps 是最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="44230-132">For most scenarios, Web Apps is the best choice.</span></span>  <span data-ttu-id="44230-133">若是微服務架構，請考慮使用 [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)，如果您需要能更加充分地掌控程式碼執行所在的 VM，則請考慮使用 [Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="44230-133">For microservice architecture, consider [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric), and if you need more control over the VMs that your code runs on, consider [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span> <span data-ttu-id="44230-134">如需如何在這些 Azure 服務之間做選擇的詳細資訊，請參閱 [Azure App Service、虛擬機器、Service Fabric 及雲端服務的比較](choose-web-site-cloud-service-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="44230-134">For more information about how to choose between these Azure services, see [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="44230-135">開始使用</span><span class="sxs-lookup"><span data-stu-id="44230-135">Getting started</span></span>
<span data-ttu-id="44230-136">若要開始在 App Service 中的新 Web 應用程式部署範例程式碼，請遵循下列下拉式方塊中的其中一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="44230-136">To get started by deploying sample code to a new web app in App Service, follow one of the tutorials in the following dropdown box.</span></span> <span data-ttu-id="44230-137">您將需要免費的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="44230-137">You'll need a free Azure account.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="44230-138">在 5 分鐘內將您的第一個 ASP.NET Web 應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="44230-138">Deploy your first ASP.NET web app to Azure in 5 minutes</span></span>](app-service-web-get-started-dotnet.md)
> * [<span data-ttu-id="44230-139">在 5 分鐘內將您的第一個 PHP Web 應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="44230-139">Deploy your first PHP web app to Azure in 5 minutes</span></span>](app-service-web-get-started-php.md)
> * [<span data-ttu-id="44230-140">在 5 分鐘內將您的第一個 Node.js Web 應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="44230-140">Deploy your first Node.js web app to Azure in 5 minutes</span></span>](app-service-web-get-started-nodejs.md)
> * [<span data-ttu-id="44230-141">在 5 分鐘內將您的第一個 Java Web 應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="44230-141">Deploy your first Java web app to Azure in 5 minutes</span></span>](app-service-web-get-started-java.md)
> * [<span data-ttu-id="44230-142">在 5 分鐘內將您的第一個 Python Web 應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="44230-142">Deploy your first Python web app to Azure in 5 minutes</span></span>](app-service-web-get-started-python.md)
> * [<span data-ttu-id="44230-143">在 5 分鐘內將您的第一個 HTML 網站部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="44230-143">Deploy your first HTML site to Azure in 5 minutes</span></span>](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> <span data-ttu-id="44230-144">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="44230-144">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="44230-145">建立入門 App，並試用長達一小時。不需要信用卡，也不需簽定合約。</span><span class="sxs-lookup"><span data-stu-id="44230-145">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 
