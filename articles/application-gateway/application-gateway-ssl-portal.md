---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "本頁面提供的指示 toocreate 使用 hello 入口網站的應用程式閘道以 SSL 卸載"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="28198-103">使用 hello 入口網站設定 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="28198-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="28198-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="28198-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="28198-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="28198-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="28198-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="28198-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="28198-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="28198-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="28198-108">Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。</span><span class="sxs-lookup"><span data-stu-id="28198-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="28198-109">Hello 前端伺服器安裝並管理 hello web 應用程式，也可以簡化 SSL 卸載。</span><span class="sxs-lookup"><span data-stu-id="28198-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="28198-110">案例</span><span class="sxs-lookup"><span data-stu-id="28198-110">Scenario</span></span>

<span data-ttu-id="28198-111">下列案例中的 hello 經歷設定 SSL 卸載上現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="28198-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="28198-112">hello 案例假設您已經有太遵循 hello 步驟[建立應用程式閘道](application-gateway-create-gateway-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="28198-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28198-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="28198-113">Before you begin</span></span>

<span data-ttu-id="28198-114">與應用程式閘道 tooconfigure SSL 卸載，需要憑證。</span><span class="sxs-lookup"><span data-stu-id="28198-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="28198-115">此憑證會載入上 hello 應用程式閘道和使用 tooencrypt 和解密透過 SSL 傳送嗨流量。</span><span class="sxs-lookup"><span data-stu-id="28198-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="28198-116">hello 憑證必須 toobe 個人資訊交換 (pfx) 格式。</span><span class="sxs-lookup"><span data-stu-id="28198-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="28198-117">這種檔案格式允許 hello 私用金鑰 toobe 匯出所需的流量 hello 應用程式閘道 tooperform hello 加密和解密。</span><span class="sxs-lookup"><span data-stu-id="28198-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="28198-118">新增 HTTPS 接聽程式</span><span class="sxs-lookup"><span data-stu-id="28198-118">Add an HTTPS listener</span></span>

<span data-ttu-id="28198-119">hello HTTPS 接聽程式會尋找其組態為基礎的流量，並協助路由 hello 流量 toohello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="28198-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="28198-120">步驟 1</span><span class="sxs-lookup"><span data-stu-id="28198-120">Step 1</span></span>

<span data-ttu-id="28198-121">瀏覽 toohello Azure 入口網站並選取現有的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="28198-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="28198-122">步驟 2</span><span class="sxs-lookup"><span data-stu-id="28198-122">Step 2</span></span>

<span data-ttu-id="28198-123">按一下接聽程式，然後按一下 hello 新增按鈕 tooadd 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="28198-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![[應用程式閘道概觀] 刀鋒視窗][1]

### <a name="step-3"></a><span data-ttu-id="28198-125">步驟 3</span><span class="sxs-lookup"><span data-stu-id="28198-125">Step 3</span></span>

<span data-ttu-id="28198-126">填寫 hello hello 接聽程式所需的資訊並上傳 hello.pfx 憑證，完成時，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="28198-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="28198-127">**名稱**-此值為 hello 接聽程式的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="28198-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="28198-128">**前端 IP 組態**-這個值是用於 hello 接聽程式的 hello 前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="28198-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="28198-129">**前端連接埠 （名稱/連接埠）** -hello hello 前端 hello 應用程式閘道和使用 hello 實際通訊埠上使用的連接埠的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="28198-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="28198-130">**通訊協定**-交換器 toodetermine 如果 hello 前端使用 https 或 http。</span><span class="sxs-lookup"><span data-stu-id="28198-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="28198-131">**憑證 (名稱/密碼)** - 如果使用 SSL 卸載，此設定就需要 .pfx 憑證，並且需要易記名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="28198-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![[加入接聽程式] 刀鋒視窗][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="28198-133">建立規則，並將它關聯 toohello 接聽程式</span><span class="sxs-lookup"><span data-stu-id="28198-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="28198-134">現在已建立 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="28198-134">hello listener has now been created.</span></span> <span data-ttu-id="28198-135">它是時間 toocreate hello 接聽程式的規則 toohandle hello 流量。</span><span class="sxs-lookup"><span data-stu-id="28198-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="28198-136">規則定義流量的多個組態設定，包括是否使用 cookie 架構工作階段親和性、 通訊協定、 連接埠和健全狀況探查為基礎的路由的 toohello 後端集區的方式。</span><span class="sxs-lookup"><span data-stu-id="28198-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="28198-137">步驟 1</span><span class="sxs-lookup"><span data-stu-id="28198-137">Step 1</span></span>

<span data-ttu-id="28198-138">按一下 hello**規則**的 hello 應用程式閘道，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="28198-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![[應用程式閘道規則] 刀鋒視窗][3]

### <a name="step-2"></a><span data-ttu-id="28198-140">步驟 2</span><span class="sxs-lookup"><span data-stu-id="28198-140">Step 2</span></span>

<span data-ttu-id="28198-141">在 hello**加入基本規則**刀鋒視窗中，輸入 hello 規則 hello 易記名稱，然後選擇 hello hello 先前步驟中建立的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="28198-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="28198-142">選擇 hello 適當的後端集區和設定的 http，然後按一下**[確定]**</span><span class="sxs-lookup"><span data-stu-id="28198-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![[https 設定] 視窗][4]

<span data-ttu-id="28198-144">hello 設定現在會儲存 toohello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="28198-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="28198-145">hello 儲存這些設定的程序可能需要一些時間，才可使用 tooview 透過 hello 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="28198-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="28198-146">儲存之後 hello 應用程式閘道處理 hello 加密和解密的流量。</span><span class="sxs-lookup"><span data-stu-id="28198-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="28198-147">透過 http 處理 hello 應用程式閘道與 hello 後端 web 伺服器之間的所有流量。</span><span class="sxs-lookup"><span data-stu-id="28198-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="28198-148">如果透過 https 起始任何通訊回復 toohello 用戶端將會傳回 toohello 加密的用戶端。</span><span class="sxs-lookup"><span data-stu-id="28198-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28198-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28198-149">Next steps</span></span>

<span data-ttu-id="28198-150">toolearn 如何 tooconfigure 自訂健全狀況探查與 Azure 應用程式閘道，請參閱[建立自訂的健全狀況探查](application-gateway-create-gateway-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="28198-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
