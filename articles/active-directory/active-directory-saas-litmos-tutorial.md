---
title: "教學課程：Azure Active Directory 與 Litmos 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Litmos 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="5214f-103">教學課程：Azure Active Directory 與 Litmos 整合</span><span class="sxs-lookup"><span data-stu-id="5214f-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="5214f-104">在本教學課程中，您會了解如何整合 Litmos 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5214f-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5214f-105">將 Litmos 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5214f-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5214f-106">您可以在 Azure AD 中控制可存取 Litmos 的人員。</span><span class="sxs-lookup"><span data-stu-id="5214f-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="5214f-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Litmos (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="5214f-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5214f-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5214f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5214f-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5214f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5214f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5214f-110">Prerequisites</span></span>

<span data-ttu-id="5214f-111">若要設定 Azure AD 與 Litmos 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5214f-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="5214f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5214f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5214f-113">啟用 Litmos 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5214f-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5214f-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5214f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5214f-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5214f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5214f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5214f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5214f-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5214f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5214f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5214f-118">Scenario description</span></span>
<span data-ttu-id="5214f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5214f-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5214f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5214f-121">從資源庫加入 Litmos</span><span class="sxs-lookup"><span data-stu-id="5214f-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="5214f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5214f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="5214f-123">從資源庫加入 Litmos</span><span class="sxs-lookup"><span data-stu-id="5214f-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="5214f-124">若要設定將 Litmos 整合到 Azure AD 中，您需要從資源庫將 Litmos 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5214f-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5214f-125">**若要從資源庫新增 Litmos，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5214f-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5214f-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5214f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="5214f-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5214f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5214f-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5214f-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="5214f-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5214f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="5214f-133">在搜尋方塊中，輸入 **Litmos**，從結果面板中選取 [Litmos]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5214f-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5214f-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5214f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5214f-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Litmos 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5214f-137">若要讓單一登入運作，Azure AD 必須知道 Litmos 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5214f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="5214f-138">換句話說，必須在 Azure AD 使用者與 Litmos 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5214f-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="5214f-139">在 Litmos 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5214f-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5214f-140">若要設定及測試與 Litmos 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="5214f-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5214f-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5214f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5214f-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5214f-143">**[建立 Litmos 測試使用者](#create-a-litmos-test-user)** - 使 Litmos 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="5214f-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5214f-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5214f-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5214f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5214f-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5214f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5214f-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Litmos 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="5214f-148">**若要設定與 Litmos 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5214f-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="5214f-149">在 Azure 入口網站的 [Litmos] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5214f-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="5214f-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="5214f-153">在 [Litmos 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5214f-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Litmos 網域及 URL 單一登入資訊](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="5214f-155">a.</span><span class="sxs-lookup"><span data-stu-id="5214f-155">a.</span></span> <span data-ttu-id="5214f-156">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="5214f-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="5214f-157">b.</span><span class="sxs-lookup"><span data-stu-id="5214f-157">b.</span></span> <span data-ttu-id="5214f-158">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="5214f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5214f-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5214f-159">These values are not real.</span></span> <span data-ttu-id="5214f-160">請使用實際的「識別碼」及「回覆 URL」來更新這些值 (本教學課程稍後會說明)，或連絡 [Litmos 支援小組](https://www.litmos.com/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5214f-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="5214f-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5214f-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="5214f-163">進行設定時，您需要為 Litmos 應用程式自訂 [SAML Token 屬性]  。</span><span class="sxs-lookup"><span data-stu-id="5214f-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![屬性區段](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="5214f-165">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="5214f-165">Attribute Name</span></span>   | <span data-ttu-id="5214f-166">屬性值</span><span class="sxs-lookup"><span data-stu-id="5214f-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="5214f-167">名字</span><span class="sxs-lookup"><span data-stu-id="5214f-167">FirstName</span></span> |<span data-ttu-id="5214f-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5214f-168">user.givenname</span></span> |
    | <span data-ttu-id="5214f-169">姓氏</span><span class="sxs-lookup"><span data-stu-id="5214f-169">LastName</span></span>  |<span data-ttu-id="5214f-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="5214f-170">user.surname</span></span> |
    | <span data-ttu-id="5214f-171">電子郵件</span><span class="sxs-lookup"><span data-stu-id="5214f-171">Email</span></span> |<span data-ttu-id="5214f-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="5214f-172">user.mail</span></span> |

    <span data-ttu-id="5214f-173">a.</span><span class="sxs-lookup"><span data-stu-id="5214f-173">a.</span></span> <span data-ttu-id="5214f-174">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5214f-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![新增屬性](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![新增屬性對話方塊](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5214f-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5214f-177">b.</span></span> <span data-ttu-id="5214f-178">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="5214f-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5214f-179">c.</span><span class="sxs-lookup"><span data-stu-id="5214f-179">c.</span></span> <span data-ttu-id="5214f-180">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="5214f-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5214f-181">d.</span><span class="sxs-lookup"><span data-stu-id="5214f-181">d.</span></span> <span data-ttu-id="5214f-182">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="5214f-183">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5214f-183">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5214f-185">在不同的瀏覽器視窗中，以系統管理員身分登入您的 Litmos 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5214f-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="5214f-186">在左側導覽列中，按一下 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![應用程式端的帳戶區段][22] 

9. <span data-ttu-id="5214f-188">按一下 [整合]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5214f-188">Click the **Integrations** tab.</span></span>
   
    ![整合索引標籤][23] 

10. <span data-ttu-id="5214f-190">在 [整合] 索引標籤上，向下捲動至 [協力廠商整合]，然後按一下 [SAML 2.0] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5214f-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 區段][24] 

11. <span data-ttu-id="5214f-192">複製 [litmos 的 SAML 端點是:] 下的值，然後貼到 Azure 入口網站中 [Litmos 網域及 URL] 區段的 [回覆 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5214f-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML 端點][26] 

12. <span data-ttu-id="5214f-194">在您的 **Litmos** 應用程式中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5214f-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Litmos 應用程式][25] 
     
     <span data-ttu-id="5214f-196">a.</span><span class="sxs-lookup"><span data-stu-id="5214f-196">a.</span></span> <span data-ttu-id="5214f-197">按一下 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="5214f-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5214f-198">b.</span></span> <span data-ttu-id="5214f-199">在記事本中開啟您的 Base-64 編碼憑證、將其內容複製到剪貼簿，然後將它貼到 [SAML X.509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5214f-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="5214f-200">c.</span><span class="sxs-lookup"><span data-stu-id="5214f-200">c.</span></span> <span data-ttu-id="5214f-201">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5214f-202">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5214f-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5214f-203">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5214f-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5214f-204">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5214f-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5214f-205">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5214f-205">Create an Azure AD test user</span></span>

<span data-ttu-id="5214f-206">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5214f-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="5214f-208">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5214f-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5214f-209">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5214f-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5214f-211">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5214f-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5214f-213">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5214f-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5214f-215">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5214f-215">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5214f-217">a.</span><span class="sxs-lookup"><span data-stu-id="5214f-217">a.</span></span> <span data-ttu-id="5214f-218">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5214f-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5214f-219">b.</span><span class="sxs-lookup"><span data-stu-id="5214f-219">b.</span></span> <span data-ttu-id="5214f-220">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="5214f-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5214f-221">c.</span><span class="sxs-lookup"><span data-stu-id="5214f-221">c.</span></span> <span data-ttu-id="5214f-222">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="5214f-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5214f-223">d.</span><span class="sxs-lookup"><span data-stu-id="5214f-223">d.</span></span> <span data-ttu-id="5214f-224">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="5214f-225">建立 Litmos 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5214f-225">Create a Litmos test user</span></span>

<span data-ttu-id="5214f-226">本節的目標是要在 Litmos 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5214f-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="5214f-227">Litmos 應用程式支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="5214f-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="5214f-228">這表示，在使用存取面板嘗試存取應用程式期間，必要時會自動建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5214f-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="5214f-229">**若要在 Litmos 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5214f-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="5214f-230">在不同的瀏覽器視窗中，以系統管理員身分登入您的 Litmos 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5214f-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="5214f-231">在左側導覽列中，按一下 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![應用程式端的帳戶區段][22] 

3. <span data-ttu-id="5214f-233">按一下 [整合]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5214f-233">Click the **Integrations** tab.</span></span>
   
    ![整合索引標籤][23] 

4. <span data-ttu-id="5214f-235">在 [整合] 索引標籤上，向下捲動至 [協力廠商整合]，然後按一下 [SAML 2.0] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5214f-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="5214f-237">選取 [自動產生使用者]</span><span class="sxs-lookup"><span data-stu-id="5214f-237">Select **Autogenerate Users**</span></span>
   
    ![自動產生使用者][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5214f-239">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5214f-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="5214f-240">在本節中，您會將 Litmos 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5214f-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="5214f-242">**若要將 Britta Simon 指派給 Litmos，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5214f-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="5214f-243">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5214f-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5214f-245">在應用程式清單中，選取 [Litmos] 。</span><span class="sxs-lookup"><span data-stu-id="5214f-245">In the applications list, select **Litmos**.</span></span>

    ![應用程式清單中的 Litmos 連結](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="5214f-247">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5214f-247">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="5214f-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5214f-249">Click **Add** button.</span></span> <span data-ttu-id="5214f-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5214f-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="5214f-252">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5214f-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5214f-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5214f-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5214f-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5214f-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5214f-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5214f-255">Test single sign-on</span></span>

<span data-ttu-id="5214f-256">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="5214f-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="5214f-257">當您在「存取面板」中按一下 [Litmos] 磚時，應該會自動登入您的 [Litmos] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5214f-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5214f-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="5214f-258">Additional resources</span></span>

* [<span data-ttu-id="5214f-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5214f-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5214f-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5214f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

