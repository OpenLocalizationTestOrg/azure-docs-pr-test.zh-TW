---
title: "教學課程：Azure Active Directory 與 AirWatch 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 AirWatch 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="ae52c-103">教學課程：Azure Active Directory 與 AirWatch 整合</span><span class="sxs-lookup"><span data-stu-id="ae52c-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="ae52c-104">在本教學課程中，您將了解如何整合 AirWatch 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ae52c-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae52c-105">AirWatch 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ae52c-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae52c-106">您可以在 Azure AD 中控制可存取 AirWatch 的人員</span><span class="sxs-lookup"><span data-stu-id="ae52c-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="ae52c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 AirWatch (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ae52c-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae52c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ae52c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae52c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ae52c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae52c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ae52c-110">Prerequisites</span></span>

<span data-ttu-id="ae52c-111">若要設定 Azure AD 與 AirWatch 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ae52c-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="ae52c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ae52c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae52c-113">啟用 AirWatch 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ae52c-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae52c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ae52c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae52c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ae52c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae52c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ae52c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae52c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ae52c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae52c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ae52c-118">Scenario description</span></span>
<span data-ttu-id="ae52c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae52c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ae52c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae52c-121">從資源庫新增 AirWatch</span><span class="sxs-lookup"><span data-stu-id="ae52c-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="ae52c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ae52c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="ae52c-123">從資源庫新增 AirWatch</span><span class="sxs-lookup"><span data-stu-id="ae52c-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="ae52c-124">若要設定 AirWatch 與 Azure AD 整合，您需要從資源庫將 AirWatch 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ae52c-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae52c-125">**若要從資源庫新增 AirWatch，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ae52c-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae52c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ae52c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae52c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae52c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ae52c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae52c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ae52c-133">在搜尋方塊中，鍵入 **AirWatch**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-133">In the search box, type **AirWatch**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="ae52c-135">在結果窗格中，選取 [AirWatch]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae52c-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae52c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ae52c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae52c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 AirWatch 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae52c-139">若要讓單一登入運作，Azure AD 必須知道 AirWatch 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ae52c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="ae52c-140">換句話說，必須在 Azure AD 使用者和 AirWatch 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ae52c-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="ae52c-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 AirWatch 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="ae52c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="ae52c-142">若要設定及測試與 AirWatch 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ae52c-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae52c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ae52c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae52c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae52c-145">**[建立 AirWatch 測試使用者](#creating-a-airwatch-test-user)** - 在 AirWatch 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="ae52c-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae52c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae52c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ae52c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae52c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ae52c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae52c-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 AirWatch 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="ae52c-150">**若要設定與 AirWatch 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ae52c-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="ae52c-151">在 Azure 入口網站的 [AirWatch] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ae52c-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="ae52c-155">在 [AirWatch 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae52c-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="ae52c-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae52c-157">a.</span></span> <span data-ttu-id="ae52c-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="ae52c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="ae52c-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae52c-159">b.</span></span> <span data-ttu-id="ae52c-160">在 [識別碼] 文字方塊中，以 `AirWatch` 形式輸入值</span><span class="sxs-lookup"><span data-stu-id="ae52c-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae52c-161">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ae52c-161">This value is not the real.</span></span> <span data-ttu-id="ae52c-162">使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="ae52c-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="ae52c-163">請連絡 [AirWatch 用戶端支援小組](http://www.air-watch.com/company/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="ae52c-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="ae52c-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ae52c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="ae52c-166">在 [AirWatch 設定] 區段上，按一下 [設定 AirWatch] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ae52c-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae52c-167">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="ae52c-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae52c-169">Click **Save** button.</span></span>

    <span data-ttu-id="ae52c-170">![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="ae52c-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="ae52c-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 AirWatch 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ae52c-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="ae52c-172">在左側導覽窗格中按一下 [帳戶]，然後按一下 [系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="ae52c-173">![系統管理員](./media/active-directory-saas-airwatch-tutorial/ic791920.png "系統管理員")</span><span class="sxs-lookup"><span data-stu-id="ae52c-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="ae52c-174">展開 [設定] 功能表，然後按一下 [目錄服務]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="ae52c-175">![設定](./media/active-directory-saas-airwatch-tutorial/ic791921.png "設定")</span><span class="sxs-lookup"><span data-stu-id="ae52c-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="ae52c-176">按一下 [使用者] 索引標籤，在 [基準 DN] 文字方塊中輸入您的網域名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="ae52c-177">![使用者](./media/active-directory-saas-airwatch-tutorial/ic791922.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ae52c-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="ae52c-178">按一下 [伺服器]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ae52c-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="ae52c-179">![伺服器](./media/active-directory-saas-airwatch-tutorial/ic791923.png "伺服器")</span><span class="sxs-lookup"><span data-stu-id="ae52c-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="ae52c-180">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae52c-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="ae52c-181">![上傳](./media/active-directory-saas-airwatch-tutorial/ic791924.png "上傳")</span><span class="sxs-lookup"><span data-stu-id="ae52c-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="ae52c-182">a.</span><span class="sxs-lookup"><span data-stu-id="ae52c-182">a.</span></span> <span data-ttu-id="ae52c-183">針對 [目錄類型]，選取 [無]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="ae52c-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae52c-184">b.</span></span> <span data-ttu-id="ae52c-185">選取 [使用 SAML 進行驗證] 。</span><span class="sxs-lookup"><span data-stu-id="ae52c-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="ae52c-186">c.</span><span class="sxs-lookup"><span data-stu-id="ae52c-186">c.</span></span> <span data-ttu-id="ae52c-187">若要上傳已下載的憑證，請按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="ae52c-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="ae52c-188">在 [要求]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae52c-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="ae52c-189">![要求](./media/active-directory-saas-airwatch-tutorial/ic791925.png "要求")</span><span class="sxs-lookup"><span data-stu-id="ae52c-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="ae52c-190">a.</span><span class="sxs-lookup"><span data-stu-id="ae52c-190">a.</span></span> <span data-ttu-id="ae52c-191">針對 [要求繫結類型]，選取 [POST]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="ae52c-192">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae52c-192">b.</span></span> <span data-ttu-id="ae52c-193">在 Azure 入口網站的 [設定在 Airwatch 單一登入] 對話頁面上，複製 [SAML 單一登入服務 URL] 值，然後將它貼到 [識別提供者單一登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="ae52c-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="ae52c-194">c.</span><span class="sxs-lookup"><span data-stu-id="ae52c-194">c.</span></span> <span data-ttu-id="ae52c-195">針對 [NameID 格式]，選取 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="ae52c-196">d.</span><span class="sxs-lookup"><span data-stu-id="ae52c-196">d.</span></span> <span data-ttu-id="ae52c-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ae52c-197">Click **Save**.</span></span>

14. <span data-ttu-id="ae52c-198">再按一次 [使用者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ae52c-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="ae52c-199">![使用者](./media/active-directory-saas-airwatch-tutorial/ic791926.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ae52c-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="ae52c-200">在 [屬性]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae52c-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="ae52c-201">![屬性](./media/active-directory-saas-airwatch-tutorial/ic791927.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="ae52c-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="ae52c-202">a.</span><span class="sxs-lookup"><span data-stu-id="ae52c-202">a.</span></span> <span data-ttu-id="ae52c-203">在 [物件識別碼] 文字方塊中，輸入 **http://schemas.microsoft.com/identity/claims/objectidentifier**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="ae52c-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae52c-204">b.</span></span> <span data-ttu-id="ae52c-205">在 [使用者名稱] 文字方塊中，輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="ae52c-206">c.</span><span class="sxs-lookup"><span data-stu-id="ae52c-206">c.</span></span> <span data-ttu-id="ae52c-207">在 [顯示名稱] 文字方塊中，輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="ae52c-208">d.</span><span class="sxs-lookup"><span data-stu-id="ae52c-208">d.</span></span> <span data-ttu-id="ae52c-209">在 [名字] 文字方塊中，輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="ae52c-210">e.</span><span class="sxs-lookup"><span data-stu-id="ae52c-210">e.</span></span> <span data-ttu-id="ae52c-211">在 [姓氏] 文字方塊中，輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="ae52c-212">f.</span><span class="sxs-lookup"><span data-stu-id="ae52c-212">f.</span></span> <span data-ttu-id="ae52c-213">在 [電子郵件] 文字方塊中，輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="ae52c-214">g.</span><span class="sxs-lookup"><span data-stu-id="ae52c-214">g.</span></span> <span data-ttu-id="ae52c-215">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ae52c-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae52c-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ae52c-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae52c-217">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ae52c-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ae52c-219">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ae52c-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae52c-220">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ae52c-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae52c-222">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae52c-224">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae52c-226">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae52c-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae52c-228">a.</span><span class="sxs-lookup"><span data-stu-id="ae52c-228">a.</span></span> <span data-ttu-id="ae52c-229">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ae52c-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae52c-230">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae52c-230">b.</span></span> <span data-ttu-id="ae52c-231">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="ae52c-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="ae52c-232">c.</span><span class="sxs-lookup"><span data-stu-id="ae52c-232">c.</span></span> <span data-ttu-id="ae52c-233">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ae52c-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae52c-234">d.</span><span class="sxs-lookup"><span data-stu-id="ae52c-234">d.</span></span> <span data-ttu-id="ae52c-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ae52c-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="ae52c-236">建立 AirWatch 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ae52c-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="ae52c-237">若要讓 Azure AD 使用者能夠登入 AirWatch，必須將他們佈建到 AirWatch。</span><span class="sxs-lookup"><span data-stu-id="ae52c-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="ae52c-238">AirWatch 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="ae52c-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="ae52c-239">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ae52c-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ae52c-240">以系統管理員身分登入您的 **AirWatch** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ae52c-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="ae52c-241">在左側導覽窗格中按一下 [帳戶]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="ae52c-242">![使用者](./media/active-directory-saas-airwatch-tutorial/ic791929.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ae52c-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="ae52c-243">在 [使用者] 功能表中，按一下 [清單檢視]，然後按一下 [新增] \> [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="ae52c-244">![新增使用者](./media/active-directory-saas-airwatch-tutorial/ic791930.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="ae52c-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="ae52c-245">在 [新增/編輯使用者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae52c-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="ae52c-246">![新增使用者](./media/active-directory-saas-airwatch-tutorial/ic791931.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="ae52c-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="ae52c-247">在相關的文字方塊中，輸入您想要佈建之有效 Azure Active Directory 帳戶的 [使用者名稱]、[密碼]、[確認密碼]、[名字]、[姓氏]、[電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="ae52c-248">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ae52c-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="ae52c-249">您可以使用任何其他的 AirWatch 使用者帳戶建立工具或 AirWatch 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae52c-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae52c-250">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ae52c-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae52c-251">在本節中，您會將 AirWatch 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ae52c-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![指派使用者][200] 

<span data-ttu-id="ae52c-253">**若要將 Britta Simon 指派給 AirWatch，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ae52c-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="ae52c-254">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ae52c-256">在應用程式清單中，選取 [AirWatch]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-256">In the applications list, select **AirWatch**.</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="ae52c-258">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-258">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ae52c-260">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae52c-260">Click **Add** button.</span></span> <span data-ttu-id="ae52c-261">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ae52c-263">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ae52c-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae52c-264">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae52c-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae52c-265">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae52c-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae52c-266">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ae52c-266">Testing single sign-on</span></span>

<span data-ttu-id="ae52c-267">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ae52c-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae52c-268">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="ae52c-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ae52c-269">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ae52c-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ae52c-270">其他資源</span><span class="sxs-lookup"><span data-stu-id="ae52c-270">Additional resources</span></span>

* [<span data-ttu-id="ae52c-271">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ae52c-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae52c-272">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ae52c-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

