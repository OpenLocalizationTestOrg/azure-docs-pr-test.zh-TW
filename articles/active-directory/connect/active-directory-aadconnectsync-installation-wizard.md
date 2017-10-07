---
title: "在重新執行 hello Azure AD Connect 的安裝精靈 |Microsoft 文件"
description: "說明 hello 安裝精靈的運作方式 hello 第二次執行它。"
keywords: "hello Azure AD Connect 的安裝精靈可讓您設定第二次執行的維護設定 hello"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="6f841-104">Azure AD Connect 同步： 第二次執行 hello 安裝精靈</span><span class="sxs-lookup"><span data-stu-id="6f841-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="6f841-105">hello 第一次執行 hello Azure AD Connect 的安裝精靈，它將逐步引導您 tooconfigure 您的安裝。</span><span class="sxs-lookup"><span data-stu-id="6f841-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="6f841-106">如果您再次執行 hello 安裝精靈，它會提供維護選項。</span><span class="sxs-lookup"><span data-stu-id="6f841-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="6f841-107">您可以找到名為 hello 開始 功能表中的 hello 安裝精靈**Azure AD Connect**。</span><span class="sxs-lookup"><span data-stu-id="6f841-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![[開始] 功能表](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="6f841-109">當您啟動 hello 安裝精靈時，您會看到與這些選項的頁面：</span><span class="sxs-lookup"><span data-stu-id="6f841-109">When you start hello installation wizard, you see a page with these options:</span></span>

![含有其他工作清單的頁面](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="6f841-111">如果您已使用 Azure AD Connect 安裝 ADFS，您會有更多選項。</span><span class="sxs-lookup"><span data-stu-id="6f841-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="6f841-112">hello 其他選項，您必須針對 ADFS 記載於[ADFS 管理](active-directory-aadconnect-federation-management.md#manage-ad-fs)。</span><span class="sxs-lookup"><span data-stu-id="6f841-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="6f841-113">選取其中一項 hello 工作，然後按一下**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="6f841-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f841-114">當 hello 安裝精靈開啟時，就會暫停 hello 同步處理引擎中的所有作業。</span><span class="sxs-lookup"><span data-stu-id="6f841-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="6f841-115">請確定您已完成設定變更時，關閉 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="6f841-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="6f841-116">檢視目前的組態</span><span class="sxs-lookup"><span data-stu-id="6f841-116">View current configuration</span></span>
<span data-ttu-id="6f841-117">此選項可讓您快速檢視目前設定的選項。</span><span class="sxs-lookup"><span data-stu-id="6f841-117">This option gives you a quick view of your currently configured options.</span></span>

![含有所有選項和其狀態之清單的頁面](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="6f841-119">按一下**上一步**toogo 上一步。</span><span class="sxs-lookup"><span data-stu-id="6f841-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="6f841-120">如果您選取**結束**，關閉 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="6f841-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="6f841-121">自訂同步處理選項</span><span class="sxs-lookup"><span data-stu-id="6f841-121">Customize synchronization options</span></span>
<span data-ttu-id="6f841-122">這個選項是使用的 toomake 變更 toohello 同步處理設定。</span><span class="sxs-lookup"><span data-stu-id="6f841-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="6f841-123">您看到的子集 hello 自訂設定安裝路徑中的選項。</span><span class="sxs-lookup"><span data-stu-id="6f841-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="6f841-124">即使您一開始是使用快速安裝也會看到此選項。</span><span class="sxs-lookup"><span data-stu-id="6f841-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="6f841-125">[新增其他目錄](active-directory-aadconnect-get-started-custom.md#connect-your-directories)。</span><span class="sxs-lookup"><span data-stu-id="6f841-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="6f841-126">若要移除目錄，請參閱 [刪除連接器](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete)。</span><span class="sxs-lookup"><span data-stu-id="6f841-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="6f841-127">[變更網域和 OU 篩選](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)。</span><span class="sxs-lookup"><span data-stu-id="6f841-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="6f841-128">移除群組篩選。</span><span class="sxs-lookup"><span data-stu-id="6f841-128">Remove Group filtering.</span></span>
* <span data-ttu-id="6f841-129">[變更選用功能](active-directory-aadconnect-get-started-custom.md#optional-features)。</span><span class="sxs-lookup"><span data-stu-id="6f841-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="6f841-130">hello hello 初始安裝中的其他選項無法變更或不能使用。</span><span class="sxs-lookup"><span data-stu-id="6f841-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="6f841-131">這些選項包括：</span><span class="sxs-lookup"><span data-stu-id="6f841-131">These options are:</span></span>

* <span data-ttu-id="6f841-132">變更 hello 屬性 toouse userPrincipalName 和 sourceAnchor。</span><span class="sxs-lookup"><span data-stu-id="6f841-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="6f841-133">變更 hello 聯結來自不同樹系的物件的方法。</span><span class="sxs-lookup"><span data-stu-id="6f841-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="6f841-134">啟用群組式篩選。</span><span class="sxs-lookup"><span data-stu-id="6f841-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="6f841-135">重新整理目錄結構描述</span><span class="sxs-lookup"><span data-stu-id="6f841-135">Refresh directory schema</span></span>
<span data-ttu-id="6f841-136">會使用此選項，如果您已經變更 hello 結構描述，其中一種您內部部署 AD DS 樹系。</span><span class="sxs-lookup"><span data-stu-id="6f841-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="6f841-137">例如，您可能已安裝 Exchange 或升級 Windows Server 2012 tooa 結構描述與裝置物件。</span><span class="sxs-lookup"><span data-stu-id="6f841-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="6f841-138">在此情況下，您需要 tooinstruct Azure AD Connect tooread hello 結構描述一次從 AD DS，並更新其快取。</span><span class="sxs-lookup"><span data-stu-id="6f841-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="6f841-139">這個動作也會重新產生 hello 同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="6f841-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="6f841-140">如果您加入 hello Exchange 結構描述，例如，適用於 Exchange 的 hello 同步處理規則會加入 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="6f841-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="6f841-141">當您選取此選項時，會列出所有組態中的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="6f841-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="6f841-142">您可以保留 hello 預設設定和重新整理所有樹系或取消選取部分。</span><span class="sxs-lookup"><span data-stu-id="6f841-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Hello 環境中的所有目錄的清單頁面](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="6f841-144">設定預備模式</span><span class="sxs-lookup"><span data-stu-id="6f841-144">Configure staging mode</span></span>
<span data-ttu-id="6f841-145">此選項可讓您 tooenable 並停用預備模式 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="6f841-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="6f841-146">預備模式和其使用方式的詳細資訊可在 [作業](active-directory-aadconnectsync-operations.md#staging-mode)中找到。</span><span class="sxs-lookup"><span data-stu-id="6f841-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="6f841-147">如果目前啟用或停用預備 hello 選項就會顯示：</span><span class="sxs-lookup"><span data-stu-id="6f841-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![也會顯示 hello 的預備模式的目前狀態的選項](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="6f841-149">toochange hello 狀態，請選取此選項和 hello 選取或取消選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6f841-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![也會顯示 hello 的預備模式的目前狀態的選項](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="6f841-151">變更使用者登入</span><span class="sxs-lookup"><span data-stu-id="6f841-151">Change user sign-in</span></span>
<span data-ttu-id="6f841-152">此選項可讓您從密碼同步 toofederation 或 hello 反過來 toochange。</span><span class="sxs-lookup"><span data-stu-id="6f841-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="6f841-153">您也無法變更**不設定**。</span><span class="sxs-lookup"><span data-stu-id="6f841-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="6f841-154">如需此選項的詳細資訊，請參閱 [使用者登入](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method)。</span><span class="sxs-lookup"><span data-stu-id="6f841-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f841-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f841-155">Next steps</span></span>
* <span data-ttu-id="6f841-156">深入了解使用 Azure AD Connect 同步處理中的 hello 組態模型[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="6f841-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="6f841-157">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="6f841-157">**Overview topics**</span></span>

* [<span data-ttu-id="6f841-158">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="6f841-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="6f841-159">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f841-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
