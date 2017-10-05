---
title: "在組織中啟用 Microsoft Windows Hello 企業版 | Microsoft Docs"
description: "在組織中啟用 Microsoft Passport 的部署指示。"
services: active-directory
documentationcenter: 
keywords: "設定 Microsoft Passport、Microsoft Windows Hello 企業版部署"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="a4487-104">在組織中啟用 Microsoft Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="a4487-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="a4487-105">[連接已加入網域的 Windows 10 裝置與 Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md) 後，請依下列方式在組織中啟用 Microsoft Windows Hello 企業版。</span><span class="sxs-lookup"><span data-stu-id="a4487-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="a4487-106">部署 System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a4487-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="a4487-107">設定原則設定</span><span class="sxs-lookup"><span data-stu-id="a4487-107">Configure policy settings</span></span>
3. <span data-ttu-id="a4487-108">設定憑證設定檔</span><span class="sxs-lookup"><span data-stu-id="a4487-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="a4487-109">部署 System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a4487-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="a4487-110">如果要根據 Windows Hello 企業版金鑰部署使用者憑證，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a4487-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="a4487-111">**System Center Configuration Manager 最新分支** - 您必須安裝 1606 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a4487-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="a4487-112">如需詳細資訊，請參閱 [System Center Configuration Manager 文件](https://technet.microsoft.com/library/mt346023.aspx)和 [System Center Configuration Manager 小組部落格](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a4487-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="a4487-113">**發佈金鑰基礎結構 (PKI)** - 若要利用使用者憑證啟用 Microsoft Windows Hello 企業版，您必須備妥 PKI。</span><span class="sxs-lookup"><span data-stu-id="a4487-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="a4487-114">如果您沒有帳戶，或您不想要用於使用者憑證，您可以部署已安裝 Windows Server 2016 組建 10551 (或更新版本) 的新網域控制站。</span><span class="sxs-lookup"><span data-stu-id="a4487-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="a4487-115">依照步驟在現有網域中[安裝複本網域控制站](https://technet.microsoft.com/library/jj574134.aspx)或[安裝新的 Active Directory 樹系 (如果您要建立新的環境)](https://technet.microsoft.com/library/jj574166)。</span><span class="sxs-lookup"><span data-stu-id="a4487-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="a4487-116">(ISO 可在 [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true) 下載。)</span><span class="sxs-lookup"><span data-stu-id="a4487-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="a4487-117">設定原則設定</span><span class="sxs-lookup"><span data-stu-id="a4487-117">Configure policy settings</span></span>
<span data-ttu-id="a4487-118">若要設定 Microsoft Windows Hello 企業版原則設定，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="a4487-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="a4487-119">Active Directory 中的群組原則</span><span class="sxs-lookup"><span data-stu-id="a4487-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="a4487-120">System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a4487-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="a4487-121">使用 Active Directory 中的群組原則是設定 Microsoft Windows Hello 企業版原則設定的建議方法。</span><span class="sxs-lookup"><span data-stu-id="a4487-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="a4487-122">當您也使用它來部署憑證時，使用 System Center Configuration Manager 是偏好的方法。</span><span class="sxs-lookup"><span data-stu-id="a4487-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="a4487-123">此案例：</span><span class="sxs-lookup"><span data-stu-id="a4487-123">This scenario:</span></span>

* <span data-ttu-id="a4487-124">可確保與較新的部署案例的相容性</span><span class="sxs-lookup"><span data-stu-id="a4487-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="a4487-125">需要用戶端使用 Windows 10 版本 1607 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a4487-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="a4487-126">透過 Active Directory 中的群組原則設定 Microsoft Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="a4487-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="a4487-127">**步驟**：</span><span class="sxs-lookup"><span data-stu-id="a4487-127">**Steps**:</span></span>

1. <span data-ttu-id="a4487-128">開啟 [伺服器管理員] 並瀏覽至 [工具]  >  [群組原則管理]。</span><span class="sxs-lookup"><span data-stu-id="a4487-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="a4487-129">從 [群組原則管理]，瀏覽至與您想要啟用 [加入 Azure AD] 的網域相對應的網域節點。</span><span class="sxs-lookup"><span data-stu-id="a4487-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="a4487-130">以滑鼠右鍵按一下 [群組原則物件]，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a4487-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="a4487-131">指定群組原則物件的名稱，例如「啟用 Windows Hello 企業版」。</span><span class="sxs-lookup"><span data-stu-id="a4487-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="a4487-132">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-132">Click **OK**.</span></span>
4. <span data-ttu-id="a4487-133">以滑鼠右鍵按一下新的群組原則物件，然後選取 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="a4487-134">瀏覽至 [電腦設定]  >  [原則]  >  [系統管理範本]  >  [Windows 元件]  >  [Windows Hello 企業版]。</span><span class="sxs-lookup"><span data-stu-id="a4487-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="a4487-135">以滑鼠右鍵按一下 [啟用 Windows Hello 企業版]，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="a4487-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="a4487-136">選取 [已啟用] 選項按鈕，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="a4487-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="a4487-137">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-137">Click **OK**.</span></span>
8. <span data-ttu-id="a4487-138">您現在可以將群組原則物件連結到您所選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="a4487-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="a4487-139">若要對組織中所有加入網域的 Windows 10 裝置啟用此原則，請將群組原則連結到網域。</span><span class="sxs-lookup"><span data-stu-id="a4487-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="a4487-140">例如：</span><span class="sxs-lookup"><span data-stu-id="a4487-140">For example:</span></span>
   * <span data-ttu-id="a4487-141">Active Directory 中將放置已加入網域的 Windows 10 電腦的特定組織單位 (OU)</span><span class="sxs-lookup"><span data-stu-id="a4487-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="a4487-142">已加入網域且會向 Azure AD 自動註冊的 Windows 10 電腦所屬的特定安全性群組</span><span class="sxs-lookup"><span data-stu-id="a4487-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="a4487-143">使用 System Center Configuration Manager設定 Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="a4487-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="a4487-144">**步驟**：</span><span class="sxs-lookup"><span data-stu-id="a4487-144">**Steps**:</span></span>

1. <span data-ttu-id="a4487-145">開啟 **System Center Configuration Manager**，然後瀏覽至 [資產與相容性] > [相容性設定] > [公司資源存取] > [Windows Hello 企業版設定檔]。</span><span class="sxs-lookup"><span data-stu-id="a4487-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="a4487-147">在頂端工具列中，按一下 [建立 Windows Hello 企業版設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="a4487-149">在 [一般]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a4487-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="a4487-151">a.</span><span class="sxs-lookup"><span data-stu-id="a4487-151">a.</span></span> <span data-ttu-id="a4487-152">在 [名稱] 文字方塊中，輸入您的設定名稱 (例如：**My WHfB Profile**)。</span><span class="sxs-lookup"><span data-stu-id="a4487-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="a4487-153">b.</span><span class="sxs-lookup"><span data-stu-id="a4487-153">b.</span></span> <span data-ttu-id="a4487-154">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-154">Click **Next**.</span></span>
4. <span data-ttu-id="a4487-155">在 [支援的平台] 對話方塊中，選取將使用此 Windows Hello 企業版設定檔佈建的平台，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a4487-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="a4487-157">在 [設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a4487-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="a4487-159">a.</span><span class="sxs-lookup"><span data-stu-id="a4487-159">a.</span></span> <span data-ttu-id="a4487-160">對於 [設定 Windows Hello 企業版]，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="a4487-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="a4487-161">b.</span><span class="sxs-lookup"><span data-stu-id="a4487-161">b.</span></span> <span data-ttu-id="a4487-162">對於 [使用信賴平台模組 (TPM)]，選取 [必要]。</span><span class="sxs-lookup"><span data-stu-id="a4487-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="a4487-163">c.</span><span class="sxs-lookup"><span data-stu-id="a4487-163">c.</span></span> <span data-ttu-id="a4487-164">對於 [驗證方法]，選取 [憑證型]。</span><span class="sxs-lookup"><span data-stu-id="a4487-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="a4487-165">d.</span><span class="sxs-lookup"><span data-stu-id="a4487-165">d.</span></span> <span data-ttu-id="a4487-166">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-166">Click **Next**.</span></span>
6. <span data-ttu-id="a4487-167">在 [摘要] 對話方塊上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a4487-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="a4487-168">在 [完成] 對話方塊上，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="a4487-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="a4487-169">在頂端工具列中，按一下 [部署] 。</span><span class="sxs-lookup"><span data-stu-id="a4487-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="a4487-171">設定憑證設定檔</span><span class="sxs-lookup"><span data-stu-id="a4487-171">Configure the certificate profile</span></span>
<span data-ttu-id="a4487-172">如果您使用憑證型驗證進行內部部署驗證，您需要設定及部署憑證設定檔。</span><span class="sxs-lookup"><span data-stu-id="a4487-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="a4487-173">這項工作需要您在 System Center Configuration Manager 中設定 NDES 伺服器和憑證登錄點網站角色。</span><span class="sxs-lookup"><span data-stu-id="a4487-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="a4487-174">如需詳細資訊，請參閱 [Configuration Manager 中憑證設定檔的必要條件](https://technet.microsoft.com/library/dn261205.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a4487-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="a4487-175">開啟 **System Center Configuration Manager**，然後瀏覽至 [資產與相容性] > [相容性設定] > [公司資源存取] > [憑證設定檔]。</span><span class="sxs-lookup"><span data-stu-id="a4487-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="a4487-176">選取一個含有智慧卡登入擴充金鑰使用方法 (EKU) 的範本。</span><span class="sxs-lookup"><span data-stu-id="a4487-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="a4487-177">在憑證設定檔的 [SCEP 註冊] 頁面上，您必須選擇 [安裝至 Passport for Work，否則便失敗] 做為 [金鑰儲存體提供者]。</span><span class="sxs-lookup"><span data-stu-id="a4487-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4487-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4487-178">Next steps</span></span>
* [<span data-ttu-id="a4487-179">適合企業使用的 Windows 10：使用裝置工作的方式</span><span class="sxs-lookup"><span data-stu-id="a4487-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="a4487-180">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="a4487-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="a4487-181">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="a4487-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="a4487-182">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="a4487-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="a4487-183">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="a4487-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="a4487-184">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="a4487-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

