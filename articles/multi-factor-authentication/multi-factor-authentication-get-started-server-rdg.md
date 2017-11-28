---
title: "使用 RADIUS 的 RDG 和 Azure MFA Server | Microsoft Docs"
description: "此 Azure Multi-Factor Authentication 頁面協助您部署使用 RADIUS 的遠端桌面 (RD) 閘道器和 Azure Multi-Factor Authentication Server。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 3b4181701c5df03a3df7e0446b313eac201ad99e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a><span data-ttu-id="e9824-103">使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="e9824-103">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>
<span data-ttu-id="e9824-104">通常，遠端桌面 (RD) 閘道會使用本機網路原則服務 (NPS) 來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="e9824-104">Often, Remote Desktop (RD) Gateway uses the local Network Policy Services (NPS) to authenticate users.</span></span> <span data-ttu-id="e9824-105">本文說明如何將 RADIUS 要求從遠端桌面閘道器 (透過本機 NPS) 傳送至 Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="e9824-105">This article describes how to route RADIUS requests out from the Remote Desktop Gateway (through the local NPS) to the Multi-Factor Authentication Server.</span></span> <span data-ttu-id="e9824-106">Azure MFA 和 RD 閘道的組合表示使用者可以從任何地方存取其工作環境，同時執行強式驗證。</span><span class="sxs-lookup"><span data-stu-id="e9824-106">The combination of Azure MFA and RD Gateway means that your users can access their work environments from anywhere while performing strong authentication.</span></span> 

<span data-ttu-id="e9824-107">由於 Server 2012 R2 不支援終端機服務的 Windows 驗證，請使用 RD 閘道和 RADIUS 來與 MFA Server 整合。</span><span class="sxs-lookup"><span data-stu-id="e9824-107">Since Windows Authentication for terminal services is not supported for Server 2012 R2, use RD Gateway and RADIUS to integrate with MFA Server.</span></span> 

<span data-ttu-id="e9824-108">在不同的伺服器上安裝 Azure Multi-Factor Authentication Server，由它代理將 RADIUS 要求傳回到遠端桌面閘道器伺服器上的 NPS。</span><span class="sxs-lookup"><span data-stu-id="e9824-108">Install the Azure Multi-Factor Authentication Server on a separate server, which proxies the RADIUS request back to the NPS on the Remote Desktop Gateway Server.</span></span> <span data-ttu-id="e9824-109">NPS 驗證使用者名稱和密碼之後，它會將回應傳回給 Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="e9824-109">After NPS validates the username and password, it returns a response to the Multi-Factor Authentication Server.</span></span> <span data-ttu-id="e9824-110">然後，MFA Server 會執行第二因素驗證，然後將結果傳回給閘道。</span><span class="sxs-lookup"><span data-stu-id="e9824-110">Then, the MFA Server performs the second factor of authentication and returns a result to the gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9824-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="e9824-111">Prerequisites</span></span>

- <span data-ttu-id="e9824-112">已加入網域的 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="e9824-112">A domain-joined Azure MFA Server.</span></span> <span data-ttu-id="e9824-113">如果尚未進行安裝，請遵循[開始使用 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e9824-113">If you don't have one installed already, follow the steps in [Getting started with the Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server.md).</span></span>
- <span data-ttu-id="e9824-114">使用網路原則服務進行驗證的遠端桌面閘道。</span><span class="sxs-lookup"><span data-stu-id="e9824-114">A Remote Desktop Gateway that authenticates with Network Policy Services.</span></span>

## <a name="configure-the-remote-desktop-gateway"></a><span data-ttu-id="e9824-115">設定遠端桌面閘道</span><span class="sxs-lookup"><span data-stu-id="e9824-115">Configure the Remote Desktop Gateway</span></span>
<span data-ttu-id="e9824-116">設定 RD 閘道，以將 RADIUS 驗證傳送到 Azure Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="e9824-116">Configure the RD Gateway to send RADIUS authentication to an Azure Multi-Factor Authentication Server.</span></span> 

1. <span data-ttu-id="e9824-117">在 [RD 閘道管理員] 中，以滑鼠右鍵按一下伺服器名稱，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="e9824-117">In RD Gateway Manager, right-click the server name and select **Properties**.</span></span>
2. <span data-ttu-id="e9824-118">移至 [RD CAP 存放區] 索引標籤並選取 [執行 NPS 的中央伺服器]。</span><span class="sxs-lookup"><span data-stu-id="e9824-118">Go to the **RD CAP Store** tab and select **Central server running NPS**.</span></span> 
3. <span data-ttu-id="e9824-119">輸入每部伺服器的名稱或 IP 位址，將一或多部 Multi-Factor Authentication Server 新增為 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9824-119">Add one or more Azure Multi-Factor Authentication Servers as RADIUS servers by entering the name or IP address of each server.</span></span> 
4. <span data-ttu-id="e9824-120">為每一部伺服器建立共用密碼。</span><span class="sxs-lookup"><span data-stu-id="e9824-120">Create a shared secret for each server.</span></span>

## <a name="configure-nps"></a><span data-ttu-id="e9824-121">設定 NPS</span><span class="sxs-lookup"><span data-stu-id="e9824-121">Configure NPS</span></span>
<span data-ttu-id="e9824-122">RD 閘道器使用 NPS 將 RADIUS 要求傳送到 Azure Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="e9824-122">The RD Gateway uses NPS to send the RADIUS request to Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="e9824-123">若要設定 NPS，首先變更逾時設定，以免 RD 閘道在雙步驟驗證完成之前逾時。</span><span class="sxs-lookup"><span data-stu-id="e9824-123">To configure NPS, first you change the timeout settings to prevent the RD Gateway from timing out before the two-step verification has completed.</span></span> <span data-ttu-id="e9824-124">然後，您可更新 NPS，以從 MFA Server 接收 RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="e9824-124">Then, you update NPS to receive RADIUS authentications from your MFA Server.</span></span> <span data-ttu-id="e9824-125">使用下列程序來設定 NPS：</span><span class="sxs-lookup"><span data-stu-id="e9824-125">Use the following procedure to configure NPS:</span></span>

### <a name="modify-the-timeout-policy"></a><span data-ttu-id="e9824-126">修改逾時原則</span><span class="sxs-lookup"><span data-stu-id="e9824-126">Modify the timeout policy</span></span>

1. <span data-ttu-id="e9824-127">在 NPS 中，開啟左欄中的 [RADIUS 用戶端及伺服器] 功能表，然後選取 [遠端 RADIUS 伺服器群組]。</span><span class="sxs-lookup"><span data-stu-id="e9824-127">In NPS, open the **RADIUS Clients and Server** menu in the left column and select **Remote RADIUS Server Groups**.</span></span> 
2. <span data-ttu-id="e9824-128">選取 [TS 閘道伺服器群組]。</span><span class="sxs-lookup"><span data-stu-id="e9824-128">Select the **TS GATEWAY SERVER GROUP**.</span></span> 
3. <span data-ttu-id="e9824-129">移至 [負載平衡] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e9824-129">Go to the **Load Balancing** tab.</span></span> 
4. <span data-ttu-id="e9824-130">將 [要求被丟棄前，無回應的秒數] 和 [伺服器被識別為無法使用時，要求之間的間隔秒數] 變更為 30 至 60 秒之間。</span><span class="sxs-lookup"><span data-stu-id="e9824-130">Change both the **Number of seconds without response before request is considered dropped** and the **Number of seconds between requests when server is identified as unavailable** to between 30 and 60 seconds.</span></span> <span data-ttu-id="e9824-131">(如果您在驗證期間發現伺服器仍然逾時，您可以回到這裡並增加秒數。)</span><span class="sxs-lookup"><span data-stu-id="e9824-131">(If you find that the server still times out during authentication, you can come back here and increase the number of seconds.)</span></span>
5. <span data-ttu-id="e9824-132">移至 [驗證/帳戶] 索引標籤，檢查指定的 RADIUS 連接埠符合 Multi-Factor Authentication Server 所接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e9824-132">Go to the **Authentication/Account** tab and check that the RADIUS ports specified match the ports that the Multi-Factor Authentication Server is listening on.</span></span>

### <a name="prepare-nps-to-receive-authentications-from-the-mfa-server"></a><span data-ttu-id="e9824-133">準備 NPS 以從 MFA Server 接收驗證</span><span class="sxs-lookup"><span data-stu-id="e9824-133">Prepare NPS to receive authentications from the MFA Server</span></span>

1. <span data-ttu-id="e9824-134">以滑鼠右鍵按一下左欄中的 [RADIUS 用戶端及伺服器] 之下的 [RADIUS 用戶端]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e9824-134">Right-click **RADIUS Clients** under RADIUS Clients and Servers in the left column and select **New**.</span></span>
2. <span data-ttu-id="e9824-135">將 Azure Multi-Factor Authentication Server 新增為 RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="e9824-135">Add the Azure Multi-Factor Authentication Server as a RADIUS client.</span></span> <span data-ttu-id="e9824-136">選擇 [好記的名稱] 並指定共用密碼。</span><span class="sxs-lookup"><span data-stu-id="e9824-136">Choose a Friendly name and specify a shared secret.</span></span>
3. <span data-ttu-id="e9824-137">開啟左欄中的 [原則] 功能表，然後選取 [連線要求原則]。</span><span class="sxs-lookup"><span data-stu-id="e9824-137">Open the **Policies** menu in the left column and select **Connection Request Policies**.</span></span> <span data-ttu-id="e9824-138">您應會看見在設定 RD 閘道時所建立的原則，其名稱為 [TS 閘道授權原則]。</span><span class="sxs-lookup"><span data-stu-id="e9824-138">You should see a policy called TS GATEWAY AUTHORIZATION POLICY that was created when RD Gateway was configured.</span></span> <span data-ttu-id="e9824-139">此原則會將 RADIUS 要求轉送到 Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="e9824-139">This policy forwards RADIUS requests to the Multi-Factor Authentication Server.</span></span>
4. <span data-ttu-id="e9824-140">以滑鼠右鍵按一下 [TS 閘道授權原則]，然後選取 [重複原則]。</span><span class="sxs-lookup"><span data-stu-id="e9824-140">Right-click **TS GATEWAY AUTHORIZATION POLICY** and select **Duplicate Policy**.</span></span> 
5. <span data-ttu-id="e9824-141">開啟新的原則，並移至 [條件] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e9824-141">Open the new policy and go to the **Conditions** tab.</span></span>
6. <span data-ttu-id="e9824-142">新增條件以比對 [好記的用戶端名稱] 與步驟 2 中為 Azure Multi-Factor Authentication Server RADIUS 用戶端設定的 [好記的名稱]。</span><span class="sxs-lookup"><span data-stu-id="e9824-142">Add a condition that matches the Client Friendly Name with the Friendly name set in step 2 for the Azure Multi-Factor Authentication Server RADIUS client.</span></span> 
7. <span data-ttu-id="e9824-143">移至 [設定] 索引標籤，然後選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="e9824-143">Go to the **Settings** tab and select **Authentication**.</span></span>
8. <span data-ttu-id="e9824-144">將 [驗證提供者] 變更為 [驗證這個伺服器上的要求]。</span><span class="sxs-lookup"><span data-stu-id="e9824-144">Change the Authentication Provider to **Authenticate requests on this server**.</span></span> <span data-ttu-id="e9824-145">此原則可確保當 NPS 收到來自 Azure MFA Server 的 RADIUS 要求時，就在本機進行驗證，而不會將 RADIUS 要求傳回給 Azure Multi-Factor Authentication Server，導致迴圈狀況。</span><span class="sxs-lookup"><span data-stu-id="e9824-145">This policy ensures that when NPS receives a RADIUS request from the Azure MFA Server, the authentication occurs locally instead of sending a RADIUS request back to the Azure Multi-Factor Authentication Server, which would result in a loop condition.</span></span> 
9. <span data-ttu-id="e9824-146">若要避免迴圈狀況，請確定新原則的順序高於 [連線要求原則] 窗格中的原始原則。</span><span class="sxs-lookup"><span data-stu-id="e9824-146">To prevent a loop condition, make sure that the new policy is ordered ABOVE the original policy in the **Connection Request Policies** pane.</span></span>

## <a name="configure-azure-multi-factor-authentication"></a><span data-ttu-id="e9824-147">設定 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e9824-147">Configure Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="e9824-148">Azure Multi-Factor Authentication Server 設定為 RD 閘道器和 NPS 之間的 RADIUS Proxy。</span><span class="sxs-lookup"><span data-stu-id="e9824-148">The Azure Multi-Factor Authentication Server is configured as a RADIUS proxy between RD Gateway and NPS.</span></span>  <span data-ttu-id="e9824-149">它應該安裝在 RD 閘道器伺服器之外另一部加入網域的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="e9824-149">It should be installed on a domain-joined server that is separate from the RD Gateway server.</span></span> <span data-ttu-id="e9824-150">使用下列程序來設定 Azure Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="e9824-150">Use the following procedure to configure the Azure Multi-Factor Authentication Server.</span></span>

1. <span data-ttu-id="e9824-151">開啟 Azure Multi-Factor Authentication Server，然後選取 [RADIUS 驗證] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e9824-151">Open the Azure Multi-Factor Authentication Server and select the RADIUS Authentication icon.</span></span> 
2. <span data-ttu-id="e9824-152">選取 [啟用 RADIUS 驗證] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e9824-152">Check the **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="e9824-153">在 [用戶端] 索引標籤上，確定連接埠符合 NPS 中設定的連接埠，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e9824-153">On the Clients tab, ensure the ports match what is configured in NPS then select **Add**.</span></span>
4. <span data-ttu-id="e9824-154">新增 RD 閘道器伺服器 IP 位址、應用程式名稱 (選擇性) 和共用密碼。</span><span class="sxs-lookup"><span data-stu-id="e9824-154">Add the RD Gateway server IP address, application name (optional), and a shared secret.</span></span> <span data-ttu-id="e9824-155">Azure Multi-Factor Authentication Server 與 RD 閘道上的共用密碼必須相同。</span><span class="sxs-lookup"><span data-stu-id="e9824-155">The shared secret needs to be the same on both the Azure Multi-Factor Authentication Server and RD Gateway.</span></span>
3. <span data-ttu-id="e9824-156">移至 [目標] 索引標籤，然後選取 [RADIUS 伺服器] 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="e9824-156">Go to the **Target** tab and select the **RADIUS server(s)** radio button.</span></span>
4. <span data-ttu-id="e9824-157">選取 [新增] 並輸入 NPS 伺服器的 IP 位址、共用密碼和連接埠。</span><span class="sxs-lookup"><span data-stu-id="e9824-157">Select **Add** and enter the IP address, shared secret, and ports of the NPS server.</span></span> <span data-ttu-id="e9824-158">除非使用中央 NPS，否則 RADIUS 用戶端和 RADIUS 目標相同。</span><span class="sxs-lookup"><span data-stu-id="e9824-158">Unless using a central NPS, the RADIUS client and RADIUS target are the same.</span></span> <span data-ttu-id="e9824-159">共用密碼必須符合 NPS 伺服器的 RADIUS 用戶端區段中設定的共用密碼。</span><span class="sxs-lookup"><span data-stu-id="e9824-159">The shared secret must match the one setup in the RADIUS client section of the NPS server.</span></span>

![Radius 驗證](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a><span data-ttu-id="e9824-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9824-161">Next steps</span></span>

- <span data-ttu-id="e9824-162">整合 Azure MFA 與 [IIS Web Apps](multi-factor-authentication-get-started-server-iis.md)</span><span class="sxs-lookup"><span data-stu-id="e9824-162">Integrate Azure MFA and [IIS web apps](multi-factor-authentication-get-started-server-iis.md)</span></span>

- <span data-ttu-id="e9824-163">在 [Azure Multi-Factor Authentication 常見問題集](multi-factor-authentication-faq.md)中取得答案</span><span class="sxs-lookup"><span data-stu-id="e9824-163">Get answers in the [Azure Multi-Factor Authentication FAQ](multi-factor-authentication-faq.md)</span></span>
