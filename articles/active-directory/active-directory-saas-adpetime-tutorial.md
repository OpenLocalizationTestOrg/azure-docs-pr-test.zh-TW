---
title: "教學課程：Azure Active Directory 與 ADP eTime 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ADP eTime 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="f78b8-103">教學課程：Azure Active Directory 與 ADP eTime 整合</span><span class="sxs-lookup"><span data-stu-id="f78b8-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="f78b8-104">在本教學課程中，您會了解如何將 ADP eTime 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="f78b8-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f78b8-105">將 ADP eTime 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f78b8-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f78b8-106">您可以在 Azure AD 中控制可存取 ADP eTime 的人員</span><span class="sxs-lookup"><span data-stu-id="f78b8-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="f78b8-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ADP eTime (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f78b8-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f78b8-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f78b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f78b8-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f78b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f78b8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f78b8-110">Prerequisites</span></span>

<span data-ttu-id="f78b8-111">若要設定 Azure AD 與 ADP eTime 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f78b8-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="f78b8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f78b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f78b8-113">已啟用 ADP eTime 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f78b8-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f78b8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f78b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f78b8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f78b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f78b8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f78b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f78b8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f78b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f78b8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f78b8-118">Scenario description</span></span>
<span data-ttu-id="f78b8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f78b8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f78b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f78b8-121">從資源庫新增 ADP eTime</span><span class="sxs-lookup"><span data-stu-id="f78b8-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="f78b8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f78b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="f78b8-123">從資源庫新增 ADP eTime</span><span class="sxs-lookup"><span data-stu-id="f78b8-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="f78b8-124">若要設定將 ADP eTime 整合到 Azure AD 中，您需要從資源庫將 ADP eTime 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f78b8-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f78b8-125">**若要從資源庫新增 ADP eTime，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f78b8-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f78b8-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f78b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f78b8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f78b8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f78b8-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f78b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f78b8-133">在搜尋方塊中，輸入 **ADP eTime**。</span><span class="sxs-lookup"><span data-stu-id="f78b8-133">In the search box, type **ADP eTime**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="f78b8-135">在結果面板中，選取 [ADP eTime]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="f78b8-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f78b8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f78b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f78b8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ADP eTime 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f78b8-139">若要讓單一登入能夠運作，Azure AD 必須知道 ADP eTime 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f78b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="f78b8-140">換句話說，必須在 Azure AD 使用者與 ADP eTime 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f78b8-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="f78b8-141">建立此連結關聯性的方法，就是將 ADP eTime 中 [Username] 的值指派為 Azure AD 中 [使用者名稱]的值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="f78b8-142">若要設定及測試與 ADP eTime 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="f78b8-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f78b8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f78b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f78b8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f78b8-145">**[建立 ADP eTime 測試使用者](#creating-an-adp-etime-test-user)** - 在 ADP eTime 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="f78b8-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f78b8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f78b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f78b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f78b8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f78b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f78b8-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ADP eTime 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="f78b8-150">**若要設定與 ADP eTime 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f78b8-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="f78b8-151">在 Azure 入口網站的 [ADP eTime] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f78b8-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="f78b8-155">在 [ADP eTime 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f78b8-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="f78b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="f78b8-157">a.</span></span> <span data-ttu-id="f78b8-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="f78b8-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="f78b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="f78b8-159">b.</span></span> <span data-ttu-id="f78b8-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="f78b8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="f78b8-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-161">These values are not the real.</span></span> <span data-ttu-id="f78b8-162">請使用實際的「回覆 URL」和「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="f78b8-163">請連絡 [ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="f78b8-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f78b8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="f78b8-166">ADP eTime 應用程式會預期要有特定格式的 SAML 判斷提示，這會要求您在 SAML 權杖屬性組態中新增自訂的屬性對應。</span><span class="sxs-lookup"><span data-stu-id="f78b8-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="f78b8-167">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="f78b8-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="f78b8-168">宣告名稱一律為 **"PersonImmutableID"** ，且值已對應至 ExtensionAttribute2，其中包含使用者的 EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="f78b8-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="f78b8-169">在這裡，會透過 EmployeeID 完成從 Azure AD 到 ADP eTime 的使用者對應，但您也可以根據應用程式設定，將之對應到不同的值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="f78b8-170">因此，請先與 [ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)合作以使用正確的使用者識別碼，然後將該值與 **"PersonImmutableID"** 宣告對應。</span><span class="sxs-lookup"><span data-stu-id="f78b8-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="f78b8-172">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f78b8-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="f78b8-173">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="f78b8-173">Attribute Name</span></span> | <span data-ttu-id="f78b8-174">屬性值</span><span class="sxs-lookup"><span data-stu-id="f78b8-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="f78b8-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="f78b8-175">PersonImmutableID</span></span> | <span data-ttu-id="f78b8-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="f78b8-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="f78b8-177">a.</span><span class="sxs-lookup"><span data-stu-id="f78b8-177">a.</span></span> <span data-ttu-id="f78b8-178">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f78b8-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f78b8-181">b.</span><span class="sxs-lookup"><span data-stu-id="f78b8-181">b.</span></span> <span data-ttu-id="f78b8-182">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="f78b8-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="f78b8-183">c.</span><span class="sxs-lookup"><span data-stu-id="f78b8-183">c.</span></span> <span data-ttu-id="f78b8-184">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f78b8-185">d.</span><span class="sxs-lookup"><span data-stu-id="f78b8-185">d.</span></span> <span data-ttu-id="f78b8-186">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f78b8-187">您必須先連絡 [ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)，向其要求租用戶的唯一識別碼屬性值，才能設定 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="f78b8-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="f78b8-188">您需要此值來設定應用程式的自訂宣告。</span><span class="sxs-lookup"><span data-stu-id="f78b8-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="f78b8-189">在 [ADP eTime 組態] 區段上，按一下 [設定 ADP eTime] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f78b8-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="f78b8-191">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f78b8-191">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="f78b8-193">若要在 **ADP eTime** 端設定單一登入，您必須將已下載的「中繼資料 XML」傳送給 [ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f78b8-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="f78b8-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f78b8-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f78b8-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f78b8-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f78b8-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f78b8-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f78b8-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f78b8-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f78b8-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f78b8-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f78b8-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f78b8-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f78b8-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f78b8-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f78b8-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f78b8-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f78b8-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f78b8-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f78b8-209">a.</span><span class="sxs-lookup"><span data-stu-id="f78b8-209">a.</span></span> <span data-ttu-id="f78b8-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f78b8-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f78b8-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f78b8-211">b.</span></span> <span data-ttu-id="f78b8-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f78b8-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f78b8-213">c.</span><span class="sxs-lookup"><span data-stu-id="f78b8-213">c.</span></span> <span data-ttu-id="f78b8-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f78b8-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f78b8-215">d.</span><span class="sxs-lookup"><span data-stu-id="f78b8-215">d.</span></span> <span data-ttu-id="f78b8-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f78b8-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="f78b8-217">建立 ADP eTime 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f78b8-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="f78b8-218">本節的目標是要在 ADP eTime 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f78b8-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="f78b8-219">請與 [ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)合作，在 ADP eTime 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="f78b8-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f78b8-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f78b8-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f78b8-221">在本節中，您會將 ADP eTime 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f78b8-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![指派使用者][200] 

<span data-ttu-id="f78b8-223">**若要將 Britta Simon 指派給 ADP eTime，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f78b8-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="f78b8-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f78b8-226">在應用程式清單中，選取 [ADP eTime]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-226">In the applications list, select **ADP eTime**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="f78b8-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-228">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f78b8-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f78b8-230">Click **Add** button.</span></span> <span data-ttu-id="f78b8-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f78b8-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f78b8-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f78b8-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f78b8-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f78b8-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f78b8-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f78b8-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f78b8-236">Testing single sign-on</span></span>

<span data-ttu-id="f78b8-237">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="f78b8-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f78b8-238">當您在「存取面板」中按一下 [ADP eTime] 圖格時，應該會自動登入您的 ADP eTime 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f78b8-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="f78b8-239">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f78b8-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f78b8-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="f78b8-240">Additional resources</span></span>

* [<span data-ttu-id="f78b8-241">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f78b8-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f78b8-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f78b8-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

