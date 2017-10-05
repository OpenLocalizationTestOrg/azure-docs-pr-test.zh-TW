---
title: "條件式存取 - Azure SQL Database 和 Data Warehouse | Microsoft Doc"
description: "了解如何設定 Azure SQL Database 和資料倉儲的條件式存取。"
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: 0dcec61c03a84197e2c351761c743683caa98a06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a><span data-ttu-id="1bede-103">使用 Azure SQL Database 和資料倉儲的條件式存取 (MFA)</span><span class="sxs-lookup"><span data-stu-id="1bede-103">Conditional Access (MFA) with Azure SQL Database and Data Warehouse</span></span>  

<span data-ttu-id="1bede-104">SQL Database 和 SQL 資料倉儲都支援 Microsoft 條件式存取。</span><span class="sxs-lookup"><span data-stu-id="1bede-104">Both SQL Database and SQL Data Warehouse support Microsoft Conditional Access.</span></span> <span data-ttu-id="1bede-105">下列步驟示範如何將 SQL Database 設定為強制執行條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="1bede-105">The following steps show how to configure SQL Database to enforce a Conditional Access policy.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="1bede-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="1bede-106">Prerequisites</span></span>  
- <span data-ttu-id="1bede-107">您必須將 SQL Database 或 SQL 資料倉儲設定為支援 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="1bede-107">You must configure your SQL Database or SQL Data Warehouse to support Azure Active Directory authentication.</span></span> <span data-ttu-id="1bede-108">如需特定步驟，請參閱[使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證](sql-database-aad-authentication-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1bede-108">For specific steps, see [Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication-configure.md).</span></span>  
- <span data-ttu-id="1bede-109">啟用多重要素驗證時，您必須在支援的工具進行連線，例如最新的 SSMS。</span><span class="sxs-lookup"><span data-stu-id="1bede-109">When multi-factor authentication is enabled, you must connect with at supported tool, such as the latest SSMS.</span></span> <span data-ttu-id="1bede-110">如需詳細資訊，請參閱[設定適用於 SQL Server Management Studio 的 Azure SQL Database 多重要素驗證](sql-database-ssms-mfa-authentication-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1bede-110">For more information, see [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).</span></span>  

## <a name="configure-ca-for-azure-sql-dbdw"></a><span data-ttu-id="1bede-111">針對 Azure SQL DB/DW 設定 CA</span><span class="sxs-lookup"><span data-stu-id="1bede-111">Configure CA for Azure SQL DB/DW</span></span>  
1.  <span data-ttu-id="1bede-112">登入入口網站、選取 **Azure Active Directory**，然後選取**條件式存取**。</span><span class="sxs-lookup"><span data-stu-id="1bede-112">Sign in to the Portal, select **Azure Active Directory**, and then select **Conditional access**.</span></span> <span data-ttu-id="1bede-113">如需詳細資訊，請參閱 [Azure Active Directory 條件式存取的技術參考](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference)。</span><span class="sxs-lookup"><span data-stu-id="1bede-113">For more information, see [Azure Active Directory Conditional Access technical reference](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).</span></span>  
  <span data-ttu-id="1bede-114">![[條件式存取] 刀鋒視窗](./media/sql-database-conditional-access/conditional-access-blade.png)</span><span class="sxs-lookup"><span data-stu-id="1bede-114">![conditional access blade](./media/sql-database-conditional-access/conditional-access-blade.png)</span></span> 
     
2.  <span data-ttu-id="1bede-115">在 [條件式存取原則] 刀鋒視窗中，按一下 [新增原則]、提供名稱，然後按一下 [設定規則]。</span><span class="sxs-lookup"><span data-stu-id="1bede-115">In the **Conditional Access-Policies** blade, click **New policy**, provide a name, and then click **Configure rules**.</span></span>  
3.  <span data-ttu-id="1bede-116">在 [指派] 下，選取 [使用者和群組]，核取 [選取使用者和群組]，然後選取要進行條件式存取的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="1bede-116">Under **Assignments**, select **Users and groups**, check **Select users and groups**, and then select the user or group for conditional access.</span></span> <span data-ttu-id="1bede-117">按一下 [選取]，然後按一下 [完成] 可接受您的選擇。</span><span class="sxs-lookup"><span data-stu-id="1bede-117">Click **Select**, and then click **Done** to accept your selection.</span></span>  
  <span data-ttu-id="1bede-118">![選取 [使用者和群組]](./media/sql-database-conditional-access/select-users-and-groups.png)</span><span class="sxs-lookup"><span data-stu-id="1bede-118">![select users and groups](./media/sql-database-conditional-access/select-users-and-groups.png)</span></span>  

4.  <span data-ttu-id="1bede-119">選取 [雲端應用程式]，按一下 [選取應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1bede-119">Select **Cloud apps**, click **Select apps**.</span></span> <span data-ttu-id="1bede-120">您會看到所有可供條件式存取使用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bede-120">You see all apps available for conditional access.</span></span> <span data-ttu-id="1bede-121">選取底部的 [Azure SQL Database]按一下 [選取]然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1bede-121">Select **Azure SQL Database**, at the bottom click **Select**, and then click **Done**.</span></span>  
  <span data-ttu-id="1bede-122">![選取 SQL Database](./media/sql-database-conditional-access/select-sql-database.png)</span><span class="sxs-lookup"><span data-stu-id="1bede-122">![select SQL Database](./media/sql-database-conditional-access/select-sql-database.png)</span></span>  
  <span data-ttu-id="1bede-123">如果找不到下列第三個螢幕擷取畫面中所列的 **Azure SQL Database**，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1bede-123">If you can’t find **Azure SQL Database** listed in the following third screen shot, complete the following steps:</span></span>   
  - <span data-ttu-id="1bede-124">使用 SSMS 搭配 AAD 管理帳戶來登入您的 Azure SQL DB/DW 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1bede-124">Sign in to your Azure SQL DB/DW instance using SSMS with an AAD admin account.</span></span>  
  - <span data-ttu-id="1bede-125">執行 `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`。</span><span class="sxs-lookup"><span data-stu-id="1bede-125">Execute `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.</span></span>  
  - <span data-ttu-id="1bede-126">登入 AAD，並確認 Azure SQL Database 和資料倉儲已列在 AAD 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1bede-126">Sign in to AAD and verify that Azure SQL Database and Data Warehouse are listed in the applications in your AAD.</span></span>  

5.  <span data-ttu-id="1bede-127">依序選取 [存取控制]、[授與]，然後核取您想要套用的原則。</span><span class="sxs-lookup"><span data-stu-id="1bede-127">Select **Access controls**, select **Grant**, and then check the policy you want to apply.</span></span> <span data-ttu-id="1bede-128">例如，我們選取 [需要多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="1bede-128">For this example, we select **Require multi-factor authentication**.</span></span>  
  <span data-ttu-id="1bede-129">![選取授與存取權](./media/sql-database-conditional-access/grant-access.png)</span><span class="sxs-lookup"><span data-stu-id="1bede-129">![select grant access](./media/sql-database-conditional-access/grant-access.png)</span></span>  

## <a name="summary"></a><span data-ttu-id="1bede-130">摘要</span><span class="sxs-lookup"><span data-stu-id="1bede-130">Summary</span></span>  
<span data-ttu-id="1bede-131">允許使用 Azure AD Premium 連線到 Azure SQL DB/DW 的選取應用程式 (Azure SQL Database)，現在會強制執行選取的條件式存取原則，**必要的多重要素驗證。**</span><span class="sxs-lookup"><span data-stu-id="1bede-131">The selected application (Azure SQL Database) allowing to connect to Azure SQL DB/DW using Azure AD Premium, now enforces the selected Conditional Access policy, **Required multi-factor authentication.**</span></span>  
<span data-ttu-id="1bede-132">若有關於多重要素驗證的 Azure SQL Database 和資料倉儲相關問題，請連絡 MFAforSQLDB@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="1bede-132">For questions about Azure SQL Database and Data Warehouse regarding multi-factor authentication, contact MFAforSQLDB@microsoft.com.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1bede-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1bede-133">Next steps</span></span>  

<span data-ttu-id="1bede-134">如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="1bede-134">For a tutorial, see [Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>
