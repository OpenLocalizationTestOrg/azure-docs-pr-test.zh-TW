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
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a><span data-ttu-id="be4ec-103">Azure AD 網域服務 - 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="be4ec-103">Azure AD Domain Services - Troubleshooting guide</span></span>
<span data-ttu-id="be4ec-104">這篇文章提供設定或管理 Azure Active Directory (AD) 網域服務時，可能會遇到的問題之疑難排解提示。</span><span class="sxs-lookup"><span data-stu-id="be4ec-104">This article provides troubleshooting hints for issues you may encounter when setting up or administering Azure Active Directory (AD) Domain Services.</span></span>

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a><span data-ttu-id="be4ec-105">您無法為 Azure AD 目錄啟用 Azure AD 網域服務</span><span class="sxs-lookup"><span data-stu-id="be4ec-105">You cannot enable Azure AD Domain Services for your Azure AD directory</span></span>
<span data-ttu-id="be4ec-106">本節可協助您疑難排解錯誤時嘗試 tooenable 您目錄的 Azure AD 網域服務和失敗或取得切換後 too'Disabled'。</span><span class="sxs-lookup"><span data-stu-id="be4ec-106">This section helps you troubleshoot errors when you try tooenable Azure AD Domain Services for your directory and it fails or gets toggled back too'Disabled'.</span></span>

<span data-ttu-id="be4ec-107">挑選 hello 對應 toohello 您遇到的錯誤訊息的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="be4ec-107">Pick hello troubleshooting steps that correspond toohello error message you encounter.</span></span>

| <span data-ttu-id="be4ec-108">**錯誤訊息**</span><span class="sxs-lookup"><span data-stu-id="be4ec-108">**Error Message**</span></span> | <span data-ttu-id="be4ec-109">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="be4ec-109">**Resolution**</span></span> |
| --- |:--- |
| <span data-ttu-id="be4ec-110">*hello 名稱 contoso100.com 已在此網路上的使用中。指定未使用的名稱。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-110">*hello name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span> |[<span data-ttu-id="be4ec-111">Hello 虛擬網路中的網域名稱衝突</span><span class="sxs-lookup"><span data-stu-id="be4ec-111">Domain name conflict in hello virtual network</span></span>](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| <span data-ttu-id="be4ec-112">*無法在此 Azure AD 租用戶中啟用網域服務。hello 服務沒有足夠的權限 toohello 應用程式呼叫 Azure AD 網域服務同步'。刪除呼叫 'Azure AD 網域服務同步處理' hello 應用程式，然後再次嘗試您的 Azure AD 租用戶的 tooenable 網域服務。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-112">*Domain Services could not be enabled in this Azure AD tenant. hello service does not have adequate permissions toohello application called 'Azure AD Domain Services Sync'. Delete hello application called 'Azure AD Domain Services Sync' and then try tooenable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="be4ec-113">沒有足夠的權限 toohello Azure AD 網域服務同步處理應用程式網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-113">Domain Services does not have adequate permissions toohello Azure AD Domain Services Sync application</span></span>](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| <span data-ttu-id="be4ec-114">*無法在此 Azure AD 租用戶中啟用網域服務。hello Azure AD 租用戶中的應用程式不會不會有 hello 的網域服務所需的權限 tooenable 網域服務。刪除與 hello 應用程式識別碼 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-114">*Domain Services could not be enabled in this Azure AD tenant. hello Domain Services application in your Azure AD tenant does not have hello required permissions tooenable Domain Services. Delete hello application with hello application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try tooenable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="be4ec-115">hello 網域服務應用程式未正確設定您的租用戶中</span><span class="sxs-lookup"><span data-stu-id="be4ec-115">hello Domain Services application is not configured properly in your tenant</span></span>](active-directory-ds-troubleshooting.md#invalid-configuration) |
| <span data-ttu-id="be4ec-116">*無法在此 Azure AD 租用戶中啟用網域服務。hello Microsoft Azure AD 應用程式已停用 Azure AD 租用戶中。啟用與 hello 應用程式識別碼 00000002-0000-0000-c000-000000000000 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-116">*Domain Services could not be enabled in this Azure AD tenant. hello Microsoft Azure AD application is disabled in your Azure AD tenant. Enable hello application with hello application identifier 00000002-0000-0000-c000-000000000000 and then try tooenable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="be4ec-117">Azure AD 租用戶中的 hello Microsoft Graph 應用程式已停用</span><span class="sxs-lookup"><span data-stu-id="be4ec-117">hello Microsoft Graph application is disabled in your Azure AD tenant</span></span>](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a><span data-ttu-id="be4ec-118">網域名稱衝突</span><span class="sxs-lookup"><span data-stu-id="be4ec-118">Domain Name conflict</span></span>
<span data-ttu-id="be4ec-119">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-119">**Error message:**</span></span>

<span data-ttu-id="be4ec-120">*hello 名稱 contoso100.com 已在此網路上的使用中。指定未使用的名稱。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-120">*hello name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span>

<span data-ttu-id="be4ec-121">**補救：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-121">**Remediation:**</span></span>

<span data-ttu-id="be4ec-122">請確定您沒有現有的網域 hello 與該虛擬網路上可用的相同網域名稱。</span><span class="sxs-lookup"><span data-stu-id="be4ec-122">Ensure that you do not have an existing domain with hello same domain name available on that virtual network.</span></span> <span data-ttu-id="be4ec-123">比方說，假設您擁有 hello 選取的虛擬網路上呼叫 'contoso.com' 已存在的網域。</span><span class="sxs-lookup"><span data-stu-id="be4ec-123">For instance, assume you have a domain called 'contoso.com' already available on hello selected virtual network.</span></span> <span data-ttu-id="be4ec-124">您嘗試 tooenable hello 與 Azure AD 網域服務受管理網域的更新版本中，該虛擬網路上相同的網域名稱 (也就是 ' contoso.com')。</span><span class="sxs-lookup"><span data-stu-id="be4ec-124">Later, you try tooenable an Azure AD Domain Services managed domain with hello same domain name (that is, 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="be4ec-125">嘗試 tooenable Azure AD 網域服務時發生失敗。</span><span class="sxs-lookup"><span data-stu-id="be4ec-125">You encounter a failure when trying tooenable Azure AD Domain Services.</span></span>

<span data-ttu-id="be4ec-126">此失敗是由於 tooname hello 網域名稱，該虛擬網路上的衝突。</span><span class="sxs-lookup"><span data-stu-id="be4ec-126">This failure is due tooname conflicts for hello domain name on that virtual network.</span></span> <span data-ttu-id="be4ec-127">在此情況下，您必須使用不同的名稱 tooset 註冊您 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="be4ec-127">In this situation, you must use a different name tooset up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="be4ec-128">或者，可以解除佈建 hello 現有網域，然後繼續 tooenable Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-128">Alternately, you can de-provision hello existing domain and then proceed tooenable Azure AD Domain Services.</span></span>

### <a name="inadequate-permissions"></a><span data-ttu-id="be4ec-129">權限不足</span><span class="sxs-lookup"><span data-stu-id="be4ec-129">Inadequate permissions</span></span>
<span data-ttu-id="be4ec-130">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-130">**Error message:**</span></span>

<span data-ttu-id="be4ec-131">*無法在此 Azure AD 租用戶中啟用網域服務。hello 服務沒有足夠的權限 toohello 應用程式呼叫 Azure AD 網域服務同步'。刪除呼叫 'Azure AD 網域服務同步處理' hello 應用程式，然後再次嘗試您的 Azure AD 租用戶的 tooenable 網域服務。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-131">*Domain Services could not be enabled in this Azure AD tenant. hello service does not have adequate permissions toohello application called 'Azure AD Domain Services Sync'. Delete hello application called 'Azure AD Domain Services Sync' and then try tooenable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="be4ec-132">**補救：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-132">**Remediation:**</span></span>

<span data-ttu-id="be4ec-133">如果您的 Azure AD 目錄中沒有 hello 名稱 'Azure AD 網域服務同步處理' 的應用程式，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="be4ec-133">Check toosee if there is an application with hello name 'Azure AD Domain Services Sync' in your Azure AD directory.</span></span> <span data-ttu-id="be4ec-134">如果此應用程式存在，請將它刪除，然後再重新啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-134">If this application exists, delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="be4ec-135">執行 hello hello 應用程式和 toodelete hello 存在的步驟 toocheck 之後，如果存在 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="be4ec-135">Perform hello following steps toocheck for hello presence of hello application and toodelete it, if hello application exists:</span></span>

1. <span data-ttu-id="be4ec-136">瀏覽 toohello **Azure 傳統入口網站**([https://manage.windowsazure.com](https://manage.windowsazure.com))。</span><span class="sxs-lookup"><span data-stu-id="be4ec-136">Navigate toohello **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span></span>
2. <span data-ttu-id="be4ec-137">選取 hello **Active Directory** hello 左窗格上的節點。</span><span class="sxs-lookup"><span data-stu-id="be4ec-137">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="be4ec-138">選取 hello Azure AD 租用戶 （目錄），您想要 tooenable Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-138">Select hello Azure AD tenant (directory) for which you would like tooenable Azure AD Domain Services.</span></span>
4. <span data-ttu-id="be4ec-139">瀏覽 toohello**應用程式**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be4ec-139">Navigate toohello **Applications** tab.</span></span>
5. <span data-ttu-id="be4ec-140">選取 hello**我公司所擁有的應用程式**hello 下拉式清單中的選項。</span><span class="sxs-lookup"><span data-stu-id="be4ec-140">Select hello **Applications my company owns** option in hello dropdown.</span></span>
6. <span data-ttu-id="be4ec-141">檢查名為 [Azure AD 網域服務同步處理] 的應用程式。如果 hello 應用程式存在，繼續 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="be4ec-141">Check for an application called **Azure AD Domain Services Sync**. If hello application exists, proceed toodelete it.</span></span>
7. <span data-ttu-id="be4ec-142">一旦您刪除 hello 應用程式之後, 再試一次一次 tooenable Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-142">Once you have deleted hello application, try tooenable Azure AD Domain Services once again.</span></span>

### <a name="invalid-configuration"></a><span data-ttu-id="be4ec-143">無效的組態</span><span class="sxs-lookup"><span data-stu-id="be4ec-143">Invalid configuration</span></span>
<span data-ttu-id="be4ec-144">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-144">**Error message:**</span></span>

<span data-ttu-id="be4ec-145">*無法在此 Azure AD 租用戶中啟用網域服務。hello Azure AD 租用戶中的應用程式不會不會有 hello 的網域服務所需的權限 tooenable 網域服務。刪除與 hello 應用程式識別碼 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。*</span><span class="sxs-lookup"><span data-stu-id="be4ec-145">*Domain Services could not be enabled in this Azure AD tenant. hello Domain Services application in your Azure AD tenant does not have hello required permissions tooenable Domain Services. Delete hello application with hello application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try tooenable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="be4ec-146">**補救：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-146">**Remediation:**</span></span>

<span data-ttu-id="be4ec-147">如果您的 Azure AD 目錄中的 hello 名稱 'AzureActiveDirectoryDomainControllerServices' （具有 d87dcbc6-a371-462e-88e3-28ad15ec4e64 的應用程式識別碼） 的應用程式，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="be4ec-147">Check toosee if you have an application with hello name 'AzureActiveDirectoryDomainControllerServices' (with an application identifier of d87dcbc6-a371-462e-88e3-28ad15ec4e64) in your Azure AD directory.</span></span> <span data-ttu-id="be4ec-148">如果此應用程式，您需要 toodelete 它，然後重新啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-148">If this application exists, you need toodelete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="be4ec-149">使用下列 PowerShell 指令碼 toofind hello 應用程式的 hello，並將它刪除。</span><span class="sxs-lookup"><span data-stu-id="be4ec-149">Use hello following PowerShell script toofind hello application and delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="be4ec-150">此指令碼會使用 **Azure AD PowerShell 第 2 版** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="be4ec-150">This script uses **Azure AD PowerShell version 2** cmdlets.</span></span> <span data-ttu-id="be4ec-151">如需所有可用的 cmdlet 與 toodownload hello 模組的完整清單，讀取 hello [azure Ad PowerShell 參考文件](https://msdn.microsoft.com/library/azure/mt757189.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be4ec-151">For a full list of all available cmdlets and toodownload hello module, read hello [AzureAD PowerShell reference documentation](https://msdn.microsoft.com/library/azure/mt757189.aspx).</span></span>
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
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a><span data-ttu-id="be4ec-152">Microsoft Graph 已停用</span><span class="sxs-lookup"><span data-stu-id="be4ec-152">Microsoft Graph disabled</span></span>
<span data-ttu-id="be4ec-153">**錯誤訊息：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-153">**Error message:**</span></span>

<span data-ttu-id="be4ec-154">無法在此 Azure AD 租用戶中啟用網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-154">Domain Services could not be enabled in this Azure AD tenant.</span></span> <span data-ttu-id="be4ec-155">hello Microsoft Azure AD 應用程式已停用 Azure AD 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="be4ec-155">hello Microsoft Azure AD application is disabled in your Azure AD tenant.</span></span> <span data-ttu-id="be4ec-156">啟用與 hello 應用程式識別碼 00000002-0000-0000-c000-000000000000 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-156">Enable hello application with hello application identifier 00000002-0000-0000-c000-000000000000 and then try tooenable Domain Services for your Azure AD tenant.</span></span>

<span data-ttu-id="be4ec-157">**補救：**</span><span class="sxs-lookup"><span data-stu-id="be4ec-157">**Remediation:**</span></span>

<span data-ttu-id="be4ec-158">如果您已停用與 hello 識別項 00000002-0000-0000-c000-000000000000 應用程式，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="be4ec-158">Check toosee if you have disabled an application with hello identifier 00000002-0000-0000-c000-000000000000.</span></span> <span data-ttu-id="be4ec-159">此應用程式是 hello Microsoft Azure AD 應用程式，並提供 Graph API 存取 tooyour Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="be4ec-159">This application is hello Microsoft Azure AD application and provides Graph API access tooyour Azure AD tenant.</span></span> <span data-ttu-id="be4ec-160">Azure AD 網域服務需要您的 Azure AD 租用戶 tooyour 管理此應用程式啟用 toobe toosynchronize 網域。</span><span class="sxs-lookup"><span data-stu-id="be4ec-160">Azure AD Domain Services needs this application toobe enabled toosynchronize your Azure AD tenant tooyour managed domain.</span></span>

<span data-ttu-id="be4ec-161">tooresolve 這個錯誤，請啟用這個應用程式，然後再次嘗試您的 Azure AD 租用戶的 tooenable 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-161">tooresolve this error, enable this application and then try tooenable Domain Services for your Azure AD tenant.</span></span>

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="be4ec-162">使用者會無法 toosign toohello Azure AD 網域服務受管理的網域中</span><span class="sxs-lookup"><span data-stu-id="be4ec-162">Users are unable toosign in toohello Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="be4ec-163">如果您的 Azure AD 租用戶中的一個或多個使用者無法 toosign toohello 新建立的受管理的網域中，執行下列疑難排解步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ec-163">If one or more users in your Azure AD tenant are unable toosign in toohello newly created managed domain, perform hello following troubleshooting steps:</span></span>

* <span data-ttu-id="be4ec-164">**使用 UPN 格式登入：**再試一次 toosign 使用 hello UPN 的格式 (例如，'joeuser@contoso.com') 而不是 hello SAMAccountName 格式 ('CONTOSO\joeuser')。</span><span class="sxs-lookup"><span data-stu-id="be4ec-164">**Sign-in using UPN format:** Try toosign in using hello UPN format (for example, 'joeuser@contoso.com') instead of hello SAMAccountName format ('CONTOSO\joeuser').</span></span> <span data-ttu-id="be4ec-165">hello SAMAccountName 可能自動產生使用者的 UPN 前置詞太長，或 hello 相同 hello 受管理的網域上的其他使用者的身分。</span><span class="sxs-lookup"><span data-stu-id="be4ec-165">hello SAMAccountName may be automatically generated for users whose UPN prefix is overly long or is hello same as another user on hello managed domain.</span></span> <span data-ttu-id="be4ec-166">hello UPN 格式會保證 toobe Azure AD 租用戶內的唯一。</span><span class="sxs-lookup"><span data-stu-id="be4ec-166">hello UPN format is guaranteed toobe unique within an Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="be4ec-167">我們建議使用 hello UPN 格式 toosign toohello Azure AD 網域服務受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="be4ec-167">We recommend using hello UPN format toosign in toohello Azure AD Domain Services managed domain.</span></span>
>
>

* <span data-ttu-id="be4ec-168">請確定您有[啟用密碼同步處理](active-directory-ds-getting-started-password-sync.md)根據 hello hello 快速入門指南中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="be4ec-168">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with hello steps outlined in hello Getting Started guide.</span></span>
* <span data-ttu-id="be4ec-169">**外部帳戶：**確保 hello 受影響的使用者帳戶不是在 hello Azure AD 租用戶中的外部帳戶。</span><span class="sxs-lookup"><span data-stu-id="be4ec-169">**External accounts:** Ensure that hello affected user account is not an external account in hello Azure AD tenant.</span></span> <span data-ttu-id="be4ec-170">外部帳戶的範例包括 Microsoft 帳戶 (例如 joe@live.com) 或來自外部 Azure AD 目錄的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="be4ec-170">Examples of external accounts include Microsoft accounts (for example, 'joe@live.com') or user accounts from an external Azure AD directory.</span></span> <span data-ttu-id="be4ec-171">由於 Azure AD 網域服務並沒有這類使用者帳戶的認證，這些使用者無法登入 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="be4ec-171">Since Azure AD Domain Services does not have credentials for such user accounts, these users cannot sign in toohello managed domain.</span></span>
* <span data-ttu-id="be4ec-172">**同步處理帳戶：**如果 hello 受影響的使用者帳戶會從內部部署目錄同步處理，請確認：</span><span class="sxs-lookup"><span data-stu-id="be4ec-172">**Synced accounts:** If hello affected user accounts are synchronized from an on-premises directory, verify that:</span></span>

  * <span data-ttu-id="be4ec-173">您已部署或更新 toohello[建議的最新版本的 Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594)。</span><span class="sxs-lookup"><span data-stu-id="be4ec-173">You have deployed or updated toohello [latest recommended release of Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).</span></span>
  * <span data-ttu-id="be4ec-174">您已設定 Azure AD Connect 太[執行完整同步處理](active-directory-ds-getting-started-password-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="be4ec-174">You have configured Azure AD Connect too[perform a full synchronization](active-directory-ds-getting-started-password-sync.md).</span></span>
  * <span data-ttu-id="be4ec-175">根據您目錄中的 hello 大小，可能需要一些時間，使用者帳戶並認證雜湊 toobe 可在 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-175">Depending on hello size of your directory, it may take a while for user accounts and credential hashes toobe available in Azure AD Domain Services.</span></span> <span data-ttu-id="be4ec-176">請確定您等待足夠的時間後再重試 （取決於您的目錄-幾個小時 tooa 天，或兩個大型目錄 hello 大小） 的驗證。</span><span class="sxs-lookup"><span data-stu-id="be4ec-176">Ensure you wait long enough before retrying authentication (depending on hello size of your directory - a few hours tooa day or two for large directories).</span></span>
  * <span data-ttu-id="be4ec-177">如果之後驗證先前步驟的 hello hello 問題持續發生，請嘗試重新啟動 hello Microsoft Azure AD 同步服務。</span><span class="sxs-lookup"><span data-stu-id="be4ec-177">If hello issue persists after verifying hello preceding steps, try restarting hello Microsoft Azure AD Sync Service.</span></span> <span data-ttu-id="be4ec-178">同步作業機器，啟動命令提示字元並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ec-178">From your sync machine, launch a command prompt and execute hello following commands:</span></span>

    1. <span data-ttu-id="be4ec-179">net stop 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="be4ec-179">net stop 'Microsoft Azure AD Sync'</span></span>
    2. <span data-ttu-id="be4ec-180">net start 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="be4ec-180">net start 'Microsoft Azure AD Sync'</span></span>
* <span data-ttu-id="be4ec-181">**僅限雲端帳戶**： 如果 hello 受影響的使用者帳戶是僅限雲端的使用者帳戶，請確定該 hello 使用者在您啟用 Azure AD 網域服務之後變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="be4ec-181">**Cloud-only accounts**: If hello affected user account is a cloud-only user account, ensure that hello user has changed their password after you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="be4ec-182">這個步驟會導致 hello 認證所需的 Azure AD 網域服務 toobe 產生的雜湊。</span><span class="sxs-lookup"><span data-stu-id="be4ec-182">This step causes hello credential hashes required for Azure AD Domain Services toobe generated.</span></span>

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a><span data-ttu-id="be4ec-183">不會從受管理的網域中移除從 Azure AD 租用戶移除的使用者</span><span class="sxs-lookup"><span data-stu-id="be4ec-183">Users removed from your Azure AD tenant are not removed from your managed domain</span></span>
<span data-ttu-id="be4ec-184">Azure AD 會防止您意外刪除使用者物件。</span><span class="sxs-lookup"><span data-stu-id="be4ec-184">Azure AD protects you from accidental deletion of user objects.</span></span> <span data-ttu-id="be4ec-185">當您刪除使用者帳戶從 Azure AD 租用戶時，hello 對應使用者物件是移動的 toohello 資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="be4ec-185">When you delete a user account from your Azure AD tenant, hello corresponding user object is moved toohello Recycle Bin.</span></span> <span data-ttu-id="be4ec-186">當此刪除操作已同步的 tooyour 受管理的網域時，它會導致 hello 對應使用者帳戶 toobe 標示為已停用。</span><span class="sxs-lookup"><span data-stu-id="be4ec-186">When this delete operation is synchronized tooyour managed domain, it causes hello corresponding user account toobe marked disabled.</span></span> <span data-ttu-id="be4ec-187">這項功能可協助您復原，或稍後復原 hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="be4ec-187">This feature helps you recover or undelete hello user account later.</span></span>

<span data-ttu-id="be4ec-188">hello 使用者帳戶會保留在 hello 停用受管理的網域中的狀態，即使您重新建立使用者帳戶與 hello 相同 Azure AD 目錄中的 UPN。</span><span class="sxs-lookup"><span data-stu-id="be4ec-188">hello user account remains in hello disabled state in your managed domain, even if you re-create a user account with hello same UPN in your Azure AD directory.</span></span> <span data-ttu-id="be4ec-189">您需要 tooforce tooremove hello 受管理的網域中的使用者帳戶，從 Azure AD 租用戶刪除它。</span><span class="sxs-lookup"><span data-stu-id="be4ec-189">tooremove hello user account from your managed domain, you need tooforce delete it from your Azure AD tenant.</span></span>

<span data-ttu-id="be4ec-190">tooremove hello 的使用者帳戶完全受管理的網域中，永久刪除 hello 使用者從 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="be4ec-190">tooremove hello user account fully from your managed domain, delete hello user permanently from your Azure AD tenant.</span></span> <span data-ttu-id="be4ec-191">使用具有 hello hello Remove-msoluser PowerShell cmdlet '-RemoveFromRecycleBin' 選項，如下所述[MSDN 文章](https://msdn.microsoft.com/library/azure/dn194132.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be4ec-191">Use hello Remove-MsolUser PowerShell cmdlet with hello '-RemoveFromRecycleBin' option, as described in this [MSDN article](https://msdn.microsoft.com/library/azure/dn194132.aspx).</span></span>

## <a name="contact-us"></a><span data-ttu-id="be4ec-192">與我們連絡</span><span class="sxs-lookup"><span data-stu-id="be4ec-192">Contact Us</span></span>
<span data-ttu-id="be4ec-193">連絡 hello Azure Active Directory 網域服務的產品小組太[分享意見反應或尋求支援](active-directory-ds-contact-us.md)。</span><span class="sxs-lookup"><span data-stu-id="be4ec-193">Contact hello Azure Active Directory Domain Services product team too[share feedback or for support](active-directory-ds-contact-us.md).</span></span>
