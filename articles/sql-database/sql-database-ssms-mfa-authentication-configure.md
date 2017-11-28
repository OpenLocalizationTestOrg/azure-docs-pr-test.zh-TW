---
title: "aaaConfigure 多重要素驗證 Azure SQL |Microsoft 文件"
description: "針對 SQL Database 和 SQL 資料倉儲，搭配使用 Multi-Factor Authentication 與 SSMS。"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a><span data-ttu-id="6c7f4-103">設定適用於 SQL Server Management Studio 和 Azure AD 的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="6c7f4-103">Configure multi-factor authentication for SQL Server Management Studio and Azure AD</span></span>

<span data-ttu-id="6c7f4-104">本主題說明如何 toouse Azure Active Directory multi-factor authentication (MFA) 與 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-104">This topic shows you how toouse Azure Active Directory multi-factor authentication (MFA) with SQL Server Management Studio.</span></span> <span data-ttu-id="6c7f4-105">連接 SSMS 或 SqlPackage.exe tooAzure SQL Database 和 Azure SQL 資料倉儲時，就可以使用 azure AD MFA。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-105">Azure AD MFA can be used when connecting SSMS or SqlPackage.exe tooAzure SQL Database and Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="6c7f4-106">如需 Azure SQL Database 多重要素驗證的概觀，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-106">For an overview of Azure SQL Database multi-factor authentication, see [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>

## <a name="configuration-steps"></a><span data-ttu-id="6c7f4-107">組態步驟</span><span class="sxs-lookup"><span data-stu-id="6c7f4-107">Configuration steps</span></span>

1. <span data-ttu-id="6c7f4-108">**設定 Azure Active Directory** -如需詳細資訊，請參閱[管理 Azure AD 目錄](https://msdn.microsoft.com/library/azure/hh967611.aspx)，[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)，[加入您自己的網域名稱 tooAzure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)， [Microsoft Azure 現在支援與 Windows Server Active Directory 同盟](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)，和[使用 Windows PowerShell 管理 Azure AD](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c7f4-108">**Configure an Azure Active Directory** - For more information, see [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name tooAzure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), and [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span></span>
2. <span data-ttu-id="6c7f4-109">**設定 MFA** - 如需逐步指示，請參閱[什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)、[使用 Azure SQL Database 和資料倉儲的條件式存取 (MFA)](sql-database-conditional-access.md)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-109">**Configure MFA** - For step-by-step instructions, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md), [Conditional Access (MFA) with Azure SQL Database and Data Warehouse](sql-database-conditional-access.md).</span></span> <span data-ttu-id="6c7f4-110">(完全條件式存取需要進階 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-110">(Full conditional access requires a Premium Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6c7f4-111">有限的 MFA 適用於標準 Azure AD。)</span><span class="sxs-lookup"><span data-stu-id="6c7f4-111">Limited MFA is available with a standard Azure AD.)</span></span>
3. <span data-ttu-id="6c7f4-112">**設定 SQL Database 或 Azure AD 驗證的 SQL 資料倉儲**-如需逐步指示，請參閱[連接 tooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-112">**Configure SQL Database or SQL Data Warehouse for Azure AD Authentication** - For step-by-step instructions, see [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>
4. <span data-ttu-id="6c7f4-113">**下載 SSMS** -hello 用戶端電腦上，下載最新的 SSMS hello 從[下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-113">**Download SSMS** - On hello client computer, download hello latest SSMS, from [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> <span data-ttu-id="6c7f4-114">針對所有本主題中的 hello 功能，使用至少第 2017 年 7 月版本 17.2。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-114">For all hello features in this topic, use at least July 2017, version 17.2.</span></span>  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a><span data-ttu-id="6c7f4-115">使用通用驗證搭配 SSMS 進行連線</span><span class="sxs-lookup"><span data-stu-id="6c7f4-115">Connecting by using universal authentication with SSMS</span></span>

<span data-ttu-id="6c7f4-116">hello 下列步驟顯示如何 tooconnect tooSQL 資料庫或使用 SQL 資料倉儲 hello 最新的 SSMS。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-116">hello following steps show how tooconnect tooSQL Database or SQL Data Warehouse by using hello latest SSMS.</span></span>

1. <span data-ttu-id="6c7f4-117">hello 上使用通用的驗證，tooconnect**連接 tooServer**對話方塊中，選取**Active Directory-MFA 支援與通用**。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-117">tooconnect using Universal Authentication, on hello **Connect tooServer** dialog box, select **Active Directory - Universal with MFA support**.</span></span> <span data-ttu-id="6c7f4-118">(如果您看到**Active Directory 通用驗證**您不在 hello 最新版本的 SSMS。)</span><span class="sxs-lookup"><span data-stu-id="6c7f4-118">(If you see **Active Directory Universal Authentication** you are not on hello latest version of SSMS.)</span></span>  
   <span data-ttu-id="6c7f4-119">![1mfa-universal-connect][1]</span><span class="sxs-lookup"><span data-stu-id="6c7f4-119">![1mfa-universal-connect][1]</span></span>  
2. <span data-ttu-id="6c7f4-120">完整的 hello**使用者名**hello Azure Active Directory 的認證，格式為 hello 方塊`user_name@domain.com`。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-120">Complete hello **User name** box with hello Azure Active Directory credentials, in hello format `user_name@domain.com`.</span></span>  
   <span data-ttu-id="6c7f4-121">![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)</span><span class="sxs-lookup"><span data-stu-id="6c7f4-121">![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)</span></span>   
3. <span data-ttu-id="6c7f4-122">如果您要的來賓使用者身分連接，您必須按一下**選項**，在 hello**連接屬性**對話方塊中，完成 hello **AD 網域名稱或租用戶識別碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-122">If you are connecting as a guest user, you must click **Options**, and on hello **Connection Property** dialog box, complete hello **AD domain name or tenant ID** box.</span></span> <span data-ttu-id="6c7f4-123">如需詳細資訊，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-123">For more information, see [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>
   <span data-ttu-id="6c7f4-124">![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)</span><span class="sxs-lookup"><span data-stu-id="6c7f4-124">![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)</span></span>   
4. <span data-ttu-id="6c7f4-125">如往常般 SQL Database 和 SQL 資料倉儲，您必須按一下**選項**hello 來指定 hello 資料庫**選項** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-125">As usual for SQL Database and SQL Data Warehouse, you must click **Options** and specify hello database on hello **Options** dialog box.</span></span> <span data-ttu-id="6c7f4-126">(如果 hello 連線使用者是 guest 使用者 (亦即joe@outlook.com)，您必須檢查 hello 方塊，並加入 hello 目前的 AD 網域名稱或租用戶識別碼作為選項的一部分。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-126">(If hello connected user is a guest user ( i.e. joe@outlook.com), you must check hello box and add hello current AD domain name or tenant ID as part of Options.</span></span> <span data-ttu-id="6c7f4-127">請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)]()(sql-database-ssms-mfa-authentication.md。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-127">See [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)]()(sql-database-ssms-mfa-authentication.md.</span></span> <span data-ttu-id="6c7f4-128">然後按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-128">Then click **Connect**.</span></span>  
5. <span data-ttu-id="6c7f4-129">當 hello**登入帳戶 tooyour**出現對話方塊，請提供 hello 帳戶與 Azure Active Directory 身分識別的密碼。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-129">When hello **Sign in tooyour account** dialog box appears, provide hello account and password of your Azure Active Directory identity.</span></span> <span data-ttu-id="6c7f4-130">如果使用者不屬於與 Azure AD 同盟的網域，則不需要密碼。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-130">No password is required if a user is part of a domain federated with Azure AD.</span></span>  
   <span data-ttu-id="6c7f4-131">![2mfa-sign-in][2]</span><span class="sxs-lookup"><span data-stu-id="6c7f4-131">![2mfa-sign-in][2]</span></span>  

   > [!NOTE]
   > <span data-ttu-id="6c7f4-132">如果是使用不需要 MFA 的帳戶進行通用驗證，則您可以在此時連線。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-132">For Universal Authentication with an account that does not require MFA, you connect at this point.</span></span> <span data-ttu-id="6c7f4-133">使用者要求 MFA，繼續執行步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c7f4-133">For users requiring MFA, continue with hello following steps:</span></span>
   >  
   
6. <span data-ttu-id="6c7f4-134">可能會顯示兩個 MFA 設定對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-134">Two MFA setup dialog boxes might appear.</span></span> <span data-ttu-id="6c7f4-135">此一次作業取決於 hello MFA 系統管理員設定，並因此可能會是選擇性。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-135">This one time operation depends on hello MFA administrator setting, and therefore may be optional.</span></span> <span data-ttu-id="6c7f4-136">MFA 啟用網域中的這個步驟是有時候預先定義 （例如，hello 網域都需要使用者 toouse 智慧卡和 pin 碼）。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-136">For an MFA enabled domain this step is sometimes pre-defined (for example, hello domain requires users toouse a smartcard and pin).</span></span>  
   ![3mfa-setup][3]  
7. <span data-ttu-id="6c7f4-138">hello 第二個可行對話方塊可讓您 tooselect hello 詳細資料的驗證方法一次。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-138">hello second possible one time dialog box allows you tooselect hello details of your authentication method.</span></span> <span data-ttu-id="6c7f4-139">您的系統管理員可以設定 hello 可能的選項。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-139">hello possible options are configured by your administrator.</span></span>  
   ![4mfa-verify-1][4]  
8. <span data-ttu-id="6c7f4-141">hello Azure Active Directory 會傳送確認資訊 tooyou hello。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-141">hello Azure Active Directory sends hello confirming information tooyou.</span></span> <span data-ttu-id="6c7f4-142">當您收到 hello 驗證碼時，請將其輸入 hello**輸入驗證碼**方塊，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-142">When you receive hello verification code, enter it into hello **Enter verification code** box, and click **Sign in**.</span></span>  
   <span data-ttu-id="6c7f4-143">![5mfa-verify-2][5]</span><span class="sxs-lookup"><span data-stu-id="6c7f4-143">![5mfa-verify-2][5]</span></span>  

<span data-ttu-id="6c7f4-144">驗證完成時，SSMS 即會正常連線 (假設認證和防火牆存取有效)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-144">When verification is complete, SSMS connects normally presuming valid credentials and firewall access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c7f4-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c7f4-145">Next steps</span></span>

* <span data-ttu-id="6c7f4-146">如需 Azure SQL Database 多重要素驗證的概觀，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="6c7f4-146">For an overview of Azure SQL Database multi-factor authentication, see Universal Authentication with [SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>
* <span data-ttu-id="6c7f4-147">授與其他人存取 tooyour 資料庫： [SQL Database 驗證和授權： 授與存取權](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="6c7f4-147">Grant others access tooyour database: [SQL Database Authentication and Authorization: Granting Access](sql-database-manage-logins.md)</span></span>  
<span data-ttu-id="6c7f4-148">請確定其他人可以透過 hello 防火牆連線：[設定 Azure SQL Database 伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="6c7f4-148">Make sure others can connect through hello firewall: [Configure an Azure SQL Database server-level firewall rule using hello Azure portal](sql-database-configure-firewall-settings.md)</span></span>


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

