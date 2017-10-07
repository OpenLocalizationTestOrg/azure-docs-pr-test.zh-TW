---
title: "驗證和 Azure MFA Server aaaRADIUS |Microsoft 文件"
description: "這是可協助您部署 RADIUS 驗證與 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="d1bea-103">將 RADIUS 驗證與 Azure Multi-Factor Authentication Server 整合</span><span class="sxs-lookup"><span data-stu-id="d1bea-103">Integrate RADIUS authentication with Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="d1bea-104">使用 Azure MFA Server tooenable hello RADIUS 驗證 區段並設定 RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="d1bea-104">Use hello RADIUS Authentication section of Azure MFA Server tooenable and configure RADIUS authentication.</span></span> <span data-ttu-id="d1bea-105">RADIUS 是標準通訊協定 tooaccept 驗證要求和 tooprocess 這些要求。</span><span class="sxs-lookup"><span data-stu-id="d1bea-105">RADIUS is a standard protocol tooaccept authentication requests and tooprocess those requests.</span></span> <span data-ttu-id="d1bea-106">hello Azure Multi-factor Authentication Server 做為 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1bea-106">hello Azure Multi-Factor Authentication Server acts as a RADIUS server.</span></span> <span data-ttu-id="d1bea-107">請將它插入您的 RADIUS 用戶端 （VPN 應用裝置） 和您可能是 Active Directory (AD)、 LDAP 目錄或其他 RADIUS 伺服器 tooadd Azure Multi-factor Authentication 的驗證目標之間。</span><span class="sxs-lookup"><span data-stu-id="d1bea-107">Insert it between your RADIUS client (VPN appliance) and your authentication target, which could be Active Directory (AD), an LDAP directory, or another RADIUS server tooadd Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="d1bea-108">針對 Azure Multi-factor Authentication (MFA) toofunction 中，您必須設定 Azure MFA Server hello，讓它可以與 hello 用戶端伺服器和 hello 驗證目標通訊。</span><span class="sxs-lookup"><span data-stu-id="d1bea-108">For Azure Multi-Factor Authentication (MFA) toofunction, you must configure hello Azure MFA Server so that it can communicate with both hello client servers and hello authentication target.</span></span> <span data-ttu-id="d1bea-109">hello Azure MFA Server 會接受來自 RADIUS 用戶端要求、 針對 hello 驗證目標驗證認證、 加入 Azure Multi-factor Authentication，和傳送回應後 toohello RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d1bea-109">hello Azure MFA Server accepts requests from a RADIUS client, validates credentials against hello authentication target, adds Azure Multi-Factor Authentication, and sends a response back toohello RADIUS client.</span></span> <span data-ttu-id="d1bea-110">只有 hello 主要驗證和 hello Azure 多重要素驗證成功，才會成功 hello 驗證要求。</span><span class="sxs-lookup"><span data-stu-id="d1bea-110">hello authentication request only succeeds if both hello primary authentication and hello Azure Multi-Factor Authentication succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="d1bea-111">hello MFA Server 只支援 PAP （密碼驗證通訊協定） 和 MSCHAPv2 （Microsoft Challenge Handshake 驗證通訊協定） 做為 RADIUS 伺服器時，RADIUS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d1bea-111">hello MFA Server only supports PAP (password authentication protocol) and MSCHAPv2 (Microsoft's Challenge-Handshake Authentication Protocol) RADIUS protocols when acting as a RADIUS server.</span></span>  <span data-ttu-id="d1bea-112">時 hello MFA server 做為支援該通訊協定的 RADIUS proxy tooanother RADIUS 伺服器，可以使用其他通訊協定，例如 EAP （可延伸驗證通訊協定）。</span><span class="sxs-lookup"><span data-stu-id="d1bea-112">Other protocols, like EAP (extensible authentication protocol), can be used when hello MFA server acts as a RADIUS proxy tooanother RADIUS server that supports that protocol.</span></span>
>
> <span data-ttu-id="d1bea-113">在此組態中，單向傳送 SMS 和 OATH 權杖不運作，因為 hello MFA Server 無法起始成功的 RADIUS 挑戰回應，使用替代的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d1bea-113">In this configuration, one-way SMS and OATH tokens don't work since hello MFA Server can't initiate a successful RADIUS Challenge response using alternative protocols.</span></span>

![Radius 驗證](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a><span data-ttu-id="d1bea-115">新增 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="d1bea-115">Add a RADIUS client</span></span>
<span data-ttu-id="d1bea-116">Windows server 上安裝 hello Azure Multi-factor Authentication Server tooconfigure RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="d1bea-116">tooconfigure RADIUS authentication, install hello Azure Multi-Factor Authentication Server on a Windows server.</span></span> <span data-ttu-id="d1bea-117">如果您有 Active Directory 環境，hello 伺服器應該加入的 toohello hello 網路內的網域。</span><span class="sxs-lookup"><span data-stu-id="d1bea-117">If you have an Active Directory environment, hello server should be joined toohello domain inside hello network.</span></span> <span data-ttu-id="d1bea-118">使用下列程序 tooconfigure hello Azure Multi-factor Authentication Server 的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1bea-118">Use hello following procedure tooconfigure hello Azure Multi-Factor Authentication Server:</span></span>

1. <span data-ttu-id="d1bea-119">在 hello Azure Multi-factor Authentication Server，按一下左窗格中 hello hello [RADIUS 驗證] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d1bea-119">In hello Azure Multi-Factor Authentication Server, click hello RADIUS Authentication icon in hello left menu.</span></span>
2. <span data-ttu-id="d1bea-120">檢查 hello**啟用 RADIUS 驗證**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d1bea-120">Check hello **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="d1bea-121">Hello 用戶端 索引標籤上變更 hello 驗證和帳戶處理連接埠如果 hello Azure MFA RADIUS 服務需要 toolisten 的非標準連接埠上的 RADIUS 要求。</span><span class="sxs-lookup"><span data-stu-id="d1bea-121">On hello Clients tab, change hello Authentication and Accounting ports if hello Azure MFA RADIUS service needs toolisten for RADIUS requests on non-standard ports.</span></span>
4. <span data-ttu-id="d1bea-122">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d1bea-122">Click **Add**.</span></span>
5. <span data-ttu-id="d1bea-123">輸入 hello hello 應用裝置/伺服器將向 Azure Multi-factor Authentication Server toohello、 應用程式名稱 （選擇性） 和共用的密碼的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d1bea-123">Enter hello IP address of hello appliance/server that will authenticate toohello Azure Multi-Factor Authentication Server, an application name (optional), and a shared secret.</span></span>

  <span data-ttu-id="d1bea-124">hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。</span><span class="sxs-lookup"><span data-stu-id="d1bea-124">hello application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>

  <span data-ttu-id="d1bea-125">hello 的共用密碼需要 toobe hello 相同的兩個 hello Azure Multi-factor Authentication Server 和應用裝置/伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1bea-125">hello shared secret needs toobe hello same on both hello Azure Multi-Factor Authentication Server and appliance/server.</span></span>

6. <span data-ttu-id="d1bea-126">檢查 hello**需要進行 Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="d1bea-126">Check hello **Require Multi-Factor Authentication user match** box if all users have been or will be imported into hello Server and subject toomulti-factor authentication.</span></span> <span data-ttu-id="d1bea-127">如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於兩步驟驗證，請不要 hello 方塊中選取。</span><span class="sxs-lookup"><span data-stu-id="d1bea-127">If a significant number of users have not yet been imported into hello Server and/or will be exempt from two-step verification, leave hello box unchecked.</span></span>
7. <span data-ttu-id="d1bea-128">檢查 hello**啟用後援 OATH 權杖**方塊，如果您要從行動裝置驗證應用程式的 toouse OATH 密碼做為後援 toohello 的頻外通話、 簡訊，或推播通知。</span><span class="sxs-lookup"><span data-stu-id="d1bea-128">Check hello **Enable fallback OATH token** box if you want toouse OATH passcodes from mobile verification apps as a fallback toohello out-of-band phone call, SMS, or push notification.</span></span>
8. <span data-ttu-id="d1bea-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d1bea-129">Click **OK**.</span></span>

<span data-ttu-id="d1bea-130">許多其他 RADIUS 用戶端視需要重複步驟 4 到 8 tooadd。</span><span class="sxs-lookup"><span data-stu-id="d1bea-130">Repeat steps 4 through 8 tooadd as many additional RADIUS clients as you need.</span></span>

## <a name="configure-your-radius-client"></a><span data-ttu-id="d1bea-131">設定 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="d1bea-131">Configure your RADIUS client</span></span>

1. <span data-ttu-id="d1bea-132">按一下 hello**目標** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d1bea-132">Click hello **Target** tab.</span></span>
2. <span data-ttu-id="d1bea-133">如果 hello Azure MFA Server 安裝在 Active Directory 環境中已加入網域的伺服器上，選取 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="d1bea-133">If hello Azure MFA Server is installed on a domain-joined server in an Active Directory environment, select Windows domain.</span></span>
3. <span data-ttu-id="d1bea-134">如果應該向 LDAP 目錄驗證使用者，請選取 [LDAP 繫結]。</span><span class="sxs-lookup"><span data-stu-id="d1bea-134">If users should be authenticated against an LDAP directory, select **LDAP bind**.</span></span>

  <span data-ttu-id="d1bea-135">toouse LDAP 繫結，按一下 hello 目錄整合 圖示，然後編輯 hello hello 設定 索引標籤上的 LDAP 組態，使 hello 伺服器可以將繫結 tooyour 目錄。</span><span class="sxs-lookup"><span data-stu-id="d1bea-135">toouse LDAP bind, click hello Directory Integration icon and edit hello LDAP configuration on hello Settings tab so that hello Server can bind tooyour directory.</span></span> <span data-ttu-id="d1bea-136">可以找到設定 LDAP 的指示，在 hello [LDAP Proxy 組態指南](multi-factor-authentication-get-started-server-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="d1bea-136">Instructions for configuring LDAP can be found in hello [LDAP Proxy configuration guide](multi-factor-authentication-get-started-server-ldap.md).</span></span>

4. <span data-ttu-id="d1bea-137">如果應該向另一部 RADIUS 伺服器驗證使用者，選取 [RADIUS 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="d1bea-137">If users should be authenticated against another RADIUS server, select RADIUS server(s).</span></span>
5. <span data-ttu-id="d1bea-138">按一下**新增**tooconfigure hello 伺服器 toowhich hello Azure MFA Server 將 proxy hello RADIUS 要求。</span><span class="sxs-lookup"><span data-stu-id="d1bea-138">Click **Add** tooconfigure hello server toowhich hello Azure MFA Server will proxy hello RADIUS requests.</span></span>
6. <span data-ttu-id="d1bea-139">在 hello [新增 RADIUS 伺服器] 對話方塊中，輸入 hello IP 位址的 hello RADIUS 伺服器和共用的密碼。</span><span class="sxs-lookup"><span data-stu-id="d1bea-139">In hello Add RADIUS Server dialog box, enter hello IP address of hello RADIUS server and a shared secret.</span></span>

  <span data-ttu-id="d1bea-140">hello 的共用密碼需要 toobe hello 相同的兩個 hello Azure Multi-factor Authentication Server 和 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1bea-140">hello shared secret needs toobe hello same on both hello Azure Multi-Factor Authentication Server and RADIUS server.</span></span> <span data-ttu-id="d1bea-141">如果 hello RADIUS 伺服器會使用不同的通訊埠，請變更 hello 驗證連接埠和帳戶處理連接埠。</span><span class="sxs-lookup"><span data-stu-id="d1bea-141">Change hello Authentication port and Accounting port if different ports are used by hello RADIUS server.</span></span>

7. <span data-ttu-id="d1bea-142">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d1bea-142">Click **OK**.</span></span>
8. <span data-ttu-id="d1bea-143">新增 Azure MFA Server 的 RADIUS 用戶端中 hello hello 其他 RADIUS 伺服器，使它可以處理 tooit 寄 hello Azure MFA Server 的存取要求。</span><span class="sxs-lookup"><span data-stu-id="d1bea-143">Add hello Azure MFA Server as a RADIUS client in hello other RADIUS server so that it can process access requests sent tooit from hello Azure MFA Server.</span></span> <span data-ttu-id="d1bea-144">使用共用 hello Azure Multi-factor Authentication Server 中設定密碼相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="d1bea-144">Use hello same shared secret configured in hello Azure Multi-Factor Authentication Server.</span></span>

<span data-ttu-id="d1bea-145">重複這些步驟 tooadd 更多的 RADIUS 伺服器，並設定 hello 順序中的 hello Azure MFA Server 呼叫它們以 hello**移**和**下移**按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1bea-145">Repeat these steps tooadd more RADIUS servers and configure hello order in which hello Azure MFA Server should call them with hello **Move Up** and **Move Down** buttons.</span></span>

<span data-ttu-id="d1bea-146">如此即完成 hello Azure Multi-factor Authentication Server 設定。</span><span class="sxs-lookup"><span data-stu-id="d1bea-146">This completes hello Azure Multi-Factor Authentication Server configuration.</span></span> <span data-ttu-id="d1bea-147">hello 伺服器的 RADIUS 存取要求來自 hello 設定用戶端正在 hello 設定連接埠上接聽。</span><span class="sxs-lookup"><span data-stu-id="d1bea-147">hello Server is now listening on hello configured ports for RADIUS access requests from hello configured clients.</span></span>   

## <a name="radius-client-configuration"></a><span data-ttu-id="d1bea-148">RADIUS 用戶端組態</span><span class="sxs-lookup"><span data-stu-id="d1bea-148">RADIUS Client configuration</span></span>
<span data-ttu-id="d1bea-149">tooconfigure hello RADIUS 用戶端，使用 hello 指導方針：</span><span class="sxs-lookup"><span data-stu-id="d1bea-149">tooconfigure hello RADIUS client, use hello guidelines:</span></span>

* <span data-ttu-id="d1bea-150">設定您的應用裝置/伺服器 tooauthenticate 透過 RADIUS toohello Azure Multi-factor Authentication Server 的 IP 位址，就會成為 hello RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1bea-150">Configure your appliance/server tooauthenticate via RADIUS toohello Azure Multi-Factor Authentication Server’s IP address, which will act as hello RADIUS server.</span></span>
* <span data-ttu-id="d1bea-151">使用先前設定的密碼共用相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="d1bea-151">Use hello same shared secret that was configured earlier.</span></span>
* <span data-ttu-id="d1bea-152">設定 hello RADIUS 逾時 too30 60 秒，以便有時間 toovalidate hello 使用者的認證、 執行雙步驟驗證、 接收其回應，以及然後回應 toohello RADIUS 存取要求。</span><span class="sxs-lookup"><span data-stu-id="d1bea-152">Configure hello RADIUS timeout too30-60 seconds so that there is time toovalidate hello user’s credentials, perform two-step verification, receive their response, and then respond toohello RADIUS access request.</span></span>
