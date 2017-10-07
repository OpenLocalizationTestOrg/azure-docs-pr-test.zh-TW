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
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="bd5e8-103">啟用密碼同步處理 tooAzure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="bd5e8-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="bd5e8-104">在先前工作中，您已啟用 Azure Active Directory (Azure AD) 租用戶的 Azure Active Directory Domain Services。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="bd5e8-105">hello 下一個工作是 tooenable 認證雜湊同步處理所需的 NT LAN Manager (NTLM) 和 Kerberos 驗證 tooAzure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="bd5e8-106">您已設定認證同步處理之後，使用者可以登入 toohello 受管理的網域，利用其公司認證。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="bd5e8-107">所需的 hello 步驟截然不同的僅限雲端的使用者帳戶與使用者帳戶從您使用 Azure AD Connect 的內部部署目錄同步。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="bd5e8-108">必須有 Azure AD 租用戶的組合雲端唯一的使用者和使用者從您內部部署 AD 中，您需要 tooperform 這兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="bd5e8-109">**僅限雲端的使用者帳戶**:[為僅限雲端的使用者帳戶 tooyour 受管理的網域，同步處理密碼](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="bd5e8-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="bd5e8-110">**在內部部署使用者帳戶**:[從您在內部同步處理的使用者帳戶的密碼同步處理 AD tooyour 管理網域](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="bd5e8-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="bd5e8-111">工作 5： 啟用密碼同步處理 tooyour 受管理的網域使用者帳戶與您在內部同步處理 AD</span><span class="sxs-lookup"><span data-stu-id="bd5e8-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="bd5e8-112">同步處理 Azure AD 租用戶與您的組織在內部部署目錄使用 Azure AD Connect 設定 toosynchronize。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="bd5e8-113">根據預設，Azure AD Connect 不會同步處理，NTLM 和 Kerberos 認證雜湊 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="bd5e8-114">toouse Azure AD 網域服務，您需要 tooconfigure Azure AD Connect toosynchronize 認證雜湊所需的 NTLM 和 Kerberos 驗證。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="bd5e8-115">hello 下列步驟啟用所需的 hello 認證雜湊，從內部部署目錄 tooyour Azure AD 租用戶的同步處理。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="bd5e8-116">如果您的組織有從您的內部部署目錄，您必須同步的使用者帳戶啟用的 NTLM 和 Kerberos 順序 toouse hello 受管理的網域中的雜湊同步處理。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="bd5e8-117">同步處理的使用者帳戶是已在內部部署目錄中建立，並且為帳戶同步處理 tooyour 使用 Azure AD Connect 的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="bd5e8-118">安裝或更新 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="bd5e8-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="bd5e8-119">安裝 hello 建議的最新版本的網域上的 Azure AD Connect 加入電腦。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="bd5e8-120">如果您有 Azure AD Connect 的安裝程式的現有執行個體，您需要 tooupdate 它 toouse hello 最新版的 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="bd5e8-121">tooavoid 已知問題/可能有已獲得修正的 bug，請確定您一律使用 Azure AD connect 的 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="bd5e8-122">**[下載 Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="bd5e8-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="bd5e8-123">建議版本：**1.1.553.0** - 已於 2017 年 6 月 27 日發佈。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="bd5e8-124">您必須安裝 hello 建議的最新版本的 Azure AD Connect tooenable hello 舊版的密碼 （NTLM 和 Kerberos 驗證所需） 認證 toosynchronize tooyour Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="bd5e8-125">無法在舊版本的 Azure AD Connect，或使用 hello 舊版目錄同步工具中使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="bd5e8-126">Azure AD Connect 的安裝指示可用於 hello 下列文件-[開始使用 Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="bd5e8-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="bd5e8-127">啟用 NTLM 和 Kerberos 認證雜湊 tooAzure AD 同步的處理</span><span class="sxs-lookup"><span data-stu-id="bd5e8-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="bd5e8-128">執行下列 PowerShell 指令碼在每個 AD 樹系，tooforce 完整密碼同步處理，hello，並啟用所有在內部部署使用者的認證雜湊 toosync tooyour Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="bd5e8-129">此指令碼可讓 hello NTLM/Kerberos 驗證 toobe 同步的 tooyour Azure AD 租用戶所需的認證雜湊。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

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

<span data-ttu-id="bd5e8-130">視您的目錄 hello 大小而定 (數字的使用者，群組等)，同步處理的認證雜湊的 tooAzure AD 花的時間。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="bd5e8-131">hello 密碼便可以使用 hello Azure AD 網域服務受管理的網域上 hello 認證雜湊已同步處理 tooAzure AD 後不久。</span><span class="sxs-lookup"><span data-stu-id="bd5e8-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="bd5e8-132">相關內容</span><span class="sxs-lookup"><span data-stu-id="bd5e8-132">Related Content</span></span>
* [<span data-ttu-id="bd5e8-133">啟用密碼同步處理 tooAAD 網域服務，僅限雲端的 azure AD 目錄</span><span class="sxs-lookup"><span data-stu-id="bd5e8-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="bd5e8-134">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="bd5e8-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="bd5e8-135">加入 Windows 虛擬機器 tooan Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="bd5e8-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="bd5e8-136">加入 Red Hat Enterprise Linux 虛擬機器 tooan Azure AD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="bd5e8-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
