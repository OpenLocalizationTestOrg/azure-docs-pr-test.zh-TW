---
title: "Azure Active Directory Domain Services：疑難排解指南 | Microsoft Docs"
description: "Azure AD 網域服務的疑難排解指南"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d6695b0c40f56093e8701dfe6394143268114453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a><span data-ttu-id="5365a-103">Azure AD 網域服務 - 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="5365a-103">Azure AD Domain Services - Troubleshooting guide</span></span>
<span data-ttu-id="5365a-104">這篇文章提供設定或管理 Azure Active Directory (AD) 網域服務時，可能會遇到的問題之疑難排解提示。</span><span class="sxs-lookup"><span data-stu-id="5365a-104">This article provides troubleshooting hints for issues you may encounter when setting up or administering Azure Active Directory (AD) Domain Services.</span></span>

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a><span data-ttu-id="5365a-105">您無法為 Azure AD 目錄啟用 Azure AD 網域服務</span><span class="sxs-lookup"><span data-stu-id="5365a-105">You cannot enable Azure AD Domain Services for your Azure AD directory</span></span>
<span data-ttu-id="5365a-106">當您嘗試為您的目錄啟用 Azure AD 網域服務，而遇到失敗或切換回 [已停用] 時，這一節可協助您針對錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5365a-106">This section helps you troubleshoot errors when you try to enable Azure AD Domain Services for your directory and it fails or gets toggled back to 'Disabled'.</span></span>

<span data-ttu-id="5365a-107">挑選對應至您所遇到之錯誤訊息的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="5365a-107">Pick the troubleshooting steps that correspond to the error message you encounter.</span></span>

| <span data-ttu-id="5365a-108">**錯誤訊息**</span><span class="sxs-lookup"><span data-stu-id="5365a-108">**Error Message**</span></span> | <span data-ttu-id="5365a-109">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="5365a-109">**Resolution**</span></span> |
| --- |:--- |
| <span data-ttu-id="5365a-110">*名稱 contoso100.com 使用於此網路上。指定未使用的名稱。*</span><span class="sxs-lookup"><span data-stu-id="5365a-110">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span> |[<span data-ttu-id="5365a-111">虛擬網路中的網域名稱衝突</span><span class="sxs-lookup"><span data-stu-id="5365a-111">Domain name conflict in the virtual network</span></span>](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| <span data-ttu-id="5365a-112">*無法在此 Azure AD 租用戶中啟用網域服務。對於名為「Azure AD 網域服務同步處理」的應用程式，此服務沒有足夠的權限。刪除名為「Azure AD 網域服務同步處理」的應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。*</span><span class="sxs-lookup"><span data-stu-id="5365a-112">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="5365a-113">網域服務沒有「Azure AD 網域服務同步處理」應用程式的足夠權限。</span><span class="sxs-lookup"><span data-stu-id="5365a-113">Domain Services does not have adequate permissions to the Azure AD Domain Services Sync application</span></span>](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| <span data-ttu-id="5365a-114">*無法在此 Azure AD 租用戶中啟用網域服務。Azure AD 租用戶中的網域服務應用程式沒有啟用網域服務所需的權限。刪除應用程式識別碼為 d87dcbc6-a371-462e-88e3-28ad15ec4e64 的應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。*</span><span class="sxs-lookup"><span data-stu-id="5365a-114">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="5365a-115">未在您的租用戶中正確設定網域服務應用程式</span><span class="sxs-lookup"><span data-stu-id="5365a-115">The Domain Services application is not configured properly in your tenant</span></span>](active-directory-ds-troubleshooting.md#invalid-configuration) |
| <span data-ttu-id="5365a-116">*無法在此 Azure AD 租用戶中啟用網域服務。您的 Azure AD 租用戶已停用 Microsoft Azure AD 應用程式。啟用應用程式識別碼為 00000002-0000-0000-c000-000000000000 的應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。*</span><span class="sxs-lookup"><span data-stu-id="5365a-116">*Domain Services could not be enabled in this Azure AD tenant. The Microsoft Azure AD application is disabled in your Azure AD tenant. Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="5365a-117">您的 Azure AD 租用戶已停用 Microsoft Graph 應用程式</span><span class="sxs-lookup"><span data-stu-id="5365a-117">The Microsoft Graph application is disabled in your Azure AD tenant</span></span>](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a><span data-ttu-id="5365a-118">網域名稱衝突</span><span class="sxs-lookup"><span data-stu-id="5365a-118">Domain Name conflict</span></span>
<span data-ttu-id="5365a-119">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="5365a-119">**Error message:**</span></span>

<span data-ttu-id="5365a-120">*名稱 contoso100.com 使用於此網路上。指定未使用的名稱。*</span><span class="sxs-lookup"><span data-stu-id="5365a-120">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span>

<span data-ttu-id="5365a-121">**補救：**</span><span class="sxs-lookup"><span data-stu-id="5365a-121">**Remediation:**</span></span>

<span data-ttu-id="5365a-122">請確定現有網域的名稱並未與該虛擬網路上可用的網域名稱相同。</span><span class="sxs-lookup"><span data-stu-id="5365a-122">Ensure that you do not have an existing domain with the same domain name available on that virtual network.</span></span> <span data-ttu-id="5365a-123">例如，假設您有名為 'contoso.com' 的網域已可用於選取的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5365a-123">For instance, assume you have a domain called 'contoso.com' already available on the selected virtual network.</span></span> <span data-ttu-id="5365a-124">接著，您可嘗試在該虛擬網路上啟用具有相同網域名稱 (即 'contoso.com') 的 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="5365a-124">Later, you try to enable an Azure AD Domain Services managed domain with the same domain name (that is, 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="5365a-125">您在嘗試啟用 Azure AD 網域服務時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5365a-125">You encounter a failure when trying to enable Azure AD Domain Services.</span></span>

<span data-ttu-id="5365a-126">這個錯誤是因為名稱與該虛擬網路上的網域名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="5365a-126">This failure is due to name conflicts for the domain name on that virtual network.</span></span> <span data-ttu-id="5365a-127">在此情況下，您必須使用不同的名稱來設定 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="5365a-127">In this situation, you must use a different name to set up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="5365a-128">或者，您可以解除佈建現有的網域，然後繼續啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-128">Alternately, you can de-provision the existing domain and then proceed to enable Azure AD Domain Services.</span></span>

### <a name="inadequate-permissions"></a><span data-ttu-id="5365a-129">權限不足</span><span class="sxs-lookup"><span data-stu-id="5365a-129">Inadequate permissions</span></span>
<span data-ttu-id="5365a-130">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="5365a-130">**Error message:**</span></span>

<span data-ttu-id="5365a-131">*無法在此 Azure AD 租用戶中啟用網域服務。對於名為「Azure AD 網域服務同步處理」的應用程式，此服務沒有足夠的權限。刪除名為「Azure AD 網域服務同步處理」的應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。*</span><span class="sxs-lookup"><span data-stu-id="5365a-131">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="5365a-132">**補救：**</span><span class="sxs-lookup"><span data-stu-id="5365a-132">**Remediation:**</span></span>

<span data-ttu-id="5365a-133">查看 Azure AD 目錄中是否有名稱為「Azure AD 網域服務同步處理」的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5365a-133">Check to see if there is an application with the name 'Azure AD Domain Services Sync' in your Azure AD directory.</span></span> <span data-ttu-id="5365a-134">如果此應用程式存在，請將它刪除，然後再重新啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-134">If this application exists, delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="5365a-135">執行下列步驟，以檢查應用程式是否存在並將它刪除 (如果應用程式存在的話)：</span><span class="sxs-lookup"><span data-stu-id="5365a-135">Perform the following steps to check for the presence of the application and to delete it, if the application exists:</span></span>

1. <span data-ttu-id="5365a-136">瀏覽到 **Azure 傳統入口網站** ([https://manage.windowsazure.com](https://manage.windowsazure.com))。</span><span class="sxs-lookup"><span data-stu-id="5365a-136">Navigate to the **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span></span>
2. <span data-ttu-id="5365a-137">在左窗格中，選取 [Active Directory]  節點。</span><span class="sxs-lookup"><span data-stu-id="5365a-137">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="5365a-138">選取您要啟用 Azure AD 網域服務的 Azure AD 租用戶 (目錄)。</span><span class="sxs-lookup"><span data-stu-id="5365a-138">Select the Azure AD tenant (directory) for which you would like to enable Azure AD Domain Services.</span></span>
4. <span data-ttu-id="5365a-139">瀏覽至 [應用程式]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5365a-139">Navigate to the **Applications** tab.</span></span>
5. <span data-ttu-id="5365a-140">選取下拉式清單中的 [我公司所擁有的應用程式]  選項。</span><span class="sxs-lookup"><span data-stu-id="5365a-140">Select the **Applications my company owns** option in the dropdown.</span></span>
6. <span data-ttu-id="5365a-141">檢查名為 [Azure AD 網域服務同步處理] 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5365a-141">Check for an application called **Azure AD Domain Services Sync**.</span></span> <span data-ttu-id="5365a-142">如果應用程式存在，請繼續將它刪除。</span><span class="sxs-lookup"><span data-stu-id="5365a-142">If the application exists, proceed to delete it.</span></span>
7. <span data-ttu-id="5365a-143">刪除此應用程式後，請嘗試再次啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-143">Once you have deleted the application, try to enable Azure AD Domain Services once again.</span></span>

### <a name="invalid-configuration"></a><span data-ttu-id="5365a-144">無效的組態</span><span class="sxs-lookup"><span data-stu-id="5365a-144">Invalid configuration</span></span>
<span data-ttu-id="5365a-145">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="5365a-145">**Error message:**</span></span>

<span data-ttu-id="5365a-146">*無法在此 Azure AD 租用戶中啟用網域服務。Azure AD 租用戶中的網域服務應用程式沒有啟用網域服務所需的權限。刪除應用程式識別碼為 d87dcbc6-a371-462e-88e3-28ad15ec4e64 的應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。*</span><span class="sxs-lookup"><span data-stu-id="5365a-146">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="5365a-147">**補救：**</span><span class="sxs-lookup"><span data-stu-id="5365a-147">**Remediation:**</span></span>

<span data-ttu-id="5365a-148">請查看 Azure AD 目錄中是否有名稱為 'AzureActiveDirectoryDomainControllerServices' (應用程式識別碼為 d87dcbc6-a371-462e-88e3-28ad15ec4e64) 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5365a-148">Check to see if you have an application with the name 'AzureActiveDirectoryDomainControllerServices' (with an application identifier of d87dcbc6-a371-462e-88e3-28ad15ec4e64) in your Azure AD directory.</span></span> <span data-ttu-id="5365a-149">如果此應用程式存在，您必須將它刪除，然後再重新啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-149">If this application exists, you need to delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="5365a-150">使用下列 PowerShell 指令碼來尋找此應用程式並加以刪除。</span><span class="sxs-lookup"><span data-stu-id="5365a-150">Use the following PowerShell script to find the application and delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="5365a-151">此指令碼會使用 **Azure AD PowerShell 第 2 版** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5365a-151">This script uses **Azure AD PowerShell version 2** cmdlets.</span></span> <span data-ttu-id="5365a-152">如需所有可用 Cmdlet 的完整清單及下載此模組，請參閱 [AzureAD PowerShell 參考文件](https://msdn.microsoft.com/library/azure/mt757189.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5365a-152">For a full list of all available cmdlets and to download the module, read the [AzureAD PowerShell reference documentation](https://msdn.microsoft.com/library/azure/mt757189.aspx).</span></span>
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a><span data-ttu-id="5365a-153">Microsoft Graph 已停用</span><span class="sxs-lookup"><span data-stu-id="5365a-153">Microsoft Graph disabled</span></span>
<span data-ttu-id="5365a-154">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="5365a-154">**Error message:**</span></span>

<span data-ttu-id="5365a-155">無法在此 Azure AD 租用戶中啟用網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-155">Domain Services could not be enabled in this Azure AD tenant.</span></span> <span data-ttu-id="5365a-156">您的 Azure AD 租用戶已停用 Microsoft Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5365a-156">The Microsoft Azure AD application is disabled in your Azure AD tenant.</span></span> <span data-ttu-id="5365a-157">啟用應用程式識別碼為 00000002-0000-0000-c000-000000000000 的應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-157">Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.</span></span>

<span data-ttu-id="5365a-158">**補救：**</span><span class="sxs-lookup"><span data-stu-id="5365a-158">**Remediation:**</span></span>

<span data-ttu-id="5365a-159">請查看您是否已停用識別碼為 00000002-0000-0000-c000-000000000000 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5365a-159">Check to see if you have disabled an application with the identifier 00000002-0000-0000-c000-000000000000.</span></span> <span data-ttu-id="5365a-160">此應用程式是 Microsoft Azure AD 應用程式，可提供 Azure AD 租用戶的圖形 API 存取權。</span><span class="sxs-lookup"><span data-stu-id="5365a-160">This application is the Microsoft Azure AD application and provides Graph API access to your Azure AD tenant.</span></span> <span data-ttu-id="5365a-161">Azure AD 網域服務需要啟用此應用程式，才能將 Azure AD 租用戶同步處理至受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="5365a-161">Azure AD Domain Services needs this application to be enabled to synchronize your Azure AD tenant to your managed domain.</span></span>

<span data-ttu-id="5365a-162">若要解決此錯誤，請啟用此應用程式，然後嘗試為 Azure AD 租用戶啟用網域服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-162">To resolve this error, enable this application and then try to enable Domain Services for your Azure AD tenant.</span></span>

## <a name="users-are-unable-to-sign-in-to-the-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="5365a-163">使用者無法登入 Azure AD 網域服務管理的網域</span><span class="sxs-lookup"><span data-stu-id="5365a-163">Users are unable to sign in to the Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="5365a-164">如果 Azure AD 租用戶中有一或多個使用者無法登入新建立的受管理網域，請執行下列疑難排解步驟：</span><span class="sxs-lookup"><span data-stu-id="5365a-164">If one or more users in your Azure AD tenant are unable to sign in to the newly created managed domain, perform the following troubleshooting steps:</span></span>

* <span data-ttu-id="5365a-165">**使用 UPN 格式進行登入：**嘗試使用 UPN 格式 (例如，joeuser@contoso.com) 進行登入，而非使用 SAMAccountName 格式 ('CONTOSO\joeuser')。</span><span class="sxs-lookup"><span data-stu-id="5365a-165">**Sign-in using UPN format:** Try to sign in using the UPN format (for example, 'joeuser@contoso.com') instead of the SAMAccountName format ('CONTOSO\joeuser').</span></span> <span data-ttu-id="5365a-166">對於 UPN 前置詞過長或與受管理網域上其他使用者相同的使用者，可能會自動產生 SAMAccountName。</span><span class="sxs-lookup"><span data-stu-id="5365a-166">The SAMAccountName may be automatically generated for users whose UPN prefix is overly long or is the same as another user on the managed domain.</span></span> <span data-ttu-id="5365a-167">UPN 格式保證是 Azure AD 租用戶內唯一的格式。</span><span class="sxs-lookup"><span data-stu-id="5365a-167">The UPN format is guaranteed to be unique within an Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="5365a-168">建議使用 UPN 格式來登入 Azure AD 網域服務受管理網域。</span><span class="sxs-lookup"><span data-stu-id="5365a-168">We recommend using the UPN format to sign in to the Azure AD Domain Services managed domain.</span></span>
>
>

* <span data-ttu-id="5365a-169">確定您已根據《入門指南》中所述的步驟來 [啟用密碼同步處理](active-directory-ds-getting-started-password-sync.md) 。</span><span class="sxs-lookup"><span data-stu-id="5365a-169">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span></span>
* <span data-ttu-id="5365a-170">**外部帳戶** 確定受影響的使用者帳戶不是 Azure AD 租用戶中的外部帳戶。</span><span class="sxs-lookup"><span data-stu-id="5365a-170">**External accounts:** Ensure that the affected user account is not an external account in the Azure AD tenant.</span></span> <span data-ttu-id="5365a-171">外部帳戶的範例包括 Microsoft 帳戶 (例如 joe@live.com) 或來自外部 Azure AD 目錄的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5365a-171">Examples of external accounts include Microsoft accounts (for example, 'joe@live.com') or user accounts from an external Azure AD directory.</span></span> <span data-ttu-id="5365a-172">因為 Azure AD 網域服務沒有這類使用者帳戶的認證，這些使用者會無法登入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="5365a-172">Since Azure AD Domain Services does not have credentials for such user accounts, these users cannot sign in to the managed domain.</span></span>
* <span data-ttu-id="5365a-173">**同步處理的帳戶：** 如果受影響的使用者帳戶會從內部部署目錄同步處理，請確認：</span><span class="sxs-lookup"><span data-stu-id="5365a-173">**Synced accounts:** If the affected user accounts are synchronized from an on-premises directory, verify that:</span></span>

  * <span data-ttu-id="5365a-174">您已部署或更新為 [Azure AD Connect 的最新版本](https://www.microsoft.com/en-us/download/details.aspx?id=47594)。</span><span class="sxs-lookup"><span data-stu-id="5365a-174">You have deployed or updated to the [latest recommended release of Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).</span></span>
  * <span data-ttu-id="5365a-175">您已設定 Azure AD Connect 以 [執行完整同步處理](active-directory-ds-getting-started-password-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="5365a-175">You have configured Azure AD Connect to [perform a full synchronization](active-directory-ds-getting-started-password-sync.md).</span></span>
  * <span data-ttu-id="5365a-176">根據您的目錄大小，可能需要一些時間，使用者帳戶和認證雜湊才可在 Azure AD 網域服務中提供使用。</span><span class="sxs-lookup"><span data-stu-id="5365a-176">Depending on the size of your directory, it may take a while for user accounts and credential hashes to be available in Azure AD Domain Services.</span></span> <span data-ttu-id="5365a-177">確定您已等候足夠長的時間之後，再重試驗證 (視目錄大小的不同，可能需要幾個小時到一天的時間，大型目錄則可能需要兩天)。</span><span class="sxs-lookup"><span data-stu-id="5365a-177">Ensure you wait long enough before retrying authentication (depending on the size of your directory - a few hours to a day or two for large directories).</span></span>
  * <span data-ttu-id="5365a-178">如果在您驗證上述步驟之後問題仍持續發生，請嘗試重新啟動 Microsoft Azure AD 同步服務。</span><span class="sxs-lookup"><span data-stu-id="5365a-178">If the issue persists after verifying the preceding steps, try restarting the Microsoft Azure AD Sync Service.</span></span> <span data-ttu-id="5365a-179">在您的同步電腦上，啟動命令提示字元，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="5365a-179">From your sync machine, launch a command prompt and execute the following commands:</span></span>

    1. <span data-ttu-id="5365a-180">net stop 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="5365a-180">net stop 'Microsoft Azure AD Sync'</span></span>
    2. <span data-ttu-id="5365a-181">net start 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="5365a-181">net start 'Microsoft Azure AD Sync'</span></span>
* <span data-ttu-id="5365a-182">**僅限雲端帳戶**：如果受影響的使用者帳戶是僅限雲端的使用者帳戶，請確定在您啟用 Azure AD 網域服務之後，使用者已變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="5365a-182">**Cloud-only accounts**: If the affected user account is a cloud-only user account, ensure that the user has changed their password after you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="5365a-183">這個步驟會導致產生 Azure AD 網域服務所需的認證雜湊。</span><span class="sxs-lookup"><span data-stu-id="5365a-183">This step causes the credential hashes required for Azure AD Domain Services to be generated.</span></span>

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a><span data-ttu-id="5365a-184">不會從受管理的網域中移除從 Azure AD 租用戶移除的使用者</span><span class="sxs-lookup"><span data-stu-id="5365a-184">Users removed from your Azure AD tenant are not removed from your managed domain</span></span>
<span data-ttu-id="5365a-185">Azure AD 會防止您意外刪除使用者物件。</span><span class="sxs-lookup"><span data-stu-id="5365a-185">Azure AD protects you from accidental deletion of user objects.</span></span> <span data-ttu-id="5365a-186">當您從您的 Azure AD 租用戶刪除使用者帳戶時，對應的使用者物件會移至資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="5365a-186">When you delete a user account from your Azure AD tenant, the corresponding user object is moved to the Recycle Bin.</span></span> <span data-ttu-id="5365a-187">此刪除作業同步處理至受管理的網域時，會導致對應的使用者帳戶被標記為已停用。</span><span class="sxs-lookup"><span data-stu-id="5365a-187">When this delete operation is synchronized to your managed domain, it causes the corresponding user account to be marked disabled.</span></span> <span data-ttu-id="5365a-188">這項功能可協助您稍後復原或取消刪除使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5365a-188">This feature helps you recover or undelete the user account later.</span></span>

<span data-ttu-id="5365a-189">即使您在 Azure AD 目錄中使用相同的 UPN 重新建立使用者帳戶，使用者帳戶在您的受管理網域中仍會維持停用狀態。</span><span class="sxs-lookup"><span data-stu-id="5365a-189">The user account remains in the disabled state in your managed domain, even if you re-create a user account with the same UPN in your Azure AD directory.</span></span> <span data-ttu-id="5365a-190">若要從受管理的網域移除使用者帳戶，請從您的 Azure AD 租用戶將它強制刪除。</span><span class="sxs-lookup"><span data-stu-id="5365a-190">To remove the user account from your managed domain, you need to force delete it from your Azure AD tenant.</span></span>

<span data-ttu-id="5365a-191">若要完全從受管理的網域移除使用者帳戶，請從您的 Azure AD 租用戶中永久刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="5365a-191">To remove the user account fully from your managed domain, delete the user permanently from your Azure AD tenant.</span></span> <span data-ttu-id="5365a-192">如這篇 [MSDN 文章](https://msdn.microsoft.com/library/azure/dn194132.aspx)所述，使用 Remove-MsolUser PowerShell Cmdlet 搭配 '-RemoveFromRecycleBin' 選項。</span><span class="sxs-lookup"><span data-stu-id="5365a-192">Use the Remove-MsolUser PowerShell cmdlet with the '-RemoveFromRecycleBin' option, as described in this [MSDN article](https://msdn.microsoft.com/library/azure/dn194132.aspx).</span></span>

## <a name="contact-us"></a><span data-ttu-id="5365a-193">與我們連絡</span><span class="sxs-lookup"><span data-stu-id="5365a-193">Contact Us</span></span>
<span data-ttu-id="5365a-194">請連絡 Azure Active Directory Domain Services 產品小組， [分享意見或尋求支援](active-directory-ds-contact-us.md)。</span><span class="sxs-lookup"><span data-stu-id="5365a-194">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span></span>
