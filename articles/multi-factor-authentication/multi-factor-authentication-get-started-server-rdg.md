---
title: "aaaRDG 和使用 RADIUS 的 Azure MFA Server |Microsoft 文件"
description: "這是可協助您部署遠端桌面閘道與 Azure Multi-factor Authentication Server 驗證使用 RADIUS 的 hello Azure 多因素驗證頁面。"
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
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a><span data-ttu-id="6a97a-103">使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="6a97a-103">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>
<span data-ttu-id="6a97a-104">通常，遠端桌面閘道會使用本機網路原則的服務 」 (NPS) tooauthenticate 使用者 hello。</span><span class="sxs-lookup"><span data-stu-id="6a97a-104">Often, Remote Desktop (RD) Gateway uses hello local Network Policy Services (NPS) tooauthenticate users.</span></span> <span data-ttu-id="6a97a-105">本文說明如何 tooroute RADIUS 要求出從 hello 遠端桌面閘道 (透過 hello 本機 NPS) toohello Multi-factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="6a97a-105">This article describes how tooroute RADIUS requests out from hello Remote Desktop Gateway (through hello local NPS) toohello Multi-Factor Authentication Server.</span></span> <span data-ttu-id="6a97a-106">hello Azure MFA 和 RD 閘道的組合表示您的使用者可以從任何地方存取其工作環境執行強式驗證時。</span><span class="sxs-lookup"><span data-stu-id="6a97a-106">hello combination of Azure MFA and RD Gateway means that your users can access their work environments from anywhere while performing strong authentication.</span></span> 

<span data-ttu-id="6a97a-107">由於終端機服務的 Windows 驗證不支援 Server 2012 r2 中，使用 MFA Server RD 閘道和 RADIUS toointegrate。</span><span class="sxs-lookup"><span data-stu-id="6a97a-107">Since Windows Authentication for terminal services is not supported for Server 2012 R2, use RD Gateway and RADIUS toointegrate with MFA Server.</span></span> 

<span data-ttu-id="6a97a-108">Hello Azure Multi-factor Authentication Server 伺服器上安裝不同，hello RADIUS 要求哪些 proxy hello 遠端桌面閘道伺服器上備份 toohello NPS。</span><span class="sxs-lookup"><span data-stu-id="6a97a-108">Install hello Azure Multi-Factor Authentication Server on a separate server, which proxies hello RADIUS request back toohello NPS on hello Remote Desktop Gateway Server.</span></span> <span data-ttu-id="6a97a-109">NPS 驗證 hello 使用者名稱和密碼之後，它會傳回回應 toohello Multi-factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="6a97a-109">After NPS validates hello username and password, it returns a response toohello Multi-Factor Authentication Server.</span></span> <span data-ttu-id="6a97a-110">然後，MFA Server hello 執行 hello 第二個驗證因素，並傳回結果 toohello 閘道。</span><span class="sxs-lookup"><span data-stu-id="6a97a-110">Then, hello MFA Server performs hello second factor of authentication and returns a result toohello gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a97a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a97a-111">Prerequisites</span></span>

- <span data-ttu-id="6a97a-112">已加入網域的 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="6a97a-112">A domain-joined Azure MFA Server.</span></span> <span data-ttu-id="6a97a-113">如果沒有任何已安裝，請依照下列中的 hello 步驟[hello Azure Multi-factor Authentication Server 使用者入門](multi-factor-authentication-get-started-server.md)。</span><span class="sxs-lookup"><span data-stu-id="6a97a-113">If you don't have one installed already, follow hello steps in [Getting started with hello Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server.md).</span></span>
- <span data-ttu-id="6a97a-114">使用網路原則服務進行驗證的遠端桌面閘道。</span><span class="sxs-lookup"><span data-stu-id="6a97a-114">A Remote Desktop Gateway that authenticates with Network Policy Services.</span></span>

## <a name="configure-hello-remote-desktop-gateway"></a><span data-ttu-id="6a97a-115">設定遠端桌面閘道 hello</span><span class="sxs-lookup"><span data-stu-id="6a97a-115">Configure hello Remote Desktop Gateway</span></span>
<span data-ttu-id="6a97a-116">設定 hello RD 閘道 toosend RADIUS 驗證 tooan Azure Multi-factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="6a97a-116">Configure hello RD Gateway toosend RADIUS authentication tooan Azure Multi-Factor Authentication Server.</span></span> 

1. <span data-ttu-id="6a97a-117">在 RD 閘道管理員中，以滑鼠右鍵按一下 hello 伺服器名稱，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-117">In RD Gateway Manager, right-click hello server name and select **Properties**.</span></span>
2. <span data-ttu-id="6a97a-118">移 toohello **RD CAP 存放區**索引標籤並選取**執行 NPS 的中央伺服器**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-118">Go toohello **RD CAP Store** tab and select **Central server running NPS**.</span></span> 
3. <span data-ttu-id="6a97a-119">輸入 hello 名稱或 IP 位址的每一部伺服器，一或多個 Azure Multi-factor Authentication Server 新增為 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6a97a-119">Add one or more Azure Multi-Factor Authentication Servers as RADIUS servers by entering hello name or IP address of each server.</span></span> 
4. <span data-ttu-id="6a97a-120">為每一部伺服器建立共用密碼。</span><span class="sxs-lookup"><span data-stu-id="6a97a-120">Create a shared secret for each server.</span></span>

## <a name="configure-nps"></a><span data-ttu-id="6a97a-121">設定 NPS</span><span class="sxs-lookup"><span data-stu-id="6a97a-121">Configure NPS</span></span>
<span data-ttu-id="6a97a-122">hello RD 閘道使用 NPS toosend hello RADIUS 要求 tooAzure Multi-factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="6a97a-122">hello RD Gateway uses NPS toosend hello RADIUS request tooAzure Multi-Factor Authentication.</span></span> <span data-ttu-id="6a97a-123">tooconfigure NPS，首先您變更 hello hello 雙步驟驗證完成之前，tooprevent hello RD 閘道在逾時的逾時設定。</span><span class="sxs-lookup"><span data-stu-id="6a97a-123">tooconfigure NPS, first you change hello timeout settings tooprevent hello RD Gateway from timing out before hello two-step verification has completed.</span></span> <span data-ttu-id="6a97a-124">接著，您會從您的 MFA 伺服器更新 NPS tooreceive RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="6a97a-124">Then, you update NPS tooreceive RADIUS authentications from your MFA Server.</span></span> <span data-ttu-id="6a97a-125">使用下列程序 tooconfigure NPS hello:</span><span class="sxs-lookup"><span data-stu-id="6a97a-125">Use hello following procedure tooconfigure NPS:</span></span>

### <a name="modify-hello-timeout-policy"></a><span data-ttu-id="6a97a-126">修改 hello 逾時原則</span><span class="sxs-lookup"><span data-stu-id="6a97a-126">Modify hello timeout policy</span></span>

1. <span data-ttu-id="6a97a-127">在 NPS 中，開啟 hello **RADIUS 用戶端和伺服器**hello 剩餘資料行，然後選取功能表**遠端 RADIUS 伺服器群組**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-127">In NPS, open hello **RADIUS Clients and Server** menu in hello left column and select **Remote RADIUS Server Groups**.</span></span> 
2. <span data-ttu-id="6a97a-128">選取 hello **TS GATEWAY SERVER GROUP**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-128">Select hello **TS GATEWAY SERVER GROUP**.</span></span> 
3. <span data-ttu-id="6a97a-129">移 toohello**負載平衡** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6a97a-129">Go toohello **Load Balancing** tab.</span></span> 
4. <span data-ttu-id="6a97a-130">變更這兩個 hello**卸除的要求都視為前，無回應的秒數**和 hello**伺服器被識別為無法使用時，在要求之間的秒數**toobetween 30 到 60秒數。</span><span class="sxs-lookup"><span data-stu-id="6a97a-130">Change both hello **Number of seconds without response before request is considered dropped** and hello **Number of seconds between requests when server is identified as unavailable** toobetween 30 and 60 seconds.</span></span> <span data-ttu-id="6a97a-131">（如果您發現該 hello 伺服器仍然會逾時在驗證期間，您可以再回到這裡並增加 hello 秒數。）</span><span class="sxs-lookup"><span data-stu-id="6a97a-131">(If you find that hello server still times out during authentication, you can come back here and increase hello number of seconds.)</span></span>
5. <span data-ttu-id="6a97a-132">移 toohello**驗證/帳戶**索引標籤上，檢查指定相符項目 hello 連接埠接聽 Multi-factor Authentication Server 的 hello hello RADIUS 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6a97a-132">Go toohello **Authentication/Account** tab and check that hello RADIUS ports specified match hello ports that hello Multi-Factor Authentication Server is listening on.</span></span>

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a><span data-ttu-id="6a97a-133">準備從 hello MFA Server NPS tooreceive 驗證</span><span class="sxs-lookup"><span data-stu-id="6a97a-133">Prepare NPS tooreceive authentications from hello MFA Server</span></span>

1. <span data-ttu-id="6a97a-134">以滑鼠右鍵按一下**RADIUS 用戶端**RADIUS 用戶端和伺服器 hello 剩餘資料行，然後選取底下**新增**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-134">Right-click **RADIUS Clients** under RADIUS Clients and Servers in hello left column and select **New**.</span></span>
2. <span data-ttu-id="6a97a-135">新增 hello Azure Multi-factor Authentication Server 的 RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6a97a-135">Add hello Azure Multi-Factor Authentication Server as a RADIUS client.</span></span> <span data-ttu-id="6a97a-136">選擇 [好記的名稱] 並指定共用密碼。</span><span class="sxs-lookup"><span data-stu-id="6a97a-136">Choose a Friendly name and specify a shared secret.</span></span>
3. <span data-ttu-id="6a97a-137">開啟 hello**原則**hello 剩餘資料行，然後選取功能表**連線要求原則**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-137">Open hello **Policies** menu in hello left column and select **Connection Request Policies**.</span></span> <span data-ttu-id="6a97a-138">您應會看見在設定 RD 閘道時所建立的原則，其名稱為 [TS 閘道授權原則]。</span><span class="sxs-lookup"><span data-stu-id="6a97a-138">You should see a policy called TS GATEWAY AUTHORIZATION POLICY that was created when RD Gateway was configured.</span></span> <span data-ttu-id="6a97a-139">此原則轉送 RADIUS 要求 toohello Multi-factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="6a97a-139">This policy forwards RADIUS requests toohello Multi-Factor Authentication Server.</span></span>
4. <span data-ttu-id="6a97a-140">以滑鼠右鍵按一下 [TS 閘道授權原則]，然後選取 [重複原則]。</span><span class="sxs-lookup"><span data-stu-id="6a97a-140">Right-click **TS GATEWAY AUTHORIZATION POLICY** and select **Duplicate Policy**.</span></span> 
5. <span data-ttu-id="6a97a-141">開啟 hello 新原則，然後移至 toohello**條件** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6a97a-141">Open hello new policy and go toohello **Conditions** tab.</span></span>
6. <span data-ttu-id="6a97a-142">加入條件符合 hello hello hello Azure Multi-factor Authentication Server RADIUS 用戶端的步驟 2 中設定的易記名稱的用戶端易記名稱。</span><span class="sxs-lookup"><span data-stu-id="6a97a-142">Add a condition that matches hello Client Friendly Name with hello Friendly name set in step 2 for hello Azure Multi-Factor Authentication Server RADIUS client.</span></span> 
7. <span data-ttu-id="6a97a-143">移 toohello**設定**索引標籤並選取**驗證**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-143">Go toohello **Settings** tab and select **Authentication**.</span></span>
8. <span data-ttu-id="6a97a-144">變更 hello 驗證提供者太**驗證此伺服器上的要求**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-144">Change hello Authentication Provider too**Authenticate requests on this server**.</span></span> <span data-ttu-id="6a97a-145">此原則可確保當 NPS 收到 RADIUS 要求從 hello Azure MFA Server 時，在本機而不是傳送 RADIUS 要求後 toohello Azure Multi-factor Authentication Server，可能會導致迴圈狀況發生 hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="6a97a-145">This policy ensures that when NPS receives a RADIUS request from hello Azure MFA Server, hello authentication occurs locally instead of sending a RADIUS request back toohello Azure Multi-Factor Authentication Server, which would result in a loop condition.</span></span> 
9. <span data-ttu-id="6a97a-146">tooprevent 迴圈條件，請確定 hello 新原則會排序在 hello hello 原始原則之上**連線要求原則**窗格。</span><span class="sxs-lookup"><span data-stu-id="6a97a-146">tooprevent a loop condition, make sure that hello new policy is ordered ABOVE hello original policy in hello **Connection Request Policies** pane.</span></span>

## <a name="configure-azure-multi-factor-authentication"></a><span data-ttu-id="6a97a-147">設定 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6a97a-147">Configure Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="6a97a-148">hello Azure Multi-factor Authentication Server 會設定為 RD 閘道和 NPS 之間的 RADIUS proxy。</span><span class="sxs-lookup"><span data-stu-id="6a97a-148">hello Azure Multi-Factor Authentication Server is configured as a RADIUS proxy between RD Gateway and NPS.</span></span>  <span data-ttu-id="6a97a-149">它應該與 hello RD 閘道伺服器位於不同網域的伺服器上安裝。</span><span class="sxs-lookup"><span data-stu-id="6a97a-149">It should be installed on a domain-joined server that is separate from hello RD Gateway server.</span></span> <span data-ttu-id="6a97a-150">使用下列程序 tooconfigure hello Azure Multi-factor Authentication Server 的 hello。</span><span class="sxs-lookup"><span data-stu-id="6a97a-150">Use hello following procedure tooconfigure hello Azure Multi-Factor Authentication Server.</span></span>

1. <span data-ttu-id="6a97a-151">開啟 hello Azure Multi-factor Authentication Server，然後選取 hello RADIUS 驗證 圖示。</span><span class="sxs-lookup"><span data-stu-id="6a97a-151">Open hello Azure Multi-Factor Authentication Server and select hello RADIUS Authentication icon.</span></span> 
2. <span data-ttu-id="6a97a-152">檢查 hello**啟用 RADIUS 驗證**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6a97a-152">Check hello **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="6a97a-153">Hello 用戶端] 索引標籤，確定 hello 連接埠符合 NPS 中的設定，然後選取 [**新增**。</span><span class="sxs-lookup"><span data-stu-id="6a97a-153">On hello Clients tab, ensure hello ports match what is configured in NPS then select **Add**.</span></span>
4. <span data-ttu-id="6a97a-154">加入 hello RD 閘道伺服器 IP 位址、 應用程式名稱 （選用） 和共用的密碼。</span><span class="sxs-lookup"><span data-stu-id="6a97a-154">Add hello RD Gateway server IP address, application name (optional), and a shared secret.</span></span> <span data-ttu-id="6a97a-155">hello 共用密碼需要 toobe hello 相同 hello Azure Multi-factor Authentication Server 和 RD 閘道上。</span><span class="sxs-lookup"><span data-stu-id="6a97a-155">hello shared secret needs toobe hello same on both hello Azure Multi-Factor Authentication Server and RD Gateway.</span></span>
3. <span data-ttu-id="6a97a-156">移 toohello**目標** 索引標籤並選取 hello **RADIUS 伺服器**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a97a-156">Go toohello **Target** tab and select hello **RADIUS server(s)** radio button.</span></span>
4. <span data-ttu-id="6a97a-157">選取**新增**，然後輸入 hello IP 位址、 共用的密碼和 hello NPS 伺服器的連接埠。</span><span class="sxs-lookup"><span data-stu-id="6a97a-157">Select **Add** and enter hello IP address, shared secret, and ports of hello NPS server.</span></span> <span data-ttu-id="6a97a-158">除非使用中央 NPS，否則 hello RADIUS 用戶端和 RADIUS 目標是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="6a97a-158">Unless using a central NPS, hello RADIUS client and RADIUS target are hello same.</span></span> <span data-ttu-id="6a97a-159">hello 共用的密碼必須符合 hello hello hello NPS 伺服器的 RADIUS 用戶端區段中的一個安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6a97a-159">hello shared secret must match hello one setup in hello RADIUS client section of hello NPS server.</span></span>

![Radius 驗證](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a><span data-ttu-id="6a97a-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a97a-161">Next steps</span></span>

- <span data-ttu-id="6a97a-162">整合 Azure MFA 與 [IIS Web Apps](multi-factor-authentication-get-started-server-iis.md)</span><span class="sxs-lookup"><span data-stu-id="6a97a-162">Integrate Azure MFA and [IIS web apps](multi-factor-authentication-get-started-server-iis.md)</span></span>

- <span data-ttu-id="6a97a-163">在 hello 解答[Azure Multi-factor Authentication 常見問題集](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6a97a-163">Get answers in hello [Azure Multi-Factor Authentication FAQ](multi-factor-authentication-faq.md)</span></span>
