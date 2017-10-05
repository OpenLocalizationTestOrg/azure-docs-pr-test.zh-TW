---
title: "RADIUS 驗證和 Azure MFA Server | Microsoft Docs"
description: "此 Azure Multi-Factor Authentication 頁面協助您部署 RADIUS 驗證與 Azure Multi-Factor Authentication Server。"
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
ms.openlocfilehash: a4c52cc40b17902d92f7a94028ddb3c641911e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="149bc-103">將 RADIUS 驗證與 Azure Multi-Factor Authentication Server 整合</span><span class="sxs-lookup"><span data-stu-id="149bc-103">Integrate RADIUS authentication with Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="149bc-104">使用 Azure MFA Server 的 [RADIUS 驗證] 區段來啟用和設定 RADIUS 驗證。</span><span class="sxs-lookup"><span data-stu-id="149bc-104">Use the RADIUS Authentication section of Azure MFA Server to enable and configure RADIUS authentication.</span></span> <span data-ttu-id="149bc-105">RADIUS 是接受驗證要求並處理這些要求的標準通訊協定。</span><span class="sxs-lookup"><span data-stu-id="149bc-105">RADIUS is a standard protocol to accept authentication requests and to process those requests.</span></span> <span data-ttu-id="149bc-106">Azure Multi-Factor Authentication Server 會作為 RADIUS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="149bc-106">The Azure Multi-Factor Authentication Server acts as a RADIUS server.</span></span> <span data-ttu-id="149bc-107">將它插入在 RADIUS 用戶端 (VPN 應用裝置) 與驗證目標 (可以是 Active Directory (AD)、LDAP 目錄或另一部 RADIUS 伺服器) 之間，以新增 Azure Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="149bc-107">Insert it between your RADIUS client (VPN appliance) and your authentication target, which could be Active Directory (AD), an LDAP directory, or another RADIUS server to add Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="149bc-108">為了讓 Azure Multi-Factor Authentication (MFA) 運作，必須將 Azure MFA Server 設定為能夠與用戶端伺服器和驗證目標進行通訊。</span><span class="sxs-lookup"><span data-stu-id="149bc-108">For Azure Multi-Factor Authentication (MFA) to function, you must configure the Azure MFA Server so that it can communicate with both the client servers and the authentication target.</span></span> <span data-ttu-id="149bc-109">Azure MFA Server 會從 RADIUS 用戶端接收要求、向驗證目標驗證認證、新增 Azure Multi-Factor Authentication，然後將回應傳回給 RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="149bc-109">The Azure MFA Server accepts requests from a RADIUS client, validates credentials against the authentication target, adds Azure Multi-Factor Authentication, and sends a response back to the RADIUS client.</span></span> <span data-ttu-id="149bc-110">只有當主要驗證和 Azure Multi-Factor Authentication 都成功時，驗證要求才會成功。</span><span class="sxs-lookup"><span data-stu-id="149bc-110">The authentication request only succeeds if both the primary authentication and the Azure Multi-Factor Authentication succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="149bc-111">MFA 伺服器在做為 RADIUS 伺服器時，僅支援 PAP (密碼驗證通訊協定) 和 MSCHAPv2 (Microsoft 的 Challenge-Handshake 驗證通訊協定) RADIUS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="149bc-111">The MFA Server only supports PAP (password authentication protocol) and MSCHAPv2 (Microsoft's Challenge-Handshake Authentication Protocol) RADIUS protocols when acting as a RADIUS server.</span></span>  <span data-ttu-id="149bc-112">當 MFA Server 是作為另一部 RADIUS 伺服器的 RADIUS Proxy，而該伺服器支援 EAP (可延伸的驗證通訊協定) 這類其他通訊協定時，則也可以使用該通訊協定。</span><span class="sxs-lookup"><span data-stu-id="149bc-112">Other protocols, like EAP (extensible authentication protocol), can be used when the MFA server acts as a RADIUS proxy to another RADIUS server that supports that protocol.</span></span>
>
> <span data-ttu-id="149bc-113">在此組態中，單向 SMS 和 OATH 權杖沒有作用，因為 MFA Server 無法使用替代通訊協定來起始成功的 RADIUS 挑戰回應。</span><span class="sxs-lookup"><span data-stu-id="149bc-113">In this configuration, one-way SMS and OATH tokens don't work since the MFA Server can't initiate a successful RADIUS Challenge response using alternative protocols.</span></span>

![Radius 驗證](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a><span data-ttu-id="149bc-115">新增 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="149bc-115">Add a RADIUS client</span></span>
<span data-ttu-id="149bc-116">若要設定 RADIUS 驗證，請在 Windows 伺服器上安裝 Azure Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="149bc-116">To configure RADIUS authentication, install the Azure Multi-Factor Authentication Server on a Windows server.</span></span> <span data-ttu-id="149bc-117">如果您有 Active Directory 環境，此伺服器應該加入網路內的網域。</span><span class="sxs-lookup"><span data-stu-id="149bc-117">If you have an Active Directory environment, the server should be joined to the domain inside the network.</span></span> <span data-ttu-id="149bc-118">使用下列程序來設定 Azure Multi-Factor Authentication Server：</span><span class="sxs-lookup"><span data-stu-id="149bc-118">Use the following procedure to configure the Azure Multi-Factor Authentication Server:</span></span>

1. <span data-ttu-id="149bc-119">在 Azure Multi-Factor Authentication Server 中，按一下左功能表中的 [RADIUS 驗證] 圖示。</span><span class="sxs-lookup"><span data-stu-id="149bc-119">In the Azure Multi-Factor Authentication Server, click the RADIUS Authentication icon in the left menu.</span></span>
2. <span data-ttu-id="149bc-120">選取 [啟用 RADIUS 驗證] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="149bc-120">Check the **Enable RADIUS authentication** checkbox.</span></span>
3. <span data-ttu-id="149bc-121">如果 Azure MFA RADIUS 服務需要在非標準連接埠上接聽 RADIUS 要求，請在 [用戶端] 索引標籤上變更 [驗證連接埠] 和 [帳戶處理連接埠]。</span><span class="sxs-lookup"><span data-stu-id="149bc-121">On the Clients tab, change the Authentication and Accounting ports if the Azure MFA RADIUS service needs to listen for RADIUS requests on non-standard ports.</span></span>
4. <span data-ttu-id="149bc-122">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="149bc-122">Click **Add**.</span></span>
5. <span data-ttu-id="149bc-123">輸入將向 Azure Multi-Factor Authentication Server 進行驗證之應用裝置/伺服器的 IP 位址、應用程式名稱 (選擇性)，以及 共用密碼。</span><span class="sxs-lookup"><span data-stu-id="149bc-123">Enter the IP address of the appliance/server that will authenticate to the Azure Multi-Factor Authentication Server, an application name (optional), and a shared secret.</span></span>

  <span data-ttu-id="149bc-124">應用程式名稱會出現在 Azure Multi-Factor Authentication 報告中，而可能顯示在簡訊或行動應用程式驗證訊息內。</span><span class="sxs-lookup"><span data-stu-id="149bc-124">The application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>

  <span data-ttu-id="149bc-125">共用密碼在 Azure Multi-Factor Authentication Server 和應用裝置/伺服器上必須相同。</span><span class="sxs-lookup"><span data-stu-id="149bc-125">The shared secret needs to be the same on both the Azure Multi-Factor Authentication Server and appliance/server.</span></span>

6. <span data-ttu-id="149bc-126">如果所有使用者都已經或將要匯入到伺服器中，且必須接受多重要素驗證，請選取 [需要進行 Multi-Factor Authentication 使用者比對] 方塊。</span><span class="sxs-lookup"><span data-stu-id="149bc-126">Check the **Require Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to multi-factor authentication.</span></span> <span data-ttu-id="149bc-127">如果有大量使用者尚未匯入伺服器及/或將免除雙步驟驗證，請勿核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="149bc-127">If a significant number of users have not yet been imported into the Server and/or will be exempt from two-step verification, leave the box unchecked.</span></span>
7. <span data-ttu-id="149bc-128">如果您想要使用來自行動驗證應用程式的 OATH 密碼作為頻外電話、簡訊或推播通知的遞補驗證，請核取 [啟用遞補 OATH 權杖] 方塊。</span><span class="sxs-lookup"><span data-stu-id="149bc-128">Check the **Enable fallback OATH token** box if you want to use OATH passcodes from mobile verification apps as a fallback to the out-of-band phone call, SMS, or push notification.</span></span>
8. <span data-ttu-id="149bc-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="149bc-129">Click **OK**.</span></span>

<span data-ttu-id="149bc-130">請重複步驟 4 到 8 以視需要新增多個其他 RADIUS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="149bc-130">Repeat steps 4 through 8 to add as many additional RADIUS clients as you need.</span></span>

## <a name="configure-your-radius-client"></a><span data-ttu-id="149bc-131">設定 RADIUS 用戶端</span><span class="sxs-lookup"><span data-stu-id="149bc-131">Configure your RADIUS client</span></span>

1. <span data-ttu-id="149bc-132">按一下 [目標] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="149bc-132">Click the **Target** tab.</span></span>
2. <span data-ttu-id="149bc-133">如果 Azure MFA Server 是安裝在 Active Directory 環境中已加入網域的伺服器上，請選取 [Windows 網域]。</span><span class="sxs-lookup"><span data-stu-id="149bc-133">If the Azure MFA Server is installed on a domain-joined server in an Active Directory environment, select Windows domain.</span></span>
3. <span data-ttu-id="149bc-134">如果應該向 LDAP 目錄驗證使用者，請選取 [LDAP 繫結]。</span><span class="sxs-lookup"><span data-stu-id="149bc-134">If users should be authenticated against an LDAP directory, select **LDAP bind**.</span></span>

  <span data-ttu-id="149bc-135">若要使用 LDAP 繫結，請按一下 [目錄整合] 圖示，然後編輯 [設定] 索引標籤上的 LDAP 組態，以便讓伺服器能夠繫結至您的目錄。</span><span class="sxs-lookup"><span data-stu-id="149bc-135">To use LDAP bind, click the Directory Integration icon and edit the LDAP configuration on the Settings tab so that the Server can bind to your directory.</span></span> <span data-ttu-id="149bc-136">如需有關設定 LDAP 的指示，請參閱 [LDAP Proxy 組態指南](multi-factor-authentication-get-started-server-ldap.md)。</span><span class="sxs-lookup"><span data-stu-id="149bc-136">Instructions for configuring LDAP can be found in the [LDAP Proxy configuration guide](multi-factor-authentication-get-started-server-ldap.md).</span></span>

4. <span data-ttu-id="149bc-137">如果應該向另一部 RADIUS 伺服器驗證使用者，選取 [RADIUS 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="149bc-137">If users should be authenticated against another RADIUS server, select RADIUS server(s).</span></span>
5. <span data-ttu-id="149bc-138">按一下 [新增] 以設定 Azure MFA Server 要作為其 Proxy 來處理 RADIUS 要求的伺服器。</span><span class="sxs-lookup"><span data-stu-id="149bc-138">Click **Add** to configure the server to which the Azure MFA Server will proxy the RADIUS requests.</span></span>
6. <span data-ttu-id="149bc-139">在 [新增 RADIUS 伺服器] 對話方塊中，輸入 RADIUS 伺服器的 IP 位址和共用密碼。</span><span class="sxs-lookup"><span data-stu-id="149bc-139">In the Add RADIUS Server dialog box, enter the IP address of the RADIUS server and a shared secret.</span></span>

  <span data-ttu-id="149bc-140">共用密碼在 Azure Multi-Factor Authentication Server 和 RADIUS 伺服器上必須相同。</span><span class="sxs-lookup"><span data-stu-id="149bc-140">The shared secret needs to be the same on both the Azure Multi-Factor Authentication Server and RADIUS server.</span></span> <span data-ttu-id="149bc-141">如果 RADIUS 伺服器使用不同的通訊埠，請變更 [驗證連接埠] 和 [帳戶處理連接埠]。</span><span class="sxs-lookup"><span data-stu-id="149bc-141">Change the Authentication port and Accounting port if different ports are used by the RADIUS server.</span></span>

7. <span data-ttu-id="149bc-142">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="149bc-142">Click **OK**.</span></span>
8. <span data-ttu-id="149bc-143">在另一部 RADIUS 伺服器中新增 Azure MFA Server 作為 RADIUS 用戶端，如此它才能夠處理從 Azure MFA Server 傳送給它的存取要求。</span><span class="sxs-lookup"><span data-stu-id="149bc-143">Add the Azure MFA Server as a RADIUS client in the other RADIUS server so that it can process access requests sent to it from the Azure MFA Server.</span></span> <span data-ttu-id="149bc-144">請使用 Azure Multi-Factor Authentication Server 中設定的相同共用密碼。</span><span class="sxs-lookup"><span data-stu-id="149bc-144">Use the same shared secret configured in the Azure Multi-Factor Authentication Server.</span></span>

<span data-ttu-id="149bc-145">您可以重複這些步驟來新增更多 RADIUS 伺服器，然後使用 [上移] 和 [下移] 按鈕來設定 Azure MFA Server 應呼叫它們的順序。</span><span class="sxs-lookup"><span data-stu-id="149bc-145">Repeat these steps to add more RADIUS servers and configure the order in which the Azure MFA Server should call them with the **Move Up** and **Move Down** buttons.</span></span>

<span data-ttu-id="149bc-146">如此便完成 Azure Multi-Factor Authentication Server 組態。</span><span class="sxs-lookup"><span data-stu-id="149bc-146">This completes the Azure Multi-Factor Authentication Server configuration.</span></span> <span data-ttu-id="149bc-147">「伺服器」正在設定的連接埠上接聽來自設定的用戶端的 RADIUS 存取要求。</span><span class="sxs-lookup"><span data-stu-id="149bc-147">The Server is now listening on the configured ports for RADIUS access requests from the configured clients.</span></span>   

## <a name="radius-client-configuration"></a><span data-ttu-id="149bc-148">RADIUS 用戶端組態</span><span class="sxs-lookup"><span data-stu-id="149bc-148">RADIUS Client configuration</span></span>
<span data-ttu-id="149bc-149">若要設定 RADIUS 用戶端，請遵循下列指導方針：</span><span class="sxs-lookup"><span data-stu-id="149bc-149">To configure the RADIUS client, use the guidelines:</span></span>

* <span data-ttu-id="149bc-150">將您的應用裝置/伺服器設定為透過 RADIUS 向 Azure Multi-Factor Authentication Server (將做為 RADIUS 伺服器) 的 IP 位址驗證。</span><span class="sxs-lookup"><span data-stu-id="149bc-150">Configure your appliance/server to authenticate via RADIUS to the Azure Multi-Factor Authentication Server’s IP address, which will act as the RADIUS server.</span></span>
* <span data-ttu-id="149bc-151">使用先前設定的相同共用密碼。</span><span class="sxs-lookup"><span data-stu-id="149bc-151">Use the same shared secret that was configured earlier.</span></span>
* <span data-ttu-id="149bc-152">將 RADIUS 逾時設定為 30 至 60 秒，以保留足夠的時間來驗證使用者的認證、執行兩步驟驗證、接收其回應，然後回應 RADIUS 存取要求。</span><span class="sxs-lookup"><span data-stu-id="149bc-152">Configure the RADIUS timeout to 30-60 seconds so that there is time to validate the user’s credentials, perform two-step verification, receive their response, and then respond to the RADIUS access request.</span></span>
