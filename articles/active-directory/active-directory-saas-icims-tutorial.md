---
title: "教學課程：Azure Active Directory 與 ICIMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ICIMS 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="16fab-103">教學課程：Azure Active Directory 與 ICIMS 整合</span><span class="sxs-lookup"><span data-stu-id="16fab-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="16fab-104">在本教學課程中，您將了解如何整合 ICIMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="16fab-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16fab-105">ICIMS 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="16fab-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16fab-106">您可以在 Azure AD 中控制可存取 ICIMS 的人員</span><span class="sxs-lookup"><span data-stu-id="16fab-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="16fab-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ICIMS (單一登入)</span><span class="sxs-lookup"><span data-stu-id="16fab-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16fab-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="16fab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16fab-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="16fab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16fab-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="16fab-110">Prerequisites</span></span>

<span data-ttu-id="16fab-111">若要設定 Azure AD 與 ICIMS 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="16fab-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="16fab-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="16fab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16fab-113">已啟用 ICIMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="16fab-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16fab-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="16fab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16fab-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="16fab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16fab-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="16fab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16fab-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="16fab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16fab-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="16fab-118">Scenario description</span></span>
<span data-ttu-id="16fab-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16fab-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="16fab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16fab-121">從資源庫新增 ICIMS</span><span class="sxs-lookup"><span data-stu-id="16fab-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="16fab-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="16fab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="16fab-123">從資源庫新增 ICIMS</span><span class="sxs-lookup"><span data-stu-id="16fab-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="16fab-124">若要設定將 ICIMS 整合到 Azure AD 中，您需要從資源庫將 ICIMS 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="16fab-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16fab-125">**若要從資源庫新增 ICIMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="16fab-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16fab-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="16fab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="16fab-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="16fab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16fab-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="16fab-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="16fab-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16fab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="16fab-133">在搜尋方塊中，輸入 **ICIMS**，從結果面板中選取 [ICIMS]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="16fab-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="16fab-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="16fab-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="16fab-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 ICIMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16fab-137">若要讓單一登入運作，Azure AD 必須知道 ICIMS 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="16fab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="16fab-138">換句話說，必須在 Azure AD 使用者和 ICIMS 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="16fab-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="16fab-139">在 ICIMS 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="16fab-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="16fab-140">若要設定及測試與 ICIMS 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="16fab-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16fab-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="16fab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16fab-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16fab-143">**[建立 ICIMS 測試使用者](#create-an-icims-test-user)** - 使 ICIMS 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="16fab-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16fab-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16fab-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="16fab-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="16fab-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="16fab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="16fab-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 ICIMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="16fab-148">**若要設定與 ICIMS 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="16fab-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="16fab-149">在 Azure 入口網站的 [ICIMS] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="16fab-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="16fab-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="16fab-153">在 [ICIMS 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="16fab-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![ICIMS 網域及 URL 單一登入資訊](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="16fab-155">a.</span><span class="sxs-lookup"><span data-stu-id="16fab-155">a.</span></span> <span data-ttu-id="16fab-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="16fab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="16fab-157">b.</span><span class="sxs-lookup"><span data-stu-id="16fab-157">b.</span></span> <span data-ttu-id="16fab-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="16fab-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="16fab-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="16fab-159">These values are not real.</span></span> <span data-ttu-id="16fab-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="16fab-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="16fab-161">請連絡 [ICIMS 用戶端支援小組](https://www.icims.com/contact-us)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="16fab-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="16fab-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="16fab-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="16fab-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="16fab-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16fab-166">在 [ICIMS 設定] 區段上，按一下 [設定 ICIMS] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="16fab-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="16fab-167">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="16fab-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ICIMS 組態](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="16fab-169">若要在 **ICIMS** 端設定單一登入，您需要將所下載的**中繼資料 XML**、**登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL** 傳送給 [ICIMS 支援小組](https://www.icims.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="16fab-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="16fab-170">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="16fab-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="16fab-171">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="16fab-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16fab-172">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="16fab-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16fab-173">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16fab-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="16fab-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="16fab-174">Create an Azure AD test user</span></span>
<span data-ttu-id="16fab-175">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="16fab-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="16fab-177">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="16fab-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16fab-178">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="16fab-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16fab-180">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="16fab-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16fab-182">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="16fab-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16fab-184">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="16fab-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16fab-186">a.</span><span class="sxs-lookup"><span data-stu-id="16fab-186">a.</span></span> <span data-ttu-id="16fab-187">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="16fab-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16fab-188">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="16fab-188">b.</span></span> <span data-ttu-id="16fab-189">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="16fab-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16fab-190">c.</span><span class="sxs-lookup"><span data-stu-id="16fab-190">c.</span></span> <span data-ttu-id="16fab-191">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="16fab-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16fab-192">d.</span><span class="sxs-lookup"><span data-stu-id="16fab-192">d.</span></span> <span data-ttu-id="16fab-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="16fab-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="16fab-194">建立 ICIMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="16fab-194">Create an ICIMS test user</span></span>

<span data-ttu-id="16fab-195">本節的目標是在 ICIMS 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="16fab-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="16fab-196">請與 [ ICIMS 支援小組](https://www.icims.com/contact-us)合作，在 ICIMS 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="16fab-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="16fab-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="16fab-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="16fab-198">在本節中，您會將 ICIMS 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="16fab-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![指派使用者角色][200]

<span data-ttu-id="16fab-200">**若要將 Britta Simon 指派給 ICIMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="16fab-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="16fab-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="16fab-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="16fab-203">在應用程式清單中，選取 [ICIMS] 。</span><span class="sxs-lookup"><span data-stu-id="16fab-203">In the applications list, select **ICIMS**.</span></span>

    ![應用程式清單中的 ICIMS 連結](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="16fab-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="16fab-205">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="16fab-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16fab-207">Click **Add** button.</span></span> <span data-ttu-id="16fab-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="16fab-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="16fab-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="16fab-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16fab-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16fab-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16fab-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16fab-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="16fab-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="16fab-213">Test single sign-on</span></span>

<span data-ttu-id="16fab-214">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="16fab-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="16fab-215">當您在存取面板中按一下 [ICIMS] 磚時，應該會自動登入您的 ICIMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16fab-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16fab-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="16fab-216">Additional resources</span></span>

* [<span data-ttu-id="16fab-217">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="16fab-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16fab-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="16fab-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

