---
title: "使用 Azure AD App Proxy 發佈遠端桌面 | Microsoft Docs"
description: "涵蓋 Azure AD 應用程式 Proxy 連接器的基本概念。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 785bb4f893cf6861ef3b090d99780fd9b6b08c0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a><span data-ttu-id="0a87b-103">使用 Azure AD 應用程式 Proxy 發佈遠端桌面</span><span class="sxs-lookup"><span data-stu-id="0a87b-103">Publish Remote Desktop with Azure AD Application Proxy</span></span>

<span data-ttu-id="0a87b-104">本文說明如何使用應用程式 Proxy 來部署遠端桌面服務 (RDS)，讓遠端使用者仍可創造生產力。</span><span class="sxs-lookup"><span data-stu-id="0a87b-104">This article covers how to deploy Remote Desktop Services (RDS) with Application Proxy so that remote users can still be productive.</span></span>

<span data-ttu-id="0a87b-105">本文的目標對象是︰</span><span class="sxs-lookup"><span data-stu-id="0a87b-105">The intended audience for this article is:</span></span>
- <span data-ttu-id="0a87b-106">目前的 Azure AD 應用程式 Proxy 客戶，想要透過遠端桌面服務發佈內部部署應用程式，以提供更多使用者應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a87b-106">Current Azure AD Application Proxy customers who want to offer more applications to their end users by publishing on-premises applications through Remote Desktop Services.</span></span>
- <span data-ttu-id="0a87b-107">目前的遠端桌面服務客戶，想要使用 Azure AD 應用程式 Proxy 來減少其部署的 Attack Surface。</span><span class="sxs-lookup"><span data-stu-id="0a87b-107">Current Remote Desktop Services customers who want to reduce the attack surface of their deployment by using Azure AD Application Proxy.</span></span> <span data-ttu-id="0a87b-108">這種情況下，會向 RDS 提供一組有限的雙步驟驗證和條件式存取控制。</span><span class="sxs-lookup"><span data-stu-id="0a87b-108">This scenario gives a limited set of two-step verification and conditional access controls to RDS.</span></span>

## <a name="how-application-proxy-fits-in-the-standard-rds-deployment"></a><span data-ttu-id="0a87b-109">應用程式 Proxy 如何放入標準 RDS 部署中</span><span class="sxs-lookup"><span data-stu-id="0a87b-109">How Application Proxy fits in the standard RDS deployment</span></span>

<span data-ttu-id="0a87b-110">標準 RDS 部署包含 Windows Server 上執行的各種遠端桌面角色服務。</span><span class="sxs-lookup"><span data-stu-id="0a87b-110">A standard RDS deployment includes various Remote Desktop role services running on Windows Server.</span></span> <span data-ttu-id="0a87b-111">查看[遠端桌面服務架構](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture)，有多個部署選項。</span><span class="sxs-lookup"><span data-stu-id="0a87b-111">Looking at the [Remote Desktop Services architecture](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), there are multiple deployment options.</span></span> <span data-ttu-id="0a87b-112">[使用 Azure AD 應用程式 Proxy 的 RDS 部署](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (如下圖所示) 和其他部署選項最明顯的差異，就是應用程式 Proxy 案例具有執行連接器服務之伺服器的永久輸出連線。</span><span class="sxs-lookup"><span data-stu-id="0a87b-112">The most noticeable difference between the [RDS deployment with Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (shown in the following diagram) and the other deployment options is that the Application Proxy scenario has a permanent outbound connection from the server running the connector service.</span></span> <span data-ttu-id="0a87b-113">其他部署會透過負載平衡器保留開啟的輸入連線。</span><span class="sxs-lookup"><span data-stu-id="0a87b-113">Other deployments leave open inbound connections through a load balancer.</span></span>

![應用程式 Proxy 位於 RDS VM 與公用網際網路之間](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

<span data-ttu-id="0a87b-115">在 RDS 部署中，RD Web 角色和 RD 閘道角色是在網際網路對應的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="0a87b-115">In an RDS deployment, the RD Web role and the RD Gateway role run on Internet-facing machines.</span></span> <span data-ttu-id="0a87b-116">這些端點是公開的，原因如下︰</span><span class="sxs-lookup"><span data-stu-id="0a87b-116">These endpoints are exposed for the following reasons:</span></span>
- <span data-ttu-id="0a87b-117">RD Web 會向使用者提供公用端點，可用來登入及檢視他們可以存取的各種內部部署應用程式和桌上型電腦。</span><span class="sxs-lookup"><span data-stu-id="0a87b-117">RD Web provides the user a public endpoint to sign in and view the various on-premises applications and desktops they can access.</span></span> <span data-ttu-id="0a87b-118">在選取資源時，會使用作業系統上的原生應用程式來建立 RDP 連線。</span><span class="sxs-lookup"><span data-stu-id="0a87b-118">Upon selecting a resource, an RDP connection is created using the native app on the OS.</span></span>
- <span data-ttu-id="0a87b-119">一旦使用者啟動 RDP 連線後，RD 閘道就會派上用場。</span><span class="sxs-lookup"><span data-stu-id="0a87b-119">RD Gateway comes into the picture once a user launches the RDP connection.</span></span> <span data-ttu-id="0a87b-120">RD 閘道會處理來自網際網路的加密 RDP 流量，並將它轉譯為使用者所連線的內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a87b-120">The RD Gateway handles the encrypted RDP traffic coming over the Internet and translates it to the on-premises server that the user is connecting to.</span></span> <span data-ttu-id="0a87b-121">在此案例中，RD 閘道正在接收的流量是來自 Azure AD 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0a87b-121">In this scenario, the traffic the RD Gateway is receiving comes from the Azure AD Application Proxy.</span></span>

>[!TIP]
><span data-ttu-id="0a87b-122">如果您之前從未部署過 RDS，或在您開始前需要更多資訊，請了解如何[使用 Azure Resource Manager 和 Azure Marketplace 順暢地部署 RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)。</span><span class="sxs-lookup"><span data-stu-id="0a87b-122">If you haven't deployed RDS before, or want more information before you begin, learn how to [seamlessly deploy RDS with Azure Resource Manager and Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).</span></span>

## <a name="requirements"></a><span data-ttu-id="0a87b-123">需求</span><span class="sxs-lookup"><span data-stu-id="0a87b-123">Requirements</span></span>

- <span data-ttu-id="0a87b-124">RD Web 和 RD 閘道端點必須位於相同的電腦上，並具有一般的根。</span><span class="sxs-lookup"><span data-stu-id="0a87b-124">Both the RD Web and RD Gateway endpoints must be located on the same machine, and with a common root.</span></span> <span data-ttu-id="0a87b-125">將發佈 RD Web 和 RD 閘道作為單一應用程式，因此您可以在這兩個應用程式之間擁有單一登入的體驗。</span><span class="sxs-lookup"><span data-stu-id="0a87b-125">RD Web and RD Gateway will be published as a single application so you can have a single sign-on experience between the two applications.</span></span>

- <span data-ttu-id="0a87b-126">您應該已經[部署 RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) 並[啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="0a87b-126">You should already have [deployed RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), and [enabled Application Proxy](active-directory-application-proxy-enable.md).</span></span>

- <span data-ttu-id="0a87b-127">此案例假設您的終端使用者在透過 RD 網頁連線的 Windows 7 或 Windows 10 桌上型電腦上使用 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="0a87b-127">This scenario assumes that your end users go through Internet Explorer on Windows 7 or Windows 10 desktops that connect through the RD Web page.</span></span> <span data-ttu-id="0a87b-128">如果您需要支援其他作業系統，請參閱[其他用戶端設定的支援](#support-for-other-client-configurations)。</span><span class="sxs-lookup"><span data-stu-id="0a87b-128">If you need to support other operating systems, see [Support for other client configurations](#support-for-other-client-configurations).</span></span>

  >[!NOTE]
  ><span data-ttu-id="0a87b-129">目前不支援 Windows 10 Creator's Update。</span><span class="sxs-lookup"><span data-stu-id="0a87b-129">Windows 10 Creator's Update is not currently supported.</span></span>

- <span data-ttu-id="0a87b-130">在 Internet Explorer 上，啟用 RDS ActiveX 附加元件。</span><span class="sxs-lookup"><span data-stu-id="0a87b-130">On Internet Explorer, enable the RDS ActiveX add-on.</span></span>

## <a name="deploy-the-joint-rds-and-application-proxy-scenario"></a><span data-ttu-id="0a87b-131">部署聯合 RDS 和應用程式 Proxy 案例</span><span class="sxs-lookup"><span data-stu-id="0a87b-131">Deploy the joint RDS and Application Proxy scenario</span></span>

<span data-ttu-id="0a87b-132">為您的環境設定 RDS 與 Azure AD 應用程式 Proxy 之後，請遵循步驟將兩種解決方案結合。</span><span class="sxs-lookup"><span data-stu-id="0a87b-132">After setting up RDS and Azure AD Application Proxy for your environment, follow the steps to combine the two solutions.</span></span> <span data-ttu-id="0a87b-133">這些步驟會逐步解說發佈兩個 Web 對向 RDS 端點 (RD Web 和 RD 閘道) 作為應用程式，然後將您 RDS 上的流量導向以通過應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0a87b-133">These steps walk through publishing the two web-facing RDS endpoints (RD Web and RD Gateway) as applications, and then directing traffic on your RDS to go through Application Proxy.</span></span>

### <a name="publish-the-rd-host-endpoint"></a><span data-ttu-id="0a87b-134">發佈 RD 主機端點</span><span class="sxs-lookup"><span data-stu-id="0a87b-134">Publish the RD host endpoint</span></span>

1. <span data-ttu-id="0a87b-135">使用下列值[發佈新的應用程式 Proxy 應用程式](application-proxy-publish-azure-portal.md)︰</span><span class="sxs-lookup"><span data-stu-id="0a87b-135">[Publish a new Application Proxy application](application-proxy-publish-azure-portal.md) with the following values:</span></span>
   - <span data-ttu-id="0a87b-136">內部 URL：https://\<rdhost\>.com/，其中 \<rdhost\> 是 RD Web 和 RD 閘道共用的共同根。</span><span class="sxs-lookup"><span data-stu-id="0a87b-136">Internal URL: https://\<rdhost\>.com/, where \<rdhost\> is the common root that RD Web and RD Gateway share.</span></span>
   - <span data-ttu-id="0a87b-137">外部 URL︰會根據應用程式名稱自動填入這個欄位，但您可以修改它。</span><span class="sxs-lookup"><span data-stu-id="0a87b-137">External URL: This field is automatically populated based on the name of the application, but you can modify it.</span></span> <span data-ttu-id="0a87b-138">您的使用者在存取 RDS 時，將會移到此 URL。</span><span class="sxs-lookup"><span data-stu-id="0a87b-138">Your users will go to this URL when they access RDS.</span></span>
   - <span data-ttu-id="0a87b-139">預先驗證方法︰Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a87b-139">Preauthentication method: Azure Active Directory</span></span>
   - <span data-ttu-id="0a87b-140">轉譯 URL 標頭：否</span><span class="sxs-lookup"><span data-stu-id="0a87b-140">Translate URL headers: No</span></span>
2. <span data-ttu-id="0a87b-141">將使用者指派給已發佈 RD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a87b-141">Assign users to the published RD application.</span></span> <span data-ttu-id="0a87b-142">並請確定它們都可存取 RDS。</span><span class="sxs-lookup"><span data-stu-id="0a87b-142">Make sure they all have access to RDS, too.</span></span>
3. <span data-ttu-id="0a87b-143">保留應用程式的單一登入方法，因為 **Azure AD 單一登入已停用**。</span><span class="sxs-lookup"><span data-stu-id="0a87b-143">Leave the single sign-on method for the application as **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="0a87b-144">系統會要求您的使用者分別驗證一次 Azure AD 及 RD Web，但可單一登入 RD 閘道。</span><span class="sxs-lookup"><span data-stu-id="0a87b-144">Your users are asked to authenticate once to Azure AD and once to RD Web, but have single sign-on to RD Gateway.</span></span>
4. <span data-ttu-id="0a87b-145">移至 [Azure Active Directory] > [應用程式註冊] > [您的應用程式] > [設定]。</span><span class="sxs-lookup"><span data-stu-id="0a87b-145">Go to **Azure Active Directory** > **App Registrations** > *Your application* > **Settings**.</span></span>
5. <span data-ttu-id="0a87b-146">選取 [內容] 並更新 [首頁 URL] 欄位，以指向 RD Web 端點 (例如 https://\<rdhost\>.com/RDWeb)。</span><span class="sxs-lookup"><span data-stu-id="0a87b-146">Select **Properties** and update the **Home-page URL** field to point to your RD Web endpoint (like https://\<rdhost\>.com/RDWeb).</span></span>

### <a name="direct-rds-traffic-to-application-proxy"></a><span data-ttu-id="0a87b-147">將 RDS 資料流導向應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="0a87b-147">Direct RDS traffic to Application Proxy</span></span>

<span data-ttu-id="0a87b-148">以系統管理員身分連線至 RDS 部署，並變更部署的 RD 閘道伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="0a87b-148">Connect to the RDS deployment as an administrator and change the RD Gateway server name for the deployment.</span></span> <span data-ttu-id="0a87b-149">這可確保連線經過 Azure AD 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0a87b-149">This ensures that connections go through the Azure AD Application Proxy.</span></span>

1. <span data-ttu-id="0a87b-150">連線到執行 RD 連線代理人角色的 RDS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a87b-150">Connect to the RDS server running the RD Connection Broker role.</span></span>
2. <span data-ttu-id="0a87b-151">啟動**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="0a87b-151">Launch **Server Manager**.</span></span>
3. <span data-ttu-id="0a87b-152">選取左窗格中的 [遠端桌面服務]。</span><span class="sxs-lookup"><span data-stu-id="0a87b-152">Select **Remote Desktop Services** from the pane on the left.</span></span>
4. <span data-ttu-id="0a87b-153">選取 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="0a87b-153">Select **Overview**.</span></span>
5. <span data-ttu-id="0a87b-154">在 [部署概觀] 區段中，選取下拉式選單，然後選擇 [編輯部署內容]。</span><span class="sxs-lookup"><span data-stu-id="0a87b-154">In the Deployment Overview section, select the drop-down menu and choose **Edit deployment properties**.</span></span>
6. <span data-ttu-id="0a87b-155">在 [RD 閘道] 索引標籤中，將 [伺服器名稱] 變更為您在應用程式 Proxy 中所設定之 RD 主機端點的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="0a87b-155">In the RD Gateway tab, change the **Server name** field to the External URL that you set for the RD host endpoint in Application Proxy.</span></span>
7. <span data-ttu-id="0a87b-156">將 [登入方法] 欄位變更為 [密碼驗證]。</span><span class="sxs-lookup"><span data-stu-id="0a87b-156">Change the **Logon method** field to **Password Authentication**.</span></span>

  ![在 RDS 上部署內容畫面](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. <span data-ttu-id="0a87b-158">針對每個集合，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="0a87b-158">For each collection, run the following command.</span></span> <span data-ttu-id="0a87b-159">使用您自己的資訊來取代 *\<yourcollectionname\>* 和 *\<proxyfrontendurl\>*。</span><span class="sxs-lookup"><span data-stu-id="0a87b-159">Replace *\<yourcollectionname\>* and *\<proxyfrontendurl\>* with your own information.</span></span> <span data-ttu-id="0a87b-160">此命令會啟用 RD Web 和 RD 閘道之間的單一登入，並將效能最佳化︰</span><span class="sxs-lookup"><span data-stu-id="0a87b-160">This command enables single sign-on between RD Web and RD Gateway, and optimizes performance:</span></span>

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   <span data-ttu-id="0a87b-161">**例如：**</span><span class="sxs-lookup"><span data-stu-id="0a87b-161">**For example:**</span></span>
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. <span data-ttu-id="0a87b-162">若要確認自訂 RDP 屬性的修改，以及檢視將會針對此集合從 RDWeb 下載的 RDP 檔案內容，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="0a87b-162">To verify the modification of the custom RDP properties as well as view the RDP file contents that will be downloaded from RDWeb for this collection, run the following command:</span></span>
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

<span data-ttu-id="0a87b-163">現在您已設定遠端桌面，Azure AD 應用程式 Proxy 已接管作為 RDS 的網際網路對應元件。</span><span class="sxs-lookup"><span data-stu-id="0a87b-163">Now that you've configured Remote Desktop, Azure AD Application Proxy has taken over as the internet-facing component of RDS.</span></span> <span data-ttu-id="0a87b-164">您可以將 RD Web 和 RD 閘道機器上的其他公用網際網路對應端點移除。</span><span class="sxs-lookup"><span data-stu-id="0a87b-164">You can remove the other public internet-facing endpoints on your RD Web and RD Gateway machines.</span></span>

## <a name="test-the-scenario"></a><span data-ttu-id="0a87b-165">測試案例</span><span class="sxs-lookup"><span data-stu-id="0a87b-165">Test the scenario</span></span>

<span data-ttu-id="0a87b-166">在 Windows 7 或 10 電腦上使用 Internet Explorer 來測試案例。</span><span class="sxs-lookup"><span data-stu-id="0a87b-166">Test the scenario with Internet Explorer on a Windows 7 or 10 computer.</span></span>

1. <span data-ttu-id="0a87b-167">移至您所設定的外部 URL，或在 [MyApps 面板](https://myapps.microsoft.com)中尋找您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a87b-167">Go to the external URL you set up, or find your application in the [MyApps panel](https://myapps.microsoft.com).</span></span>
2. <span data-ttu-id="0a87b-168">系統會要求您向 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0a87b-168">You are asked to authenticate to Azure Active Directory.</span></span> <span data-ttu-id="0a87b-169">使用您指派給應用程式的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a87b-169">Use an account that you assigned to the application.</span></span>
3. <span data-ttu-id="0a87b-170">系統會要求您向 RD Web 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0a87b-170">You are asked to authenticate to RD Web.</span></span>
4. <span data-ttu-id="0a87b-171">一旦 RDS 驗證成功後，您可以選取所需的桌上型電腦或應用程式，然後開始使用。</span><span class="sxs-lookup"><span data-stu-id="0a87b-171">Once your RDS authentication succeeds, you can select the desktop or application you want, and start working.</span></span>

## <a name="support-for-other-client-configurations"></a><span data-ttu-id="0a87b-172">其他用戶端設定的支援</span><span class="sxs-lookup"><span data-stu-id="0a87b-172">Support for other client configurations</span></span>

<span data-ttu-id="0a87b-173">本文中所述的設定是針對具有 Internet Explorer 和 RDS ActiveX 附加元件之 Windows 7 或 10 上的使用者。</span><span class="sxs-lookup"><span data-stu-id="0a87b-173">The configuration outlined in this article is for users on Windows 7 or 10, with Internet Explorer plus the RDS ActiveX add-on.</span></span> <span data-ttu-id="0a87b-174">不過，如果需要，您可以支援其他作業系統或瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="0a87b-174">If you need to, however, you can support other operating systems or browsers.</span></span> <span data-ttu-id="0a87b-175">差異在於您所使用的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="0a87b-175">The difference is in the authentication method that you use.</span></span>

| <span data-ttu-id="0a87b-176">驗證方法</span><span class="sxs-lookup"><span data-stu-id="0a87b-176">Authentication method</span></span> | <span data-ttu-id="0a87b-177">支援的用戶端設定</span><span class="sxs-lookup"><span data-stu-id="0a87b-177">Supported client configuration</span></span> |
| --------------------- | ------------------------------ |
| <span data-ttu-id="0a87b-178">預先驗證</span><span class="sxs-lookup"><span data-stu-id="0a87b-178">Pre-authentication</span></span>    | <span data-ttu-id="0a87b-179">使用 Internet Explorer + RDS ActiveX 附加元件的 Windows 7/10</span><span class="sxs-lookup"><span data-stu-id="0a87b-179">Windows 7/10 using Internet Explorer + RDS ActiveX add-on</span></span> |
| <span data-ttu-id="0a87b-180">通道</span><span class="sxs-lookup"><span data-stu-id="0a87b-180">Passthrough</span></span> | <span data-ttu-id="0a87b-181">支援 Microsoft 遠端桌面應用程式的任何其他作業系統</span><span class="sxs-lookup"><span data-stu-id="0a87b-181">Any other operating system that supports the Microsoft Remote Desktop application</span></span> |

<span data-ttu-id="0a87b-182">預先驗證流程的安全性優點多於通道流程。</span><span class="sxs-lookup"><span data-stu-id="0a87b-182">The pre-authentication flow offers more security benefits than the passthrough flow.</span></span> <span data-ttu-id="0a87b-183">使用預先驗證，您可以利用內部部署資源的 Azure AD 驗證功能，例如單一登入、條件式存取和雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="0a87b-183">With pre-authentication you can leverage Azure AD authentication features like single sign-on, conditional access, and two-step verification for your on-premises resources.</span></span> <span data-ttu-id="0a87b-184">您也可以確定只有驗證過的流量到達您的網路。</span><span class="sxs-lookup"><span data-stu-id="0a87b-184">You also ensure that only authenticated traffic reaches your network.</span></span>

<span data-ttu-id="0a87b-185">若要使用通道驗證，只需要對本文中所列的步驟進行兩項修改：</span><span class="sxs-lookup"><span data-stu-id="0a87b-185">To use passthrough authentication, there are just two modifications to the steps listed in this article:</span></span>
1. <span data-ttu-id="0a87b-186">在 [Publish the RD host endpoint] (發佈 RD 主機端點)[](#publish-the-rd-host-endpoint) 步驟 1 中，請將預先驗證方法設為 [通道]。</span><span class="sxs-lookup"><span data-stu-id="0a87b-186">In [Publish the RD host endpoint](#publish-the-rd-host-endpoint) step 1, set the Preauthentication method to **Passthrough**.</span></span>
2. <span data-ttu-id="0a87b-187">在 [Direct RDS traffic to Application Proxy] (將 RDS 流量導向應用程式 Proxy)[](#direct-rds-traffic-to-application-proxy) 中，完全略過步驟 8。</span><span class="sxs-lookup"><span data-stu-id="0a87b-187">In [Direct RDS traffic to Application Proxy](#direct-rds-traffic-to-application-proxy), skip step 8 entirely.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a87b-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a87b-188">Next steps</span></span>

[<span data-ttu-id="0a87b-189">使用 Azure AD 應用程式 Proxy 啟用 SharePoint 的遠端存取</span><span class="sxs-lookup"><span data-stu-id="0a87b-189">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)  
[<span data-ttu-id="0a87b-190">使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量</span><span class="sxs-lookup"><span data-stu-id="0a87b-190">Security considerations for accessing apps remotely by using Azure AD Application Proxy</span></span>](application-proxy-security-considerations.md)
