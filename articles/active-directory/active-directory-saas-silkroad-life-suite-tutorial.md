---
title: "教學課程：Azure Active Directory 與 SilkRoad Life Suite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SilkRoad Life Suite 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="08c92-103">教學課程：Azure Active Directory 與 SilkRoad Life Suite 整合</span><span class="sxs-lookup"><span data-stu-id="08c92-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="08c92-104">本教學課程旨在說明如何整合 SilkRoad Life Suite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="08c92-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="08c92-105">SilkRoad Life Suite 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="08c92-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="08c92-106">您可以在 Azure AD 中控制可存取 SilkRoad Life Suite 的人員</span><span class="sxs-lookup"><span data-stu-id="08c92-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="08c92-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SilkRoad Life Suite 單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="08c92-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="08c92-108">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="08c92-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08c92-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="08c92-109">Prerequisites</span></span>
<span data-ttu-id="08c92-110">若要設定與 SilkRoad Life Suite 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="08c92-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="08c92-111">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="08c92-111">An Azure AD subscription</span></span>
* <span data-ttu-id="08c92-112">已啟用 SilkRoad Life Suite SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="08c92-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="08c92-113">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="08c92-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="08c92-114">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="08c92-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="08c92-115">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="08c92-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="08c92-116">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="08c92-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="08c92-117">案例描述</span><span class="sxs-lookup"><span data-stu-id="08c92-117">Scenario Description</span></span>
<span data-ttu-id="08c92-118">此教學課程的目標是讓您在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="08c92-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="08c92-119">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="08c92-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08c92-120">從資源庫加入 SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="08c92-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="08c92-121">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="08c92-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="08c92-122">從資源庫加入 SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="08c92-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="08c92-123">若要設定 SilkRoad Life Suite 與 Azure AD 整合，您需要從資源庫將 SilkRoad Life Suite 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="08c92-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="08c92-124">**若要從資源庫新增 SilkRoad Life Suite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08c92-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="08c92-125">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="08c92-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="08c92-127">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="08c92-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="08c92-128">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="08c92-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2]

4. <span data-ttu-id="08c92-130">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="08c92-130">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]

5. <span data-ttu-id="08c92-132">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="08c92-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4]

6. <span data-ttu-id="08c92-134">在 [搜尋] 方塊中，輸入 **SilkRoad Life Suite**。</span><span class="sxs-lookup"><span data-stu-id="08c92-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![應用程式][5]

7. <span data-ttu-id="08c92-136">在結果窗格中，選取 [SilkRoad Life Suite]，然後按一下 [完成] 以加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="08c92-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![應用程式][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="08c92-138">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="08c92-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="08c92-139">本節的目標是說明如何以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 SilkRoad Life Suite 搭配運作的 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="08c92-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08c92-140">若要讓 SSO 能夠運作，Azure AD 必須知道 SilkRoad Life Suite 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="08c92-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="08c92-141">換句話說，Azure AD 使用者和 SilkRoad Life Suite 中的相關使用者之間必須建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="08c92-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="08c92-142">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 SilkRoad Life Suite 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="08c92-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="08c92-143">若要設定及測試對 SilkRoad Life Suite 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="08c92-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="08c92-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="08c92-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="08c92-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08c92-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08c92-146">**[建立 SilkRoad Life Suite 測試使用者](#creating-a-silkroad-life-suite-test-user)** - 使 SilkRoad Life Suite 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="08c92-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="08c92-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08c92-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08c92-148">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="08c92-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="08c92-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="08c92-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="08c92-150">本節的目標是要在 Azure 傳統入口網站中啟用 Azure AD SSO，並在您的 SilkRoad Life Suite 應用程式中設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="08c92-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="08c92-151">**若要使用 SilkRoad Life Suite 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08c92-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="08c92-152">以系統管理員身分登入您的 SilkRoad 公司網站。</span><span class="sxs-lookup"><span data-stu-id="08c92-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="08c92-153">若要取得用於設定與 Microsoft Azure AD 的同盟存取的 SilkRoad Life Suite 驗證應用程式，請連絡 SilkRoad 支援人員或您的 SilkRoad 服務代表。</span><span class="sxs-lookup"><span data-stu-id="08c92-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="08c92-154">移至 [服務提供者]，然後按一下 [同盟詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="08c92-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD 單一登入][10] 

3. <span data-ttu-id="08c92-156">按一下 [下載同盟中繼資料] ，然後將資料檔儲存在您的電腦中。</span><span class="sxs-lookup"><span data-stu-id="08c92-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD 單一登入][11] 

4. <span data-ttu-id="08c92-158">在 Azure 傳統入口網站的 [SilkRoad Life Suite] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="08c92-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 

5. <span data-ttu-id="08c92-160">在 [您希望使用者如何登入 SilkRoad Life Suite] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="08c92-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][7] 

6. <span data-ttu-id="08c92-162">在 [設定應用程式設定]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 單一登入][8]   
 1. <span data-ttu-id="08c92-164">在 [登入 URL] 文字方塊中，輸入您的使用者用來登入 SilkRoad Life Suite 網站的 URL (例如：*https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*)。</span><span class="sxs-lookup"><span data-stu-id="08c92-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="08c92-165">開啟下載的 **Silkroad** 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="08c92-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="08c92-166">找到 **AssertionConsumerService** 標籤，然後複製 **Location** 屬性。</span><span class="sxs-lookup"><span data-stu-id="08c92-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Azure AD 單一登入][21] 
 4. <span data-ttu-id="08c92-168">請將該值貼入 [回覆 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="08c92-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="08c92-169">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-169">Click **Next**.</span></span>

6. <span data-ttu-id="08c92-170">在 [設定在 SilkRoad Life Suite 單一登入]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Azure AD 單一登入][9]  
 1. <span data-ttu-id="08c92-172">按一下 [下載憑證]，然後將檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="08c92-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="08c92-173">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-173">Click **Next**.</span></span>

7. <span data-ttu-id="08c92-174">在您的 **SilkRoad** 應用程式中，按一下 [驗證來源]。</span><span class="sxs-lookup"><span data-stu-id="08c92-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD 單一登入][12] 

8. <span data-ttu-id="08c92-176">按一下 [加入驗證來源] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD 單一登入][13] 

9. <span data-ttu-id="08c92-178">在 [加入驗證來源]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD 單一登入][14]  
 1. <span data-ttu-id="08c92-180">在 [選項 2 - 中繼資料檔案] 下，按一下 [瀏覽] 來上傳下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="08c92-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="08c92-181">按一下 [使用檔案資料建立身分識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="08c92-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="08c92-182">在 [驗證來源] 區段中，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="08c92-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD 單一登入][15] 

11. <span data-ttu-id="08c92-184">在 [編輯驗證來源]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD 單一登入][16] 
 1. <span data-ttu-id="08c92-186">對 [已啟用] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="08c92-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="08c92-187">在 [IdP 描述] 文字方塊中，輸入您的組態描述 (例如：*Azure AD SSO*)。</span><span class="sxs-lookup"><span data-stu-id="08c92-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="08c92-188">在 [IdP 名稱] 文字方塊中，輸入組態特定的名稱 (例如：*Azure SP*)。</span><span class="sxs-lookup"><span data-stu-id="08c92-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="08c92-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-189">Click **Save**.</span></span>

12. <span data-ttu-id="08c92-190">停用所有其他驗證來源。</span><span class="sxs-lookup"><span data-stu-id="08c92-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD 單一登入][17]

13. <span data-ttu-id="08c92-192">在 Azure 傳統入口網站的 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="08c92-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD 單一登入][18]

14. <span data-ttu-id="08c92-194">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="08c92-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD 單一登入][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="08c92-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="08c92-196">Create an Azure AD test user</span></span>
<span data-ttu-id="08c92-197">本節的目標是要在 Azure 傳統入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="08c92-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="08c92-199">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08c92-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="08c92-200">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="08c92-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="08c92-202">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="08c92-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="08c92-203">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08c92-205">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="08c92-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="08c92-207">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="08c92-209">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="08c92-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="08c92-210">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="08c92-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="08c92-211">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-211">Click **Next**.</span></span>

6. <span data-ttu-id="08c92-212">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="08c92-214">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="08c92-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="08c92-215">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="08c92-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="08c92-216">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="08c92-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="08c92-217">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="08c92-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="08c92-218">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-218">Click **Next**.</span></span>

7. <span data-ttu-id="08c92-219">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="08c92-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="08c92-221">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08c92-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="08c92-223">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="08c92-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="08c92-224">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="08c92-225">建立 SilkRoad Life Suite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="08c92-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="08c92-226">本節目標是在 SilkRoad Life Suite 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="08c92-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="08c92-227">Britta 必須具備符合 Britta 在 Azure AD 中 *電子郵件位址*的 SSO 識別碼 (有時稱為 **AuthParam** )。</span><span class="sxs-lookup"><span data-stu-id="08c92-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="08c92-228">**若要在 SilkRoad Life Suite 中建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="08c92-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="08c92-229">要求您的 SilkRoad Life Suite 支援小組建立一個使用者，其 **SSO ID** 屬性與 Azure AD 中 Britta Simon 的 **emailaddress** 屬性的值相同。</span><span class="sxs-lookup"><span data-stu-id="08c92-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="08c92-230">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="08c92-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="08c92-231">本節的目標是授與 Britta Simon 對 SilkRoad Life Suite 的存取權，讓她能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="08c92-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![指派使用者][200] 

<span data-ttu-id="08c92-233">**若要將 Britta Simon 指派到 SilkRoad Life Suite，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="08c92-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="08c92-234">在 Azure 傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="08c92-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![指派使用者][201] 

2. <span data-ttu-id="08c92-236">在應用程式清單中，選取 [SilkRoad Life Suite] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![指派使用者][202] 

3. <span data-ttu-id="08c92-238">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-238">In the menu on the top, click **Users**.</span></span>
   
    ![指派使用者][203] 

4. <span data-ttu-id="08c92-240">在 [使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="08c92-241">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="08c92-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="08c92-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="08c92-243">Test single sign-on</span></span>
<span data-ttu-id="08c92-244">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="08c92-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="08c92-245">當您在 [存取面板] 中按一下 [SilkRoad Life Suite] 磚時，您應該會自動登入您的 SilkRoad Life Suite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08c92-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08c92-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="08c92-246">Additional Resources</span></span>
* [<span data-ttu-id="08c92-247">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="08c92-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08c92-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="08c92-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





