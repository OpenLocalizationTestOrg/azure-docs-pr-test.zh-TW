---
title: "Azure AD 應用程式 Proxy 中的自訂網域 | Microsoft Docs"
description: "管理 Azure AD 應用程式 Proxy 中的自訂網域，讓不論使用者從何處存取都能看到相同的應用程式 URL。"
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="1cfd2-103">使用 Azure AD 應用程式 Proxy 中的自訂網域</span><span class="sxs-lookup"><span data-stu-id="1cfd2-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="1cfd2-104">當您透過 Azure Active Directory 應用程式 Proxy 發佈應用程式時，您會建立可供使用者在遠端工作時移至的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="1cfd2-105">此 URL 會取得預設網域 *yourtenant.msappproxy.net*。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="1cfd2-106">例如，如果您發佈一個名為 Expenses 的應用程式，且您的租用戶名為 Contoso，則外部 URL 會是 https://expenses-contoso.msappproxy.net。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="1cfd2-107">如果您想要使用自己的網域名稱，請為您的應用程式設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="1cfd2-108">建議您盡可能為應用程式設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="1cfd2-109">自訂網域的一些優點包括：</span><span class="sxs-lookup"><span data-stu-id="1cfd2-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="1cfd2-110">使用者可以透過相同的 URL 移至應用程式，不論他們是在網路內部或外部作業。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="1cfd2-111">如果所有應用程式有相同的內部和外部 URL，則某一個應用程式中指向另一個應用程式的連結會繼續在公司網路外部運作。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="1cfd2-112">您可控制您的品牌，並建立您想要的 URL。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="1cfd2-113">設定自訂網域</span><span class="sxs-lookup"><span data-stu-id="1cfd2-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1cfd2-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="1cfd2-114">Prerequisites</span></span>

<span data-ttu-id="1cfd2-115">設定自訂網域之前，請確定您已備妥下列需求：</span><span class="sxs-lookup"><span data-stu-id="1cfd2-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="1cfd2-116">[新增至 Azure Active Directory 的已驗證網域](active-directory-domains-add-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="1cfd2-117">網域的自訂憑證 (採用 PFX 檔格式)。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="1cfd2-118">[透過應用程式 Proxy 發佈](application-proxy-publish-azure-portal.md)的內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="1cfd2-119">設定自訂網域</span><span class="sxs-lookup"><span data-stu-id="1cfd2-119">Configure your custom domain</span></span>

<span data-ttu-id="1cfd2-120">當您備妥這三項需求時，請遵循下列步驟來設定自訂網域：</span><span class="sxs-lookup"><span data-stu-id="1cfd2-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="1cfd2-121">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1cfd2-122">瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式]，然後選擇您要管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="1cfd2-123">選取 [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="1cfd2-124">在 [外部 URL] 欄位中，使用下拉式清單來選取您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="1cfd2-125">如果您未在清單中看到您的網域，則它尚未經過驗證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="1cfd2-126">選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-126">Select **Save**</span></span>
5. <span data-ttu-id="1cfd2-127">已停用的 [憑證] 欄位會變成已啟用。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="1cfd2-128">選取此欄位。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-128">Select this field.</span></span> 

   ![按一下以上傳憑證](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="1cfd2-130">如果您已上傳此網域的憑證，則 [憑證] 欄位會顯示憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="1cfd2-131">上傳 PFX 憑證，然後輸入憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="1cfd2-132">選取 [儲存] 來儲存變更。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="1cfd2-133">新增 [DNS 記錄](../dns/dns-operations-recordsets-portal.md)，此記錄會將新的外部 URL 重新導向至 msappproxy.net 網域。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="1cfd2-134">您只需要針對每個自訂網域上傳一個憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="1cfd2-135">一旦上傳憑證，您即可在發佈新應用程式時選擇自訂網域，而不需要進行額外的設定 (DNS 記錄除外)。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="1cfd2-136">管理憑證</span><span class="sxs-lookup"><span data-stu-id="1cfd2-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="1cfd2-137">憑證格式</span><span class="sxs-lookup"><span data-stu-id="1cfd2-137">Certificate format</span></span>
<span data-ttu-id="1cfd2-138">憑證簽章方法沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="1cfd2-139">橢圓曲線密碼編譯 (ECC)、主體別名 (SAN) 和其他常見的憑證類型均可支援。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="1cfd2-140">只要萬用字元符合所需的外部 URL，便可使用萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="1cfd2-141">您也可以使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="1cfd2-142">如果您使用私人憑證授權單位，則憑證的 CDP (憑證撤銷點發佈點) 應是公開的。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="1cfd2-143">變更網域</span><span class="sxs-lookup"><span data-stu-id="1cfd2-143">Changing the domain</span></span>
<span data-ttu-id="1cfd2-144">所有已驗證的網域會出現在您應用程式的外部 URL 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="1cfd2-145">若要變更的網域，只要更新應用程式的該欄位。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="1cfd2-146">如果您想要的網域不在清單中，請[將它新增為已驗證的網域](active-directory-domains-add-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="1cfd2-147">如果您選取的網域還沒有相關聯的憑證，請遵循步驟 5-7 來新增憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="1cfd2-148">接著，務必更新 DNS 記錄以從新的外部 URL 重新導向。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="1cfd2-149">憑證管理</span><span class="sxs-lookup"><span data-stu-id="1cfd2-149">Certificate management</span></span>
<span data-ttu-id="1cfd2-150">除非應用程式共用外部主機，否則您可以將相同的憑證使用於多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="1cfd2-151">您會在憑證過期時收到警告，告知您透過入口網站上傳另一個憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="1cfd2-152">如果已撤銷憑證，使用者在存取應用程式時可能會看到安全性警告。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="1cfd2-153">我們不會執行憑證的撤銷檢查。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="1cfd2-154">若要更新指定應用程式的憑證，請巡覽至該應用程式並遵循步驟 5-7 以在已發佈的應用程式上設定自訂網域，進而上傳新的憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="1cfd2-155">如果其他應用程式並未使用舊憑證，則系統會自動將它刪除。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="1cfd2-156">目前所有憑證管理都是透過個別的應用程式頁面進行，所以您必須在相關應用程式的環境中管理憑證。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1cfd2-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1cfd2-157">Next steps</span></span>
* <span data-ttu-id="1cfd2-158">[啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)以登入您使用 Azure AD 驗證發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="1cfd2-159">[啟用條件式存取](active-directory-application-proxy-conditional-access.md)以存取您發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cfd2-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="1cfd2-160">將自訂網域名稱新增至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="1cfd2-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


