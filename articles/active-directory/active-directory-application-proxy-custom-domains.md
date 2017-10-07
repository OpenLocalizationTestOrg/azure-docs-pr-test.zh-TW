---
title: "在 Azure AD Application Proxy aaaCustom 網域 |Microsoft 文件"
description: "管理 Azure AD Application Proxy 中的自訂網域，所以 hello hello 應用程式 URL 是 hello 相同不論您的使用者存取的位置。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="eb7f3-103">使用 Azure AD 應用程式 Proxy 中的自訂網域</span><span class="sxs-lookup"><span data-stu-id="eb7f3-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="eb7f3-104">當您發行應用程式透過 Azure Active Directory 應用程式 Proxy 時，您會建立從遠端使用您的使用者 toogo toowhen 的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="eb7f3-105">此 URL 取得 hello 預設網域*yourtenant.msappproxy.net*。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="eb7f3-106">比方說，如果您發行應用程式名為費用，而且您的租用戶名為 Contoso，則 hello 外部 URL 將是 https://expenses-contoso.msappproxy.net。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="eb7f3-107">如果您想 toouse 您自己的網域名稱，請設定您的應用程式的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="eb7f3-108">建議您盡可能為應用程式設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="eb7f3-109">自訂網域的 hello 優點包括：</span><span class="sxs-lookup"><span data-stu-id="eb7f3-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="eb7f3-110">您的使用者可以取得 toohello 應用程式與 hello 相同的 URL，是否正在內部或外部網路。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="eb7f3-111">如果所有應用程式有 hello 相同的內部和外部 Url，一個應用程式中點 tooanother 的連結就會繼續 toowork 即使外部 hello 公司網路。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="eb7f3-112">您控制您的品牌，並建立您想要的 hello Url。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="eb7f3-113">設定自訂網域</span><span class="sxs-lookup"><span data-stu-id="eb7f3-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eb7f3-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="eb7f3-114">Prerequisites</span></span>

<span data-ttu-id="eb7f3-115">設定自訂網域之前，請確定您有下列需求已備妥的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb7f3-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="eb7f3-116">A[已驗證的網域加入 Active Directory tooAzure](active-directory-domains-add-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="eb7f3-117">Hello 網域，請在 PFX 檔案的 hello 表單自訂的憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="eb7f3-118">[透過應用程式 Proxy 發佈](application-proxy-publish-azure-portal.md)的內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="eb7f3-119">設定自訂網域</span><span class="sxs-lookup"><span data-stu-id="eb7f3-119">Configure your custom domain</span></span>

<span data-ttu-id="eb7f3-120">當您準備這些三個需求時，請遵循這些步驟 tooset，註冊您的自訂網域：</span><span class="sxs-lookup"><span data-stu-id="eb7f3-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="eb7f3-121">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="eb7f3-122">瀏覽過**Azure Active Directory** > **企業應用程式** > **所有應用程式**選擇 hello 應用程式想 toomanage。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="eb7f3-123">選取 [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="eb7f3-124">在 [hello 外部 URL] 欄位中，使用 hello 下拉式清單 tooselect 您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="eb7f3-125">如果您沒有看到 hello 清單中的網域，然後它尚未經過驗證尚未。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="eb7f3-126">選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-126">Select **Save**</span></span>
5. <span data-ttu-id="eb7f3-127">hello**憑證**已停用的欄位會變成啟用。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="eb7f3-128">選取此欄位。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-128">Select this field.</span></span> 

   ![按一下 tooupload 憑證](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="eb7f3-130">如果您已上傳此網域的憑證，憑證 [hello] 欄位會顯示 hello 憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="eb7f3-131">Hello PFX 憑證上傳，然後輸入 hello 憑證 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="eb7f3-132">選取**儲存**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="eb7f3-133">新增[DNS 記錄](../dns/dns-operations-recordsets-portal.md)重新導向 hello 新外部 URL toohello msappproxy.net 網域。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="eb7f3-134">您只需要每個自訂網域的 tooupload 一個憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="eb7f3-135">一旦您上傳憑證，您可以選擇 hello 自訂網域，當您發行新應用程式並沒有 toodo 除了 hello DNS 記錄的其他組態。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="eb7f3-136">管理憑證</span><span class="sxs-lookup"><span data-stu-id="eb7f3-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="eb7f3-137">憑證格式</span><span class="sxs-lookup"><span data-stu-id="eb7f3-137">Certificate format</span></span>
<span data-ttu-id="eb7f3-138">沒有任何限制 hello 憑證簽章方法上。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="eb7f3-139">橢圓曲線密碼編譯 (ECC)、主體別名 (SAN) 和其他常見的憑證類型均可支援。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="eb7f3-140">只要 hello 萬用字元比對所需的 hello 外部 URL，您可以使用萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="eb7f3-141">您也可以使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="eb7f3-142">如果您使用私人憑證授權單位，hello CDP （憑證撤銷點發佈點） hello 憑證應該是公用的。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="eb7f3-143">變更 hello 定義域</span><span class="sxs-lookup"><span data-stu-id="eb7f3-143">Changing hello domain</span></span>
<span data-ttu-id="eb7f3-144">所有已驗證的網域會出現在您的應用程式的 hello 外部 URL 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="eb7f3-145">toochange hello 網域中，只需欄位 hello 應用程式的更新。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="eb7f3-146">如果您想要的 hello 網域不在 hello 清單[將它新增為已驗證的網域](active-directory-domains-add-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="eb7f3-147">如果您選取的網域沒有相關聯的憑證，請依照下列步驟 5-7 tooadd hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="eb7f3-148">接著，請確認您已更新 hello DNS 記錄 tooredirect 從 hello 新的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="eb7f3-149">憑證管理</span><span class="sxs-lookup"><span data-stu-id="eb7f3-149">Certificate management</span></span>
<span data-ttu-id="eb7f3-150">您可以使用相同憑證的多個應用程式除非 hello 應用程式共用的外部主機的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="eb7f3-151">您會收到警告憑證過期時，告知您 tooupload 透過 hello 入口網站的另一個憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="eb7f3-152">如果 hello 憑證已撤銷，因為您的使用者存取 hello 應用程式時可能會看到安全性警告。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="eb7f3-153">我們不會執行憑證的撤銷檢查。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="eb7f3-154">tooupdate hello 憑證指定的應用程式中，瀏覽 toohello 應用程式，並遵循步驟 5-7 上發行的應用程式 tooupload 新的憑證設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="eb7f3-155">如果 hello 舊的憑證未由其他應用程式使用中，它會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="eb7f3-156">目前所有憑證管理都是透過個別的應用程式頁面，您需要 toomanage hello hello 相關應用程式內容中的憑證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eb7f3-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb7f3-157">Next steps</span></span>
* <span data-ttu-id="eb7f3-158">[啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)tooyour 發行應用程式與 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="eb7f3-159">[啟用條件式存取](active-directory-application-proxy-conditional-access.md)tooyour 已發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eb7f3-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="eb7f3-160">加入您的自訂網域名稱 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="eb7f3-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


