---
title: "Azure AD 網域服務︰啟用密碼同步處理 | Microsoft Docs"
description: "開始使用 Azure Active Directory 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 947ea3c9d789ecf5a754001aafcda6f8bcd41047
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="5257a-103">啟用 Azure Active Directory Domain Services 的密碼同步</span><span class="sxs-lookup"><span data-stu-id="5257a-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="5257a-104">在先前工作中，您已啟用 Azure Active Directory (Azure AD) 租用戶的 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="5257a-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="5257a-105">下一項工作是啟用 NT LAN Manager (NTLM) 和 Kerberos 驗證所需的認證雜湊與 Azure AD Domain Services 的同步。</span><span class="sxs-lookup"><span data-stu-id="5257a-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="5257a-106">設定認證同步處理後，使用者即可使用他們的公司認證來登入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="5257a-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="5257a-107">僅限雲端使用者帳戶，與使用 Azure AD Connect 從內部部署目錄同步的使用者帳戶，其所含的步驟不同。</span><span class="sxs-lookup"><span data-stu-id="5257a-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="5257a-108">如果您的 Azure AD 租用戶同時具有僅限雲端使用者以及來自您內部部署 AD 的使用者，則需要執行兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="5257a-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="5257a-109">**僅限雲端使用者帳戶**：[將僅限雲端使用者帳戶的密碼同步到受管理的網域](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="5257a-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="5257a-110">**內部部署使用者帳戶**：[將從您內部部署 AD 同步之使用者帳戶的密碼同步到受管理的網域](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="5257a-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="5257a-111">工作 5：針對與內部部署 AD 同步的使用者帳戶啟用與受管理網域的密碼同步</span><span class="sxs-lookup"><span data-stu-id="5257a-111">Task 5: enable password synchronization to your managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="5257a-112">已同步處理的 Azure AD 租用戶會設定為使用 Azure AD Connect 來與您組織的內部部署目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="5257a-112">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="5257a-113">根據預設，Azure AD Connect 不會將 NTLM 和 Kerberos 認證雜湊同步到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="5257a-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD.</span></span> <span data-ttu-id="5257a-114">若要使用 Azure AD 網域服務，您需要設定 Azure AD Connect 以同步處理 NTLM 和 Kerberos 驗證所需的認證雜湊。</span><span class="sxs-lookup"><span data-stu-id="5257a-114">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="5257a-115">下列步驟能夠將必要的認證雜湊從內部部署目錄同步到 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5257a-115">The following steps enable synchronization of the required credential hashes from your on-premises directory to your Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="5257a-116">如果您的組織具有從您的內部部署目錄同步的使用者帳戶，則您必須啟用 NTLM 與 Kerberos 雜湊的同步，才能使用受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="5257a-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order to use the managed domain.</span></span> <span data-ttu-id="5257a-117">同步的使用者帳戶是已在內部部署目錄中建立的帳戶，並會使用 Azure AD Connect 同步到 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5257a-117">A synced user account is an account that was created in your on-premises directory and is synchronized to your Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="5257a-118">安裝或更新 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5257a-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="5257a-119">在已加入網域的電腦上安裝建議的最新 Azure AD Connect 版本。</span><span class="sxs-lookup"><span data-stu-id="5257a-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="5257a-120">如果您目前已設定 Azure AD Connect 的執行個體，則必須加以更新才能使用最新版的 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="5257a-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span></span> <span data-ttu-id="5257a-121">若要避免已知問題/錯誤可能已經修復，請確定您使用的是最新的 Azure AD Connect 版本。</span><span class="sxs-lookup"><span data-stu-id="5257a-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span></span>

<span data-ttu-id="5257a-122">**[下載 Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="5257a-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="5257a-123">建議版本：**1.1.553.0** - 已於 2017 年 6 月 27 日發佈。</span><span class="sxs-lookup"><span data-stu-id="5257a-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="5257a-124">您「必須」安裝建議的最新 Azure AD Connect 版本，才能將傳統密碼認證 (NTLM 和 Kerberos 驗證所需的認證) 同步處理到 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5257a-124">You MUST install the latest recommended release of Azure AD Connect to enable the legacy password credentials (required for NTLM and Kerberos authentication) to synchronize to your Azure AD tenant.</span></span> <span data-ttu-id="5257a-125">此功能無法在舊版的 Azure AD Connect 中使用，或與舊版 DirSync 工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5257a-125">This functionality is not available in prior releases of Azure AD Connect or with the legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="5257a-126">Azure AD Connect 的安裝指示可於下列文章中取得： [開始使用 Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="5257a-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a><span data-ttu-id="5257a-127">能夠將 NTLM 和 Kerberos 認證雜湊同步處理到 Azure AD</span><span class="sxs-lookup"><span data-stu-id="5257a-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span></span>
<span data-ttu-id="5257a-128">在每個 AD 樹系上執行下列 PowerShell 指令碼，以強制執行完整密碼同步處理，並能夠讓所有內部部署使用者的密碼雜湊同步處理到 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5257a-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span></span> <span data-ttu-id="5257a-129">此指令碼能夠讓 NTLM/Kerberos 驗證所需的認證雜湊同步處理到 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5257a-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="5257a-130">視目錄的大小而定 (使用者、群組等的數目)，將認證雜湊同步處理到 Azure AD 需要花一點時間。</span><span class="sxs-lookup"><span data-stu-id="5257a-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span></span> <span data-ttu-id="5257a-131">將認證雜湊同步處理到 Azure AD 之後，密碼短時間內就能在 Azure AD 網域服務管理的網域上使用。</span><span class="sxs-lookup"><span data-stu-id="5257a-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="5257a-132">相關內容</span><span class="sxs-lookup"><span data-stu-id="5257a-132">Related Content</span></span>
* [<span data-ttu-id="5257a-133">為僅限雲端的 Azure AD 目錄啟用 AAD 網域服務的密碼同步處理</span><span class="sxs-lookup"><span data-stu-id="5257a-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="5257a-134">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="5257a-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="5257a-135">將 Windows 虛擬機器加入 Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="5257a-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="5257a-136">將 Red Hat Enterprise Linux 虛擬機器加入 Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="5257a-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
