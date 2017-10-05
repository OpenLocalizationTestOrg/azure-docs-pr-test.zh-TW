---
title: "在傳統入口網站中啟用 Azure AD 應用程式 Proxy | Microsoft Docs"
description: "在 Azure 傳統入口網站中開啟應用程式 Proxy，並安裝反向 Proxy 的連接器。"
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
ms.openlocfilehash: ea97fdc8d146ed524a932018b572ceda0982738b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-application-proxy-in-the-classic-portal-and-download-connectors"></a><span data-ttu-id="497f2-103">在傳統入口網站中啟用應用程式 Proxy 並下載連接器</span><span class="sxs-lookup"><span data-stu-id="497f2-103">Enable Application Proxy in the classic portal and download connectors</span></span>
<span data-ttu-id="497f2-104">本文將逐步引導您完成為 Azure AD 中的雲端目錄啟用 Microsoft Azure AD 應用程式 Proxy 的步驟。</span><span class="sxs-lookup"><span data-stu-id="497f2-104">This article walks you through the steps to enable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="497f2-105">如果您不熟悉應用程式 Proxy 可協助您執行的工作，請深入了解 [如何為內部部署應用程式提供安全的遠端存取](active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="497f2-105">If you're unfamiliar with what Application Proxy can help you do, learn more about [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="497f2-106">應用程式 Proxy 先決條件</span><span class="sxs-lookup"><span data-stu-id="497f2-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="497f2-107">您可以啟用並使用應用程式 Proxy 服務之前，必須具備：</span><span class="sxs-lookup"><span data-stu-id="497f2-107">Before you can enable and use Application Proxy services, you need to have:</span></span>

* <span data-ttu-id="497f2-108">Microsoft Azure AD [基本或進階訂用帳戶](active-directory-editions.md) 以及您是全域管理員的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="497f2-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="497f2-109">您可以在執行 Windows Server 2012 R2 或 2016 的伺服器上，安裝應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="497f2-109">A server running Windows Server 2012 R2 or 2016, on which you can install the Application Proxy Connector.</span></span> <span data-ttu-id="497f2-110">伺服器會將要求傳送至雲端的應用程式 Proxy 服務，而且需要您所發佈之應用程式的 HTTP 或 HTTPS 連線。</span><span class="sxs-lookup"><span data-stu-id="497f2-110">The server sends requests to the Application Proxy services in the cloud, and it needs an HTTP or HTTPS connection to the applications that you are publishing.</span></span>
  * <span data-ttu-id="497f2-111">如需單一登入已發佈的應用程式，這部電腦應該會加入與您要發佈的應用程式相同的 AD 網域中。</span><span class="sxs-lookup"><span data-stu-id="497f2-111">For single sign-on to your published applications, this machine should be domain-joined in the same AD domain as the applications that you are publishing.</span></span> <span data-ttu-id="497f2-112">如需詳細資訊，請參閱[使用應用程式 Proxy 進行單一登入](active-directory-application-proxy-sso-using-kcd.md)</span><span class="sxs-lookup"><span data-stu-id="497f2-112">For information, see [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span></span>
* <span data-ttu-id="497f2-113">如果您的組織使用 Proxy 伺服器來連線至網際網路，請參閱[使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md)，以取得如何設定伺服器的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="497f2-113">If your organization uses proxy servers to connect to the internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how to configure them.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="497f2-114">開啟您的連接埠</span><span class="sxs-lookup"><span data-stu-id="497f2-114">Open your ports</span></span>

<span data-ttu-id="497f2-115">若要準備適合 Azure AD 應用程式 Proxy 的環境，您需要先啟用 Azure 資料中心的通訊。</span><span class="sxs-lookup"><span data-stu-id="497f2-115">To prepare your environment for Azure AD Application Proxy, you first need to enable communication to Azure data centers.</span></span> <span data-ttu-id="497f2-116">如果路徑中有防火牆，請確定防火牆已開啟，以便連接器可以對應用程式 Proxy 提出 HTTPS (TCP) 要求。</span><span class="sxs-lookup"><span data-stu-id="497f2-116">If there is a firewall in the path, make sure that it's open so that the Connector can make HTTPS (TCP) requests to the Application Proxy.</span></span>

1. <span data-ttu-id="497f2-117">開啟下列連接埠以**輸出**流量：</span><span class="sxs-lookup"><span data-stu-id="497f2-117">Open the following ports to **outbound** traffic:</span></span>

   | <span data-ttu-id="497f2-118">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="497f2-118">Port number</span></span> | <span data-ttu-id="497f2-119">使用方式</span><span class="sxs-lookup"><span data-stu-id="497f2-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="497f2-120">80</span><span class="sxs-lookup"><span data-stu-id="497f2-120">80</span></span> | <span data-ttu-id="497f2-121">下載憑證撤銷清單 (CRL) 時驗證 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="497f2-121">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span></span> |
   | <span data-ttu-id="497f2-122">443</span><span class="sxs-lookup"><span data-stu-id="497f2-122">443</span></span> | <span data-ttu-id="497f2-123">應用程式 Proxy 服務的所有傳出通訊</span><span class="sxs-lookup"><span data-stu-id="497f2-123">All outbound communication with the Application Proxy service</span></span> |

   <span data-ttu-id="497f2-124">如果您的防火牆根據原始使用者強制執行流量，請針對來自當做網路服務執行的 Windows 服務的流量，開放這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="497f2-124">If your firewall enforces traffic according to originating users, open these ports for traffic coming from Windows services running as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="497f2-125">下表反映連接器 1.5.132.0 版及更新版本的連接埠需求。</span><span class="sxs-lookup"><span data-stu-id="497f2-125">The table reflects the port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="497f2-126">如果仍有舊版的連接器，您也需要啟用下列連接埠：5671、8080、9090、9091、9350、9352 和 10100–10120。</span><span class="sxs-lookup"><span data-stu-id="497f2-126">If you still have an older connector version, you also need to enable the following ports: 5671, 8080, 9090, 9091, 9350, 9352, and 10100–10120.</span></span>
   >
   ><span data-ttu-id="497f2-127">如需將連接器更新至最新版本的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md#automatic-updates)。</span><span class="sxs-lookup"><span data-stu-id="497f2-127">For information about updating your connectors to the newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="497f2-128">如果您的防火牆或 Proxy 允許建立 DNS 白名單，您可以建立 msappProxy.net 和 servicebus.windows.net 的白名單連線。</span><span class="sxs-lookup"><span data-stu-id="497f2-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections to msappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="497f2-129">如果不是，您需要允許對每週更新的 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)的存取。</span><span class="sxs-lookup"><span data-stu-id="497f2-129">If not, you need to allow access to the [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="497f2-130">請使用 [Azure AD 應用程式 Proxy 連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)，來確認您的連接器是否能夠連線到「應用程式 Proxy」服務。</span><span class="sxs-lookup"><span data-stu-id="497f2-130">Use the [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) to verify that your connector can reach the Application Proxy service.</span></span> <span data-ttu-id="497f2-131">至少，請確定「美國中部」區域及離您最近的區域都具有綠色勾選記號。</span><span class="sxs-lookup"><span data-stu-id="497f2-131">At a minimum, make sure that the Central US region and the region closest to you have all green checkmarks.</span></span> <span data-ttu-id="497f2-132">除此之外，綠色勾選記號越多代表恢復能力越佳。</span><span class="sxs-lookup"><span data-stu-id="497f2-132">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="enable-application-proxy-in-azure-ad"></a><span data-ttu-id="497f2-133">Azure AD 中啟用應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="497f2-133">Enable Application Proxy in Azure AD</span></span>
1. <span data-ttu-id="497f2-134">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，以系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="497f2-134">Sign in as an administrator in the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="497f2-135">移至 Active Directory，並選取您要啟用應用程式 Proxy 所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="497f2-135">Go to Active Directory and select the directory in which you want to enable Application Proxy.</span></span>

    ![Active Directory - 圖示](./media/active-directory-application-proxy-enable/ad_icon.png)
3. <span data-ttu-id="497f2-137">在目錄頁面上選取 [設定]，然後向下捲動至 [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="497f2-137">Select **Configure** from the directory page, and scroll down to **Application Proxy**.</span></span>
4. <span data-ttu-id="497f2-138">將 [啟用此目錄的應用程式 Proxy 服務] 切換為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="497f2-138">Toggle **Enable Application Proxy Services for this Directory** to **Enabled**.</span></span>

    ![啟用應用程式 Proxy](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. <span data-ttu-id="497f2-140">選取 [立即下載] 。</span><span class="sxs-lookup"><span data-stu-id="497f2-140">Select **Download now**.</span></span> <span data-ttu-id="497f2-141">[Azure AD 應用程式 Proxy 連接器下載] 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="497f2-141">The **Azure AD Application Proxy Connector Download** opens.</span></span> <span data-ttu-id="497f2-142">閱讀並接受授權條款，然後按一下 [下載]  以儲存連接器的 Windows Installer 檔案 (.exe)。</span><span class="sxs-lookup"><span data-stu-id="497f2-142">Read and accept the license terms and click **Download** to save the Windows Installer file (.exe) for the connector.</span></span>

## <a name="install-and-register-the-connector"></a><span data-ttu-id="497f2-143">安裝並註冊連接器</span><span class="sxs-lookup"><span data-stu-id="497f2-143">Install and register the Connector</span></span>
1. <span data-ttu-id="497f2-144">在您根據必要條件所準備好的伺服器上執行 **AADApplicationProxyConnectorInstaller.exe** 。</span><span class="sxs-lookup"><span data-stu-id="497f2-144">Run **AADApplicationProxyConnectorInstaller.exe** on the server you prepared according to the prerequisites.</span></span>
2. <span data-ttu-id="497f2-145">依照精靈中的指示進行安裝。</span><span class="sxs-lookup"><span data-stu-id="497f2-145">Follow the instructions in the wizard to install.</span></span>
3. <span data-ttu-id="497f2-146">在安裝期間，系統將提示您向 Azure AD 租用戶的應用程式 Proxy 註冊連接器。</span><span class="sxs-lookup"><span data-stu-id="497f2-146">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="497f2-147">提供您的 Azure AD 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="497f2-147">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="497f2-148">您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。</span><span class="sxs-lookup"><span data-stu-id="497f2-148">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="497f2-149">請確定註冊連接器的系統管理員與您啟用應用程式 Proxy 服務的位置在相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="497f2-149">Make sure the admin who registers the connector is in the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="497f2-150">例如，如果租用戶網域為 contoso.com，則系統管理員應該是 admin@contoso.com ，或該網域上的其他別名。</span><span class="sxs-lookup"><span data-stu-id="497f2-150">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="497f2-151">如果 [IE 增強式安全性設定] 在伺服器上設定為 [開啟]，可能會封鎖註冊畫面。</span><span class="sxs-lookup"><span data-stu-id="497f2-151">If **IE Enhanced Security Configuration** is set to **On** on the server, the registration screen might be blocked.</span></span> <span data-ttu-id="497f2-152">若要允許存取，請依照錯誤訊息中的指示。</span><span class="sxs-lookup"><span data-stu-id="497f2-152">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="497f2-153">請確定已停用 [Internet Explorer 增強式安全性]。</span><span class="sxs-lookup"><span data-stu-id="497f2-153">Make sure that Internet Explorer Enhanced Security is off.</span></span>
   * <span data-ttu-id="497f2-154">如果連接器註冊不成功，請參閱 [針對應用程式 Proxy 進行疑難排解](active-directory-application-proxy-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="497f2-154">If connector registration does not succeed, see [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md).</span></span>  
4. <span data-ttu-id="497f2-155">安裝完成後，會在您的伺服器中新增兩個新的服務：</span><span class="sxs-lookup"><span data-stu-id="497f2-155">When the installation completes, two new services are added to your server:</span></span>

   * <span data-ttu-id="497f2-156">**Microsoft AAD 應用程式 Proxy 連接器** 可啟用連線</span><span class="sxs-lookup"><span data-stu-id="497f2-156">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

     * <span data-ttu-id="497f2-157">**Microsoft AAD 應用程式 Proxy 連接器更新程式**是自動更新服務。</span><span class="sxs-lookup"><span data-stu-id="497f2-157">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="497f2-158">更新程式會檢查連接器的新版本，並且視需要更新連接器。</span><span class="sxs-lookup"><span data-stu-id="497f2-158">It periodically checks for new versions of the connector and updates the connector as needed.</span></span>

     ![應用程式 Proxy 連接器服務 - 螢幕擷取畫面](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. <span data-ttu-id="497f2-160">按一下安裝視窗中的 [完成]  。</span><span class="sxs-lookup"><span data-stu-id="497f2-160">Click **Finish** in the installation window.</span></span>

<span data-ttu-id="497f2-161">如需連接器的相關資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="497f2-161">For information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

<span data-ttu-id="497f2-162">為了實現高可用性，您應該至少部署兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="497f2-162">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="497f2-163">若要部署更多連接器，請重複步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="497f2-163">To deploy more connectors, repeat steps 2 and 3.</span></span> <span data-ttu-id="497f2-164">每個連接器都必須分別進行註冊。</span><span class="sxs-lookup"><span data-stu-id="497f2-164">Each connector must be registered separately.</span></span>

<span data-ttu-id="497f2-165">如果您想要解除安裝連接器，請解除安裝連接器服務和更新程式服務。</span><span class="sxs-lookup"><span data-stu-id="497f2-165">If you want to uninstall the Connector, uninstall both the Connector service and the Updater service.</span></span> <span data-ttu-id="497f2-166">重新啟動電腦，才能完全移除此服務。</span><span class="sxs-lookup"><span data-stu-id="497f2-166">Restart your computer to fully remove the service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="497f2-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="497f2-167">Next steps</span></span>
<span data-ttu-id="497f2-168">您現在已經準備好 [使用應用程式 Proxy 發佈應用程式](active-directory-application-proxy-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="497f2-168">You are now ready to [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

<span data-ttu-id="497f2-169">如果您有位於不同網路或不同位置上的應用程式，您可以使用連接器群組將不同的連接器組織成邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="497f2-169">If you have applications that are on separate networks or different locations, you can use connector groups to organize the different connectors into logical units.</span></span> <span data-ttu-id="497f2-170">深入了解 [使用應用程式 Proxy 連接器](active-directory-application-proxy-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="497f2-170">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors.md).</span></span>
