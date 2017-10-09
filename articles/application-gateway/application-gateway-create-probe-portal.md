---
title: "aaaCreate 自訂探查-Azure 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "了解如何 toocreate 自訂探查應用程式閘道使用 hello 入口網站"
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
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a><span data-ttu-id="8df22-103">建立自訂探查使用 hello 入口網站應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8df22-103">Create a custom probe for Application Gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8df22-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8df22-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="8df22-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="8df22-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="8df22-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="8df22-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="8df22-107">在本文中，您可以加入自訂探查 tooan 現有應用程式閘道透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8df22-107">In this article, you add a custom probe tooan existing application gateway through hello Azure portal.</span></span> <span data-ttu-id="8df22-108">自訂探查適合應用程式的健全狀況檢查 頁面，或未提供成功的回應 hello 預設 web 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df22-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8df22-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="8df22-109">Before you begin</span></span>

<span data-ttu-id="8df22-110">如果您還沒有應用程式閘道，請瀏覽[建立應用程式閘道](application-gateway-create-gateway-portal.md)toocreate 應用程式閘道 toowork 與。</span><span class="sxs-lookup"><span data-stu-id="8df22-110">If you do not already have an application gateway, visit [Create an Application Gateway](application-gateway-create-gateway-portal.md) toocreate an application gateway toowork with.</span></span>

## <span data-ttu-id="8df22-111"><a name="createprobe"></a>建立 hello 探查</span><span class="sxs-lookup"><span data-stu-id="8df22-111"><a name="createprobe"></a>Create hello probe</span></span>

<span data-ttu-id="8df22-112">探查的兩步驟程序，透過 hello 入口網站中設定。</span><span class="sxs-lookup"><span data-stu-id="8df22-112">Probes are configured in a two-step process through hello portal.</span></span> <span data-ttu-id="8df22-113">hello 第一個步驟是 toocreate hello 探查。</span><span class="sxs-lookup"><span data-stu-id="8df22-113">hello first step is toocreate hello probe.</span></span> <span data-ttu-id="8df22-114">在 hello 第二個步驟中，您可以加入 hello 探查 toohello 後端 http 設定的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8df22-114">In hello second step, you add hello probe toohello backend http settings of hello application gateway.</span></span>

1. <span data-ttu-id="8df22-115">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8df22-115">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8df22-116">如果您沒有帳戶，可以註冊[免費試用一個月](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="8df22-116">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>

1. <span data-ttu-id="8df22-117">在 hello Azure 入口網站的 我的最愛 窗格中，按一下 所有資源。</span><span class="sxs-lookup"><span data-stu-id="8df22-117">In hello Azure portal Favorites pane, click All resources.</span></span> <span data-ttu-id="8df22-118">按一下 hello 應用程式閘道 hello 中的所有資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8df22-118">Click hello application gateway in hello All resources blade.</span></span> <span data-ttu-id="8df22-119">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入 hello 篩選 partners.contoso.net 依名稱...</span><span class="sxs-lookup"><span data-stu-id="8df22-119">If hello subscription you selected already has several resources in it, you can enter partners.contoso.net in hello Filter by name…</span></span> <span data-ttu-id="8df22-120">方塊 tooeasily 存取 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8df22-120">box tooeasily access hello application gateway.</span></span>

1. <span data-ttu-id="8df22-121">按一下**探查**按一下 hello**新增**按鈕 tooadd 探查。</span><span class="sxs-lookup"><span data-stu-id="8df22-121">Click **Probes** and click hello **Add** button tooadd a probe.</span></span>

  ![已填入資訊的 [新增探查] 刀鋒視窗][1]

1. <span data-ttu-id="8df22-123">在 hello**新增健全狀況探查**刀鋒視窗中，填寫必要的 hello 資訊 hello 探查和完成時按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="8df22-123">On hello **Add health probe** blade, fill out hello required information for hello probe, and when complete click **OK**.</span></span>

  |<span data-ttu-id="8df22-124">**設定**</span><span class="sxs-lookup"><span data-stu-id="8df22-124">**Setting**</span></span> | <span data-ttu-id="8df22-125">**值**</span><span class="sxs-lookup"><span data-stu-id="8df22-125">**Value**</span></span> | <span data-ttu-id="8df22-126">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="8df22-126">**Details**</span></span>|
  |---|---|---|
  |<span data-ttu-id="8df22-127">**名稱**</span><span class="sxs-lookup"><span data-stu-id="8df22-127">**Name**</span></span>|<span data-ttu-id="8df22-128">customProbe</span><span class="sxs-lookup"><span data-stu-id="8df22-128">customProbe</span></span>|<span data-ttu-id="8df22-129">此值為 hello 入口網站中存取的易記名稱 toohello 探查。</span><span class="sxs-lookup"><span data-stu-id="8df22-129">This value is a friendly name toohello probe that is accessible in hello portal.</span></span>|
  |<span data-ttu-id="8df22-130">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="8df22-130">**Protocol**</span></span>|<span data-ttu-id="8df22-131">HTTP 或 HTTPS</span><span class="sxs-lookup"><span data-stu-id="8df22-131">HTTP or HTTPS</span></span> | <span data-ttu-id="8df22-132">hello 健全狀況探查的 hello 通訊協定使用。</span><span class="sxs-lookup"><span data-stu-id="8df22-132">hello protocol that hello health probe uses.</span></span>|
  |<span data-ttu-id="8df22-133">**Host**</span><span class="sxs-lookup"><span data-stu-id="8df22-133">**Host**</span></span>|<span data-ttu-id="8df22-134">亦即</span><span class="sxs-lookup"><span data-stu-id="8df22-134">i.e</span></span> <span data-ttu-id="8df22-135">contoso.com</span><span class="sxs-lookup"><span data-stu-id="8df22-135">contoso.com</span></span>|<span data-ttu-id="8df22-136">這個值是用於 hello 探查 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8df22-136">This value is hello host name that is used for hello probe.</span></span> <span data-ttu-id="8df22-137">只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="8df22-137">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="8df22-138">這個值會與 hello VM 主機名稱不同。</span><span class="sxs-lookup"><span data-stu-id="8df22-138">This value is different from hello VM host name.</span></span>|
  |<span data-ttu-id="8df22-139">**路徑**</span><span class="sxs-lookup"><span data-stu-id="8df22-139">**Path**</span></span>|<span data-ttu-id="8df22-140">/ 或另一個路徑</span><span class="sxs-lookup"><span data-stu-id="8df22-140">/ or another path</span></span>|<span data-ttu-id="8df22-141">hello hello 完整 hello 自訂探查 url 的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="8df22-141">hello remainder of hello full url for hello custom probe.</span></span> <span data-ttu-id="8df22-142">有效路徑的開頭為 '/'。</span><span class="sxs-lookup"><span data-stu-id="8df22-142">A valid path starts with '/'.</span></span> <span data-ttu-id="8df22-143">只要 http://contoso.com hello 預設路徑使用 '/'</span><span class="sxs-lookup"><span data-stu-id="8df22-143">For hello default path of http://contoso.com just use '/'</span></span> |
  |<span data-ttu-id="8df22-144">**間隔 (秒)**</span><span class="sxs-lookup"><span data-stu-id="8df22-144">**Interval (secs)**</span></span>|<span data-ttu-id="8df22-145">30</span><span class="sxs-lookup"><span data-stu-id="8df22-145">30</span></span>|<span data-ttu-id="8df22-146">Hello 探查是的執行頻率 toocheck 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="8df22-146">How often hello probe is run toocheck for health.</span></span> <span data-ttu-id="8df22-147">不建議 tooset hello 低於 30 秒。</span><span class="sxs-lookup"><span data-stu-id="8df22-147">It is not recommended tooset hello lower than 30 seconds.</span></span>|
  |<span data-ttu-id="8df22-148">**逾時 (秒)**</span><span class="sxs-lookup"><span data-stu-id="8df22-148">**Timeout (secs)**</span></span>|<span data-ttu-id="8df22-149">30</span><span class="sxs-lookup"><span data-stu-id="8df22-149">30</span></span>|<span data-ttu-id="8df22-150">逾時之前，等候時間 hello 探查的 hello 數量。使用 hello 逾時時間間隔需求 toobe 高 tooensure hello 後端健全狀況 頁面可以進行 http 呼叫。</span><span class="sxs-lookup"><span data-stu-id="8df22-150">hello amount of time hello probe waits before timing out. hello timeout interval needs toobe high enough that an http call can be made tooensure hello backend health page is available.</span></span>|
  |<span data-ttu-id="8df22-151">**狀況不良臨界值**</span><span class="sxs-lookup"><span data-stu-id="8df22-151">**Unhealthy threshold**</span></span>|<span data-ttu-id="8df22-152">3</span><span class="sxs-lookup"><span data-stu-id="8df22-152">3</span></span>|<span data-ttu-id="8df22-153">被視為狀況不良的嘗試 toobe 失敗的次數。</span><span class="sxs-lookup"><span data-stu-id="8df22-153">Number of failed attempts toobe considered unhealthy.</span></span> <span data-ttu-id="8df22-154">如果健全狀況檢查失敗後端的 hello 決定不良立即 0 表示的臨界值。</span><span class="sxs-lookup"><span data-stu-id="8df22-154">A threshold of 0 means that if a health check fails hello back-end is determined unhealthy immediately.</span></span>|

  > [!IMPORTANT]
  > <span data-ttu-id="8df22-155">hello 主機名稱不是 hello 做為伺服器名稱相同。</span><span class="sxs-lookup"><span data-stu-id="8df22-155">hello host name is not hello same as server name.</span></span> <span data-ttu-id="8df22-156">此值為 hello hello hello 應用程式伺服器上執行的虛擬主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8df22-156">This value is hello name of hello virtual host running on hello application server.</span></span> <span data-ttu-id="8df22-157">傳送嗨探查 toohttp: / /(host name):(port from httpsetting)/urlPath</span><span class="sxs-lookup"><span data-stu-id="8df22-157">hello probe is sent toohttp://(host name):(port from httpsetting)/urlPath</span></span>

## <a name="add-probe-toohello-gateway"></a><span data-ttu-id="8df22-158">新增探查 toohello 閘道</span><span class="sxs-lookup"><span data-stu-id="8df22-158">Add probe toohello gateway</span></span>

<span data-ttu-id="8df22-159">既然 hello 探查建立之後，它是時間 tooadd 它 toohello 閘道。</span><span class="sxs-lookup"><span data-stu-id="8df22-159">Now that hello probe has been created, it is time tooadd it toohello gateway.</span></span> <span data-ttu-id="8df22-160">探查設定會設定在 hello 的 hello 應用程式閘道後端 http 設定值。</span><span class="sxs-lookup"><span data-stu-id="8df22-160">Probe settings are set on hello backend http settings of hello application gateway.</span></span>

1. <span data-ttu-id="8df22-161">按一下**HTTP 設定**hello 應用程式在閘道上，toobring hello 組態刀鋒視窗上的按一下 hello 目前後端 http 設定 hello 視窗中列出。</span><span class="sxs-lookup"><span data-stu-id="8df22-161">Click **HTTP settings** on hello application gateway, toobring up hello configuration blade click hello current backend http settings listed in hello window.</span></span>

  ![[https 設定] 視窗][2]

1. <span data-ttu-id="8df22-163">在 hello **appGatewayBackEndHttpSettings**設定] 刀鋒視窗中，核取 hello**使用自訂探查**核取方塊，然後選擇 建立 hello 中的 hello 探查[建立 hello 探查](#createprobe)區段在 hello**自訂探查**下拉式清單...</span><span class="sxs-lookup"><span data-stu-id="8df22-163">On hello **appGatewayBackEndHttpSettings** settings blade, check hello **Use custom probe** checkbox and choose hello probe created in hello [Create hello probe](#createprobe) section on hello **Custom probe** drop-down..</span></span>
<span data-ttu-id="8df22-164">完成後，按**儲存**和 hello 設定會套用。</span><span class="sxs-lookup"><span data-stu-id="8df22-164">When complete, click **Save** and hello settings are applied.</span></span>

<span data-ttu-id="8df22-165">hello 預設探查檢查 hello 預設存取 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df22-165">hello default probe checks hello default access toohello web application.</span></span> <span data-ttu-id="8df22-166">已建立自訂探查，hello 應用程式閘道會使用針對 hello 後端伺服器 hello 定義的自訂路徑 toomonitor 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="8df22-166">Now that a custom probe has been created, hello application gateway uses hello custom path defined toomonitor health for hello backend servers.</span></span> <span data-ttu-id="8df22-167">根據已定義的 hello 準則，hello 應用程式閘道會檢查 hello hello 探查中指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="8df22-167">Based on hello criteria that was defined, hello application gateway checks hello path specified in hello probe.</span></span> <span data-ttu-id="8df22-168">如果 hello 呼叫 toohost:Port / 路徑不會傳回 HTTP 200 399 狀態回應，hello 伺服器不會採取離輪替循環達到 hello 狀況不良閾值後。</span><span class="sxs-lookup"><span data-stu-id="8df22-168">If hello call toohost:Port/path does not return an HTTP 200-399 status response, hello server is taken out of rotation after hello unhealthy threshold is reached.</span></span> <span data-ttu-id="8df22-169">探查時，會繼續在 hello 狀況不良的執行個體 toodetermine 它再度變成狀況良好。</span><span class="sxs-lookup"><span data-stu-id="8df22-169">Probing continues on hello unhealthy instance toodetermine when it becomes healthy again.</span></span> <span data-ttu-id="8df22-170">流量 hello 執行個體，加入之後回復 toohealthy 伺服器集區開始再次流動 tooit 以及探查 toohello 執行個體會繼續依使用者指定的間隔，像平常一樣。</span><span class="sxs-lookup"><span data-stu-id="8df22-170">Once hello instance is added back toohealthy server pool, traffic begins flowing tooit again and probing toohello instance continues at user specified interval as normal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df22-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8df22-171">Next steps</span></span>

<span data-ttu-id="8df22-172">如何 tooconfigure SSL 卸載，以及 Azure 應用程式閘道，請參閱的 toolearn[設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8df22-172">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

