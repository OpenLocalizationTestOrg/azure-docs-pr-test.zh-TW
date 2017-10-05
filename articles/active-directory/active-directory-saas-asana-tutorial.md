---
title: "教學課程：Azure Active Directory 與 Asana 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Asana 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: a2f0cecb93cc382bcfd710c44eb70f80ae67f9b6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="7cde7-103">教學課程：Azure Active Directory 與 Asana 整合</span><span class="sxs-lookup"><span data-stu-id="7cde7-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="7cde7-104">在本教學課程中，您會了解如何整合 Asana 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7cde7-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cde7-105">將 Asana 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7cde7-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7cde7-106">您可以在 Azure AD 中控制可存取 Asana 的人員</span><span class="sxs-lookup"><span data-stu-id="7cde7-106">You can control in Azure AD who has access to Asana</span></span>
- <span data-ttu-id="7cde7-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Asana (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7cde7-107">You can enable your users to automatically get signed-on to Asana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7cde7-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7cde7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7cde7-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7cde7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cde7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7cde7-110">Prerequisites</span></span>

<span data-ttu-id="7cde7-111">若要設定與 Asana 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7cde7-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

- <span data-ttu-id="7cde7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7cde7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cde7-113">已啟用 Asana 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7cde7-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cde7-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7cde7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cde7-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7cde7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cde7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7cde7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cde7-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7cde7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cde7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7cde7-118">Scenario description</span></span>
<span data-ttu-id="7cde7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cde7-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7cde7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cde7-121">從資源庫新增 Asana</span><span class="sxs-lookup"><span data-stu-id="7cde7-121">Adding Asana from the gallery</span></span>
2. <span data-ttu-id="7cde7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7cde7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="7cde7-123">從資源庫新增 Asana</span><span class="sxs-lookup"><span data-stu-id="7cde7-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="7cde7-124">若要設定將 Asana 整合到 Azure AD 中，您需要從資源庫將 Asana 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7cde7-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7cde7-125">**若要從資源庫加入 Asana，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cde7-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7cde7-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7cde7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="7cde7-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7cde7-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="7cde7-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cde7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="7cde7-133">在搜尋方塊中，輸入 **Asana**，從結果面板中選取 [Asana]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cde7-133">In the search box, type **Asana**, select **Asana** from result panel then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7cde7-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7cde7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7cde7-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Asana 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7cde7-137">若要讓單一登入能夠運作，Azure AD 必須知道 Asana 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7cde7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="7cde7-138">換句話說，必須在 Azure AD 使用者與 Asana 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7cde7-138">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="7cde7-139">在 Asana 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7cde7-139">In Asana, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7cde7-140">若要設定及測試與 Asana 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="7cde7-140">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7cde7-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7cde7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7cde7-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cde7-143">**[建立 Asana 測試使用者](#create-an-asana-test-user)** - 在 Asana 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="7cde7-143">**[Create an Asana test user](#create-an-asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cde7-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cde7-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7cde7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7cde7-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7cde7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7cde7-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Asana 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="7cde7-148">**若要設定與 Asana 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cde7-148">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="7cde7-149">在 Azure 入口網站的 [Asana] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-149">In the Azure portal, on the **Asana** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7cde7-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="7cde7-153">在 [Asana 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cde7-153">On the **Asana Domain and URLs** section, perform the following steps:</span></span>

    ![Asana 網域與 URL 單一登入資訊](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="7cde7-155">a.</span><span class="sxs-lookup"><span data-stu-id="7cde7-155">a.</span></span> <span data-ttu-id="7cde7-156">在 [登入 URL] 文字方塊中，輸入 URL：`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="7cde7-156">In the **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="7cde7-157">b.</span><span class="sxs-lookup"><span data-stu-id="7cde7-157">b.</span></span> <span data-ttu-id="7cde7-158">在 [識別碼] 文字方塊中，輸入值：`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="7cde7-158">In the **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="7cde7-159">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7cde7-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="7cde7-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cde7-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7cde7-163">在 [Asana 組態] 區段上，按一下 [設定 Asana] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7cde7-163">On the **Asana Configuration** section, click **Configure Asana** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7cde7-164">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Asana 設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="7cde7-166">在不同的瀏覽器視窗中，登入您的 Asana 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cde7-166">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="7cde7-167">若要在 Asana 中設定 SSO，請按一下螢幕右上角的工作區名稱來存取工作區設定。</span><span class="sxs-lookup"><span data-stu-id="7cde7-167">To configure SSO in Asana, access the workspace settings by clicking the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="7cde7-168">然後，按一下 [\<您的工作區名稱\> 設定]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Asana sso 設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="7cde7-170">在 [組織設定] 視窗中，按一下 [管理]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-170">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="7cde7-171">然後按一下 [成員必須透過 SAML 登入]  以啟用 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="7cde7-171">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="7cde7-172">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cde7-172">The perform the following steps:</span></span>
   
    ![設定單一登入組織設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="7cde7-174">a.</span><span class="sxs-lookup"><span data-stu-id="7cde7-174">a.</span></span> <span data-ttu-id="7cde7-175">在 [登入頁面 URL] 文字方塊中，貼上「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="7cde7-175">In the **Sign-in page URL** textbox, paste the **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="7cde7-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cde7-176">b.</span></span> <span data-ttu-id="7cde7-177">在從 Azure 入口網站下載的憑證上按一下滑鼠右鍵，然後使用「記事本」或您慣用的文字編輯器來開啟該憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="7cde7-177">Right click the certificate downloaded from Azure portal, then open the certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="7cde7-178">複製開始和結束憑證標題之間的內容，然後將它貼到 [X.509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7cde7-178">Copy the content between the begin and the end certificate title and paste it in the **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="7cde7-179">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7cde7-179">Click **Save**.</span></span> <span data-ttu-id="7cde7-180">如需進一步協助，請移至 [用於設定 SSO 的 Asana 指南](https://asana.com/guide/help/premium/authentication#gl-saml) 。</span><span class="sxs-lookup"><span data-stu-id="7cde7-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="7cde7-181">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7cde7-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7cde7-182">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7cde7-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7cde7-183">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7cde7-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7cde7-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7cde7-184">Create an Azure AD test user</span></span>

<span data-ttu-id="7cde7-185">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7cde7-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="7cde7-187">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cde7-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7cde7-188">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7cde7-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7cde7-190">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7cde7-192">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7cde7-194">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cde7-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7cde7-196">a.</span><span class="sxs-lookup"><span data-stu-id="7cde7-196">a.</span></span> <span data-ttu-id="7cde7-197">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7cde7-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cde7-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cde7-198">b.</span></span> <span data-ttu-id="7cde7-199">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7cde7-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7cde7-200">c.</span><span class="sxs-lookup"><span data-stu-id="7cde7-200">c.</span></span> <span data-ttu-id="7cde7-201">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7cde7-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7cde7-202">d.</span><span class="sxs-lookup"><span data-stu-id="7cde7-202">d.</span></span> <span data-ttu-id="7cde7-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7cde7-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="7cde7-204">建立 Asana 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7cde7-204">Create an Asana test user</span></span>

<span data-ttu-id="7cde7-205">在本節中，您要在 Asana 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7cde7-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="7cde7-206">在 [Asana] 移至左面板上的 [小組] 區段。</span><span class="sxs-lookup"><span data-stu-id="7cde7-206">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="7cde7-207">按一下加號按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cde7-207">Click the plus sign button.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="7cde7-209">在文字方塊中輸入電子郵件 britta.simon@contoso.com，然後選取 [邀請]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-209">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>

3. <span data-ttu-id="7cde7-210">按一下 [傳送邀請] 。</span><span class="sxs-lookup"><span data-stu-id="7cde7-210">Click **Send Invite**.</span></span> <span data-ttu-id="7cde7-211">新的使用者會在她的電子郵件帳戶收到一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="7cde7-211">The new user will receive an email into her email account.</span></span> <span data-ttu-id="7cde7-212">她將需要建立並驗證帳戶。</span><span class="sxs-lookup"><span data-stu-id="7cde7-212">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7cde7-213">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7cde7-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="7cde7-214">在本節中，您會將 Asana 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asana.</span></span>

![指派使用者角色][200]

<span data-ttu-id="7cde7-216">**若要將 Britta Simon 指派給 Asana，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cde7-216">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="7cde7-217">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7cde7-219">在應用程式清單中，選取 [Asana]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-219">In the applications list, select **Asana**.</span></span>

    ![應用程式清單中的 Asana 連結](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="7cde7-221">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-221">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="7cde7-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cde7-223">Click **Add** button.</span></span> <span data-ttu-id="7cde7-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="7cde7-226">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7cde7-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cde7-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cde7-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cde7-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7cde7-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7cde7-229">Test single sign-on</span></span>

<span data-ttu-id="7cde7-230">本節的目標是要測試您的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-230">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="7cde7-231">移至 Asana 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="7cde7-231">Go to Asana login page.</span></span> <span data-ttu-id="7cde7-232">在 [電子郵件地址] 文字方塊中，插入電子郵件地址 britta.simon@contoso.com。讓 [密碼] 文字方塊保持空白，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="7cde7-232">In the Email address textbox, insert the email address britta.simon@contoso.com. Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="7cde7-233">系統會將您重新導向至 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="7cde7-233">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="7cde7-234">完成您的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="7cde7-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="7cde7-235">現在，您已在 Asana 上登入。</span><span class="sxs-lookup"><span data-stu-id="7cde7-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7cde7-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="7cde7-236">Additional resources</span></span>

* [<span data-ttu-id="7cde7-237">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7cde7-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cde7-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7cde7-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
