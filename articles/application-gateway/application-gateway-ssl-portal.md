---
title: "設定 SSL 卸載 - Azure 應用程式閘道 - Azure 入口網站 | Microsoft Docs"
description: "本頁面提供使用入口網站來建立具有 SSL 卸載之應用程式閘道的指示"
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
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="8df48-103">使用入口網站設定適用於 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8df48-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8df48-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8df48-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="8df48-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="8df48-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="8df48-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="8df48-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="8df48-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8df48-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="8df48-108">Azure 應用程式閘道可以設定為在閘道終止安全通訊端層 (SSL) 工作階段，以避免 Web 伺服陣列發生高成本的 SSL 解密工作。</span><span class="sxs-lookup"><span data-stu-id="8df48-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="8df48-109">SSL 卸載也可以簡化 Web 應用程式的前端伺服器設定和管理。</span><span class="sxs-lookup"><span data-stu-id="8df48-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="8df48-110">案例</span><span class="sxs-lookup"><span data-stu-id="8df48-110">Scenario</span></span>

<span data-ttu-id="8df48-111">下列案例會完成在現有應用程式閘道上設定 SSL 卸載的程序。</span><span class="sxs-lookup"><span data-stu-id="8df48-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="8df48-112">此案例假設您已經依照步驟 [建立應用程式閘道](application-gateway-create-gateway-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8df48-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8df48-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="8df48-113">Before you begin</span></span>

<span data-ttu-id="8df48-114">若要設定與應用程式閘道搭配運作的 SSL 卸載，必須要有憑證。</span><span class="sxs-lookup"><span data-stu-id="8df48-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="8df48-115">系統會在應用程式閘道上載入此憑證，然後用來對透過 SSL 傳送的流量進行加密和解密。</span><span class="sxs-lookup"><span data-stu-id="8df48-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="8df48-116">此憑證必須採用「個人資訊交換」(pfx) 格式。</span><span class="sxs-lookup"><span data-stu-id="8df48-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="8df48-117">此檔案格式可允許將私密金鑰匯出，而應用程式閘道需要這個匯出的金鑰來執行流量的加密和解密。</span><span class="sxs-lookup"><span data-stu-id="8df48-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="8df48-118">新增 HTTPS 接聽程式</span><span class="sxs-lookup"><span data-stu-id="8df48-118">Add an HTTPS listener</span></span>

<span data-ttu-id="8df48-119">HTTPS 接聽程式會根據其組態來尋找流量，並協助將流量路由傳送到後端集區。</span><span class="sxs-lookup"><span data-stu-id="8df48-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="8df48-120">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8df48-120">Step 1</span></span>

<span data-ttu-id="8df48-121">瀏覽到 Azure 入口網站，然後選取現有的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8df48-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="8df48-122">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8df48-122">Step 2</span></span>

<span data-ttu-id="8df48-123">按一下 [接聽程式]，然後按一下 [加入] 按鈕來加入接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8df48-123">Click Listeners and click the Add button to add a listener.</span></span>

![[應用程式閘道概觀] 刀鋒視窗][1]

### <a name="step-3"></a><span data-ttu-id="8df48-125">步驟 3</span><span class="sxs-lookup"><span data-stu-id="8df48-125">Step 3</span></span>

<span data-ttu-id="8df48-126">填入必要的接聽程式資訊，然後上傳 .pfx 憑證，完成時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8df48-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="8df48-127">**名稱** - 此值是接聽程式的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="8df48-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="8df48-128">**前端 IP 組態** - 此值是用於接聽程式的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="8df48-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="8df48-129">**前端連接埠 (名稱/連接埠)** - 應用程式閘道前端上所使用之連接埠的易記名稱，以及實際使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="8df48-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="8df48-130">**通訊協定** - 用以判斷前端使用的是 https 還是 http 的參數。</span><span class="sxs-lookup"><span data-stu-id="8df48-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="8df48-131">**憑證 (名稱/密碼)** - 如果使用 SSL 卸載，此設定就需要 .pfx 憑證，並且需要易記名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8df48-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![[加入接聽程式] 刀鋒視窗][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="8df48-133">建立規則並將它與接聽程式建立關聯</span><span class="sxs-lookup"><span data-stu-id="8df48-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="8df48-134">現在已建立接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8df48-134">The listener has now been created.</span></span> <span data-ttu-id="8df48-135">此時即可建立規則來處理來自接聽程式的流量。</span><span class="sxs-lookup"><span data-stu-id="8df48-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="8df48-136">規則會定義如何根據多個組態設定將流量路由傳送到後端集區，包括是否使用以 Cookie 為基礎的工作階段同質性、通訊協定、連接埠和健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="8df48-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="8df48-137">步驟 1</span><span class="sxs-lookup"><span data-stu-id="8df48-137">Step 1</span></span>

<span data-ttu-id="8df48-138">按一下應用程式閘道的 [規則]  ，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8df48-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![[應用程式閘道規則] 刀鋒視窗][3]

### <a name="step-2"></a><span data-ttu-id="8df48-140">步驟 2</span><span class="sxs-lookup"><span data-stu-id="8df48-140">Step 2</span></span>

<span data-ttu-id="8df48-141">在 [新增基本規則]  刀鋒視窗中，輸入規則的易記名稱，然後選擇在上一個步驟中建立的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8df48-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="8df48-142">選擇適當的後端集區和 http 設定，然後按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="8df48-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![[https 設定] 視窗][4]

<span data-ttu-id="8df48-144">這些設定現在已儲存至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8df48-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="8df48-145">這些設定可能需要一些時間進行儲存，然後才能透過入口網站或 PowerShell 檢視。</span><span class="sxs-lookup"><span data-stu-id="8df48-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="8df48-146">儲存之後，應用程式閘道就會處理流量的加密和解密。</span><span class="sxs-lookup"><span data-stu-id="8df48-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="8df48-147">應用程式閘道與後端 Web 伺服器之間的所有流量都會透過 http 進行處理。</span><span class="sxs-lookup"><span data-stu-id="8df48-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="8df48-148">任何回到用戶端的通訊只要是透過 https 起始，就會以加密的方式傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="8df48-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df48-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8df48-149">Next steps</span></span>

<span data-ttu-id="8df48-150">若要了解如何設定與「Azure 應用程式閘道」搭配運作的自訂健康狀態探查，請參閱 [建立自訂健康狀態探查](application-gateway-create-gateway-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8df48-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
