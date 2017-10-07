---
title: "aaaAzure AD 應用程式 Proxy-快速入門安裝連接器 |Microsoft 文件"
description: "Hello Azure 入口網站中開啟應用程式 Proxy，並安裝 hello hello 反向 proxy 連接器。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a><span data-ttu-id="8b140-103">開始使用應用程式 Proxy 並安裝 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="8b140-103">Get started with Application Proxy and install hello connector</span></span>
<span data-ttu-id="8b140-104">本文將告訴您透過 hello 步驟 tooenable Microsoft Azure AD 應用程式 Proxy 為您的雲端目錄，在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8b140-104">This article walks you through hello steps tooenable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="8b140-105">如果您不知道 hello 安全性和產能優勢的應用程式 Proxy 將 tooyour 組織，請深入了解[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8b140-105">If you're not yet aware of hello security and productivity benefits Application Proxy brings tooyour organization, learn more about [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="8b140-106">應用程式 Proxy 先決條件</span><span class="sxs-lookup"><span data-stu-id="8b140-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="8b140-107">您可以啟用及使用應用程式 Proxy 服務之前，您會需要 toohave:</span><span class="sxs-lookup"><span data-stu-id="8b140-107">Before you can enable and use Application Proxy services, you need toohave:</span></span>

* <span data-ttu-id="8b140-108">Microsoft Azure AD [基本或進階訂用帳戶](active-directory-editions.md) 以及您是全域管理員的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="8b140-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="8b140-109">執行 Windows Server 2012 R2 或 2016，您可以安裝 hello 應用程式 Proxy 連接器的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8b140-109">A server running Windows Server 2012 R2 or 2016, on which you can install hello Application Proxy Connector.</span></span> <span data-ttu-id="8b140-110">hello 伺服器需要 toobe 無法 tooconnect toohello hello 雲端中的應用程式 Proxy 服務而 hello 內部部署您發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b140-110">hello server needs toobe able tooconnect toohello Application Proxy services in hello cloud, and hello on-premises applications that you are publishing.</span></span>
  * <span data-ttu-id="8b140-111">針對單一登入 tooyour 已發行的應用程式使用 Kerberos 限制委派，這部電腦應該被網域的 hello 相同的 AD 網域中做為您要發行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b140-111">For single sign-on tooyour published applications using Kerberos Constrained Delegation, this machine should be domain-joined in hello same AD domain as hello applications that you are publishing.</span></span> <span data-ttu-id="8b140-112">如需詳細資訊，請參閱[使用應用程式 Proxy 進行單一登入的 KCD](active-directory-application-proxy-sso-using-kcd.md)。</span><span class="sxs-lookup"><span data-stu-id="8b140-112">For information, see [KCD for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

<span data-ttu-id="8b140-113">如果您的組織使用 proxy 伺服器 tooconnect toohello 網際網路，讀取[使用現有的內部 proxy 伺服器](application-proxy-working-with-proxy-servers.md)如需詳細資訊如何 tooconfigure 它們才能取得啟動應用程式 proxy。</span><span class="sxs-lookup"><span data-stu-id="8b140-113">If your organization uses proxy servers tooconnect toohello internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how tooconfigure them before you get started with Application Proxy.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="8b140-114">開啟您的連接埠</span><span class="sxs-lookup"><span data-stu-id="8b140-114">Open your ports</span></span>

<span data-ttu-id="8b140-115">tooprepare 環境針對 Azure AD Application Proxy，您必須先 tooenable 通訊 tooAzure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="8b140-115">tooprepare your environment for Azure AD Application Proxy, you first need tooenable communication tooAzure data centers.</span></span> <span data-ttu-id="8b140-116">如果 hello 路徑中有防火牆，請確認它已開啟，因此該連接器可以進行 HTTPS (TCP) 的 hello 要求 toohello 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8b140-116">If there is a firewall in hello path, make sure that it's open so that hello Connector can make HTTPS (TCP) requests toohello Application Proxy.</span></span>

1. <span data-ttu-id="8b140-117">開啟 hello siguientes puertos 太**輸出**流量：</span><span class="sxs-lookup"><span data-stu-id="8b140-117">Open hello following ports too**outbound** traffic:</span></span>

   | <span data-ttu-id="8b140-118">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="8b140-118">Port number</span></span> | <span data-ttu-id="8b140-119">使用方式</span><span class="sxs-lookup"><span data-stu-id="8b140-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="8b140-120">80</span><span class="sxs-lookup"><span data-stu-id="8b140-120">80</span></span> | <span data-ttu-id="8b140-121">下載憑證撤銷清單 (Crl) 時驗證 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="8b140-121">Downloading certificate revocation lists (CRLs) while validating hello SSL certificate</span></span> |
   | <span data-ttu-id="8b140-122">443</span><span class="sxs-lookup"><span data-stu-id="8b140-122">443</span></span> | <span data-ttu-id="8b140-123">所有的連出通訊以 hello 應用程式 Proxy 服務</span><span class="sxs-lookup"><span data-stu-id="8b140-123">All outbound communication with hello Application Proxy service</span></span> |

   <span data-ttu-id="8b140-124">如果您的防火牆，強制執行根據 toooriginating 使用者流量，開啟這些連接埠的流量從做為網路服務執行的 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="8b140-124">If your firewall enforces traffic according toooriginating users, open these ports for traffic from Windows services that run as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8b140-125">hello 反映出 hello 連接器版本 1.5.132.0 的連接埠需求及更新版本。</span><span class="sxs-lookup"><span data-stu-id="8b140-125">hello table reflects hello port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="8b140-126">如果仍有舊版的連接器，您也需要 tooenable hello 9350，下列連接埠在加法 too80 和 443: 5671、 8080，9090 9091，則為 9352 10100 – 10120。</span><span class="sxs-lookup"><span data-stu-id="8b140-126">If you still have an older connector version, you also need tooenable hello following ports in addition too80 and 443: 5671, 8080, 9090-9091, 9350, 9352, 10100–10120.</span></span>
   >
   ><span data-ttu-id="8b140-127">如需更新連接器 toohello 的最新版本的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md#automatic-updates)。</span><span class="sxs-lookup"><span data-stu-id="8b140-127">For information about updating your connectors toohello newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="8b140-128">如果您的防火牆或 proxy 可讓 DNS 允許清單，您可以允許清單連接 toomsappproxy.net 和.servicebus.windows.net 的支援。</span><span class="sxs-lookup"><span data-stu-id="8b140-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections toomsappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="8b140-129">如果沒有，您需要 tooallow 存取 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)，這會更新每週。</span><span class="sxs-lookup"><span data-stu-id="8b140-129">If not, you need tooallow access toohello [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="8b140-130">Microsoft 會使用四個位址 tooverify 憑證。</span><span class="sxs-lookup"><span data-stu-id="8b140-130">Microsoft uses four addresses tooverify certificates.</span></span> <span data-ttu-id="8b140-131">允許存取 toohello 如果您尚未這樣做其他產品的下列 Url:</span><span class="sxs-lookup"><span data-stu-id="8b140-131">Allow access toohello following URLs if you haven't done so for other products:</span></span>
   * <span data-ttu-id="8b140-132">mscrl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="8b140-132">mscrl.microsoft.com:80</span></span>
   * <span data-ttu-id="8b140-133">crl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="8b140-133">crl.microsoft.com:80</span></span>
   * <span data-ttu-id="8b140-134">ocsp.msocsp.com:80</span><span class="sxs-lookup"><span data-stu-id="8b140-134">ocsp.msocsp.com:80</span></span>
   * <span data-ttu-id="8b140-135">www.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="8b140-135">www.microsoft.com:80</span></span>

4. <span data-ttu-id="8b140-136">您的連接器需要存取 toologin.windows.net 和 login.microsoftonline.net 的 hello 註冊程序。</span><span class="sxs-lookup"><span data-stu-id="8b140-136">Your connector needs access toologin.windows.net and login.microsoftonline.net for hello registration process.</span></span>

5. <span data-ttu-id="8b140-137">使用 hello [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)tooverify 連接器可達到 hello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="8b140-137">Use hello [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify that your connector can reach hello Application Proxy service.</span></span> <span data-ttu-id="8b140-138">最少，請確定 hello 美國中部地區和 hello 區域最接近 tooyou 具有所有綠色的核取記號。</span><span class="sxs-lookup"><span data-stu-id="8b140-138">At a minimum, make sure that hello Central US region and hello region closest tooyou have all green checkmarks.</span></span> <span data-ttu-id="8b140-139">除此之外，綠色勾選記號越多代表恢復能力越佳。</span><span class="sxs-lookup"><span data-stu-id="8b140-139">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="install-and-register-a-connector"></a><span data-ttu-id="8b140-140">安裝並註冊連接器</span><span class="sxs-lookup"><span data-stu-id="8b140-140">Install and register a connector</span></span>
1. <span data-ttu-id="8b140-141">Hello 中的系統管理員身分登入[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8b140-141">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8b140-142">您目前的目錄會出現在 hello 右上角的 在您的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8b140-142">Your current directory appears under your username in hello top right corner.</span></span> <span data-ttu-id="8b140-143">如果您需要 toochange 目錄，請選取該圖示。</span><span class="sxs-lookup"><span data-stu-id="8b140-143">If you need toochange directories, select that icon.</span></span>
3. <span data-ttu-id="8b140-144">跳過**Azure Active Directory** > **應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="8b140-144">Go too**Azure Active Directory** > **Application Proxy**.</span></span>

   ![瀏覽 tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. <span data-ttu-id="8b140-146">選取 [下載連接器]。</span><span class="sxs-lookup"><span data-stu-id="8b140-146">Select **Download Connector**.</span></span>

   ![下載連接器](./media/active-directory-application-proxy-enable/download_connector.png)

5. <span data-ttu-id="8b140-148">執行**AADApplicationProxyConnectorInstaller.exe** hello 伺服器上您備妥相應 toohello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="8b140-148">Run **AADApplicationProxyConnectorInstaller.exe** on hello server you prepared according toohello prerequisites.</span></span>
6. <span data-ttu-id="8b140-149">遵循 hello 精靈 tooinstall hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="8b140-149">Follow hello instructions in hello wizard tooinstall.</span></span> <span data-ttu-id="8b140-150">在安裝期間，您必須提示的 tooregister hello hello 的 Azure AD 租用戶的應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="8b140-150">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="8b140-151">提供您的 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8b140-151">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="8b140-152">您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。</span><span class="sxs-lookup"><span data-stu-id="8b140-152">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="8b140-153">請確定暫存器 hello 連接器處於 hello 相同的目錄已啟用 hello 管理員 hello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="8b140-153">Make sure hello admin who registers hello connector is in hello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="8b140-154">例如，如果 hello 租用戶網域為 contoso.com，hello admin 應該是admin@contoso.com或在該網域上的任何其他別名。</span><span class="sxs-lookup"><span data-stu-id="8b140-154">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="8b140-155">如果**IE 增強式安全性設定**設定得**上**hello 在伺服器上安裝 hello 連接器，您可能無法看見 hello 註冊 畫面中。</span><span class="sxs-lookup"><span data-stu-id="8b140-155">If **IE Enhanced Security Configuration** is set too**On** on hello server where you are installing hello connector, you may not see hello registration screen.</span></span> <span data-ttu-id="8b140-156">tooget 存取權，遵循 hello hello 錯誤訊息中的指示。</span><span class="sxs-lookup"><span data-stu-id="8b140-156">tooget access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="8b140-157">請確定已停用 [Internet Explorer 增強式安全性]。</span><span class="sxs-lookup"><span data-stu-id="8b140-157">Make sure that Internet Explorer Enhanced Security is off.</span></span>

<span data-ttu-id="8b140-158">為了實現高可用性，您應該至少部署兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="8b140-158">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="8b140-159">每個連接器都必須分別進行註冊。</span><span class="sxs-lookup"><span data-stu-id="8b140-159">Each connector must be registered separately.</span></span>

## <a name="test-that-hello-connector-installed-correctly"></a><span data-ttu-id="8b140-160">測試已正確安裝該 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="8b140-160">Test that hello connector installed correctly</span></span>

<span data-ttu-id="8b140-161">您可以確認新的連接器，檢查它在任一個 hello Azure 入口網站或伺服器上正確安裝。</span><span class="sxs-lookup"><span data-stu-id="8b140-161">You can confirm that a new connector installed correctly by checking for it in either hello Azure portal or on your server.</span></span> 

<span data-ttu-id="8b140-162">在 hello Azure 入口網站、 登入 tooyour 租用戶和瀏覽過**Azure Active Directory** > **應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="8b140-162">In hello Azure portal, sign in tooyour tenant and navigate too**Azure Active Directory** > **Application Proxy**.</span></span> <span data-ttu-id="8b140-163">所有的連接器與連接器群組都會出現在此頁面上。</span><span class="sxs-lookup"><span data-stu-id="8b140-163">All of your connectors and connector groups appear on this page.</span></span> <span data-ttu-id="8b140-164">選取連接器 toosee 其詳細資料，或將它移至不同的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="8b140-164">Select a connector toosee its details or move it into a different connector group.</span></span> 

<span data-ttu-id="8b140-165">在您的伺服器，請檢查 hello 清單 hello 連接器與 hello 連接器更新程式的作用中服務。</span><span class="sxs-lookup"><span data-stu-id="8b140-165">On your server, check hello list of active services for hello connector and hello connector updater.</span></span> <span data-ttu-id="8b140-166">hello 兩個服務應該立即，開始執行，但如果沒有，請加以啟動：</span><span class="sxs-lookup"><span data-stu-id="8b140-166">hello two services should start running immediately, but if not, turn them on:</span></span> 

   * <span data-ttu-id="8b140-167">**Microsoft AAD 應用程式 Proxy 連接器** 可啟用連線</span><span class="sxs-lookup"><span data-stu-id="8b140-167">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

   * <span data-ttu-id="8b140-168">**Microsoft AAD 應用程式 Proxy 連接器更新程式**是自動更新服務。</span><span class="sxs-lookup"><span data-stu-id="8b140-168">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="8b140-169">hello updater 會檢查新版本的 hello 連接器，並且更新 hello 連接器，視需要。</span><span class="sxs-lookup"><span data-stu-id="8b140-169">hello updater checks for new versions of hello connector and updates hello connector as needed.</span></span>

   ![應用程式 Proxy 連接器服務 - 螢幕擷取畫面](./media/active-directory-application-proxy-enable/app_proxy_services.png)

<span data-ttu-id="8b140-171">如需連接器和方式，就會維持 toodate 註冊資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="8b140-171">For information about connectors and how they stay up toodate, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8b140-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b140-172">Next steps</span></span>
<span data-ttu-id="8b140-173">現在您已經準備就緒太[發行應用程式 Proxy](application-proxy-publish-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8b140-173">You are now ready too[Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

<span data-ttu-id="8b140-174">如果您有個別的網路或不同的位置上的應用程式，使用連接器，將邏輯單元分 tooorganize hello 不同連接器。</span><span class="sxs-lookup"><span data-stu-id="8b140-174">If you have applications that are on separate networks or different locations, use connector groups tooorganize hello different connectors into logical units.</span></span> <span data-ttu-id="8b140-175">深入了解 [使用應用程式 Proxy 連接器](active-directory-application-proxy-connectors-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8b140-175">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors-azure-portal.md).</span></span>
