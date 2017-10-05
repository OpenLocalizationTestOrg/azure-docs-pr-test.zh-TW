---
title: "建立自訂探查 - Azure 應用程式閘道 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用入口網站建立應用程式閘道的自訂探查"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 65e9bba4ce9ac41ae2a9a8c3fa7f661165fc1403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-the-portal"></a><span data-ttu-id="c708e-103">使用入口網站建立應用程式閘道的自訂探查</span><span class="sxs-lookup"><span data-stu-id="c708e-103">Create a custom probe for Application Gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c708e-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c708e-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="c708e-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="c708e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="c708e-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="c708e-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="c708e-107">在本文中，您會透過 Azure 入口網站將自訂探查新增到現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="c708e-107">In this article, you add a custom probe to an existing application gateway through the Azure portal.</span></span> <span data-ttu-id="c708e-108">對於具有特定健康狀態檢查頁面的應用程式，或是在預設 Web 應用程式上不提供成功回應的應用程式，自訂探查非常實用。</span><span class="sxs-lookup"><span data-stu-id="c708e-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c708e-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="c708e-109">Before you begin</span></span>

<span data-ttu-id="c708e-110">如果您還沒有應用程式閘道，請瀏覽[建立應用程式閘道](application-gateway-create-gateway-portal.md)以建立要使用的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="c708e-110">If you do not already have an application gateway, visit [Create an Application Gateway](application-gateway-create-gateway-portal.md) to create an application gateway to work with.</span></span>

## <span data-ttu-id="c708e-111"><a name="createprobe"></a>建立探查</span><span class="sxs-lookup"><span data-stu-id="c708e-111"><a name="createprobe"></a>Create the probe</span></span>

<span data-ttu-id="c708e-112">您可以透過入口網站中兩個步驟的程序來設定探查。</span><span class="sxs-lookup"><span data-stu-id="c708e-112">Probes are configured in a two-step process through the portal.</span></span> <span data-ttu-id="c708e-113">第一個步驟是建立探查。</span><span class="sxs-lookup"><span data-stu-id="c708e-113">The first step is to create the probe.</span></span> <span data-ttu-id="c708e-114">在第二個步驟中，將探查新增至應用程式閘道的後端 http 設定。</span><span class="sxs-lookup"><span data-stu-id="c708e-114">In the second step, you add the probe to the backend http settings of the application gateway.</span></span>

1. <span data-ttu-id="c708e-115">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c708e-115">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c708e-116">如果您沒有帳戶，可以註冊[免費試用一個月](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="c708e-116">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>

1. <span data-ttu-id="c708e-117">在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="c708e-117">In the Azure portal Favorites pane, click All resources.</span></span> <span data-ttu-id="c708e-118">按一下 [所有資源] 刀鋒視窗中的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="c708e-118">Click the application gateway in the All resources blade.</span></span> <span data-ttu-id="c708e-119">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選] 方塊中輸入 partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="c708e-119">If the subscription you selected already has several resources in it, you can enter partners.contoso.net in the Filter by name…</span></span> <span data-ttu-id="c708e-120">輕鬆地存取應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="c708e-120">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="c708e-121">按一下 [探查]，然後按一下 [加入] 按鈕來新增探查。</span><span class="sxs-lookup"><span data-stu-id="c708e-121">Click **Probes** and click the **Add** button to add a probe.</span></span>

  ![已填入資訊的 [新增探查] 刀鋒視窗][1]

1. <span data-ttu-id="c708e-123">在 [新增健康狀態探查] 刀鋒視窗中，填入探查的必要資訊，然後在完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c708e-123">On the **Add health probe** blade, fill out the required information for the probe, and when complete click **OK**.</span></span>

  |<span data-ttu-id="c708e-124">**設定**</span><span class="sxs-lookup"><span data-stu-id="c708e-124">**Setting**</span></span> | <span data-ttu-id="c708e-125">**值**</span><span class="sxs-lookup"><span data-stu-id="c708e-125">**Value**</span></span> | <span data-ttu-id="c708e-126">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="c708e-126">**Details**</span></span>|
  |---|---|---|
  |<span data-ttu-id="c708e-127">**名稱**</span><span class="sxs-lookup"><span data-stu-id="c708e-127">**Name**</span></span>|<span data-ttu-id="c708e-128">customProbe</span><span class="sxs-lookup"><span data-stu-id="c708e-128">customProbe</span></span>|<span data-ttu-id="c708e-129">此值是可在入口網站中存取的易記探查名稱。</span><span class="sxs-lookup"><span data-stu-id="c708e-129">This value is a friendly name to the probe that is accessible in the portal.</span></span>|
  |<span data-ttu-id="c708e-130">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="c708e-130">**Protocol**</span></span>|<span data-ttu-id="c708e-131">HTTP 或 HTTPS</span><span class="sxs-lookup"><span data-stu-id="c708e-131">HTTP or HTTPS</span></span> | <span data-ttu-id="c708e-132">健康狀態探查所使用的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="c708e-132">The protocol that the health probe uses.</span></span>|
  |<span data-ttu-id="c708e-133">**Host**</span><span class="sxs-lookup"><span data-stu-id="c708e-133">**Host**</span></span>|<span data-ttu-id="c708e-134">亦即</span><span class="sxs-lookup"><span data-stu-id="c708e-134">i.e</span></span> <span data-ttu-id="c708e-135">contoso.com</span><span class="sxs-lookup"><span data-stu-id="c708e-135">contoso.com</span></span>|<span data-ttu-id="c708e-136">此值是用於探查的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c708e-136">This value is the host name that is used for the probe.</span></span> <span data-ttu-id="c708e-137">只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="c708e-137">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="c708e-138">此值與 VM 主機名稱不同。</span><span class="sxs-lookup"><span data-stu-id="c708e-138">This value is different from the VM host name.</span></span>|
  |<span data-ttu-id="c708e-139">**路徑**</span><span class="sxs-lookup"><span data-stu-id="c708e-139">**Path**</span></span>|<span data-ttu-id="c708e-140">/ 或另一個路徑</span><span class="sxs-lookup"><span data-stu-id="c708e-140">/ or another path</span></span>|<span data-ttu-id="c708e-141">自訂探查完整 URL 的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="c708e-141">The remainder of the full url for the custom probe.</span></span> <span data-ttu-id="c708e-142">有效路徑的開頭為 '/'。</span><span class="sxs-lookup"><span data-stu-id="c708e-142">A valid path starts with '/'.</span></span> <span data-ttu-id="c708e-143">針對 http://contoso.com 的預設路徑，只要使用 '/'</span><span class="sxs-lookup"><span data-stu-id="c708e-143">For the default path of http://contoso.com just use '/'</span></span> |
  |<span data-ttu-id="c708e-144">**間隔 (秒)**</span><span class="sxs-lookup"><span data-stu-id="c708e-144">**Interval (secs)**</span></span>|<span data-ttu-id="c708e-145">30</span><span class="sxs-lookup"><span data-stu-id="c708e-145">30</span></span>|<span data-ttu-id="c708e-146">執行探查以檢查健康狀態的頻率。</span><span class="sxs-lookup"><span data-stu-id="c708e-146">How often the probe is run to check for health.</span></span> <span data-ttu-id="c708e-147">建議您不要設定低於 30 秒。</span><span class="sxs-lookup"><span data-stu-id="c708e-147">It is not recommended to set the lower than 30 seconds.</span></span>|
  |<span data-ttu-id="c708e-148">**逾時 (秒)**</span><span class="sxs-lookup"><span data-stu-id="c708e-148">**Timeout (secs)**</span></span>|<span data-ttu-id="c708e-149">30</span><span class="sxs-lookup"><span data-stu-id="c708e-149">30</span></span>|<span data-ttu-id="c708e-150">探查逾時前所等待的時間。</span><span class="sxs-lookup"><span data-stu-id="c708e-150">The amount of time the probe waits before timing out.</span></span> <span data-ttu-id="c708e-151">逾時間隔需要高到足以進行 http 呼叫，以確保可使用後端的健康狀態頁面。</span><span class="sxs-lookup"><span data-stu-id="c708e-151">The timeout interval needs to be high enough that an http call can be made to ensure the backend health page is available.</span></span>|
  |<span data-ttu-id="c708e-152">**狀況不良臨界值**</span><span class="sxs-lookup"><span data-stu-id="c708e-152">**Unhealthy threshold**</span></span>|<span data-ttu-id="c708e-153">3</span><span class="sxs-lookup"><span data-stu-id="c708e-153">3</span></span>|<span data-ttu-id="c708e-154">視為狀況不良的失敗嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="c708e-154">Number of failed attempts to be considered unhealthy.</span></span> <span data-ttu-id="c708e-155">臨界值為 0 表示，如果健康狀態檢查失敗，後端會被立即斷定為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="c708e-155">A threshold of 0 means that if a health check fails the back-end is determined unhealthy immediately.</span></span>|

  > [!IMPORTANT]
  > <span data-ttu-id="c708e-156">主機名稱與伺服器名稱不同。</span><span class="sxs-lookup"><span data-stu-id="c708e-156">The host name is not the same as server name.</span></span> <span data-ttu-id="c708e-157">此值是在應用程式伺服器上執行的虛擬主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c708e-157">This value is the name of the virtual host running on the application server.</span></span> <span data-ttu-id="c708e-158">探查會傳送到 http://(host name):(port from httpsetting)/urlPath</span><span class="sxs-lookup"><span data-stu-id="c708e-158">The probe is sent to http://(host name):(port from httpsetting)/urlPath</span></span>

## <a name="add-probe-to-the-gateway"></a><span data-ttu-id="c708e-159">將探查新增到閘道</span><span class="sxs-lookup"><span data-stu-id="c708e-159">Add probe to the gateway</span></span>

<span data-ttu-id="c708e-160">既然已經建立探查，此時即可將它新增到閘道。</span><span class="sxs-lookup"><span data-stu-id="c708e-160">Now that the probe has been created, it is time to add it to the gateway.</span></span> <span data-ttu-id="c708e-161">探查設定是在應用程式閘道的後端 http 設定上設定。</span><span class="sxs-lookup"><span data-stu-id="c708e-161">Probe settings are set on the backend http settings of the application gateway.</span></span>

1. <span data-ttu-id="c708e-162">按一下應用程式閘道的 [HTTP 設定] 來開啟組態刀鋒視窗，然後按一下視窗中列出的目前後端 http 設定。</span><span class="sxs-lookup"><span data-stu-id="c708e-162">Click **HTTP settings** on the application gateway, to bring up the configuration blade click the current backend http settings listed in the window.</span></span>

  ![[https 設定] 視窗][2]

1. <span data-ttu-id="c708e-164">在 [appGatewayBackEndHttpSettings] 設定刀鋒視窗中，選取 [使用自訂探查] 核取方塊，然後在 [自訂探查] 下拉式清單中選擇在[建立探查](#createprobe)一節中建立的探查。</span><span class="sxs-lookup"><span data-stu-id="c708e-164">On the **appGatewayBackEndHttpSettings** settings blade, check the **Use custom probe** checkbox and choose the probe created in the [Create the probe](#createprobe) section on the **Custom probe** drop-down..</span></span>
<span data-ttu-id="c708e-165">完成時，按一下 [儲存] 即可套用設定。</span><span class="sxs-lookup"><span data-stu-id="c708e-165">When complete, click **Save** and the settings are applied.</span></span>

<span data-ttu-id="c708e-166">預設探查會檢查 Web 應用程式的預設存取權。</span><span class="sxs-lookup"><span data-stu-id="c708e-166">The default probe checks the default access to the web application.</span></span> <span data-ttu-id="c708e-167">建立自訂探查之後，應用程式閘道便可使用定義的自訂路徑來監視後端伺服器的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="c708e-167">Now that a custom probe has been created, the application gateway uses the custom path defined to monitor health for the backend servers.</span></span> <span data-ttu-id="c708e-168">應用程式閘道會根據定義的準則，以檢查探查中指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="c708e-168">Based on the criteria that was defined, the application gateway checks the path specified in the probe.</span></span> <span data-ttu-id="c708e-169">如果對 host:Port/path 的呼叫沒有傳回 HTTP 200-399 狀態回應，當達到狀況不良閾值時，系統就會將該伺服器從輪替的行列中移除。</span><span class="sxs-lookup"><span data-stu-id="c708e-169">If the call to host:Port/path does not return an HTTP 200-399 status response, the server is taken out of rotation after the unhealthy threshold is reached.</span></span> <span data-ttu-id="c708e-170">探查會繼續在狀況不良的執行個體上執行，以判斷它何時再次變成狀況良好。</span><span class="sxs-lookup"><span data-stu-id="c708e-170">Probing continues on the unhealthy instance to determine when it becomes healthy again.</span></span> <span data-ttu-id="c708e-171">系統將執行個體重新加回至狀況良好的伺服器集區之後，流量就會再次開始流向它，而對執行個體的探查則會如常依據使用者指定的間隔繼續執行。</span><span class="sxs-lookup"><span data-stu-id="c708e-171">Once the instance is added back to healthy server pool, traffic begins flowing to it again and probing to the instance continues at user specified interval as normal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c708e-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c708e-172">Next steps</span></span>

<span data-ttu-id="c708e-173">若要了解如何設定與「Azure 應用程式閘道」搭配運作的「SSL 卸載」，請參閱 [設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c708e-173">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

