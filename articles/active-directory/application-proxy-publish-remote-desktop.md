---
title: "使用 Azure AD 應用程式 Proxy 的遠端桌面 aaaPublish |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念。"
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
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a><span data-ttu-id="a86a8-103">使用 Azure AD 應用程式 Proxy 發佈遠端桌面</span><span class="sxs-lookup"><span data-stu-id="a86a8-103">Publish Remote Desktop with Azure AD Application Proxy</span></span>

<span data-ttu-id="a86a8-104">本文件涵蓋如何 toodeploy 應用程式 proxy 的遠端桌面服務 (RDS)，讓遠端使用者仍能提高生產力。</span><span class="sxs-lookup"><span data-stu-id="a86a8-104">This article covers how toodeploy Remote Desktop Services (RDS) with Application Proxy so that remote users can still be productive.</span></span>

<span data-ttu-id="a86a8-105">hello 想要針對這個發行項的對象：</span><span class="sxs-lookup"><span data-stu-id="a86a8-105">hello intended audience for this article is:</span></span>
- <span data-ttu-id="a86a8-106">目前 Azure AD Application Proxy 客戶希望 toooffer 多個應用程式 tootheir 使用者藉由發行內部應用程式，透過遠端桌面服務。</span><span class="sxs-lookup"><span data-stu-id="a86a8-106">Current Azure AD Application Proxy customers who want toooffer more applications tootheir end users by publishing on-premises applications through Remote Desktop Services.</span></span>
- <span data-ttu-id="a86a8-107">目前遠端桌面服務的客戶想使用 Azure AD Application Proxy 部署 tooreduce hello 受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="a86a8-107">Current Remote Desktop Services customers who want tooreduce hello attack surface of their deployment by using Azure AD Application Proxy.</span></span> <span data-ttu-id="a86a8-108">此案例提供一組有限的雙步驟驗證和條件式存取控制 tooRDS。</span><span class="sxs-lookup"><span data-stu-id="a86a8-108">This scenario gives a limited set of two-step verification and conditional access controls tooRDS.</span></span>

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a><span data-ttu-id="a86a8-109">應用程式 Proxy 如何納入 hello 標準 RDS 部署</span><span class="sxs-lookup"><span data-stu-id="a86a8-109">How Application Proxy fits in hello standard RDS deployment</span></span>

<span data-ttu-id="a86a8-110">標準 RDS 部署包含 Windows Server 上執行的各種遠端桌面角色服務。</span><span class="sxs-lookup"><span data-stu-id="a86a8-110">A standard RDS deployment includes various Remote Desktop role services running on Windows Server.</span></span> <span data-ttu-id="a86a8-111">查看 hello[遠端桌面服務架構](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture)，有多個部署選項。</span><span class="sxs-lookup"><span data-stu-id="a86a8-111">Looking at hello [Remote Desktop Services architecture](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), there are multiple deployment options.</span></span> <span data-ttu-id="a86a8-112">hello 最明顯差異 hello [RDS 部署與 Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) （hello 下列圖表所示） 和 hello 其他部署選項是該 hello 應用程式 Proxy 案例已永久的輸出從執行 hello 連接器服務的 hello 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="a86a8-112">hello most noticeable difference between hello [RDS deployment with Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (shown in hello following diagram) and hello other deployment options is that hello Application Proxy scenario has a permanent outbound connection from hello server running hello connector service.</span></span> <span data-ttu-id="a86a8-113">其他部署會透過負載平衡器保留開啟的輸入連線。</span><span class="sxs-lookup"><span data-stu-id="a86a8-113">Other deployments leave open inbound connections through a load balancer.</span></span>

![Hello RDS VM 和 hello 公用網際網路之間的應用程式 Proxy 位於](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

<span data-ttu-id="a86a8-115">在 RDS 部署中，hello RD Web 角色和 hello RD 閘道角色網際網路對向在機器上執行。</span><span class="sxs-lookup"><span data-stu-id="a86a8-115">In an RDS deployment, hello RD Web role and hello RD Gateway role run on Internet-facing machines.</span></span> <span data-ttu-id="a86a8-116">這些端點會公開下列原因 hello:</span><span class="sxs-lookup"><span data-stu-id="a86a8-116">These endpoints are exposed for hello following reasons:</span></span>
- <span data-ttu-id="a86a8-117">RD Web 提供 hello 使用者的公用端點 toosign 中，並檢視 hello 各種內部部署應用程式和桌面他們可以存取。</span><span class="sxs-lookup"><span data-stu-id="a86a8-117">RD Web provides hello user a public endpoint toosign in and view hello various on-premises applications and desktops they can access.</span></span> <span data-ttu-id="a86a8-118">在選取的資源，RDP 連線會使用 hello OS 上的 hello 原生應用程式所建立的。</span><span class="sxs-lookup"><span data-stu-id="a86a8-118">Upon selecting a resource, an RDP connection is created using hello native app on hello OS.</span></span>
- <span data-ttu-id="a86a8-119">RD 閘道進入 hello 圖片，一旦使用者啟動 hello RDP 連接。</span><span class="sxs-lookup"><span data-stu-id="a86a8-119">RD Gateway comes into hello picture once a user launches hello RDP connection.</span></span> <span data-ttu-id="a86a8-120">hello RD 閘道處理 hello 網際網路透過傳入的 hello 加密 RDP 流量，並將它轉譯的 toohello hello 使用者的內部部署伺服器連線到。</span><span class="sxs-lookup"><span data-stu-id="a86a8-120">hello RD Gateway handles hello encrypted RDP traffic coming over hello Internet and translates it toohello on-premises server that hello user is connecting to.</span></span> <span data-ttu-id="a86a8-121">在此案例中，RD 閘道收到 hello 流量 hello 來自 hello Azure AD Application Proxy。</span><span class="sxs-lookup"><span data-stu-id="a86a8-121">In this scenario, hello traffic hello RD Gateway is receiving comes from hello Azure AD Application Proxy.</span></span>

>[!TIP]
><span data-ttu-id="a86a8-122">如果您尚未部署之前，RDS，或想要的詳細資訊，在您開始前，了解如何太[順暢地部署與 Azure 資源管理員和 Azure Marketplace 的 RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)。</span><span class="sxs-lookup"><span data-stu-id="a86a8-122">If you haven't deployed RDS before, or want more information before you begin, learn how too[seamlessly deploy RDS with Azure Resource Manager and Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).</span></span>

## <a name="requirements"></a><span data-ttu-id="a86a8-123">需求</span><span class="sxs-lookup"><span data-stu-id="a86a8-123">Requirements</span></span>

- <span data-ttu-id="a86a8-124">同時 hello RD Web 和 RD 閘道必須位於端點 hello 相同電腦，以及常見的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a86a8-124">Both hello RD Web and RD Gateway endpoints must be located on hello same machine, and with a common root.</span></span> <span data-ttu-id="a86a8-125">RD Web 和 RD 閘道將做為單一的應用程式發行，因此您可以擁有單一登入體驗 hello 兩個應用程式之間。</span><span class="sxs-lookup"><span data-stu-id="a86a8-125">RD Web and RD Gateway will be published as a single application so you can have a single sign-on experience between hello two applications.</span></span>

- <span data-ttu-id="a86a8-126">您應該已經[部署 RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) 並[啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="a86a8-126">You should already have [deployed RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), and [enabled Application Proxy](active-directory-application-proxy-enable.md).</span></span>

- <span data-ttu-id="a86a8-127">此案例假設您的使用者移到 Internet Explorer 在 hello RD 網頁進行連接的 Windows 7 或 Windows 10 桌上型電腦上。</span><span class="sxs-lookup"><span data-stu-id="a86a8-127">This scenario assumes that your end users go through Internet Explorer on Windows 7 or Windows 10 desktops that connect through hello RD Web page.</span></span> <span data-ttu-id="a86a8-128">如果您需要 toosupport 其他作業系統，請參閱[其他用戶端設定的支援](#support-for-other-client-configurations)。</span><span class="sxs-lookup"><span data-stu-id="a86a8-128">If you need toosupport other operating systems, see [Support for other client configurations](#support-for-other-client-configurations).</span></span>

  >[!NOTE]
  ><span data-ttu-id="a86a8-129">目前不支援 Windows 10 Creator's Update。</span><span class="sxs-lookup"><span data-stu-id="a86a8-129">Windows 10 Creator's Update is not currently supported.</span></span>

- <span data-ttu-id="a86a8-130">在 Internet Explorer 中，啟用 hello RDS ActiveX 附加元件。</span><span class="sxs-lookup"><span data-stu-id="a86a8-130">On Internet Explorer, enable hello RDS ActiveX add-on.</span></span>

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a><span data-ttu-id="a86a8-131">部署 hello 聯合 RDS 和應用程式 Proxy 案例</span><span class="sxs-lookup"><span data-stu-id="a86a8-131">Deploy hello joint RDS and Application Proxy scenario</span></span>

<span data-ttu-id="a86a8-132">設定好 RDS 和 Azure AD Application Proxy 為您的環境之後，請遵循 hello 步驟 toocombine hello 這兩個方案。</span><span class="sxs-lookup"><span data-stu-id="a86a8-132">After setting up RDS and Azure AD Application Proxy for your environment, follow hello steps toocombine hello two solutions.</span></span> <span data-ttu-id="a86a8-133">這些步驟逐步解說發行 hello 兩個 web 面對 RDS 端點 （RD Web 和 RD 閘道） 做為應用程式，並再將流量導向您透過應用程式 Proxy 的 RDS toogo 上。</span><span class="sxs-lookup"><span data-stu-id="a86a8-133">These steps walk through publishing hello two web-facing RDS endpoints (RD Web and RD Gateway) as applications, and then directing traffic on your RDS toogo through Application Proxy.</span></span>

### <a name="publish-hello-rd-host-endpoint"></a><span data-ttu-id="a86a8-134">發行 hello RD 主應用程式端點</span><span class="sxs-lookup"><span data-stu-id="a86a8-134">Publish hello RD host endpoint</span></span>

1. <span data-ttu-id="a86a8-135">[將新的應用程式 Proxy 應用程式發行](application-proxy-publish-azure-portal.md)以 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="a86a8-135">[Publish a new Application Proxy application](application-proxy-publish-azure-portal.md) with hello following values:</span></span>
   - <span data-ttu-id="a86a8-136">內部 URL: https://\<rdhost\>.com /，其中\<rdhost\>是 hello 常見的根目錄 RD Web 和 RD 閘道的共用。</span><span class="sxs-lookup"><span data-stu-id="a86a8-136">Internal URL: https://\<rdhost\>.com/, where \<rdhost\> is hello common root that RD Web and RD Gateway share.</span></span>
   - <span data-ttu-id="a86a8-137">外部 URL： 這個欄位會自動擴展根據 hello hello 應用程式名稱，但您可以修改它。</span><span class="sxs-lookup"><span data-stu-id="a86a8-137">External URL: This field is automatically populated based on hello name of hello application, but you can modify it.</span></span> <span data-ttu-id="a86a8-138">您的使用者將會移 toothis URL 存取.rds 時</span><span class="sxs-lookup"><span data-stu-id="a86a8-138">Your users will go toothis URL when they access RDS.</span></span>
   - <span data-ttu-id="a86a8-139">預先驗證方法︰Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a86a8-139">Preauthentication method: Azure Active Directory</span></span>
   - <span data-ttu-id="a86a8-140">轉譯 URL 標頭：否</span><span class="sxs-lookup"><span data-stu-id="a86a8-140">Translate URL headers: No</span></span>
2. <span data-ttu-id="a86a8-141">將使用者指派 toohello RD 應用程式發行。</span><span class="sxs-lookup"><span data-stu-id="a86a8-141">Assign users toohello published RD application.</span></span> <span data-ttu-id="a86a8-142">請確定它們都有存取 tooRDS 太。</span><span class="sxs-lookup"><span data-stu-id="a86a8-142">Make sure they all have access tooRDS, too.</span></span>
3. <span data-ttu-id="a86a8-143">保留 hello 單一登入方法 hello 應用程式做為**Azure AD 單一登入已停用**。</span><span class="sxs-lookup"><span data-stu-id="a86a8-143">Leave hello single sign-on method for hello application as **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="a86a8-144">您的使用者要求 tooauthenticate 一旦 tooAzure AD，另一次 tooRD Web，但沒有單一登入 tooRD 閘道。</span><span class="sxs-lookup"><span data-stu-id="a86a8-144">Your users are asked tooauthenticate once tooAzure AD and once tooRD Web, but have single sign-on tooRD Gateway.</span></span>
4. <span data-ttu-id="a86a8-145">跳過**Azure Active Directory** > **應用程式註冊** > *您的應用程式* > **設定**.</span><span class="sxs-lookup"><span data-stu-id="a86a8-145">Go too**Azure Active Directory** > **App Registrations** > *Your application* > **Settings**.</span></span>
5. <span data-ttu-id="a86a8-146">選取**屬性**和更新 hello**首頁的 URL**欄位 toopoint tooyour RD Web 端點 (例如 https://\<rdhost\>.com/RDWeb)。</span><span class="sxs-lookup"><span data-stu-id="a86a8-146">Select **Properties** and update hello **Home-page URL** field toopoint tooyour RD Web endpoint (like https://\<rdhost\>.com/RDWeb).</span></span>

### <a name="direct-rds-traffic-tooapplication-proxy"></a><span data-ttu-id="a86a8-147">直接 RDS 流量 tooApplication Proxy</span><span class="sxs-lookup"><span data-stu-id="a86a8-147">Direct RDS traffic tooApplication Proxy</span></span>

<span data-ttu-id="a86a8-148">Toohello RDS 部署，以系統管理員身分連接，並變更 hello 部署的 hello RD 閘道伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="a86a8-148">Connect toohello RDS deployment as an administrator and change hello RD Gateway server name for hello deployment.</span></span> <span data-ttu-id="a86a8-149">這可確保連接經過 hello Azure AD Application Proxy。</span><span class="sxs-lookup"><span data-stu-id="a86a8-149">This ensures that connections go through hello Azure AD Application Proxy.</span></span>

1. <span data-ttu-id="a86a8-150">連接執行 hello RD 連線代理人角色 toohello RDS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86a8-150">Connect toohello RDS server running hello RD Connection Broker role.</span></span>
2. <span data-ttu-id="a86a8-151">啟動**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="a86a8-151">Launch **Server Manager**.</span></span>
3. <span data-ttu-id="a86a8-152">選取**遠端桌面服務**hello hello 左側窗格中。</span><span class="sxs-lookup"><span data-stu-id="a86a8-152">Select **Remote Desktop Services** from hello pane on hello left.</span></span>
4. <span data-ttu-id="a86a8-153">選取 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="a86a8-153">Select **Overview**.</span></span>
5. <span data-ttu-id="a86a8-154">在 hello 部署概觀 區段中，選取 hello 下拉功能表並選擇**編輯部署屬性**。</span><span class="sxs-lookup"><span data-stu-id="a86a8-154">In hello Deployment Overview section, select hello drop-down menu and choose **Edit deployment properties**.</span></span>
6. <span data-ttu-id="a86a8-155">在 hello RD 閘道索引標籤上，變更 hello**伺服器名稱**欄位 toohello 您為應用程式 Proxy 中的 hello RD 主機端點的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="a86a8-155">In hello RD Gateway tab, change hello **Server name** field toohello External URL that you set for hello RD host endpoint in Application Proxy.</span></span>
7. <span data-ttu-id="a86a8-156">變更 hello**登入方法**欄位太**密碼驗證**。</span><span class="sxs-lookup"><span data-stu-id="a86a8-156">Change hello **Logon method** field too**Password Authentication**.</span></span>

  ![在 RDS 上部署內容畫面](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. <span data-ttu-id="a86a8-158">針對每個集合中，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="a86a8-158">For each collection, run hello following command.</span></span> <span data-ttu-id="a86a8-159">使用您自己的資訊來取代 *\<yourcollectionname\>* 和 *\<proxyfrontendurl\>*。</span><span class="sxs-lookup"><span data-stu-id="a86a8-159">Replace *\<yourcollectionname\>* and *\<proxyfrontendurl\>* with your own information.</span></span> <span data-ttu-id="a86a8-160">此命令會啟用 RD Web 和 RD 閘道之間的單一登入，並將效能最佳化︰</span><span class="sxs-lookup"><span data-stu-id="a86a8-160">This command enables single sign-on between RD Web and RD Gateway, and optimizes performance:</span></span>

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   <span data-ttu-id="a86a8-161">**例如：**</span><span class="sxs-lookup"><span data-stu-id="a86a8-161">**For example:**</span></span>
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. <span data-ttu-id="a86a8-162">tooverify hello 自訂 RDP 屬性，以及檢視 hello RDP 檔案內容，將會針對此集合中，執行下列命令的 hello RDWeb 從下載的 hello 修改：</span><span class="sxs-lookup"><span data-stu-id="a86a8-162">tooverify hello modification of hello custom RDP properties as well as view hello RDP file contents that will be downloaded from RDWeb for this collection, run hello following command:</span></span>
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

<span data-ttu-id="a86a8-163">既然您已經設定遠端桌面，Azure AD 應用程式 Proxy 已花費為.rds hello 網際網路對向元件</span><span class="sxs-lookup"><span data-stu-id="a86a8-163">Now that you've configured Remote Desktop, Azure AD Application Proxy has taken over as hello internet-facing component of RDS.</span></span> <span data-ttu-id="a86a8-164">您可以移除 hello RD Web 和 RD 閘道的機器上的其他公用網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="a86a8-164">You can remove hello other public internet-facing endpoints on your RD Web and RD Gateway machines.</span></span>

## <a name="test-hello-scenario"></a><span data-ttu-id="a86a8-165">測試 hello 情節</span><span class="sxs-lookup"><span data-stu-id="a86a8-165">Test hello scenario</span></span>

<span data-ttu-id="a86a8-166">測試與 Windows 7 或 10 的電腦上的 Internet Explorer 的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="a86a8-166">Test hello scenario with Internet Explorer on a Windows 7 or 10 computer.</span></span>

1. <span data-ttu-id="a86a8-167">移 toohello 外部 URL 設定，或您的應用程式在 hello [MyApps 面板](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="a86a8-167">Go toohello external URL you set up, or find your application in hello [MyApps panel](https://myapps.microsoft.com).</span></span>
2. <span data-ttu-id="a86a8-168">系統會詢問 tooauthenticate tooAzure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="a86a8-168">You are asked tooauthenticate tooAzure Active Directory.</span></span> <span data-ttu-id="a86a8-169">使用您指派 toohello 應用程式的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a86a8-169">Use an account that you assigned toohello application.</span></span>
3. <span data-ttu-id="a86a8-170">系統會詢問 tooauthenticate tooRD Web。</span><span class="sxs-lookup"><span data-stu-id="a86a8-170">You are asked tooauthenticate tooRD Web.</span></span>
4. <span data-ttu-id="a86a8-171">RDS 驗證成功後，您可以選取 hello 桌面或應用程式，並開始使用。</span><span class="sxs-lookup"><span data-stu-id="a86a8-171">Once your RDS authentication succeeds, you can select hello desktop or application you want, and start working.</span></span>

## <a name="support-for-other-client-configurations"></a><span data-ttu-id="a86a8-172">其他用戶端設定的支援</span><span class="sxs-lookup"><span data-stu-id="a86a8-172">Support for other client configurations</span></span>

<span data-ttu-id="a86a8-173">這篇文章所述的 hello 設定是在 Windows 7 或 10、 Internet Explorer 再加上 hello RDS ActiveX 附加元件與使用者。</span><span class="sxs-lookup"><span data-stu-id="a86a8-173">hello configuration outlined in this article is for users on Windows 7 or 10, with Internet Explorer plus hello RDS ActiveX add-on.</span></span> <span data-ttu-id="a86a8-174">不過，如果需要，您可以支援其他作業系統或瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a86a8-174">If you need to, however, you can support other operating systems or browsers.</span></span> <span data-ttu-id="a86a8-175">hello 差異是在您使用的 hello 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="a86a8-175">hello difference is in hello authentication method that you use.</span></span>

| <span data-ttu-id="a86a8-176">驗證方法</span><span class="sxs-lookup"><span data-stu-id="a86a8-176">Authentication method</span></span> | <span data-ttu-id="a86a8-177">支援的用戶端設定</span><span class="sxs-lookup"><span data-stu-id="a86a8-177">Supported client configuration</span></span> |
| --------------------- | ------------------------------ |
| <span data-ttu-id="a86a8-178">預先驗證</span><span class="sxs-lookup"><span data-stu-id="a86a8-178">Pre-authentication</span></span>    | <span data-ttu-id="a86a8-179">使用 Internet Explorer + RDS ActiveX 附加元件的 Windows 7/10</span><span class="sxs-lookup"><span data-stu-id="a86a8-179">Windows 7/10 using Internet Explorer + RDS ActiveX add-on</span></span> |
| <span data-ttu-id="a86a8-180">通道</span><span class="sxs-lookup"><span data-stu-id="a86a8-180">Passthrough</span></span> | <span data-ttu-id="a86a8-181">任何其他作業系統支援 hello Microsoft 遠端桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="a86a8-181">Any other operating system that supports hello Microsoft Remote Desktop application</span></span> |

<span data-ttu-id="a86a8-182">hello 預先驗證流程好處也較多的安全性比 hello 通過資料流程。</span><span class="sxs-lookup"><span data-stu-id="a86a8-182">hello pre-authentication flow offers more security benefits than hello passthrough flow.</span></span> <span data-ttu-id="a86a8-183">使用預先驗證，您可以利用內部部署資源的 Azure AD 驗證功能，例如單一登入、條件式存取和雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="a86a8-183">With pre-authentication you can leverage Azure AD authentication features like single sign-on, conditional access, and two-step verification for your on-premises resources.</span></span> <span data-ttu-id="a86a8-184">您也可以確定只有驗證過的流量到達您的網路。</span><span class="sxs-lookup"><span data-stu-id="a86a8-184">You also ensure that only authenticated traffic reaches your network.</span></span>

<span data-ttu-id="a86a8-185">toouse 通過驗證，那里兩個修改 toohello 步驟所述這篇文章：</span><span class="sxs-lookup"><span data-stu-id="a86a8-185">toouse passthrough authentication, there are just two modifications toohello steps listed in this article:</span></span>
1. <span data-ttu-id="a86a8-186">在[發行 hello RD 主機端點](#publish-the-rd-host-endpoint)步驟 1，以設定 hello 預先驗證方法太**通過**。</span><span class="sxs-lookup"><span data-stu-id="a86a8-186">In [Publish hello RD host endpoint](#publish-the-rd-host-endpoint) step 1, set hello Preauthentication method too**Passthrough**.</span></span>
2. <span data-ttu-id="a86a8-187">在[直接 RDS 流量 tooApplication Proxy](#direct-rds-traffic-to-application-proxy)，完全略過步驟 8。</span><span class="sxs-lookup"><span data-stu-id="a86a8-187">In [Direct RDS traffic tooApplication Proxy](#direct-rds-traffic-to-application-proxy), skip step 8 entirely.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86a8-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a86a8-188">Next steps</span></span>

[<span data-ttu-id="a86a8-189">啟用與 Azure AD Application Proxy 的遠端存取 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="a86a8-189">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)  
[<span data-ttu-id="a86a8-190">使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量</span><span class="sxs-lookup"><span data-stu-id="a86a8-190">Security considerations for accessing apps remotely by using Azure AD Application Proxy</span></span>](application-proxy-security-considerations.md)
