---
title: "aaaAzure AD Connect 同步服務功能和組態 |Microsoft 文件"
description: "描述 Azure AD Connect 同步處理服務的服務端功能。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="fbcb5-103">Azure AD Connect 同步處理服務功能</span><span class="sxs-lookup"><span data-stu-id="fbcb5-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="fbcb5-104">Azure AD connect 的 hello 同步處理功能具有兩個元件：</span><span class="sxs-lookup"><span data-stu-id="fbcb5-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="fbcb5-105">hello 內部元件，名為**Azure AD Connect 同步處理**，也稱為**同步處理引擎**。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="fbcb5-106">也就位於 Azure AD 中的 hello 服務**Azure AD Connect 同步處理服務**</span><span class="sxs-lookup"><span data-stu-id="fbcb5-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="fbcb5-107">本主題說明 hello 下列功能如何的 hello **Azure AD Connect 同步處理服務**工作並設定它們使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="fbcb5-108">這些設定是由 hello [Azure Active Directory 的 Windows PowerShell 模組](http://aka.ms/aadposh)。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="fbcb5-109">從 Azure AD Connect 個別進行下載和安裝。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="fbcb5-110">在本主題中的 hello cmdlet 已導入 hello [2016 年 3 月發行 （建置 9031.1）](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1)。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="fbcb5-111">如果您不需要在本主題中的 hello cmdlet，或它們不會產生的 hello 相同結果，則請確定您執行 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="fbcb5-112">在執行的 Azure AD 目錄中的 toosee hello 組態`Get-MsolDirSyncFeatures`。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="fbcb5-113">![Get-MsolDirSyncFeatures 結果](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="fbcb5-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="fbcb5-114">其中許多設定只能由 Azure AD Connect 進行變更。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="fbcb5-115">hello 設定下列設定可以是`Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="fbcb5-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="fbcb5-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="fbcb5-116">DirSyncFeature</span></span> | <span data-ttu-id="fbcb5-117">註解</span><span class="sxs-lookup"><span data-stu-id="fbcb5-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="fbcb5-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="fbcb5-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="fbcb5-119">允許物件 toojoin 上的 userPrincipalName 加法 tooprimary SMTP 位址。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="fbcb5-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="fbcb5-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="fbcb5-121">Hello 同步處理引擎 tooupdate hello userPrincipalName 屬性可讓受管理/授權 （非同盟） 的使用者。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="fbcb5-122">啟用功能後，即無法將其停用。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="fbcb5-123">從 2016 年 8 月 24 日 hello 功能*重複屬性復原*預設會啟用新的 azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="fbcb5-124">這項功能也會在此日期前建立的目錄上推出和啟用。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="fbcb5-125">當您的目錄是 tooget 有關啟用這項功能，您會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="fbcb5-126">hello 下列設定由 Azure AD Connect 設定，而且無法修改由`Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="fbcb5-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="fbcb5-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="fbcb5-127">DirSyncFeature</span></span> | <span data-ttu-id="fbcb5-128">註解</span><span class="sxs-lookup"><span data-stu-id="fbcb5-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="fbcb5-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="fbcb5-129">DeviceWriteback</span></span> |[<span data-ttu-id="fbcb5-130">Azure AD Connect：啟用裝置回寫</span><span class="sxs-lookup"><span data-stu-id="fbcb5-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="fbcb5-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="fbcb5-131">DirectoryExtensions</span></span> |[<span data-ttu-id="fbcb5-132">Azure AD Connect 同步處理：目錄擴充</span><span class="sxs-lookup"><span data-stu-id="fbcb5-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="fbcb5-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="fbcb5-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="fbcb5-134">可讓它是另一個物件，而非在匯出期間失敗 hello 整個物件的複本時，隔離屬性 toobe。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="fbcb5-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="fbcb5-135">PasswordSync</span></span> |[<span data-ttu-id="fbcb5-136">使用 Azure AD Connect 同步處理實作密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="fbcb5-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="fbcb5-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="fbcb5-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="fbcb5-138">預覽：群組回寫</span><span class="sxs-lookup"><span data-stu-id="fbcb5-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="fbcb5-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="fbcb5-139">UserWriteback</span></span> |<span data-ttu-id="fbcb5-140">目前不支援。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="fbcb5-141">重複屬性恢復功能</span><span class="sxs-lookup"><span data-stu-id="fbcb5-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="fbcb5-142">而非發生失敗 tooprovision 物件具有重複的 Upn/proxyAddresses，hello 重複的屬性 「 隔離 」，而且會指派暫時的值。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="fbcb5-143">Hello 衝突解決時，暫時的 hello UPN 的自動變更 toohello 適當的值。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="fbcb5-144">如需詳細資訊，請參閱 [身分識別同步處理和重複屬性恢復功能](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="fbcb5-145">UserPrincipalName 大致比對</span><span class="sxs-lookup"><span data-stu-id="fbcb5-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="fbcb5-146">啟用這項功能時，軟體相符項目中已啟用的 UPN 加法 toohello[主要 SMTP 位址](https://support.microsoft.com/kb/2641663)，永遠啟用。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="fbcb5-147">軟相符項目是使用的 toomatch 現有的雲端使用者與內部部署使用者的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="fbcb5-148">如果您需要 toomatch 內部 AD 帳戶與 hello 雲端中建立的現有帳戶，而且您不能使用 Exchange Online，則此功能十分有用。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="fbcb5-149">在此案例中，您通常不需要原因 tooset hello SMTP 屬性 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="fbcb5-150">在新建立的 Azure AD 目錄中，預設會開啟這項功能。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="fbcb5-151">您可以執行下列項目，查看是否已啟用此功能︰</span><span class="sxs-lookup"><span data-stu-id="fbcb5-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="fbcb5-152">如果您的 Azure AD 目錄未啟用這項功能，您可以執行下列項目加以啟用︰</span><span class="sxs-lookup"><span data-stu-id="fbcb5-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="fbcb5-153">同步處理 userPrincipalName 更新</span><span class="sxs-lookup"><span data-stu-id="fbcb5-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="fbcb5-154">在過去，使用從內部部署的 hello 同步服務更新 toohello UserPrincipalName 屬性已被封鎖，除非這些條件都成立：</span><span class="sxs-lookup"><span data-stu-id="fbcb5-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="fbcb5-155">hello 使用者被管理 （非同盟）。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="fbcb5-156">hello 使用者尚未指派授權。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="fbcb5-157">如需詳細資訊，請參閱[Office 365、 Azure 或 Intune 中的名稱不相符的使用者 hello 在內部部署 UPN 或替代登入識別碼](https://support.microsoft.com/kb/2523192)。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="fbcb5-158">啟用這項功能可讓 hello 同步處理引擎 tooupdate hello userPrincipalName，變更在內部部署，且您使用密碼同步處理時。如果您使用同盟，則不支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="fbcb5-159">在新建立的 Azure AD 目錄中，預設會開啟這項功能。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="fbcb5-160">您可以執行下列項目，查看是否已啟用此功能︰</span><span class="sxs-lookup"><span data-stu-id="fbcb5-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="fbcb5-161">如果您的 Azure AD 目錄未啟用這項功能，您可以執行下列項目加以啟用︰</span><span class="sxs-lookup"><span data-stu-id="fbcb5-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="fbcb5-162">啟用這項功能之後，現有的 userPrincipalName 值會保持不變。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="fbcb5-163">下次 hello userPrincipalName 屬性在內部變更，對使用者的 hello 一般差異同步處理會更新 hello UPN。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="fbcb5-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fbcb5-164">See also</span></span>
* [<span data-ttu-id="fbcb5-165">Azure AD Connect 同步處理</span><span class="sxs-lookup"><span data-stu-id="fbcb5-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="fbcb5-166">[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="fbcb5-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

