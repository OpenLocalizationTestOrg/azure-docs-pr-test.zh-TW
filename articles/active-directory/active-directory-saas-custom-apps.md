---
title: "設定應用程式的 Azure AD SSO | Microsoft Docs"
description: "了解如何使用 SAML 和密碼 SSO 以自助方式將應用程式連接到 Azure Active Directory"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9049f526243cb4659aaf86b3d31146abe8f5f3ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configuring-single-sign-on-to-applications-that-are-not-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="208c9-103">設定對不在 Azure Active Directory 應用程式庫中的應用程式的單一登入</span><span class="sxs-lookup"><span data-stu-id="208c9-103">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="208c9-104">本文是關於可讓系統管理員設定單一登入不存在於 Azure Active Directory 應用程式資源庫的應用程式，而「不需要撰寫程式碼」 的功能。</span><span class="sxs-lookup"><span data-stu-id="208c9-104">This article is about a feature that enables administrators to configure single sign-on to applications not present in the Azure Active Directory app gallery *without writing code*.</span></span> <span data-ttu-id="208c9-105">此功能已在 2015 年 11 月 18 日的技術預覽中發行，並且包含在 [Azure Active Directory Premium](active-directory-editions.md)中。</span><span class="sxs-lookup"><span data-stu-id="208c9-105">This feature was released from technical preview on November 18th, 2015 and is included in [Azure Active Directory Premium](active-directory-editions.md).</span></span> <span data-ttu-id="208c9-106">如果您要改為尋找有關如何透過程式碼將自訂應用程式與 Azure AD 整合的開發人員指導方針，請參閱 [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="208c9-106">If you are instead looking for developer guidance on how to integrate custom apps with Azure AD through code, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

<span data-ttu-id="208c9-107">Azure Active Directory 應用程式資源庫提供一份已知能支援單一登入搭配 Azure Active Directory 的應用程式清單，如 [本文](active-directory-appssoaccess-whatis.md)所說明。</span><span class="sxs-lookup"><span data-stu-id="208c9-107">The Azure Active Directory application gallery provides a listing of applications that are known to support a form of single sign-on with Azure Active Directory, as described in [this article](active-directory-appssoaccess-whatis.md).</span></span> <span data-ttu-id="208c9-108">一旦您 (假設您是 IT 專業人員或組織中的系統整合者) 找到所要連接的應用程式，您就可以遵循應 Azure 管理入口網站中顯示的逐步指示，啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="208c9-108">Once you (as an IT specialist or system integrator in your organization) have found the application you want to connect, you can get started by follow the step-by-step instructions presented in the Azure management portal to enable single sign-on.</span></span>

<span data-ttu-id="208c9-109">具有 [Azure Active Directory Premium](active-directory-editions.md) 授權的客戶也會取得以下額外功能：</span><span class="sxs-lookup"><span data-stu-id="208c9-109">Customers with [Azure Active Directory Premium](active-directory-editions.md) licenses also get these additional capabilities:</span></span>

* <span data-ttu-id="208c9-110">任何支援 SAML 2.0 身分識別提供者的應用程式皆可進行自助式整合 (SP 起始或 IdP 起始)</span><span class="sxs-lookup"><span data-stu-id="208c9-110">Self-service integration of any application that supports SAML 2.0 identity providers (SP-initiated or IdP-initiated)</span></span>
* <span data-ttu-id="208c9-111">Web 應用程式可在使用 [密碼型 SSO](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="208c9-111">Self-service integration of any web application that has an HTML-based sign-in page using [password-based SSO](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)</span></span>
* <span data-ttu-id="208c9-112">應用程式可使用 SCIM 通訊協定進行自助式連線，以執行使用者佈建 ([說明請見此處](active-directory-scim-provisioning.md))</span><span class="sxs-lookup"><span data-stu-id="208c9-112">Self-service connection of applications that use the SCIM protocol for user provisioning ([described here](active-directory-scim-provisioning.md))</span></span>
* <span data-ttu-id="208c9-113">能夠在 [Office 365 應用程式啟動器](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/)或 [Azure AD 存取面板](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)中新增任何應用程式的連結</span><span class="sxs-lookup"><span data-stu-id="208c9-113">Ability to add links to any application in the [Office 365 app launcher](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) or the [Azure AD access panel](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)</span></span>

<span data-ttu-id="208c9-114">這不僅包括您所使用、但尚未在 Azure AD 應用程式庫中上線的 SaaS 應用程式，也包括您的組織已部署至您所控制的伺服器 (在雲端或內部部署中) 的第三方 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="208c9-114">This can include not only SaaS applications that you use but have not yet been on-boarded to the Azure AD application gallery, but third-party web applications that your organization has deployed to servers you control, either in the cloud or on-premises.</span></span>

<span data-ttu-id="208c9-115">這些功能 (也稱為「應用程式整合範本」 )，為支援 SAML、SCIM 或表單型驗證的應用程式提供標準型連接點，包括有彈性的選項和與廣泛應用程式相容性的設定。</span><span class="sxs-lookup"><span data-stu-id="208c9-115">These capabilities, also known as *app integration templates*, provide standards-based connection points for apps that support SAML, SCIM, or forms-based authentication, and include flexible options and settings for compatibility with a broad number of applications.</span></span> 

## <a name="adding-an-unlisted-application"></a><span data-ttu-id="208c9-116">新增未列出的應用程式</span><span class="sxs-lookup"><span data-stu-id="208c9-116">Adding an unlisted application</span></span>
<span data-ttu-id="208c9-117">若要使用應用程式整合範本連接應用程式，使用您的 Azure Active Directory 系統管理員帳戶登入 Azure 管理入口網站，並瀏覽至 [Active Directory] > [目錄] > [應用程式] 區段、選取 [新增]，然後選取 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="208c9-117">To connect an application using an app integration template, sign into the Azure management portal using your Azure Active Directory administrator account, and browse to the **Active Directory > [Directory] > Applications** section, select **Add**, and then **Add an application from the gallery**.</span></span> 

![][1]

<span data-ttu-id="208c9-118">在應用程式資源庫，您可以使用左側的 [自訂] 類別來新增未列出的應用程式；找不到您想要的應用程式，可以選取顯示在搜尋結果中的 [新增未列出的應用程式] 連結來進行新增。</span><span class="sxs-lookup"><span data-stu-id="208c9-118">In the app gallery, you can add an unlisted app using the **Custom** category on the left, or by selecting the **Add an unlisted application** link that is shown in the search results if your desired app wasn't found.</span></span> <span data-ttu-id="208c9-119">輸入應用程式的名稱之後，您可以設定單一登入選項和行為。</span><span class="sxs-lookup"><span data-stu-id="208c9-119">After entering a Name for your application, you can configure the single sign-on options and behavior.</span></span> 

<span data-ttu-id="208c9-120">**快速提示**：最佳作法是使用搜尋函式來查看應用程式是否已存在於應用程式庫中。</span><span class="sxs-lookup"><span data-stu-id="208c9-120">**Quick tip**:  As a best practice, use the search function to check to see if the application already exists in the application gallery.</span></span> <span data-ttu-id="208c9-121">如果找到應用程式，且其描述提及「單一登入」，則應用程式已支援同盟單一登入。</span><span class="sxs-lookup"><span data-stu-id="208c9-121">If the app is found and its description mentions "single sign on", then the application is already supported for federated single sign-on.</span></span> 

![][2]

<span data-ttu-id="208c9-122">以這樣的方式新增應用程式所提供的體驗，非常類似於預先整合的應用程式所提供的體驗。</span><span class="sxs-lookup"><span data-stu-id="208c9-122">Adding an application this way provides a very similar experience to the one available for pre-integrated applications.</span></span> <span data-ttu-id="208c9-123">若要開始作業，請選取 [設定單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="208c9-123">To start, select **Configure Single Sign-On**.</span></span> <span data-ttu-id="208c9-124">下一個畫面會呈現下列三個單一登入設定選項，其說明將在後續幾節提供。</span><span class="sxs-lookup"><span data-stu-id="208c9-124">The next screen presents the following three options for configuring single sign on, which are described in the following sections.</span></span>

![][3]

## <a name="azure-ad-single-sign-on"></a><span data-ttu-id="208c9-125">Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="208c9-125">Azure AD Single Sign-On</span></span>
<span data-ttu-id="208c9-126">選取此選項，可為應用程式設定 SAML 型驗證。</span><span class="sxs-lookup"><span data-stu-id="208c9-126">Select this option to configure SAML-based authentication for the application.</span></span> <span data-ttu-id="208c9-127">若使用此選項，應用程式必須支援 SAML 2.0，您應先收集有關於如何使用應用程式之 SAML 功能的資訊，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="208c9-127">This requires that the application support SAML 2.0, and you should collect information on how to use the SAML capabilities of the application before continuing.</span></span> <span data-ttu-id="208c9-128">選取 [下一步] 後，系統會提示您為應用程式輸入三個對應於 SAML 端點的不同 URL。</span><span class="sxs-lookup"><span data-stu-id="208c9-128">After selecting **Next**, you will be prompted to enter three different URLs corresponding to the SAML endpoints for the application.</span></span> 

![][4]

<span data-ttu-id="208c9-129">它們是：</span><span class="sxs-lookup"><span data-stu-id="208c9-129">These are:</span></span>

* <span data-ttu-id="208c9-130">**登入 URL (僅限 SP 起始)** - 使用者在此登入此應用程式。</span><span class="sxs-lookup"><span data-stu-id="208c9-130">**Sign On URL (SP-initiated only)** – Where the user goes to sign-in to this application.</span></span> <span data-ttu-id="208c9-131">如果應用程式設定為執行服務提供者起始單一登入，則當使用者導覽到此 URL，服務提供者會執行必要的重新導向至 Azure AD，以進行驗證並將使用者登入。</span><span class="sxs-lookup"><span data-stu-id="208c9-131">If the application is configured to perform service provider-initiated single sign on, then when a user navigates to this URL, the service provider will do the necessary redirection to Azure AD to authenticate and log on the user in.</span></span> <span data-ttu-id="208c9-132">如果已填入此欄位，Azure AD 將使用此 URL 從 Office 365 和 Azure AD 存取面板中啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="208c9-132">If this field is populated, then Azure AD will use this URL to launch the application from Office 365 and the Azure AD Access Panel.</span></span> <span data-ttu-id="208c9-133">如果略過這個欄位，則 Azure AD 會改為執行識別提供者 - 即從 Office 365、Azure AD 存取面板或 Azure AD 單一登入 URL (可從 [儀表板] 索引標籤複製) 啟動應用程式時起始登入。</span><span class="sxs-lookup"><span data-stu-id="208c9-133">If this field is ommited, then Azure AD will instead perform identity provider -initiated sign on when the app is launched from Office 365, the Azure AD Access Panel, or from the Azure AD single sign-on URL (copiable from the Dashboard tab).</span></span>
* <span data-ttu-id="208c9-134">**簽發者 URL** - 簽發者 URL 應專門用於識別正在設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="208c9-134">**Issuer URL** - The issuer URL should uniquely identify the application for which single sign on is being configured.</span></span> <span data-ttu-id="208c9-135"> 參數值，應用程式預期會驗證它。</span><span class="sxs-lookup"><span data-stu-id="208c9-135">This is the value that Azure AD sends back to application as the **Audience** parameter of the SAML token, and the application is expected to validate it.</span></span> <span data-ttu-id="208c9-136">在應用程式中提供的任何 SAML 中繼資料中，這個值也會顯示為實體識別碼  。</span><span class="sxs-lookup"><span data-stu-id="208c9-136">This value also appears as the **Entity ID** in any SAML metadata provided by the application.</span></span> <span data-ttu-id="208c9-137">查看應用程式的 SAML 文件，了解實體識別碼或 Audience 值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="208c9-137">Check the application’s SAML documentation for details on what it's Entity ID or Audience value is.</span></span> <span data-ttu-id="208c9-138">以下是觀眾 URL 在傳回應用程式的 SAML 權杖中的外觀範例︰</span><span class="sxs-lookup"><span data-stu-id="208c9-138">Below is an example of how the Audience URL appears in the SAML token returned to the application:</span></span>

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* <span data-ttu-id="208c9-139">**回覆 URL** -回覆 URL 是應用程式預期接收 SAML 權杖的位置。</span><span class="sxs-lookup"><span data-stu-id="208c9-139">**Reply URL** - The reply URL is where the application expects to receive the SAML token.</span></span> <span data-ttu-id="208c9-140">。</span><span class="sxs-lookup"><span data-stu-id="208c9-140">This is also referred to as the **Assertion Consumer Service (ACS) URL**.</span></span> <span data-ttu-id="208c9-141">查看應用程式的 SAML 文件，了解 SAML 權杖回覆 URL 或 ACS URL 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="208c9-141">Check the application’s SAML documentation for details on what its SAML token reply URL or ACS URL is.</span></span>
  <span data-ttu-id="208c9-142">在輸入這些資料後，請按 [下一步]  繼續前往下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="208c9-142">After these have been entered, click **Next** to proceed to the next screen.</span></span> <span data-ttu-id="208c9-143">此畫面會提供相關資訊來說明在應用程式端需要進行哪些設定，才能使應用程式接受來自於 Azure AD 的 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="208c9-143">This screen provides information about what needs to be configured on the application side to enable it to accept a SAML token from Azure AD.</span></span> 

![][5]

<span data-ttu-id="208c9-144">所需的值會隨應用程式而不同，請查看應用程式的 SAML 文件以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="208c9-144">Which values are required will vary depending on the application, so check the application's SAML documentation for details.</span></span> <span data-ttu-id="208c9-145">**登入**和**登出**服務 URL 會解析為相同的端點，這是您的 Azure AD 執行個體的 SAML 要求處理端點。</span><span class="sxs-lookup"><span data-stu-id="208c9-145">The **Sign-On** and **Sign-Out** service URL both resolve to the same endpoint, which is the SAML request-handling endpoint for your instance of Azure AD.</span></span> <span data-ttu-id="208c9-146">「簽發者 URL」是在發出給應用程式的 SAML 權杖內顯示為「簽發者」的值。</span><span class="sxs-lookup"><span data-stu-id="208c9-146">The Issuer URL is the value that appears as the "Issuer" inside the SAML token issued to the application.</span></span> 

<span data-ttu-id="208c9-147">設定您的應用程式之後，請按 [下一步] 按鈕，再按 [完成]，以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="208c9-147">After your application has been configured, click **Next** button and then the **Complete** to close the dialog.</span></span> 

## <a name="assigning-users-and-groups-to-your-saml-application"></a><span data-ttu-id="208c9-148">將使用者和群組指派給您的 SAML 應用程式</span><span class="sxs-lookup"><span data-stu-id="208c9-148">Assigning users and groups to your SAML application</span></span>
<span data-ttu-id="208c9-149">您的應用程式在設定為使用 Azure AD 作為 SAML 型身分識別提供者之後，就幾乎可以進行測試了。</span><span class="sxs-lookup"><span data-stu-id="208c9-149">Once your application has been configured to use Azure AD as a SAML-based identity provider, then it is almost ready to test.</span></span> <span data-ttu-id="208c9-150">為了控制安全性，Azure AD 不會核發允許他們登入應用程式的權杖，除非他們已使用 Azure AD 獲得存取存取權。</span><span class="sxs-lookup"><span data-stu-id="208c9-150">As a security control, Azure AD will not issue a token allowing them to sign into the application unless they have been granted access using Azure AD.</span></span> <span data-ttu-id="208c9-151">使用者可以直接獲得存取權，或透過其所屬的群組取得。</span><span class="sxs-lookup"><span data-stu-id="208c9-151">Users may be granted access directly, or through a group that they are a member of.</span></span> 

<span data-ttu-id="208c9-152">若要將使用者或群組指派給您的應用程式，請按一下 [指派使用者]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="208c9-152">To assign a user or group to your application, click the **Assign Users** button.</span></span> <span data-ttu-id="208c9-153">選取您要指派的使用者或群組，然後選取 [指派]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="208c9-153">Select the user or group you wish to assign, and then select the **Assign** button.</span></span> 

![][6]

<span data-ttu-id="208c9-154">指派使用者可讓 Azure AD 為該使用者核發權杖，並使此應用程式的圖格出現在使用者的存取面板中。</span><span class="sxs-lookup"><span data-stu-id="208c9-154">Assigning a user will allow Azure AD to issue a token for the user, as well as causing a tile for this application to appear in the user's Access Panel.</span></span> <span data-ttu-id="208c9-155">如果使用者使用 Office 365，則也會有應用程式圖格出現在 Office 365 應用程式啟動器中。</span><span class="sxs-lookup"><span data-stu-id="208c9-155">An application tile will also appear in the Office 365 application launcher if the user is using Office 365.</span></span> 

<span data-ttu-id="208c9-156">您可以在應用程式的 [設定] 索引標籤上使用 [上傳標誌] 按鈕，來上傳應用程式的圖格標誌。</span><span class="sxs-lookup"><span data-stu-id="208c9-156">You can upload a tile logo for the application using the **Upload Logo** button on the **Configure** tab for the application.</span></span> 

### <a name="customizing-the-claims-issued-in-the-saml-token"></a><span data-ttu-id="208c9-157">自訂在 SAML 權杖中發出的宣告</span><span class="sxs-lookup"><span data-stu-id="208c9-157">Customizing the claims issued in the SAML token</span></span>
<span data-ttu-id="208c9-158">當使用者對應用程式進行驗證時，Azure AD 會將 SAML 權杖發出給應用程式，其中包含可唯一識別使用者的使用者相關資訊 (或宣告)。</span><span class="sxs-lookup"><span data-stu-id="208c9-158">When a user authenticates to the application, Azure AD will issue a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="208c9-159">根據預設，其中包含使用者的使用者名稱、電子郵件地址、名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="208c9-159">By default this includes the user's username, email address, first name, and last name.</span></span> 

<span data-ttu-id="208c9-160">您可以在 [屬性]  索引標籤下檢視或編輯在 SAML 權杖中傳送給應用程式的宣告。</span><span class="sxs-lookup"><span data-stu-id="208c9-160">You can view or edit the claims sent in the SAML token to the application under the **Attributes** tab.</span></span> 

![][7]

<span data-ttu-id="208c9-161">您可能需要編輯在 SAML 權杖中發出的宣告的兩個可能原因為：•被寫入的應用程式需要一組不同的宣告 URI 或宣告值 •您的應用程式的部署方式需要 NameIdentifier 宣告不同於儲存在 Azure Active Directory 中的使用者名稱 (也稱為使用者主體名稱)。</span><span class="sxs-lookup"><span data-stu-id="208c9-161">There are two possible reasons why you might need to edit the claims issued in the SAML token: •The application has been written to require a different set of claim URIs or claim values •Your application has been deployed in a way that requires the NameIdentifier claim to be something other than the username (AKA user principal name) stored in Azure Active Directory.</span></span> 

<span data-ttu-id="208c9-162">如需在這些情況下如何新增和編輯宣告的相關資訊，請參閱這篇 [關於宣告自訂的文章](active-directory-saml-claims-customization.md)。</span><span class="sxs-lookup"><span data-stu-id="208c9-162">For information on how to add and edit claims for these scenarios, check out this [article on claims customization](active-directory-saml-claims-customization.md).</span></span> 

### <a name="testing-the-saml-application"></a><span data-ttu-id="208c9-163">測試 SAML 應用程式</span><span class="sxs-lookup"><span data-stu-id="208c9-163">Testing the SAML application</span></span>
<span data-ttu-id="208c9-164">在 Azure AD 中和應用程式中設定 SAML URL 和憑證、將使用者或群組指派給 Azure 中的應用程式，並且已視需要檢視和編輯宣告之後，使用者即可登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="208c9-164">Once the SAML URLs and certificate have been configured in Azure AD and in the application, users or groups have been assigned to the application in Azure, and the claims have been reviewed and edited if necessary, then the user is ready to sign into the application.</span></span> 

<span data-ttu-id="208c9-165">若要進行測試，請在 https://myapps.microsoft.com 上使用您指派給應用程式的使用者帳戶登入 Azure AD 存取面板，然後按一下應用程式的圖格開始進行單一登入程序。</span><span class="sxs-lookup"><span data-stu-id="208c9-165">To test, simply sign-into the Azure AD access panel at https://myapps.microsoft.com using a user account you assigned to the application, and then click on the tile for the application to kick off the single sign-on process.</span></span> <span data-ttu-id="208c9-166">或者，您可以直接瀏覽至應用程式的 [登入 URL]，並從該處登入。</span><span class="sxs-lookup"><span data-stu-id="208c9-166">Alternately, you can browse directly to the Sign-On URL for the application and sign-in from there.</span></span> 

<span data-ttu-id="208c9-167">如需偵錯提示，請參閱這篇 [有關於如何對應用程式的 SAML 型單一登入進行偵錯的文章](active-directory-saml-debugging.md)</span><span class="sxs-lookup"><span data-stu-id="208c9-167">For debugging tips, see this [article on how to debug SAML-based single sign-on to applications](active-directory-saml-debugging.md)</span></span> 

## <a name="password-single-sign-on"></a><span data-ttu-id="208c9-168">密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="208c9-168">Password Single Sign-On</span></span>
<span data-ttu-id="208c9-169">選取此選項，可為具有 HTML 登入頁面的 Web 應用程式設定 [密碼單一登入](active-directory-appssoaccess-whatis.md) 。</span><span class="sxs-lookup"><span data-stu-id="208c9-169">Select this option to configure [password-based single sign-on](active-directory-appssoaccess-whatis.md) for a web application that has an HTML sign-in page.</span></span> <span data-ttu-id="208c9-170">密碼 SSO 也稱為密碼儲存庫存，可讓您管理使用者對不支援身分識別同盟之 Web 應用程式的存取和密碼。</span><span class="sxs-lookup"><span data-stu-id="208c9-170">Password-based SSO, also referred to as password vaulting, enables you to manage user access and passwords to web applications that don't support identity federation.</span></span> <span data-ttu-id="208c9-171">如果有數個使用者需要共用單一帳戶 (例如共用組織的社交媒體應用程式帳戶)，這也很有用處。</span><span class="sxs-lookup"><span data-stu-id="208c9-171">It is also useful for scenarios where several users need to share a single account, such as to your organization's social media app accounts.</span></span> 

<span data-ttu-id="208c9-172">選取 [下一步] 之後，系統會提示您輸入應用程式的 Web 型登入頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="208c9-172">After selecting **Next**, you will be prompted to enter the URL of the application's web-based sign-in page.</span></span> <span data-ttu-id="208c9-173">請注意，這必須是包含使用者名稱和密碼輸入欄位的頁面。</span><span class="sxs-lookup"><span data-stu-id="208c9-173">Note that this must be the page that includes the username and password input fields.</span></span> <span data-ttu-id="208c9-174">輸入之後，Azure AD 會啟動程序來剖析使用者名稱輸入和密碼輸入的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="208c9-174">Once entered, Azure AD starts a process to parse the sign-in page for a username input and a password input.</span></span> <span data-ttu-id="208c9-175">如果此程序不成功，系統會引導您執行安裝瀏覽器延伸模組 (需要 Internet Explorer、Chrome 或 Firefox) 的替代程序，以讓您手動擷取欄位。</span><span class="sxs-lookup"><span data-stu-id="208c9-175">If the process is not successful, then it guides you through an alternate process of installing a browser extension (requires Internet Explorer, Chrome, or Firefox) that will allow you to manually capture the fields.</span></span>

<span data-ttu-id="208c9-176">在擷取登入頁面後，即可指派使用者和群組，並且可像 [密碼 SSO 應用程式](active-directory-appssoaccess-whatis.md)一般設定認證原則。</span><span class="sxs-lookup"><span data-stu-id="208c9-176">Once the sign-in page is captured, users and groups may be assigned and credential policies can be set just like regular [password SSO apps](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="208c9-177">注意：您可以在應用程式的 [設定] 索引標籤上使用 [上傳標誌] 按鈕，來上傳應用程式的圖格標誌。</span><span class="sxs-lookup"><span data-stu-id="208c9-177">Note: You can upload a tile logo for the application using the **Upload Logo** button on the **Configure** tab for the application.</span></span> 

## <a name="existing-single-sign-on"></a><span data-ttu-id="208c9-178">現有單一登入</span><span class="sxs-lookup"><span data-stu-id="208c9-178">Existing Single Sign-On</span></span>
<span data-ttu-id="208c9-179">選取此選項，可將應用程式的連結新增至組織的 Azure AD 存取面板或 Office 365 入口網站。</span><span class="sxs-lookup"><span data-stu-id="208c9-179">Select this option to add a link to an application to your organization's Azure AD Access Panel or Office 365 portal.</span></span> <span data-ttu-id="208c9-180">使用此選項，可讓您新增目前使用 Azure Active Directory 同盟服務 (或其他同盟服務)、而不是使用 Azure AD 的自訂 Web 應用程式的連結，以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="208c9-180">You can use this to add links to custom web apps that currently use Azure Active Directory Federation Services (or other federation service) instead of Azure AD for authentication.</span></span> <span data-ttu-id="208c9-181">或者，您可以新增特定 SharePoint 網頁或其他只要出現在使用者存取面板上的網頁的深層連結。</span><span class="sxs-lookup"><span data-stu-id="208c9-181">Or, you can add deep links to specific SharePoint pages or other web pages that you just want to appear on your user's Access Panels.</span></span> 

<span data-ttu-id="208c9-182">選取 [下一步] 之後，系統會提示您輸入要連結到的應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="208c9-182">After selecting **Next**, you will be prompted to enter the URL of the application to link to.</span></span> <span data-ttu-id="208c9-183">完成之後，使用者和群組即可指派給應用程式，而使應用程式出現在這些使用者的 [Office 365 應用程式啟動器](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/)或 [Azure AD 存取面板](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)中。</span><span class="sxs-lookup"><span data-stu-id="208c9-183">Once completed, users and groups may be assigned to the application, which causes the application to appear in the [Office 365 app launcher](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) or the [Azure AD access panel](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) for those users.</span></span>

<span data-ttu-id="208c9-184">注意：您可以在應用程式的 [設定] 索引標籤上使用 [上傳標誌] 按鈕，來上傳應用程式的圖格標誌。</span><span class="sxs-lookup"><span data-stu-id="208c9-184">Note: You can upload a tile logo for the application using the **Upload Logo** button on the **Configure** tab for the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="208c9-185">相關文章</span><span class="sxs-lookup"><span data-stu-id="208c9-185">Related Articles</span></span>
* [<span data-ttu-id="208c9-186">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="208c9-186">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="208c9-187">如何為預先整合的應用程式自訂在 SAML 權杖中發出的宣告</span><span class="sxs-lookup"><span data-stu-id="208c9-187">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)
* [<span data-ttu-id="208c9-188">SAML 型單一登入疑難排解</span><span class="sxs-lookup"><span data-stu-id="208c9-188">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
