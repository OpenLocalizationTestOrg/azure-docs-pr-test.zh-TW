---
title: "Azure Active Directory B2C︰使用自訂原則新增 ADFS 作為 SAML 識別提供者"
description: "如何 tooarticle ADFS 2016 使用 SAML 通訊協定和自訂原則設定"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="c942d-103">Azure Active Directory B2C︰使用自訂原則新增 ADFS 作為 SAML 識別提供者</span><span class="sxs-lookup"><span data-stu-id="c942d-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c942d-104">本文章向您示範如何 tooenable 登入使用者從 ADFS 帳戶透過 hello 使用[自訂原則](active-directory-b2c-overview-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="c942d-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c942d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="c942d-105">Prerequisites</span></span>

<span data-ttu-id="c942d-106">完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="c942d-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="c942d-107">這些步驟包括：</span><span class="sxs-lookup"><span data-stu-id="c942d-107">These steps include:</span></span>

1.  <span data-ttu-id="c942d-108">建立 ADFS 信賴憑證者信任。</span><span class="sxs-lookup"><span data-stu-id="c942d-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="c942d-109">加入 hello ADFS Relying Party Trust 憑證 tooAzure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="c942d-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="c942d-110">新增宣告提供者 tooa 原則。</span><span class="sxs-lookup"><span data-stu-id="c942d-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="c942d-111">註冊 hello ADFS 帳戶宣告提供者 tooa 使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="c942d-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="c942d-112">上傳 hello 原則 tooan Azure AD B2C 租用戶，並進行測試。</span><span class="sxs-lookup"><span data-stu-id="c942d-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="c942d-113">toocreate 的宣告感知信賴憑證者信任</span><span class="sxs-lookup"><span data-stu-id="c942d-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="c942d-114">toouse ADFS 中 Azure Active Directory (Azure AD) B2C 身分識別提供者，您需要 toocreate ADFS 信賴憑證者信任和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="c942d-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="c942d-115">tooadd 新的信賴憑證者合作對象 hello AD FS 管理嵌入式管理單元使用信任，然後手動設定 hello，執行下列程序，在同盟伺服器上的 hello。</span><span class="sxs-lookup"><span data-stu-id="c942d-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="c942d-116">中的成員資格**管理員**，或在 hello 本機電腦上同等 hello 最小必要的 toocomplete 此程序。</span><span class="sxs-lookup"><span data-stu-id="c942d-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="c942d-117">檢閱使用 hello 適當的帳戶詳細資料和群組成員資格[本機與網域預設群組](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="c942d-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="c942d-118">在 [伺服器管理員] 中按一下 [工具]，然後選取 [ADFS 管理]。</span><span class="sxs-lookup"><span data-stu-id="c942d-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="c942d-119">按一下 [新增信賴憑證者信任]。</span><span class="sxs-lookup"><span data-stu-id="c942d-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="c942d-120">![新增信賴憑證者信任](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="c942d-121">在 hello ** 褖畫惎**頁面上，選擇**宣告感知**按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="c942d-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="c942d-122">![在 [hello 歡迎使用] 頁面上選擇 [宣告感知](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="c942d-123">在 hello**選取資料來源**頁面上，按一下**手動輸入 hello 信賴憑證者的合作對象相關資料**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c942d-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="c942d-124">![輸入 hello 信賴憑證者相關資料](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="c942d-125">在 hello**指定顯示名稱**頁面上，輸入中的名稱**顯示名稱**下**備忘稿**輸入此信賴憑證者信任的描述，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="c942d-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="c942d-126">![指定顯示名稱和注意事項](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="c942d-127">選用。</span><span class="sxs-lookup"><span data-stu-id="c942d-127">Optional.</span></span> <span data-ttu-id="c942d-128">如果您有選擇性的權杖加密憑證，然後在 hello**設定憑證**頁面上，按一下**瀏覽**toolocate 您憑證檔案，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="c942d-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="c942d-129">![設定憑證](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="c942d-130">在 hello**設定 URL**頁面上，選取 hello**啟用 hello SAML 2.0 WebSSO 通訊協定的支援**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c942d-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="c942d-131">在下**信賴憑證者合作對象 SAML 2.0 SSO 服務 URL**，輸入此信賴憑證者信任，hello 安全性聲明標記語言 (SAML) 服務端點 URL，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c942d-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="c942d-132">Hello**信賴憑證者合作對象 SAML 2.0 SSO 服務 URL**，貼上 hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`。</span><span class="sxs-lookup"><span data-stu-id="c942d-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="c942d-133">{Tenant} 取代為您的租用戶名稱 (例如，contosob2c.onmicrosoft.com) 和 hello {原則} 取代為您擴充功能的原則名稱 (例如，B2C_1A_TrustFrameworkExtensions)。</span><span class="sxs-lookup"><span data-stu-id="c942d-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="c942d-134">hello 原則名稱為 hello 其中一個，在此情況下，它是繼承自 signup_or_signin 原則： `B2C_1A_TrustFrameworkExtensions`。</span><span class="sxs-lookup"><span data-stu-id="c942d-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="c942d-135">例如 hello URL 可能是： https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**。</span><span class="sxs-lookup"><span data-stu-id="c942d-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![信賴憑證者 SAML 2.0 SSO 服務 URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="c942d-137">在 hello**設定識別碼**頁面上，指定 hello 相同的 URL hello 先前步驟中，按一下**新增**tooadd 它們 toohello 清單，然後再按**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c942d-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="c942d-138">![信賴憑證者信任識別碼](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="c942d-139">在 hello**選擇的存取控制原則**選取原則，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="c942d-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="c942d-140">![選擇存取控制原則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="c942d-141">在 [hello**準備 tooAdd 信任**頁面上，檢閱 hello 設定，然後按一下**下一步]** toosave 您信賴憑證者信任資訊。</span><span class="sxs-lookup"><span data-stu-id="c942d-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="c942d-142">![儲存您的信賴憑證者信任資訊](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="c942d-143">在 [hello**完成**頁面上，按一下**關閉**，此動作會自動顯示 hello**編輯宣告規則**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c942d-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="c942d-144">![編輯宣告規則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="c942d-145">按一下 [新增規則] 。</span><span class="sxs-lookup"><span data-stu-id="c942d-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="c942d-146">![新增規則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="c942d-147">在 [宣告規則範本] 中，選取 [傳送 LDAP 屬性作為宣告]。</span><span class="sxs-lookup"><span data-stu-id="c942d-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="c942d-148">![選取傳送 LDAP 屬性作為宣告範本規則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="c942d-149">提供**宣告規則名稱**。</span><span class="sxs-lookup"><span data-stu-id="c942d-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="c942d-150">Hello**屬性存放區**選取**選取 Active Directory**新增 hello 下列宣告，然後按一下 **完成**和**確定**。</span><span class="sxs-lookup"><span data-stu-id="c942d-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="c942d-151">![設定規則屬性](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="c942d-152">在 伺服器管理員 中，選取**信賴憑證者信任**選取 hello 信賴憑證者信任您所建立，然後按一下 **屬性**。</span><span class="sxs-lookup"><span data-stu-id="c942d-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="c942d-153">![信賴憑證者編輯屬性](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="c942d-154">其中一個 hello 信賴憑證者的合作對象信任 （B2C 示範） 屬性] 視窗按一下**簽章**索引標籤上，按一下 [**新增**。</span><span class="sxs-lookup"><span data-stu-id="c942d-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="c942d-155">![設定簽章](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="c942d-156">新增簽章憑證 (.cert 檔案，不含私密金鑰)。</span><span class="sxs-lookup"><span data-stu-id="c942d-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![新增簽章憑證](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="c942d-158">在 [hello 信賴憑證者合作對象信任 （B2C 示範） 屬性] 視窗上按一下**進階**索引標籤，然後變更 hello**安全雜湊演算法**太**sha-1**，按一下**確定**.</span><span class="sxs-lookup"><span data-stu-id="c942d-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="c942d-159">![設定安全雜湊演算法 tooSHA 1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="c942d-160">新增 hello ADFS 帳戶應用程式金鑰 tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c942d-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="c942d-161">使用 ADFS 帳戶的同盟需要 ADFS 帳戶 tootrust Azure AD B2C 代表 hello 應用程式用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="c942d-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="c942d-162">您需要 toostore ADFS 憑證在 Azure AD B2C 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="c942d-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="c942d-163">移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構**</span><span class="sxs-lookup"><span data-stu-id="c942d-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="c942d-164">選取**原則機碼**tooview hello 金鑰用於您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="c942d-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="c942d-165">按一下 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="c942d-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="c942d-166">針對 [選項] 使用 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="c942d-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="c942d-167">針對 [名稱] 使用 `ADFSSamlCert`。</span><span class="sxs-lookup"><span data-stu-id="c942d-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="c942d-168">hello 前置詞`B2C_1A_`可能會自動加入。</span><span class="sxs-lookup"><span data-stu-id="c942d-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="c942d-169">在 hello 檔案上傳，* * 選取私密金鑰憑證.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="c942d-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="c942d-170">注意： 這個憑證 （含 hello 私密金鑰） 應該 hello 核發，會用於 hello ADFS 信賴憑證者的合作對象的同一個。</span><span class="sxs-lookup"><span data-stu-id="c942d-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="c942d-171">![上傳原則金鑰](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="c942d-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="c942d-172">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="c942d-172">Click **Create**</span></span>
8.  <span data-ttu-id="c942d-173">確認您已建立 hello 金鑰`B2C_1A_ADFSSamlCert`。</span><span class="sxs-lookup"><span data-stu-id="c942d-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="c942d-174">在擴充原則中新增宣告提供者</span><span class="sxs-lookup"><span data-stu-id="c942d-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="c942d-175">如果您希望使用者 toosign 使用 ADFS 帳戶，您會需要 toodefine ADFS 帳戶做為宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="c942d-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="c942d-176">換句話說，您需要 toospecify 與 Azure AD B2C 通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="c942d-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="c942d-177">hello 端點提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。</span><span class="sxs-lookup"><span data-stu-id="c942d-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="c942d-178">定義 ADFS 作為宣告提供者，方法是在擴充原則檔案中新增 `<ClaimsProvider>` 節點：</span><span class="sxs-lookup"><span data-stu-id="c942d-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="c942d-179">從您的工作目錄中開啟 hello 擴充原則檔 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="c942d-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="c942d-180">如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。</span><span class="sxs-lookup"><span data-stu-id="c942d-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="c942d-181">尋找 hello`<ClaimsProviders>`區段</span><span class="sxs-lookup"><span data-stu-id="c942d-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="c942d-182">加入下列 XML 程式碼片段在 hello hello`ClaimsProviders`項目和取代`identityProvider`DNS （任意值，指出您的網域），然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c942d-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="c942d-183">註冊 hello ADFS 帳戶宣告提供者 tooSign 註冊或登入使用者之旅</span><span class="sxs-lookup"><span data-stu-id="c942d-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="c942d-184">此時，hello 身分識別提供者已設定。</span><span class="sxs-lookup"><span data-stu-id="c942d-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="c942d-185">不過，它不是可在任何 hello sign-up/登入畫面。</span><span class="sxs-lookup"><span data-stu-id="c942d-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="c942d-186">現在您需要 tooadd hello ADFS 帳戶身分識別提供者 tooyour 使用者`SignUpOrSignIn`使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="c942d-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="c942d-187">toomake 它可用，我們建立的現有的範本使用者旅程重複。</span><span class="sxs-lookup"><span data-stu-id="c942d-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="c942d-188">然後，我們修改它使其包含 hello ADFS 身分識別提供者：</span><span class="sxs-lookup"><span data-stu-id="c942d-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="c942d-189">開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。</span><span class="sxs-lookup"><span data-stu-id="c942d-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="c942d-190">尋找 hello`<UserJourneys>`項目，並複製 hello 整個內容`<UserJourneys>`節點。</span><span class="sxs-lookup"><span data-stu-id="c942d-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="c942d-191">開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="c942d-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="c942d-192">如果 hello 項目不存在，請加入一個參考。</span><span class="sxs-lookup"><span data-stu-id="c942d-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="c942d-193">貼上 hello 整個內容`<UserJournesy>`您複製 hello 的子系的節點`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="c942d-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="c942d-194">顯示 hello 按鈕</span><span class="sxs-lookup"><span data-stu-id="c942d-194">Display hello button</span></span>
<span data-ttu-id="c942d-195">hello`<ClaimsProviderSelections>`項目會定義 hello 宣告提供者選擇的選項清單以及它們的順序。</span><span class="sxs-lookup"><span data-stu-id="c942d-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="c942d-196">`<ClaimsProviderSelection>`項目是 sign-up/登入頁面上的類似 tooan 身分識別提供者按鈕。</span><span class="sxs-lookup"><span data-stu-id="c942d-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="c942d-197">如果您將加入`<ClaimsProviderSelection>`ADFS 帳戶項目，新的按鈕顯示落在 hello 頁面上的使用者。</span><span class="sxs-lookup"><span data-stu-id="c942d-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="c942d-198">tooadd 這個項目：</span><span class="sxs-lookup"><span data-stu-id="c942d-198">tooadd this element:</span></span>

1.  <span data-ttu-id="c942d-199">尋找 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`hello 您複製的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="c942d-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="c942d-200">找出 hello`<OrchestrationStep>`包含的節點`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="c942d-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="c942d-201">在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="c942d-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="c942d-202">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="c942d-202">Link hello button tooan action</span></span>

<span data-ttu-id="c942d-203">既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。</span><span class="sxs-lookup"><span data-stu-id="c942d-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="c942d-204">hello 動作，在此情況下，為 Azure AD B2C toocommunicate 與 ADFS 帳戶 tooreceive 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c942d-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="c942d-205">連結 hello 按鈕 tooan 動作連結 hello 技術設定檔的 ADFS 帳戶宣告提供者：</span><span class="sxs-lookup"><span data-stu-id="c942d-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="c942d-206">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="c942d-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="c942d-207">在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="c942d-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="c942d-208">請確定 hello`Id`具有相同的值為 hello `TargetClaimsExchangeId` hello 前面一節中。</span><span class="sxs-lookup"><span data-stu-id="c942d-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="c942d-209">請確定`TechnicalProfileReferenceId`設定您建立舊版 (Contoso-SAML2) toohello 技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="c942d-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="c942d-210">上傳 hello 原則 tooyour 租用戶</span><span class="sxs-lookup"><span data-stu-id="c942d-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="c942d-211">在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c942d-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="c942d-212">選取 [識別體驗架構]。</span><span class="sxs-lookup"><span data-stu-id="c942d-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="c942d-213">開啟 hello**所有原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c942d-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="c942d-214">選取 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="c942d-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="c942d-215">請檢查**如果存在的話，請覆寫 hello 原則**方塊。</span><span class="sxs-lookup"><span data-stu-id="c942d-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="c942d-216">**上傳**TrustFrameworkExtensions.xml，並確定它不會通過 hello 驗證</span><span class="sxs-lookup"><span data-stu-id="c942d-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="c942d-217">使用 立即執行測試 hello 自訂原則</span><span class="sxs-lookup"><span data-stu-id="c942d-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="c942d-218">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="c942d-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="c942d-219">開啟**B2C_1A_signup_signin**，hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="c942d-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="c942d-220">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="c942d-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="c942d-221">您應該能夠使用 ADFS 帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="c942d-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="c942d-222">[選用]註冊 hello ADFS 帳戶宣告提供者 tooProfile 編輯使用者旅程</span><span class="sxs-lookup"><span data-stu-id="c942d-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="c942d-223">您可能會想 tooadd hello ADFS 帳戶身分識別提供者也 tooyour 使用者`ProfileEdit`使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="c942d-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="c942d-224">toomake 提供，我們可以重覆 hello 最後的兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="c942d-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="c942d-225">顯示 hello 按鈕</span><span class="sxs-lookup"><span data-stu-id="c942d-225">Display hello button</span></span>
1.  <span data-ttu-id="c942d-226">開啟 hello 原則 (例如，TrustFrameworkExtensions.xml) 的延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="c942d-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="c942d-227">尋找 hello`<UserJourney>`節點包含`Id="ProfileEdit"`hello 您複製的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="c942d-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="c942d-228">找出 hello`<OrchestrationStep>`包含的節點`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="c942d-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="c942d-229">在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="c942d-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="c942d-230">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="c942d-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="c942d-231">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="c942d-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="c942d-232">在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="c942d-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="c942d-233">使用 立即執行測試 hello 自訂設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="c942d-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="c942d-234">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="c942d-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="c942d-235">開啟**B2C_1A_ProfileEdit**，hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="c942d-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="c942d-236">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="c942d-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="c942d-237">您應該能夠使用 ADFS 帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="c942d-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="c942d-238">下載 hello 完整的原則檔案</span><span class="sxs-lookup"><span data-stu-id="c942d-238">Download hello complete policy files</span></span>
<span data-ttu-id="c942d-239">選擇性： 我們建議您建置您的案例完成的 hello 開始使用自訂原則逐步解說之後使用您自己的自訂原則檔案。</span><span class="sxs-lookup"><span data-stu-id="c942d-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="c942d-240">原則範例檔案僅供參考</span><span class="sxs-lookup"><span data-stu-id="c942d-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
