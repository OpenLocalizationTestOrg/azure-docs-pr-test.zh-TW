---
title: "教學課程：Azure Active Directory 與 IBM Kenexa Survey Enterprise 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 IBM Kenexa Survey Enterprise 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="293a3-103">教學課程：Azure Active Directory 與 IBM Kenexa Survey Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="293a3-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="293a3-104">在本教學課程中，您會了解如何整合 IBM Kenexa Survey Enterprise 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="293a3-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="293a3-105">IBM Kenexa Survey Enterprise 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="293a3-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="293a3-106">您可以在 Azure AD 中控制可存取 IBM Kenexa Survey Enterprise 的人員。</span><span class="sxs-lookup"><span data-stu-id="293a3-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="293a3-107">您可以讓使用者使用他們的 Azure AD 帳戶，透過單一登入 (SSO) 自動登入 IBM Kenexa Survey Enterprise。</span><span class="sxs-lookup"><span data-stu-id="293a3-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="293a3-108">您可以集中管理您的帳戶：Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="293a3-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="293a3-109">若您想深入了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="293a3-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="293a3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="293a3-110">Prerequisites</span></span>

<span data-ttu-id="293a3-111">若要設定 Azure AD 與 IBM Kenexa Survey Enterprise 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="293a3-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="293a3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="293a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="293a3-113">啟用 IBM Kenexa Survey Enterprise SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="293a3-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="293a3-114">當您測試本教學課程中的步驟時，不建議您使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="293a3-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="293a3-115">若要測試本教學課程中的步驟，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="293a3-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="293a3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="293a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="293a3-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="293a3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="293a3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="293a3-118">Scenario description</span></span>
<span data-ttu-id="293a3-119">在本教學課程中，您會在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="293a3-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="293a3-120">教學課程中說明的情節由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="293a3-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="293a3-121">從資源庫新增 IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="293a3-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="293a3-122">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="293a3-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="293a3-123">從資源庫新增 IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="293a3-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="293a3-124">若要設定將 IBM Kenexa Survey Enterprise 整合到 Azure AD 中，您需要從資源庫將 IBM Kenexa Survey Enterprise 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="293a3-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="293a3-125">若要從資源庫新增 IBM Kenexa Survey Enterprise，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="293a3-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="293a3-126">在 [Azure 入口網站](https://portal.azure.com)的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="293a3-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="293a3-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="293a3-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="293a3-130">若要新增應用程式，請按一下 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="293a3-130">To add an application, click the **New application** button.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="293a3-132">在搜尋方塊中輸入 **IBM Kenexa Survey Enterprise**。</span><span class="sxs-lookup"><span data-stu-id="293a3-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="293a3-134">在結果清單中，選取 [IBM Kenexa Survey Enterprise]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="293a3-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![結果清單中的 IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="293a3-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="293a3-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="293a3-137">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 IBM Kenexa Survey Enterprise 搭配運作的 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="293a3-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="293a3-138">為了讓 SSO 運作，Azure AD 需要識別 Azure AD 中對應的 IBM Kenexa Survey Enterprise 使用者。</span><span class="sxs-lookup"><span data-stu-id="293a3-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="293a3-139">換句話說，必須在 Azure AD 使用者和 IBM Kenexa Survey Enterprise 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="293a3-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="293a3-140">若要建立連結關聯性，請將 IBM Kenexa Survey Enterprise 中**使用者名稱**的值，指派為 Azure AD 中**使用者名稱**的值。</span><span class="sxs-lookup"><span data-stu-id="293a3-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="293a3-141">若要設定及測試與 IBM Kenexa Survey Enterprise 搭配運作的 Azure AD SSO，請完成下兩節中的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="293a3-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="293a3-142">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="293a3-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="293a3-143">在本節中，您會執行下列步驟，在 Azure 入口網站中啟用 Azure AD SSO，並在 IBM Kenexa Survey Enterprise 中設定 SSO：</span><span class="sxs-lookup"><span data-stu-id="293a3-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="293a3-144">在 Azure 入口網站的 [IBM Kenexa Survey Enterprise] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="293a3-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa Survey Enterprise 設定單一登入連結][4]

2. <span data-ttu-id="293a3-146">在 [單一登入] 對話方塊的 [模式] 方塊中，選取 [SAML 登入] 來啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="293a3-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="293a3-148">在 [IBM Kenexa Survey Enterprise 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="293a3-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![IBM Kenexa Survey Enterprise 網域及 URL 單一登入資訊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="293a3-150">a.</span><span class="sxs-lookup"><span data-stu-id="293a3-150">a.</span></span> <span data-ttu-id="293a3-151">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="293a3-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="293a3-152">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="293a3-152">b.</span></span> <span data-ttu-id="293a3-153">在 [回覆 URL] 文字方塊中，使用下列模式輸入 URL：`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="293a3-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="293a3-154">上述值並非真正的值。</span><span class="sxs-lookup"><span data-stu-id="293a3-154">The preceding values are not real.</span></span> <span data-ttu-id="293a3-155">請使用實際的識別碼和回覆 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="293a3-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="293a3-156">若要取得實際的值，請連絡 [IBM Kenexa Survey Enterprise 支援小組](https://www.ibm.com/support/home/?lnk=fcw)。</span><span class="sxs-lookup"><span data-stu-id="293a3-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="293a3-157">在 [SAML 簽署憑證] 下，按一下 [憑證 (Base64/)]，然後將憑證檔案儲存到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="293a3-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![憑證 (Base64) 下載連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="293a3-159">IBM Kenexa Survey Enterprise 應用程式需要特定格式的「安全性聲明標記語言 (SAML)」判斷提示，所以您必須將自訂屬性對應新增至 SAML 權杖屬性設定。</span><span class="sxs-lookup"><span data-stu-id="293a3-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="293a3-160">回應中的使用者識別碼宣告的值，必須符合 Kenexa 系統中設定的 SSO 識別碼。</span><span class="sxs-lookup"><span data-stu-id="293a3-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="293a3-161">若要將組織中適當的使用者識別碼對應為 SSO 網際網路資料包通訊協定 (IDP)，請與 [IBM Kenexa Survey Enterprise 支援小組](https://www.ibm.com/support/home/?lnk=fcw)合作。</span><span class="sxs-lookup"><span data-stu-id="293a3-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="293a3-162">根據預設，Azure AD 會將使用者識別碼設為使用者主體名稱 (UPN) 值。</span><span class="sxs-lookup"><span data-stu-id="293a3-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="293a3-163">您可以在 [屬性] 索引標籤中變更此值，如以下螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="293a3-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="293a3-164">只有在您正確完成對應之後，整合才有作用。</span><span class="sxs-lookup"><span data-stu-id="293a3-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![[使用者屬性] 對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="293a3-166">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="293a3-166">Click **Save**.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="293a3-168">若要開啟 [設定登入] 視窗，請在 [IBM Kenexa Survey Enterprise 組態] 下，按一下 [設定 IBM Kenexa Survey Enterprise]。</span><span class="sxs-lookup"><span data-stu-id="293a3-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![設定 IBM Kenexa Survey Enterprise 連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="293a3-170">從 [快速參考] 區段中，複製 [登出 URL]、[SAML 實體識別碼] 和 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="293a3-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="293a3-171">在 [設定登入] 視窗的 [快速參考] 下，複製 [登出 URL]、[SAML 實體識別碼] 和 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="293a3-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="293a3-172">若要在 **IBM Kenexa Survey Enterprise** 端設定 SSO，請將已下載的**憑證 (Base64)**、**登出 URL**、**SAML 實體識別碼**和 **SAML 單一登入服務 URL** 值，傳送給 [IBM Kenexa Survey Enterprise 支援小組](https://www.ibm.com/support/home/?lnk=fcw)。</span><span class="sxs-lookup"><span data-stu-id="293a3-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="293a3-173">當您設定應用程式時，您可以在 [Azure 入口網站](https://portal.azure.com)中參考這些指示的簡要版本。</span><span class="sxs-lookup"><span data-stu-id="293a3-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="293a3-174">當您從 [Active Directory] > [企業應用程式] 區段新增應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過最後的 [設定] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="293a3-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="293a3-175">若要深入了解內嵌文件功能，請參閱 [Azure AD 內嵌文件](https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="293a3-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="293a3-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="293a3-176">Create an Azure AD test user</span></span>
<span data-ttu-id="293a3-177">在本節中，您會執行下列步驟，在 Azure 入口網站中建立測試使用者 Britta Simon：</span><span class="sxs-lookup"><span data-stu-id="293a3-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![建立 Azure AD 測試使用者][100]

1. <span data-ttu-id="293a3-179">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="293a3-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="293a3-181">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="293a3-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="293a3-183">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="293a3-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="293a3-185">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="293a3-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="293a3-187">a.</span><span class="sxs-lookup"><span data-stu-id="293a3-187">a.</span></span> <span data-ttu-id="293a3-188">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="293a3-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="293a3-189">b.</span><span class="sxs-lookup"><span data-stu-id="293a3-189">b.</span></span> <span data-ttu-id="293a3-190">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="293a3-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="293a3-191">c.</span><span class="sxs-lookup"><span data-stu-id="293a3-191">c.</span></span> <span data-ttu-id="293a3-192">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="293a3-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="293a3-193">d.</span><span class="sxs-lookup"><span data-stu-id="293a3-193">d.</span></span> <span data-ttu-id="293a3-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="293a3-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="293a3-195">建立 IBM Kenexa Survey Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="293a3-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="293a3-196">在本節中，您要在 IBM Kenexa Survey Enterprise 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="293a3-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="293a3-197">若要在 IBM Kenexa Survey Enterprise 中建立使用者，並對應其 SSO 識別碼，您可以與 [IBM Kenexa Survey Enterprise 支援小組](https://www.ibm.com/support/home/?lnk=fcw)合作。</span><span class="sxs-lookup"><span data-stu-id="293a3-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="293a3-198">此 SSO 識別碼值也應該至 Azure AD 中的使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="293a3-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="293a3-199">您可以在 [屬性] 索引標籤上變更此預設設定。</span><span class="sxs-lookup"><span data-stu-id="293a3-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="293a3-200">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="293a3-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="293a3-201">在本節中，您會將 IBM Kenexa Survey Enterprise 的存取權授與使用者 Britta Simon，讓她能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="293a3-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="293a3-203">若要將使用者 Britta Simon 指派給 IBM Kenexa Survey Enterprise，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="293a3-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="293a3-204">在 Azure 入口網站中，開啟 [應用程式] 檢視，移至 [目錄] 檢視，選取 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="293a3-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![[企業應用程式] 和 [所有應用程式] 連結][201] 

2. <span data-ttu-id="293a3-206">在 [應用程式] 清單中，選取 [IBM Kenexa Survey Enterprise]。</span><span class="sxs-lookup"><span data-stu-id="293a3-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![[應用程式] 清單中的 IBM Kenexa Survey Enterprise 連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="293a3-208">在左窗格中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="293a3-208">In the left pane, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="293a3-210">按一下 [新增] 按鈕，然後在 [新增指派] 窗格中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="293a3-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="293a3-212">在 [使用者和群組] 對話方塊的 [使用者] 清單中，選取 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="293a3-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="293a3-213">在 [使用者和群組] 對話方塊中，按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="293a3-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="293a3-214">在 [新增指派] 對話方塊中，按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="293a3-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="293a3-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="293a3-215">Test single sign-on</span></span>

<span data-ttu-id="293a3-216">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="293a3-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="293a3-217">當您在存取面板中按一下 [IBM Kenexa Survey Enterprise] 圖格時，應該會自動登入您的 IBM Kenexa Survey Enterprise 應用程式。</span><span class="sxs-lookup"><span data-stu-id="293a3-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="293a3-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="293a3-218">Additional resources</span></span>

* [<span data-ttu-id="293a3-219">如何整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="293a3-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="293a3-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="293a3-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
