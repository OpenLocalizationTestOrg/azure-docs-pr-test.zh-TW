---
title: "Azure 入口網站：SQL Database 動態資料遮罩 | Microsoft Docs"
description: "如何開始在 Azure 入口網站中使用 SQL Database 動態資料遮罩"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="86b91-103">透過 Azure 入口網站開始使用 SQL Database 動態資料遮罩</span><span class="sxs-lookup"><span data-stu-id="86b91-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="86b91-104">本主題說明如何使用 Azure 入口網站來實作[動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="86b91-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="86b91-105">您也可以使用 [Azure SQL Database Cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 或 [REST API](https://msdn.microsoft.com/library/dn505719.aspx) 來實作動態資料遮罩。</span><span class="sxs-lookup"><span data-stu-id="86b91-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="86b91-106">使用 Azure 入口網站為您的資料庫設定動態資料遮罩</span><span class="sxs-lookup"><span data-stu-id="86b91-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="86b91-107">啟動 Azure 入口網站，位址是 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="86b91-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86b91-108">導覽至您要遮罩處理的敏感性資料所在資料庫的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86b91-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="86b91-109">按一下 [動態資料遮罩] 圖格，以啟動 [動態資料遮罩] 組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86b91-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="86b91-110">或者，您可以向下捲動至 [作業] 區段，然後按一下 [動態資料遮罩]。</span><span class="sxs-lookup"><span data-stu-id="86b91-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="86b91-112">在 [動態資料遮罩]  設定刀鋒視窗中，您可能會看到建議引擎已標示要進行遮罩處理的某些資料庫資料行。</span><span class="sxs-lookup"><span data-stu-id="86b91-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="86b91-113">若要接受建議，只要對一或多個資料行按一下 [新增遮罩]  ，就會根據此資料行的預設類型建立遮罩。</span><span class="sxs-lookup"><span data-stu-id="86b91-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="86b91-114">您可按一下遮罩規則並編輯遮罩欄位格式，使其成為您選擇的不同格式，即可變更遮罩函數。</span><span class="sxs-lookup"><span data-stu-id="86b91-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="86b91-115">務必按一下 [儲存]  以儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="86b91-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="86b91-117">若要為資料庫中的任何資料行新增遮罩，請在 [動態資料遮罩] 設定刀鋒視窗的頂端，按一下 [新增遮罩] 以開啟 [新增遮罩規則] 設定刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="86b91-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="86b91-119">請選取 [結構描述]、[資料表] 和 [資料行]，以定義將會遮罩處理的指定欄位。</span><span class="sxs-lookup"><span data-stu-id="86b91-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="86b91-120">從敏感性資料遮罩類別清單中，選擇 [遮罩欄位格式]  。</span><span class="sxs-lookup"><span data-stu-id="86b91-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="86b91-122">按一下資料遮罩規則刀鋒視窗中的 [儲存]  ，以更新動態遮罩原則中的遮罩資料規則集。</span><span class="sxs-lookup"><span data-stu-id="86b91-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="86b91-123">輸入應從遮罩處理中排除，並可存取未經遮罩處理之敏感性資料的 SQL 使用者或 AAD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="86b91-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="86b91-124">這應該是以分號分隔的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="86b91-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="86b91-125">請注意，具有系統管理員權限的使用者永遠都有未經遮罩處理之原始資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="86b91-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![導覽窗格](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="86b91-127">若要讓應用程式層級可以對具有特殊權限的應用程式使用者顯示敏感性資料，請新增應用程式用於查詢資料庫的 SQL 使用者或 ADD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="86b91-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="86b91-128">強烈建議此清單應包含最少的特殊權限使用者數目，以儘可能減少公開的敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="86b91-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="86b91-129">按一下資料遮罩組態刀鋒視窗中的 [儲存]  ，以儲存新的或更新的遮罩原則。</span><span class="sxs-lookup"><span data-stu-id="86b91-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="86b91-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86b91-130">Next steps</span></span>

* <span data-ttu-id="86b91-131">如需動態資料遮罩的概觀，請參閱[動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="86b91-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="86b91-132">您也可以使用 [Azure SQL Database Cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 或 [REST API](https://msdn.microsoft.com/library/dn505719.aspx) 來實作動態資料遮罩。</span><span class="sxs-lookup"><span data-stu-id="86b91-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>