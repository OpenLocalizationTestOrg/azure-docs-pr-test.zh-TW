---
title: "Azure AD 應用程式 Proxy - 開始安裝連接器 | Microsoft Docs"
description: "在 Azure 入口網站中開啟應用程式 Proxy，並安裝反向 Proxy 的連接器。"
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
ms.openlocfilehash: 77acb23f33fd656a12c27107cb159613a8b2aec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-proxy-and-install-the-connector"></a><span data-ttu-id="fc408-103">開始使用應用程式 Proxy 並安裝連接器</span><span class="sxs-lookup"><span data-stu-id="fc408-103">Get started with Application Proxy and install the connector</span></span>
<span data-ttu-id="fc408-104">本文將逐步引導您完成為 Azure AD 中的雲端目錄啟用 Microsoft Azure AD 應用程式 Proxy 的步驟。</span><span class="sxs-lookup"><span data-stu-id="fc408-104">This article walks you through the steps to enable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="fc408-105">如果您還不知道應用程式 Proxy 為您的組織帶來的安全性和生產力優勢，請深入了解[如何為內部部署應用程式提供安全的遠端存取](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fc408-105">If you're not yet aware of the security and productivity benefits Application Proxy brings to your organization, learn more about [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="fc408-106">應用程式 Proxy 先決條件</span><span class="sxs-lookup"><span data-stu-id="fc408-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="fc408-107">您可以啟用並使用應用程式 Proxy 服務之前，必須具備：</span><span class="sxs-lookup"><span data-stu-id="fc408-107">Before you can enable and use Application Proxy services, you need to have:</span></span>

* <span data-ttu-id="fc408-108">Microsoft Azure AD [基本或進階訂用帳戶](active-directory-editions.md) 以及您是全域管理員的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="fc408-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="fc408-109">您可以在執行 Windows Server 2012 R2 或 2016 的伺服器上，安裝應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="fc408-109">A server running Windows Server 2012 R2 or 2016, on which you can install the Application Proxy Connector.</span></span> <span data-ttu-id="fc408-110">伺服器必須能夠連線至雲端中的應用程式 Proxy 服務，以及您所發佈的內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc408-110">The server needs to be able to connect to the Application Proxy services in the cloud, and the on-premises applications that you are publishing.</span></span>
  * <span data-ttu-id="fc408-111">如需使用 Kerberos 限制委派單一登入已發佈的應用程式，這部電腦應該會加入與您要發佈的應用程式相同的 AD 網域中。</span><span class="sxs-lookup"><span data-stu-id="fc408-111">For single sign-on to your published applications using Kerberos Constrained Delegation, this machine should be domain-joined in the same AD domain as the applications that you are publishing.</span></span> <span data-ttu-id="fc408-112">如需詳細資訊，請參閱[使用應用程式 Proxy 進行單一登入的 KCD](active-directory-application-proxy-sso-using-kcd.md)。</span><span class="sxs-lookup"><span data-stu-id="fc408-112">For information, see [KCD for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

<span data-ttu-id="fc408-113">如果您的組織使用 Proxy 伺服器來連線至網際網路，請參閱[使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md)，以取得如何在開始使用應用程式 Proxy 之前設定伺服器的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fc408-113">If your organization uses proxy servers to connect to the internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how to configure them before you get started with Application Proxy.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="fc408-114">開啟您的連接埠</span><span class="sxs-lookup"><span data-stu-id="fc408-114">Open your ports</span></span>

<span data-ttu-id="fc408-115">若要準備適合 Azure AD 應用程式 Proxy 的環境，您需要先啟用 Azure 資料中心的通訊。</span><span class="sxs-lookup"><span data-stu-id="fc408-115">To prepare your environment for Azure AD Application Proxy, you first need to enable communication to Azure data centers.</span></span> <span data-ttu-id="fc408-116">如果路徑中有防火牆，請確定防火牆已開啟，以便連接器可以對應用程式 Proxy 提出 HTTPS (TCP) 要求。</span><span class="sxs-lookup"><span data-stu-id="fc408-116">If there is a firewall in the path, make sure that it's open so that the Connector can make HTTPS (TCP) requests to the Application Proxy.</span></span>

1. <span data-ttu-id="fc408-117">開啟下列連接埠以**輸出**流量：</span><span class="sxs-lookup"><span data-stu-id="fc408-117">Open the following ports to **outbound** traffic:</span></span>

   | <span data-ttu-id="fc408-118">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="fc408-118">Port number</span></span> | <span data-ttu-id="fc408-119">使用方式</span><span class="sxs-lookup"><span data-stu-id="fc408-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="fc408-120">80</span><span class="sxs-lookup"><span data-stu-id="fc408-120">80</span></span> | <span data-ttu-id="fc408-121">下載憑證撤銷清單 (CRL) 時驗證 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="fc408-121">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span></span> |
   | <span data-ttu-id="fc408-122">443</span><span class="sxs-lookup"><span data-stu-id="fc408-122">443</span></span> | <span data-ttu-id="fc408-123">應用程式 Proxy 服務的所有傳出通訊</span><span class="sxs-lookup"><span data-stu-id="fc408-123">All outbound communication with the Application Proxy service</span></span> |

   <span data-ttu-id="fc408-124">如果您的防火牆根據原始使用者強制執行流量，請針對來自當作網路服務執行之 Windows 服務的流量，開放這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="fc408-124">If your firewall enforces traffic according to originating users, open these ports for traffic from Windows services that run as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fc408-125">下表反映連接器 1.5.132.0 版及更新版本的連接埠需求。</span><span class="sxs-lookup"><span data-stu-id="fc408-125">The table reflects the port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="fc408-126">如果仍有舊版的連接器，您也需要啟用除了80 和 443 以外的下列連接埠：5671、8080、9090、9091、9350、9352、10100–10120。</span><span class="sxs-lookup"><span data-stu-id="fc408-126">If you still have an older connector version, you also need to enable the following ports in addition to 80 and 443: 5671, 8080, 9090-9091, 9350, 9352, 10100–10120.</span></span>
   >
   ><span data-ttu-id="fc408-127">如需將連接器更新至最新版本的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md#automatic-updates)。</span><span class="sxs-lookup"><span data-stu-id="fc408-127">For information about updating your connectors to the newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="fc408-128">如果您的防火牆或 Proxy 允許建立 DNS 白名單，您可以建立 msappProxy.net 和 servicebus.windows.net 的白名單連線。</span><span class="sxs-lookup"><span data-stu-id="fc408-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections to msappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="fc408-129">如果不是，您需要允許對每週更新的 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)的存取。</span><span class="sxs-lookup"><span data-stu-id="fc408-129">If not, you need to allow access to the [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="fc408-130">Microsoft 使用四個位址來驗證憑證。</span><span class="sxs-lookup"><span data-stu-id="fc408-130">Microsoft uses four addresses to verify certificates.</span></span> <span data-ttu-id="fc408-131">請允許存取下列 URL (若尚未允許其他產品存取)：</span><span class="sxs-lookup"><span data-stu-id="fc408-131">Allow access to the following URLs if you haven't done so for other products:</span></span>
   * <span data-ttu-id="fc408-132">mscrl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="fc408-132">mscrl.microsoft.com:80</span></span>
   * <span data-ttu-id="fc408-133">crl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="fc408-133">crl.microsoft.com:80</span></span>
   * <span data-ttu-id="fc408-134">ocsp.msocsp.com:80</span><span class="sxs-lookup"><span data-stu-id="fc408-134">ocsp.msocsp.com:80</span></span>
   * <span data-ttu-id="fc408-135">www.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="fc408-135">www.microsoft.com:80</span></span>

4. <span data-ttu-id="fc408-136">您的連接器必須為了註冊程序存取 login.windows.net 和 login.microsoftonline.net。</span><span class="sxs-lookup"><span data-stu-id="fc408-136">Your connector needs access to login.windows.net and login.microsoftonline.net for the registration process.</span></span>

5. <span data-ttu-id="fc408-137">請使用 [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)，來確認您的連接器是否能夠連線到「應用程式 Proxy」服務。</span><span class="sxs-lookup"><span data-stu-id="fc408-137">Use the [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) to verify that your connector can reach the Application Proxy service.</span></span> <span data-ttu-id="fc408-138">至少，請確定「美國中部」區域及離您最近的區域都具有綠色勾選記號。</span><span class="sxs-lookup"><span data-stu-id="fc408-138">At a minimum, make sure that the Central US region and the region closest to you have all green checkmarks.</span></span> <span data-ttu-id="fc408-139">除此之外，綠色勾選記號越多代表恢復能力越佳。</span><span class="sxs-lookup"><span data-stu-id="fc408-139">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="install-and-register-a-connector"></a><span data-ttu-id="fc408-140">安裝並註冊連接器</span><span class="sxs-lookup"><span data-stu-id="fc408-140">Install and register a connector</span></span>
1. <span data-ttu-id="fc408-141">在 [Azure 入口網站](https://portal.azure.com/)中，以系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="fc408-141">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fc408-142">您目前的目錄會顯示在右上角的使用者名稱之下。</span><span class="sxs-lookup"><span data-stu-id="fc408-142">Your current directory appears under your username in the top right corner.</span></span> <span data-ttu-id="fc408-143">如果您需要變更目錄，請選取該圖示。</span><span class="sxs-lookup"><span data-stu-id="fc408-143">If you need to change directories, select that icon.</span></span>
3. <span data-ttu-id="fc408-144">移至 [Azure Active Directory] > [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="fc408-144">Go to **Azure Active Directory** > **Application Proxy**.</span></span>

   ![瀏覽至 [應用程式 Proxy]](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. <span data-ttu-id="fc408-146">選取 [下載連接器]。</span><span class="sxs-lookup"><span data-stu-id="fc408-146">Select **Download Connector**.</span></span>

   ![下載連接器](./media/active-directory-application-proxy-enable/download_connector.png)

5. <span data-ttu-id="fc408-148">在您根據必要條件所準備好的伺服器上執行 **AADApplicationProxyConnectorInstaller.exe** 。</span><span class="sxs-lookup"><span data-stu-id="fc408-148">Run **AADApplicationProxyConnectorInstaller.exe** on the server you prepared according to the prerequisites.</span></span>
6. <span data-ttu-id="fc408-149">依照精靈中的指示進行安裝。</span><span class="sxs-lookup"><span data-stu-id="fc408-149">Follow the instructions in the wizard to install.</span></span> <span data-ttu-id="fc408-150">在安裝期間，系統將提示您向 Azure AD 租用戶的應用程式 Proxy 註冊連接器。</span><span class="sxs-lookup"><span data-stu-id="fc408-150">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="fc408-151">提供您的 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="fc408-151">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="fc408-152">您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。</span><span class="sxs-lookup"><span data-stu-id="fc408-152">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="fc408-153">請確定註冊連接器的系統管理員與您啟用應用程式 Proxy 服務的位置在相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="fc408-153">Make sure the admin who registers the connector is in the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="fc408-154">例如，如果租用戶網域為 contoso.com，則系統管理員應該是 admin@contoso.com ，或該網域上的其他別名。</span><span class="sxs-lookup"><span data-stu-id="fc408-154">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="fc408-155">如果 [IE 增強式安全性組態] 在您要安裝連接器的伺服器上設定為 [開啟]，您可能看不到註冊畫面。</span><span class="sxs-lookup"><span data-stu-id="fc408-155">If **IE Enhanced Security Configuration** is set to **On** on the server where you are installing the connector, you may not see the registration screen.</span></span> <span data-ttu-id="fc408-156">若要取得存取權，請依照錯誤訊息中的指示。</span><span class="sxs-lookup"><span data-stu-id="fc408-156">To get access, follow the instructions in the error message.</span></span> <span data-ttu-id="fc408-157">請確定已停用 [Internet Explorer 增強式安全性]。</span><span class="sxs-lookup"><span data-stu-id="fc408-157">Make sure that Internet Explorer Enhanced Security is off.</span></span>

<span data-ttu-id="fc408-158">為了實現高可用性，您應該至少部署兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="fc408-158">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="fc408-159">每個連接器都必須分別進行註冊。</span><span class="sxs-lookup"><span data-stu-id="fc408-159">Each connector must be registered separately.</span></span>

## <a name="test-that-the-connector-installed-correctly"></a><span data-ttu-id="fc408-160">測試連接器是否安裝正確</span><span class="sxs-lookup"><span data-stu-id="fc408-160">Test that the connector installed correctly</span></span>

<span data-ttu-id="fc408-161">您可以在 Azure 入口網站中或在您的伺服器上檢查新的連接器，以確認它是否安裝正確。</span><span class="sxs-lookup"><span data-stu-id="fc408-161">You can confirm that a new connector installed correctly by checking for it in either the Azure portal or on your server.</span></span> 

<span data-ttu-id="fc408-162">在 Azure 入口網站中，登入您的租用戶並巡覽至 [Azure Active Directory] > [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="fc408-162">In the Azure portal, sign in to your tenant and navigate to **Azure Active Directory** > **Application Proxy**.</span></span> <span data-ttu-id="fc408-163">所有的連接器與連接器群組都會出現在此頁面上。</span><span class="sxs-lookup"><span data-stu-id="fc408-163">All of your connectors and connector groups appear on this page.</span></span> <span data-ttu-id="fc408-164">選取連接器，以查看其詳細資料，或將它移至不同的連接器群組。</span><span class="sxs-lookup"><span data-stu-id="fc408-164">Select a connector to see its details or move it into a different connector group.</span></span> 

<span data-ttu-id="fc408-165">在您的伺服器上，檢查連接器與連接器更新程式的作用中服務清單。</span><span class="sxs-lookup"><span data-stu-id="fc408-165">On your server, check the list of active services for the connector and the connector updater.</span></span> <span data-ttu-id="fc408-166">這兩項服務應該立即開始執行，但非如此，請加以啟動：</span><span class="sxs-lookup"><span data-stu-id="fc408-166">The two services should start running immediately, but if not, turn them on:</span></span> 

   * <span data-ttu-id="fc408-167">**Microsoft AAD 應用程式 Proxy 連接器** 可啟用連線</span><span class="sxs-lookup"><span data-stu-id="fc408-167">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

   * <span data-ttu-id="fc408-168">**Microsoft AAD 應用程式 Proxy 連接器更新程式**是自動更新服務。</span><span class="sxs-lookup"><span data-stu-id="fc408-168">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="fc408-169">更新程式會檢查連接器的新版本，並且視需要更新連接器。</span><span class="sxs-lookup"><span data-stu-id="fc408-169">The updater checks for new versions of the connector and updates the connector as needed.</span></span>

   ![應用程式 Proxy 連接器服務 - 螢幕擷取畫面](./media/active-directory-application-proxy-enable/app_proxy_services.png)

<span data-ttu-id="fc408-171">如需有關連接器以及其如何保持最新狀態的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="fc408-171">For information about connectors and how they stay up to date, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fc408-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc408-172">Next steps</span></span>
<span data-ttu-id="fc408-173">您現在已經準備好 [使用應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fc408-173">You are now ready to [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

<span data-ttu-id="fc408-174">如果您有位於不同網路或不同位置上的應用程式，請使用連接器群組將不同的連接器組織成邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="fc408-174">If you have applications that are on separate networks or different locations, use connector groups to organize the different connectors into logical units.</span></span> <span data-ttu-id="fc408-175">深入了解 [使用應用程式 Proxy 連接器](active-directory-application-proxy-connectors-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fc408-175">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors-azure-portal.md).</span></span>
