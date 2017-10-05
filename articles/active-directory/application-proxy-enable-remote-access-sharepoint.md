---
title: "使用 Azure AD 應用程式 Proxy 啟用 SharePoint 的遠端存取 | Microsoft Docs"
description: "涵蓋如何整合內部部署 SharePoint 伺服器與 Azure AD 應用程式 Proxy 的基本概念。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="faf80-103">使用 Azure AD 應用程式 Proxy 啟用 SharePoint 的遠端存取</span><span class="sxs-lookup"><span data-stu-id="faf80-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="faf80-104">本文討論如何將內部部署 SharePoint 伺服器與 Azure Active Directory (Azure AD) 應用程式 Proxy 整合。</span><span class="sxs-lookup"><span data-stu-id="faf80-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="faf80-105">若要啟用使用 Azure AD 應用程式 Proxy 對 SharePoint 的遠端存取，請遵循本逐步解說文件中的各節。</span><span class="sxs-lookup"><span data-stu-id="faf80-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faf80-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="faf80-106">Prerequisites</span></span>

<span data-ttu-id="faf80-107">本文假設您的環境中已經有 SharePoint 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="faf80-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="faf80-108">此外，請考慮下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="faf80-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="faf80-109">SharePoint 包含 Kerberos 的原生支援。</span><span class="sxs-lookup"><span data-stu-id="faf80-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="faf80-110">因此，透過 Azure AD 應用程式 Proxy 遠端存取內部網站的使用者，應該可以有單一登入 (SSO) 體驗。</span><span class="sxs-lookup"><span data-stu-id="faf80-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="faf80-111">您必須對 SharePoint Server 進行一些設定變更。</span><span class="sxs-lookup"><span data-stu-id="faf80-111">You need to make a few configuration changes to your SharePoint server.</span></span> <span data-ttu-id="faf80-112">建議您使用預備環境。</span><span class="sxs-lookup"><span data-stu-id="faf80-112">We recommend using a staging environment.</span></span> <span data-ttu-id="faf80-113">如此一來，您可以先更新預備伺服器，以便在進行測試週期後再進入生產環境。</span><span class="sxs-lookup"><span data-stu-id="faf80-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="faf80-114">我們假設您已設定 SharePoint 的 SSL，因為已發佈的 URL 需要使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="faf80-114">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span></span> <span data-ttu-id="faf80-115">必須啟用內部網站的 SSL，才能確保可正確傳送/對應連結。</span><span class="sxs-lookup"><span data-stu-id="faf80-115">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="faf80-116">如果您尚未設定 SSL，請參閱[設定 SharePoint 2013 的 SSL](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) 以取得相關指示。</span><span class="sxs-lookup"><span data-stu-id="faf80-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="faf80-117">另外，請確定連接器電腦可信任您發出的憑證 </span><span class="sxs-lookup"><span data-stu-id="faf80-117">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="faf80-118">(此憑證不需公開發行。)</span><span class="sxs-lookup"><span data-stu-id="faf80-118">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="faf80-119">步驟 1︰設定 SharePoint 的單一登入</span><span class="sxs-lookup"><span data-stu-id="faf80-119">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="faf80-120">在此案例中，我們的客戶想要在後端應用程式 SharePoint Server 中享有最佳 SSO 體驗。</span><span class="sxs-lookup"><span data-stu-id="faf80-120">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="faf80-121">在這個常見的 Azure AD 案例中，使用者只需驗證一次，因為系統不會提示他們再次進行驗證。</span><span class="sxs-lookup"><span data-stu-id="faf80-121">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="faf80-122">對於需要或使用 Windows 驗證的內部部署應用程式來說，您可以使用 Kerberos 驗證通訊協定和稱為 Kerberos 限制委派 (KCD) 的功能來達成 SSO。</span><span class="sxs-lookup"><span data-stu-id="faf80-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="faf80-123">KCD 一經設定，即可讓應用程式 Proxy 連接器為使用者取得 Windows 票證/權杖，即使使用者並未直接登入 Windows 也是如此。</span><span class="sxs-lookup"><span data-stu-id="faf80-123">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="faf80-124">若要深入了解 KCD，請參閱 [Kerberos 限制委派概觀](https://technet.microsoft.com/library/jj553400.aspx)。</span><span class="sxs-lookup"><span data-stu-id="faf80-124">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="faf80-125">若要設定 SharePoint 伺服器的 KCD，請使用下列後續章節中的程序：</span><span class="sxs-lookup"><span data-stu-id="faf80-125">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="faf80-126">確定 SharePoint 是在服務帳戶下執行</span><span class="sxs-lookup"><span data-stu-id="faf80-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="faf80-127">首先，確定 SharePoint 是在定義的服務帳戶下執行，而不是本機系統、本機服務或網路服務帳戶下。</span><span class="sxs-lookup"><span data-stu-id="faf80-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="faf80-128">請務必確定這一點，您才可以將服務主體名稱 (SPN) 附加至有效的帳戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-128">Do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="faf80-129">SPN 是 Kerberos 通訊協定用來識別不同服務的方法。</span><span class="sxs-lookup"><span data-stu-id="faf80-129">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="faf80-130">稍候您需要使用該帳戶來設定 KCD。</span><span class="sxs-lookup"><span data-stu-id="faf80-130">And you will need the account later to configure the KCD.</span></span>

<span data-ttu-id="faf80-131">若要確定網站是根據所定義的服務帳戶來執行，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="faf80-131">To ensure that your sites are running under a defined service account, perform the following steps:</span></span>

1. <span data-ttu-id="faf80-132">開啟 [SharePoint 2013 管理中心] 網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-132">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="faf80-133">移至 [安全性]，然後選取 [設定服務帳戶]。</span><span class="sxs-lookup"><span data-stu-id="faf80-133">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="faf80-134">選取 [Web 應用程式集區 - SharePoint - 80]。</span><span class="sxs-lookup"><span data-stu-id="faf80-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="faf80-135">根據 Web 集區的名稱或是否 Web 集區預設使用 SSL，選項可能會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="faf80-135">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![設定服務帳戶的選項](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="faf80-137">如果 [選取此元件的帳戶] 是 [本機服務] 或 [網路服務]，則需要建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="faf80-138">若不是，則您已完成，可以進行下一節。</span><span class="sxs-lookup"><span data-stu-id="faf80-138">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="faf80-139">選取 [註冊新的受管理帳戶]。</span><span class="sxs-lookup"><span data-stu-id="faf80-139">Select **Register new managed account**.</span></span> <span data-ttu-id="faf80-140">帳戶建立之後，您必須設定 [Web 應用程式集區] 才能使用該帳戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-140">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

> [!NOTE]
<span data-ttu-id="faf80-141">您必須擁有先前為服務建立的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-141">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="faf80-142">建議您允許密碼自動變更。</span><span class="sxs-lookup"><span data-stu-id="faf80-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="faf80-143">如需完整的步驟和針對問題進行疑難排解的詳細資訊，請參閱[在 SharePoint 2013 中設定自動密碼變更](https://technet.microsoft.com/library/ff724280.aspx)。</span><span class="sxs-lookup"><span data-stu-id="faf80-143">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="faf80-144">設定 SharePoint 的 Kerberos</span><span class="sxs-lookup"><span data-stu-id="faf80-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="faf80-145">您會使用 KCD 來執行 SharePoint Server 的單一登入，而這只能搭配 Kerberos 來運作。</span><span class="sxs-lookup"><span data-stu-id="faf80-145">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="faf80-146">若要設定 SharePoint 網站的 Kerberos 驗證︰</span><span class="sxs-lookup"><span data-stu-id="faf80-146">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="faf80-147">開啟 [SharePoint 2013 管理中心] 網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-147">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="faf80-148">移至 [應用程式管理]，選取 [管理 Web 應用程式]，然後選取 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-148">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="faf80-149">在此範例中為 **SharePoint - 80**。</span><span class="sxs-lookup"><span data-stu-id="faf80-149">In this example, it is **SharePoint - 80**.</span></span>

  ![選取 SharePoint 網站](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="faf80-151">按一下工具列中的 [驗證提供者]。</span><span class="sxs-lookup"><span data-stu-id="faf80-151">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="faf80-152">在 [驗證提供者] 方塊中，按一下 [預設區域] 來檢視設定。</span><span class="sxs-lookup"><span data-stu-id="faf80-152">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="faf80-153">在 [編輯驗證] 對話方塊中，向下捲動直到您看到 [宣告驗證類型]，並確定已選取 [啟用 Windows 驗證] 和 [整合式 Windows 驗證]。</span><span class="sxs-lookup"><span data-stu-id="faf80-153">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="faf80-154">在下拉式清單方塊中，確定已選取 [交涉 (Kerberos)]。</span><span class="sxs-lookup"><span data-stu-id="faf80-154">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![編輯 [驗證] 對話方塊](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="faf80-156">在 [編輯驗證] 對話方塊的最下面，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="faf80-156">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="faf80-157">為 SharePoint 服務帳戶設定服務主體名稱</span><span class="sxs-lookup"><span data-stu-id="faf80-157">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="faf80-158">在設定 KCD 之前，您需要識別以上面所設定之服務帳戶身分執行的 SharePoint 服務。</span><span class="sxs-lookup"><span data-stu-id="faf80-158">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="faf80-159">您可以透過設定 SPN 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="faf80-159">You do this by setting an SPN.</span></span> <span data-ttu-id="faf80-160">如需詳細資訊，請參閱[服務主體名稱](https://technet.microsoft.com/library/cc961723.aspx)。</span><span class="sxs-lookup"><span data-stu-id="faf80-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="faf80-161">SPN 格式如下︰</span><span class="sxs-lookup"><span data-stu-id="faf80-161">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="faf80-162">在 SPN 格式中︰</span><span class="sxs-lookup"><span data-stu-id="faf80-162">In the SPN format:</span></span>

* <span data-ttu-id="faf80-163">service class 是服務的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="faf80-163">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="faf80-164">針對 SharePoint，您會使用 **HTTP**。</span><span class="sxs-lookup"><span data-stu-id="faf80-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="faf80-165">_host_ 是服務執行所在之主機的完整網域或 NetBIOS 名稱。</span><span class="sxs-lookup"><span data-stu-id="faf80-165">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="faf80-166">對於 SharePoint 網站，此文字可能必須是網站的 URL，視您使用的 IIS 版本而定。</span><span class="sxs-lookup"><span data-stu-id="faf80-166">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="faf80-167">port 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="faf80-167">_port_ is optional.</span></span>

<span data-ttu-id="faf80-168">如果 SharePoint Server 的 FQDN 是：</span><span class="sxs-lookup"><span data-stu-id="faf80-168">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="faf80-169">則 SPN 是︰</span><span class="sxs-lookup"><span data-stu-id="faf80-169">Then the SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="faf80-170">您可能也必須為伺服器上的特定網站設定 SPN。</span><span class="sxs-lookup"><span data-stu-id="faf80-170">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="faf80-171">如需詳細資訊，請參閱[設定 Kerberos 驗證](https://technet.microsoft.com/library/cc263449(v=office.12).aspx)。</span><span class="sxs-lookup"><span data-stu-id="faf80-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="faf80-172">密切注意＜使用 Kerberos 驗證為 Web 應用程式建立服務主體名稱＞一節。</span><span class="sxs-lookup"><span data-stu-id="faf80-172">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="faf80-173">設定 SPN 最簡單的方式是遵循網站上可能已存在的 SPN 格式。</span><span class="sxs-lookup"><span data-stu-id="faf80-173">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="faf80-174">複製這些 SPN 來對服務帳戶進行註冊。</span><span class="sxs-lookup"><span data-stu-id="faf80-174">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="faf80-175">作法：</span><span class="sxs-lookup"><span data-stu-id="faf80-175">To do this:</span></span>

1. <span data-ttu-id="faf80-176">從另一部電腦使用 SPN 瀏覽至此網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-176">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="faf80-177">當您這樣做時，系統會快取電腦上的一組相關 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="faf80-177">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="faf80-178">這些票證包含您所瀏覽之目標網站的 SPN。</span><span class="sxs-lookup"><span data-stu-id="faf80-178">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="faf80-179">您可以使用稱為 [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html) 的工具提取該網站的 SPN。</span><span class="sxs-lookup"><span data-stu-id="faf80-179">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="faf80-180">在執行於和瀏覽器中網站存取使用者相同之內容中的命令視窗中，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="faf80-180">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="faf80-181">然後 Klist 會傳回目標 SPN 的集合。</span><span class="sxs-lookup"><span data-stu-id="faf80-181">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="faf80-182">在此範例中，醒目提示的值即為所需的 SPN：</span><span class="sxs-lookup"><span data-stu-id="faf80-182">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![範例 Klist 結果](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="faf80-184">現在您已經有 SPN，接下來您必須確定，它已在稍早為 Web 應用程式所設定的服務帳戶上正確設定。</span><span class="sxs-lookup"><span data-stu-id="faf80-184">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="faf80-185">請以網域系統管理員身分從命令提示字元執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="faf80-185">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="faf80-186">此命令會為以 _demo\sp_svc_ 身分執行的 SharePoint 服務帳戶設定 SPN。</span><span class="sxs-lookup"><span data-stu-id="faf80-186">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="faf80-187">將 _http/sharepoint.demo.o365identity.us_ 取代為伺服器的 SPN，並將 _demo\sp_svc_ 取代為環境中的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-187">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="faf80-188">Setspn 命令會先搜尋 SPN 再予以新增。</span><span class="sxs-lookup"><span data-stu-id="faf80-188">The Setspn command searches for the SPN before it adds it.</span></span> <span data-ttu-id="faf80-189">在此情況下，您可能會看到 **SPN 值重複**錯誤。</span><span class="sxs-lookup"><span data-stu-id="faf80-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="faf80-190">如果您看到此錯誤，請確定值已與服務帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="faf80-190">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="faf80-191">您可以執行 Setspn 命令並搭配 -l 選項，來確認是否已新增 SPN。</span><span class="sxs-lookup"><span data-stu-id="faf80-191">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="faf80-192">若要深入了解此命令，請參閱 [Setspn](https://technet.microsoft.com/library/cc731241.aspx)。</span><span class="sxs-lookup"><span data-stu-id="faf80-192">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="faf80-193">確定已將連接器設定為 SharePoint 信任的委派</span><span class="sxs-lookup"><span data-stu-id="faf80-193">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="faf80-194">設定 KCD，讓 Azure AD 應用程式 Proxy 服務可以將使用者識別委派給 SharePoint 服務。</span><span class="sxs-lookup"><span data-stu-id="faf80-194">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="faf80-195">其作法是啟用應用程式 Proxy 連接器，以便為已在 Azure AD 中驗證的使用者擷取 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="faf80-195">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="faf80-196">然後該伺服器會將內容傳遞至目標應用程式，在此案例中即為 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="faf80-196">Then that server passes the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="faf80-197">若要設定 KCD，請針對每個連接器電腦重複下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="faf80-197">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="faf80-198">以網域系統管理員身分登入 DC，然後開啟 **Active Directory 使用者和電腦**。</span><span class="sxs-lookup"><span data-stu-id="faf80-198">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="faf80-199">尋找連接器執行所在的電腦。</span><span class="sxs-lookup"><span data-stu-id="faf80-199">Find the computer that the connector is running on.</span></span> <span data-ttu-id="faf80-200">在此範例中，它與 SharePoint 伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="faf80-200">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="faf80-201">按兩下該電腦，然後按一下 [委派] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="faf80-201">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="faf80-202">確定委派設定已設為 [只針對指定服務的委派信任這台電腦]，然後選取 [使用任何驗證通訊協定]。</span><span class="sxs-lookup"><span data-stu-id="faf80-202">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![委派設定](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="faf80-204">按一下 [新增] 按鈕，按一下 [使用者或電腦]，並找出服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![新增服務帳戶的 SPN](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="faf80-206">在 SPN 的清單中，選取您稍早針對服務帳戶建立的 SPN。</span><span class="sxs-lookup"><span data-stu-id="faf80-206">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="faf80-207">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="faf80-207">Click **OK**.</span></span> <span data-ttu-id="faf80-208">再按一下 [確定] 以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="faf80-208">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="faf80-209">步驟 2︰啟用 SharePoint 的遠端存取</span><span class="sxs-lookup"><span data-stu-id="faf80-209">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="faf80-210">現在您已啟用 SharePoint 的 Kerberos 並已設定 KCD，您已準備好可以設定 SharePoint 的單一登入。</span><span class="sxs-lookup"><span data-stu-id="faf80-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span></span> <span data-ttu-id="faf80-211">接下來，您可以從連接器發佈 SharePoint 伺服器陣列，以便透過 Azure AD 應用程式 Proxy 進行遠端存取。</span><span class="sxs-lookup"><span data-stu-id="faf80-211">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="faf80-212">若要執行下列步驟，您必須是貴組織 Azure Active Directory 帳戶內全域管理員角色的成員。</span><span class="sxs-lookup"><span data-stu-id="faf80-212">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="faf80-213">登入 [Azure 入口網站](https://manage.windowsazure.com)，並尋找您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="faf80-213">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="faf80-214">按一下 [應用程式]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="faf80-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="faf80-215">選取 [發佈將可從您的網路外部存取的應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="faf80-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="faf80-216">如果您沒看到這個選項，請確定您已在租用戶中設定了 Azure AD Basic 或 Premium。</span><span class="sxs-lookup"><span data-stu-id="faf80-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span></span>
4. <span data-ttu-id="faf80-217">完成每個選項，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="faf80-217">Complete each of the options as follows:</span></span>
 * <span data-ttu-id="faf80-218">**名稱**︰使用任何您想要的值，例如 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="faf80-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="faf80-219">**內部 URL**︰這是 SharePoint 網站的內部 URL，例如 **https://SharePoint/**。</span><span class="sxs-lookup"><span data-stu-id="faf80-219">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="faf80-220">在此範例中，請務必使用 **https**。</span><span class="sxs-lookup"><span data-stu-id="faf80-220">In this example, make sure to use **https**.</span></span>
 * <span data-ttu-id="faf80-221">**預先驗證方法**︰選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="faf80-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![用於新增應用程式的選項](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="faf80-223">應用程式發佈後，按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="faf80-223">After the app is published, click the **Configure** tab.</span></span>
6. <span data-ttu-id="faf80-224">向下捲動至 [轉譯標頭中的 URL] 選項。</span><span class="sxs-lookup"><span data-stu-id="faf80-224">Scroll down to the option **Translate URL in Headers**.</span></span> <span data-ttu-id="faf80-225">預設值為 [是]。</span><span class="sxs-lookup"><span data-stu-id="faf80-225">The default value is **YES**.</span></span> <span data-ttu-id="faf80-226">將它變更為 [否]。</span><span class="sxs-lookup"><span data-stu-id="faf80-226">Change it to **NO**.</span></span>

 <span data-ttu-id="faf80-227">SharePoint 會使用 [主機標頭] 值來查閱網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-227">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="faf80-228">它也會根據此值產生連結。</span><span class="sxs-lookup"><span data-stu-id="faf80-228">It also generates links based on this value.</span></span> <span data-ttu-id="faf80-229">最後的結果是可確保 SharePoint 所產生的任何連結，都是已正確設定為使用外部 URL 的已發佈 URL。</span><span class="sxs-lookup"><span data-stu-id="faf80-229">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="faf80-230">將值設定為 [是] 也可讓連接器將要求轉送至後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="faf80-230">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="faf80-231">不過，將值設定為 [否] 表示連接器不會傳送內部主機名稱。</span><span class="sxs-lookup"><span data-stu-id="faf80-231">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="faf80-232">相反地，連接器會傳送主機標頭作為對後端應用程式發佈的 URL。</span><span class="sxs-lookup"><span data-stu-id="faf80-232">Instead, the connector sends the host header as the published URL to the back-end application.</span></span>

 <span data-ttu-id="faf80-233">此外，若要確保 SharePoint 會接受此 URL，您必須於 SharePoint Server 上再完成一項設定。</span><span class="sxs-lookup"><span data-stu-id="faf80-233">Also, to ensure that SharePoint accepts this URL, you need to complete one more configuration on the SharePoint server.</span></span> <span data-ttu-id="faf80-234">您將在下一節中執行該動作。</span><span class="sxs-lookup"><span data-stu-id="faf80-234">You'll do that in the next section.</span></span>

7. <span data-ttu-id="faf80-235">將 [內部驗證方法] 變更為 [整合式 Windows 驗證]。</span><span class="sxs-lookup"><span data-stu-id="faf80-235">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span></span> <span data-ttu-id="faf80-236">如果 Azure AD 租用戶在雲端所使用的 UPN 不同於內部部署 UPN，請記得一併更新 [委派的登入識別]。</span><span class="sxs-lookup"><span data-stu-id="faf80-236">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="faf80-237">將**內部應用程式 SPN** 設定為您先前設定的值。</span><span class="sxs-lookup"><span data-stu-id="faf80-237">Set **Internal Application SPN** to the value that you set earlier.</span></span> <span data-ttu-id="faf80-238">例如，使用 **http/sharepoint.demo.o365identity.us**。</span><span class="sxs-lookup"><span data-stu-id="faf80-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="faf80-239">將應用程式指派給目標使用者。</span><span class="sxs-lookup"><span data-stu-id="faf80-239">Assign the application to your target users.</span></span>

<span data-ttu-id="faf80-240">您的應用程式看起來應該像下面範例：</span><span class="sxs-lookup"><span data-stu-id="faf80-240">Your application should look similar to the following example:</span></span>

  ![完成的應用程式](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="faf80-242">步驟 3︰確定 SharePoint 知道外部 URL</span><span class="sxs-lookup"><span data-stu-id="faf80-242">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="faf80-243">最後一個步驟是確定 SharePoint 可以根據外部 URL 找到網站，以便根據該外部 URL 轉譯連結。</span><span class="sxs-lookup"><span data-stu-id="faf80-243">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="faf80-244">其方法是設定 SharePoint 網站的備用存取對應。</span><span class="sxs-lookup"><span data-stu-id="faf80-244">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="faf80-245">開啟 [SharePoint 2013 管理中心] 網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-245">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="faf80-246">在 [系統設定] 下，選取 [設定備用存取對應]。</span><span class="sxs-lookup"><span data-stu-id="faf80-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="faf80-247">這會開啟 [備用存取對應] 方塊。</span><span class="sxs-lookup"><span data-stu-id="faf80-247">This opens the **Alternate Access Mappings** box.</span></span>

  ![[備用存取對應] 方塊](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="faf80-249">在 [備用存取對應集合] 旁的下拉式清單中，選取 [變更備用存取對應集合]。</span><span class="sxs-lookup"><span data-stu-id="faf80-249">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="faf80-250">選取您的網站，例如 **SharePoint - 80**。</span><span class="sxs-lookup"><span data-stu-id="faf80-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![選取網站](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="faf80-252">您可以選擇將已發佈的 URL 新增為內部 URL 或公用 URL。</span><span class="sxs-lookup"><span data-stu-id="faf80-252">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="faf80-253">本範例使用公用 URL 做為外部網路。</span><span class="sxs-lookup"><span data-stu-id="faf80-253">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="faf80-254">按一下 [外部網路] 路徑中的 [編輯公用 URL]，然後和上一個步驟一樣，輸入用於所發佈應用程式的路徑。</span><span class="sxs-lookup"><span data-stu-id="faf80-254">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span></span> <span data-ttu-id="faf80-255">例如，輸入 **https://sharepoint-iddemo.msappproxy.net**。</span><span class="sxs-lookup"><span data-stu-id="faf80-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![輸入路徑](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="faf80-257">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="faf80-257">Click **Save**.</span></span>

 <span data-ttu-id="faf80-258">您現在可以透過 Azure AD 應用程式 Proxy 從外部存取 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="faf80-258">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="faf80-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="faf80-259">Next steps</span></span>

- [<span data-ttu-id="faf80-260">如何為內部部署應用程式提供安全的遠端存取</span><span class="sxs-lookup"><span data-stu-id="faf80-260">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="faf80-261">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="faf80-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="faf80-262">使用 Azure AD 應用程式 Proxy 發佈 SharePoint 2016 和 Office Online Server</span><span class="sxs-lookup"><span data-stu-id="faf80-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
