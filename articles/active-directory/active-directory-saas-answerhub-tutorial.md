---
title: "教學課程：Azure Active Directory 與 AnswerHub 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 AnswerHub 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="ed289-103">教學課程：Azure Active Directory 與 AnswerHub 整合</span><span class="sxs-lookup"><span data-stu-id="ed289-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="ed289-104">在本教學課程中，您會了解如何將 AnswerHub 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="ed289-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed289-105">將 AnswerHub 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ed289-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed289-106">您可以在 Azure AD 中控制可存取 AnswerHub 的人員</span><span class="sxs-lookup"><span data-stu-id="ed289-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="ed289-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 AnswerHub (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ed289-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed289-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ed289-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ed289-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ed289-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed289-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed289-110">Prerequisites</span></span>

<span data-ttu-id="ed289-111">若要設定 Azure AD 與 AnswerHub 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ed289-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="ed289-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ed289-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed289-113">已啟用 AnswerHub 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ed289-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed289-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ed289-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed289-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ed289-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed289-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ed289-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed289-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ed289-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed289-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ed289-118">Scenario description</span></span>
<span data-ttu-id="ed289-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed289-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ed289-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed289-121">從資源庫新增 AnswerHub</span><span class="sxs-lookup"><span data-stu-id="ed289-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="ed289-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed289-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="ed289-123">從資源庫新增 AnswerHub</span><span class="sxs-lookup"><span data-stu-id="ed289-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="ed289-124">若要設定將 AnswerHub 整合到 Azure AD 中，您需要從資源庫將 AnswerHub 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ed289-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed289-125">**若要從資源庫新增 AnswerHub，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed289-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed289-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ed289-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed289-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed289-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed289-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed289-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ed289-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed289-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ed289-133">在搜尋方塊中，輸入 **AnswerHub**。</span><span class="sxs-lookup"><span data-stu-id="ed289-133">In the search box, type **AnswerHub**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="ed289-135">在結果面板中，選取 [AnswerHub]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed289-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed289-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed289-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed289-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 AnswerHub 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed289-139">若要讓單一登入能夠運作，Azure AD 必須知道 AnswerHub 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ed289-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="ed289-140">換句話說，必須在 Azure AD 使用者與 AnswerHub 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ed289-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="ed289-141">在 AnswerHub 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ed289-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ed289-142">若要設定及測試與 AnswerHub 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ed289-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed289-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ed289-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed289-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed289-145">**[建立 AnswerHub 測試使用者](#creating-an-answerhub-test-user)** - 在 AnswerHub 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="ed289-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed289-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed289-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ed289-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed289-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed289-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed289-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 AnswerHub 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="ed289-150">**若要設定與 AnswerHub 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed289-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="ed289-151">在 Azure 入口網站的 [AnswerHub] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ed289-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ed289-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="ed289-155">在 [AnswerHub 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ed289-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="ed289-157">a.</span><span class="sxs-lookup"><span data-stu-id="ed289-157">a.</span></span> <span data-ttu-id="ed289-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="ed289-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="ed289-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed289-159">b.</span></span> <span data-ttu-id="ed289-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="ed289-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed289-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ed289-161">These values are not real.</span></span> <span data-ttu-id="ed289-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ed289-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ed289-163">請連絡 [AnswerHub 用戶端支援小組](mailto:success@answerhub.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="ed289-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="ed289-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ed289-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="ed289-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed289-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ed289-168">在 [AnswerHub 組態] 區段上，按一下 [設定 AnswerHub] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ed289-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ed289-169">從 [快速參考] 區段中複製「登出 URL」和「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="ed289-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="ed289-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 AnswerHub 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ed289-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ed289-172">如果您需要設定 AnswerHub 的協助，請連絡 [AnswerHub 的支援小組](mailto:success@answerhub.com.)。</span><span class="sxs-lookup"><span data-stu-id="ed289-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="ed289-173">移至 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="ed289-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="ed289-174">按一下 [使用者和群組]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ed289-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="ed289-175">在左側瀏覽窗格的 [社交設定] 區段中，按一下 [SAML 設定]。</span><span class="sxs-lookup"><span data-stu-id="ed289-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="ed289-176">按一下 [IDP 設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ed289-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="ed289-177">在 [IDP 設定]  索引標籤上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ed289-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="ed289-178">![SAML 設定](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="ed289-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="ed289-179">a.</span><span class="sxs-lookup"><span data-stu-id="ed289-179">a.</span></span> <span data-ttu-id="ed289-180">在 [IDP 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="ed289-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="ed289-181">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed289-181">b.</span></span> <span data-ttu-id="ed289-182">在 [IDP 登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的「登出 URL」。</span><span class="sxs-lookup"><span data-stu-id="ed289-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="ed289-183">c.</span><span class="sxs-lookup"><span data-stu-id="ed289-183">c.</span></span> <span data-ttu-id="ed289-184">在 [IDP 名稱識別碼格式] 文字方塊中，輸入與在 Azure 入口網站的 [使用者屬性] 區段中所選相同的使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ed289-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="ed289-185">d.</span><span class="sxs-lookup"><span data-stu-id="ed289-185">d.</span></span> <span data-ttu-id="ed289-186">按一下 [金鑰和憑證] 。</span><span class="sxs-lookup"><span data-stu-id="ed289-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="ed289-187">在 [金鑰和憑證] 索引標籤上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ed289-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="ed289-188">![金鑰和憑證](./media/active-directory-saas-answerhub-tutorial/ic785173.png "金鑰和憑證")</span><span class="sxs-lookup"><span data-stu-id="ed289-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="ed289-189">a.</span><span class="sxs-lookup"><span data-stu-id="ed289-189">a.</span></span> <span data-ttu-id="ed289-190">在記事本中開啟您從 Azure 入口網站下載的 Base-64 編碼憑證，將其內容複製到剪貼簿，然後貼到 [IDP 公開金鑰 (x509 格式)] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="ed289-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="ed289-191">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed289-191">b.</span></span> <span data-ttu-id="ed289-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ed289-192">Click **Save**.</span></span>

14. <span data-ttu-id="ed289-193">在 [IDP 設定] 索引標籤上，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ed289-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ed289-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ed289-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ed289-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ed289-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ed289-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed289-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed289-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed289-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed289-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ed289-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ed289-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed289-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed289-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ed289-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed289-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ed289-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed289-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ed289-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed289-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ed289-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed289-209">a.</span><span class="sxs-lookup"><span data-stu-id="ed289-209">a.</span></span> <span data-ttu-id="ed289-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ed289-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed289-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed289-211">b.</span></span> <span data-ttu-id="ed289-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ed289-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed289-213">c.</span><span class="sxs-lookup"><span data-stu-id="ed289-213">c.</span></span> <span data-ttu-id="ed289-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ed289-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ed289-215">d.</span><span class="sxs-lookup"><span data-stu-id="ed289-215">d.</span></span> <span data-ttu-id="ed289-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ed289-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="ed289-217">建立 AnswerHub 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed289-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="ed289-218">若要讓 Azure AD 使用者能夠登入 AnswerHub，必須將他們佈建到 AnswerHub。</span><span class="sxs-lookup"><span data-stu-id="ed289-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="ed289-219">就 AnswerHub 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="ed289-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="ed289-220">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed289-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ed289-221">以系統管理員身分登入您的 **AnswerHub** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ed289-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="ed289-222">移至 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="ed289-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="ed289-223">按一下 [使用者和群組] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ed289-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="ed289-224">在左側瀏覽窗格的 [管理使用者] 區段中，按一下 [建立或匯入使用者]。</span><span class="sxs-lookup"><span data-stu-id="ed289-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="ed289-225">![使用者和群組](./media/active-directory-saas-answerhub-tutorial/ic785175.png "使用者和群組")</span><span class="sxs-lookup"><span data-stu-id="ed289-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="ed289-226">在相關的文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的 [電子郵件地址]、[使用者名稱] 和 [密碼]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ed289-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="ed289-227">您可以使用任何其他的 AnswerHub 使用者帳戶建立工具或 AnswerHub 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed289-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ed289-228">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed289-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ed289-229">在本節中，您會將 AnswerHub 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed289-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![指派使用者][200] 

<span data-ttu-id="ed289-231">**若要將 Britta Simon 指派給 AnswerHub，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed289-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="ed289-232">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed289-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ed289-234">在應用程式清單中，選取 [AnswerHub]。</span><span class="sxs-lookup"><span data-stu-id="ed289-234">In the applications list, select **AnswerHub**.</span></span>

    ![設定單一登入](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="ed289-236">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ed289-236">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ed289-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed289-238">Click **Add** button.</span></span> <span data-ttu-id="ed289-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ed289-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ed289-241">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ed289-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ed289-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed289-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed289-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed289-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed289-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ed289-244">Testing single sign-on</span></span>

<span data-ttu-id="ed289-245">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ed289-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ed289-246">當您在「存取面板」中按一下 [AnswerHub] 圖格時，應該會自動登入您的 AnswerHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed289-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="ed289-247">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ed289-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed289-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="ed289-248">Additional resources</span></span>

* [<span data-ttu-id="ed289-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ed289-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed289-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ed289-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

