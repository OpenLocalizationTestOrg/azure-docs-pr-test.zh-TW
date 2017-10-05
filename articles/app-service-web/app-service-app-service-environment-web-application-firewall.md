---
title: "設定 App Service 環境的 Web 應用程式防火牆 (WAF)"
description: "了解如何設定 Web 應用程式防火牆來保護 App Service 環境。"
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="3af23-103">設定 App Service 環境的 Web 應用程式防火牆 (WAF)</span><span class="sxs-lookup"><span data-stu-id="3af23-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="3af23-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3af23-104">Overview</span></span>
<span data-ttu-id="3af23-105">[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) 上的 Web 應用程式防火牆 (如 [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure)) 有助於保護 Web 應用程式安全，方法是檢查輸入 Web 流量來封鎖 SQL 插入、跨站台指令碼，惡意上傳和應用程式 DDoS 以及其他攻擊。</span><span class="sxs-lookup"><span data-stu-id="3af23-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="3af23-106">它也會針對資料外洩防護 (DLP) 檢查來自後端 Web 伺服器的回應。</span><span class="sxs-lookup"><span data-stu-id="3af23-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="3af23-107">這與隔離以及 App Service 環境所提供的額外調整合併使用，以提供裝載商務關鍵 Web 應用程式的理想環境，而這些 Web 應用程式需要防禦惡意要求和大量流量。</span><span class="sxs-lookup"><span data-stu-id="3af23-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="3af23-108">設定</span><span class="sxs-lookup"><span data-stu-id="3af23-108">Setup</span></span>
<span data-ttu-id="3af23-109">在本文中，我們將設定受多個 Barracuda WAF 負載平衡執行個體保護的 App Service 環境，只讓來自 WAF 的流量到達 App Service 環境，而且無法從 DMZ 進行存取。</span><span class="sxs-lookup"><span data-stu-id="3af23-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="3af23-110">在 Barracuda WAF 執行個體之前，我們也有 Azure 流量管理員可在 Azure 資料中心和區域中進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="3af23-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="3af23-111">安裝程式的高階圖表看起來會像下方內容所示。</span><span class="sxs-lookup"><span data-stu-id="3af23-111">A high level diagram of the setup would look like what is shown below.</span></span>

![架構][Architecture] 

> <span data-ttu-id="3af23-113">注意︰藉由引進 [App Service 環境的 ILB 支援](app-service-environment-with-internal-load-balancer.md)，您可以設定讓 ASE 無法從 DMZ 供人存取，並僅可供私人網路使用。</span><span class="sxs-lookup"><span data-stu-id="3af23-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="3af23-114">設定 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="3af23-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="3af23-115">若要設定 App Service 環境，請參閱有關本主題的 [文件](app-service-web-how-to-create-an-app-service-environment.md) 。</span><span class="sxs-lookup"><span data-stu-id="3af23-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="3af23-116">建立 App Service 環境之後，即可在此環境中建立 [Web Apps](app-service-web-overview.md)、[API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) 和 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md)，而這些都是由下一節中設定的 WAF 所保護。</span><span class="sxs-lookup"><span data-stu-id="3af23-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="3af23-117">設定 Barracuda WAF 雲端服務</span><span class="sxs-lookup"><span data-stu-id="3af23-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="3af23-118">Barracuda 具有在 Azure 中於虛擬機器上部署其 WAF 的 [詳細文章](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) 。</span><span class="sxs-lookup"><span data-stu-id="3af23-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="3af23-119">但是，因為我們想要具有備援性，但不想要引進單一失敗點，所以您想要在遵循這些指示時將至少 2 個 WAF 執行個體 VM 部署至相同的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3af23-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="3af23-120">將端點加入雲端服務</span><span class="sxs-lookup"><span data-stu-id="3af23-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="3af23-121">雲端服務中有 2 個以上的 WAF VM 執行個體之後，即可使用 [Azure 入口網站](https://portal.azure.com/) 加入應用程式所使用的 HTTP 和 HTTPS 端點 (如下圖所示)。</span><span class="sxs-lookup"><span data-stu-id="3af23-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![設定端點][ConfigureEndpoint]

<span data-ttu-id="3af23-123">如果您的應用程式使用其他端點，則也請一定要將它們加入這份清單中。</span><span class="sxs-lookup"><span data-stu-id="3af23-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="3af23-124">透過管理入口網站設定 Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="3af23-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="3af23-125">Barracuda WAF 使用 TCP 連接埠 8000，以透過其管理入口網站進行設定。</span><span class="sxs-lookup"><span data-stu-id="3af23-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="3af23-126">因為我們有多個 WAF VM 執行個體，所以您需要針對每個 VM 執行個體重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="3af23-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="3af23-127">附註：完成 WAF 設定之後，請從所有 WAF VM 中移除 TCP/8000 端點，以保護 WAF 的安全。</span><span class="sxs-lookup"><span data-stu-id="3af23-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="3af23-128">若要設定 Barracuda WAF，請加入管理端點 (如下列影像所示)。</span><span class="sxs-lookup"><span data-stu-id="3af23-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![加入管理端點][AddManagementEndpoint]

<span data-ttu-id="3af23-130">使用瀏覽器瀏覽至雲端服務上的管理端點。</span><span class="sxs-lookup"><span data-stu-id="3af23-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="3af23-131">如果您的雲端服務稱為 test.cloudapp.net，則瀏覽至 http://test.cloudapp.net:8000 即可存取此端點。</span><span class="sxs-lookup"><span data-stu-id="3af23-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="3af23-132">您應該會看到與下面類似的登入頁面，以使用您在 WAF VM 設定階段中指定的認證進行登入。</span><span class="sxs-lookup"><span data-stu-id="3af23-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![管理登入頁面][ManagementLoginPage]

<span data-ttu-id="3af23-134">登入之後，應該會看到下圖中所顯示的儀表板，而此儀表板會顯示 WAF 保護的基本統計資料。</span><span class="sxs-lookup"><span data-stu-id="3af23-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![管理儀表板][ManagementDashboard]

<span data-ttu-id="3af23-136">按一下 [服務] 索引標籤，可讓您設定所保護服務的 WAF。</span><span class="sxs-lookup"><span data-stu-id="3af23-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="3af23-137">如需設定 Barracuda WAF 的詳細資料，您可以查閱 [其文件](https://techlib.barracuda.com/waf/getstarted1)。</span><span class="sxs-lookup"><span data-stu-id="3af23-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="3af23-138">在下列範例中，已設定處理 HTTP 和 HTTPS 流量的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3af23-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![管理加入服務][ManagementAddServices]

> <span data-ttu-id="3af23-140">附註：根據應用程式的設定方式與 App Service 環境中正在使用的功能，您需要轉送非 80 和 443 之 TCP 連接埠的流量 (例如，如果您為 Web 應用程式設定 IP SSL)。</span><span class="sxs-lookup"><span data-stu-id="3af23-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="3af23-141">如需 App Service 環境中所使用網路連接埠的清單，請參閱 [控制輸入流量文件](app-service-app-service-environment-control-inbound-traffic.md) 的＜網路連接埠＞一節。</span><span class="sxs-lookup"><span data-stu-id="3af23-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="3af23-142">設定 Microsoft Azure 流量管理員 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="3af23-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="3af23-143">如果多個區域中都有您的應用程式，則您會想要使用 [Azure 流量管理員](../traffic-manager/traffic-manager-overview.md)對它們進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="3af23-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="3af23-144">若要這麼做，您可以使用流量管理員設定檔中 WAF 的雲端服務名稱在 [Azure 傳統入口網站](https://manage.azure.com) 中加入端點 (如下列影像所示)。</span><span class="sxs-lookup"><span data-stu-id="3af23-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![流量管理員端點][TrafficManagerEndpoint]

<span data-ttu-id="3af23-146">如果您的應用程式需要驗證，請確定您有某個資源不需要任何驗證，以讓流量管理員進行 Ping 處理確認應用程式是否可用。</span><span class="sxs-lookup"><span data-stu-id="3af23-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="3af23-147">您可以在 [Azure 傳統入口網站](https://manage.azure.com) 的 [設定] 區段下設定 URL (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="3af23-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![設定流量管理員][ConfigureTrafficManager]

<span data-ttu-id="3af23-149">若要將流量管理員 Ping 從 WAF 轉送給應用程式，則需要在 Barracuda WAF 上設定網站轉譯，以將流量轉送給應用程式 (如下面範例所示)。</span><span class="sxs-lookup"><span data-stu-id="3af23-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![網站轉譯][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="3af23-151">使用網路安全性群組 (NSG) 保護 App Service 環境流量的安全</span><span class="sxs-lookup"><span data-stu-id="3af23-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="3af23-152">如需使用雲端服務的 VIP 位址只限制從 WAF 流入 App Service 環境之流量的詳細資訊，請遵循 [控制輸入流量文件](app-service-app-service-environment-control-inbound-traffic.md) 。</span><span class="sxs-lookup"><span data-stu-id="3af23-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="3af23-153">以下是針對 TCP 通訊埠 80 執行這項工作的範例 Powershell 命令。</span><span class="sxs-lookup"><span data-stu-id="3af23-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="3af23-154">將 SourceAddressPrefix 取代為 WAF 雲端服務的虛擬 IP 位址 (VIP)。</span><span class="sxs-lookup"><span data-stu-id="3af23-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="3af23-155">附註：刪除並重新建立雲端服務之後，將會變更雲端服務的 VIP。</span><span class="sxs-lookup"><span data-stu-id="3af23-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="3af23-156">在這樣做之後，請一定要更新網路資源群組中的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3af23-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
