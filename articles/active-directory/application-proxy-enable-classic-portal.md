---
title: "aaaEnable hello 傳統入口網站中的 Azure AD Application Proxy |Microsoft 文件"
description: "開啟應用程式 Proxy 在 hello Azure 傳統入口網站，並安裝 hello hello 反向 proxy 連接器。"
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
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a><span data-ttu-id="70445-103">Hello 傳統入口網站中啟用應用程式 Proxy 並下載連接器</span><span class="sxs-lookup"><span data-stu-id="70445-103">Enable Application Proxy in hello classic portal and download connectors</span></span>
<span data-ttu-id="70445-104">本文將告訴您透過 hello 步驟 tooenable Microsoft Azure AD 應用程式 Proxy 為您的雲端目錄，在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="70445-104">This article walks you through hello steps tooenable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="70445-105">如果您不熟悉哪些應用程式 Proxy 可協助您執行，深入了解[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="70445-105">If you're unfamiliar with what Application Proxy can help you do, learn more about [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="70445-106">應用程式 Proxy 先決條件</span><span class="sxs-lookup"><span data-stu-id="70445-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="70445-107">您可以啟用及使用應用程式 Proxy 服務之前，您會需要 toohave:</span><span class="sxs-lookup"><span data-stu-id="70445-107">Before you can enable and use Application Proxy services, you need toohave:</span></span>

* <span data-ttu-id="70445-108">Microsoft Azure AD [基本或進階訂用帳戶](active-directory-editions.md) 以及您是全域管理員的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="70445-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="70445-109">執行 Windows Server 2012 R2 或 2016，您可以安裝 hello 應用程式 Proxy 連接器的伺服器。</span><span class="sxs-lookup"><span data-stu-id="70445-109">A server running Windows Server 2012 R2 or 2016, on which you can install hello Application Proxy Connector.</span></span> <span data-ttu-id="70445-110">hello 伺服器要求 toohello 應用程式 Proxy 會將服務傳送 hello 雲端中，需要 HTTP 或 HTTPS 連線 toohello 應用程式，您要發行。</span><span class="sxs-lookup"><span data-stu-id="70445-110">hello server sends requests toohello Application Proxy services in hello cloud, and it needs an HTTP or HTTPS connection toohello applications that you are publishing.</span></span>
  * <span data-ttu-id="70445-111">單一登入 tooyour 已發佈的應用程式，這部電腦應該是網域的 hello 相同的 AD 網域中做為您要發行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70445-111">For single sign-on tooyour published applications, this machine should be domain-joined in hello same AD domain as hello applications that you are publishing.</span></span> <span data-ttu-id="70445-112">如需詳細資訊，請參閱[使用應用程式 Proxy 進行單一登入](active-directory-application-proxy-sso-using-kcd.md)</span><span class="sxs-lookup"><span data-stu-id="70445-112">For information, see [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span></span>
* <span data-ttu-id="70445-113">如果您的組織使用 proxy 伺服器 tooconnect toohello 網際網路，讀取[使用現有的內部 proxy 伺服器](application-proxy-working-with-proxy-servers.md)的詳細資料 tooconfigure 它們。</span><span class="sxs-lookup"><span data-stu-id="70445-113">If your organization uses proxy servers tooconnect toohello internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how tooconfigure them.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="70445-114">開啟您的連接埠</span><span class="sxs-lookup"><span data-stu-id="70445-114">Open your ports</span></span>

<span data-ttu-id="70445-115">tooprepare 環境針對 Azure AD Application Proxy，您必須先 tooenable 通訊 tooAzure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="70445-115">tooprepare your environment for Azure AD Application Proxy, you first need tooenable communication tooAzure data centers.</span></span> <span data-ttu-id="70445-116">如果 hello 路徑中有防火牆，請確認它已開啟，因此該連接器可以進行 HTTPS (TCP) 的 hello 要求 toohello 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="70445-116">If there is a firewall in hello path, make sure that it's open so that hello Connector can make HTTPS (TCP) requests toohello Application Proxy.</span></span>

1. <span data-ttu-id="70445-117">開啟 hello siguientes puertos 太**輸出**流量：</span><span class="sxs-lookup"><span data-stu-id="70445-117">Open hello following ports too**outbound** traffic:</span></span>

   | <span data-ttu-id="70445-118">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="70445-118">Port number</span></span> | <span data-ttu-id="70445-119">使用方式</span><span class="sxs-lookup"><span data-stu-id="70445-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="70445-120">80</span><span class="sxs-lookup"><span data-stu-id="70445-120">80</span></span> | <span data-ttu-id="70445-121">下載憑證撤銷清單 (Crl) 時驗證 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="70445-121">Downloading certificate revocation lists (CRLs) while validating hello SSL certificate</span></span> |
   | <span data-ttu-id="70445-122">443</span><span class="sxs-lookup"><span data-stu-id="70445-122">443</span></span> | <span data-ttu-id="70445-123">所有的連出通訊以 hello 應用程式 Proxy 服務</span><span class="sxs-lookup"><span data-stu-id="70445-123">All outbound communication with hello Application Proxy service</span></span> |

   <span data-ttu-id="70445-124">如果您的防火牆，強制執行根據 toooriginating 使用者流量，開啟 estos puertos para el 與執行以網路服務的 Windows 服務的流量。</span><span class="sxs-lookup"><span data-stu-id="70445-124">If your firewall enforces traffic according toooriginating users, open these ports for traffic coming from Windows services running as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="70445-125">hello 反映出 hello 連接器版本 1.5.132.0 的連接埠需求及更新版本。</span><span class="sxs-lookup"><span data-stu-id="70445-125">hello table reflects hello port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="70445-126">如果仍有舊版的連接器，您也需要下列連接埠 tooenable hello: 5671、 8080、 9090、 9091、 9350、 9352，和 10100 – 10120。</span><span class="sxs-lookup"><span data-stu-id="70445-126">If you still have an older connector version, you also need tooenable hello following ports: 5671, 8080, 9090, 9091, 9350, 9352, and 10100–10120.</span></span>
   >
   ><span data-ttu-id="70445-127">如需更新連接器 toohello 的最新版本的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md#automatic-updates)。</span><span class="sxs-lookup"><span data-stu-id="70445-127">For information about updating your connectors toohello newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="70445-128">如果您的防火牆或 proxy 可讓 DNS 允許清單，您可以允許清單連接 toomsappproxy.net 和.servicebus.windows.net 的支援。</span><span class="sxs-lookup"><span data-stu-id="70445-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections toomsappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="70445-129">如果沒有，您需要 tooallow 存取 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)，這會更新每週。</span><span class="sxs-lookup"><span data-stu-id="70445-129">If not, you need tooallow access toohello [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="70445-130">使用 hello [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)tooverify 連接器可達到 hello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="70445-130">Use hello [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify that your connector can reach hello Application Proxy service.</span></span> <span data-ttu-id="70445-131">最少，請確定 hello 美國中部地區和 hello 區域最接近 tooyou 具有所有綠色的核取記號。</span><span class="sxs-lookup"><span data-stu-id="70445-131">At a minimum, make sure that hello Central US region and hello region closest tooyou have all green checkmarks.</span></span> <span data-ttu-id="70445-132">除此之外，綠色勾選記號越多代表恢復能力越佳。</span><span class="sxs-lookup"><span data-stu-id="70445-132">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="enable-application-proxy-in-azure-ad"></a><span data-ttu-id="70445-133">Azure AD 中啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="70445-133">Enable Application Proxy in Azure AD</span></span>
1. <span data-ttu-id="70445-134">Hello 中的系統管理員身分登入[Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="70445-134">Sign in as an administrator in hello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="70445-135">請 tooActive 目錄並選取您想在其中 tooenable 應用程式 Proxy 的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="70445-135">Go tooActive Directory and select hello directory in which you want tooenable Application Proxy.</span></span>

    ![Active Directory - 圖示](./media/active-directory-application-proxy-enable/ad_icon.png)
3. <span data-ttu-id="70445-137">選取**設定**從 hello 目錄 頁面上，向下捲動太**應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="70445-137">Select **Configure** from hello directory page, and scroll down too**Application Proxy**.</span></span>
4. <span data-ttu-id="70445-138">切換**此目錄啟用應用程式 Proxy 服務**太**啟用**。</span><span class="sxs-lookup"><span data-stu-id="70445-138">Toggle **Enable Application Proxy Services for this Directory** too**Enabled**.</span></span>

    ![啟用應用程式 Proxy](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. <span data-ttu-id="70445-140">選取 [立即下載] 。</span><span class="sxs-lookup"><span data-stu-id="70445-140">Select **Download now**.</span></span> <span data-ttu-id="70445-141">hello **Azure 的 AD 應用程式 Proxy 連接器下載**隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="70445-141">hello **Azure AD Application Proxy Connector Download** opens.</span></span> <span data-ttu-id="70445-142">閱讀並接受 hello 授權條款，然後按一下**下載**toosave hello Windows Installer 檔案 (.exe) hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="70445-142">Read and accept hello license terms and click **Download** toosave hello Windows Installer file (.exe) for hello connector.</span></span>

## <a name="install-and-register-hello-connector"></a><span data-ttu-id="70445-143">安裝並註冊 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="70445-143">Install and register hello Connector</span></span>
1. <span data-ttu-id="70445-144">執行**AADApplicationProxyConnectorInstaller.exe** hello 伺服器上您備妥相應 toohello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="70445-144">Run **AADApplicationProxyConnectorInstaller.exe** on hello server you prepared according toohello prerequisites.</span></span>
2. <span data-ttu-id="70445-145">遵循 hello 精靈 tooinstall hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="70445-145">Follow hello instructions in hello wizard tooinstall.</span></span>
3. <span data-ttu-id="70445-146">在安裝期間，您必須提示的 tooregister hello hello 的 Azure AD 租用戶的應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="70445-146">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="70445-147">提供您的 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="70445-147">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="70445-148">您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。</span><span class="sxs-lookup"><span data-stu-id="70445-148">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="70445-149">請確定暫存器 hello 連接器處於 hello 相同的目錄已啟用 hello 管理員 hello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="70445-149">Make sure hello admin who registers hello connector is in hello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="70445-150">例如，如果 hello 租用戶網域為 contoso.com，hello admin 應該是admin@contoso.com或在該網域上的任何其他別名。</span><span class="sxs-lookup"><span data-stu-id="70445-150">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="70445-151">如果**IE 增強式安全性設定**設定得**上**hello 註冊畫面可能會封鎖 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="70445-151">If **IE Enhanced Security Configuration** is set too**On** on hello server, hello registration screen might be blocked.</span></span> <span data-ttu-id="70445-152">tooallow 存取權，遵循 hello hello 錯誤訊息中的指示。</span><span class="sxs-lookup"><span data-stu-id="70445-152">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="70445-153">請確定已停用 [Internet Explorer 增強式安全性]。</span><span class="sxs-lookup"><span data-stu-id="70445-153">Make sure that Internet Explorer Enhanced Security is off.</span></span>
   * <span data-ttu-id="70445-154">如果連接器註冊不成功，請參閱 [針對應用程式 Proxy 進行疑難排解](active-directory-application-proxy-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="70445-154">If connector registration does not succeed, see [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md).</span></span>  
4. <span data-ttu-id="70445-155">Hello 安裝完成時，兩個 se agregan dos nuevos tooyour 伺服器：</span><span class="sxs-lookup"><span data-stu-id="70445-155">When hello installation completes, two new services are added tooyour server:</span></span>

   * <span data-ttu-id="70445-156">**Microsoft AAD 應用程式 Proxy 連接器** 可啟用連線</span><span class="sxs-lookup"><span data-stu-id="70445-156">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

     * <span data-ttu-id="70445-157">**Microsoft AAD 應用程式 Proxy 連接器更新程式**是自動更新服務。</span><span class="sxs-lookup"><span data-stu-id="70445-157">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="70445-158">定期檢查有新版本的 hello 連接器，並視需要更新 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="70445-158">It periodically checks for new versions of hello connector and updates hello connector as needed.</span></span>

     ![應用程式 Proxy 連接器服務 - 螢幕擷取畫面](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. <span data-ttu-id="70445-160">按一下**完成**hello 安裝視窗中。</span><span class="sxs-lookup"><span data-stu-id="70445-160">Click **Finish** in hello installation window.</span></span>

<span data-ttu-id="70445-161">如需連接器的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="70445-161">For information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

<span data-ttu-id="70445-162">為了實現高可用性，您應該至少部署兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="70445-162">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="70445-163">toodeploy 多個連接器，重複步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="70445-163">toodeploy more connectors, repeat steps 2 and 3.</span></span> <span data-ttu-id="70445-164">每個連接器都必須分別進行註冊。</span><span class="sxs-lookup"><span data-stu-id="70445-164">Each connector must be registered separately.</span></span>

<span data-ttu-id="70445-165">如果您想 toouninstall hello 連接器，請解除安裝 hello 連接器服務和 hello Updater 服務。</span><span class="sxs-lookup"><span data-stu-id="70445-165">If you want toouninstall hello Connector, uninstall both hello Connector service and hello Updater service.</span></span> <span data-ttu-id="70445-166">重新啟動電腦 toofully 移除 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="70445-166">Restart your computer toofully remove hello service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70445-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70445-167">Next steps</span></span>
<span data-ttu-id="70445-168">現在您已經準備就緒太[發行應用程式 Proxy](active-directory-application-proxy-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="70445-168">You are now ready too[Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

<span data-ttu-id="70445-169">如果您有個別的網路或不同的位置上的應用程式，您可以使用連接器群組 tooorganize hello 不同連接器成邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="70445-169">If you have applications that are on separate networks or different locations, you can use connector groups tooorganize hello different connectors into logical units.</span></span> <span data-ttu-id="70445-170">深入了解 [使用應用程式 Proxy 連接器](active-directory-application-proxy-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="70445-170">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors.md).</span></span>
