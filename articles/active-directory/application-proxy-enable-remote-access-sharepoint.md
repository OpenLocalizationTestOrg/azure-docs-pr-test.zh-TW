---
title: "使用 Azure AD Application Proxy aaaEnable 遠端存取 tooSharePoint |Microsoft 文件"
description: "涵蓋如何 hello 基本概念 toointegrate Azure AD Application Proxy 的內部部署 SharePoint 伺服器。"
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
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="db3d7-103">啟用與 Azure AD Application Proxy 的遠端存取 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="db3d7-103">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="db3d7-104">本文將討論如何 toointegrate Azure Active Directory (Azure AD) 應用程式 Proxy 的內部部署 SharePoint 伺服器。</span><span class="sxs-lookup"><span data-stu-id="db3d7-104">This article discusses how toointegrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="db3d7-105">將遠端存取 tooSharePoint tooenable 與 Azure AD Application Proxy，請遵循本文逐步解說中的 hello 章節。</span><span class="sxs-lookup"><span data-stu-id="db3d7-105">tooenable remote access tooSharePoint with Azure AD Application Proxy, follow hello sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db3d7-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="db3d7-106">Prerequisites</span></span>

<span data-ttu-id="db3d7-107">本文假設您的環境中已經有 SharePoint 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="db3d7-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="db3d7-108">此外，請考慮下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="db3d7-108">In addition, consider hello following prerequisites:</span></span>

* <span data-ttu-id="db3d7-109">SharePoint 包含 Kerberos 的原生支援。</span><span class="sxs-lookup"><span data-stu-id="db3d7-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="db3d7-110">因此，透過 Azure AD Application Proxy 從遠端存取內部網站的使用者可以假設的 toohave 單一登入 (SSO) 體驗。</span><span class="sxs-lookup"><span data-stu-id="db3d7-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume toohave a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="db3d7-111">您需要 toomake 一些組態變更 tooyour SharePoint 伺服器。</span><span class="sxs-lookup"><span data-stu-id="db3d7-111">You need toomake a few configuration changes tooyour SharePoint server.</span></span> <span data-ttu-id="db3d7-112">建議您使用預備環境。</span><span class="sxs-lookup"><span data-stu-id="db3d7-112">We recommend using a staging environment.</span></span> <span data-ttu-id="db3d7-113">如此一來，您可以做出更新 tooyour 首先，臨時伺服器，並再進行實際執行前先測試循環。</span><span class="sxs-lookup"><span data-stu-id="db3d7-113">This way, you can make updates tooyour staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="db3d7-114">我們假設您有已設定 SSL for SharePoint，因為我們需要 SSL hello 上的發行 URL。</span><span class="sxs-lookup"><span data-stu-id="db3d7-114">We assume that you have already set up SSL for SharePoint, because we require SSL on hello published URL.</span></span> <span data-ttu-id="db3d7-115">您需要啟用 SSL toohave tooensure 連結傳送/對應的正確內部網站。</span><span class="sxs-lookup"><span data-stu-id="db3d7-115">You need toohave SSL enabled on your internal site, tooensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="db3d7-116">如果您尚未設定 SSL，請參閱[設定 SharePoint 2013 的 SSL](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) 以取得相關指示。</span><span class="sxs-lookup"><span data-stu-id="db3d7-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="db3d7-117">此外，請確定該 hello 連接器電腦信任 hello 憑證所發出。</span><span class="sxs-lookup"><span data-stu-id="db3d7-117">Also, make sure that hello connector machine trusts hello certificate that you issue.</span></span> <span data-ttu-id="db3d7-118">（hello 憑證不需要公開發出 toobe）。</span><span class="sxs-lookup"><span data-stu-id="db3d7-118">(hello certificate does not need toobe publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a><span data-ttu-id="db3d7-119">步驟 1： 設定單一登入 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="db3d7-119">Step 1: Set up single sign-on tooSharePoint</span></span>

<span data-ttu-id="db3d7-120">我們的客戶想的 hello 最佳 SSO 的體驗的後端應用程式中，SharePoint 伺服器在此情況下。</span><span class="sxs-lookup"><span data-stu-id="db3d7-120">Our customers want hello best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="db3d7-121">在這個常見的 Azure AD 案例，hello 驗證使用者一次，因為它們不會進行一次驗證提示。</span><span class="sxs-lookup"><span data-stu-id="db3d7-121">In this common Azure AD scenario, hello user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="db3d7-122">對於需要或不使用 Windows 驗證的內部部署應用程式，您可以使用 hello Kerberos 驗證通訊協定和名為 Kerberos 限制委派 (KCD) 的功能，以達到 SSO。</span><span class="sxs-lookup"><span data-stu-id="db3d7-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using hello Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="db3d7-123">KCD 設定時，可以讓 hello 應用程式 Proxy 連接器 tooobtain windows 票證/權杖的使用者，即使 hello 使用者尚未直接登入 tooWindows。</span><span class="sxs-lookup"><span data-stu-id="db3d7-123">KCD, when configured, allows hello Application Proxy connector tooobtain a windows ticket/token for a user, even if hello user hasn’t signed in tooWindows directly.</span></span> <span data-ttu-id="db3d7-124">toolearn 深入了解 KCD，請參閱[Kerberos 限制委派概觀](https://technet.microsoft.com/library/jj553400.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db3d7-124">toolearn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="db3d7-125">for SharePoint 伺服器，使用 hello 程序，在下列各節循序 hello 向上 KCD tooset:</span><span class="sxs-lookup"><span data-stu-id="db3d7-125">tooset up KCD for a SharePoint server, use hello procedures in hello following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="db3d7-126">確定 SharePoint 是在服務帳戶下執行</span><span class="sxs-lookup"><span data-stu-id="db3d7-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="db3d7-127">首先，確定 SharePoint 是在定義的服務帳戶下執行，而不是本機系統、本機服務或網路服務帳戶下。</span><span class="sxs-lookup"><span data-stu-id="db3d7-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="db3d7-128">如此您就可以附加服務主要名稱 (Spn) tooa 有效的帳戶，請執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="db3d7-128">Do this so that you can attach service principal names (SPNs) tooa valid account.</span></span> <span data-ttu-id="db3d7-129">Spn 是 hello Kerberos 通訊協定如何識別不同的服務。</span><span class="sxs-lookup"><span data-stu-id="db3d7-129">SPNs are how hello Kerberos protocol identifies different services.</span></span> <span data-ttu-id="db3d7-130">您將需要 hello 帳戶和更新版本 tooconfigure hello KCD。</span><span class="sxs-lookup"><span data-stu-id="db3d7-130">And you will need hello account later tooconfigure hello KCD.</span></span>

<span data-ttu-id="db3d7-131">tooensure 定義的服務帳戶下執行您的站台執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="db3d7-131">tooensure that your sites are running under a defined service account, perform hello following steps:</span></span>

1. <span data-ttu-id="db3d7-132">開啟 hello **SharePoint 2013 管理中心內**站台。</span><span class="sxs-lookup"><span data-stu-id="db3d7-132">Open hello **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="db3d7-133">跳過**安全性**選取**設定服務帳戶**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-133">Go too**Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="db3d7-134">選取 [Web 應用程式集區 - SharePoint - 80]。</span><span class="sxs-lookup"><span data-stu-id="db3d7-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="db3d7-135">hello 選項可能稍有不同根據 hello 名稱的 web 集區，或如果 hello web 集區預設會使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="db3d7-135">hello options may be slightly different based on hello name of your web pool, or if hello web pool uses SSL by default.</span></span>

  ![設定服務帳戶的選項](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="db3d7-137">如果**選取帳戶，此元件**是**本機服務**或**Network Service**，您需要 toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need toocreate an account.</span></span> <span data-ttu-id="db3d7-138">如果沒有，您完成時，可以移 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="db3d7-138">If not, you're finished and can move toohello next section.</span></span>
5. <span data-ttu-id="db3d7-139">選取 [註冊新的受管理帳戶]。</span><span class="sxs-lookup"><span data-stu-id="db3d7-139">Select **Register new managed account**.</span></span> <span data-ttu-id="db3d7-140">建立您的帳戶之後，您必須設定**Web 應用程式集區**才能夠使用 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-140">After your account is created, you must set **Web Application Pool** before you can use hello account.</span></span>

> [!NOTE]
<span data-ttu-id="db3d7-141">您需要的先前 toohave 建立 hello 服務的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-141">You need toohave a previously created Azure AD account for hello service.</span></span> <span data-ttu-id="db3d7-142">建議您允許密碼自動變更。</span><span class="sxs-lookup"><span data-stu-id="db3d7-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="db3d7-143">步驟和疑難排解問題的 hello 完整集的相關資訊，請參閱[SharePoint 2013 中設定自動密碼變更](https://technet.microsoft.com/library/ff724280.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db3d7-143">For more information about hello full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="db3d7-144">設定 SharePoint 的 Kerberos</span><span class="sxs-lookup"><span data-stu-id="db3d7-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="db3d7-145">使用 KCD tooperform 單一登入 toohello SharePoint 伺服器，這只適用於 Kerberos。</span><span class="sxs-lookup"><span data-stu-id="db3d7-145">You use KCD tooperform single sign-on toohello SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="db3d7-146">tooconfigure SharePoint 網站的 Kerberos 驗證：</span><span class="sxs-lookup"><span data-stu-id="db3d7-146">tooconfigure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="db3d7-147">開啟 hello **SharePoint 2013 管理中心內**站台。</span><span class="sxs-lookup"><span data-stu-id="db3d7-147">Open hello **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="db3d7-148">跳過**應用程式管理**，選取**管理 web 應用程式**，然後選取您的 SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="db3d7-148">Go too**Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="db3d7-149">在此範例中為 **SharePoint - 80**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-149">In this example, it is **SharePoint - 80**.</span></span>

  ![選取 hello SharePoint 網站](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="db3d7-151">按一下**驗證提供者**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="db3d7-151">Click **Authentication Providers** on hello toolbar.</span></span>
4. <span data-ttu-id="db3d7-152">在 hello**驗證提供者**方塊中，按一下**預設區域**tooview hello 設定。</span><span class="sxs-lookup"><span data-stu-id="db3d7-152">In hello **Authentication Providers** box, click **Default Zone** tooview hello settings.</span></span>
5. <span data-ttu-id="db3d7-153">在 hello**編輯驗證**對話方塊方塊中，向下捲動直到您看到**宣告驗證類型**，並確定兩者**啟用 Windows 驗證**和**整合式 Windows 驗證**已選取。</span><span class="sxs-lookup"><span data-stu-id="db3d7-153">In hello **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="db3d7-154">在 [hello] 下拉式清單方塊中，確定**交涉 (Kerberos)**已選取。</span><span class="sxs-lookup"><span data-stu-id="db3d7-154">In hello drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![編輯 [驗證] 對話方塊](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="db3d7-156">在 hello 底部 hello**編輯驗證**對話方塊中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-156">At hello bottom of hello **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a><span data-ttu-id="db3d7-157">設定 hello SharePoint 服務帳戶的服務主體名稱</span><span class="sxs-lookup"><span data-stu-id="db3d7-157">Set a service principal name for hello SharePoint service account</span></span>

<span data-ttu-id="db3d7-158">Hello KCD 設定之前，您需要以 hello 您已設定的服務帳戶執行 tooidentify hello SharePoint 服務。</span><span class="sxs-lookup"><span data-stu-id="db3d7-158">Before you configure hello KCD, you need tooidentify hello SharePoint service running as hello service account that you've configured.</span></span> <span data-ttu-id="db3d7-159">您可以透過設定 SPN 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="db3d7-159">You do this by setting an SPN.</span></span> <span data-ttu-id="db3d7-160">如需詳細資訊，請參閱[服務主體名稱](https://technet.microsoft.com/library/cc961723.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db3d7-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="db3d7-161">hello SPN 格式如下：</span><span class="sxs-lookup"><span data-stu-id="db3d7-161">hello SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="db3d7-162">Hello SPN 格式：</span><span class="sxs-lookup"><span data-stu-id="db3d7-162">In hello SPN format:</span></span>

* <span data-ttu-id="db3d7-163">_服務類別_是 hello 服務的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="db3d7-163">_service class_ is a unique name for hello service.</span></span> <span data-ttu-id="db3d7-164">針對 SharePoint，您會使用 **HTTP**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="db3d7-165">_主機_hello 完整的網域或 NetBIOS 名稱 hello 主控件以 hello 服務上執行。</span><span class="sxs-lookup"><span data-stu-id="db3d7-165">_host_ is hello fully qualified domain or NetBIOS name of hello host that hello service is running on.</span></span> <span data-ttu-id="db3d7-166">對於 SharePoint 網站，此文字可能需要 toobe hello 網站的 URL hello，視您正在使用的 IIS hello 版本而定。</span><span class="sxs-lookup"><span data-stu-id="db3d7-166">For a SharePoint site, this text might need toobe hello URL of hello site, depending on hello version of IIS that you're using.</span></span>

* <span data-ttu-id="db3d7-167">port 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="db3d7-167">_port_ is optional.</span></span>

<span data-ttu-id="db3d7-168">如果是 hello hello SharePoint 伺服器的 FQDN:</span><span class="sxs-lookup"><span data-stu-id="db3d7-168">If hello FQDN of hello SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="db3d7-169">然後是 hello SPN:</span><span class="sxs-lookup"><span data-stu-id="db3d7-169">Then hello SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="db3d7-170">您可能也需要 tooset Spn 特定網站的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="db3d7-170">You might also need tooset SPNs for specific sites on your server.</span></span> <span data-ttu-id="db3d7-171">如需詳細資訊，請參閱[設定 Kerberos 驗證](https://technet.microsoft.com/library/cc263449(v=office.12).aspx)。</span><span class="sxs-lookup"><span data-stu-id="db3d7-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="db3d7-172">特別注意 toohello 區段 」 建立服務主體使用 Kerberos 驗證的 Web 應用程式的名稱 」。</span><span class="sxs-lookup"><span data-stu-id="db3d7-172">Pay close attention toohello section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="db3d7-173">hello tooset Spn 的最簡單的方式是 toofollow hello 的 SPN 格式可能已經存在您的網站。</span><span class="sxs-lookup"><span data-stu-id="db3d7-173">hello easiest way for you tooset SPNs is toofollow hello SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="db3d7-174">複製針對 hello 服務帳戶的 Spn tooregister。</span><span class="sxs-lookup"><span data-stu-id="db3d7-174">Copy those SPNs tooregister against hello service account.</span></span> <span data-ttu-id="db3d7-175">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="db3d7-175">toodo this:</span></span>

1. <span data-ttu-id="db3d7-176">瀏覽 toohello 站台，以從另一部電腦的 hello SPN。</span><span class="sxs-lookup"><span data-stu-id="db3d7-176">Browse toohello site with hello SPN from another machine.</span></span>
 <span data-ttu-id="db3d7-177">當您執行動作，hello 組相關的 Kerberos 票證會快取 hello 機器上。</span><span class="sxs-lookup"><span data-stu-id="db3d7-177">When you do, hello relevant set of Kerberos tickets is cached on hello machine.</span></span> <span data-ttu-id="db3d7-178">這些票證包含 hello hello 您瀏覽至的目標網站的 SPN。</span><span class="sxs-lookup"><span data-stu-id="db3d7-178">These tickets contain hello SPN of hello target site that you browsed to.</span></span>

2. <span data-ttu-id="db3d7-179">您可以使用一個工具，稱為提取 hello SPN 該站台[Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html)。</span><span class="sxs-lookup"><span data-stu-id="db3d7-179">You can pull hello SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="db3d7-180">在命令視窗中執行 hello hello 使用者身分存取的 hello 站台在 hello 瀏覽器中執行的相同內容 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="db3d7-180">In a command window that's running in hello same context as hello user who accessed hello site in hello browser, run hello following command:</span></span>
```
Klist
```
<span data-ttu-id="db3d7-181">Klist 則會傳回目標 Spn 的 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="db3d7-181">Klist then returns hello set of target SPNs.</span></span> <span data-ttu-id="db3d7-182">在此範例中，反白顯示 hello 值為 hello 所需的 SPN:</span><span class="sxs-lookup"><span data-stu-id="db3d7-182">In this example, hello highlighted value is hello SPN that's needed:</span></span>

  ![範例 Klist 結果](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="db3d7-184">有 hello SPN 之後，您會需要 toomake 確認它已正確設定 hello 您稍早 hello web 應用程式設定的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-184">Now that you have hello SPN, you need toomake sure that it's configured correctly on hello service account that you set up for hello web application earlier.</span></span> <span data-ttu-id="db3d7-185">執行下列命令從 hello 命令提示字元，hello 網域的系統管理員身分的 hello:</span><span class="sxs-lookup"><span data-stu-id="db3d7-185">Run hello following command from hello command prompt as an administrator of hello domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="db3d7-186">此命令集 hello SPN hello SharePoint 服務帳戶身分執行_demo\sp_svc_。</span><span class="sxs-lookup"><span data-stu-id="db3d7-186">This command sets hello SPN for hello SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="db3d7-187">取代_http/sharepoint.demo.o365identity.us_以 hello SPN 為您的伺服器和_demo\sp_svc_與您的環境中的 hello 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-187">Replace _http/sharepoint.demo.o365identity.us_ with hello SPN for your server and _demo\sp_svc_ with hello service account in your environment.</span></span> <span data-ttu-id="db3d7-188">hello Setspn hello 再增加其 SPN 的命令搜尋。</span><span class="sxs-lookup"><span data-stu-id="db3d7-188">hello Setspn command searches for hello SPN before it adds it.</span></span> <span data-ttu-id="db3d7-189">在此情況下，您可能會看到 **SPN 值重複**錯誤。</span><span class="sxs-lookup"><span data-stu-id="db3d7-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="db3d7-190">如果您看到此錯誤，請確定 hello 值為 hello 服務帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="db3d7-190">If you see this error, make sure that hello value is associated with hello service account.</span></span>

<span data-ttu-id="db3d7-191">您可以確認該 hello 與 hello-l 選項執行 hello Setspn 命令加入 SPN。</span><span class="sxs-lookup"><span data-stu-id="db3d7-191">You can verify that hello SPN was added by running hello Setspn command with hello -l option.</span></span> <span data-ttu-id="db3d7-192">toolearn 進一步了解此命令，請參閱[Setspn](https://technet.microsoft.com/library/cc731241.aspx)。</span><span class="sxs-lookup"><span data-stu-id="db3d7-192">toolearn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a><span data-ttu-id="db3d7-193">請確定該 hello 連接器設定為受信任的委派 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="db3d7-193">Ensure that hello connector is set as a trusted delegate tooSharePoint</span></span>

<span data-ttu-id="db3d7-194">設定 hello KCD 讓 hello Azure AD Application Proxy 服務可以委派使用者識別 toohello SharePoint 服務。</span><span class="sxs-lookup"><span data-stu-id="db3d7-194">Configure hello KCD so that hello Azure AD Application Proxy service can delegate user identities toohello SharePoint service.</span></span> <span data-ttu-id="db3d7-195">您可以啟用 hello 應用程式 Proxy 連接器 tooretrieve Kerberos 票證為您在 Azure AD 中已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="db3d7-195">You do this by enabling hello Application Proxy connector tooretrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="db3d7-196">然後該伺服器在此情況下傳遞 hello 內容 toohello 目標應用程式或 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="db3d7-196">Then that server passes hello context toohello target application, or SharePoint in this case.</span></span>

<span data-ttu-id="db3d7-197">tooconfigure 的 hello KCD，重複步驟，針對每個連接器機器的 hello:</span><span class="sxs-lookup"><span data-stu-id="db3d7-197">tooconfigure hello KCD, repeat hello following steps for each connector machine:</span></span>

1. <span data-ttu-id="db3d7-198">以網域系統管理員 tooa DC，登入，然後開啟**Active Directory 使用者和電腦**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-198">Log in as a domain administrator tooa DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="db3d7-199">尋找 hello hello 連接器的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="db3d7-199">Find hello computer that hello connector is running on.</span></span> <span data-ttu-id="db3d7-200">在此範例中，它具有 hello 相同 SharePoint 伺服器。</span><span class="sxs-lookup"><span data-stu-id="db3d7-200">In this example, it's hello same SharePoint server.</span></span>
3. <span data-ttu-id="db3d7-201">按兩下 hello 電腦，然後按一下hello**委派** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="db3d7-201">Double-click hello computer, and then click hello **Delegation** tab.</span></span>
4. <span data-ttu-id="db3d7-202">確定 hello 委派設定已設定太**信任這台電腦所委派 toohello 指定僅限服務**，然後選取**使用任何驗證通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-202">Ensure that hello delegation settings are set too**Trust this computer for delegation toohello specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![委派設定](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="db3d7-204">按一下 hello**新增**按鈕，再按一下**使用者或電腦**，並找出 hello 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-204">Click hello **Add** button, click **Users or Computers**, and locate hello service account.</span></span>

  ![新增 hello SPN hello 服務帳戶](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="db3d7-206">在 hello Spn 的清單，選取您稍早建立 hello 服務帳戶的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="db3d7-206">In hello list of SPNs, select hello one that you created earlier for hello service account.</span></span>
7. <span data-ttu-id="db3d7-207">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="db3d7-207">Click **OK**.</span></span> <span data-ttu-id="db3d7-208">按一下**確定**再次 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="db3d7-208">Click **OK** again toosave hello changes.</span></span>

## <a name="step-2-enable-remote-access-toosharepoint"></a><span data-ttu-id="db3d7-209">步驟 2： 啟用遠端存取 tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="db3d7-209">Step 2: Enable remote access tooSharePoint</span></span>

<span data-ttu-id="db3d7-210">現在您已啟用 Kerberos 的 SharePoint，並設定 KCD，您已準備好設定單一登入 tooSharePoint tooset。</span><span class="sxs-lookup"><span data-stu-id="db3d7-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready tooset up single sign-on tooSharePoint.</span></span> <span data-ttu-id="db3d7-211">然後從 hello 連接器，您可以發佈 hello 經由 Azure AD Application Proxy 的遠端存取的 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="db3d7-211">Then from hello connector, you can publish hello SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="db3d7-212">tooperform hello 下列步驟，您需要 toobe 貴組織的 Azure Active Directory 帳戶中的 hello 全域管理員角色的成員。</span><span class="sxs-lookup"><span data-stu-id="db3d7-212">tooperform hello following steps, you need toobe a member of hello Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="db3d7-213">登入 toohello [Azure 入口網站](https://manage.windowsazure.com)並尋找您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="db3d7-213">Sign in toohello [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="db3d7-214">按一下 應用程式，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="db3d7-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="db3d7-215">選取 [發佈將可從您的網路外部存取的應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="db3d7-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="db3d7-216">如果您沒有看到此選項，請確定您有 Azure AD Basic 或 Premium hello 租用戶中設定。</span><span class="sxs-lookup"><span data-stu-id="db3d7-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in hello tenant.</span></span>
4. <span data-ttu-id="db3d7-217">完成每個 hello 選項，如下所示：</span><span class="sxs-lookup"><span data-stu-id="db3d7-217">Complete each of hello options as follows:</span></span>
 * <span data-ttu-id="db3d7-218">**名稱**︰使用任何您想要的值，例如 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="db3d7-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="db3d7-219">**內部 URL**： 這是 hello hello SharePoint 網站 URL 在內部，例如**https://SharePoint/**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-219">**Internal URL**: This is hello URL of hello SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="db3d7-220">在此範例中，請確定 toouse **https**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-220">In this example, make sure toouse **https**.</span></span>
 * <span data-ttu-id="db3d7-221">**預先驗證方法**︰選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="db3d7-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![用於新增應用程式的選項](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="db3d7-223">Hello 應用程式發行之後，按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="db3d7-223">After hello app is published, click hello **Configure** tab.</span></span>
6. <span data-ttu-id="db3d7-224">捲動 toohello 選項**標頭中的 轉譯 URL**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-224">Scroll down toohello option **Translate URL in Headers**.</span></span> <span data-ttu-id="db3d7-225">hello 預設值是**是**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-225">hello default value is **YES**.</span></span> <span data-ttu-id="db3d7-226">它也變更**否**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-226">Change it too**NO**.</span></span>

 <span data-ttu-id="db3d7-227">SharePoint 會使用 hello_主機標頭_值 toolook hello 站台。</span><span class="sxs-lookup"><span data-stu-id="db3d7-227">SharePoint uses hello _Host Header_ value toolook up hello site.</span></span> <span data-ttu-id="db3d7-228">它也會根據此值產生連結。</span><span class="sxs-lookup"><span data-stu-id="db3d7-228">It also generates links based on this value.</span></span> <span data-ttu-id="db3d7-229">hello 淨效果為 toomake 確定 SharePoint 會產生任何連結已正確設定 toouse hello 外部 URL 的已發行的 URL。</span><span class="sxs-lookup"><span data-stu-id="db3d7-229">hello net effect is toomake sure that any link that SharePoint generates is a published URL that is correctly set toouse hello external URL.</span></span> <span data-ttu-id="db3d7-230">將 hello 值設定為太**是**也可讓 hello 連接器 tooforward hello 要求 toohello 後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="db3d7-230">Setting hello value too**YES** also enables hello connector tooforward hello request toohello back-end application.</span></span> <span data-ttu-id="db3d7-231">不過，設定太 hello 值**否**hello 連接器的方法不會傳送 hello 內部主機名稱。</span><span class="sxs-lookup"><span data-stu-id="db3d7-231">However, setting hello value too**NO** means that hello connector will not send hello internal host name.</span></span> <span data-ttu-id="db3d7-232">相反地，hello 連接器會傳送 hello 主機標頭為 hello 發行 URL toohello 後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="db3d7-232">Instead, hello connector sends hello host header as hello published URL toohello back-end application.</span></span>

 <span data-ttu-id="db3d7-233">此外，tooensure SharePoint 接受此 URL，您需要 toocomplete hello SharePoint 伺服器上其他的設定。</span><span class="sxs-lookup"><span data-stu-id="db3d7-233">Also, tooensure that SharePoint accepts this URL, you need toocomplete one more configuration on hello SharePoint server.</span></span> <span data-ttu-id="db3d7-234">您要進行的 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="db3d7-234">You'll do that in hello next section.</span></span>

7. <span data-ttu-id="db3d7-235">變更**內部驗證方法**太**整合式 Windows 驗證**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-235">Change **Internal Authentication Method** too**Integrated Windows Authentication**.</span></span> <span data-ttu-id="db3d7-236">如果您的 Azure AD 租用戶會使用 UPN 不同 hello UPN 內部部署的 hello 雲端中，請記得 tooupdate**委派登入身分識別**以及。</span><span class="sxs-lookup"><span data-stu-id="db3d7-236">If your Azure AD tenant uses a UPN in hello cloud that's different from hello UPN on-premises, remember tooupdate **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="db3d7-237">設定**內部應用程式 SPN** toohello 您先前設定的值。</span><span class="sxs-lookup"><span data-stu-id="db3d7-237">Set **Internal Application SPN** toohello value that you set earlier.</span></span> <span data-ttu-id="db3d7-238">例如，使用 **http/sharepoint.demo.o365identity.us**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="db3d7-239">指派 hello 應用程式 tooyour 目標使用者。</span><span class="sxs-lookup"><span data-stu-id="db3d7-239">Assign hello application tooyour target users.</span></span>

<span data-ttu-id="db3d7-240">您的應用程式應該看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="db3d7-240">Your application should look similar toohello following example:</span></span>

  ![完成的應用程式](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a><span data-ttu-id="db3d7-242">步驟 3： 確定 SharePoint 知道 hello 外部 URL</span><span class="sxs-lookup"><span data-stu-id="db3d7-242">Step 3: Ensure that SharePoint knows about hello external URL</span></span>

<span data-ttu-id="db3d7-243">SharePoint 可以找到 hello hello 外部 URL 為基礎的站台，讓它將會根據該外部 URL 的連結呈現您最後一個步驟 tooensure。</span><span class="sxs-lookup"><span data-stu-id="db3d7-243">Your last step tooensure that SharePoint can find hello site based on hello external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="db3d7-244">您藉由設定備用存取對應 hello SharePoint 網站。</span><span class="sxs-lookup"><span data-stu-id="db3d7-244">You do this by configuring alternate access mappings for hello SharePoint site.</span></span>

1. <span data-ttu-id="db3d7-245">開啟 hello **SharePoint 2013 管理中心內**站台。</span><span class="sxs-lookup"><span data-stu-id="db3d7-245">Open hello **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="db3d7-246">在 [系統設定] 下，選取 [設定備用存取對應]。</span><span class="sxs-lookup"><span data-stu-id="db3d7-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="db3d7-247">這會開啟 hello**備用存取對應**方塊。</span><span class="sxs-lookup"><span data-stu-id="db3d7-247">This opens hello **Alternate Access Mappings** box.</span></span>

  ![[備用存取對應] 方塊](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="db3d7-249">在 [hello] 旁邊的下拉式清單中**備用存取對應集合**，選取**變更備用存取對應集合**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-249">In hello drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="db3d7-250">選取您的網站，例如 **SharePoint - 80**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![選取網站](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="db3d7-252">您可以選擇 tooadd hello 發行 URL 做為內部的 URL 或公用 URL。</span><span class="sxs-lookup"><span data-stu-id="db3d7-252">You can choose tooadd hello published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="db3d7-253">此範例使用 hello 外部網路的公用 URL。</span><span class="sxs-lookup"><span data-stu-id="db3d7-253">This example uses a public URL as hello extranet.</span></span>
6. <span data-ttu-id="db3d7-254">按一下**編輯公用 Url**在 hello**外部網路**路徑，然後輸入 hello hello 路徑發行應用程式中的，如同 hello 前一個步驟。</span><span class="sxs-lookup"><span data-stu-id="db3d7-254">Click **Edit Public URLs** in hello **Extranet** path, and then enter hello path for hello published application, as in hello previous step.</span></span> <span data-ttu-id="db3d7-255">例如，輸入 **https://sharepoint-iddemo.msappproxy.net**。</span><span class="sxs-lookup"><span data-stu-id="db3d7-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![輸入 hello 路徑](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="db3d7-257">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="db3d7-257">Click **Save**.</span></span>

 <span data-ttu-id="db3d7-258">您現在可以存取 hello SharePoint 網站，從外部透過 Azure AD Application Proxy。</span><span class="sxs-lookup"><span data-stu-id="db3d7-258">You can now access hello SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db3d7-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db3d7-259">Next steps</span></span>

- [<span data-ttu-id="db3d7-260">如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="db3d7-260">How tooprovide secure remote access tooon-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="db3d7-261">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="db3d7-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="db3d7-262">使用 Azure AD 應用程式 Proxy 發佈 SharePoint 2016 和 Office Online Server</span><span class="sxs-lookup"><span data-stu-id="db3d7-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
