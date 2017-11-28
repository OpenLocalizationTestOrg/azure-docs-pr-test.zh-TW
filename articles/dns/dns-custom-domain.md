---
title: "整合 Azure DNS 與您的 Azure 資源 | Microsoft Docs"
description: "了解如何使用 Azure DNS 為您的 Azure 資源提供 DNS。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: e0e7144c38c36f1583e0bcb7dfffba26e9a8bdad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-dns-to-provide-custom-domain-settings-for-an-azure-service"></a><span data-ttu-id="d4dcf-103">使用 Azure DNS 為 Azure 服務提供自訂網域設定</span><span class="sxs-lookup"><span data-stu-id="d4dcf-103">Use Azure DNS to provide custom domain settings for an Azure service</span></span>

<span data-ttu-id="d4dcf-104">Azure DNS 提供自訂網域的 DNS，可用於任何支援自訂網域或具有完整網域名稱 (FQDN) 的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-104">Azure DNS provides DNS for a custom domain for any of your Azure resources that support custom domains or that have a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="d4dcf-105">例如，您有一個 Azure Web 應用程式，而且想要使用 contoso.com 或 www.contoso.com 作為 FQDN 讓使用者存取它。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-105">An example is you have an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span> <span data-ttu-id="d4dcf-106">本文章會引導您使用 Azure DNS 設定您的 Azure 服務，以便使用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-106">This article walks you through configuring your Azure service with Azure DNS for using custom domains.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4dcf-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4dcf-107">Prerequisites</span></span>

<span data-ttu-id="d4dcf-108">為了在您的自訂網域 Azure DNS，您必須先將您的網域委派給 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-108">In order to use Azure DNS for your custom domain, you must first delegate your domain to Azure DNS.</span></span> <span data-ttu-id="d4dcf-109">如需如何設定名稱伺服器以便進行委派的指示，請參閱[將網域委派給 Azure DNS](./dns-delegate-domain-azure-dns.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-109">Visit [Delegate a domain to Azure DNS](./dns-delegate-domain-azure-dns.md) for instructions on how to configure your name servers for delegation.</span></span> <span data-ttu-id="d4dcf-110">一旦將您的網域委派給您的 Azure DNS 區域，您就能夠設定所需的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-110">Once your domain is delegated to your Azure DNS zone, you are able to configure the DNS records needed.</span></span>

<span data-ttu-id="d4dcf-111">您可以為 [Azure 函數應用程式](#azure-function-app)、[Azure IoT](#azure-iot)、[公用 IP 位址](#public-ip-address)、[App Service (Web Apps)](#app-service-web-apps)、[Blob 儲存體](#blob-storage)、[Azure CDN](#azure-cdn) 設定虛名或自訂網域。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-111">You can configure a vanity or custom domain for [Azure Function Apps](#azure-function-app), [Azure IoT](#azure-iot), [Public IP addresses](#public-ip-address), [App Service (Web Apps)](#app-service-web-apps), [Blob storage](#blob-storage), and [Azure CDN](#azure-cdn).</span></span>

## <a name="azure-function-app"></a><span data-ttu-id="d4dcf-112">Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="d4dcf-112">Azure Function App</span></span>

<span data-ttu-id="d4dcf-113">若要設定 Azure 函式應用程式的自訂網域，建立 CNAME 記錄以及函數應用程式本身的組態需。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-113">To configure a custom domain for Azure function apps, a CNAME record is created as well as configuration on the function app itself.</span></span>
 
<span data-ttu-id="d4dcf-114">瀏覽至 [其他]  >  [函數應用程式]，選取您的函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-114">Navigate to **Other** > **Function App** and select your Function App.</span></span> <span data-ttu-id="d4dcf-115">按一下 [平台功能]，然後按一下 [網路] 下方的[自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-115">Click **Platform features** and under **NETWORKING** click **Custom domains**.</span></span>

![函數應用程式刀鋒視窗](./media/dns-custom-domain/functionapp.png)

<span data-ttu-id="d4dcf-117">記下眼前 [自訂網域] 刀鋒視窗中的 URL，這個位址要作為建立之 DNS 記錄的別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-117">Note the current url on the **Custom domains** blade, this address is used as the alias for the DNS record created.</span></span>

![自訂網域刀鋒視窗](./media/dns-custom-domain/functionshostname.png)

<span data-ttu-id="d4dcf-119">瀏覽至您的 DNS 區域，按一下 [+ 記錄集]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-119">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="d4dcf-120">填寫 [新增記錄集] 刀鋒視窗中的資訊，然後按一下 [確定] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-120">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>

|<span data-ttu-id="d4dcf-121">屬性</span><span class="sxs-lookup"><span data-stu-id="d4dcf-121">Property</span></span>  |<span data-ttu-id="d4dcf-122">值</span><span class="sxs-lookup"><span data-stu-id="d4dcf-122">Value</span></span>  |<span data-ttu-id="d4dcf-123">描述</span><span class="sxs-lookup"><span data-stu-id="d4dcf-123">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="d4dcf-124">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dcf-124">Name</span></span>     | <span data-ttu-id="d4dcf-125">myFunctionApp</span><span class="sxs-lookup"><span data-stu-id="d4dcf-125">myfunctionapp</span></span>        | <span data-ttu-id="d4dcf-126">這個值以及網域名稱標籤是自訂網域名稱的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-126">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="d4dcf-127">類型</span><span class="sxs-lookup"><span data-stu-id="d4dcf-127">Type</span></span>     | <span data-ttu-id="d4dcf-128">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4dcf-128">CNAME</span></span>        | <span data-ttu-id="d4dcf-129">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-129">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="d4dcf-130">TTL</span><span class="sxs-lookup"><span data-stu-id="d4dcf-130">TTL</span></span>     | <span data-ttu-id="d4dcf-131">1</span><span class="sxs-lookup"><span data-stu-id="d4dcf-131">1</span></span>        | <span data-ttu-id="d4dcf-132">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-132">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="d4dcf-133">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-133">TTL unit</span></span>     | <span data-ttu-id="d4dcf-134">小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-134">Hours</span></span>        | <span data-ttu-id="d4dcf-135">使用小時作為時間量值單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-135">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="d4dcf-136">Alias</span><span class="sxs-lookup"><span data-stu-id="d4dcf-136">Alias</span></span>     | <span data-ttu-id="d4dcf-137">adatumfunction.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="d4dcf-137">adatumfunction.azurewebsites.net</span></span>        | <span data-ttu-id="d4dcf-138">您正在為其建立別名的 DNS 名稱，在此範例中是 adatumfunction.azurewebsites.net (預設提供給函數應用程式的 DNS 名稱)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-138">The DNS name you are creating the alias for, in this example it is the adatumfunction.azurewebsites.net DNS name provided by default to the function app.</span></span>        |

<span data-ttu-id="d4dcf-139">瀏覽回到您的函數應用程式，按一下 [平台功能]，再按一下 [網路] 下的 [自訂網域]，然後按一下[主機名稱] 下的 [+ 新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-139">Navigate back to your function app, click **Platform features**, and under **NETWORKING** click **Custom domains**, then under **Hostnames** click **+ Add hostname**.</span></span>

<span data-ttu-id="d4dcf-140">在 [新增主機名稱] 刀鋒視窗的 [主機名稱] 文字欄位中輸入 CNAME 記錄，然後按一下 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-140">On the **Add hostname** blade, enter the CNAME record in the **hostname** text field and click **Validate**.</span></span> <span data-ttu-id="d4dcf-141">如果能夠找到記錄，就會出現 [新增主機名稱] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-141">If the record was able to be found, the **Add hostname** button appears.</span></span> <span data-ttu-id="d4dcf-142">按一下 [新增主機名稱] 以新增別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-142">Click **Add hostname** to add the alias.</span></span>

![函數應用程式的新增主機名稱刀鋒視窗](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a><span data-ttu-id="d4dcf-144">Azure IoT</span><span class="sxs-lookup"><span data-stu-id="d4dcf-144">Azure IoT</span></span>

<span data-ttu-id="d4dcf-145">Azure IoT 沒有服務本身所需的任何自訂。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-145">Azure IoT does not have any customizations that are needed on the service itself.</span></span> <span data-ttu-id="d4dcf-146">若要搭配使用自訂網域與 IoT 中樞，只需要一筆指向資源的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-146">To use a custom domain with an IoT Hub only a CNAME record pointed to the resources is needed.</span></span>

<span data-ttu-id="d4dcf-147">瀏覽至 [物聯網]  >  [IoT 中樞]，選取您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-147">Navigate to **Internet of Things** > **IoT Hub** and select your IoT hub.</span></span> <span data-ttu-id="d4dcf-148">在 [概觀] 刀鋒視窗中，請注意 IoT 中樞的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-148">On the **Overview** blade, note the FQDN of the IoT hub.</span></span>

![IoT 中樞刀鋒視窗](./media/dns-custom-domain/iot.png)

<span data-ttu-id="d4dcf-150">接下來，瀏覽至您的 DNS 區域，按一下 [+ 記錄集]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-150">Next, navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="d4dcf-151">填寫 [新增記錄集] 刀鋒視窗中的資訊，然後按一下 [確定] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-151">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="d4dcf-152">屬性</span><span class="sxs-lookup"><span data-stu-id="d4dcf-152">Property</span></span>  |<span data-ttu-id="d4dcf-153">值</span><span class="sxs-lookup"><span data-stu-id="d4dcf-153">Value</span></span>  |<span data-ttu-id="d4dcf-154">描述</span><span class="sxs-lookup"><span data-stu-id="d4dcf-154">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="d4dcf-155">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dcf-155">Name</span></span>     | <span data-ttu-id="d4dcf-156">myiothub</span><span class="sxs-lookup"><span data-stu-id="d4dcf-156">myiothub</span></span>        | <span data-ttu-id="d4dcf-157">這個值以及網域名稱標籤是 IoT 中樞的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-157">This value along with the domain name label is the FQDN for the IoT hub.</span></span>        |
|<span data-ttu-id="d4dcf-158">類型</span><span class="sxs-lookup"><span data-stu-id="d4dcf-158">Type</span></span>     | <span data-ttu-id="d4dcf-159">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4dcf-159">CNAME</span></span>        | <span data-ttu-id="d4dcf-160">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-160">Use a CNAME record is using an alias.</span></span>
|<span data-ttu-id="d4dcf-161">TTL</span><span class="sxs-lookup"><span data-stu-id="d4dcf-161">TTL</span></span>     | <span data-ttu-id="d4dcf-162">1</span><span class="sxs-lookup"><span data-stu-id="d4dcf-162">1</span></span>        | <span data-ttu-id="d4dcf-163">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-163">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="d4dcf-164">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-164">TTL unit</span></span>     | <span data-ttu-id="d4dcf-165">小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-165">Hours</span></span>        | <span data-ttu-id="d4dcf-166">使用小時作為時間量值單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-166">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="d4dcf-167">Alias</span><span class="sxs-lookup"><span data-stu-id="d4dcf-167">Alias</span></span>     | <span data-ttu-id="d4dcf-168">adatumIOT.azure-devices.net</span><span class="sxs-lookup"><span data-stu-id="d4dcf-168">adatumIOT.azure-devices.net</span></span>        | <span data-ttu-id="d4dcf-169">您正在為其建立別名的 DNS 名稱，在此範例中是 adatumIOT.azure-devices.net (IoT 中樞提供的主機名稱)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-169">The DNS name you are creating the alias for, in this example it is the adatumIOT.azure-devices.net host name provided by the IoT hub.</span></span>

<span data-ttu-id="d4dcf-170">建立記錄之後，使用 `nslookup` 測試 CNAME 記錄的名稱解析</span><span class="sxs-lookup"><span data-stu-id="d4dcf-170">Once the record is created, test name resolution with the CNAME record using `nslookup`</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="d4dcf-171">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d4dcf-171">Public IP address</span></span>

<span data-ttu-id="d4dcf-172">如果服務使用公用 IP 位址資源 (例如，應用程式閘道、負載平衡器、雲端服務、Resource Manager 的 VM、傳統 VM)，若要設定此種服務的自訂網域，則要使用 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-172">To configure a custom domain for services that use a public IP address resource such as Application Gateway, Load Balancer, Cloud Service, Resource Manager VMs, and, Classic VMs, a CNAME record used.</span></span>

<span data-ttu-id="d4dcf-173">瀏覽至 [網路]  >  [公用 IP 位址]，選取公用 IP 資源，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-173">Navigate to **Networking** > **Public IP address**, select the Public IP resource and click **Configuration**.</span></span> <span data-ttu-id="d4dcf-174">記下顯示的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-174">Notate the IP address shown.</span></span>

![公用 IP 刀鋒視窗](./media/dns-custom-domain/publicip.png)

<span data-ttu-id="d4dcf-176">瀏覽至您的 DNS 區域，按一下 [+ 記錄集]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-176">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="d4dcf-177">填寫 [新增記錄集] 刀鋒視窗中的資訊，然後按一下 [確定] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-177">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="d4dcf-178">屬性</span><span class="sxs-lookup"><span data-stu-id="d4dcf-178">Property</span></span>  |<span data-ttu-id="d4dcf-179">值</span><span class="sxs-lookup"><span data-stu-id="d4dcf-179">Value</span></span>  |<span data-ttu-id="d4dcf-180">描述</span><span class="sxs-lookup"><span data-stu-id="d4dcf-180">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="d4dcf-181">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dcf-181">Name</span></span>     | <span data-ttu-id="d4dcf-182">mywebserver</span><span class="sxs-lookup"><span data-stu-id="d4dcf-182">mywebserver</span></span>        | <span data-ttu-id="d4dcf-183">這個值以及網域名稱標籤是自訂網域名稱的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-183">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="d4dcf-184">類型</span><span class="sxs-lookup"><span data-stu-id="d4dcf-184">Type</span></span>     | <span data-ttu-id="d4dcf-185">A</span><span class="sxs-lookup"><span data-stu-id="d4dcf-185">A</span></span>        | <span data-ttu-id="d4dcf-186">使用 A 記錄，因為該資源是 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-186">Use an A record as the resource is an IP address.</span></span>        |
|<span data-ttu-id="d4dcf-187">TTL</span><span class="sxs-lookup"><span data-stu-id="d4dcf-187">TTL</span></span>     | <span data-ttu-id="d4dcf-188">1</span><span class="sxs-lookup"><span data-stu-id="d4dcf-188">1</span></span>        | <span data-ttu-id="d4dcf-189">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-189">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="d4dcf-190">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-190">TTL unit</span></span>     | <span data-ttu-id="d4dcf-191">小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-191">Hours</span></span>        | <span data-ttu-id="d4dcf-192">使用小時作為時間量值單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-192">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="d4dcf-193">IP 位址</span><span class="sxs-lookup"><span data-stu-id="d4dcf-193">IP Address</span></span>     | <your ip address>       | <span data-ttu-id="d4dcf-194">公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-194">The public IP address.</span></span>|

![建立 A 記錄](./media/dns-custom-domain/arecord.png)

<span data-ttu-id="d4dcf-196">一旦建立 A 記錄，執行 `nslookup` 驗證記錄解析。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-196">Once the A record is created, run `nslookup` to validate the record resolves.</span></span>

![公用 IP DNS 查閱](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a><span data-ttu-id="d4dcf-198">App Service (Web Apps)</span><span class="sxs-lookup"><span data-stu-id="d4dcf-198">App Service (Web Apps)</span></span>

<span data-ttu-id="d4dcf-199">以下步驟引導您設定 App Service Web 應用程式的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-199">The following steps take you through configuring a custom domain for an app service web app.</span></span>

<span data-ttu-id="d4dcf-200">瀏覽至 [Web 與行動]  >  [App Service]，選取您要設定自訂網域名稱的資源，然後按一下 [自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-200">Navigate to **Web & Mobile** > **App Service** and select the resource you are configuring a custom domain name, and click **Custom domains**.</span></span>

<span data-ttu-id="d4dcf-201">記下眼前 [自訂網域] 刀鋒視窗中的 URL，這個位址要作為建立之 DNS 記錄的別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-201">Note the current url on the **Custom domains** blade, this address is used as the alias for the DNS record created.</span></span>

![自訂網域刀鋒視窗](./media/dns-custom-domain/url.png)

<span data-ttu-id="d4dcf-203">瀏覽至您的 DNS 區域，按一下 [+ 記錄集]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-203">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="d4dcf-204">填寫 [新增記錄集] 刀鋒視窗中的資訊，然後按一下 [確定] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-204">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="d4dcf-205">屬性</span><span class="sxs-lookup"><span data-stu-id="d4dcf-205">Property</span></span>  |<span data-ttu-id="d4dcf-206">值</span><span class="sxs-lookup"><span data-stu-id="d4dcf-206">Value</span></span>  |<span data-ttu-id="d4dcf-207">描述</span><span class="sxs-lookup"><span data-stu-id="d4dcf-207">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="d4dcf-208">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dcf-208">Name</span></span>     | <span data-ttu-id="d4dcf-209">mywebserver</span><span class="sxs-lookup"><span data-stu-id="d4dcf-209">mywebserver</span></span>        | <span data-ttu-id="d4dcf-210">這個值以及網域名稱標籤是自訂網域名稱的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-210">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="d4dcf-211">類型</span><span class="sxs-lookup"><span data-stu-id="d4dcf-211">Type</span></span>     | <span data-ttu-id="d4dcf-212">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4dcf-212">CNAME</span></span>        | <span data-ttu-id="d4dcf-213">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-213">Use a CNAME record is using an alias.</span></span> <span data-ttu-id="d4dcf-214">如果資源使用 IP 位址，就會使用 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-214">If the resource used an IP address, an A record would be used.</span></span>        |
|<span data-ttu-id="d4dcf-215">TTL</span><span class="sxs-lookup"><span data-stu-id="d4dcf-215">TTL</span></span>     | <span data-ttu-id="d4dcf-216">1</span><span class="sxs-lookup"><span data-stu-id="d4dcf-216">1</span></span>        | <span data-ttu-id="d4dcf-217">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-217">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="d4dcf-218">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-218">TTL unit</span></span>     | <span data-ttu-id="d4dcf-219">小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-219">Hours</span></span>        | <span data-ttu-id="d4dcf-220">使用小時作為時間量值單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-220">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="d4dcf-221">Alias</span><span class="sxs-lookup"><span data-stu-id="d4dcf-221">Alias</span></span>     | <span data-ttu-id="d4dcf-222">webserver.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="d4dcf-222">webserver.azurewebsites.net</span></span>        | <span data-ttu-id="d4dcf-223">您正在為其建立別名的 DNS 名稱，在此範例中是 webserver.azurewebsites.net (預設提供給 Web 應用程式的 DNS 名稱)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-223">The DNS name you are creating the alias for, in this example it is the webserver.azurewebsites.net DNS name provided by default to the web app.</span></span>        |


![建立 CNAME 記錄](./media/dns-custom-domain/createcnamerecord.png)

<span data-ttu-id="d4dcf-225">瀏覽回到設定自訂網域名稱的 App Service。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-225">Navigate back to the app service that is configured for the custom domain name.</span></span> <span data-ttu-id="d4dcf-226">按一下 [自訂網域] ，然後按一下 [主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-226">Click **Custom domains**, then click **Hostnames**.</span></span> <span data-ttu-id="d4dcf-227">若要新增您所建立的 CNAME 記錄，按一下 [+ 新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-227">To add the CNAME record you created, click **+ Add hostname**.</span></span>

![圖 1](./media/dns-custom-domain/figure1.png)

<span data-ttu-id="d4dcf-229">處理程序完成之後，執行**nslookup** 驗證名稱解析的運作。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-229">Once the process is complete, run **nslookup** to validate name resolution is working.</span></span>

![圖 1](./media/dns-custom-domain/finalnslookup.png)

<span data-ttu-id="d4dcf-231">若要深入了解自訂網域對應至 App Service，請造訪[將現有的自訂 DNS 名稱對應至 Azure Web Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-231">To learn more about mapping a custom domain to App Service, visit [Map an existing custom DNS name to Azure Web Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).</span></span>

<span data-ttu-id="d4dcf-232">如果您需要購買自訂網域，請造訪[購買 Azure Web Apps 的自訂網域名稱](../app-service-web/custom-dns-web-site-buydomains-web-app.md)，以深入了解 App Service 網域。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-232">If you need to purchase a custom domain, visit [Buy a custom domain name for Azure Web Apps](../app-service-web/custom-dns-web-site-buydomains-web-app.md) to learn more about App Service domains.</span></span>

## <a name="blob-storage"></a><span data-ttu-id="d4dcf-233">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d4dcf-233">Blob storage</span></span>

<span data-ttu-id="d4dcf-234">下列步驟引導您使用 asverify 方法設定 blob 儲存體帳戶的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-234">The following steps take you through configuring a CNAME record for a blob storage account using the asverify method.</span></span> <span data-ttu-id="d4dcf-235">這個方法可確保沒有任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-235">This method ensures there is no downtime.</span></span>

<span data-ttu-id="d4dcf-236">瀏覽至 [儲存體]  >  [儲存體帳戶]，選取您的儲存體帳戶，然後選取 [自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-236">Navigate to **Storage** > **Storage Accounts**, select your storage account, and click **Custom domain**.</span></span> <span data-ttu-id="d4dcf-237">記下步驟 2 的 FQDN，這個值用來建立第一筆 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="d4dcf-237">Notate the FQDN under step 2, this value is used to create the first CNAME record</span></span>

![Blob 儲存體自訂網域](./media/dns-custom-domain/blobcustomdomain.png)

<span data-ttu-id="d4dcf-239">瀏覽至您的 DNS 區域，按一下 [+ 記錄集]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-239">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="d4dcf-240">填寫 [新增記錄集] 刀鋒視窗中的資訊，然後按一下 [確定] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-240">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>


|<span data-ttu-id="d4dcf-241">屬性</span><span class="sxs-lookup"><span data-stu-id="d4dcf-241">Property</span></span>  |<span data-ttu-id="d4dcf-242">值</span><span class="sxs-lookup"><span data-stu-id="d4dcf-242">Value</span></span>  |<span data-ttu-id="d4dcf-243">描述</span><span class="sxs-lookup"><span data-stu-id="d4dcf-243">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="d4dcf-244">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dcf-244">Name</span></span>     | <span data-ttu-id="d4dcf-245">asverify.mystorageaccount</span><span class="sxs-lookup"><span data-stu-id="d4dcf-245">asverify.mystorageaccount</span></span>        | <span data-ttu-id="d4dcf-246">這個值以及網域名稱標籤是自訂網域名稱的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-246">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="d4dcf-247">類型</span><span class="sxs-lookup"><span data-stu-id="d4dcf-247">Type</span></span>     | <span data-ttu-id="d4dcf-248">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4dcf-248">CNAME</span></span>        | <span data-ttu-id="d4dcf-249">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-249">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="d4dcf-250">TTL</span><span class="sxs-lookup"><span data-stu-id="d4dcf-250">TTL</span></span>     | <span data-ttu-id="d4dcf-251">1</span><span class="sxs-lookup"><span data-stu-id="d4dcf-251">1</span></span>        | <span data-ttu-id="d4dcf-252">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-252">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="d4dcf-253">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-253">TTL unit</span></span>     | <span data-ttu-id="d4dcf-254">小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-254">Hours</span></span>        | <span data-ttu-id="d4dcf-255">使用小時作為時間量值單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-255">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="d4dcf-256">Alias</span><span class="sxs-lookup"><span data-stu-id="d4dcf-256">Alias</span></span>     | <span data-ttu-id="d4dcf-257">asverify.adatumfunctiona9ed.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d4dcf-257">asverify.adatumfunctiona9ed.blob.core.windows.net</span></span>        | <span data-ttu-id="d4dcf-258">您正在為其建立別名的 DNS 名稱，在此範例中是 asverify.adatumfunctiona9ed.blob.core.windows.net (預設提供給儲存體帳戶的 DNS 名稱)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-258">The DNS name you are creating the alias for, in this example it is the asverify.adatumfunctiona9ed.blob.core.windows.net DNS name provided by default to the storage account.</span></span>        |

<span data-ttu-id="d4dcf-259">按一下 [儲存體]  >  [儲存體帳戶] 以回到您的儲存體帳戶，選取您的儲存體帳戶，然後選取 [自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-259">Navigate back to your storage account by clicking **Storage** > **Storage Accounts**, select your storage account and click **Custom domain**.</span></span> <span data-ttu-id="d4dcf-260">在文字方塊中輸入您建立的別名但不含 asverify 前置詞，核取 [使用間接 CNAME 驗證]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-260">Type in the alias you created without the asverify prefix in the text box, check **Use indirect CNAME validation, and click **Save**.</span></span> <span data-ttu-id="d4dcf-261">一旦完成這個步驟，返回您的 DNS 區域，建立不含 asverify 前置詞的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-261">Once this step is complete, return to your DNS zone and create a CNAME record without the asverify prefix.</span></span>  <span data-ttu-id="d4dcf-262">此時，您就可以放心刪除具有 cdnverify 前置詞的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-262">After that point, you are safe to delete the CNAME record with the cdnverify prefix.</span></span>

![Blob 儲存體自訂網域](./media/dns-custom-domain/indirectvalidate.png)

<span data-ttu-id="d4dcf-264">執行 `nslookup` 驗證 DNS 解析</span><span class="sxs-lookup"><span data-stu-id="d4dcf-264">Validate DNS resolution by running `nslookup`</span></span>

<span data-ttu-id="d4dcf-265">若要深入了解自訂網域對應至 Blob 儲存體，請造訪[為您的 Blob 儲存體端點設定自訂網域名稱](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-265">To learn more about mapping a custom domain to a blob storage endpoint visit [Configure a custom domain name for your Blob storage endpoint](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)</span></span>

## <a name="azure-cdn"></a><span data-ttu-id="d4dcf-266">Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d4dcf-266">Azure CDN</span></span>

<span data-ttu-id="d4dcf-267">下列步驟引導您使用 asverify 方法設定 CDN 端點的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-267">The following steps take you through configuring a CNAME record for a CDN endpoint using the cdnverify method.</span></span> <span data-ttu-id="d4dcf-268">這個方法可確保沒有任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-268">This method ensures there is no downtime.</span></span>

<span data-ttu-id="d4dcf-269">瀏覽至 [網路]  >  [CDN 設定檔]，選取您的 CDN 設定檔，然後按一下 [一般] 下的 [端點]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-269">Navigate to **Networking** > **CDN Profiles**, select your CDN profile, and click **Endpoints** under **General**.</span></span>

<span data-ttu-id="d4dcf-270">選取您使用的端點，按一下 [+ 自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-270">Select the endpoint you are working with and click **+ Custom domain**.</span></span> <span data-ttu-id="d4dcf-271">請注意 [端點主機名稱]，因為這個值是 CNAME 記錄指向的記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-271">Note the **Endpoint hostname** as this value is the record that the CNAME record points to.</span></span>

![CDN 自訂網域](./media/dns-custom-domain/endpointcustomdomain.png)

<span data-ttu-id="d4dcf-273">瀏覽至您的 DNS 區域，按一下 [+ 記錄集]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-273">Navigate to your DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="d4dcf-274">填寫 [新增記錄集] 刀鋒視窗中的資訊，然後按一下 [確定] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-274">Fill out the following information on the **Add record set** blade and click **OK** to create it.</span></span>

|<span data-ttu-id="d4dcf-275">屬性</span><span class="sxs-lookup"><span data-stu-id="d4dcf-275">Property</span></span>  |<span data-ttu-id="d4dcf-276">值</span><span class="sxs-lookup"><span data-stu-id="d4dcf-276">Value</span></span>  |<span data-ttu-id="d4dcf-277">描述</span><span class="sxs-lookup"><span data-stu-id="d4dcf-277">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="d4dcf-278">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dcf-278">Name</span></span>     | <span data-ttu-id="d4dcf-279">cdnverify.mycdnendpoint</span><span class="sxs-lookup"><span data-stu-id="d4dcf-279">cdnverify.mycdnendpoint</span></span>        | <span data-ttu-id="d4dcf-280">這個值以及網域名稱標籤是自訂網域名稱的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-280">This value along with the domain name label is the FQDN for the custom domain name.</span></span>        |
|<span data-ttu-id="d4dcf-281">類型</span><span class="sxs-lookup"><span data-stu-id="d4dcf-281">Type</span></span>     | <span data-ttu-id="d4dcf-282">CNAME</span><span class="sxs-lookup"><span data-stu-id="d4dcf-282">CNAME</span></span>        | <span data-ttu-id="d4dcf-283">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-283">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="d4dcf-284">TTL</span><span class="sxs-lookup"><span data-stu-id="d4dcf-284">TTL</span></span>     | <span data-ttu-id="d4dcf-285">1</span><span class="sxs-lookup"><span data-stu-id="d4dcf-285">1</span></span>        | <span data-ttu-id="d4dcf-286">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-286">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="d4dcf-287">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-287">TTL unit</span></span>     | <span data-ttu-id="d4dcf-288">小時</span><span class="sxs-lookup"><span data-stu-id="d4dcf-288">Hours</span></span>        | <span data-ttu-id="d4dcf-289">使用小時作為時間量值單位</span><span class="sxs-lookup"><span data-stu-id="d4dcf-289">Hours are used as the time measurement</span></span>         |
|<span data-ttu-id="d4dcf-290">Alias</span><span class="sxs-lookup"><span data-stu-id="d4dcf-290">Alias</span></span>     | <span data-ttu-id="d4dcf-291">cdnverify.adatumcdnendpoint.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d4dcf-291">cdnverify.adatumcdnendpoint.azureedge.net</span></span>        | <span data-ttu-id="d4dcf-292">您正在為其建立別名的 DNS 名稱，在此範例中是 cdnverify.adatumcdnendpoint.azureedge.net (預設提供給儲存體帳戶的 DNS 名稱)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-292">The DNS name you are creating the alias for, in this example it is the cdnverify.adatumcdnendpoint.azureedge.net DNS name provided by default to the storage account.</span></span>        |

<span data-ttu-id="d4dcf-293">按一下 [網路]  >  [CDN 設定檔] 以回到您的 CDN端點，選取您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-293">Navigate back to your CDN endpoint by clicking **Networking** > **CDN Profiles**, and select your CDN profile.</span></span> <span data-ttu-id="d4dcf-294">按一下 [+ 自訂網域] 並輸入您的 CNAME 記錄別名但不含 cdnverify 前置詞，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-294">Click **+ Custom domain** and enter your CNAME record alias without the cdnverify prefix and click **Add**.</span></span>

<span data-ttu-id="d4dcf-295">一旦完成這個步驟，返回您的 DNS 區域，建立不含 asverify 前置詞的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-295">Once this step is complete, return to your DNS zone and create a CNAME record without the cdnverify prefix.</span></span>  <span data-ttu-id="d4dcf-296">此時，您就可以放心刪除具有 cdnverify 前置詞的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-296">After that point, you are safe to delete the CNAME record with the cdnverify prefix.</span></span> <span data-ttu-id="d4dcf-297">針對 CDN 以及如何設定自訂網域，而不經過中間註冊步驟，如需詳細資訊請造訪[將 Azure CDN 內容對應至自訂網域](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-297">For more information on CDN and how to configure a custom domain without the intermediate registration step visit [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4dcf-298">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4dcf-298">Next steps</span></span>

<span data-ttu-id="d4dcf-299">了解如何[為 Azure 裝載的服務設定反向 DNS](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dcf-299">Learn how to [configure reverse DNS for services hosted in Azure](dns-reverse-dns-for-azure-services.md).</span></span>