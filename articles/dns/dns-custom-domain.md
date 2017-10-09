---
title: "您的 Azure 資源與 aaaIntegrate Azure DNS |Microsoft 文件"
description: "深入了解如何為您的 Azure 資源的 DNS tooprovide 沿著 toouse Azure DNS。"
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
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a><span data-ttu-id="ec5ab-103">針對一項 Azure 服務使用 Azure DNS tooprovide 自訂網域設定</span><span class="sxs-lookup"><span data-stu-id="ec5ab-103">Use Azure DNS tooprovide custom domain settings for an Azure service</span></span>

<span data-ttu-id="ec5ab-104">Azure DNS 提供自訂網域的 DNS，可用於任何支援自訂網域或具有完整網域名稱 (FQDN) 的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-104">Azure DNS provides DNS for a custom domain for any of your Azure resources that support custom domains or that have a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="ec5ab-105">範例是您 Azure web 應用程式，您想要使用者 tooaccess 它透過使用 contoso.com 或 www.contoso.com 當做 FQDN。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-105">An example is you have an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span> <span data-ttu-id="ec5ab-106">本文章會引導您使用 Azure DNS 設定您的 Azure 服務，以便使用自訂網域。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-106">This article walks you through configuring your Azure service with Azure DNS for using custom domains.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec5ab-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ec5ab-107">Prerequisites</span></span>

<span data-ttu-id="ec5ab-108">在您的自訂網域的順序 toouse Azure DNS，您必須先委派您網域 tooAzure DNS。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-108">In order toouse Azure DNS for your custom domain, you must first delegate your domain tooAzure DNS.</span></span> <span data-ttu-id="ec5ab-109">請瀏覽[委派網域 tooAzure DNS](./dns-delegate-domain-azure-dns.md)如需有關指示 tooconfigure 名稱伺服器進行委派。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-109">Visit [Delegate a domain tooAzure DNS](./dns-delegate-domain-azure-dns.md) for instructions on how tooconfigure your name servers for delegation.</span></span> <span data-ttu-id="ec5ab-110">一旦您的網域委派的 tooyour Azure DNS 區域，您就可以 tooconfigure hello DNS 記錄所需。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-110">Once your domain is delegated tooyour Azure DNS zone, you are able tooconfigure hello DNS records needed.</span></span>

<span data-ttu-id="ec5ab-111">您可以為 [Azure 函數應用程式](#azure-function-app)、[Azure IoT](#azure-iot)、[公用 IP 位址](#public-ip-address)、[App Service (Web Apps)](#app-service-web-apps)、[Blob 儲存體](#blob-storage)、[Azure CDN](#azure-cdn) 設定虛名或自訂網域。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-111">You can configure a vanity or custom domain for [Azure Function Apps](#azure-function-app), [Azure IoT](#azure-iot), [Public IP addresses](#public-ip-address), [App Service (Web Apps)](#app-service-web-apps), [Blob storage](#blob-storage), and [Azure CDN](#azure-cdn).</span></span>

## <a name="azure-function-app"></a><span data-ttu-id="ec5ab-112">Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="ec5ab-112">Azure Function App</span></span>

<span data-ttu-id="ec5ab-113">tooconfigure Azure 函式應用程式的自訂網域，以及在 hello 函式應用程式本身的組態建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-113">tooconfigure a custom domain for Azure function apps, a CNAME record is created as well as configuration on hello function app itself.</span></span>
 
<span data-ttu-id="ec5ab-114">瀏覽過**其他** > **函式應用程式**並選取您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-114">Navigate too**Other** > **Function App** and select your Function App.</span></span> <span data-ttu-id="ec5ab-115">按一下 [平台功能]，然後按一下 [網路] 下方的[自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-115">Click **Platform features** and under **NETWORKING** click **Custom domains**.</span></span>

![函數應用程式刀鋒視窗](./media/dns-custom-domain/functionapp.png)

<span data-ttu-id="ec5ab-117">請注意在 hello hello 目前 url**自訂網域**刀鋒視窗中，此位址作為 hello 別名建立 hello DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-117">Note hello current url on hello **Custom domains** blade, this address is used as hello alias for hello DNS record created.</span></span>

![自訂網域刀鋒視窗](./media/dns-custom-domain/functionshostname.png)

<span data-ttu-id="ec5ab-119">瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-119">Navigate tooyour DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="ec5ab-120">填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-120">Fill out hello following information on hello **Add record set** blade and click **OK** toocreate it.</span></span>

|<span data-ttu-id="ec5ab-121">屬性</span><span class="sxs-lookup"><span data-stu-id="ec5ab-121">Property</span></span>  |<span data-ttu-id="ec5ab-122">值</span><span class="sxs-lookup"><span data-stu-id="ec5ab-122">Value</span></span>  |<span data-ttu-id="ec5ab-123">描述</span><span class="sxs-lookup"><span data-stu-id="ec5ab-123">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ec5ab-124">名稱</span><span class="sxs-lookup"><span data-stu-id="ec5ab-124">Name</span></span>     | <span data-ttu-id="ec5ab-125">myFunctionApp</span><span class="sxs-lookup"><span data-stu-id="ec5ab-125">myfunctionapp</span></span>        | <span data-ttu-id="ec5ab-126">Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-126">This value along with hello domain name label is hello FQDN for hello custom domain name.</span></span>        |
|<span data-ttu-id="ec5ab-127">類型</span><span class="sxs-lookup"><span data-stu-id="ec5ab-127">Type</span></span>     | <span data-ttu-id="ec5ab-128">CNAME</span><span class="sxs-lookup"><span data-stu-id="ec5ab-128">CNAME</span></span>        | <span data-ttu-id="ec5ab-129">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-129">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="ec5ab-130">TTL</span><span class="sxs-lookup"><span data-stu-id="ec5ab-130">TTL</span></span>     | <span data-ttu-id="ec5ab-131">1</span><span class="sxs-lookup"><span data-stu-id="ec5ab-131">1</span></span>        | <span data-ttu-id="ec5ab-132">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-132">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="ec5ab-133">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="ec5ab-133">TTL unit</span></span>     | <span data-ttu-id="ec5ab-134">小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-134">Hours</span></span>        | <span data-ttu-id="ec5ab-135">時數會做為 hello 時間度量</span><span class="sxs-lookup"><span data-stu-id="ec5ab-135">Hours are used as hello time measurement</span></span>         |
|<span data-ttu-id="ec5ab-136">Alias</span><span class="sxs-lookup"><span data-stu-id="ec5ab-136">Alias</span></span>     | <span data-ttu-id="ec5ab-137">adatumfunction.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ec5ab-137">adatumfunction.azurewebsites.net</span></span>        | <span data-ttu-id="ec5ab-138">hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello 函式應用程式所提供的 hello adatumfunction.azurewebsites.net DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-138">hello DNS name you are creating hello alias for, in this example it is hello adatumfunction.azurewebsites.net DNS name provided by default toohello function app.</span></span>        |

<span data-ttu-id="ec5ab-139">瀏覽後 tooyour 函式應用程式中，按一下**平台功能**，然後在**網路**按一下**自訂網域**，然後在**Hostname**按一下**+ 加入 hostname**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-139">Navigate back tooyour function app, click **Platform features**, and under **NETWORKING** click **Custom domains**, then under **Hostnames** click **+ Add hostname**.</span></span>

<span data-ttu-id="ec5ab-140">在 hello**新增主機名稱**刀鋒視窗中，輸入 hello hello CNAME 記錄**主機名稱**文字欄位，然後按一下**驗證**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-140">On hello **Add hostname** blade, enter hello CNAME record in hello **hostname** text field and click **Validate**.</span></span> <span data-ttu-id="ec5ab-141">如果 hello 記錄無法找到的 toobe，hello**新增主機名稱**按鈕隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-141">If hello record was able toobe found, hello **Add hostname** button appears.</span></span> <span data-ttu-id="ec5ab-142">按一下**新增 hostname** tooadd hello 別名。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-142">Click **Add hostname** tooadd hello alias.</span></span>

![函數應用程式的新增主機名稱刀鋒視窗](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a><span data-ttu-id="ec5ab-144">Azure IoT</span><span class="sxs-lookup"><span data-stu-id="ec5ab-144">Azure IoT</span></span>

<span data-ttu-id="ec5ab-145">Azure IoT 沒有 hello 服務本身所需的任何自訂。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-145">Azure IoT does not have any customizations that are needed on hello service itself.</span></span> <span data-ttu-id="ec5ab-146">toouse 與 IoT 中樞的自訂網域的 CNAME 記錄指向 toohello 資源只需要。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-146">toouse a custom domain with an IoT Hub only a CNAME record pointed toohello resources is needed.</span></span>

<span data-ttu-id="ec5ab-147">瀏覽過**物聯網** > **IoT 中樞**，並選取您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-147">Navigate too**Internet of Things** > **IoT Hub** and select your IoT hub.</span></span> <span data-ttu-id="ec5ab-148">在 hello**概觀**刀鋒視窗中，注意 hello hello IoT 中樞的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-148">On hello **Overview** blade, note hello FQDN of hello IoT hub.</span></span>

![IoT 中樞刀鋒視窗](./media/dns-custom-domain/iot.png)

<span data-ttu-id="ec5ab-150">接下來，瀏覽 tooyour DNS 區域，然後按一下**+ 記錄集**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-150">Next, navigate tooyour DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="ec5ab-151">填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-151">Fill out hello following information on hello **Add record set** blade and click **OK** toocreate it.</span></span>


|<span data-ttu-id="ec5ab-152">屬性</span><span class="sxs-lookup"><span data-stu-id="ec5ab-152">Property</span></span>  |<span data-ttu-id="ec5ab-153">值</span><span class="sxs-lookup"><span data-stu-id="ec5ab-153">Value</span></span>  |<span data-ttu-id="ec5ab-154">描述</span><span class="sxs-lookup"><span data-stu-id="ec5ab-154">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ec5ab-155">名稱</span><span class="sxs-lookup"><span data-stu-id="ec5ab-155">Name</span></span>     | <span data-ttu-id="ec5ab-156">myiothub</span><span class="sxs-lookup"><span data-stu-id="ec5ab-156">myiothub</span></span>        | <span data-ttu-id="ec5ab-157">此值以及 hello 網域名稱標籤為 hello IoT 中樞的 hello FQDN。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-157">This value along with hello domain name label is hello FQDN for hello IoT hub.</span></span>        |
|<span data-ttu-id="ec5ab-158">類型</span><span class="sxs-lookup"><span data-stu-id="ec5ab-158">Type</span></span>     | <span data-ttu-id="ec5ab-159">CNAME</span><span class="sxs-lookup"><span data-stu-id="ec5ab-159">CNAME</span></span>        | <span data-ttu-id="ec5ab-160">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-160">Use a CNAME record is using an alias.</span></span>
|<span data-ttu-id="ec5ab-161">TTL</span><span class="sxs-lookup"><span data-stu-id="ec5ab-161">TTL</span></span>     | <span data-ttu-id="ec5ab-162">1</span><span class="sxs-lookup"><span data-stu-id="ec5ab-162">1</span></span>        | <span data-ttu-id="ec5ab-163">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-163">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="ec5ab-164">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="ec5ab-164">TTL unit</span></span>     | <span data-ttu-id="ec5ab-165">小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-165">Hours</span></span>        | <span data-ttu-id="ec5ab-166">時數會做為 hello 時間度量</span><span class="sxs-lookup"><span data-stu-id="ec5ab-166">Hours are used as hello time measurement</span></span>         |
|<span data-ttu-id="ec5ab-167">Alias</span><span class="sxs-lookup"><span data-stu-id="ec5ab-167">Alias</span></span>     | <span data-ttu-id="ec5ab-168">adatumIOT.azure-devices.net</span><span class="sxs-lookup"><span data-stu-id="ec5ab-168">adatumIOT.azure-devices.net</span></span>        | <span data-ttu-id="ec5ab-169">hello DNS 名稱建立 hello 別名，在此範例中是 hello IoT 中心所提供的 hello adatumIOT.azure devices.net 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-169">hello DNS name you are creating hello alias for, in this example it is hello adatumIOT.azure-devices.net host name provided by hello IoT hub.</span></span>

<span data-ttu-id="ec5ab-170">一旦建立 hello 記錄時，測試與 hello CNAME 記錄使用名稱解析`nslookup`</span><span class="sxs-lookup"><span data-stu-id="ec5ab-170">Once hello record is created, test name resolution with hello CNAME record using `nslookup`</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="ec5ab-171">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ec5ab-171">Public IP address</span></span>

<span data-ttu-id="ec5ab-172">tooconfigure 自訂網域，以服務的公用 IP 位址資源，例如應用程式閘道，負載平衡器，雲端服務，資源管理員的 Vm，並使用傳統的 Vm，CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-172">tooconfigure a custom domain for services that use a public IP address resource such as Application Gateway, Load Balancer, Cloud Service, Resource Manager VMs, and, Classic VMs, a CNAME record used.</span></span>

<span data-ttu-id="ec5ab-173">瀏覽過**網路** > **公用 IP 位址**、 選取 hello 公用 IP 資源，然後按一下 **組態**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-173">Navigate too**Networking** > **Public IP address**, select hello Public IP resource and click **Configuration**.</span></span> <span data-ttu-id="ec5ab-174">Notate hello 所顯示的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-174">Notate hello IP address shown.</span></span>

![公用 IP 刀鋒視窗](./media/dns-custom-domain/publicip.png)

<span data-ttu-id="ec5ab-176">瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-176">Navigate tooyour DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="ec5ab-177">填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-177">Fill out hello following information on hello **Add record set** blade and click **OK** toocreate it.</span></span>


|<span data-ttu-id="ec5ab-178">屬性</span><span class="sxs-lookup"><span data-stu-id="ec5ab-178">Property</span></span>  |<span data-ttu-id="ec5ab-179">值</span><span class="sxs-lookup"><span data-stu-id="ec5ab-179">Value</span></span>  |<span data-ttu-id="ec5ab-180">描述</span><span class="sxs-lookup"><span data-stu-id="ec5ab-180">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ec5ab-181">名稱</span><span class="sxs-lookup"><span data-stu-id="ec5ab-181">Name</span></span>     | <span data-ttu-id="ec5ab-182">mywebserver</span><span class="sxs-lookup"><span data-stu-id="ec5ab-182">mywebserver</span></span>        | <span data-ttu-id="ec5ab-183">Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-183">This value along with hello domain name label is hello FQDN for hello custom domain name.</span></span>        |
|<span data-ttu-id="ec5ab-184">類型</span><span class="sxs-lookup"><span data-stu-id="ec5ab-184">Type</span></span>     | <span data-ttu-id="ec5ab-185">A</span><span class="sxs-lookup"><span data-stu-id="ec5ab-185">A</span></span>        | <span data-ttu-id="ec5ab-186">使用 A 記錄，因為 hello 資源是 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-186">Use an A record as hello resource is an IP address.</span></span>        |
|<span data-ttu-id="ec5ab-187">TTL</span><span class="sxs-lookup"><span data-stu-id="ec5ab-187">TTL</span></span>     | <span data-ttu-id="ec5ab-188">1</span><span class="sxs-lookup"><span data-stu-id="ec5ab-188">1</span></span>        | <span data-ttu-id="ec5ab-189">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-189">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="ec5ab-190">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="ec5ab-190">TTL unit</span></span>     | <span data-ttu-id="ec5ab-191">小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-191">Hours</span></span>        | <span data-ttu-id="ec5ab-192">時數會做為 hello 時間度量</span><span class="sxs-lookup"><span data-stu-id="ec5ab-192">Hours are used as hello time measurement</span></span>         |
|<span data-ttu-id="ec5ab-193">IP 位址</span><span class="sxs-lookup"><span data-stu-id="ec5ab-193">IP Address</span></span>     | <your ip address>       | <span data-ttu-id="ec5ab-194">hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-194">hello public IP address.</span></span>|

![建立 A 記錄](./media/dns-custom-domain/arecord.png)

<span data-ttu-id="ec5ab-196">一旦建立 hello A 記錄時，執行`nslookup`toovalidate hello 記錄解析。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-196">Once hello A record is created, run `nslookup` toovalidate hello record resolves.</span></span>

![公用 IP DNS 查閱](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a><span data-ttu-id="ec5ab-198">App Service (Web Apps)</span><span class="sxs-lookup"><span data-stu-id="ec5ab-198">App Service (Web Apps)</span></span>

<span data-ttu-id="ec5ab-199">hello 下列步驟會引導您進行設定 app service web 應用程式的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-199">hello following steps take you through configuring a custom domain for an app service web app.</span></span>

<span data-ttu-id="ec5ab-200">瀏覽過**Web 和行動裝置版** > **App Service**並選取您要設定自訂網域名稱，然後按一下 hello 資源**自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-200">Navigate too**Web & Mobile** > **App Service** and select hello resource you are configuring a custom domain name, and click **Custom domains**.</span></span>

<span data-ttu-id="ec5ab-201">請注意在 hello hello 目前 url**自訂網域**刀鋒視窗中，此位址作為 hello 別名建立 hello DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-201">Note hello current url on hello **Custom domains** blade, this address is used as hello alias for hello DNS record created.</span></span>

![自訂網域刀鋒視窗](./media/dns-custom-domain/url.png)

<span data-ttu-id="ec5ab-203">瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-203">Navigate tooyour DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="ec5ab-204">填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-204">Fill out hello following information on hello **Add record set** blade and click **OK** toocreate it.</span></span>


|<span data-ttu-id="ec5ab-205">屬性</span><span class="sxs-lookup"><span data-stu-id="ec5ab-205">Property</span></span>  |<span data-ttu-id="ec5ab-206">值</span><span class="sxs-lookup"><span data-stu-id="ec5ab-206">Value</span></span>  |<span data-ttu-id="ec5ab-207">描述</span><span class="sxs-lookup"><span data-stu-id="ec5ab-207">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ec5ab-208">名稱</span><span class="sxs-lookup"><span data-stu-id="ec5ab-208">Name</span></span>     | <span data-ttu-id="ec5ab-209">mywebserver</span><span class="sxs-lookup"><span data-stu-id="ec5ab-209">mywebserver</span></span>        | <span data-ttu-id="ec5ab-210">Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-210">This value along with hello domain name label is hello FQDN for hello custom domain name.</span></span>        |
|<span data-ttu-id="ec5ab-211">類型</span><span class="sxs-lookup"><span data-stu-id="ec5ab-211">Type</span></span>     | <span data-ttu-id="ec5ab-212">CNAME</span><span class="sxs-lookup"><span data-stu-id="ec5ab-212">CNAME</span></span>        | <span data-ttu-id="ec5ab-213">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-213">Use a CNAME record is using an alias.</span></span> <span data-ttu-id="ec5ab-214">如果 hello 資源使用的 IP 位址，就會使用 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-214">If hello resource used an IP address, an A record would be used.</span></span>        |
|<span data-ttu-id="ec5ab-215">TTL</span><span class="sxs-lookup"><span data-stu-id="ec5ab-215">TTL</span></span>     | <span data-ttu-id="ec5ab-216">1</span><span class="sxs-lookup"><span data-stu-id="ec5ab-216">1</span></span>        | <span data-ttu-id="ec5ab-217">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-217">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="ec5ab-218">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="ec5ab-218">TTL unit</span></span>     | <span data-ttu-id="ec5ab-219">小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-219">Hours</span></span>        | <span data-ttu-id="ec5ab-220">時數會做為 hello 時間度量</span><span class="sxs-lookup"><span data-stu-id="ec5ab-220">Hours are used as hello time measurement</span></span>         |
|<span data-ttu-id="ec5ab-221">Alias</span><span class="sxs-lookup"><span data-stu-id="ec5ab-221">Alias</span></span>     | <span data-ttu-id="ec5ab-222">webserver.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ec5ab-222">webserver.azurewebsites.net</span></span>        | <span data-ttu-id="ec5ab-223">hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello web 應用程式所提供的 hello webserver.azurewebsites.net DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-223">hello DNS name you are creating hello alias for, in this example it is hello webserver.azurewebsites.net DNS name provided by default toohello web app.</span></span>        |


![建立 CNAME 記錄](./media/dns-custom-domain/createcnamerecord.png)

<span data-ttu-id="ec5ab-225">瀏覽後 toohello hello 自訂網域名稱所設定的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-225">Navigate back toohello app service that is configured for hello custom domain name.</span></span> <span data-ttu-id="ec5ab-226">按一下 [自訂網域] ，然後按一下 [主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-226">Click **Custom domains**, then click **Hostnames**.</span></span> <span data-ttu-id="ec5ab-227">您建立 tooadd hello CNAME 記錄，請按一下**+ 加入 hostname**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-227">tooadd hello CNAME record you created, click **+ Add hostname**.</span></span>

![圖 1](./media/dns-custom-domain/figure1.png)

<span data-ttu-id="ec5ab-229">Hello 程序完成之後，請執行**nslookup** toovalidate 名稱解析可正常運作。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-229">Once hello process is complete, run **nslookup** toovalidate name resolution is working.</span></span>

![圖 1](./media/dns-custom-domain/finalnslookup.png)

<span data-ttu-id="ec5ab-231">toolearn 深入了解對應自訂網域 tooApp 服務，請瀏覽[對應現有自訂 DNS 名稱 tooAzure Web 應用程式](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-231">toolearn more about mapping a custom domain tooApp Service, visit [Map an existing custom DNS name tooAzure Web Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).</span></span>

<span data-ttu-id="ec5ab-232">如果您需要 toopurchase 自訂網域，請瀏覽[購買 Azure Web 應用程式的自訂網域名稱](../app-service-web/custom-dns-web-site-buydomains-web-app.md)toolearn 深入了解應用程式服務網域。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-232">If you need toopurchase a custom domain, visit [Buy a custom domain name for Azure Web Apps](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn more about App Service domains.</span></span>

## <a name="blob-storage"></a><span data-ttu-id="ec5ab-233">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ec5ab-233">Blob storage</span></span>

<span data-ttu-id="ec5ab-234">hello 下列步驟會引導您進行設定 CNAME 記錄 blob 儲存體帳戶使用 hello asverify 方法。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-234">hello following steps take you through configuring a CNAME record for a blob storage account using hello asverify method.</span></span> <span data-ttu-id="ec5ab-235">這個方法可確保沒有任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-235">This method ensures there is no downtime.</span></span>

<span data-ttu-id="ec5ab-236">瀏覽過**儲存體** > **儲存體帳戶**，選取您的儲存體帳戶，然後按一下**自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-236">Navigate too**Storage** > **Storage Accounts**, select your storage account, and click **Custom domain**.</span></span> <span data-ttu-id="ec5ab-237">Notate hello FQDN 步驟 2，這個值會使用 toocreate hello 第一筆 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="ec5ab-237">Notate hello FQDN under step 2, this value is used toocreate hello first CNAME record</span></span>

![Blob 儲存體自訂網域](./media/dns-custom-domain/blobcustomdomain.png)

<span data-ttu-id="ec5ab-239">瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-239">Navigate tooyour DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="ec5ab-240">填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-240">Fill out hello following information on hello **Add record set** blade and click **OK** toocreate it.</span></span>


|<span data-ttu-id="ec5ab-241">屬性</span><span class="sxs-lookup"><span data-stu-id="ec5ab-241">Property</span></span>  |<span data-ttu-id="ec5ab-242">值</span><span class="sxs-lookup"><span data-stu-id="ec5ab-242">Value</span></span>  |<span data-ttu-id="ec5ab-243">描述</span><span class="sxs-lookup"><span data-stu-id="ec5ab-243">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ec5ab-244">名稱</span><span class="sxs-lookup"><span data-stu-id="ec5ab-244">Name</span></span>     | <span data-ttu-id="ec5ab-245">asverify.mystorageaccount</span><span class="sxs-lookup"><span data-stu-id="ec5ab-245">asverify.mystorageaccount</span></span>        | <span data-ttu-id="ec5ab-246">Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-246">This value along with hello domain name label is hello FQDN for hello custom domain name.</span></span>        |
|<span data-ttu-id="ec5ab-247">類型</span><span class="sxs-lookup"><span data-stu-id="ec5ab-247">Type</span></span>     | <span data-ttu-id="ec5ab-248">CNAME</span><span class="sxs-lookup"><span data-stu-id="ec5ab-248">CNAME</span></span>        | <span data-ttu-id="ec5ab-249">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-249">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="ec5ab-250">TTL</span><span class="sxs-lookup"><span data-stu-id="ec5ab-250">TTL</span></span>     | <span data-ttu-id="ec5ab-251">1</span><span class="sxs-lookup"><span data-stu-id="ec5ab-251">1</span></span>        | <span data-ttu-id="ec5ab-252">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-252">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="ec5ab-253">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="ec5ab-253">TTL unit</span></span>     | <span data-ttu-id="ec5ab-254">小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-254">Hours</span></span>        | <span data-ttu-id="ec5ab-255">時數會做為 hello 時間度量</span><span class="sxs-lookup"><span data-stu-id="ec5ab-255">Hours are used as hello time measurement</span></span>         |
|<span data-ttu-id="ec5ab-256">Alias</span><span class="sxs-lookup"><span data-stu-id="ec5ab-256">Alias</span></span>     | <span data-ttu-id="ec5ab-257">asverify.adatumfunctiona9ed.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ec5ab-257">asverify.adatumfunctiona9ed.blob.core.windows.net</span></span>        | <span data-ttu-id="ec5ab-258">hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello 儲存體帳戶所提供的 hello asverify.adatumfunctiona9ed.blob.core.windows.net DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-258">hello DNS name you are creating hello alias for, in this example it is hello asverify.adatumfunctiona9ed.blob.core.windows.net DNS name provided by default toohello storage account.</span></span>        |

<span data-ttu-id="ec5ab-259">按一下瀏覽後 tooyour 儲存體帳戶**儲存體** > **儲存體帳戶**、 選取儲存體帳戶，然後按一下**自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-259">Navigate back tooyour storage account by clicking **Storage** > **Storage Accounts**, select your storage account and click **Custom domain**.</span></span> <span data-ttu-id="ec5ab-260">類型在您建立不含 hello asverify 前置詞在 hello] 文字方塊中，核取的別名 hello * * 使用間接 CNAME 驗證，然後按一下 [**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-260">Type in hello alias you created without hello asverify prefix in hello text box, check **Use indirect CNAME validation, and click **Save**.</span></span> <span data-ttu-id="ec5ab-261">一旦完成此步驟中，傳回 tooyour DNS 區域，而且建立不含 hello asverify 前置詞的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-261">Once this step is complete, return tooyour DNS zone and create a CNAME record without hello asverify prefix.</span></span>  <span data-ttu-id="ec5ab-262">該時間點之後，您就 hello cdnverify 前置詞的安全 toodelete hello CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-262">After that point, you are safe toodelete hello CNAME record with hello cdnverify prefix.</span></span>

![Blob 儲存體自訂網域](./media/dns-custom-domain/indirectvalidate.png)

<span data-ttu-id="ec5ab-264">執行 `nslookup` 驗證 DNS 解析</span><span class="sxs-lookup"><span data-stu-id="ec5ab-264">Validate DNS resolution by running `nslookup`</span></span>

<span data-ttu-id="ec5ab-265">關於對應自訂網域 tooa blob 儲存體端點，請瀏覽的 toolearn[設定您的 Blob 儲存體端點的自訂網域名稱](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ec5ab-265">toolearn more about mapping a custom domain tooa blob storage endpoint visit [Configure a custom domain name for your Blob storage endpoint](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)</span></span>

## <a name="azure-cdn"></a><span data-ttu-id="ec5ab-266">Azure CDN</span><span class="sxs-lookup"><span data-stu-id="ec5ab-266">Azure CDN</span></span>

<span data-ttu-id="ec5ab-267">hello 下列步驟會引導您進行設定使用 hello cdnverify 方法的 CDN 端點的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-267">hello following steps take you through configuring a CNAME record for a CDN endpoint using hello cdnverify method.</span></span> <span data-ttu-id="ec5ab-268">這個方法可確保沒有任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-268">This method ensures there is no downtime.</span></span>

<span data-ttu-id="ec5ab-269">瀏覽過**網路** > **CDN 設定檔**，選取您的 CDN 設定檔，然後按一下**端點**下**一般**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-269">Navigate too**Networking** > **CDN Profiles**, select your CDN profile, and click **Endpoints** under **General**.</span></span>

<span data-ttu-id="ec5ab-270">選取您正在使用，然後按一下 hello 端點**+ 自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-270">Select hello endpoint you are working with and click **+ Custom domain**.</span></span> <span data-ttu-id="ec5ab-271">請注意 hello**端點主機名稱**為此值為 hello 記錄該 hello CNAME 記錄會指到。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-271">Note hello **Endpoint hostname** as this value is hello record that hello CNAME record points to.</span></span>

![CDN 自訂網域](./media/dns-custom-domain/endpointcustomdomain.png)

<span data-ttu-id="ec5ab-273">瀏覽 tooyour DNS 區域，按一下**+ 記錄集**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-273">Navigate tooyour DNS Zone and click **+ Record set**.</span></span> <span data-ttu-id="ec5ab-274">填寫下列資訊在 hello hello**加入資料錄集**刀鋒視窗，然後按一下**確定**toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-274">Fill out hello following information on hello **Add record set** blade and click **OK** toocreate it.</span></span>

|<span data-ttu-id="ec5ab-275">屬性</span><span class="sxs-lookup"><span data-stu-id="ec5ab-275">Property</span></span>  |<span data-ttu-id="ec5ab-276">值</span><span class="sxs-lookup"><span data-stu-id="ec5ab-276">Value</span></span>  |<span data-ttu-id="ec5ab-277">描述</span><span class="sxs-lookup"><span data-stu-id="ec5ab-277">Description</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ec5ab-278">名稱</span><span class="sxs-lookup"><span data-stu-id="ec5ab-278">Name</span></span>     | <span data-ttu-id="ec5ab-279">cdnverify.mycdnendpoint</span><span class="sxs-lookup"><span data-stu-id="ec5ab-279">cdnverify.mycdnendpoint</span></span>        | <span data-ttu-id="ec5ab-280">Hello 網域名稱標籤以及此值為 hello FQDN hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-280">This value along with hello domain name label is hello FQDN for hello custom domain name.</span></span>        |
|<span data-ttu-id="ec5ab-281">類型</span><span class="sxs-lookup"><span data-stu-id="ec5ab-281">Type</span></span>     | <span data-ttu-id="ec5ab-282">CNAME</span><span class="sxs-lookup"><span data-stu-id="ec5ab-282">CNAME</span></span>        | <span data-ttu-id="ec5ab-283">使用 CNAME 記錄會使用別名。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-283">Use a CNAME record is using an alias.</span></span>        |
|<span data-ttu-id="ec5ab-284">TTL</span><span class="sxs-lookup"><span data-stu-id="ec5ab-284">TTL</span></span>     | <span data-ttu-id="ec5ab-285">1</span><span class="sxs-lookup"><span data-stu-id="ec5ab-285">1</span></span>        | <span data-ttu-id="ec5ab-286">1 為使用 1 小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-286">1 is used for 1 hour</span></span>        |
|<span data-ttu-id="ec5ab-287">TTL 單位</span><span class="sxs-lookup"><span data-stu-id="ec5ab-287">TTL unit</span></span>     | <span data-ttu-id="ec5ab-288">小時</span><span class="sxs-lookup"><span data-stu-id="ec5ab-288">Hours</span></span>        | <span data-ttu-id="ec5ab-289">時數會做為 hello 時間度量</span><span class="sxs-lookup"><span data-stu-id="ec5ab-289">Hours are used as hello time measurement</span></span>         |
|<span data-ttu-id="ec5ab-290">Alias</span><span class="sxs-lookup"><span data-stu-id="ec5ab-290">Alias</span></span>     | <span data-ttu-id="ec5ab-291">cdnverify.adatumcdnendpoint.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="ec5ab-291">cdnverify.adatumcdnendpoint.azureedge.net</span></span>        | <span data-ttu-id="ec5ab-292">hello DNS 名稱建立 hello 別名，在此範例中是預設 toohello 儲存體帳戶所提供的 hello cdnverify.adatumcdnendpoint.azureedge.net DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-292">hello DNS name you are creating hello alias for, in this example it is hello cdnverify.adatumcdnendpoint.azureedge.net DNS name provided by default toohello storage account.</span></span>        |

<span data-ttu-id="ec5ab-293">按一下瀏覽後 tooyour CDN 端點**網路** > **CDN 設定檔**，然後選取您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-293">Navigate back tooyour CDN endpoint by clicking **Networking** > **CDN Profiles**, and select your CDN profile.</span></span> <span data-ttu-id="ec5ab-294">按一下**+ 自訂網域**並輸入您的 CNAME 記錄別名，不含 hello cdnverify 前置詞，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-294">Click **+ Custom domain** and enter your CNAME record alias without hello cdnverify prefix and click **Add**.</span></span>

<span data-ttu-id="ec5ab-295">一旦完成此步驟中，傳回 tooyour DNS 區域，而且建立不含 hello cdnverify 前置詞的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-295">Once this step is complete, return tooyour DNS zone and create a CNAME record without hello cdnverify prefix.</span></span>  <span data-ttu-id="ec5ab-296">該時間點之後，您就 hello cdnverify 前置詞的安全 toodelete hello CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-296">After that point, you are safe toodelete hello CNAME record with hello cdnverify prefix.</span></span> <span data-ttu-id="ec5ab-297">如需有關 CDN 如何 tooconfigure hello 中繼註冊步驟沒有自訂網域造訪[對應 Azure CDN 內容 tooa 自訂網域](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-297">For more information on CDN and how tooconfigure a custom domain without hello intermediate registration step visit [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec5ab-298">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec5ab-298">Next steps</span></span>

<span data-ttu-id="ec5ab-299">了解如何太[設定服務在 Azure 中裝載的反向 DNS](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="ec5ab-299">Learn how too[configure reverse DNS for services hosted in Azure](dns-reverse-dns-for-azure-services.md).</span></span>
