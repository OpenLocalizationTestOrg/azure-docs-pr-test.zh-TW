---
title: "aaaConditional 存取-Azure SQL Database 和資料倉儲 |Microsoft 文件"
description: "深入了解如何針對 Azure SQL Database 和資料倉儲的 tooconfigure 條件式存取。"
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a><span data-ttu-id="60b3b-103">使用 Azure SQL Database 和資料倉儲的條件式存取 (MFA)</span><span class="sxs-lookup"><span data-stu-id="60b3b-103">Conditional Access (MFA) with Azure SQL Database and Data Warehouse</span></span>  

<span data-ttu-id="60b3b-104">SQL Database 和 SQL 資料倉儲都支援 Microsoft 條件式存取。</span><span class="sxs-lookup"><span data-stu-id="60b3b-104">Both SQL Database and SQL Data Warehouse support Microsoft Conditional Access.</span></span> <span data-ttu-id="60b3b-105">hello 下列步驟顯示如何 tooconfigure SQL Database tooenforce 條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="60b3b-105">hello following steps show how tooconfigure SQL Database tooenforce a Conditional Access policy.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="60b3b-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="60b3b-106">Prerequisites</span></span>  
- <span data-ttu-id="60b3b-107">您必須設定您的 SQL 資料庫或 SQL 資料倉儲 toosupport 的 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="60b3b-107">You must configure your SQL Database or SQL Data Warehouse toosupport Azure Active Directory authentication.</span></span> <span data-ttu-id="60b3b-108">如需特定步驟，請參閱[使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證](sql-database-aad-authentication-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="60b3b-108">For specific steps, see [Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication-configure.md).</span></span>  
- <span data-ttu-id="60b3b-109">啟用多因素驗證時，您必須在支援的工具，例如 hello 最新的 SSMS 連接使用。</span><span class="sxs-lookup"><span data-stu-id="60b3b-109">When multi-factor authentication is enabled, you must connect with at supported tool, such as hello latest SSMS.</span></span> <span data-ttu-id="60b3b-110">如需詳細資訊，請參閱[設定適用於 SQL Server Management Studio 的 Azure SQL Database 多重要素驗證](sql-database-ssms-mfa-authentication-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="60b3b-110">For more information, see [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).</span></span>  

## <a name="configure-ca-for-azure-sql-dbdw"></a><span data-ttu-id="60b3b-111">針對 Azure SQL DB/DW 設定 CA</span><span class="sxs-lookup"><span data-stu-id="60b3b-111">Configure CA for Azure SQL DB/DW</span></span>  
1.  <span data-ttu-id="60b3b-112">登入 toohello 入口網站中，選取**Azure Active Directory**，然後選取**條件式存取**。</span><span class="sxs-lookup"><span data-stu-id="60b3b-112">Sign in toohello Portal, select **Azure Active Directory**, and then select **Conditional access**.</span></span> <span data-ttu-id="60b3b-113">如需詳細資訊，請參閱 [Azure Active Directory 條件式存取的技術參考](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference)。</span><span class="sxs-lookup"><span data-stu-id="60b3b-113">For more information, see [Azure Active Directory Conditional Access technical reference](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).</span></span>  
  <span data-ttu-id="60b3b-114">![[條件式存取] 刀鋒視窗](./media/sql-database-conditional-access/conditional-access-blade.png)</span><span class="sxs-lookup"><span data-stu-id="60b3b-114">![conditional access blade](./media/sql-database-conditional-access/conditional-access-blade.png)</span></span> 
     
2.  <span data-ttu-id="60b3b-115">在 hello**條件式存取原則**刀鋒視窗中，按一下 **新原則**，提供名稱，然後按**設定規則**。</span><span class="sxs-lookup"><span data-stu-id="60b3b-115">In hello **Conditional Access-Policies** blade, click **New policy**, provide a name, and then click **Configure rules**.</span></span>  
3.  <span data-ttu-id="60b3b-116">在下**指派**，選取**使用者和群組**，檢查**選取使用者和群組**，然後選取 hello 使用者或群組的條件式存取。</span><span class="sxs-lookup"><span data-stu-id="60b3b-116">Under **Assignments**, select **Users and groups**, check **Select users and groups**, and then select hello user or group for conditional access.</span></span> <span data-ttu-id="60b3b-117">按一下**選取**，然後按一下**完成**tooaccept 選取項目。</span><span class="sxs-lookup"><span data-stu-id="60b3b-117">Click **Select**, and then click **Done** tooaccept your selection.</span></span>  
  <span data-ttu-id="60b3b-118">![選取 [使用者和群組]](./media/sql-database-conditional-access/select-users-and-groups.png)</span><span class="sxs-lookup"><span data-stu-id="60b3b-118">![select users and groups](./media/sql-database-conditional-access/select-users-and-groups.png)</span></span>  

4.  <span data-ttu-id="60b3b-119">選取 [雲端應用程式]，按一下 [選取應用程式]。</span><span class="sxs-lookup"><span data-stu-id="60b3b-119">Select **Cloud apps**, click **Select apps**.</span></span> <span data-ttu-id="60b3b-120">您會看到所有可供條件式存取使用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="60b3b-120">You see all apps available for conditional access.</span></span> <span data-ttu-id="60b3b-121">選取**Azure SQL Database**，hello 底部按一下**選取**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="60b3b-121">Select **Azure SQL Database**, at hello bottom click **Select**, and then click **Done**.</span></span>  
  <span data-ttu-id="60b3b-122">![選取 SQL Database](./media/sql-database-conditional-access/select-sql-database.png)</span><span class="sxs-lookup"><span data-stu-id="60b3b-122">![select SQL Database](./media/sql-database-conditional-access/select-sql-database.png)</span></span>  
  <span data-ttu-id="60b3b-123">如果找不到**Azure SQL Database** hello 遵循第三個螢幕擷取畫面中列出，請完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="60b3b-123">If you can’t find **Azure SQL Database** listed in hello following third screen shot, complete hello following steps:</span></span>   
  - <span data-ttu-id="60b3b-124">登入的 AAD 系統管理員帳戶使用 SSMS tooyour Azure SQL DB/DW 執行個體。</span><span class="sxs-lookup"><span data-stu-id="60b3b-124">Sign in tooyour Azure SQL DB/DW instance using SSMS with an AAD admin account.</span></span>  
  - <span data-ttu-id="60b3b-125">執行 `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`。</span><span class="sxs-lookup"><span data-stu-id="60b3b-125">Execute `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.</span></span>  
  - <span data-ttu-id="60b3b-126">登入 tooAAD，並確認 Azure SQL Database 和資料倉儲已列在 AAD 中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="60b3b-126">Sign in tooAAD and verify that Azure SQL Database and Data Warehouse are listed in hello applications in your AAD.</span></span>  

5.  <span data-ttu-id="60b3b-127">選取**存取控制項**，選取**Grant**，然後核取您想要 tooapply hello 原則。</span><span class="sxs-lookup"><span data-stu-id="60b3b-127">Select **Access controls**, select **Grant**, and then check hello policy you want tooapply.</span></span> <span data-ttu-id="60b3b-128">例如，我們選取 [需要多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="60b3b-128">For this example, we select **Require multi-factor authentication**.</span></span>  
  <span data-ttu-id="60b3b-129">![選取授與存取權](./media/sql-database-conditional-access/grant-access.png)</span><span class="sxs-lookup"><span data-stu-id="60b3b-129">![select grant access](./media/sql-database-conditional-access/grant-access.png)</span></span>  

## <a name="summary"></a><span data-ttu-id="60b3b-130">摘要</span><span class="sxs-lookup"><span data-stu-id="60b3b-130">Summary</span></span>  
<span data-ttu-id="60b3b-131">hello 選取應用程式 (Azure SQL Database) 允許 tooconnect tooAzure SQL DB/DW 使用 Azure AD Premium，現在會強制執行選取的 hello 條件式存取原則，**需要多重要素驗證。**</span><span class="sxs-lookup"><span data-stu-id="60b3b-131">hello selected application (Azure SQL Database) allowing tooconnect tooAzure SQL DB/DW using Azure AD Premium, now enforces hello selected Conditional Access policy, **Required multi-factor authentication.**</span></span>  
<span data-ttu-id="60b3b-132">若有關於多重要素驗證的 Azure SQL Database 和資料倉儲相關問題，請連絡 MFAforSQLDB@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="60b3b-132">For questions about Azure SQL Database and Data Warehouse regarding multi-factor authentication, contact MFAforSQLDB@microsoft.com.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="60b3b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60b3b-133">Next steps</span></span>  

<span data-ttu-id="60b3b-134">如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="60b3b-134">For a tutorial, see [Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>
