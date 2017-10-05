---
title: "設定 Multi-Factor Authentication - Azure SQL | Microsoft Docs"
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
ms.openlocfilehash: fd78b34e8bbefdaa79a73d69ff2a0e3c1c342e98
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a><span data-ttu-id="93754-103">設定適用於 SQL Server Management Studio 和 Azure AD 的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="93754-103">Configure multi-factor authentication for SQL Server Management Studio and Azure AD</span></span>

<span data-ttu-id="93754-104">本主題說明如何使用 Azure Active Directory 多重要素驗證 (MFA) 搭配 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="93754-104">This topic shows you how to use Azure Active Directory multi-factor authentication (MFA) with SQL Server Management Studio.</span></span> <span data-ttu-id="93754-105">將 SSMS 或 SqlPackage.exe 連線到 Azure SQL Database 和 Azure SQL 資料倉儲時，可以使用 Azure AD MFA。</span><span class="sxs-lookup"><span data-stu-id="93754-105">Azure AD MFA can be used when connecting SSMS or SqlPackage.exe to Azure SQL Database and Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="93754-106">如需 Azure SQL Database 多重要素驗證的概觀，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="93754-106">For an overview of Azure SQL Database multi-factor authentication, see [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>

## <a name="configuration-steps"></a><span data-ttu-id="93754-107">組態步驟</span><span class="sxs-lookup"><span data-stu-id="93754-107">Configuration steps</span></span>

1. <span data-ttu-id="93754-108">**設定 Azure Active Directory** - 如需詳細資訊，請參閱[管理 Azure AD 目錄](https://msdn.microsoft.com/library/azure/hh967611.aspx)、[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)、[將您自己的網域名稱新增至 Azure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)、[Microsoft Azure 現在支援與 Windows Server Active Directory 同盟](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)、[使用 Windows PowerShell 管理 Azure AD](https://msdn.microsoft.com/library/azure/jj151815.aspx)。</span><span class="sxs-lookup"><span data-stu-id="93754-108">**Configure an Azure Active Directory** - For more information, see [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), and [Manage Azure AD using Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx).</span></span>
2. <span data-ttu-id="93754-109">**設定 MFA** - 如需逐步指示，請參閱[什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)、[使用 Azure SQL Database 和資料倉儲的條件式存取 (MFA)](sql-database-conditional-access.md)。</span><span class="sxs-lookup"><span data-stu-id="93754-109">**Configure MFA** - For step-by-step instructions, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md), [Conditional Access (MFA) with Azure SQL Database and Data Warehouse](sql-database-conditional-access.md).</span></span> <span data-ttu-id="93754-110">(完全條件式存取需要進階 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="93754-110">(Full conditional access requires a Premium Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="93754-111">有限的 MFA 適用於標準 Azure AD。)</span><span class="sxs-lookup"><span data-stu-id="93754-111">Limited MFA is available with a standard Azure AD.)</span></span>
3. <span data-ttu-id="93754-112">**設定 SQL Database 或 SQL 資料倉儲進行 Azure AD 驗證** - 如需逐步指示，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database 或 SQL 資料倉儲](sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="93754-112">**Configure SQL Database or SQL Data Warehouse for Azure AD Authentication** - For step-by-step instructions, see [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>
4. <span data-ttu-id="93754-113">**下載 SSMS** - 在用戶端電腦上，從[下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) 下載最新的 SSMS。</span><span class="sxs-lookup"><span data-stu-id="93754-113">**Download SSMS** - On the client computer, download the latest SSMS, from [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> <span data-ttu-id="93754-114">對於本主題中的所有功能，至少使用 2017 年 7 月的 17.2 版。</span><span class="sxs-lookup"><span data-stu-id="93754-114">For all the features in this topic, use at least July 2017, version 17.2.</span></span>  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a><span data-ttu-id="93754-115">使用通用驗證搭配 SSMS 進行連線</span><span class="sxs-lookup"><span data-stu-id="93754-115">Connecting by using universal authentication with SSMS</span></span>

<span data-ttu-id="93754-116">下列步驟示範如何使用最新的 SSMS 連線至 SQL Database 或 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="93754-116">The following steps show how to connect to SQL Database or SQL Data Warehouse by using the latest SSMS.</span></span>

1. <span data-ttu-id="93754-117">若要使用通用驗證進行連線，請在 [連線到伺服器] 對話方塊中，選取 [Active Directory - 通用驗證搭配 MFA 支援]。</span><span class="sxs-lookup"><span data-stu-id="93754-117">To connect using Universal Authentication, on the **Connect to Server** dialog box, select **Active Directory - Universal with MFA support**.</span></span> <span data-ttu-id="93754-118">(如果您看到 **Active Directory 通用驗證**，則表示您不是使用最新的 SSMS 版本。)</span><span class="sxs-lookup"><span data-stu-id="93754-118">(If you see **Active Directory Universal Authentication** you are not on the latest version of SSMS.)</span></span>  
   <span data-ttu-id="93754-119">![1mfa-universal-connect][1]</span><span class="sxs-lookup"><span data-stu-id="93754-119">![1mfa-universal-connect][1]</span></span>  
2. <span data-ttu-id="93754-120">使用 Azure Active Directory 認證完成 [使用者名稱] 方塊 (採用 `user_name@domain.com` 格式)。</span><span class="sxs-lookup"><span data-stu-id="93754-120">Complete the **User name** box with the Azure Active Directory credentials, in the format `user_name@domain.com`.</span></span>  
   <span data-ttu-id="93754-121">![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)</span><span class="sxs-lookup"><span data-stu-id="93754-121">![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)</span></span>   
3. <span data-ttu-id="93754-122">如果您以來賓使用者身分進行連線，您必須按一下 [選項]，然後在 [連線屬性] 對話方塊中，完成 [AD 網域名稱或租用戶 ID] 方塊。</span><span class="sxs-lookup"><span data-stu-id="93754-122">If you are connecting as a guest user, you must click **Options**, and on the **Connection Property** dialog box, complete the **AD domain name or tenant ID** box.</span></span> <span data-ttu-id="93754-123">如需詳細資訊，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="93754-123">For more information, see [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>
   <span data-ttu-id="93754-124">![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)</span><span class="sxs-lookup"><span data-stu-id="93754-124">![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)</span></span>   
4. <span data-ttu-id="93754-125">如同平常針對 SQL Database 和 SQL 資料倉儲所做的一樣，您必須按一下 [選項]，然後在 [選項] 對話方塊上指定資料庫。</span><span class="sxs-lookup"><span data-stu-id="93754-125">As usual for SQL Database and SQL Data Warehouse, you must click **Options** and specify the database on the **Options** dialog box.</span></span> <span data-ttu-id="93754-126">(如果已連線的使用者是來賓使用者 (亦即joe@outlook.com)，您必須核取此方塊，並將目前的 AD 網域名稱或租用戶 ID 新增為 [選項] 的一部分。</span><span class="sxs-lookup"><span data-stu-id="93754-126">(If the connected user is a guest user ( i.e. joe@outlook.com), you must check the box and add the current AD domain name or tenant ID as part of Options.</span></span> <span data-ttu-id="93754-127">請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)]()(sql-database-ssms-mfa-authentication.md。</span><span class="sxs-lookup"><span data-stu-id="93754-127">See [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA)]()(sql-database-ssms-mfa-authentication.md.</span></span> <span data-ttu-id="93754-128">然後按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="93754-128">Then click **Connect**.</span></span>  
5. <span data-ttu-id="93754-129">當 [登入您的帳戶]  對話方塊顯示時，請提供您 Azure Active Directory 身分識別的帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="93754-129">When the **Sign in to your account** dialog box appears, provide the account and password of your Azure Active Directory identity.</span></span> <span data-ttu-id="93754-130">如果使用者不屬於與 Azure AD 同盟的網域，則不需要密碼。</span><span class="sxs-lookup"><span data-stu-id="93754-130">No password is required if a user is part of a domain federated with Azure AD.</span></span>  
   <span data-ttu-id="93754-131">![2mfa-sign-in][2]</span><span class="sxs-lookup"><span data-stu-id="93754-131">![2mfa-sign-in][2]</span></span>  

   > [!NOTE]
   > <span data-ttu-id="93754-132">如果是使用不需要 MFA 的帳戶進行通用驗證，則您可以在此時連線。</span><span class="sxs-lookup"><span data-stu-id="93754-132">For Universal Authentication with an account that does not require MFA, you connect at this point.</span></span> <span data-ttu-id="93754-133">對於需要 MFA 的使用者，請繼續執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="93754-133">For users requiring MFA, continue with the following steps:</span></span>
   >  
   
6. <span data-ttu-id="93754-134">可能會顯示兩個 MFA 設定對話方塊。</span><span class="sxs-lookup"><span data-stu-id="93754-134">Two MFA setup dialog boxes might appear.</span></span> <span data-ttu-id="93754-135">這個一次性作業是根據 MFA 系統管理員設定而定，因此可能是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="93754-135">This one time operation depends on the MFA administrator setting, and therefore may be optional.</span></span> <span data-ttu-id="93754-136">對於已啟用 MFA 的網域，有時會預先定義這個步驟 (例如，網域會要求使用者使用智慧卡和 pin)。</span><span class="sxs-lookup"><span data-stu-id="93754-136">For an MFA enabled domain this step is sometimes pre-defined (for example, the domain requires users to use a smartcard and pin).</span></span>  
   ![3mfa-setup][3]  
7. <span data-ttu-id="93754-138">第二個可能的一次性對話方塊可讓您選取驗證方法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="93754-138">The second possible one time dialog box allows you to select the details of your authentication method.</span></span> <span data-ttu-id="93754-139">可能的選項是由您的系統管理員所設定。</span><span class="sxs-lookup"><span data-stu-id="93754-139">The possible options are configured by your administrator.</span></span>  
   ![4mfa-verify-1][4]  
8. <span data-ttu-id="93754-141">Azure Active Directory 會傳送確認資訊給您。</span><span class="sxs-lookup"><span data-stu-id="93754-141">The Azure Active Directory sends the confirming information to you.</span></span> <span data-ttu-id="93754-142">當您收到驗證碼時，請將其輸入 [輸入驗證碼] 方塊，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="93754-142">When you receive the verification code, enter it into the **Enter verification code** box, and click **Sign in**.</span></span>  
   <span data-ttu-id="93754-143">![5mfa-verify-2][5]</span><span class="sxs-lookup"><span data-stu-id="93754-143">![5mfa-verify-2][5]</span></span>  

<span data-ttu-id="93754-144">驗證完成時，SSMS 即會正常連線 (假設認證和防火牆存取有效)。</span><span class="sxs-lookup"><span data-stu-id="93754-144">When verification is complete, SSMS connects normally presuming valid credentials and firewall access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93754-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93754-145">Next steps</span></span>

* <span data-ttu-id="93754-146">如需 Azure SQL Database 多重要素驗證的概觀，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="93754-146">For an overview of Azure SQL Database multi-factor authentication, see Universal Authentication with [SQL Database and SQL Data Warehouse (SSMS support for MFA)](sql-database-ssms-mfa-authentication.md).</span></span>
* <span data-ttu-id="93754-147">授與對資料庫的其他存取權：[SQL Database 驗證和授權：授與存取權](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="93754-147">Grant others access to your database: [SQL Database Authentication and Authorization: Granting Access](sql-database-manage-logins.md)</span></span>  
<span data-ttu-id="93754-148">確定其他人可透過防火牆連線：[使用 Azure 入口網站設定 Azure SQL Database 伺服器層級防火牆規則](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="93754-148">Make sure others can connect through the firewall: [Configure an Azure SQL Database server-level firewall rule using the Azure portal](sql-database-configure-firewall-settings.md)</span></span>


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

