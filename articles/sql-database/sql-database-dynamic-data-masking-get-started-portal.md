---
title: "Azure 入口網站：SQL Database 動態資料遮罩 | Microsoft Docs"
description: "Tooget 與 SQL Database 動態資料遮罩 hello Azure 入口網站中啟動的方式"
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
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="75a80-103">開始使用 SQL Database 動態資料遮罩功能以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="75a80-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="75a80-104">本主題說明如何 tooimplement[動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)以 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="75a80-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="75a80-105">您也可以實作動態資料遮罩使用[Azure SQL Database cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx)或 hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx)。</span><span class="sxs-lookup"><span data-stu-id="75a80-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="75a80-106">設定動態資料遮罩的資料庫使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="75a80-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="75a80-107">啟動 hello Azure 入口網站則位於[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="75a80-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="75a80-108">瀏覽 toohello hello 資料庫，其中包含您想要 toomask hello 機密資料的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="75a80-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="75a80-109">按一下 hello**動態資料遮罩**磚可用來啟動 hello**動態資料遮罩**組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="75a80-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="75a80-110">或者，您可以向下捲動 toohello**作業**區段，然後按一下**動態資料遮罩**。</span><span class="sxs-lookup"><span data-stu-id="75a80-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![瀏覽窗格](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="75a80-112">在 hello**動態資料遮罩**組態刀鋒視窗，您可能會看到資料庫中的某些資料行，hello 建議引擎已標幟的遮罩。</span><span class="sxs-lookup"><span data-stu-id="75a80-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="75a80-113">若要 tooaccept hello 建議，只要按一下**新增遮罩**供一個或多個資料行和遮罩來建立根據 hello 這個資料行的預設類型。</span><span class="sxs-lookup"><span data-stu-id="75a80-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="75a80-114">您可以變更 hello hello 遮罩規則上按一下，然後編輯 hello 遮罩欄位格式 tooa 不同的格式您選擇的遮罩函數。</span><span class="sxs-lookup"><span data-stu-id="75a80-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="75a80-115">要確定 tooclick**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="75a80-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![瀏覽窗格](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="75a80-117">您在 hello hello 最上方的資料庫中任何資料行的遮罩 tooadd**動態資料遮罩**設定刀鋒視窗，請按一下**新增遮罩**tooopen hello**遮罩規則**設定刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="75a80-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![瀏覽窗格](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="75a80-119">選取 hello**結構描述**，**資料表**和**資料行**toodefine hello 指定的遮罩的欄位。</span><span class="sxs-lookup"><span data-stu-id="75a80-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="75a80-120">選擇**遮罩欄位格式**hello 清單中的機密資料遮罩類別。</span><span class="sxs-lookup"><span data-stu-id="75a80-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![瀏覽窗格](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="75a80-122">按一下**儲存**hello 資料遮罩規則刀鋒視窗 tooupdate hello 組遮罩 hello 動態資料遮罩原則中的規則中。</span><span class="sxs-lookup"><span data-stu-id="75a80-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="75a80-123">型別 hello SQL 的使用者或 AAD 身分識別，應該從遮罩排除，而且沒有存取 toohello 取消遮罩敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="75a80-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="75a80-124">這應該是以分號分隔的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="75a80-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="75a80-125">請注意，系統管理員權限的使用者一律存取 toohello 原始未遮罩的資料。</span><span class="sxs-lookup"><span data-stu-id="75a80-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![瀏覽窗格](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="75a80-127">toomake 它因此 hello 應用程式層級可以顯示為特殊權限的應用程式使用者的敏感性資料，請加入 hello SQL 使用者或 AAD 身分識別 hello 應用程式會使用 tooquery hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a80-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="75a80-128">強烈建議這份清單包含最少的權限的使用者 toominimize 公開 hello 機密資料。</span><span class="sxs-lookup"><span data-stu-id="75a80-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="75a80-129">按一下**儲存**hello 資料遮罩設定刀鋒視窗 toosave hello 新的或更新遮罩原則中。</span><span class="sxs-lookup"><span data-stu-id="75a80-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="75a80-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75a80-130">Next steps</span></span>

* <span data-ttu-id="75a80-131">如需動態資料遮罩的概觀，請參閱[動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="75a80-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="75a80-132">您也可以實作動態資料遮罩使用[Azure SQL Database cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx)或 hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx)。</span><span class="sxs-lookup"><span data-stu-id="75a80-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
