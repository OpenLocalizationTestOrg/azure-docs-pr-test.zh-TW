---
title: "aaaEnable Microsoft Windows Hello 企業版中組織 |Microsoft 文件"
description: "部署指示 tooenable Microsoft Passport 您組織中。"
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
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="acde0-104">在組織中啟用 Microsoft Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="acde0-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="acde0-105">之後[連接 Windows 10 已加入網域的裝置與 Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md)，請勿遵循您組織中的 Microsoft Windows Hello 企業 tooenable hello:</span><span class="sxs-lookup"><span data-stu-id="acde0-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do hello following tooenable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="acde0-106">部署 System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="acde0-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="acde0-107">設定原則設定</span><span class="sxs-lookup"><span data-stu-id="acde0-107">Configure policy settings</span></span>
3. <span data-ttu-id="acde0-108">設定 hello 憑證設定檔</span><span class="sxs-lookup"><span data-stu-id="acde0-108">Configure hello certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="acde0-109">部署 System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="acde0-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="acde0-110">根據 Windows Hello 的商務索引鍵 toodeploy 使用者憑證，您需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="acde0-110">toodeploy user certificates based on Windows Hello for Business keys, you need hello following:</span></span>

* <span data-ttu-id="acde0-111">**System Center Configuration Manager 最新分支**-您需要 tooinstall 版本 1606年或更高。</span><span class="sxs-lookup"><span data-stu-id="acde0-111">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span> <span data-ttu-id="acde0-112">如需詳細資訊，請參閱 hello [for System Center Configuration Manager 文件](https://technet.microsoft.com/library/mt346023.aspx)和[System Center Configuration Manager 小組部落格](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="acde0-112">For more information, see hello [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="acde0-113">**公開金鑰基礎結構 (PKI)** -tooenable Microsoft Windows Hello 商務藉由使用使用者憑證，您必須具備 PKI。</span><span class="sxs-lookup"><span data-stu-id="acde0-113">**Public key infrastructure (PKI)** - tooenable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="acde0-114">如果您沒有其中一個，或您不想 toouse 它的使用者憑證，您可以部署新的網域控制站已建置 10551 （或更新版本） 安裝的 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="acde0-114">If you don’t have one, or you don’t want toouse it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="acde0-115">請依照下列步驟 hello 太[現有網域中安裝複本網域控制站](https://technet.microsoft.com/library/jj574134.aspx)或太[安裝新的 Active Directory 樹系中，如果您要建立新環境](https://technet.microsoft.com/library/jj574166)。</span><span class="sxs-lookup"><span data-stu-id="acde0-115">Follow hello steps too[install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or too[install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="acde0-116">(hello Iso 可供下載[Signiant 媒體交換](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true)。)</span><span class="sxs-lookup"><span data-stu-id="acde0-116">(hello ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="acde0-117">設定原則設定</span><span class="sxs-lookup"><span data-stu-id="acde0-117">Configure policy settings</span></span>
<span data-ttu-id="acde0-118">tooconfigure hello Microsoft Windows Hello 的商務原則設定，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="acde0-118">tooconfigure hello Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="acde0-119">Active Directory 中的群組原則</span><span class="sxs-lookup"><span data-stu-id="acde0-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="acde0-120">hello System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="acde0-120">hello System Center Configuration Manager</span></span> 

<span data-ttu-id="acde0-121">在 Active Directory 中的使用 「 群組原則是 hello 建議方法 tooconfigure Microsoft Windows Hello 的商務原則設定。</span><span class="sxs-lookup"><span data-stu-id="acde0-121">Using Group Policy in Active Directory is hello recommended method tooconfigure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="acde0-122">使用 System Center Configuration Manager 是 hello 慣用方法，當您使用它 toodeploy 憑證。</span><span class="sxs-lookup"><span data-stu-id="acde0-122">Using System Center Configuration Manager is hello preferred method when you also use it toodeploy certificates.</span></span> <span data-ttu-id="acde0-123">此案例：</span><span class="sxs-lookup"><span data-stu-id="acde0-123">This scenario:</span></span>

* <span data-ttu-id="acde0-124">可確保與 hello 較新的部署案例的相容性</span><span class="sxs-lookup"><span data-stu-id="acde0-124">Ensures compatibility with hello newer deployment scenarios</span></span>
* <span data-ttu-id="acde0-125">需要 Windows 10 版本 1607年或更佳的 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="acde0-125">Requires on hello client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="acde0-126">透過 Active Directory 中的群組原則設定 Microsoft Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="acde0-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="acde0-127">**步驟**：</span><span class="sxs-lookup"><span data-stu-id="acde0-127">**Steps**:</span></span>

1. <span data-ttu-id="acde0-128">開啟 [伺服器管理員] 並瀏覽過**工具** > **群組原則管理**。</span><span class="sxs-lookup"><span data-stu-id="acde0-128">Open Server Manager, and navigate too**Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="acde0-129">從群組原則管理 瀏覽 toohello 對應您想要設定 Azure AD Join tooenable toohello 網域的網域節點。</span><span class="sxs-lookup"><span data-stu-id="acde0-129">From Group Policy Management, navigate toohello domain node that corresponds toohello domain in which you want tooenable Azure AD Join.</span></span>
3. <span data-ttu-id="acde0-130">以滑鼠右鍵按一下 [群組原則物件]，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="acde0-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="acde0-131">指定群組原則物件的名稱，例如「啟用 Windows Hello 企業版」。</span><span class="sxs-lookup"><span data-stu-id="acde0-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="acde0-132">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="acde0-132">Click **OK**.</span></span>
4. <span data-ttu-id="acde0-133">以滑鼠右鍵按一下新的群組原則物件，然後選取 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="acde0-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="acde0-134">瀏覽過**電腦設定** > **原則** > **系統管理範本** > **Windows元件** > **Windows Hello 企業**。</span><span class="sxs-lookup"><span data-stu-id="acde0-134">Navigate too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="acde0-135">以滑鼠右鍵按一下 [啟用 Windows Hello 企業版]，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="acde0-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="acde0-136">選取 hello**啟用**選項按鈕，然後再按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="acde0-136">Select hello **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="acde0-137">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="acde0-137">Click **OK**.</span></span>
8. <span data-ttu-id="acde0-138">您現在可以將連結 hello 群組原則物件 tooa 您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="acde0-138">You can now link hello Group Policy Object tooa location of your choice.</span></span> <span data-ttu-id="acde0-139">tooenable hello 組織連結 hello 群組原則 toohello 網域中，已加入網域的 Windows 10 裝置的所有此原則。</span><span class="sxs-lookup"><span data-stu-id="acde0-139">tooenable this policy for all of hello domain-joined Windows 10 devices in your organization, link hello Group Policy toohello domain.</span></span> <span data-ttu-id="acde0-140">例如：</span><span class="sxs-lookup"><span data-stu-id="acde0-140">For example:</span></span>
   * <span data-ttu-id="acde0-141">Active Directory 中將放置已加入網域的 Windows 10 電腦的特定組織單位 (OU)</span><span class="sxs-lookup"><span data-stu-id="acde0-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="acde0-142">已加入網域且會向 Azure AD 自動註冊的 Windows 10 電腦所屬的特定安全性群組</span><span class="sxs-lookup"><span data-stu-id="acde0-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="acde0-143">使用 System Center Configuration Manager設定 Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="acde0-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="acde0-144">**步驟**：</span><span class="sxs-lookup"><span data-stu-id="acde0-144">**Steps**:</span></span>

1. <span data-ttu-id="acde0-145">開啟 hello **System Center Configuration Manager**，然後瀏覽過**資產與相容性 > 相容性設定 > 公司資源存取 > 商務設定檔的 Windows Hello**。</span><span class="sxs-lookup"><span data-stu-id="acde0-145">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="acde0-147">在 hello hello 上方的工具列中按一下**建立商務設定檔的 Windows Hello**。</span><span class="sxs-lookup"><span data-stu-id="acde0-147">In hello toolbar on hello top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="acde0-149">在 [hello**一般**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acde0-149">On hello **General** dialog, perform hello following steps:</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="acde0-151">a.</span><span class="sxs-lookup"><span data-stu-id="acde0-151">a.</span></span> <span data-ttu-id="acde0-152">在 hello**名稱**文字方塊中，輸入您設定檔名稱，例如**WHfB 我的設定檔**。</span><span class="sxs-lookup"><span data-stu-id="acde0-152">In hello **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="acde0-153">b.</span><span class="sxs-lookup"><span data-stu-id="acde0-153">b.</span></span> <span data-ttu-id="acde0-154">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="acde0-154">Click **Next**.</span></span>
4. <span data-ttu-id="acde0-155">在 hello**支援的平台**對話方塊中，選取 hello 平台，必須具備此 Windows Hello，為商務設定檔，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="acde0-155">On hello **Supported Platforms** dialog, select hello platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="acde0-157">在 [hello**設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acde0-157">On hello **Settings** dialog, perform hello following steps:</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="acde0-159">a.</span><span class="sxs-lookup"><span data-stu-id="acde0-159">a.</span></span> <span data-ttu-id="acde0-160">對於 [設定 Windows Hello 企業版]，選取 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="acde0-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="acde0-161">b.</span><span class="sxs-lookup"><span data-stu-id="acde0-161">b.</span></span> <span data-ttu-id="acde0-162">對於 [使用信賴平台模組 (TPM)]，選取 [必要]。</span><span class="sxs-lookup"><span data-stu-id="acde0-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="acde0-163">c.</span><span class="sxs-lookup"><span data-stu-id="acde0-163">c.</span></span> <span data-ttu-id="acde0-164">對於 [驗證方法]，選取 [憑證型]。</span><span class="sxs-lookup"><span data-stu-id="acde0-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="acde0-165">d.</span><span class="sxs-lookup"><span data-stu-id="acde0-165">d.</span></span> <span data-ttu-id="acde0-166">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="acde0-166">Click **Next**.</span></span>
6. <span data-ttu-id="acde0-167">在 hello**摘要** 對話方塊中，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="acde0-167">On hello **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="acde0-168">在 hello**完成** 對話方塊中，按一下 **關閉**。</span><span class="sxs-lookup"><span data-stu-id="acde0-168">On hello **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="acde0-169">在 hello hello 上方的工具列中按一下**部署**。</span><span class="sxs-lookup"><span data-stu-id="acde0-169">In hello toolbar on hello top, click **Deploy**.</span></span>
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a><span data-ttu-id="acde0-171">設定 hello 憑證設定檔</span><span class="sxs-lookup"><span data-stu-id="acde0-171">Configure hello certificate profile</span></span>
<span data-ttu-id="acde0-172">如果您在內部部署驗證使用憑證型驗證，您需要 tooconfigure 並部署憑證設定檔。</span><span class="sxs-lookup"><span data-stu-id="acde0-172">If you are using certificate-based authentication for on-premises authentication, you need tooconfigure and deploy a certificate profile.</span></span> <span data-ttu-id="acde0-173">這項工作需要 tooset 設定 NDES 伺服器，在 hello System Center Configuration Manager 憑證登錄點站台角色。</span><span class="sxs-lookup"><span data-stu-id="acde0-173">This task requires you tooset up an NDES server and Certificate Registration Point site role in hello System Center Configuration Manager.</span></span> <span data-ttu-id="acde0-174">如需詳細資訊，請參閱 hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx)。</span><span class="sxs-lookup"><span data-stu-id="acde0-174">For more details, see hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="acde0-175">開啟 hello **System Center Configuration Manager**，然後瀏覽過**資產與相容性 > 相容性設定 > 公司資源存取 > 憑證設定檔**。</span><span class="sxs-lookup"><span data-stu-id="acde0-175">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="acde0-176">選取一個含有智慧卡登入擴充金鑰使用方法 (EKU) 的範本。</span><span class="sxs-lookup"><span data-stu-id="acde0-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="acde0-177">在 hello**頁面 SCEP 註冊**頁面 hello 憑證設定檔，您需要 toochoose**安裝 tooPassport for Work 否則便失敗**為 hello**金鑰儲存提供者**。</span><span class="sxs-lookup"><span data-stu-id="acde0-177">On hello **SCEP Enrollment** page of hello certificate profile, you need toochoose **Install tooPassport for Work otherwise fail** as hello **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acde0-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acde0-178">Next steps</span></span>
* [<span data-ttu-id="acde0-179">Hello 企業版的 Windows 10： 工作的方式 toouse 裝置</span><span class="sxs-lookup"><span data-stu-id="acde0-179">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="acde0-180">擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端</span><span class="sxs-lookup"><span data-stu-id="acde0-180">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="acde0-181">透過 Microsoft Passport 不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="acde0-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="acde0-182">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="acde0-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="acde0-183">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="acde0-183">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="acde0-184">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="acde0-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

